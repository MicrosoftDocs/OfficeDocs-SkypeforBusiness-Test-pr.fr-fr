---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg413089(v=OCS.15)
ms:contentKeyID: 49299462
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une région de réseau existante. Les régions de réseau sont des concentrateurs de réseau ou les routeurs principaux d’un réseau d’entreprise. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans cet exemple, la région de réseau appelée NorthAmerica est modifiée. La valeur « North American Region » est attribuée au paramètre Description. Si une description existait dans la région Amérique du Nord, cette commande la remplace par cette valeur. Si aucune description n’existe, cette commande la définit.

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## EXEMPLE 2

Dans cet exemple, la région de réseau appelée EMEA est modifiée et un nouveau paramètre de chemin alternatif vidéo lui est attribué. Pour ce faire, nous appelons l’applet de commande **Set-CsNetworkRegion** qui transmet une identité EMEA. Nous spécifions ensuite le paramètre VideoAlternatePath en lui transmettant la valeur $False. La définition de VideoAlternatePath sur False indique que si la bande passante adéquate n’est pas disponible, l’appel vidéo ne sera pas acheminé vers un chemin alternatif. Il ne sera simplement pas terminé.

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## EXEMPLE 3

L’exemple 3 illustre l’affectation du même ensemble de paramètres de chemin alternatif à la région de réseau Asie que ceux qui ont été définis pour la région Amérique du Nord. La première ligne de cet exemple extrait une instance de la région de réseau NorthAmerica et l’affecte à la variable $a. La deuxième ligne commence par extraire le contenu de la propriété BWAlternatePaths ou la région NorthAmerica (stockée dans la variable $a) : $a.BWAlternatePaths. Il s’agit d’un ensemble de tous les paramètres de chemin alternatif dans la région NorthAmerica.

La prochaine étape consiste à rediriger cette collection de paramètres vers la fonction foreach. Foreach parcourt les éléments de la collection un à un, en effectuant les actions décrites dans les accolades suivantes. Dans ce cas, l’action consiste à appeler l’applet de commande **Set-CsNetworkRegion** avec une valeur Identity « Asia » afin de définir les propriétés de la région Asie. Le paramètre suivant est BWAlternatePaths. Nous transmettons la valeur @{add=$\_} à ce paramètre. La variable $\_ représente l’élément actuel de la collection, dans ce cas le chemin alternatif actuel. La partie @{add=} de la valeur ajoute cet élément à la collection de paramètres BWAlternatePaths pour la région Asie.

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## Description détaillée

Une région de réseau interconnecte diverses parties d’un réseau sur plusieurs zones géographiques. Chaque région de réseau doit être associée à un site central. Le site central est le site du centre de données dans lequel le service de stratégie de bande passante du contrôle d’admission des appels (CAC) est exécuté. Utilisez cette applet de commande pour modifier une région de réseau existante, notamment les paramètres qui déterminent si d’autres chemins sont autorisés pour les connexions audio et vidéo et qui associent les sites de la région à une configuration de déviation du trafic multimédia.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkRegion** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Ce paramètre détermine si les appels audio seront acheminés via un autre chemin si la bande passante adéquate n’existe pas dans le chemin principal.</p>
<p>Ce paramètre renseigne la propriété BWAlternatePaths. La valeur saisie pour ce paramètre est stockée dans la propriété AlternatePath pour l’élément de chemin alternatif dont le paramètre BWPolicyModality est défini sur la valeur Audio.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWAlternatePaths.</p>
<p>Si certains de vos appels seront des appels Internet, cette valeur doit être définie sur True, quels que soient les paramètres de bande passante.</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste des objets qui contiennent des informations déterminant si des chemins de connexion alternatifs sont autorisés en cas d’échec d’une demande de support sur le chemin préféré (par exemple, si les limites de ce chemin ont été dépassées). Les objets de chemin alternatif doivent être de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType. Vous pouvez créer des objets de ce type en appelant l’applet de commande <strong>New-CsNetworkBWAlternatePath</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identificateur global unique (GUID). Ce GUID est utilisé pour mapper des régions de réseau à des paramètres de déviation du trafic multimédia au sein d’une configuration réseau CAC ou Enhanced 9-1-1 (E9-1-1). (Utilisez cette valeur BypassID au moment d’appeler l’applet de commande <strong>New-CsNetworkMediaBypassConfiguration</strong>).</p>
<p>Ce paramètre peut être automatiquement généré lors de la création de la région (en appelant l’applet de commande <strong>New-CsNetworkRegion</strong>). Il est déconseillé de modifier cette valeur. Si vous ne spécifiez pas de valeur, elle doit être au format d’un GUID (par exemple : 3b24a047-dce6-48b2-9f20-9fbff17ed62a). Une confirmation vous invitant à vérifier que vous souhaitez définir manuellement cette valeur s’affiche.</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Le site central sur lequel le service de stratégie de bande passante est exécuté. Ce service doit être activé pour pouvoir utiliser le contrôle d’admission des appels. Ce service fonctionne sur le serveur frontal ou le serveur Standard Edition.</p></td>
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
<td><p>Chaîne décrivant la région. Vous pouvez utiliser ce paramètre pour fournir une description plus explicite de l’objectif d’une région qui peut être exprimé par l’identité seule.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique de la région de réseau que vous souhaitez modifier. L’identité apparaîtra sous la forme d’une chaîne qui identifie cette région de manière unique.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSObject</p></td>
<td><p>Référence à un objet de région de réseau. Cet objet doit être du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType et peut être extrait en appelant l’applet de commande <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Ce paramètre détermine si les appels vidéo seront acheminés via un chemin alternatif si la bande passante adéquate n’existe pas dans le chemin principal.</p>
<p>Ce paramètre renseigne la propriété BWAlternatePaths. La valeur saisie pour ce paramètre est stockée dans la propriété AlternatePath pour l’élément de chemin alternatif dont le paramètre BWPolicyModality est défini sur la valeur Video.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWAlternatePaths.</p>
<p>Si certains de vos appels seront des appels Internet, cette valeur doit être définie sur True, quels que soient les paramètres de bande passante.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Accepte l’entrée redirigée pour les objets de région de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

