---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399013(v=OCS.15)
ms:contentKeyID: 49299154
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**Dernière rubrique modifiée :** 2015-03-09_

L’applet de commande **Test-CsDialInConferencing** vérifie si un utilisateur peut participer à une session de conférence rendez-vous. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 vérifie qu’un utilisateur de test préconfiguré peut participer à une conférence rendez-vous sur le pool atl-cs-001.litwareinc.com. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande détermine si le premier utilisateur de test peut se connecter à Lync Server.

Si les utilisateurs de test n’ont pas été définis, la commande échoue car elle ne sait pas sous quel utilisateur se connecter. Si vous n’avez pas défini d’utilisateurs de test pour le pool, vous devez inclure le paramètre UserCredential et les informations d’identification de l’utilisateur que la commande doit utiliser pour se connecter.

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes présentées dans l’exemple 2 vérifient la capacité d’un utilisateur spécifique (litwareinc\\pilar) à participer à une conférence rendez-vous sur le pool atl-cs-001.litwareinc.com. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion litwareinc\\pilar étant inclus comme paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell demande seulement à l’administrateur de saisir le mot de passe correspondant au compte de Pilar Ackerman.) L’objet d’identification résultant est ensuite stocké dans une variable appelée $cred1.

La deuxième commande vérifie ensuite si l’utilisateur Pilar Ackerman peut se connecter au pool atl-cs-001.litwareinc.com et participer ensuite à une conférence rendez-vous. Afin d’effectuer cette tâche, l’applet de commande **Test-CsDialInConferencing** est appelée avec trois paramètres : TargetFqdn (nom de domaine complet du pool de serveurs d’inscriptions) ; UserCredential (objet Windows PowerShell contenant les informations d’identification de Pilar Ackerman) ; et UserSipAddress (adresse SIP correspondant aux informations d’identification fournies).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## Description détaillée

L’applet de commande **Test-CsDialInConferencing** est un exemple de « transaction synthétique » dans Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide des comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (par opposition à un groupe de comptes de test), et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsDialInConferencing** essaie de connecter un utilisateur de test au système. (Si vous utilisez des utilisateurs de test, l’applet de commande **Test-CsDialInConferencing** se servira du premier compte de test configuré pour ce pool). Si l’ouverture de session réussit, l’applet de commande utilise alors les informations d’identification et les autorisations de l’utilisateur pour essayer les numéros disponibles d’accès à la conférence rendez-vous. Le succès ou l’échec de chaque tentative de connexion est consigné, puis l’utilisateur de test est déconnecté de Lync Server.

L’applet de commande **Test-CsDialInConferencing** vérifie uniquement que les connexions appropriées peuvent être effectuées. L’applet de commande ne passe pas réellement d’appels téléphoniques ou ne crée pas de conférences rendez-vous que d’autres utilisateurs peuvent rejoindre.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsDialInConferencing** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p>System.String</p></td>
<td><p>Nom de domaine complet (FQDN) du pool à tester.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Objet d’identification du compte utilisateur à tester. La valeur transmise à UserCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et stocke cet objet dans une variable appelée $x :</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande. Ce paramètre n’est pas requis si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>Type d’authentification utilisé pendant le test. Les valeurs autorisées sont les suivantes :</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Cette variable inclut deux méthodes, ToHTML et ToXML, qui permettent d’enregistrer cette sortie dans un fichier HTML ou XML.</p>
<p>Pour stocker la sortie dans la variable d’un journal $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Remarque : n’ajoutez pas de caractère $ en préfixe lorsque vous spécifiez le nom de la variable. Pour enregistrer les informations stockées dans la variable du journal dans un fichier HTML, utilisez une commande similaire à celle-ci :</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier XML, utilisez une commande telle que :</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Par exemple, pour stocker une sortie dans une variable appelée $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutVerboseVariable TestOutput</p>
<p>N’utilisez pas le caractère $ pour indiquer le nom de la variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Numéro de téléphone pour un téléphone PSTN qui sera utilisé pour vérifier que les utilisateurs PSTN peuvent participer à la conférence rendez-vous. Exemple :</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>Notez que TargetPstnPhoneNumber doit uniquement être inclus lorsque vous utilisez le paramètre VerifyConferenceJoinType.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Adresse SIP du compte d’utilisateur à tester. Par exemple : -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre UserSipAddress doit se référer au même compte d’utilisateur que UserCredential. Ce paramètre n’est pas requis si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité.</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, vérifie qu’il est possible d’accéder à la conférence rendez-vous à l’aide d’un téléphone PSTN. Lorsque vous effectuez ce test, vous pouvez éventuellement inclure TargetPstnPhoneNumber. Dans ce cas, TargetPstnPhoneNumber doit spécifier le téléphone PSTN à utiliser pour participer à la conférence. Si TargetPstnPhoneNumber n’est pas inclus, l’applet de commande <strong>Test-CsDialInConferencing</strong> utilise les numéros de téléphone de la conférence rendez-vous affectés au préalable à la région de conférence rendez-vous appropriée.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsDialInConferencing** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsDialInConferencing** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsAVConference](test-csavconference.md)

