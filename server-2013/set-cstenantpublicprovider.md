---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994047(v=OCS.15)
ms:contentKeyID: 53095452
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Active et désactive la communication avec les fournisseurs de messagerie instantanée et de présence tiers, Windows Live, AOL et Yahoo. Lorsque la communication est activée, les utilisateurs de Microsoft Lync Online pourront échanger des messages instantanés et des informations de présence avec des utilisateurs possédant des comptes dans le fournisseur public spécifié.

L’applet de commande **Set-CsTenantPublicProvider** peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 permet la fédération avec Windows Live pour le client possédant l’ID client « bf19b7db-6960-41e5-a139-2aa373474354 ». Comme Windows Live est le seul fournisseur spécifié, les fournisseurs AOL et Yahoo seront désactivés une fois que la commande est exécutée.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## Exemple 2

Dans l’exemple 2, deux fournisseurs publics sont activés : Windows Live et AOL. Cela signifie que seul le fournisseur public Yahoo sera désactivé pour le client spécifié.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## Exemple 3

L’exemple 3 montre comment vous pouvez désactiver tous les fournisseurs publics pour un client donné. Cette opération est effectuée en définissant la propriété Provider sur une chaîne vide ("").

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## Exemple 4

La commande présentée dans l’exemple 4 désactive tous les fournisseurs publics pour tous vos clients Lync Online. Pour effectuer cette tâche, la commande utilise d’abord l’applet de commande **Get-CsTenant** pour renvoyer une collection de tous vos clients. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object**, qui utilise chaque client de la collection, appelle l’applet de commande **Set-CsTenantPublicProvider** pour chacun de ces clients et désactive les fournisseurs publics. La dernière tâche est effectuée en définissant la propriété Provider sur une chaîne vide ("").

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## Description détaillée

Les fournisseurs publics sont des organisations offrant des services de communication SIP au grand public. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous fédérez avec Windows Live, vos utilisateurs pourront échanger des messages instantanés et des informations de présence avec toute personne possédant un compte de messagerie instantanée Windows Live.

Lync Online permet aux administrateurs de configurer la fédération avec un ou plusieurs fournisseurs publics de messagerie instantanée et de présence :

  -   
    Windows Live

  -   
    AOL

  -   
    Yahoo\!

L’applet de commande **Set-CsTenantPublicProvider** peut être utilisée pour activer ou désactiver la fédération avec ces fournisseurs publics. Lorsque vous utilisez cette applet de commande, n’oubliez pas que chaque fois que vous exécutez l’applet de commande **Set-CsTenantPublicProvider**, vous devez spécifier tous les fournisseurs à activer. Par exemple, imaginez que les trois fournisseurs sont désactivés et que vous exécutez cette commande :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

Comme vous vous y attendez sans doute, cette opération va permettre de désactiver Windows Live et de conserver AOL et Yahoo.

À présent, imaginez que vous exécutez cette commande :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

Cette commande va activer AOL. Cependant, elle va également désactiver Windows Live : c’est parce que Windows Live n’a pas été spécifié dans la valeur de paramètre fournie pour le paramètre Provider. Si vous souhaitez activer AOL et maintenir Windows Live activé également, vous devez spécifier AOL et Windows Live lors de l’appel de Set-CsTenantPublicProvider :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Pour désactiver la fédération pour les trois fournisseurs, définissez la propriété Provider sur une chaîne vide ("") :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

Notez que si vous activez simplement le statut d’un fournisseur public, cela ne signifie pas que les utilisateurs peuvent échanger des messages instantanés et des informations de présence avec des utilisateurs disposant d’un compte chez ce fournisseur. Outre la possibilité de permettre la fédération avec le fournisseur proprement dit, les administrateurs doivent également définir la propriété AllowPublicUsers des paramètres de configuration de la fédération sur True. Si cette propriété est définie sur False, la communication ne sera autorisée avec aucun fournisseur public, indépendamment des paramètres de configuration des fournisseurs publics.

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
<td><p>System.Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte du client pour lequel les paramètres des fournisseurs publics sont modifiés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez renvoyer l’ID de client de chacun de vos clients en exécutant la commande suivante :</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String[]</p></td>
<td><p>Indique le fournisseur (ou les fournisseurs) public avec lequel les utilisateurs sont autorisés à communiquer. Les valeurs valides sont les suivantes :</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>Notez que, lorsque vous configurez des fournisseurs publics, les fournisseurs inclus dans la valeur de paramètre Provider sont activés pour être utilisés, alors que les fournisseurs non inclus dans la valeur de paramètre sont désactivés. Par exemple, cette syntaxe active uniquement Yahoo et désactive Windows Live et AOL :</p>
<p>-Provider &quot;AOL&quot;</p>
<p>Vous pouvez activer plusieurs fournisseurs en séparant le nom des fournisseurs par des virgules :</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

L’applet de commande **Set-CsTenantPublicProvider** accepte des instances redirigées de l’objet Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Set-CsTenantPublicProvider** modifie les instances existantes de l’objet Microsoft.Rtc.Management.Hosted.TenantPICStatus.

## Voir aussi

#### Autres ressources

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

