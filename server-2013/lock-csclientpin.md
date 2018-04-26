---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398650(v=OCS.15)
ms:contentKeyID: 49297908
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet à un administrateur d’empêcher un utilisateur de recourir à l’authentification par code confidentiel. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans l’exemple 1, l’applet de commande **Lock-CsClientPin** permet de verrouiller le code confidentiel de l’utilisateur kenmyer@litwareinc.com.

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## EXEMPLE 2

L’exemple 2 utilise l’applet de commande **Lock-CsClientPin** pour verrouiller les codes confidentiels de tous les utilisateurs auxquels est affecté un code confidentiel. Pour ce faire, la commande appelle l’applet de commande **Get-CsUser** qui retourne la collection de tous les utilisateurs activés pour Lync Server. La collection est ensuite redirigée vers l’applet de commande **Get-CsClientPinInfo**, utilisée, en liaison avec l’applet de commande **Where-Object**, pour retourner la collection des utilisateurs dont la propriété IsPinSet a la valeur True. Cette collection filtrée est ensuite redirigée vers l’applet de commande **Lock-CsClientPin**, qui verrouille le code confidentiel de chaque utilisateur de la collection.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## EXEMPLE 3

Dans l’exemple 3, l’applet de commande **Lock-CsClientPin** permet de verrouiller les codes confidentiels de tous les utilisateurs dont le code confidentiel a expiré. Pour exécuter cette tâche, l’applet de commande **Get-CsUser** est d’abord appelée pour retourner la collection de tous les utilisateurs activés pour Lync Server. Cette collection est ensuite redirigée vers l’applet de commande **Get-CsClientPinInfo** utilisée avec l’applet de commande **Where-Object** pour limiter la collection aux utilisateurs dont le code confidentiel a expiré. Pour identifier les utilisateurs dont le code confidentiel a expiré, l’applet de commande **Where-Object** recherche les comptes dont la valeur de la propriété PinExpirationTime (qui indique la date d’expiration du code confidentiel) est inférieure à la date actuelle. (La date actuelle est extraite avec l’applet de commande **Get-Date**.) Si la date d’expiration (par exemple September 1, 2010) est antérieure à la date actuelle (par exemple, September 2, 2010), cela signifie que le code confidentiel a expiré. Ensuite, l’applet de commande **Lock-CsClientPin** sert à verrouiller chaque code confidentiel ayant expiré.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## Description détaillée

Lync Server permet aux utilisateurs de se connecter au système ou de prendre part à des conférences PSTN (réseau téléphonique commuté) par téléphone. Généralement, la connexion au système ou la participation à une conférence nécessite que l’utilisateur saisisse un nom d’utilisateur ou un mot de passe. Néanmoins, la saisie d’un nom d’utilisateur et d’un mot de passe peut constituer un problème si vous utilisez un téléphone qui ne comporte pas de clavier alphanumérique. De ce fait, Lync Server vous permet de fournir aux utilisateurs des codes confidentiels uniquement numériques ; à l’invite, les utilisateurs peuvent ainsi se connecter au système ou prendre part à une conférence en saisissant le code confidentiel à la place d’un nom d’utilisateur et d’un mot de passe.

À des fins de sécurité, Lync Server permet de verrouiller le code confidentiel d’un utilisateur. Dans ce cas, l’utilisateur ne peut plus utiliser le code pour accéder au système ou participer à une conférence. (Toutefois, il peut toujours accéder au système et participer aux conférences en utilisant une application telle que Lync 2013 et en fournissant un nom d’utilisateur et un mot de passe.) Lorsqu’un code confidentiel est verrouillé, la seule manière de le restaurer (ainsi que les privilèges d’accès de l’utilisateur) consiste à demander à un administrateur de le déverrouiller. Cette opération peut être exécutée avec l’applet de commande **Unlock-CsClientPin**.

L’applet de commande **Lock-CsClientPin** permet aux administrateurs de désactiver temporairement l’accès d’un utilisateur au système au moyen de l’authentification par code confidentiel. Les codes confidentiels peuvent également être verrouillés par le système : si un utilisateur ne parvient pas à se connecter au système à plusieurs reprises, son code confidentiel est verrouillé automatiquement et un administrateur devra le déverrouiller.

Notez que, par défaut, les exceptions du pare-feu pour SQL Server Express ne sont pas activées quand vous installez l’édition standard de Lync Server. Cela signifie que vous ne pourrez pas exécuter l’applet de commande **Lock-CsClientPin** à partir d’une instance distante de Windows PowerShell. En effet, votre commande ne pourra pas traverser le pare-feu et accéder à la base de données SQL Server Express. (Vous pouvez toutefois exécuter l’applet de commande en local sur le serveur Standard Edition lui-même.) Pour exécuter l’applet de commande **Lock-CsClientPin** à distance, vous devrez activer manuellement les exceptions du pare-feu pour SQL Server Express.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Lock-CsClientPin** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identité du compte d’utilisateur pour lequel le code confidentiel doit être verrouillé. Les identités utilisateur peuvent être spécifiées dans l’un des quatre formats suivants : 1) L’adresse SIP de l’utilisateur ; 2) Le nom d’utilisateur principal de l’utilisateur ; 3) Le nom de domaine et le nom d’ouverture de session de l’utilisateur, sous la forme domaine\ouverture de session (par exemple, litwareinc\kenmyer) ; et 4) Le nom complet Active Directory de l’utilisateur (par exemple, Ken Myer). Vous pouvez également faire référence aux identités utilisateur en utilisant son nom unique Active Directory.</p>
<p>En outre, vous pouvez recourir à l’astérisque (caractère générique *) si vous utilisez le nom complet comme identité utilisateur. Par exemple, l’identité « * Smith » renvoie tous les utilisateurs dont le nom complet se termine par la valeur de chaîne « Smith ».</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Valeur de chaîne ou objet Microsoft.Rtc.Management.ADConnect.Schema.ADUser. L’applet de commande **Lock-CsClientPin** accepte une valeur de chaîne redirigée représentant l’identité d’un compte d’utilisateur. L’applet de commande accepte également l’entrée redirigée pour les objets utilisateur.

## Types de retours

L’applet de commande **Lock-CsClientPin** ne retourne aucune valeur ni aucun objet. Au lieu de cela, l’applet de commande configure une ou plusieurs instances de l’objet Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Voir aussi

#### Autres ressources

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

