---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398497(v=OCS.15)
ms:contentKeyID: 49297495
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la configuration LIS (Location Information Server). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## Exemples

## EXEMPLE 1

Cet exemple teste la configuration LIS du nom de domaine complet (FQDN) atl-cs-001.litwareinc.com. Ce test réussit si une connexion au service web LIS peut être établie avec les informations d’identification de l’utilisateur pour ce nom de domaine complet. Si un emplacement peut être trouvé et qu’il est associé à l’adresse IP du sous-réseau 192.168.0.0, cette adresse géographique sera retournée.

Pour que cette commande soit concluante, une configuration d’analyse d’intégrité contenant des utilisateurs de transactions synthétiques doit exister. Pour savoir s’il existe une configuration d’analyse d’intégrité, exécutez l’applet de commande **Get-CsHealthMonitoringConfiguration**. Pour créer une configuration d’analyse d’intégrité, exécutez l’applet de commande **New-CsHealthMonitoringConfiguration**.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## EXEMPLE 2

Cet exemple est identique à l’exemple 1 mais il ajoute le paramètre UserSipAddress. Utilisez cette commande lorsqu’aucun utilisateur de transactions synthétiques n’a été défini, mais quand l’ordinateur sur lequel la commande est exécutée dispose d’un certificat de serveur.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## EXEMPLE 3

La première ligne de cet exemple appelle une applet de commande Windows PowerShell, l’applet de commande **Get-Credential** qui invite l’utilisateur à fournir un nom d’utilisateur et un mot de passe. Ces informations sont enregistrées de manière chiffrée dans la variable $cred.

La deuxième ligne est identique à la commande dans l’exemple 2 mais elle ajoute le paramètre UserSipAddress. Utilisez cette commande lorsqu’aucun utilisateur de transactions synthétiques n’a été défini, et quand l’ordinateur sur lequel la commande est exécutée ne dispose pas d’un certificat de serveur.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## EXEMPLE 4

La première ligne de cet exemple appelle l’applet de commande **Get-Credential** qui invite l’utilisateur à fournir un nom d’utilisateur et un mot de passe. Ces informations sont enregistrées de manière chiffrée dans la variable $cred.

La ligne 2 teste la configuration LIS en appelant l’URI du service web (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) en fonction de l’adresse SIP de l’utilisateur distant (sip:kmyer@litwareinc.com) et en utilisant les informations d’identification que nous avons obtenues à la ligne 1 et en les transférant au paramètre WebCredential. Ce test sera réussi si la connexion au service web LIS peut être réalisée avec les informations d’identification de l’utilisateur pour ce nom de domaine complet. Si un emplacement est trouvé et s’il est associé à l’adresse IP de sous-réseau 192.168.0.0, l’adresse MAC 0A-23-00-00-00-AA ou l’ID de port 4500 et ChassisId 0A-23-00-00-00-AA, cette adresse géographique sera retournée.

Utilisez cette commande quand l’ordinateur sur lequel la commande est exécutée ne dispose pas d’un certificat de serveur.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## EXEMPLE 5

Cet exemple est identique à l’exemple 4, sauf que la commande n’utilise pas le paramètre WebCredential (et donc, elle n’appelle pas non plus l’applet de commande **Get-Credential**). Utilisez cette commande quand l’ordinateur sur lequel la commande est exécutée dispose d’un certificat de serveur.

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## Description détaillée

