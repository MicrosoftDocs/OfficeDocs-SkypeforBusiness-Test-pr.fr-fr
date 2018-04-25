---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994080(v=OCS.15)
ms:contentKeyID: 53095544
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Gère les paramètres de configuration de la fédération pour vos clients Microsoft Lync Online. Ces paramètres permettent de déterminer les domaines (le cas échéant) avec lesquels vos utilisateurs sont autorisés à communiquer.

L’applet de commande **Set-CsTenantFederationConfiguration** peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 désactive la communication avec les fournisseurs publics pour le client associé au TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

Le paramètre Tenant est facultatif. Si vous conservez ce paramètre, Windows PowerShell insère automatiquement l’ID de client correct sur la base de vos informations de connexion.

## Exemple 2

L’exemple 2 montre comment désactiver la communication des fournisseurs publics pour tous les clients dans votre organisation. Pour ce faire, la commande commence par appeler l’applet de commande **Get-CsTenant** pour retourner une collection des clients disponibles. Cette collection est ensuite redirigée vers l’applet de commande **Select-Object**, laquelle récupère la seule propriété TenantId pour chaque élément dans la collection. Cette collection d’ID de client est ensuite redirigée vers l’applet de commande **ForEach-Object**. L’applet de commande F**orEach-Object** récupère ensuite chaque ID de client, exécute l’applet de commande **Set-CsTenantFederationConfiguration** sur cet ID et définit la propriété AllowPublicUsers de chaque client sur False ($False).

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## Exemple 3

Dans l’exemple 3, le domaine fabrikam.com est affecté comme seul domaine de la liste des domaines bloqués pour le client associé au TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ». Pour ce faire, la première commande dans l’exemple utilise l’applet de commande **New-CsEdgeDomainPattern** pour créer un objet domaine pour fabrikam.com. Cet objet domaine est stocké dans une variable nommée $x.

La deuxième commande dans l’exemple utilise ensuite l’applet de commande **Set-CsTenantFederationConfiguration** pour mettre à jour la liste des domaines bloqués. L’utilisation de la méthode Replace garantit que la liste des domaines bloqués existante sera remplacée par la nouvelle liste : une liste qui contient uniquement le domaine fabrikam.com.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## Exemple 4

Les commandes de l’exemple 4 suppriment fabrikam.com de la liste des domaines bloqués par le client associé au TenantID « bf19b7db-6960-41e5-a139-2aa373474354 ». Pour ce faire, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeDomainPattern** pour créer un objet domaine pour fabrikam.com. L’objet domaine résultant est ensuite stocké dans une variable nommée $x.

La deuxième commande de l’exemple utilise ensuite l’applet de commande **Set-CsTenantFederationConfiguration** et la méthode Remove pour supprimer fabrikam.com de la liste des domaines bloqués pour le client spécifié.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## Exemple 5

Les commandes de l’exemple 5 ajoutent le domaine fabrikam.com à la liste des domaines bloqués par le client associé au TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ». Pour ajouter un nouveau domaine bloqué, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeDomainPattern** pour créer un objet domaine pour fabrikam.com. Cet objet est stocké dans une variable nommée $x.

Une fois l’objet domaine créé, la deuxième commande utilise l’applet de commande **Set-CsTenantFederationConfiguration** et la méthode Add pour ajouter fabrikam.com aux domaines figurant déjà dans la liste des domaines bloqués.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## Exemple 6

L’exemple 6 montre comment supprimer tous les domaines affectés à la liste des domaines bloqués pour un client donné. Pour ce faire, incluez simplement le paramètre BlockedDomains, et définissez la valeur de paramètre sur null ($Null). Une fois la commande exécutée, la liste des domaines bloqués est effacée pour le client associé au TenantID « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## Description détaillée

La fédération est un service qui permet aux utilisateurs d’échanger des messages instantanés et des informations de présence avec les utilisateurs d’autres domaines. Lync Online permet aux administrateurs d’utiliser les paramètres de configuration de la fédération pour déterminer :

  -   
    si les utilisateurs peuvent communiquer avec des personnes appartenant à d’autres domaines et, le cas échéant, les domaines avec lesquels ils peuvent communiquer.

  -   
    si les utilisateurs peuvent communiquer avec des personnes ayant des comptes auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, AOL et Yahoo.

