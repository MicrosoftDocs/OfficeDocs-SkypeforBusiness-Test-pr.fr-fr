---
title: Test-CsAddressBookService
TOCTitle: Test-CsAddressBookService
ms:assetid: 8398c9ea-eaab-4a4d-9e09-473ea2b27e22
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398661(v=OCS.15)
ms:contentKeyID: 49297929
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService

 

_**Dernière rubrique modifiée :** 2015-03-09_

Vérifie si un utilisateur peut accéder au serveur qui héberge le service web de téléchargement des carnets d’adresses. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsAddressBookService -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Exemples

## EXEMPLE 1

L’exemple 1 teste le service web de téléchargement des carnets d’adresses du pool atl-cs-001.litwareinc.com. Cette commande teste le service web de téléchargement des carnets d’adresses à l’aide des utilisateurs de test préconfigurés pour le pool atl-cs-001.litwareinc.com.

    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

Les commandes illustrées dans l’exemple 2 testent également la disponibilité du serveur qui exécute le service web de téléchargement des carnets d’adresses. Dans ce cas toutefois, les commandes s’exécutent avec les informations d’identification de l’utilisateur Ken Myer (litwareinc\\kenmyer). Pour ce faire, la première commande utilise l’applet de commande **Get-Credential** pour créer un objet d’identification Windows PowerShell contenant le nom et le mot de passe de l’utilisateur Ken Myer. (le nom de connexion litwareinc\\kenmyer ayant été inclus en tant que paramètre, la boîte de dialogue Demande d’informations d’identification Windows PowerShell qui s’affiche exige uniquement que l’administrateur entre le mot de passe relatif au compte Ken Myer). L’objet d’identification qui en résulte est ensuite stocké dans une variable appelée $cred1.

Dans la seconde commande, l’applet de commande **Test-CsAddressBookService** est utilisée pour tester le service web de téléchargement des carnets d’adresses pour le pool atl-cs-001.litwareinc.com. Pour exécuter cette commande avec les informations d’identification de l’utilisateur Ken Myer, le paramètre UserCredential est défini avec la valeur $cred1. En outre, l’adresse SIP de Ken doit être fournie à l’aide du paramètre UserSipAddress.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com"

## EXEMPLE 3

L’exemple 3 explique comment tester le service web de téléchargement des carnets d’adresses pour atl-cs-001.litwareinc.com. Pour cela, l’applet de commande **Test-CsAddressBookService** est appelée conjointement avec deux paramètres : TargetUri, qui indique l’URI du service web de téléchargement des carnets d’adresses et UserSipAddress, qui contient l’adresse SIP Windows PowerShell du compte d’utilisateur employé pour le test.

``` 


Test-CsAddressBookService -TargetUri https://atl-cs-001.litwareinc.com/abs/handler -UserSipAddress "sip:kenmyer@litwareinc.com"
```

## Description détaillée

L’applet de commande **Test-CsAddressBookService** est un exemple de « transaction synthétique ». Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

Les transactions synthétiques sont généralement exécutées de deux manières. De nombreux administrateurs utiliseront les applets de commande **CsHealthMonitoringConfiguration** pour configurer des utilisateurs de test pour chacun de leurs pools de serveurs d’inscriptions. Ces utilisateurs de test sont un groupe de deux utilisateurs préconfigurés pour être utilisés avec des transactions synthétiques. (En règle générale, il s’agit de comptes de test et non de comptes appartenant à de réels utilisateurs.) Avec des utilisateurs de test configurés pour un pool, les administrateurs peuvent exécuter une transaction synthétique dans ce pool sans spécifier les identités (et saisir les informations d’identification) des comptes d’utilisateur impliqués dans le test.

Les administrateurs peuvent également exécuter une transaction synthétique à l’aide des comptes d’utilisateur réels. Par exemple, si deux utilisateurs ne parviennent pas à échanger des messages instantanés, un administrateur peut exécuter une transaction synthétique à l’aide de deux comptes d’utilisateur (par opposition à un groupe de comptes de test) et essayer de diagnostiquer et de résoudre le problème. Si vous décidez d’effectuer une transaction synthétique à l’aide de comptes d’utilisateur réels, vous devrez saisir les noms des utilisateurs et les mots de passe de chacun d’eux.

L’applet de commande **Test-CsAddressBookService** permet de vérifier qu’un utilisateur peut se connecter au service web de téléchargement des carnets d’adresses. Lorsque vous exécutez l’applet de commande, l’applet de commande **Test-CsAddressBookService** se connecte au service web de téléchargement des carnets d’adresses dans le pool défini et demande l’emplacement des fichiers du carnet d’adresses. Si le service web de téléchargement des carnets d’adresses fournit cet emplacement, alors la vérification aboutit. Si la demande est rejetée, cela signifie que la vérification a échoué.

Vous pouvez tester le service web de téléchargement des carnets d’adresses de deux manières : en testant le service lui-même ou en testant le service web associé.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsAddressBookService** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookService"}

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
<td><p>Nom de domaine complet du pool de serveurs d’inscriptions dans lequel le service web de téléchargement des carnets d’adresses doit être testé. Par exemple : -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Vous ne pouvez pas utiliser les paramètres TargetUri et TargetFqdn dans une même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>URI (Uniform Resource Identifier) du service de requête sur le web du carnet d’adresses. Par exemple : -TargetUri &quot;https://atl-cs-001.litwareinc.com/abs/handler&quot;.</p>
<p>Vous ne pouvez pas utiliser les paramètres TargetUri et TargetFqdn dans une même commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet d’identification utilisateur du compte d’utilisateur à utiliser dans la vérification. La valeur transmise à UserCredential doit être une référence d’objet obtenue à l’aide de l’applet de commande <strong>Get-Credential</strong>. Par exemple, ce code retourne un objet d’identification de l’utilisateur litwareinc\kenmyer et le stocke dans une variable appelée $x :</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
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
<td><p>Permet de vérifier que les utilisateurs externes peuvent utiliser le service web de téléchargement des carnets d’adresses.</p></td>
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
<td><p>String</p></td>
<td><p>Lorsqu’elle est définie, la sortie détaillée de l’exécution de l’applet de commande est stockée dans la variable spécifiée. Cette variable inclut deux méthodes, ToHTML et ToXML, qui permettent d’enregistrer cette sortie dans un fichier HTML ou XML.</p>
<p>Pour stocker la sortie dans la variable d’un journal $TestOutput, utilisez la syntaxe suivante :</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Remarque : n’utilisez pas le caractère $ pour indiquer le nom de la variable. Pour enregistrer les informations stockées dans la variable d’un journal dans un fichier HTML, utilisez une commande telle que :</p>
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
<td><p>Port SIP utilisé par le service Serveur d’inscriptions. Ce paramètre n’est pas obligatoire si le serveur d’inscriptions utilise le port par défaut 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Adresse SIP de l’utilisateur à utiliser lors du test. Si ce paramètre n’est pas spécifié, <strong>Test-CsAddressBookService</strong> effectue ses vérifications à l’aide du compte de l’utilisateur connecté.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet dans lequel sont stockées les informations d’identification de l’utilisateur lui permettant d’accéder au service Informations d’emplacement. Cet objet peut être récupéré en appelant l’applet de commande <strong>Get-Credential</strong> et en fournissant les informations d’identification appropriées.</p>
<p>Ce paramètre est requis si les paramètres TargetUri et UserSipAddress sont spécifiés, et si l’ordinateur sur lequel vous exécutez la commande n’a pas de certificat de serveur.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsAddressBookService** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsAddressBookService** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)  
[Update-CsAddressBook](update-csaddressbook.md)

