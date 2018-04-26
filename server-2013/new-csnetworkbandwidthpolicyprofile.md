---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398675(v=OCS.15)
ms:contentKeyID: 49297938
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée un profil de stratégie de bande passante réseau. Cette applet de commande peut être également utilisée pour définir des stratégies de bande passante au sein du profil. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 crée le profil de stratégie de bandes passante LowBWLimits. Deux stratégies seront affectées à ce nouveau profil : une stratégie audio et une stratégie vidéo (les deux seules stratégies possibles dans Lync Server). La stratégie audio est ajoutée au profil au moyen du paramètre AudioBWLimit pour affecter une limite de 2 000 Kbits/s (dans le cas présent) à toutes les connexions audio et au moyen du paramètre AudioBWSessionLimit pour définir 2 000 Kbits/s comme limite pour les sessions vidéo. La même opération est exécutée pour créer des limites de session vidéo, mais en utilisant les paramètres VideoBWLimit et VideoBWSessionLimit.

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## Description détaillée

La stratégie de bande passante utilisée dans le cadre du contrôle d’admission des appels (CAC) permet de définir des restrictions de bande passante pour des modes bien précis. (Dans Lync Server, seuls les modes audio et vidéo peuvent être soumis à des restrictions en matière de bande passante.) Cette applet de commande crée un profil pour ces stratégies au sein du conteneur. Vous définissez les stratégies individuelles dans le conteneur en indiquant les limites de bande passante audio et vidéo lorsque vous appelez cette applet de commande.

Les profils de stratégies de bande passante sont appliqués aux sites du réseau par l’applet de commande **New-CsNetworkSite** ou l’applet de commande **Set-CsNetworkSite**

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsNetworkBandwidthPolicyProfile** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Valeur de type chaîne qui identifie de manière unique la stratégie. Tous les profils de stratégies de bande passante sont créés au niveau de l’étendue globale. Par conséquent, l’étendue est implicite et seul un nom unique doit être défini lors de la création d’un profil de stratégie de bande passante. Notez que cette valeur est également affectée à la propriété BWPolicyProfileID du profil.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Quantité maximale de bande passante à allouer pour toutes les connexions audio. Si une seule session audio dépasse la limite de bande passante, cette session ne sera pas autorisée à démarrer.</p>
<p>Valeur exprimée en Kbits/s. Par exemple, une valeur de 1000 signifie 1 000 Kbits/s.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : si vous indiquez une valeur pour le paramètre AudioBWSessionLimit mais pas pour le paramètre AudioBWLimit, alors ce dernier prend la valeur 0 par défaut.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Largeur maximale de bande passante allouée par session audio. Valeur exprimée en Kbits/s. La valeur doit être égale ou supérieure à 40.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : si vous indiquez une valeur pour le paramètre AudioBWLimit mais pas pour le paramètre AudioBWSessionLimit, alors ce dernier prend la valeur 175 par défaut.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Liste d’objets contenant les profils de stratégie de bande passante. Chaque objet de la liste comprend un mode de bande passante (audio ou vidéo), une limite de bande passante et une limite pour la session de bande passante.</p>
<p>Si vous affectez une valeur à ce paramètre, vous ne pouvez pas affecter de valeur au paramètre AudioBWLimit, AudioBWSessionLimit, VideoBWLimit ou VideoBWSessionLimit.</p>
<p>Les objets de la liste peuvent être créés par l’applet de commande <strong>New-CsNetworkBWPolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Description du profil de stratégie de bande passante. Par exemple, vous pouvez utiliser ce paramètre pour clarifier l’utilisation du profil souhaité.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Quantité maximale de bande passante à allouer pour toutes les connexions vidéo. Si une seule session vidéo dépasse la limite de bande passante vidéo, cette session ne sera pas autorisée à démarrer.</p>
<p>Valeur exprimée en Kbits/s. Par exemple, une valeur de 1000 signifie 1 000 Kbits/s.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : si vous indiquez une valeur pour le paramètre VideoBWSessionLimit mais pas pour le paramètre VideoBWLimit, alors ce dernier prend la valeur 0 par défaut.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Largeur maximale de bande passante allouée par session vidéo. Valeur exprimée en Kbits/s. La valeur doit être égale ou supérieure à 100.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : si vous indiquez une valeur pour le paramètre VideoBWLimit mais pas pour le paramètre VideoBWSessionLimit, alors ce dernier prend la valeur 700 par défaut.</p></td>
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

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Voir aussi

#### Autres ressources

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

