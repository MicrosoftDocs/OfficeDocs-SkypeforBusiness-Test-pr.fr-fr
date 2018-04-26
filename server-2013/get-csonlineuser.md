---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994026(v=OCS.15)
ms:contentKeyID: 53095386
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les utilisateurs qui possèdent des comptes hébergés dans Microsoft Lync Online. Cette applet de commande ne peut être utilisée qu’avec Skype Entreprise Online.

## Syntaxe

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 renvoie des informations pour tous les utilisateurs configurés comme utilisateur en ligne.

    Get-CsOnlineUser

## Exemple 2

Dans l’exemple 2, les informations sont renvoyées pour un utilisateur en ligne unique : l’utilisateur avec l’adresse SIP « sip:kenmyer@litwareinc.com ».

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## Exemple 3

La commande présentée dans l’exemple 3 renvoie des informations pour tous les utilisateurs en ligne qui ont été activés pour Lync Online, mais ne sont pas affectés actuellement à un pool de serveur d’inscriptions.

    Get-CsOnlineUser -UnassignedUser

## Exemple 4

L’exemple 4 utilise le paramètre Filter pour limiter les données renvoyées aux utilisateurs en ligne auxquels la stratégie d’archivage utilisateur RedmondArchiving a été affectée. À cet effet, la valeur de filtre {ArchivingPolicy -eq "RedmondArchiving"} est employée. Cette syntaxe limite les données renvoyées aux utilisateurs lorsque la propriété ArchivingPolicy est égale à (-eq) "RedmondArchiving".

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## Exemple 5

L’exemple 5 renvoie des informations uniquement pour les comptes d’utilisateur configurés dans les listes d’adresses Microsoft Exchange. (C’est-à-dire, l’attribut Active Directory msExchHideFromAddressLists est défini sur True.) Pour exécuter cette tâche, le paramètre Filter est inclus avec la valeur de filtre {HideFromAddressLists -eq $True}.

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## Exemple 6

