---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398927(v=OCS.15)
ms:contentKeyID: 49298959
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les paramètres d’une configuration réseau. Cette applet de commande est le plus souvent utilisée pour activer ou désactiver le contrôle d’admission des appels (Call Admission Control ; CAC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de cet exemple exécutera un contrôle de validation sur l’ensemble de la configuration CAC, puis (en fonction de vos réponses aux avertissements retournés) activera CAC. Si CAC est déjà activé (en d’autres termes, si la propriété EnableBandwidthPolicyCheck a la valeur True) et que vous exécutez cette commande, elle exécutera simplement le contrôle de validation.

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## Description détaillée

L’objet de configuration réseau contient tous les paramètres d’une configuration CAC complète au sein d’un déploiement Lync Server, ainsi que les paramètres de déviation du trafic multimédia. Vous pouvez utiliser cette applet de commande pour modifier n’importe quelle partie de la configuration CAC et vous devez y recourir pour changer les paramètres de déviation du trafic multimédia. Néanmoins, il est recommandé d’utiliser des applets de commande spécifiques au type d’objet lorsque vous modifiez la plupart des paramètres de configuration CAC. Par exemple, pour travailler avec des régions réseau, utilisez les applets de commande se terminant par le nom CsNetworkRegion au lieu de manipuler le paramètre NetworkRegions de cette applet de commande.

Le principal rôle de cette applet de commande est d’activer (et de désactiver) CAC et d’appliquer des paramètres de déviation du trafic multimédia. Une fois que vous avez configuré les divers composants nécessaires à votre configuration (tels que régions, sites et sous-réseaux), vous devez activer la configuration pour permettre sa mise en œuvre. Pour ce faire, attribuez simplement la valeur True au paramètre EnableBandwidthPolicyCheck. Veuillez noter que même si EnableBandwidthPolicyCheck est défini sur True, l’exécution de cette applet de commande n’active pas immédiatement CAC. Avant de pouvoir activer CAC, une série de contrôles de validation doit être effectuée pour s’assurer que la configuration est correcte. Si des erreurs ou des incohérences sont détectées dans la configuration, des messages d’avertissement s’affichent, vous demandant si vous souhaitez continuer à activer CAC en dépit du problème rencontré. Si vous choisissez de continuer (en appuyant sur Entrée ou O), la validation se poursuit. Si un autre problème est détecté, vous devez à nouveau indiquer la marche à suivre.

Si vous effectuez l’intégralité de la validation en choisissant de continuer à chaque avertissement, la valeur True sera attribuée à EnableBandwidthPolicyCheck et CAC sera activé. Cependant, il ne fonctionnera probablement pas de façon correcte tant que les problèmes ne seront pas résolus. Si à n’importe quel stade de la validation, vous choisissez de l’interrompre (en saisissant N à l’invite d’avertissement), la validation prendra fin et EnableBandwidthPolicyCheck restera défini sur False (valeur par défaut).

Si EnableBandwidthPolicyCheck est déjà défini sur True, vous pouvez appeler l’applet de commande **Set-CsNetworkConfiguration** et attribuer la valeur True au paramètre EnableBandwidthPolicyCheck de façon à exécuter la validation sans modifier aucun paramètre. En outre, si EnableBandwidthPolicyCheck est défini sur True, toute modification que vous tentez d’effectuer en appelant l’applet de commande **Set-CsNetworkConfiguration** entraînera une nouvelle fois l’exécution du contrôle de validation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection de tous les profils de stratégie de bande passante qui peuvent être affectés aux sites, stratégies intersites et liens de région réseau. Chaque profil de stratégie de bande passante contient des limitations de bande passante (limitations globales et limitations de session) pour les connexions audio et/ou vidéo. Vous pouvez récupérer une liste complète des profils de stratégie de bande passante en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>En définissant ce paramètre sur True, vous exécutez un contrôle de validation sur l’intégralité de la configuration CAC. Si tous les contrôles de validation sont réussis ou si vous choisissez d’ignorer l’ensemble des avertissements, CAC sera activé. Si un contrôle de validation échoue, vous pouvez choisir d’arrêter la validation et la valeur de EnableBandwidthPolicyCheck restera inchangée. Des itinéraires de région doivent être définis entre chaque paire de régions réseau avant de pouvoir exécuter la vérification de la validation.</p>
<p>En définissant cette valeur sur False, vous désactivez CAC.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Ce paramètre n’accepte aucune valeur. Si vous incluez ce paramètre, toute modification apportée à la configuration, y compris son activation, sera appliquée sans aucun avertissement ou contrôle de validation.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Cette valeur est toujours Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>Référence à un objet de configuration réseau. Cet objet doit être de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings et peut être récupéré en appelant l’applet de commande <strong>Get-CsNetworkConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection de tous les itinéraires de région réseau définis dans la configuration CAC. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection de stratégies inter-sites réseau définies dans la configuration CAC. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>Facultatif</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>Référence à un objet qui définit les paramètres globaux de déviation du trafic multimédia pour la configuration CAC. Si vous définissez cette valeur, le système remplacera tous les paramètres existants de déviation du trafic multimédia. Pour obtenir cette référence d’objet, appelez l’applet de commande <strong>New-CsNetworkMediaBypassConfiguration</strong> et affectez les nouveaux paramètres de configuration à une variable. Transmettez ensuite cette variable au paramètre MediaBypassSettings afin de modifier les paramètres globaux de déviation du trafic multimédia.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection des liens de région réseau définis dans la configuration CAC. Chaque lien de région réseau définit une connexion entre deux régions et toutes les limitations de bande passante qui doivent être appliquées aux connexions entre ces régions. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection des régions réseau (chacune d’entre elles représentant un concentrateur ou une dorsale principale dans le réseau) définies dans la configuration CAC. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection des sites réseau (chacun d’entre eux représentant un bureau ou un emplacement dans une région) définis dans la configuration CAC. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection des sous-réseaux de réseau (chacun d’entre eux étant associé par un point de terminaison à un site) définis dans la configuration CAC. Vous pouvez récupérer tous les membres de cette collection en appelant l’applet de commande <strong>Get-CsNetworkSubnet</strong>.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings. Accepte l’entrée redirigée pour un objet de configuration de réseau.

## Types de retours

L’applet de commande **Set-CsNetworkConfiguration** ne renvoie ni valeur, ni objet. Au lieu de cela, l’applet de commande modifie les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Voir aussi

#### Autres ressources

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

