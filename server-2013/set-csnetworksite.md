---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398295(v=OCS.15)
ms:contentKeyID: 49296485
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un site réseau existant qui a été défini pour le contrôle d’admission des appels (CAC) ou pour le système Enhanced 9-1-1 (E9-1-1). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans cet exemple, le site réseau appelé Vancouver est modifié. Le nom du site modifié est spécifié en tant que valeur du paramètre Identity. Le site de Vancouver est déplacé vers une nouvelle région, qui requiert la modification du paramètre NetworkRegionID, dans ce cas, la région nommée Canada. Parce que le paramètre NetworkRegionID a été fourni, mais qu’aucune valeur n’a été spécifiée pour le paramètre BypassID, une valeur sera automatiquement générée. Tout ID de dérivation précédemment existant sera remplacé.

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## EXEMPLE 2

L’exemple 2 illustre simplement le profil de stratégie de bande passante associé au site de Vancouver. Le nom de site est spécifié en tant que valeur du paramètre Identity. Nous spécifions ensuite une valeur pour le paramètre BWPolicyProfileID : LowBWLimits. Les stratégies associées à ce profil seront utilisées pour ce site.

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## Description détaillée

Les sites réseau sont les bureaux ou emplacements configurés au sein de chaque région d’un contrôle d’admission des appels (Call Admission Control ou CAC) ou encore d’un déploiement E9-1-1. Cette applet de commande modifie les paramètres sur un site existant. Ces derniers incluent notamment la région à laquelle le site est associé, la description du site et le profil de stratégie de bande passante associé.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkSite** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identité du profil de stratégie de bande passante qui définira les limitations pour ce site. Vous pouvez récupérer une liste des profils disponibles en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p>
<p>Si vous spécifiez une valeur pour ce paramètre, vous devez également saisir une valeur pour le paramètre NetworkRegionID.</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identificateur global unique (GUID). Ce GUID est utilisé pour mapper des sites réseau à des paramètres de déviation du trafic multimédia au sein d’une configuration réseau CAC ou E9-1-1 (Utilisez cette valeur BypassID au moment d’appeler l’applet de commande <strong>New-CsNetworkMediaBypassConfiguration</strong>).</p>
<p>Si vous spécifiez une valeur pour ce paramètre, vous devez également saisir une valeur pour le paramètre NetworkRegionID. Si vous spécifiez une valeur pour le paramètre NetworkRegionID mais pas pour ce paramètre, une valeur BypassID sera automatiquement générée.</p>
<p>Si vous spécifiez explicitement une valeur, elle doit être au format d’un GUID (par exemple : 3b24a047-dce6-48b2-9f20-9fbff17ed62a). Il est recommandé de saisir une valeur pour le paramètre NetworkRegionID et d’autoriser la génération automatique de la valeur BypassID. Si vous entrez une valeur manuellement, vous recevrez une invitation à confirmer que vous ne voulez pas que la valeur soit générée automatiquement.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Chaîne décrivant le site. Vous pouvez utiliser ce paramètre pour fournir une description plus explicite de l’objectif et de l’emplacement du site qui peut être exprimé par l’identité seule.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsqu’il est défini à True, le routage de la voix sera géré en prenant en compte l’emplacement de l’utilisateur qui passe l’appel et de l’utilisateur qui reçoit l’appel. La valeur par défaut est False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du site réseau que vous souhaitez modifier. Les sites étant uniquement créés dans l’étendue globale, il est inutile de spécifier une étendue. Il suffit de spécifier l’ID du site réseau.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>Référence à un objet de site réseau (objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType). Vous pouvez extraire cet objet en appelant l’applet de commande <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom de la stratégie d’emplacement associée à ce site. La stratégie d’emplacement assigne des paramètres E9-1-1 spécifiques au site. Vous pouvez récupérer une liste de stratégies d’emplacement en appelant l’applet de commande <strong>Get-CsLocationPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identité de la région réseau à laquelle ce site est associé. Ce paramètre doit contenir une valeur si vous souhaitez spécifier une valeur BypassID (soit via un processus de génération automatique, soit manuellement) ou si la propriété EnableBandwidthPolicyCheck de la configuration du réseau est True. Vous pouvez récupérer les paramètres de configuration du réseau en appelant l’applet de commande <strong>Get-CsNetworkConfiguration</strong>.</p>
<p>Si une valeur BypassID existe déjà sur ce site et que vous ne spécifiez aucune valeur pour le paramètre BypassID, il sera remplacé par un paramètre BypassID automatiquement généré.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Stratégie de routage de la voix par utilisateur à assigner au site. Exemple :</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>Notez que vous devez indiquer une stratégie par utilisateur, les stratégies globales et/ou de site ne peuvent pas être assignées à un site à l’aide du paramètre VoiceRoutingPolicy.</p>
<p>Ce paramètre est une nouveauté de la version de Lync Server 2013 de février 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Accepte l’entrée redirigée pour les objets de site réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

