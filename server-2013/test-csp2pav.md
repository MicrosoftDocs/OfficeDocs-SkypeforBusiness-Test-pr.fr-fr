---
title: Test-CsP2PAV
TOCTitle: Test-CsP2PAV
ms:assetid: acb01fb7-4685-4f38-a724-8c2ae8e0219a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412821(v=OCS.15)
ms:contentKeyID: 49298528
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsP2PAV

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste l’aptitude de deux utilisateurs à mener un appel audio/vidéo (A/V) d’égal à égal. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsP2PAV -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsP2PAV -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsP2PAV [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si deux utilisateurs de test préconfigurés peuvent se connecter au pool atl-cs-001.litwareinc.com, puis effectuer un appel audio/vidéo d’égal à égal. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande déterminera si les deux utilisateurs peuvent se connecter au système et, dans l’affirmative, s’ils sont en mesure d’engager une conversation dans le cadre d’un appel audio/vidéo.

Si aucun utilisateur de test n’a été défini, la commande échouera car elle ignore quels utilisateurs employer lors de l’exécution du test. Si vous n’avez pas défini d’utilisateurs de test pour un pool, vous devez inclure les paramètres SenderSipAddress et ReceiverSipAddress, ainsi que les informations d’identification correspondantes pour les utilisateurs intervenant dans cet échange de messages instantanés. L’applet de commande **Test-CsP2PAV** effectue ensuite ses vérifications à l’aide des deux utilisateurs spécifiés.

    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes de l’exemple 2 permettent de vérifier si deux utilisateurs (litwareinc\\pilar et litwareinc\\kenmyer) peuvent se connecter à Lync Server et établir un appel audio/vidéo d’égal à égal. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion litwareinc\\pilar ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur entre le mot de passe relatif au compte Pilar Ackerman). L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1. La deuxième commande remplit la même fonction, en renvoyant cette fois un objet d’identification pour le compte de l’utilisateur Ken Myer.

En utilisant les deux objets d’identification, la troisième commande décrite dans l’exemple détermine si les deux utilisateurs peuvent ou non se connecter à Lync Server et mener un appel audio/vidéo d’égal à égal. Pour réaliser cette tâche, l’applet de commande **Test-CsP2PAV** est appelée avec les paramètres suivants : TargetFqdn (nom de domaine complet du pool de serveurs d’inscriptions) ; SenderSipAddress (adresse SIP du premier utilisateur de test) ; SenderCredential (objet Windows PowerShell contenant les informations d’identification de cet utilisateur) ; ReceiverSipAddress (adresse SIP du second utilisateur de test) et ReceiverCredential (objet Windows PowerShell contenant les informations d’identification du second utilisateur de test).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Description détaillée

L’applet de commande **Test-CsP2PAV** est un exemple de « transaction synthétique » Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test), et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsP2PAV** permet de déterminer si deux utilisateurs test sont en mesure de participer à une conversation audio/vidéo (A/V) d’égal à égal. Afin de tester ce scénario, l’applet de commande connecte d’abord les deux utilisateurs à Lync Server. Si les deux connexions réussissent, le premier utilisateur invite alors le deuxième à participer à un appel audio/vidéo. Le deuxième utilisateur accepte l’appel, la connexion entre les deux utilisateurs est testée, puis l’appel est mené à son terme et enfin les utilisateurs de test sont déconnectés du système.

L’applet de commande **Test-CsP2PAV** ne réalise pas réellement un appel audio/vidéo et des données multimédias ne sont pas échangées entre les utilisateurs test. À la place, l’applet de commande vérifie simplement que les connexions appropriées peuvent être établies et que les deux utilisateurs sont en mesure de mener un appel de ce type.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsP2PAV"}

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
<td><p>Objet d’identification utilisateur du premier des deux comptes d’utilisateur à tester. La valeur transmise à ReceiverCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\pilar et le stocke dans une variable appelée $y :</p>
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
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du deuxième compte d’utilisateur à tester. Par exemple : -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre SenderSipAddress doit faire référence au même compte d’utilisateur que SenderCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsP2PAV** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **Test-CsP2PAV** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsAVConference](test-csavconference.md)

