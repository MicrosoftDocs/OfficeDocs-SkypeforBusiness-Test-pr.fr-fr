---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412769(v=OCS.15)
ms:contentKeyID: 49298398
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Récupère une ou plusieurs stratégies réseau intersites définissant les restrictions de bande passante entre des sites directement liés au sein d’une configuration de contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Le fait d’appeler l’applet de commande **Get-CsNetworkInterSitePolicy** sans paramètres récupère toutes les stratégies de site réseau définies entre deux sites réseau directement liés.

    Get-CsNetworkInterSitePolicy

## EXEMPLE 2

Cet exemple récupère la stratégie de site réseau ayant l’identité Reno\_Portland.

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## EXEMPLE 3

L’exemple 3 récupère toutes les stratégies de site réseau contenant la chaîne Reno n’importe où au sein de la valeur Identity. Les caractères génériques (\*) au sein de la valeur transmise au paramètre Filter signifie « tout caractère ou jeu de caractères. » En d’autres termes, la chaîne \*Reno\* fait correspondre des valeurs d’identité correspondant à un ou plusieurs caractères, suivi de la chaîne Reno et d’un ou plusieurs caractères.

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## EXEMPLE 4

Cet exemple récupère toutes les stratégies de site réseau qui n’ont pas de profil de stratégie de bande passante. La commande commence par appeler l’applet de commande **Get-CsNetworkInterSitePolicy** qui, comme dans l’exemple 1, récupère une collection de toutes les stratégies de site réseau. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object**. **Where-Object** restreint la collection aux stratégies de site réseau qui n’ont pas de profil de stratégie de bande passante. Pour ce faire, elle recherche pour chaque stratégie de site la propriété BWPolicyProfileID égale (-eq) à Null ($null).

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## Description détaillée

Quand des sites réseau partagent un lien direct, des restrictions de bande passante pour les connexions audio et vidéo peuvent être définies pour lesdits sites. Cette applet de commande récupère une ou plusieurs stratégies de site réseau associant des paramètres de restriction de bande passante à deux sites directement connectés.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkInterSitePolicy** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>Chaîne contenant des caractères génériques recherchant les stratégies dont les valeurs d’identité correspondent à la chaîne à caractère générique.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique de la stratégie de site réseau que vous souhaitez récupérer. Les stratégies de site réseau étant créées au niveau de l’étendue globale seulement, il n’est pas nécessaire de spécifier une étendue pour cet identificateur. Il contient en effet une chaîne au nom unique permettant d’identifier cette stratégie.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les informations de stratégie intersite réseau à partir du réplica local du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Récupère un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

