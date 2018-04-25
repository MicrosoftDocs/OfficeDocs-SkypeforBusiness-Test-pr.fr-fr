---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398148(v=OCS.15)
ms:contentKeyID: 49296190
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la capacité d’un utilisateur à se connecter à Lync Server, à publier ses informations de présence et à souscrire à des informations de présence publiées par un deuxième utilisateur. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie si deux utilisateurs de test préconfigurés peuvent se connecter au pool atl-cs-001.litwareinc.com. Une fois les utilisateurs de test connectés, l’applet de commande **Test-CsPresence** vérifie ensuite si les deux utilisateurs peuvent échanger des informations de présence. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande détermine si le premier utilisateur de test peut se connecter au système, puis vérifie s’il peut échanger des informations de présence avec le deuxième utilisateur de test défini pour le pool.

Si un serveur d’inscriptions avancé n’a pas été défini, la commande échouera, car elle ignore quels utilisateurs employer lors de l’exécution du test. Si vous n’avez pas défini d’utilisateurs de test pour un pool, vous devez inclure les paramètres SubscriberSipAddress et PublisherSipAddress, ainsi que les informations d’identification correspondantes pour les utilisateurs faisant office d’abonnés aux données de présence et d’éditeurs des données de présence. L’applet de commande **Test-CsPresence** effectuera ensuite ses vérifications à l’aide des deux utilisateurs spécifiés.

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent la capacité de deux utilisateurs (litwareinc\\pilar et litwareinc\\kenmyer) à se connecter à Lync Server et à échanger des informations de présence. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman (le nom de connexion litwareinc\\pilar étant inclus comme paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell demande seulement à l’administrateur de saisir le mot de passe correspondant au compte de Pilar Ackerman). L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1. La deuxième commande remplit la même fonction, en renvoyant cette fois un objet d’identification pour le compte Ken Myer.

Avec les deux objets d’identification en main, la troisième commande décrite dans l’exemple détermine si les deux utilisateurs peuvent ou non se connecter à Lync Server et échanger des informations de présence. Pour exécuter cette tâche, l’applet de commande **Test-CsPresence** est appelée, avec les paramètres suivants : TargetFqdn (le nom de domaine complet du pool de serveurs d’inscriptions), SubscriberSipAddress (l’adresse SIP d’un utilisateur de test), SubscriberCredential (l’objet Windows PowerShell contenant les informations d’identification de ce même utilisateur), PublisherSipAddress (l’adresse SIP de l’autre utilisateur de test) et PublisherCredential (l’objet Windows PowerShell contenant les informations d’identification de cet autre utilisateur).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## Description détaillée

L’applet de commande **Test-CsPresence** est un exemple de transaction synthétique de Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier si les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs. Avec comptes d’utilisateur configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test), et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsPresence** est utilisé pour déterminer si une paire d’utilisateurs test peut se connecter à Lync Server, puis échanger des informations de présence. Pour ce faire, l’applet de commande connecte d’abord les deux utilisateurs au système. Si les deux connexions aboutissent, le premier utilisateur test demande à recevoir les informations de présence du deuxième utilisateur. Le deuxième utilisateur publie ces informations et l’applet de commande **Test-CsPresence** vérifie que les informations ont été correctement transmises au premier utilisateur. Une fois les informations de présence échangées, les deux utilisateurs test sont ensuite déconnectés de Lync Server.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification du premier compte d’utilisateur à tester. La valeur transmise à PublisherCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et le stocke dans une variable appelée $x :</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification de l’éditeur ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration de l’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification utilisateur du deuxième compte d’utilisateur à tester. La valeur transmise à SubscriberCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\pilar et le stocke dans une variable appelée $y :</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p>
<p>Les informations d’identification de l’abonné ne sont pas nécessaires si vous exécutez le test d’après les paramètres de configuration de l’analyse d’intégrité du pool.</p></td>
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
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du premier des deux comptes d’utilisateur à tester. Par exemple : -PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre PublisherSipAddress doit faire référence au même compte d’utilisateur que PublisherCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP du deuxième compte d’utilisateur à tester. Par exemple : -SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;. Le paramètre SubscriberSipAddress doit faire référence au même compte d’utilisateur que SubscriberCredential.</p>
<p>L’adresse SIP n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsPresence** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsPresence** renvoie une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsRegistration](test-csregistration.md)

