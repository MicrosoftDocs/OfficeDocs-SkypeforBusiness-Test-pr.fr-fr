---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412737(v=OCS.15)
ms:contentKeyID: 49298334
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la capacité d’un utilisateur à se connecter à Lync Server. L’applet de commande **Test-CsRegistration** est une « transaction synthétique » : une simulation des activités courantes de Lync Server utilisée pour l’analyse de l’intégrité et des performances. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 teste le service Serveur d’inscriptions du pool atl-cs-001.litwareinc.com. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si c’est le cas, la commande détermine si le premier utilisateur de test peut se connecter à Lync Server.

Si aucun utilisateur de test n’a pas été défini, la commande échoue car elle ne sait pas quel utilisateur employer pour la connexion. Si vous n’avez pas défini d’utilisateurs de test pour le pool, vous devez inclure le paramètre UserSipAddress et les informations d’identification de l’utilisateur que la commande doit utiliser pour la connexion.

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes indiquées dans l’exemple 2 testent la capacité d’un utilisateur spécifique (litwareinc\\pilar) à se connecter à Lync Server. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Pilar Ackerman. (Le nom de connexion litwareinc\\pilar ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur entre le mot de passe relatif au compte Pilar Ackerman). L’objet d’identification qui en résulte est ensuite stocké dans une variable appelée $cred1.

La deuxième commande vérifie ensuite si cet utilisateur peut se connecter au pool atl-cs-001.litwareinc.com. Afin d’effectuer cette tâche, l’applet de commande **Test-CsRegistration** est appelée avec trois paramètres : TargetFqdn (nom de domaine complet du pool de serveurs d’inscriptions), UserCredential (objet Windows PowerShell contenant les informations d’identification de Pilar Ackerman) et UserSipAddress (adresse SIP correspondant aux informations d’identification fournies).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## Description détaillée

L’applet de commande **Test-CsRegistration** est un exemple de « transaction synthétique » Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement conduites de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande CsHealthMonitoringConfiguration pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter simplement une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide de comptes de vrais utilisateurs. Ainsi, si deux utilisateurs ne peuvent pas échanger de messages instantanés, l’administrateur peut exécuter une transaction synthétique à l’aide des deux comptes d’utilisateur en question (et non à l’aide de comptes de test) afin de diagnostiquer et résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsRegistration** permet de vérifier que les utilisateurs de votre organisation parviennent à se connecter à Lync Server. Afin d’effectuer cette vérification, l’applet de commande **Test-CsRegistration** nécessite un compte de test unique. Si vous avez défini des utilisateurs de test pour le pool concerné, vous n’avez pas besoin de spécifier de compte. L’applet de commande **Test-CsRegistration** utilise en effet automatiquement le premier compte de test affecté au pool. (Pour plus d’informations, consultez la rubrique d’aide relative à l’applet de commande [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md).) Vous pouvez également effectuer le test à l’aide d’un compte qui n’a pas été affecté au pool. Ainsi, vous exécutez des tests même si n’avez pas configuré d’utilisateurs de test. Vous pouvez également tester la capacité d’un utilisateur spécifique à se connecter à Lync Server. (Si vous choisissez d’utiliser cette approche, vous devrez fournir le nom et le mot de passe de l’utilisateur du compte à tester.)

Quand vous exécutez l’applet de commande **Test-CsRegistration**, l’applet de commande tente de connecter l’utilisateur de test à Lync Server. Si l’opération réussit, elle déconnecte alors l’utilisateur du système. Ces actions sont effectuées sans interaction des utilisateurs et sans affecter ces derniers. Supposons, par exemple, que le compte de test sip:kenmyer@litwareinc.com correspond à un utilisateur bien réel possédant effectivement un compte Lync Server. Dans ces cas, le test sera effectué sans perturbation pour le vrai utilisateur Ken Myer. Lorsque le compte de test de Ken Myer se déconnecte du système, la personne Ken Myer reste connectée.

L’ajout du paramètre Verbose permet d’obtenir un compte détaillé de toutes les actions effectuées par l’applet de commande **Test-CsRegistration** afin de mener à bien le test.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p>Chaîne</p></td>
<td><p>Nom de domaine complet (FQDN) du pool à tester.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification du compte à tester. La valeur transmise à UserCredential doit être une référence d’objet obtenue par l’utilisation de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et stocke cet objet dans une variable appelée</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande. Ce paramètre n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Type d’authentification utilisé pendant le test. Les valeurs autorisées sont les suivantes :</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Par exemple, pour stocker une sortie dans une variable appelée $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutVerboseVariable TestOutput</p>
<p>N’utilisez pas le caractère $ pour indiquer le nom de la variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du compte d’utilisateur à tester, par exemple : -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Le paramètre UserSipAddress doit se référer au même compte d’utilisateur que UserCredential. Ce paramètre n’est pas obligatoire si vous exécutez le test d’après les paramètres de configuration d’analyse d’intégrité du pool.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsRegistration** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **Test-CsRegistration** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

