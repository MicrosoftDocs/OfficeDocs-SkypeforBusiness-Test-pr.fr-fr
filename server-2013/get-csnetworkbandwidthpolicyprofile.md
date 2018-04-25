---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425815(v=OCS.15)
ms:contentKeyID: 49296794
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**Dernière rubrique modifiée :** 2015-03-09_

Extrait un ou plusieurs profils de stratégie de bande passante réseau. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’appel de l’applet de commande **Get-CsNetworkBandwidthPolicyProfile** sans paramètre récupère tous les profils de stratégies de bande passante définis dans le déploiement de Lync Server.

    Get-CsNetworkBandwidthPolicyProfile

## EXEMPLE 2

Cet exemple récupère le profil de stratégie de bande passante dont la propriété Identity est LowBWProfile. Étant donné que les identités doivent être uniques, cet exemple retourne, au plus, un profil.

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## EXEMPLE 3

Dans cet exemple, nous utilisons le paramètre Filter pour spécifier un ou plusieurs profils à récupérer d’après une chaîne à caractères génériques. Nous avons utilisé la chaîne \*50MB\*, qui indique que nous souhaitons récupérer tous les profils de stratégies de bande passante dont la valeur de la propriété Identity contient la chaîne 50MB quelque part. Par exemple, les profils dont l’identité est « BW profile for 50MB links », « 50MB audio limit » et « video limits of 50MB » seraient retournés.

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## Description détaillée

Dans le cadre du contrôle d’admission des appels, une stratégie de bande passante est utilisée pour définir les limites de bande passante pour certaines modalités. (Dans Lync Server, seuls les modes audio et vidéo peuvent être soumis à des restrictions en matière de bande passante). Cette applet de commande extrait un ou plusieurs profils de conteneurs pour ces stratégies.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkBandwidthPolicyProfile** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Chaîne contenant des caractères génériques, utilisée pour récupérer les profils de stratégies de bande passante dont la valeur de la propriété Identity correspond au modèle de caractères génériques.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Valeur de chaîne qui identifie de façon unique le profil de stratégie de bande passante à récupérer. Le fait de spécifier une propriété Identity récupèrera, au plus, un profil.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère le profil de stratégie de bande passante réseau à partir de la réplique locale du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Retourne un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Voir aussi

#### Autres ressources

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

