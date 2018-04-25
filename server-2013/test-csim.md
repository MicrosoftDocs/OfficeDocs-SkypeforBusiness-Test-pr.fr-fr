---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425802(v=OCS.15)
ms:contentKeyID: 49296763
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste l’aptitude de deux utilisateurs à échanger des messages instantanés. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si deux utilisateurs de test préconfigurés peuvent se connecter au pool atl-cs-001.litwareinc.com, puis échanger des messages instantanés. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande déterminera si les deux utilisateurs peuvent se connecter au système et, dans l’affirmative, s’ils sont en mesure d’échanger des messages instantanés.

Si aucun utilisateur de test n’a été défini, la commande échouera, car elle ignore quels utilisateurs employer lors de l’exécution du test. Si vous n’avez pas défini de serveur d’inscriptions avancé pour un pool, vous devez inclure les paramètres SenderSipAddress et ReceiverSipAddress, ainsi que les informations d’identification correspondantes pour les utilisateurs intervenant dans la session de messagerie instantanée. L’applet de commande **Test-CsIM** effectuera ensuite ses vérifications à l’aide des deux utilisateurs spécifiés.

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent la capacité de deux utilisateurs (litwareinc\\pilar et litwareinc\\kenmyer) à se connecter à Lync Server et à échanger des messages instantanés. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion litwareinc\\pilar étant inclus comme paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell demande seulement à l’administrateur de saisir le mot de passe correspondant au compte de Pilar Ackerman). L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1. La deuxième commande remplit la même fonction, en renvoyant cette fois un objet d’identification pour le compte de l’utilisateur Ken Myer.

Avec les deux objets d’identification en main, la troisième commande décrite dans l’exemple détermine si les deux utilisateurs peuvent ou non se connecter à Lync Server et échanger des messages instantanés. Pour ce faire, l’applet de commande **Test-CsIM** est appelé, avec les paramètres suivants : TargetFqdn (nom de domaine complet du pool de serveurs d’inscriptions), SenderSipAddress (adresse SIP de l’utilisateur 1), SenderCredential (objet Windows PowerShell contenant les informations d’identification de l’utilisateur 1), -ReceiverSipAddress (adresse SIP de l’utilisateur 2) et ReceiverCredential (objet Windows PowerShell contenant les informations d’identification de l’utilisateur 2).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Description détaillée

L’applet de commande **Test-CsIM** est un exemple de « transaction synthétique » de Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test) pour essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez fournir les informations d’identification de chaque utilisateur.

L’applet de commande **Test-CsIM** tente d’abord de connecter les deux utilisateurs à Lync Server. Si les deux connexions réussissent, l’applet de commande lance ensuite une session de messagerie instantanée entre les deux utilisateurs de test. (L’utilisateur 1 invite l’utilisateur 2 à une session de messagerie instantanée, l’utilisateur 2 accepte cette invitation.) Après avoir vérifié que les messages peuvent être échangés entre les deux utilisateurs, l’applet de commande **Test-CsIM** met fin à la session de messagerie instantanée et déconnecte les deux utilisateurs du système.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<td><p><em>EmailHost</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Hôte de messagerie électronique pour l’utilisateur employé dans le test Legal Intercept. Exemple :</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, spécifie que ce test est mené à l’aide du protocole SSL (Secure Socket Layer).</p></td>
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
<td><p><em>Password</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Mot de passe de l’employé dans le test Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>Facultatif</p></td>
<td><p>UInt16</p></td>
<td><p>Port utilisé pour le service Legal Intercept.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du premier des deux comptes d’utilisateur à tester. Par exemple : -ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;. Le paramètre ReceiverSipAddress doit faire référence au même compte d’utilisateur que ReceiverCredential.</p>
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
<td><p>Adresse SIP du deuxième compte d’utilisateur à tester. Par exemple : -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre SenderSipAddress doit faire référence au même compte d’utilisateur que SenderCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>S’il est utilisé, indique à Test-CsIM de tester le service Legal Intercept pour l’utilisateur spécifié.</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom d’utilisateur employé dans le test Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int16</p></td>
<td><p>Spécifie la durée d’attente (en secondes) du système avant la réponse du service Legal Intercept.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsIM** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsIM** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsGroupIM](test-csgroupim.md)

