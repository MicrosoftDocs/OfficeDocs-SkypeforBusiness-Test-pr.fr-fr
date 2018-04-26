---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398121(v=OCS.15)
ms:contentKeyID: 49296139
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les interfaces réseau utilisées sur des ordinateurs exécutant les services ou les rôles serveur Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## Exemples

## EXEMPLE 1

L’exemple 1 renvoie des informations sur toutes les interfaces réseau configurées pour être utilisées dans l’organisation.

    Get-CsNetworkInterface

## EXEMPLE 2

La commande illustrée dans l’exemple 2 renvoie des informations sur une seule interface réseau : l’interface comportant l’identité atl-cs-001.litwareinc.com.com/Primary/1.

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## EXEMPLE 3

Dans l’exemple 3, des informations sont renvoyées sur toutes les interfaces réseau dans le domaine litwareinc.com. Pour cela, on inclut le paramètre Filter, associé à la valeur de filtre « \*.litwareinc.com\* ». Cette valeur limite les données renvoyées aux interfaces dont l’identité inclut la valeur de chaîne « litwareinc.com ».

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## EXEMPLE 4

L’exemple 4 renvoie des informations sur toutes les interfaces réseau configurées pour l’adresse IP 192.168.0.240. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsNetworkInterface** sans aucun paramètre, qui entraîne le renvoi d’un ensemble contenant toutes les interfaces réseau configurées pour être utilisées dans l’organisation. Cet ensemble est ensuite redirigé vers l’applet de commande **Where-Object**, qui sélectionne uniquement les interfaces dont la propriété IPAddress est égale à 192.168.0.240.

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## EXEMPLE 5

La commande illustrée dans l’exemple 5 est une variante de la commande décrite dans l’exemple 4. Dans ce cas cependant, les informations renvoyées concernent toutes les interfaces réseau configurées pour le sous-réseau « 192.168.0.\* ». Cette opération est effectuée en extrayant un ensemble de toutes les interfaces réseau, en redirigeant cet ensemble vers l’applet de commande **Where-Object**, puis en sélectionnant uniquement les interfaces dont la propriété IPAddress commence par la valeur de chaîne « 192.168.0. ».

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## EXEMPLE 6

L’exemple 6 renvoie toutes les interfaces réseau qui ont été configurées pour un accès externe. Pour cela, l’applet de commande **Get-CsNetworkInterface** est d’abord appelée sans aucun paramètre, qui renvoie une collection de toutes les interfaces réseau actuellement utilisées. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object**, qui sélectionne uniquement les éléments pour lesquels la propriété Interface est égale à External.

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## Description détaillée

Pour que les ordinateurs s’échangent des informations, ils doivent disposer d’interfaces réseau, c’est-à-dire de connexions entre l’ordinateur et le réseau. Les ordinateurs exécutant des services ou des rôles serveur Lync Server doivent comporter au moins une interface réseau, sinon ils ne pourront pas communiquer avec d’autres ordinateurs. Toutefois, ces ordinateurs peuvent également avoir plusieurs interfaces réseau. Par exemple, un serveur Edge peut inclure une interface pour la connexion au réseau interne et une autre pour la connexion à Internet. L’applet de commande **Get-CsNetworkInterface** permet aux administrateurs de renvoyer des informations sur les interfaces réseau actuellement utilisées sur des ordinateurs exécutant les services ou les rôles serveur Lync Server.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkInterface** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet de l’ordinateur sur lequel des informations d’interface réseau doivent être renvoyées. Par exemple, pour renvoyer des informations sur l’interface réseau de l’ordinateur atl-cs-001.litwareinc.com (et uniquement de cet ordinateur), utilisez la syntaxe suivante : -ComputerFqdn atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet d’utiliser des caractères génériques lors de la spécification de l’interface (ou des interfaces) réseau à renvoyer. Par exemple, la syntaxe suivante renvoie des informations sur l’interface réseau principale utilisée sur tous les ordinateurs exécutant un service ou un rôle serveur Lync Server : -Filter « */Primary/* ».</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>Identificateur unique de l’interface réseau à renvoyer. Une identité d’interface réseau se compose de trois parties :</p>
<p>Le nom de domaine complet (FQDN) de l’ordinateur proprement dit (par exemple : atl-cs-001.litwareinc.com).</p>
<p>Le « côté » interface réseau (principal, interne, externe, réseau téléphonique commuté). Le côté indique le type de trafic pour lequel le port est utilisé.</p>
<p>Le numéro de l’interface réseau pour ce côté particulier.</p>
<p>Par exemple : -Identity « atl-cs-001.litwareinc.com/Primary/1 ».</p>
<p>Les paramètres Identity, ComputerFqdn et Filter doivent être utilisés séparément. Par exemple, il n’est pas possible d’exécuter une commande utilisant simultanément ComputerFqdn et Identity. Vous ne pouvez pas non plus utiliser de caractères génériques pour spécifier l’identité. Pour employer des caractères génériques, utilisez plutôt le paramètre Filter.</p>
<p>Si vous utilisez les paramètres Identity, ComputerFqdn ou Filter, l’applet de commande <strong>Get-CsNetworkInterface</strong> renvoie des informations sur toutes les interfaces réseau actuellement utilisées sur vos ordinateurs exécutant un service ou un rôle serveur Lync Server.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsNetworkInterface** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsNetworkInterface** renvoie l’instance de l’objet Microsoft.Rtc.Management.Xds.DisplayNetworkInterface.

## Voir aussi

#### Autres ressources

[Get-CsComputer](get-cscomputer.md)

