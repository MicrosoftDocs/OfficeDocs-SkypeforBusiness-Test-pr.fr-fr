---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398410(v=OCS.15)
ms:contentKeyID: 49297349
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie l’itinéraire existant qui relie des régions réseau à l’intérieur d’une configuration du contrôle d’admission des appels (CAC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie l’itinéraire NA\_APAC\_Route en modifiant les liens entre régions qui seront traversés sur l’itinéraire. Le paramètre NetworkRegionLinkIDs est utilisé avec la valeur NA\_SA,SA\_APAC qui remplace tout lien existant par deux liens spécifiés dans cette chaîne.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## EXEMPLE 2

Comme à l’exemple 1, l’exemple 2 modifie les liens avec l’itinéraire NA\_APAC\_Route. Dans cet exemple toutefois, au lieu de remplacer tous les liens pour cet itinéraire en utilisant le paramètre NetworkRegionLinkIDs, le paramètre NetworkRegionLinks est utilisé pour ajouter un lien à la liste de liens qui existe déjà sur cet itinéraire. Dans ce cas, le lien SA\_EMEA est ajouté à cet itinéraire. La syntaxe @{add=\<link\>} ajoute un élément à la liste de liens. Vous pouvez également utiliser la syntaxe @{replace=\<link\>} pour remplacer tous les liens existants par les liens spécifiés par \<link\> (qui se comporte essentiellement comme NetworkRegionLinkIDs) ou la syntaxe @{remove=\<link\>} qui permet de supprimer un lien de la liste.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## EXEMPLE 3

L’exemple 3 modifie l’itinéraire appelé NA\_Route5. Cet exemple modifie l’une des régions qui constitue cet itinéraire. Le paramètre NetworkRegionID2 est utilisé pour spécifier la nouvelle région, puis le paramètre NetworkRegionLinkIDs crée une nouvelle liste de liens afin de connecter les régions de cet itinéraire.

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## Description détaillée

Chaque région à l’intérieur d’une configuration CAC doit pouvoir accéder à l’autre région d’une manière ou d’une autre. Alors que les liens de région définissent des restrictions de bande passante sur les connexions entre les régions et qu’ils représentent des liens physiques, un itinéraire détermine le chemin lié que la connexion traverse d’une région à une autre. Cette applet de commande modifie le routage de ces connexions.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkInterRegionRoute** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
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
<td><p>L’identificateur unique de la région de réseau que vous souhaitez modifier. Les itinéraires des régions de réseau ne sont créés que pour l’étendue globale, si bien que cet identificateur n’a pas besoin de spécifier une étendue. Il contient plutôt une chaîne avec un nom unique qui identifie cet itinéraire.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>InterNetworkRegionRouteType</p></td>
<td><p>Référence d’objet à un itinéraire de région existant. L’objet doit être de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType, qui peut être récupéré en appelant l’applet de commande <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>L’identité (NetworkRegionID) de l’une des deux régions connectées sur cet itinéraire. La valeur affectée à ce paramètre doit être une autre région que la valeur du paramètre NetworkRegionID2. (En d’autres mots, vous ne pouvez pas router une région à elle-même.) De plus, la combinaison NetworkRegionID1 et NetworkRegionID2 doit être unique (par exemple, vous ne pouvez pas définir deux itinéraires pour connecter NorthAmerica et EMEA).</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>L’identité (NetworkRegionID) de l’une de ces deux régions connectées grâce à cet itinéraire. La valeur affectée à ce paramètre doit être une autre région que la valeur du paramètre NetworkRegionID1. (En d’autres mots, vous ne pouvez pas router une région à elle-même.) De plus, la combinaison NetworkRegionID1 et NetworkRegionID2 doit être unique (par exemple, vous ne pouvez pas définir deux itinéraires pour connecter NorthAmerica et EMEA).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Vous permet de spécifier tous les liens de cet itinéraire sous la forme d’une chaîne de valeurs CSV. Les valeurs sont des identités (NetworkRegionLinkID) des liens entre régions. Si vous entrez des valeurs pour NetworkRegionLinkIDs et pour NetworkRegionLinks à la fois, NetworkRegionLinkIDs sera ignoré. Tout lien modifié et qui utilise ce paramètre remplacera tous les liens existants sur l’itinéraire.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Objet de liste contenant les identités (NetworkRegionLinkIDs) des liens de région qui s’appliquent à cet itinéraire. Pour cette applet de commande, le paramètre diffère de NetworkRegionLinkIDs dans la mesure où il vous permet non seulement de remplacer les liens existants pour cet itinéraire, mais également d’ajouter ou de supprimer des liens individuels.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Accepte l’entrée redirigée pour les objets d’itinéraire entre les zones de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

