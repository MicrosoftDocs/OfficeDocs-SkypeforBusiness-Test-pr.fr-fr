---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425718(v=OCS.15)
ms:contentKeyID: 49296548
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée des paramètres globaux de déviation du trafic multimédia. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## Exemples

## EXEMPLE 1

Les commandes illustrées dans cet exemple activent la déviation du trafic multimédia et la configurent pour contourner toujours le trafic. La première ligne de l’exemple appelle l’applet de commande **New-CsNetworkMediaBypassConfiguration**. Nous transmettons deux paramètres à cette applet de commande : AlwaysBypass et Enabled, en les définissant sur True ($true). La définition du paramètre Activé sur True entraîne l’activation de la déviation du trafic multimédia, alors que la définition du paramètre AlwaysBypass sur True engendre une tentative de déviation du trafic multimédia sur tous les appels (notez que la définition de ces deux paramètres entraînera la génération automatique d’une valeur pour la propriété BypassID). L’applet de commande **New-CsNetworkMediaBypassConfiguration** crée l’objet en mémoire seulement. Nous affectons donc cet objet à la variable $a.

La configuration de la déviation du trafic multimédia est stockée dans les paramètres de configuration réseau. Par conséquent, sur la ligne 2 de l’exemple, nous enregistrons les modifications de la configuration de déviation du trafic multimédia dans la configuration réseau en appelant l’applet de commande **Set-CsNetworkConfiguration**, et en transmettant au paramètre MediaBypassSettings l’objet de configuration de déviation du trafic multimédia ($a) que nous avons créé sur la ligne 1.

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## EXEMPLE 2

Lync Server n’inclut aucune applet de commande **Set-CsNetworkMediaBypassConfiguration**. Pour modifier les paramètres existants, vous devez donc créer une nouvelle configuration (comme illustré dans l’exemple 1) pour remplacer la configuration existante ou modifier les paramètres en récupérant les paramètres existants, en les modifiant, puis en utilisant l’applet de commande **Set-CsNetworkConfiguration** pour enregistrer les modifications. Cet exemple illustre la désactivation de l’option Toujours ignorer à l’aide de cette dernière option.

La première ligne de l’exemple extrait les paramètres de déviation de trafic multimédia existants. Pour cela, elle appelle l’applet de commande **Get-CsNetworkConfiguration**. L’appel de cette applet de commande est placé entre parenthèses pour s’assurer que l’applet de commande est terminée avant l’exécution d’une autre partie de la commande. L’applet de commande **Get-CsNetworkConfiguration** extrait tous les paramètres d’une configuration réseau intégrale. Parce que seuls les paramètres de déviation du trafic multimédia nous intéressent ici, nous spécifions la propriété MediaBypassSettings afin de n’extraire que ces paramètres. Nous affectons ces paramètres à la variable $a.

Sur la ligne 2, nous modifions les paramètres stockés dans la variable $a en attribuant la valeur False ($false) à la propriété AlwaysBypass. Enfin, sur la ligne 3, nous appelons l’applet de commande **Set-CsNetworkConfiguration**, en transmettant au paramètre MediaBypassSettings la variable $a, qui enregistre la modification que nous avons apportée à la propriété AlwaysBypass.

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## Description détaillée

Cette applet de commande crée des paramètres globaux pour la déviation du trafic multimédia des connexions audio.

Contrairement à la plupart des applets de commande New- de Lync Server, cette applet de commande n’enregistre pas immédiatement la nouvelle configuration : elle crée les paramètres en mémoire seulement. L’objet créé par cette applet de commande doit être enregistré dans une variable, puis affecté à la propriété MediaBypassSettings de la configuration réseau (pour plus d’informations, consultez les exemples de cette rubrique).