Cette applet de commande détermine si le service web LIS (Location Information Server) peut être contacté sur la base des informations contenues dans les paramètres fournis. Si le service web peut être contacté et qu’un emplacement correspondant à l’un des paramètres fournis est trouvé, le test est jugé concluant et l’emplacement est affiché. Même si l’emplacement n’est pas trouvé, si le service web peut être contacté, le test sera positif mais ne fournira aucune information sur l’emplacement. De plus, si vous appelez cette applet de commande sans fournir de paramètres facultatifs, le test sera toujours concluant à condition que le service web puisse être contacté. Mais une nouvelle fois, aucune information sur l’emplacement ne sera retournée.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsLisConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Nom de domaine complet (sous la forme server.litwareinc.com) du serveur à partir duquel vous voulez effectuer le test.</p>
<p>Ce paramètre est nécessaire à moins que vous ne spécifiiez le paramètre TargetUri, auquel cas vous ne pouvez pas spécifier de paramètre TargetFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>URI (Uniform Resource Identifier) du service d’informations sur l’emplacement. Vous pouvez récupérer l’URI du service d’informations sur l’emplacement en exécutant la commande suivante : Get-CsService –WebServer | Select-Object LIServiceInternalUri</p>
<p>Si vous spécifiez une valeur pour ce paramètre, le paramètre UserSipAddress sera également requis. Si l’ordinateur sur lequel vous exécutez la commande n’a pas de certificat de serveur, vous devrez également spécifier une valeur pour le paramètre WebCredential.</p>
<p>Ce paramètre est nécessaire à moins que vous ne spécifiiez le paramètre TargetFqdn.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet dans lequel sont stockées les informations d’identification de l’utilisateur permettant à celui-ci d’accéder au service d’informations sur l’emplacement. Cet objet peut être récupéré en appelant l’applet de commande <strong>Get-Credential</strong> et en fournissant les informations d’identification appropriées.</p>
<p>Ce paramètre est requis si les paramètres TargetFqdn et UserSipAddress sont spécifiés, et si l’ordinateur à partir duquel vous exécutez l’applet de commande n’a pas de certificat de serveur.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Type d’authentification utilisé pendant le test. Les valeurs autorisées sont les suivantes :</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>BssId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identificateur BSSID (Basic Service Set Identifier) d’un point d’accès sans fil. Cette valeur prendra la forme nn-nn-nn-nn-nn-nn (par exemple, 12-34-56-78-90-ab).</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse MAC (Media Access Control) d’un commutateur de réseau. Cette valeur prendra la forme nn-nn-nn-nn-nn-nn (par exemple, 12-34-56-78-90-ab) ou celle d’une adresse IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Ce paramètre n’est pas pris en charge pour le serveur LIS.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse MAC du commutateur de port. Cette valeur prendra la forme nn-nn-nn-nn-nn-nn (par exemple, 12-34-56-78-90-ab).</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Cette variable inclut deux méthodes, ToHTML et ToXML, qui permettent d’enregistrer cette sortie dans un fichier HTML ou XML.</p>
<p>Pour stocker la sortie dans la variable d’un journal $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Remarque : n’utilisez pas le caractère $ pour indiquer le nom de la variable. Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier HTML, utilisez une commande telle que :</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier XML, utilisez une commande telle que :</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Par exemple, pour stocker une sortie dans une variable appelée $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutVerboseVariable TestOutput</p>
<p>N’utilisez pas le caractère $ pour indiquer le nom de la variable.</p></td>
</tr>
<tr class="even">
<td><p><em>PortId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>ID du port associé à l’emplacement à tester. Ce paramètre peut également inclure une adresse MAC ou une adresse IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PortIDSubType</p></td>
<td><p>Sous-type du port. Cette valeur peut être saisie sous la forme d’une valeur numérique ou d’une chaîne mais elle doit être un sous-type valide. Les sous-types valides sont les suivants :</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Numéro du port du service Serveur d’inscriptions.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse IP du sous-réseau. Cette valeur doit apparaître sous la forme d’une adresse IPv4 (chiffres séparés par des points ; par exemple, 192.0.2.0).</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP d’un utilisateur distant.</p>
<p>Si vous spécifiez une valeur pour ce paramètre, le paramètre TargetFqdn ou TargetUri sera également requis.</p>
<p>Ce paramètre est nécessaire lorsque vous spécifiez le paramètre TargetFqdn uniquement si vous n’avez pas défini d’utilisateurs pour les transactions synthétiques. Pour savoir si des utilisateurs de transactions synthétiques ont été définis, exécutez l’applet de commande <strong>Get-CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet dans lequel sont stockées les informations d’identification de l’utilisateur permettant à celui-ci d’accéder au service d’informations sur l’emplacement. Cet objet peut être récupéré en appelant l’applet de commande <strong>Get-Credential</strong> et en fournissant les informations d’identification.</p>
<p>Ce paramètre est requis si les paramètres TargetUri et UserSipAddress sont spécifiés, et si l’ordinateur sur lequel vous exécutez la commande n’a pas de certificat de serveur.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Test-CsLisConfiguration** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