La commande présentée dans l’exemple 6 renvoie des informations pour tous les utilisateurs en ligne affectés au client dont le paramètre TenantID est « bf19b7db-6960-41e5-a139-2aa373474354 ». Pour exécuter cette tâche, la commande inclut le paramètre Filter avec la valeur de filtre {TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"}. Ce filtre limite les données renvoyées aux utilisateurs en ligne affectés au client « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## Description détaillée

L’applet de commande **Get-CsOnlineUser** renvoie des informations sur les utilisateurs possédant des comptes hébergés dans Microsoft Lync Online. Les informations renvoyées incluent des informations de compte Active Directory standard (comme le service dans lequel l’utilisateur travaille, son adresse et son numéro de téléphone, etc.), ainsi que des informations Lync Server spécifiques : l’applet de commande **Get-CsOnlineUser** renvoie des informations sur des éléments comme l’activation ou non de l’utilisateur pour Voix Entreprise et les stratégies utilisateur (le cas échéant) qui ont été affectées à l’utilisateur.

Notez que l’applet de commande **Get-CsOnlineUser** ne comporte pas de paramètre TenantId, ce qui signifie que vous ne pouvez pas utiliser de commande similaire à celle-ci pour limiter les données renvoyées aux utilisateurs possédant des comptes avec un client Lync Online spécifique :

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

Cependant, si vous possédez plusieurs clients Lync Online, vous pouvez renvoyer des utilisateurs à partir d’un client spécifique en utilisant le paramètre Filter et une commande similaire à celle-ci :

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

Cette commande limite les données renvoyées aux comptes d’utilisateur appartenant au client dont le paramètre TenantId est « bf19b7db-6960-41e5-a139-2aa373474354 ». Si vous ne connaissez pas vos ID client, vous pouvez renvoyer ces informations en utilisant cette commande :

    Get-CsTenant

Si vous possédez un déploiement hybride ou « à domaine séparé » (c’est-à-dire un déploiement dans lequel certains utilisateurs possèdent des comptes hébergés dans Lync Online tandis que d’autres utilisateurs possèdent des comptes hébergés sur une version locale de Lync Server), pensez que l’applet de commande **Get-CsOnlineUser** ne renvoie des informations que pour les utilisateurs de Lync Online. Cependant, l’applet de commande [Get-CsUser](get-csuser.md) renvoie des informations pour les utilisateurs de Lync Online et les utilisateurs de la version locale de Lync Server. Si vous souhaitez exclure les utilisateurs de Lync Online des données renvoyées par l’applet de commande **Get-CsUser**, utilisez la commande suivante :

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

Par définition, pour les utilisateurs hébergés dans la version locale de Lync Server, le paramètre TenantId est toujours égal à 00000000-0000-0000-0000-000000000000. Pour les utilisateurs hébergés dans Lync Online, il est égal à une valeur différente de 00000000-0000-0000-0000-000000000000.

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
<td><p><em>Credential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Vous permet d’exécuter l’applet de commande <strong>Get-CsOnlineUser</strong> sous d’autres informations d’identification. Cela peut être nécessaire si le compte que vous avez utilisé pour vous connecter à Windows ne dispose pas des privilèges nécessaires pour manipuler des objets Utilisateur.</p>
<p>Pour utiliser le paramètre Credential, vous devez d’abord créer un objet PSCredential à l’aide de l’applet de commande <strong>Get-Credential</strong>. Pour plus d’informations, consultez la rubrique d’aide relative à l’applet de commande <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vous permet de vous connecter au contrôleur de domaine spécifié afin d’extraire des informations sur l’utilisateur. Pour vous connecter à un contrôleur de domaine spécifique, incluez le paramètre DomainController suivi du nom de domaine complet (FQDN) (par exemple, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de limiter les données renvoyées en filtrant sur des attributs Lync Server spécifiques. Par exemple, vous pouvez limiter les données renvoyées aux utilisateurs auxquels une stratégie de voix spécifique a été attribuée ou aux utilisateurs auxquels aucune stratégie de voix spécifique n’a été attribuée.</p>
<p>Le paramètre -Filter utilise la même syntaxe de filtrage Windows PowerShell que l’applet de commande Where-Object. Par exemple, un filtre qui ne renvoie que les utilisateurs activés pour Voix Entreprise se présenterait comme ceci, avec EnterpriseVoiceEnabled représentant l’attribut Active Directory, -eq représentant l’opérateur de comparaison (equal to) et $True (variable Windows PowerShell intégré) représentant la valeur de filtre :</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indique l’identité du compte d’utilisateur à extraire. Les identités utilisateur peuvent être spécifiées dans l’un des quatre formats suivants : 1) L’adresse SIP de l’utilisateur ; 2) Le nom d’utilisateur principal de l’utilisateur ; 3) Le nom de domaine et le nom d’ouverture de session de l’utilisateur, sous la forme domaine\ouverture de session (par exemple, litwareinc\kenmyer) ; et 4) Le nom complet Active Directory de l’utilisateur (par exemple, Ken Myer). Vous pouvez également faire référence à un compte d’utilisateur en utilisant son nom unique Active Directory.</p>
<p>Vous pouvez recourir à l’astérisque (caractère générique *) si vous utilisez le nom complet comme identité utilisateur. Par exemple, l’identité « * Smith » renvoie tous les utilisateurs dont le nom complet se termine par la valeur de chaîne « Smith ».</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de limiter les données retournées en filtrant les attributs Active Directory génériques (c’est-à-dire les attributs qui ne sont pas spécifiques à Lync Server). Par exemple, vous pouvez limiter les données renvoyées aux utilisateurs qui travaillent dans un service donné ou aux utilisateurs rapportant à un supérieur ou occupant un poste spécifique.</p>
<p>Le paramètre LdapFilter utilise le langage de requête LDAP lors de la création des filtres. Par exemple, un filtre qui retourne uniquement les utilisateurs travaillant dans la ville de Redmond se présente comme suit : « l=Redmond », où « l » (soit un L minuscule) correspond à l’attribut Active Directory (localité), « = » correspond à l’opérateur de comparaison (égal à) et « Redmond » correspond à la valeur de filtre.</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Renvoie une collection d’utilisateurs hébergés sur Lync Server. Les utilisateurs disposant de comptes hébergés sur des versions antérieures du logiciel ne sont pas retournés lorsque vous utilisez ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retourne un ensemble d’utilisateurs hébergés sur une version antérieure de Lync Server (par exemple, Microsoft Office Communications Server 2007 R2). Les utilisateurs disposant de comptes hébergés sur la version actuelle du logiciel ne sont pas retournés lorsque vous utilisez ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Vous permet de retourner des informations sur les comptes d’utilisateur d’une unité d’organisation (OU) ou d’un conteneur spécifique. Le paramètre OU renvoie les données provenant de l’unité d’organisation (OU) spécifiée et de toutes ses unités d’organisation enfants. Par exemple, si l’unité d’organisation Finance compte deux unités d’organisation enfants, AccountsPayable et AccountsReceivable, les utilisateurs seront retournés par chacune de ces trois unités d’organisation.</p>
<p>Lors de la spécification d’une unité d’organisation (OU), utilisez le nom unique (DN) de ce conteneur. Par exemple : -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;. Pour renvoyer des comptes d’utilisateur à partir du conteneur Utilisateurs, utilisez cette syntaxe :</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Vous permet de limiter le nombre d’enregistrements retournés par l’applet de commande. Par exemple, pour retourner sept utilisateurs (quel que soit le nombre d’utilisateurs présents dans votre forêt), incluez le paramètre ResultSize et définissez sa valeur sur 7. Notez qu’il est impossible de savoir quels seront les sept utilisateurs retournés.</p>
<p>La taille des résultats peut être définie sur n’importe quel entier compris entre 0 et 2147483647 (inclus). Si le paramètre est défini sur 0, la commande sera exécutée, mais aucune donnée ne sera retournée. Si vous définissez ResultSize sur 7, mais que votre forêt ne compte que trois utilisateurs, la commande renverra ces trois utilisateurs et se terminera sans erreur.</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Permet de renvoyer un ensemble de tous les utilisateurs activés pour Lync Online, mais qui ne sont pas actuellement affectés à un pool de serveurs d’inscription. Les utilisateurs n’ont pas l’autorisation de se connecter sauf s’ils sont affectés à un pool de serveur d’inscriptions.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

L’applet de commande **Get-CsOnlineUser** accepte des instances redirigées de l’objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser, ainsi que des valeurs de chaîne représentant une identité de compte d’utilisateur valide (par exemple, « sip:kenmyer@litwareinc.com »).

## Types de retours

L’applet de commande **Get-CsOnlineUser** renvoie les instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser.

## Voir aussi

#### Autres ressources

[Get-CsUser](get-csuser.md)

