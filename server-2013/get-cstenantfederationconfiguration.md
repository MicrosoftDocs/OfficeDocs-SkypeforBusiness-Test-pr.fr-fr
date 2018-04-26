---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994072(v=OCS.15)
ms:contentKeyID: 53095550
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les paramètres de configuration de la fédération pour vos clients Microsoft Lync Online. Les paramètres de configuration de la fédération sont utilisés pour déterminer les domaines (le cas échéant) avec lesquels vos utilisateurs sont autorisés à communiquer.

L’applet de commande **Get-CsTenantFederationConfiguration** peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## Exemples

## Exemple 1

La commande présentée dans l’exercice 1 renvoie les informations de configuration de la fédération pour le client avec l’ID client « bf19b7db-6960-41e5-a139-2aa373474354 ». Les ID client peuvent être extraits avec une commande similaire à celle-ci :

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Le paramètre Tenant est facultatif. Vous pouvez également appeler Get-CsTenantFederationConfiguration en utilisant cette syntaxe :

    Get-CsTenantFederationConfiguration

## Exemple 2

Dans l’exemple 2, les informations sont renvoyées pour tous les domaines trouvés dans la liste des domaines autorisés pour la fédération pour le client bf19b7db-6960-41e5-a139-2aa373474354. (La liste des domaines autorisés représente tous les domaines avec lesquels le client a l’autorisation d’être fédéré.) À cet effet, la commande appelle d’abord l’applet de commande **Get-CsTenantFederationConfiguration** pour renvoyer les informations de fédération pour le client spécifié. Ces informations sont ensuite redirigées vers l’applet de commande **Select-Object**, qui utilise la ExpandProperty pour « étendre » la propriété AllowedList. L’extension d’une propriété signifie simplement afficher à l’écran toutes les informations stockées dans cette propriété dans un format facile à lire.

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## Exemple 3

La commande précédente renvoie la configuration de la fédération pour tous les clients utilisés dans l’organisation. Pour effectuer cette tâche, la commande appelle d’abord l’applet de commande **Get-CsTenant** sans paramètre. Cette opération renvoie une collection de tous les clients disponibles. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object**. ForEach-Object utilise chaque client de la collection et appelle l’applet de commande **Get-CsTenantFederationConfiguration**, en utilisant la valeur de propriété TenantID (renvoyée par l’applet de commande **Get-CsTenant**) pour représenter l’ID client.

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## Exemple 4

Dans l’exemple 4, les informations de configuration de la fédération ne sont renvoyées que pour les clients qui n’autorisent pas les fédérations avec les utilisateurs publics. À cet effet, la commande appelle d’abord l’applet de commande **Get-CsTenant** sans paramètre afin de renvoyer une collection de tous les clients configurés de manière à être utilisés dans l’organisation. Cette collection est redirigée vers l’applet de commande **ForEach-Object**, qui utilise chaque client de la collection, puis utilise l’applet de commande **Get-CsTenantFederationConfiguration** pour renvoyer les informations de configuration de la fédération. L’ensemble d’informations sur la fédération est ensuite redirigé dans son intégralité vers l’applet de commande **Where-Object**, qui sélectionne uniquement les clients pour lesquels la propriété AllowPublicUsers est égale à (-eq) $False.

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## Description détaillée

La fédération est un service qui permet aux utilisateurs d’échanger des messages instantanés et des informations de présence avec les utilisateurs d'autres domaines. Lync Online permet aux administrateurs d’utiliser les paramètres de configuration de la fédération pour déterminer :

  - si les utilisateurs peuvent communiquer avec des personnes appartenant à d’autres domaines et, le cas échéant, les domaines avec lesquels ils peuvent communiquer.

  - si les utilisateurs peuvent communiquer avec des personnes ayant des comptes auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, AOL et Yahoo.

L’applet de commande **Get-CsTenantFederationConfiguration** permet aux administrateurs de renvoyer des informations de fédération pour leurs clients Lync Online. Cette applet de commande peut également être utilisée pour consulter les listes de domaines autorisés et bloqués, qui sont utilisées pour spécifier les domaines avec lesquels les utilisateurs peuvent communiquer ou non. Cependant, les administrateurs doivent utiliser l’applet de commande **Get-CsTenantPublicProvider** afin de voir les fournisseurs publics de messagerie instantanée et de présence avec lesquels les utilisateurs ont l’autorisation de communiquer.

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
<td><p>Permet d’utiliser des caractères génériques pour renvoyer une collection de paramètres de configuration de la fédération des clients. Comme chaque client est limité à une seule collection de paramètres de configuration de la fédération, il n’est pas nécessaire d’utiliser le paramètre Filter. Cependant, voici la syntaxe valide pour l’applet de commande <strong>Get-CsTenantFederationConfiguration</strong> :</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Spécifie la collection de paramètres de configuration de la fédération des clients à renvoyer. Comme chaque client est limité à une seule collection globale de paramètres de fédération, il n’est pas nécessaire d’inclure ce paramètre lorsque vous appelez l’applet de commande <strong>Get-CsTenantFederationConfiguration</strong>. Si vous choisissez d’utiliser le paramètre Identity, vous devez également inclure le paramètre Tenant. Par exemple :</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données de configuration de la fédération des clients à partir de la réplique locale du magasin de gestion centralisée, plutôt qu’à partir du magasin de gestion centralisée proprement dit.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID du compte de client dont les paramètres de fédération sont retournés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous utilisez une session à distance de Windows PowerShell et que vous êtes seulement connecté à Skype Entreprise Online, vous n’avez pas besoin d’inclure le paramètre Tenant. L’ID de client est renseigné automatiquement sur la base de vos informations de connexion. Le paramètre Tenant est principalement destiné à être utilisé dans un déploiement hybride.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsTenantFederationConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsTenantFederationConfiguration** renvoie des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Voir aussi

#### Autres ressources

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

