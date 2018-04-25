---
title: Test-CsAddressBookWebQuery
TOCTitle: Test-CsAddressBookWebQuery
ms:assetid: 9753dcba-83b3-437b-98f0-2806305a5bbb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398773(v=OCS.15)
ms:contentKeyID: 49298184
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookWebQuery

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste la capacité d’un utilisateur à rechercher et retourner des informations depuis le carnet d’adresses à l’aide du service de requête sur le web du carnet d’adresses. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsAddressBookWebQuery -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TargetSipAddress <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 teste le service de requête sur le web du carnet d’adresses pour le pool atl-cs-001.litwareinc.com en recherchant le contact dont l’adresse SIP est sip:kenmyer@litwareinc.com. Cette commande ne fonctionne que si des utilisateurs de test ont été définis pour le pool atl-cs-001.litwareinc.com. Si tel est le cas, la commande s’exécute en utilisant les informations d’identification du premier utilisateur de test défini pour le pool.

Si aucun utilisateur de test n’a été défini, la commande échoue. Si vous n’avez pas défini d’utilisateurs de test pour le pool, vous devez inclure le paramètre UserSipAddress et les informations d’identification de l’utilisateur employé pour l’exécution de la commande.

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com  -TargetSipAddress "sip:kenmyer@litwareinc.com"

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent également la disponibilité du service de requête sur le web du carnet d’adresses. Dans ce cas toutefois, les commandes s’exécutent avec les informations d’identification de l’utilisateur Ken Myer (litwareinc\\kenmyer). Pour ce faire, la première commande utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Ken Myer. (Le nom de connexion litwareinc\\kenmyer étant inclus comme paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell demande seulement à l’administrateur de saisir le mot de passe correspondant au compte de Ken Myer.) L’objet d’identification qui en résulte est ensuite stocké dans une variable appelée $cred1.

Dans la seconde commande, l’applet de commande **Test-CsAddressBookWebQuery** est utilisée pour tester le service de requête sur le web du carnet d’adresses pour le pool atl-cs-001.litwareinc.com. Pour exécuter cette commande avec les informations d’identification de l’utilisateur Ken Myer, le paramètre UserCredential est défini avec la valeur $cred1. La commande utilise également TargetSipAddress afin d’indiquer à l’applet de commande qu’elle doit rechercher dans le carnet d’adresses le contact dont l’adresse SIP est sip:kenmyer@litwareinc.com.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## EXEMPLE 3

L’exemple 3 explique comment tester le service de requête sur le web du carnet d’adresses pour le pool atl-cs-001.litwareinc.com. Pour ce faire, l’applet de commande **Test-CsAddressBookWebQuery** est d’abord appelée avec trois paramètres : TargetUri, qui indique l’URI du service de requête sur le web du carnet d’adresses, UserSipAddress, qui contient l’adresse SIP Windows PowerShell du compte d’utilisateur employé pour le test et TargetSipAddress, qui contient l’adresse SIP du compte d’utilisateur recherché.

    Test-CsAddressBookWebQuery -TargetUri https://atl-cs-001.litwareinc.com/groupexpansion -UserSipAddress "sip:packerman@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## Description détaillée

L’applet de commande **Test-CsAddressBookWebQuery** est un exemple de « transaction synthétique ». Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement effectuées de deux manières différentes. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide des comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide de deux comptes d’utilisateur (par opposition à un groupe de comptes de test) et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsAddressBookWebQuery** permet aux administrateurs de vérifier que les utilisateurs peuvent utiliser le service de requête sur le web du carnet d’adresses afin d’y rechercher un contact spécifique. Lorsqu’elle est exécutée, l’applet de commande **Test-CsAddressBookWebQuery** se connecte d’abord au service de ticket sur le web afin d’être authentifié. Si l’authentification réussit, l’applet de commande se connecte ensuite au service de requête sur le web du carnet d’adresses et recherche le contact indiqué. Si le contact est trouvé, l’applet de commande tente ensuite de transmettre cette information à l’ordinateur local. Le test n’est marqué comme étant réussi que si ces étapes ont été effectuées.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookWebQuery"}

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
<td><p>Nom de domaine complet du pool de serveurs d’inscriptions dans lequel le service de requête sur le web du carnet d’adresses doit être testé. Par exemple : -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Notez que vous ne pouvez pas utiliser les paramètres TargetUri et TargetFqdn dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Chaîne</p></td>
<td><p>URI (Uniform Resource Identifier) du service de requête sur le web du carnet d’adresses. Par exemple : -TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;.</p>
<p>Notez que vous ne pouvez pas utiliser les paramètres TargetUri et TargetFqdn dans la même commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification du compte d’utilisateur à utiliser dans le test. La valeur transmise à UserCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification pour l’utilisateur litwareinc\kenmyer et stocke cet objet dans une variable appelée</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Vous devez saisir le mot de passe de l’utilisateur lors de l’exécution de cette commande.</p></td>
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
<td><p><em>External</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Permet de vérifier que les utilisateurs externes peuvent utiliser le service de requête sur le web du carnet d’adresses.</p></td>
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
<td><p>Chaîne</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Par exemple, pour stocker une sortie dans une variable appelée $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutVerboseVariable TestOutput</p>
<p>N’utilisez pas le caractère $ pour indiquer le nom de la variable.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du contact devant être retournée par le service de requête sur le web du carnet d’adresses. Par exemple : -TargetSipAddress &quot;sip:kenmyer@litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP de l’utilisateur à utiliser lors du test. Si ce paramètre n’est pas indiqué, l’applet de commande <strong>Test-CsAddressBookWebQuery</strong> effectue ses vérifications en utilisant les paramètres de configuration d’analyse d’intégrité du pool en cours de test.</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet dans lequel sont stockées les informations d’identification de l’utilisateur lui permettant d’accéder au service Informations d’emplacement. Cet objet peut être récupéré en appelant l’applet de commande <strong>Get-Credential</strong> et en fournissant les informations d’identification appropriées.</p>
<p>Ce paramètre est requis si les paramètres TargetUri et UserSipAddress sont spécifiés, et si l’ordinateur sur lequel vous exécutez la commande n’a pas de certificat de serveur.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsAddressBookWebQuery** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **Test-CsAddressBookWebQuery** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Update-CsAddressBook](update-csaddressbook.md)

