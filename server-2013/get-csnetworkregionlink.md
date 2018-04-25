---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398972(v=OCS.15)
ms:contentKeyID: 49299068
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**Dernière rubrique modifiée :** 2015-03-09_

Récupère un ou plusieurs liens entre des régions du réseau configurés pour le contrôle d’admission des appels (CAC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 récupère tous les liens de région de réseau définis dans un déploiement Lync Server.

    Get-CsNetworkRegionLink

## EXEMPLE 2

L’exemple 2 récupère des informations sur (au plus) un lien de région réseau, le lien dont l’identité est NA\_EMEA.

    Get-CsNetworkRegionLink -Identity NA_EMEA

## EXEMPLE 3

Dans cet exemple, nous utilisons le paramètre Filter pour récupérer tous les liens de région réseau dont le nom (identité) comporte la chaîne EMEA. Remarquez les caractères \*, un avant la chaîne EMEA et l’autre après. Cela signifie qu’un ou plusieurs caractères peuvent précéder ou suivre la chaîne ; la chaîne EMEA doit simplement être incluse quelque part dans l’identité. Cela récupérera les liens portant des noms tels que NA\_EMEA, EMEA\_APAC et EMEA2\_SA.

    Get-CsNetworkRegionLink -Filter *EMEA*

## EXEMPLE 4

Cet exemple récupère tous les liens de région réseau qui incluent EMEA comme l’une des deux régions liées. L’exemple commence par appeler l’applet de commande **Get-CsNetworkRegionLink** sans paramètre afin de récupérer tous les liens de région. Cette collection de liens est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** parcourt chaque membre de la collection un par un et vérifie les valeurs des propriétés NetworkRegionID1 et NetworkRegionID2. Si une de ces propriétés est égale à EMEA, en d’autres termes si NetworkRegionID1 est égale à (-eq) EMEA ou (-or) NetworkRegionID2 est égale à (-eq) EMEA, alors il faut conserver cet élément dans la collection et l’afficher.

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## Description détaillée

Les régions au sein d’un réseau sont liées par le biais d’une connectivité WAN physique. Cette applet de commande récupère un ou plusieurs liens de région qui sont définis dans les paramètres de configuration réseau pour un déploiement Lync Server.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkRegionLink** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>Accepte une chaîne de caractères génériques qui est utilisée pour récupérer des liens réseau selon la correspondance de la valeur de Identity à la chaîne de caractères génériques.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du lien de région réseau que vous souhaitez récupérer. Les liens de région réseau sont créés uniquement au niveau de l’étendue globale. Par conséquent, cet identificateur ne doit pas nécessairement spécifier une étendue. Au lieu de cela, il contient une chaîne qui est un nom unique qui identifie ce lien. (Notez que cette valeur est identique à NetworkRegionLinkID).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les informations de lien entre les régions de réseau à partir du réplica local du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Récupère un ou plusieurs objets de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

