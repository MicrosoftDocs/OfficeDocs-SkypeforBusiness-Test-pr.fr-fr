---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994044(v=OCS.15)
ms:contentKeyID: 53095450
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les clients Skype Entreprise Online configurés de manière à être utilisés dans votre organisation. Les clients représentent des groupes d’utilisateurs en ligne. Dans de nombreux cas, vous aurez peut-être besoin d’un seul client. Cependant, si d’autres groupes d’utilisateurs ont des besoins de gestion différents, Skype Entreprise Online fournit la prise en charge pour une organisation unique comportant plusieurs clients.

Get-CsTenant ne peut être utilisé qu’avec Skype Entreprise Online.

## Syntaxe

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 renvoie des informations sur tous les clients configurés de manière à être utilisés dans l’organisation.

    Get-CsTenant

## Exemple 2

Dans l’exemple 2, les informations sont renvoyées pour un seul client : le client avec l’identité « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## Exemple 3

La commande précédente présente une autre manière de renvoyer des informations pour un client unique. Dans cet exemple, cette opération est effectuée en incluant le paramètre Filter et la valeur de filtre {DisplayName –eq "Fabrikam"}. Cette syntaxe renvoie des informations uniquement pour le client dont le nom d’affichage est Fabrikam.

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## Exemple 4

La commande présentée dans l’exemple 4 renvoie des informations pour tous les clients dont le paramètre ServiceInstance est égal à « LitwareincCommunicationsOnline/San Antonio ». À cet effet, la commande inclut le paramètre Filter et la valeur de filtre {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}. Cette valeur de filtre limite les données renvoyées aux clients dont la propriété ServiceInstance est égale à (-eq) « LitwareincCommunicationsOnline/San Antonio ».

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## Exemple 5

L’exemple 5 renvoie des informations pour tous les clients dont le nom d’affichage du pays ou de la région est égal à « Australie ». Cette opération est effectuée en utilisant le paramètre Filter et la valeur de paramètre {CountryOrRegionDisplayName -eq "Australie"}.

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## Description détaillée

Dans Skype Entreprise Online, les clients représentent des groupes d’utilisateurs disposant de comptes hébergés sur le service. De nombreuses organisations n’ont besoin que d’un seul client dans lequel héberger tous leurs comptes d’utilisateur. Cependant, la gestion de Skype Entreprise Online est souvent effectuée pour chaque client. Cela signifie que tous les utilisateurs dans le même client possèdent la même stratégie de communication vocale, les mêmes paramètres de configuration de fédération, etc. Si vous avez besoin de gérer certains utilisateurs d’une façon et d’autres utilisateurs d’une autre façon, vous pouvez envisager d’utiliser plusieurs clients, chacun possédant sa propre collection de stratégies et de paramètres.

Indépendamment du nombre de clients utilisé, vous pouvez renvoyer des informations sur ces clients en utilisant l’applet de commande **Get-CsTenant**.

## Paramètres


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de renvoyer des données en utilisant les attributs Active Directory et sans avoir à spécifier le nom distinctif Active Directory complet. Par exemple, pour extraire un client en utilisant le nom d’affichage du client, utilisez une syntaxe comme celle-ci :</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>Pour renvoyer tous les clients qui utilisent un domaine Fabrikam, utilisez cette syntaxe :</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>Le paramètre Filter utilise la même syntaxe de filtrage Windows PowerShell que l’applet de commande Where-Object.</p>
<p>Vous ne pouvez pas utiliser les paramètres Identity et Filter dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Nom distinctif Active Directory du client. Par exemple :</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>Si vous n’incluez ni le paramètre Identity ni le paramètre Filter, l’applet de commande <strong>Get-CsTenant</strong> renvoie des informations sur tous vos clients.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>Permet de limiter le nombre d’enregistrements retournés par l’applet de commande. Par exemple, pour renvoyer sept clients (indépendamment du nombre de clients dans votre forêt), incluez le paramètre ResultSize et définissez sa valeur sur 7. Notez qu’il est impossible de savoir quels seront les sept utilisateurs renvoyés.</p>
<p>La taille des résultats peut être définie sur un entier compris entre 0 et 2147483647 (inclus). Si le paramètre est défini sur 0, la commande sera exécutée, mais aucune donnée ne sera renvoyée. Si vous définissez les clients sur 7, mais que vous n’avez que trois contacts dans votre forêt, la commande renverra ces trois clients, puis se terminera sans erreur.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

L’applet de commande **Get-CsTenant** accepte les instances redirigées de l’objet Microsoft.Rtc.Management.ADConnect.Schema.TenantObject, ainsi que les chaînes de valeur représentant la propriété Identity d’un client Skype Entreprise Online (par exemple, « OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com »).

## Types de retours

L’applet de commande **Get-CsTenant** renvoie des instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.TenantObject.

## Voir aussi

#### Autres ressources

[Get-CsOnlineUser](get-csonlineuser.md)

