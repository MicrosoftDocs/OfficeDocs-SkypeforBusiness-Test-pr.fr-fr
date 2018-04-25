---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425821(v=OCS.15)
ms:contentKeyID: 49296804
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime une collection existante de paramètres de configuration de la confidentialité. Les paramètres de configuration de la confidentialité aident à déterminer les informations que les utilisateurs mettent à la disposition d’autres utilisateurs. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 retourne les paramètres de configuration de la confidentialité attribués au site de Redmond. Lorsque ces paramètres sont supprimés, les utilisateurs du site de Redmond héritent automatiquement des paramètres de configuration de la confidentialité globaux.

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## EXEMPLE 2

Dans l’exemple 2, tous les paramètres de configuration de la confidentialité attribués au niveau de l’étendue Site sont supprimés. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsPrivacyConfiguration** avec le paramètre Filter ; la valeur de filtre « site:\* » assure que seuls les paramètres dont l’identité commence par la chaîne « site » sont retournés. La collection filtrée est alors redirigée vers l’applet de commande **Remove-CsPrivacyConfiguration** qui supprime chaque élément contenu dans la collection.

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## EXEMPLE 3

La commande illustrée dans l’exemple 3 supprime tous les paramètres de configuration de la confidentialité pour lesquels le mode de confidentialité est désactivé. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsPrivacyConfiguration** sans paramètre ; cet appel retourne une collection de tous les paramètres de configuration de la confidentialité utilisés dans l’organisation. Cette collection est alors redirigée vers l’applet de commande **Where-Object**, qui sélectionne uniquement les paramètres dont la propriété EnablePrivacyMode est égale à False. Cette collection filtrée est ensuite redirigée vers l’applet de commande **Remove-CsPrivacyConfiguration** qui supprime chaque élément dans la collection.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## Description détaillée

Lync Server donne aux utilisateurs la possibilité de partager un large éventail d’informations de présence avec d’autres personnes. Les utilisateurs peuvent publier une photographie d’eux-mêmes, donner des informations détaillées sur leur zone géographique et partager automatiquement des informations de présence avec toute l’organisation (plutôt qu’uniquement avec les personnes de leur liste de contacts).

Certains utilisateurs apprécieront de pouvoir partager ces informations avec leurs collègues ; d’autres seront plus réticents. (Par exemple, de nombreuses personnes peuvent hésiter à inclure leur photo à leurs informations de présence.) En règle générale, les utilisateurs décident des informations qu’ils partagent ou non. Par exemple, ils peuvent activer ou désactiver une case à cocher afin de partager ou non leurs informations d’emplacement. Les applets de commande de configuration de la confidentialité permettent aux administrateurs de gérer les paramètres de confidentialité de leurs utilisateurs. Dans certains cas, les administrateurs sont en mesure d’activer ou de désactiver les paramètres. Par exemple, si la propriété AutoInitiateContacts est configurée sur True, les membres de l’équipe sont ajoutés automatiquement à la liste de contacts de chaque utilisateur. Si elle est configurée sur False, les membres de l’équipe ne sont pas ajoutés automatiquement à la liste de contacts de chaque utilisateur.

Dans d’autres cas, les administrateurs peuvent configurer les valeurs par défaut dans Lync Server tout en donnant aux utilisateurs la possibilité de modifier ces valeurs. Par exemple, par défaut, les données de position géographique sont publiées pour les utilisateurs, mais ces derniers peuvent désactiver leur publication. En définissant la propriété PublishLocationDataByDefault sur False, les administrateurs peuvent modifier ce comportement : dans ce cas, les données de position géographique ne sont pas publiées par défaut, mais les utilisateurs peuvent activer leur publication s’ils le souhaitent.

Les paramètres de configuration de la confidentialité peuvent être appliqués au niveau de l’étendue globale, de l’étendue Site et de l’étendue Service (mais seulement pour le service User Server). L’applet de commande **Remove-CsPrivacyConfiguration** vous permet de supprimer des paramètres ayant été configurés au niveau de l’étendue Site ou Service ; par exemple, si vous exécutez l’applet de commande sur des paramètres configurés au niveau de l’étendue Site, ces paramètres seront supprimés et les utilisateurs verront leurs paramètres de confidentialité régis par la collection globale. L’applet de commande **Remove-CsPrivacyConfiguration** peut également être exécutée sur la collection globale, mais celle-ci n’est pas supprimée. Au lieu de cela, toutes les propriétés de cette collection sont réinitialisées sur leurs valeurs par défaut. Par exemple, supposons que vous ayez défini la propriété EnablePrivacyMode sur True. Si vous « supprimez » la collection globale, la propriété EnablePrivacyMode reprendra sa valeur par défaut : False.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsPrivacyConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique des paramètres de configuration de la confidentialité à supprimer. Pour supprimer les paramètres configurés au niveau de l’étendue Site, utilisez une syntaxe du type : -Identity site:Redmond. Pour supprimer les paramètres au niveau de l’étendue Service, utilisez une syntaxe du type : -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>L’applet de commande <strong>Remove-CsPrivacyConfiguration</strong> peut également être exécutée sur la collection globale de paramètres. Dans ce cas, toutefois, les paramètres globaux ne sont pas supprimés. Au lieu de cela, toutes les propriétés de cette collection sont réinitialisées sur leurs valeurs par défaut.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte client Skype Entreprise Online pour lequel les paramètres de configuration de la confidentialité sont supprimés. Exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration. L’applet de commande **Remove-CsPrivacyConfiguration** accepte les instances redirigées de l’objet de configuration de la confidentialité.

## Types de retours

Aucun. En fait, l’applet de commande **Remove-CsPrivacyConfiguration** supprime les instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

