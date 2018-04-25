---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425959(v=OCS.15)
ms:contentKeyID: 49297106
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations relatives aux ordinateurs de votre infrastructure Lync Server dont le rôle est de fournir des services. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## Exemples

## EXEMPLE 1

Dans l’exemple 1, l’applet de commande **Get-CsComputer** est utilisée pour retourner les informations des ordinateurs dont le rôle est de fournir des services dans votre infrastructure Lync Server.

    Get-CsComputer

## EXEMPLE 2

La commande indiquée à l’exemple 2 utilise le paramètre Filter pour retourner les informations des ordinateurs dont le rôle est de fournir des services et qui font partie du domaine litwareinc.com. La chaîne générique \*.litwareinc.com restreint le renvoi d’informations aux ordinateurs dont le nom de domaine complet (FQDN) se termine par la valeur de chaîne .litwareinc.com.

    Get-CsComputer -Filter "*.litwareinc.com"

## EXEMPLE 3

Dans l’exemple 3, le paramètre Identity est utilisé pour restreindre le renvoi des données à un ordinateur dont le nom de domaine complet est atl-cs-001.litwareinc.com.

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## EXEMPLE 4

Dans l’exemple 4, le paramètre Pool est utilisé pour retourner des informations sur tous les ordinateurs du pool atl-cs-001.litwareinc.com.

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## Description détaillée

L’applet de commande **Get-CsComputer** fournit un moyen d’identifier rapidement les ordinateurs qui exploitent les services Lync Server ou des rôles serveur. Appelée sans aucun paramètre, l’applet de commande **Get-CsComputer**retourne une collection de tous les ordinateurs qui exploitent les services Lync Server ou des rôles serveur. Cette collection inclut l’identité, le nom de pool et le nom du domaine complet de chaque ordinateur. Vous pouvez également utiliser des paramètres facultatifs tels que Identity, Filter ou Pool, pour limiter le renvoi des données à un seul ordinateur ou un groupe d’ordinateurs.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsComputer** : RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p>Permet d’utiliser des caractères génériques pour spécifier l’identité de l’ordinateur (ou des ordinateurs) dont les informations doivent être renvoyées. Par exemple, cette commande retourne des informations sur les ordinateurs dont l’identité commence par la valeur de chaîne « atl- » : -Filter &quot;atl-*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nom de domaine complet à retourner. Par exemple : -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Si ce paramètre n’est pas spécifié, tous les ordinateurs exécutant Lync Server seront retournés.</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Si le paramètre est présent, ne retourne les informations que pour l’ordinateur local.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de domaine complet d’un pool Lync Server. Si vous utilisez ce paramètre, ce sont les informations de tous les ordinateurs du pool spécifié qui seront renvoyées.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsComputer** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsComputer** retourne les instances de l’objet Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Voir aussi

#### Autres ressources

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