Vous ne pouvez extraire les paramètres créés à l’aide de cette applet de commande qu’en accédant à la propriété MediaBypassSettings de la configuration réseau globale. Pour extraire ces paramètres, exécutez la commande suivante : (Get-CsNetworkConfiguration).MediaBypassSettings.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsNetworkMediaBypassConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La définition de ce paramètre sur True entraîne une tentative de déviation du trafic multimédia sur tous les appels.</p>
<p>Définissez cette valeur sur True uniquement si le contrôle d’admission des appels (CAC) est désactivé. Définissez ce paramètre sur True uniquement pour les déploiements où :</p>
<p>- Il n’est pas nécessaire de contrôler la bande passante.</p>
<p>- Il n’est pas nécessaire d’affiner la configuration pour déterminer à quel moment la déviation doit avoir lieu.</p>
<p>- La connectivité entre passerelles et clients est complète.</p>
<p>Si le paramètre Enabled est défini sur True et AlwaysBypass est défini sur False, la logique de déviation utilisera les sites et régions de configuration réseau pour déterminer à quel moment la déviation est possible.</p>
<p>Si vous définissez le paramètre AlwaysBypass sur True sans définir la valeur du paramètre Enabled sur True, un message d’avertissement s’affiche : Le paramètre AlwaysBypass est ignoré si le paramètre Enabled est défini sur False.</p>
<p>La définition des paramètres AlwaysBypass et Enabled sur True entraîne la génération automatique d’un ID de dérivation qui sera stocké dans la propriété BypassID.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>L’ID de déviation du trafic multimédia. Si le paramètre AlwaysBypass est défini sur True et qu’une valeur est fournie pour ce paramètre, BypassID sera associé à tous les sous-réseaux. Si AlwaysBypass est défini sur False, la valeur BypassID est associée à tous les sous-réseaux qui ne sont pas détectés dans les sites et régions de configuration réseau.</p>
<p>Cet ID doit être au format d’un GUID (par exemple : 96f14dea-5170-429a-b92b-f1cb909c4bb6). Toutefois, vous n’aurez généralement pas à définir ou modifier ce paramètre. Cette valeur est automatiquement générée lorsque le paramètre Enabled est défini sur True et que l’une des conditions suivantes est vérifiée : 1) AlwaysBypass est défini sur True ou 2) le paramètre EnableDefaultBypassID est défini sur True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Définissez ce paramètre sur True pour activer la déviation du trafic multimédia. À cette étape, les décisions reposeront sur la valeur du paramètre AlwaysBypass comme suit :</p>
<p>- Si AlwaysBypass est défini sur True, la déviation concernera tous les appels.</p>
<p>- Si AlwaysBypass est défini sur False, utilisez les sites et régions de configuration réseau pour déterminer si la déviation est possible.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Cette valeur s’applique uniquement lorsque AlwaysBypass est défini sur False.</p>
<p>La définition de cette valeur sur True entraîne automatiquement la génération d’un ID de déviation par défaut. Cette valeur automatiquement générée sera stockée dans la propriété BypassID.</p>
<p>Ce paramètre est utile dans le cas d’un réseau principal parfaitement connecté à des sites distants dont les liaisons présentent une bande passante restreinte. L’administrateur devra définir uniquement les sous-réseaux associés aux sites distants via les sites et régions de configuration réseau. Tous les sous-réseaux associés au réseau principal n’ont pas besoin d’être définis et la déviation s’effectuera automatiquement entre ces sous-réseaux.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si la déviation du trafic multimédia doit être utilisée pour les conférences A/V. La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Réservé à un usage ultérieur. La fonction de déviation du trafic multimédia externe n’est pas prise en charge dans Lync Server.</p>
<p>Valeur par défaut : Désactivé</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>La valeur de ce paramètre contrôle quand les clients qui se connectent depuis le réseau de l’organisation peuvent essayer d’effectuer une déviation du trafic multimédia. S’il est toutefois défini sur True, cette valeur sera automatiquement modifiée à N’importe lequel. Les autres valeurs de ce paramètre sont réservées à un usage ultérieur.</p>
<p>Valeur par défaut : Désactivé</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Crée une référence d’objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType.

## Voir aussi

#### Autres ressources

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