Les administrateurs peuvent utiliser l’applet de commande **Set-CsTenantFederationConfiguration** pour activer et désactiver la fédération avec d’autres domaines et la fédération avec des fournisseurs publics. Par ailleurs, cette applet de commande peut être utilisée pour indiquer expressément les domaines avec lesquels les utilisateurs peuvent communiquer et/ou les domaines avec lesquels les utilisateurs ne sont pas autorisés à communiquer. Les administrateurs doivent toutefois utiliser l’applet de commande **Set-CsTenantPublicProvider** pour spécifier les fournisseurs publics de messagerie instantanée et de présence avec lesquels les utilisateurs ne peuvent pas communiquer.

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>Objets domaine (créés à l’aide de l’applet de commande <strong>New-CsEdgeAllowList</strong> ou <strong>New-CsEdgeAllowAllKnownDomains</strong>) qui représentent les domaines avec lesquels les utilisateurs peuvent communiquer. Si l’applet de commande <strong>New-CsEdgeAllowAllKnownDomains</strong> est utilisée, les utilisateurs peuvent communiquer avec n’importe quel domaine ne figurant pas dans la liste des domaines bloqués. Si l’applet de commande <strong>New-CsEdgeAllowList</strong> est utilisée, les utilisateurs peuvent seulement communiquer avec les domaines qui ont été ajoutés à la liste des domaines autorisés.</p>
<p>Notez que des valeurs de chaîne ne peuvent pas être transmises directement au paramètre AllowedDomains. Vous devez créer une référence d’objet à l’aide de l’applet de commande <strong>New-CsEdgeAllowList</strong> ou <strong>New-CsEdgeAllowAllKnownDomains</strong>, puis utiliser la variable de référence d’objet comme valeur de paramètre.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True (valeur par défaut), les utilisateurs pourront éventuellement communiquer avec les utilisateurs des autres domaines. Si cette propriété est définie sur False, les utilisateurs ne peuvent pas communiquer avec les utilisateurs des autres domaines, quelles que soient les valeurs affectées aux propriétés AllowedDomains et BlockedDomains.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True (valeur par défaut), les utilisateurs pourront éventuellement communiquer avec les utilisateurs dont le compte est hébergé auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, Yahoo, et AOL. La collection de fournisseurs publics avec lesquels les utilisateurs peuvent effectivement communiquer est gérée à l’aide de l’applet de commande Set-CsTenantPublicProvider.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si la propriété AllowedDomains a été définie sur AllowAllKnownDomains, les utilisateurs seront autorisés à communiquer avec les utilisateurs appartenant à d’autres domaines, à l’exception des domaines qui apparaissent dans la liste des domaines bloqués. Si la propriété AllowedDomains n’a pas été définie sur AllowAllKnownDomains, la liste des domaines bloqués est ignorée, et les utilisateurs peuvent seulement communiquer avec les domaines expressément ajoutés à la liste des domaines autorisés.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Spécifie la collection de paramètres de configuration de la fédération de client devant être modifiés. Comme chaque client est limité à une seule collection globale de paramètres de fédération, il n’est pas utile d’inclure ce paramètre lorsque vous appelez l’applet de commande <strong>Set-CsTenantFederationConfiguration</strong>. Si vous choisissez d’utiliser le paramètre Identity, vous devez également inclure le paramètre Tenant. Par exemple :</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Permet de transmettre une référence à un objet à l’applet de commande plutôt que de définir des valeurs de paramètre individuelles.</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, indique que les utilisateurs hébergés sur Lync Online utilisent le même domaine SIP que ceux hébergés sur la version locale de Lync Server. La valeur par défaut est False, ce qui signifie que les deux ensembles d’utilisateurs ont des domaines SIP différents.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID du compte de client dont les paramètres de fédération sont modifiés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous utilisez une session à distance de Windows PowerShell et que vous êtes seulement connecté à Skype Entreprise Online, vous n’avez pas besoin d’inclure le paramètre Tenant. L’ID de client est renseigné automatiquement sur la base de vos informations de connexion. Le paramètre Tenant est principalement destiné à être utilisé dans un déploiement hybride.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

L’applet de commande **Set-CsTenantFederationConfiguration** accepte les instances redirigées de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Types de retours

Aucun. L’applet de commande **Set-CsTenantFederationConfiguration** modifie à la place les instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings.

## Voir aussi

#### Autres ressources

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

