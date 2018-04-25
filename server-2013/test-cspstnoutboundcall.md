---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398207(v=OCS.15)
ms:contentKeyID: 49296314
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la capacité d’un utilisateur à appeler un numéro de téléphone situé sur le réseau téléphonique commuté (RTC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si un utilisateur préconfiguré peut se connecter au pool atl-cs-001.litwareinc.com et effectuer ensuite un appel téléphonique sur la passerelle PSTN. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande déterminera si le premier utilisateur de test peut se connecter au système et, si tel est le cas, s’il peut appeler un numéro de téléphone situé sur le réseau PSTN.

Si aucun utilisateur de test n’a été défini, la commande échouera car elle ignore quel utilisateur employer lors de l’exécution du test. Si vous n’avez pas défini d’utilisateur de test pour un pool, vous devez inclure le paramètre UserSipAddress ainsi que les informations d’identification correspondantes pour le compte d’utilisateur impliqué dans le test. L’applet de commande **Test-CsPstnOutboundCall** effectuera ensuite ses vérifications à l’aide du nom d’utilisateur spécifié.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent la capacité d’un utilisateur de test (litwareinc\\kenmyer) à se connecter à Lync Server et à effectuer ensuite un appel téléphonique sur la passerelle RTC. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Ken Myer (le nom de connexion litwareinc\\kenmyer ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur entre le mot de passe relatif au compte Ken Myer). L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1.

À partir de cet objet d’identification, la deuxième commande de l’exemple détermine si l’utilisateur de test peut ou non se connecter à Lync Server et appeler ensuite le numéro de téléphone cible (+15551234567). Pour exécuter cette tâche, l’applet de commande **Test-CsPstnOutboundCall** est appelée avec les paramètres suivants : TargetFqdn (le nom de domaine complet du pool de serveurs d’inscriptions), UserSipAddress (l’adresse SIP de l’utilisateur qui effectue l’appel), UserCredential (l’objet Windows PowerShell contenant les informations d’identification de l’utilisateur de test) et TargetPstnPhoneNumber (le numéro de téléphone composé).

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## EXEMPLE 3

L’exemple 3 présente une utilisation de **Test-CsPstnOutboundCall** en mode plateforme de serveur. Avec ce mode, les adresses SIP des utilisateurs sont indiquées, mais les informations d’identification des utilisateurs ne le sont pas. Avec ce mode d’exécution, Lync Server utilise des certificats pour authentifier l’utilisateur de test.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## Description détaillée

L’applet de commande **Test-CsPstnOutboundCall** est un exemple de « transaction synthétique » de Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier si les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test), et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande Test-CsPstnOutboundCall peut également être utilisée en mode plateforme de serveur. Dans ce cas, il vous suffit de spécifier l’adresse SIP d’un utilisateur et Lync Server utilisera des certificats pour authentifier cet utilisateur.

Lorsque vous exécutez l’applet de commande **Test-CsPstnOutboundCall**, l’applet de commande tente d’abord de connecter l’utilisateur test à Lync Server. Si la connexion est correctement établie, l’applet de commande essaiera de passer un appel téléphonique sur la passerelle RTC. Cet appel sera effectué en se basant sur le plan de numérotation, la stratégie de voix et d’autres stratégies et paramètres affectés au compte de test. Lorsque l’appel est répondu, l’applet de commande envoie des codes de numérotation en fréquences vocales (DTMF) sur le réseau pour vérifier la connectivité multimédia.

Lors de la réalisation d’un test, l’applet de commande **Test-CsPstnOutboundCall** passe un appel téléphonique réel : le téléphone cible retentit et doit être décroché pour que le test réussisse. Par ailleurs, cet appel doit être conclu manuellement par l’administrateur.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p>Nom de domaine complet (FQDN) du pool à tester.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Numéro de téléphone PSTN à appeler lors de l’exécution du test. Pour spécifier au mieux le numéro de téléphone, il est préférable d’utiliser le format E.164. Le numéro ressemblera donc à « +14255551298 », autrement dit, un signe plus (+) suivi de l’indicatif du pays (1), de l’indicatif régional (425) et du numéro de téléphone (5551298). N’utilisez pas de tirets, de parenthèses ou d’autres caractères lors de la saisie du numéro de téléphone.</p>
<p>Si vous n’utilisez pas le format E.164, le plan de numérotation de l’utilisateur de test sera ajouté à la fin du numéro. Lync Server utilisera ensuite ce plan de numérotation pour normaliser le numéro au format E.164. S’il ne peut pas être normalisé, l’appel ne pourra pas être passé et le test échouera.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification du compte à tester. La valeur transmise à UserCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et le stocke dans une variable appelée $x :</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Ce paramètre n’est pas nécessaire si la commande utilise des utilisateurs de test configurés à l’aide de l’applet de commande CsHealthMonitoringConfiguration. Vous n’avez pas non plus besoin de spécifier ce paramètre si le test est réalisé en mode plateforme de serveur. Dans ce cas, Lync Server essaiera d’authentifier l’utilisateur en utilisant des certificats.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Cette variable inclut deux méthodes, ToHTML et ToXML, qui permettent d’enregistrer cette sortie dans un fichier HTML ou XML.</p>
<p>Pour stocker la sortie dans la variable d’un journal $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Remarque : n’utilisez pas le caractère $ lorsque vous spécifiez le nom de la variable. Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier HTML, utilisez une commande telle que :</p>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du compte d’utilisateur à tester. Par exemple : -SenderSipAddress « sip:kenmyer@litwareinc.com ». Le paramètre UserSipAddress doit se référer au même compte d’utilisateur que UserCredential.</p>
<p>Ce paramètre n’est pas nécessaire si la commande utilise des utilisateurs de test configurés à l’aide de l’applet de commande CsHealthMonitoringConfiguration.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsPstnOutboundCall** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsPstnOutboundCall** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

