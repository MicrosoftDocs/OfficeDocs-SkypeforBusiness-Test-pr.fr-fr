---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994016(v=OCS.15)
ms:contentKeyID: 53095357
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations indiquant si les utilisateurs de Microsoft Lync Online ont l’autorisation de communiquer avec des personnes possédant des comptes chez les fournisseurs de messagerie instantanée et de présence tiers Windows Live, AOL et Yahoo.

Cette applet de commande peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 renvoie des informations sur les fournisseurs publics pour le client possédant l’ID client « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Le paramètre Tenant est facultatif. Vous pouvez également appeler Get-CsTenantPublicProvider en utilisant cette syntaxe :

    Get-CsTenantPublicProvider

## Exemple 2

La commande précédente renvoie des informations détaillées sur le statut de tous les fournisseurs publics affectés au client bf19b7db-6960-41e5-a139-2aa373474354. À cet effet, la commande utilise d’abord l’applet de commande **Get-CsTenantPublicProvider** pour renvoyer des informations sur les fournisseurs publics pour le client spécifié. Ces informations sont ensuite redirigées vers l’applet de commande **Select-Object**, qui utilise le paramètre ExpandProperty pour « étendre » la valeur de la propriété DomainPICStatus. L’extension d’une propriété signifie simplement que toutes les valeurs stockées dans cette propriété sont affichées à l’écran dans un format facile à lire.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Une commande comme celle-ci serait utilisée dans un déploiement hybride de Lync Server 2013.

## Exemple 3

La commande présentée dans l’exemple 3 est une variante de la commande de l’exemple 2. Dans l’exemple 3, cependant, les informations sur les fournisseurs publics renvoyées en « étendant » la valeur de la propriété DomainPICStatus sont ensuite redirigées vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** sélectionne ensuite les fournisseurs dans lesquels la propriété Status est définie sur Enabled. L’effet net est de n’afficher que les fournisseurs publics activés pour être utilisés.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## Description détaillée

Les fournisseurs publics sont des organisations offrant des services de communication SIP au grand public. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous définissez une fédération avec Windows Live, vos utilisateurs peuvent échanger des messages instantanés et des informations de présence avec toute personne disposant d’un compte de messagerie instantanée Windows Live.

Lync Online permet aux administrateurs de configurer la fédération avec un ou plusieurs fournisseurs publics de messagerie instantanée et de présence :

  - Windows Live

  - AOL

  - Yahoo\!

Les administrateurs peuvent utiliser l’applet de commande **Get-CsTenantPublicProvider** pour déterminer lequel de ces fournisseurs (le cas échéant) a été activé pour la fédération. Lorsque vous appelez l’applet de commande **Get-CsTenantPublicProvider**, vous récupérez des informations similaires à celles-ci :

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

La propriété PublicProviderSet indique si la fédération a été activée ou non pour un ou plusieurs fournisseurs publics. Si PublicProviderSet est définie sur True, la fédération a été activée avec au moins un fournisseur. Si PublicProviderSet est définie sur False, la fédération a été désactivée pour les trois fournisseurs publics (Windows Live, AOL et Yahoo). Pour déterminer le statut réel de chaque fournisseur, utilisez cette commande :

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Notez que si vous activez simplement le statut d’un fournisseur public, cela ne signifie pas que les utilisateurs peuvent échanger des messages instantanés et des informations de présence avec des utilisateurs disposant d’un compte chez ce fournisseur. Outre la possibilité de permettre la fédération avec le fournisseur proprement dit, les administrateurs doivent également définir la propriété AllowPublicUsers des paramètres de configuration de la fédération sur True. Si cette propriété est définie sur False, la communication ne sera autorisée avec aucun fournisseur public, indépendamment des paramètres de configuration des fournisseurs publics.

Pour plus d’informations, voir la rubrique d’aide sur l’applet de commande **Set-CsTenantFederationConfiguration**.

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
<td><p><em>Tenant</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Identificateur global unique (GUID) du compte du client dont les paramètres de fournisseur public sont renvoyés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous utilisez une session à distance de Windows PowerShell et que vous êtes seulement connecté à Skype Entreprise Online, vous n’avez pas besoin d’inclure le paramètre Tenant. L’ID de client est renseigné automatiquement sur la base de vos informations de connexion. Le paramètre Tenant est principalement destiné à être utilisé dans un déploiement hybride.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsTenantPublicProvider** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsTenantPublicProvider** renvoie des instances de l’objet Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Voir aussi

#### Autres ressources

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

