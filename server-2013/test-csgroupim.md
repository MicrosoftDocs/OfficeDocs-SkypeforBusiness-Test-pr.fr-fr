---
title: Test-CsGroupIM
TOCTitle: Test-CsGroupIM
ms:assetid: 1e73fd7a-5727-4688-8d4c-a3107c3985e9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398273(v=OCS.15)
ms:contentKeyID: 49296452
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupIM

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la capacité de deux utilisateurs à organiser une conférence de messagerie instantanée. L’applet de commande **Test-CsGroupIM** est une « transaction synthétique » : une simulation des opérations courantes de Lync Server utilisées pour l’analyse du fonctionnement et des performances. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsGroupIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si une paire d’utilisateurs de test préconfigurés peut se connecter au pool atl-cs-001.litwareinc.com et participer à une conférence de messagerie instantanée. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande déterminera si les deux utilisateurs peuvent se connecter au système, puis vérifie s’ils peuvent participer à une conférence de messagerie instantanée.

Si aucun utilisateur de test n’a été défini, la commande échouera, car elle ignore quels utilisateurs employer lors de l’exécution du test. Si vous n’avez pas défini d’utilisateurs de test pour un pool, vous devez inclure les paramètres SenderSipAddress et ReceiverSipAddress, ainsi que les informations d’identification correspondantes pour les utilisateurs intervenant dans cet échange de messages instantanés. L’applet de commande **Test-CsGroupIM** effectuera ensuite ses vérifications à l’aide des deux utilisateurs spécifiés.

    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent la capacité d’une paire d’utilisateurs (litwareinc\\pilar et litwareinc\\kenmyer) à se connecter à Lync Server et à participer à une conférence de messagerie instantanée. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion, litwareinc\\pilar, ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur saisisse le mot de passe relatif au compte Pilar Ackerman). L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1. La deuxième commande remplit la même fonction, en renvoyant cette fois un objet d’identification pour le compte Ken Myer.

Avec ces deux objets d’identification, la troisième commande de l’exemple détermine si les deux utilisateurs peuvent ou non se connecter à Lync Server et participer à une conférence de messagerie instantanée. Pour exécuter cette tâche, l’applet de commande **Test-CsGroupIM** est appelée, ainsi que les paramètres suivants : TargetFqdn (le nom de domaine complet du pool de serveurs d’inscriptions), SenderSipAddress (l’adresse SIP du premier utilisateur), SenderCredential (les informations d’identification du premier utilisateur), ReceiverSipAddress (l’adresse SIP du deuxième utilisateur) et ReceiverCredential (les informations d’identification du deuxième utilisateur).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Description détaillée

L’applet de commande **Test-CsGroupIM** est un exemple de transaction synthétique de Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test), et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les informations d’identification de chaque utilisateur.

L’applet de commande **Test-CsGroupIM** vous permet de vérifier que les utilisateurs de votre organisation peuvent organiser des conférences. L’applet de commande **Test-CsGroupIM** requiert deux comptes d’utilisateur pour effectuer ses tests. Si vous avez configuré des utilisateurs de test pour le pool sur lequel le test doit être effectué, il n’est pas nécessaire de spécifier ces comptes. Au lieu de cela, l’applet de commande **Test-CsGroupIM** utilisera automatiquement les comptes affectés au serveur d’inscriptions d’analyse d’intégrité. (Pour plus d’informations, consultez la rubrique d’aide [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md).) Vous pouvez également effectuer le test à l’aide de comptes autres que ceux affectés au serveur d’inscriptions. Vous pouvez ainsi exécuter des tests, même si vous n’avez pas configuré d’utilisateurs de test pour le pool. De plus, vous pouvez tester la capacité de deux utilisateurs donnés à organiser une conférence. Si vous choisissez cette approche, vous devrez saisir le nom d’utilisateur et le mot de passe de ces utilisateurs.

Lorsque vous exécutez l’applet de commande **Test-CsGroupIM**, l’applet de commande tente d’authentifier les deux utilisateurs test sur Lync Server. Si l’opération réussit, **Test-CsGroupIM** crée une nouvelle conférence à l’aide du premier utilisateur test, puis invite le deuxième utilisateur à participer à la conférence. Après un échange de messages, les deux utilisateurs sont déconnectés du système. Tout cela se passe sans aucune intervention de l’utilisateur et ce, sans affecter aucun utilisateur. Supposez par exemple que le compte de test sip:kenmyer@litwareinc.com corresponde à un vrai utilisateur possédant un vrai compte Lync Server. Dans ce cas, le test sera effectué sans interrompre les activités de l’utilisateur réel Ken Myer. Par exemple, même si le compte de test Ken Myer se déconnecte du système Ken Myer, l’utilisateur restera connecté. De même, le compte réel Ken Myer ne recevra pas d’invitation à participer à la conférence. Cette invitation sera envoyée au compte de test et acceptée par ce dernier.

L’ajout du paramètre Verbose vous permet d’obtenir un compte détaillé de toutes les actions effectuées par l’applet de commande **Test-CsGroupIM** pour terminer son test.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupIM"}

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
<td><p>Objet d’identification du premier compte d’utilisateur à tester. La valeur transmise à ReceiverCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\pilar et le stocke dans une variable appelée $y :</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification du destinataire ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification utilisateur du deuxième compte d’utilisateur à tester. La valeur transmise à SenderCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et le stocke dans une variable appelée $x :</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification de l’expéditeur ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Nom de domaine complet (FQDN) du pool à tester.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
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
<td><p>String</p></td>
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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du premier des deux comptes d’utilisateur à tester. Par exemple : -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Le paramètre ReceiverSipAddress doit se référer au même compte d’utilisateur que ReceiverCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du deuxième compte d’utilisateur à tester. Par exemple : -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre SenderSipAddress doit faire référence au même compte d’utilisateur que SenderCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>S’il est présent, teste la capacité du lanceur de participation à participer à une conférence A/V. Le lanceur de participation est utilisé pour aider les utilisateurs d’appareils mobiles (et, par conséquent, les utilisateurs du service Mobility Service) à participer à des conférences.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsGroupIM** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsGroupIM** renvoie une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsIM](test-csim.md)

