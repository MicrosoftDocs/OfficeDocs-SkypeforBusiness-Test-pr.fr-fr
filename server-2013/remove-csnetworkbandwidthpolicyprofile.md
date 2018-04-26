---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398609(v=OCS.15)
ms:contentKeyID: 49297821
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un profil de stratégie de bande passante du réseau. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple supprime le profil de stratégie de bande passante avec l’identité LowBWProfile. Puisque les identités sont uniques, cette commande supprime au maximum un profil.

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## EXEMPLE 2

L’exemple 2 supprime de tous les sites toutes les références au profil de stratégie de bande passante auquel l’identité LowBWProfile a été affectée, puis supprime ce profil. La première ligne de cet exemple commence par appeler l’applet de commande **Get-CsNetworkSite** pour récupérer tous les sites configurés pour le contrôle d’admission des appels (CAC). Cette collection de sites est ensuite redirigée vers l’applet de commande **Where-Object** qui ne recherche que les sites avec une identité BWPolicyProfileID égale à (-eq) LowBWProfile. Cette collection filtrée qui ne contient que les sites avec une valeur BWPolicyProfileID définie sur LowBWProfile est redirigée vers l’applet de commande **Set-CSNetworkSite** qui modifie chacun de ces sites pour modifier la valeur BWPolicyProfileID en lui donnant la valeur Null ($null). Ce que nous venons de faire consiste à trouver tous les sites avec une identité BWPolicyProfileID définie sur LowBWProfile et définir cette valeur sur Null. À ce stade, aucun site n’utilise le profil LowBWProfile, À présent, appelons l’applet de commande **Remove-CsNetworkBandwidthPolicyProfile** sur le profil LowBWProfile afin de le supprimer, en sachant que ce profil n’est utilisé par aucun site.

Pour vérifier que ce profil n’est pas utilisé dans la configuration réseau, exécutez les étapes de la ligne 1 sur les stratégies intersites et les liens de région réseau.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## Description détaillée

La stratégie de bande passante utilisée dans le cadre du contrôle d’admission des appels (CAC) permet de définir des restrictions de bande passante pour des modes bien précis. (Dans Lync Server, seuls les modes audio et vidéo peuvent être soumis à des restrictions en matière de bande passante.) Cette applet de commande supprime un profil pour ces stratégies au sein du conteneur.

IMPORTANT : si un profil a été affecté à un site (à l’aide de l’applet de commande **New-CsNetworkSite** ou de l’applet de commande **Set-CsNetworkSite**), à une stratégie intersite (à l’aide de l’applet de commande **New-CsNetworkInterSitePolicy** ou de l’applet de commande **Set-CsNetworkInterSitePolicy**) ou à un lien de région réseau (à l’aide de l’applet de commande **New-CsNetworkRegionLink** ou de l’applet de commande **Set-CsNetworkRegionLink**), il ne peut pas être supprimé. Vous recevrez une erreur si vous essayez de supprimer le profil en appelant l’applet de commande **Remove-CsNetworkBandwidthPolicyProfile**. Vous devez d’abord supprimer le profil de tous les sites, stratégies intersites et liens de région réseau pour pouvoir supprimer le profil.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkBandwidthPolicyProfile** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Cette valeur de chaîne identifie de manière unique le profil de stratégie de bande passante que vous voulez supprimer. Spécifier une identité supprimera, au maximum, un seul profil.</p></td>
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
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Accepte la saisie de données des objets de profil de stratégie de bande passante réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Voir aussi

#### Autres ressources

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

