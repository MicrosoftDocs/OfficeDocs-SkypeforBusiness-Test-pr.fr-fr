---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398807(v=OCS.15)
ms:contentKeyID: 49298336
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une nouvelle collection de paramètres de configuration de la confidentialité. Les paramètres de configuration de la confidentialité contribuent à déterminer les informations que les utilisateurs peuvent accepter de partager avec d’autres utilisateurs. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 crée une nouvelle collection de paramètres de configuration de la confidentialité qui seront appliqués au site Redmond (-Identity site:Redmond). Les nouveaux paramètres activent le mode de confidentialité. Pour cela, le paramètre EnablePrivacyMode est ajouté et sa valeur est définie sur True. Notez que cette commande échouera si le site Redmond dispose déjà d’une collection de paramètres de confidentialité.

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## EXEMPLE 2

L’exemple 2 explique comment utiliser le paramètre InMemory pour créer une collection de paramètres de configuration de la confidentialité qui n’existent au départ que dans la mémoire. Pour ce faire, l’applet de commande **New-CsPrivacyConfiguration** est appelée avec les paramètres Identity et InMemory. L’objet qui en résulte est stocké dans la variable $x. À ce stade, les paramètres de confidentialité n’existent que dans la mémoire. Si vous exécutez l’applet de commande **Get-CsPrivacyConfiguration**, vous ne verrez pas de liste pour site:Redmond.

Dans le second exemple, la valeur de la propriété EnablePrivacyMode est définie sur True. Enfin, la troisième commande utilise l’applet de commande **Set-CsPrivacyConfiguration** pour transformer cette collection virtuelle de paramètres de confidentialité en une collection réelle de paramètres appliqués au site Redmond. L’appel de l’applet de commande **Set-CsPrivacyConfiguration** est indispensable : si vous échouez dans l’appel de cette applet de commande, vos nouveaux paramètres de confidentialité ne seront jamais appliqués au site Redmond et disparaîtront dès la fin de votre session Windows PowerShell ou lorsque vous supprimerez la variable $x.

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## Description détaillée

Lync Server donne aux utilisateurs la possibilité de partager un large éventail d’informations de présence avec d’autres personnes. Les utilisateurs peuvent publier une photographie d’eux-mêmes, donner des informations détaillées sur leur zone géographique et partager automatiquement des informations de présence avec toute l’organisation (plutôt qu’avec les personnes de leur liste de contacts uniquement).

Certains utilisateurs apprécieront de pouvoir partager ces informations avec leurs collègues ; d’autres seront plus réticents. (Par exemple, de nombreuses personnes peuvent hésiter à inclure leur photo à leurs informations de présence.) En règle générale, les utilisateurs décident des informations qu’ils partagent ou non. Par exemple, ils peuvent activer ou désactiver une case à cocher afin de partager ou non leurs informations d’emplacement. Les applets de commande de configuration de la confidentialité permettent aux administrateurs de gérer les paramètres de confidentialité de leurs utilisateurs. Dans certains cas, les administrateurs sont en mesure d’activer ou de désactiver les paramètres ; par exemple, si la propriété AutoInitiateContacts est configurée sur True, les membres de l’équipe sont ajoutés automatiquement à la liste de contacts de chaque utilisateur. Si elle est configurée sur False, les membres de l’équipe ne sont pas ajoutés automatiquement à la liste de contacts de chaque utilisateur.

Dans d’autres cas, les administrateurs peuvent configurer les valeurs par défaut dans Lync tout en donnant aux utilisateurs la possibilité de modifier ces valeurs. Par exemple, les données d’emplacement sont par défaut publiées pour chaque utilisateur, mais ces derniers ont le droit d’en arrêter la publication. En définissant la propriété PublishLocationDataByDefault sur False, les administrateurs peuvent changer ce comportement : dans ce cas, les données d’emplacement ne seront pas publiées par défaut, mais les utilisateurs pourront toujours les publier s’ils le souhaitent.

Les paramètres de configuration de la confidentialité peuvent être appliqués au niveau de l’étendue globale, de l’étendue Site et de l’étendue Service (pour le service User Server uniquement). L’applet de commande **New-CsPrivacyConfiguration** permet de créer de nouveaux paramètres de configuration de la confidentialité qui seront appliqués au site ou au service. (Les nouvelles collections ne peuvent pas être créées au niveau de l’étendue globale.) Notez que chaque site ou service individuel peut avoir au maximum une seule collection de paramètres de configuration de la confidentialité : si vous essayez de créer une nouvelle collection pour le site Redmond alors qu’il a déjà une, votre commande échoue.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsPrivacyConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p>Identificateur unique des paramètres de configuration de la confidentialité à créer. Pour créer une nouvelle collection de paramètres au niveau de l’étendue Site, utilisez une syntaxe similaire à celle-ci : -Identity site:Redmond. Pour créer des nouveaux paramètres au niveau de l’étendue Service, utilisez une syntaxe comparable à celle-ci : -Identity service:UserServer:atl-cs-001.litwareinc.com. Les paramètres de confidentialité ne peuvent être créés que pour le service User Server. Une erreur se produit si vous tentez d’appliquer ces paramètres à un autre service.</p>
<p>Notez que votre commande échouera si les paramètres de configuration de la confidentialité existent déjà pour le site ou le service spécifié. De même, votre commande échouera si vous tentez de créer une nouvelle collection de paramètres globaux.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, Lync ajoute automatiquement l’ensemble des contacts de votre responsable, ainsi que vos contacts directs à votre liste de contacts. La valeur par défaut est True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, la photo de l’utilisateur est automatiquement publiée dans Lync. Lorsqu’il est défini sur False, la photo de l’utilisateur ne sera pas visible, à moins qu’il ne sélectionne explicitement l’option Autoriser d’autres personnes à voir ma photo. La valeur par défaut est True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, les utilisateurs ont la possibilité d’activer le mode avancé de confidentialité. En mode avancé de confidentialité, seules les personnes de votre liste de contacts seront autorisées à visualiser vos informations de présence. Lorsqu’il est défini sur False, vos informations de présence seront visibles par tous les tiers de votre organisation. La valeur par défaut est False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, les données d’emplacement sont automatiquement publiées dans Lync. Lorsqu’il est défini sur False, les données d’emplacement ne seront pas visibles, à moins que l’utilisateur ne sélectionne explicitement l’option Afficher Mon emplacement aux contacts. La valeur par défaut est True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte du client Skype Entreprise Online pour lequel les paramètres de configuration de confidentialité sont créés. Exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Aucun. L’applet de commande **New-CsPrivacyConfiguration** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **New-CsPrivacyConfiguration** crée de nouvelles instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

