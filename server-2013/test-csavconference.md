---
title: Test-CsAVConference
TOCTitle: Test-CsAVConference
ms:assetid: a1492563-9a97-44ac-b19a-8d5972cdd062
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412749(v=OCS.15)
ms:contentKeyID: 49298402
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVConference

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste l’aptitude de deux utilisateurs à prendre part à une conférence audio/vidéo (A/V). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsAVConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si une paire d’utilisateurs de test préconfigurés peut se connecter au pool atl-cs-001.litwareinc.com et participer à une conférence audio/vidéo. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande détermine si les deux utilisateurs peuvent se connecter au système. Si oui, le premier utilisateur de test crée une conférence audio/vidéo et invite le second utilisateur à s’y joindre. L’applet de commande vérifie ensuite si les deux utilisateurs de test peuvent établir une connexion.

Si aucun utilisateur de test n’a été défini, la commande échouera car elle ignore quels utilisateurs employer lors de l’exécution du test. Si vous n’avez pas défini d’utilisateurs de test pour un pool, vous devez inclure les paramètres SenderSipAddress et ReceiverSipAddress, ainsi que les informations d’identification correspondantes pour les utilisateurs intervenant dans cet échange de messages instantanés. L’applet de commande **Test-CsAVConference** effectue ensuite ses vérifications à l’aide des deux utilisateurs spécifiés.

    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent la capacité d’une paire d’utilisateurs (litwareinc\\pilar et litwareinc\\kenmyer) à se connecter à Lync Server puis à participer à une conférence A/V. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion litwareinc\\pilar ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur entre le mot de passe relatif au compte Pilar Ackerman). L’objet d’identification qui en résulte est ensuite stocké dans une variable appelée $cred1. La deuxième commande effectue la même action, en retournant cette fois un objet d’identification pour le compte de Ken Myer.

Avec ces deux objets d’identification, la troisième commande de l’exemple détermine si les deux utilisateurs peuvent ou non se connecter à Lync Server et participer à une conférence A/V. Afin d’effectuer cette tâche, l’applet de commande **Test-CsAVConference** est appelée avec les paramètres suivants : TargetFqdn (nom de domaine complet du pool de serveurs d’inscriptions) ; SenderSipAddress (adresse SIP du premier utilisateur de test) ; SenderCredential (objet Windows PowerShell contenant les informations d’identification de cet utilisateur) ; ReceiverSipAddress (adresse SIP du second utilisateur de test) et ReceiverCredential (objet Windows PowerShell contenant les informations d’identification du second utilisateur).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Description détaillée

L’applet de commande **Test-CsAVConference** est un exemple de « transaction synthétique ». Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide des comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide de deux comptes d’utilisateur (par opposition à un groupe de comptes de test) et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsAVConference** vérifie si deux utilisateurs de test peuvent établir une conférence audio/vidéo (A/V). Quand l’applet de commande est exécutée, les deux utilisateurs sont connectés au système. Après la connexion, le premier utilisateur crée une conférence audio/vidéo et attend que le second utilisateur se joigne à cette conférence. Après un bref échange de données, la conférence est supprimée et les deux utilisateurs de test sont déconnectés.

En réalité, l’applet de commande **Test-CsAVConference** n’établit pas de conférence audio/vidéo entre deux utilisateurs de test. L’applet de commande vérifie en fait que les deux utilisateurs parviennent à établir les connexions nécessaires au déroulement de la conférence A/V.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVConference"}

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification utilisateur du premier des deux comptes d’utilisateur à tester. La valeur transmise à ReceiverCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\pilar et le stocke dans une variable appelée $y :</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification du destinataire ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification du compte d’utilisateur du deuxième compte d’utilisateur à tester. La valeur transmise à SenderCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et stocke cet objet dans une variable appelée $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification de l’expéditeur ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Chaîne</p></td>
<td><p>Nom de domaine complet (FQDN) du pool à tester.</p></td>
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
<td><p>Chaîne</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Cette variable inclut deux méthodes, ToHTML et ToXML, qui permettent d’enregistrer cette sortie dans un fichier HTML ou XML.</p>
<p>Pour stocker la sortie dans la variable d’un journal $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Remarque : n’ajoutez pas de caractère $ en préfixe lorsque vous spécifiez le nom de la variable. Pour enregistrer les informations stockées dans la variable du journal dans un fichier HTML, utilisez une commande similaire à celle-ci :</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier XML, utilisez une commande telle que :</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Par exemple, pour stocker une sortie dans une variable appelée $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutVerboseVariable TestOutput</p>
<p>N’utilisez pas le caractère $ pour indiquer le nom de la variable.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du premier des deux comptes d’utilisateur à tester. Par exemple : -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Le paramètre ReceiverSipAddress doit se référer au même compte d’utilisateur que ReceiverCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du deuxième compte d’utilisateur à tester. Par exemple : -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre SenderSipAddress doit faire référence au même compte d’utilisateur que SenderCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Si vous définissez ce paramètre, il permet de tester la capacité du lanceur de participation à participer à une conférence. Le lanceur de participation est utilisé pour aider les utilisateurs d’appareils mobiles (et, par conséquent, les utilisateurs de Mobility Service) à participer à des conférences.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Test-CsAVConference** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Test-CsDialInConferencing](test-csdialinconferencing.md)

