---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425962(v=OCS.15)
ms:contentKeyID: 49297137
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Effectue un test pour déterminer la stratégie d’emplacement qui sera utilisée en fonction des critères spécifiés dans les valeurs de paramétrage. Cette stratégie contient les paramètres qui décideront si Enhanced 9-1-1 (E9-1-1) doit être appliqué et comment il le sera. Le système E9-1-1 permet à des personnes répondant à des appels d’urgence de déterminer la position géographique de l’appelant. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## Exemples

## EXEMPLE 1

Cet exemple détermine la stratégie d’emplacement de l’utilisateur actuel (ou utilisateur configuré actuellement). TargetFqdn est obligatoire.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## EXEMPLE 2

La première ligne de l’exemple 2 est un appel vers l’applet de commande **Get-Credential** de Windows PowerShell. Cette applet de commande récupérera les informations d’identification de l’utilisateur et les renverra comme objet sécurisé. Le seul paramètre fourni pour cette applet de commande est l’ID utilisateur. Le fait d’exécuter cette applet de commande ouvre une boîte de dialogue préremplie avec l’ID utilisateur. Elle comporte en outre une zone de texte permettant de saisir le mot de passe de l’utilisateur. Les informations d’identification sont enregistrées dans la variable $cred.

La ligne 2 appelle l’applet de commande **Test-CsLocationPolicy**. Comme à l’exemple 1, nous fournissons le FQDN cible. Cependant, dans cet exemple, plutôt que d’utiliser l’utilisateur préconfiguré, nous allons effectuer le test de l’adresse SIP kenmyer@litwareinc.com. Nous transférons la valeur (avec le préfixe:SIP au paramètre UserSipAddress et les informations d’identification pour cet utilisateur (enregistrées dans la variable $cred) au paramètre UserCredential.

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## EXEMPLE 3

Cet exemple est similaire à l’exemple 2, mais sans informations d’identification spécifiées. Quand l’applet de commande **Test-CsLocationPolicy** est appelée sans informations d’identification, le certificat du serveur de l’ordinateur sur lequel cette applet de commande est exécutée est utilisé pour authentifier et mettre en évidence la stratégie d’emplacement de l’utilisateur. Si l’ordinateur n’a pas de certificat de serveur, vous devez spécifier des informations d’identification comme indiqué dans l’exemple 2. Pour savoir si l’ordinateur possède un certificat de serveur, appelez l’applet de commande **Get-CsCertificate**.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## EXEMPLE 4

Cet exemple détermine la stratégie d’emplacement du sous-réseau ID 172.15.11.0. Si le sous-réseau n’est pas associé à une stratégie d’emplacement, c’est la stratégie de l’utilisateur configuré actuellement qui sera récupérée.

Remarque : Une stratégie d’emplacement pour un sous-réseau se définit en configurant le paramètre LocationPolicy de l’applet de commande **Set-CsNetworkSite** avec l’identité de stratégie d’emplacement, puis en configurant le paramètre NetworkSiteId de l’applet de commande **Set-CsNetworkSubnet** avec l’identifiant de ce site. Par exemple :

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## Description détaillée

La stratégie d’emplacement est utilisée pour appliquer des paramètres liés à la fonctionnalité E9-1-1 et la position du client. La stratégie d’emplacement détermine si un utilisateur peut avoir recours au système E9-1-1 et, le cas échéant, quel est le comportement d’un appel d’urgence. Par exemple, la stratégie d’emplacement permet de définir le numéro d’appel d’urgence (911 aux États-Unis), de déterminer si le service de sécurité de l’entreprise doit être automatiquement averti et comment l’appel doit être acheminé. Cette applet de commande retourne les informations concernant la stratégie d’emplacement qui seront utilisées quand les appels seront effectués par un client spécifique sur un pool, un sous-réseau, un commutateur ou un point d’accès sans fil.

Si un utilisateur n’est pas spécifié lors de l’appel effectué vers cette applet de commande, un test effectué sur l’utilisateur configuré. Pour trouver les utilisateurs configurés actuellement, appelez l’applet de commande **Get-CsHealthMonitoringConfiguration**. Pour configurer les utilisateurs, appelez **Set-CsHealthMonitoringConfiguration**.

Le test est réussi quand une stratégie d’emplacement correspond à un utilisateur ou le sous-réseau. Les informations retournées par défaut incluent le nom de la stratégie d’emplacement (si une stratégie par utilisateur a été assignée) et l’activation, le cas échéant, de E9-1-1 pour l’utilisateur ou le sous-réseau. Incluez Verbose, le paramètre commun de Windows PowerShell, pour récupérer les informations supplémentaires concernant le test.

Vous pouvez tester les stratégies d’emplacement sur les utilisateurs ou les sous-réseaux. Si vous effectuez un test sur un sous-réseau (en spécifiant la valeur pour le paramètre de sous-réseau), l’applet de commande essaiera de résoudre la stratégie d’emplacement pour ce sous-réseau. Si aucune stratégie d’emplacement n’a été assignée au sous-réseau, c’est la stratégie d’emplacement de l’utilisateur configuré qui sera récupérée. Si la stratégie de sous-réseau a été récupérée avec succès, le résultat comprendra une valeur LocationPolicyTagID commençant par le label de sous-réseau. Si la stratégie d’emplacement pour le sous-réseau n’a pas été récupérée, LocationPolicyTagID commencera par l’identifiant de l’utilisateur.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsLocationPolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p>Nom de domaine complet (FQDN) du pool dans lequel l’utilisateur ou le sous-réseau spécifié est hébergé. (Si aucun utilisateur n’a été spécifié, c’est l’utilisateur actuel ou préconfiguré qui sera pris en compte).</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PSCredential</p></td>
<td><p>Objet contenant l’identificateur de l’utilisateur et le mot de passe du compte d’utilisateur pour lequel la politique d’emplacement a été testée. Un objet d’information d’identification peut être récupéré en appelant l’applet de commande <strong>Get-Credential</strong>, en fournissant les informations qui conviennent et en sauvegardant les résultats dans une variable.</p></td>
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
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
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
<td><p>Indique le numéro du port du service de serveur d’inscriptions.</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identificateur (ou l’adresse IP) du sous-réseau pour lequel vous voulez tester la politique d’emplacement.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>L’adresse SIP de l’utilisateur pour lequel vous voulez tester la stratégie d’emplacement. Elle doit être au format sip :&lt;id_utilisateur&gt;, par exemple, sip:kenmyer@litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Test-CsLocationPolicy** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

