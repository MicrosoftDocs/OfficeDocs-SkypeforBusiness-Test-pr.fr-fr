---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398992(v=OCS.15)
ms:contentKeyID: 49299094
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les pools utilisés dans votre déploiement de Lync Server. Les pools sont une collection d’ordinateurs dans un site, qui exécutent tous le même ensemble de services Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 retourne tous les pools de votre déploiement Lync Server.

    Get-CsPool

## EXEMPLE 2

L’exemple 2 affiche des informations détaillées sur les ordinateurs de chaque pool. Pour ce faire, l’applet de commande **Get-CsPool** est appelée, puis les données retournées sont redirigées vers l’applet de commande **Select-Object**. Le paramètre ExpandProperty est utilisé pour « développer » la valeur de la propriété Computers. La propriété Computers est en réalité un groupe d’objets représentant chaque ordinateur du pool. Lorsque vous développez la propriété Computers, vous obtenez des informations détaillées sur chacun de ces ordinateurs.

    Get-CsPool | Select-Object -ExpandProperty Computers

## EXEMPLE 3

Dans l’exemple 3, le paramètre Identity est utilisé pour restreindre les données retournées à un pool dont l’identité est atl-cs-001.litwareinc.com.

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## EXEMPLE 4

L’exemple 4 retourne tous les pools trouvés dans le site Redmond. Pour ce faire, la commande utilise le paramètre Site. La valeur de paramètre « Redmond » limite les données retournées aux pools dont la propriété Site est égale à Redmond.

    Get-CsPool -Site "Redmond"

## EXEMPLE 5

La commande présentée dans l’exemple 5 retourne une collection de tous les pools pour lesquels Lync Server n’est pas installé. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsPool** sans paramètre ; cet appel retourne une collection de tous les pools actuellement utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne tous les pools dont la propriété Services.Count est égale à 0. Si Count est égal à 0, il n’y a aucun service Lync Server configuré pour ce pool.

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## Description détaillée

Dans Lync Server, un pool correspond à un ou plusieurs ordinateurs dans le même site, qui exécutent le même ensemble de services. Par exemple, si vous avez un serveur exécutant le service de serveur de médiation sur le site Redmond, vous avez alors un pool de service de serveur de médiation constitué d’un seul ordinateur. Si vous avez deux ordinateurs exécutant le serveur de médiation sur le site Redmond, vous avez alors un pool de serveur de médiation constitué de deux ordinateurs. Le nombre de pools utilisés dans votre organisation dépend du nombre de serveurs dont vous disposez et des différents services exécutés par ces serveurs.

L’applet de commande **Get-CsPool** permet de récupérer des informations sur chaque pool utilisé dans votre organisation, y compris des informations sur les services qui s’exécutent sur chacun de ces pools.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsPool** : RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p>Permet d’utiliser des caractères génériques lors de la spécification de l’identité du ou des pools à retourner. Par exemple, cette syntaxe retourne tous les pools ayant une identité qui se termine par la valeur de chaîne « .fabrikam.com » : -Filter &quot;*.fabrikam.com&quot;.</p>
<p>Notez que vous ne pouvez pas utiliser les paramètres Filter et Identity dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nom de domaine complet (FQDN) du pool à retourner. Par exemple : -Identity atl-cs-001.litwareinc.com.</p>
<p>Si ce paramètre n’est pas présent, tous les pools de votre organisation seront retournés.</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Retourne tous les pools trouvés sur le site spécifié. Le site en question doit être référencé à l’aide de la valeur DisplayName du site (par exemple, Redmond) plutôt qu’à l’aide de l’identité du site (par exemple, site:Redmond). Par exemple : -Site &quot;Redmond&quot;. Vous pouvez récupérer les noms complets pour les sites exécutant cette commande :</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsPool** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsPool** retourne les instances de l’objet Microsoft.Rtc.Management.Deploy.Internal.Cluster.

## Voir aussi

#### Autres ressources

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

