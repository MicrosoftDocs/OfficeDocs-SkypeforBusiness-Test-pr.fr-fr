---
title: Connexion à Lync Online à l’aide de Windows PowerShell
TOCTitle: Connexion à Lync Online à l’aide de Windows PowerShell
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56269592
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connexion à Lync Online à l’aide de Windows PowerShell

 

_**Dernière rubrique modifiée :** 2017-03-03_

Une fois que vous avez installé les logiciels requis, vous pouvez commencer à utiliser Windows PowerShell pour gérer Skype Entreprise Online. Pour ce faire, commencez par ouvrir une instance standard de Windows PowerShell. Vous n’avez pas besoin d’ouvrir une instance spéciale de Windows PowerShell (semblable à Lync Server Management Shell), une application du Panneau de configuration ou un autre type spécial d’application. En effet, la gestion de Skype Entreprise Online est effectuée via une session à distance de Windows PowerShell. Ceci a les implications suivantes :

1.  Vous utilisez une session normale de Windows PowerShell pour vous connecter à Skype Entreprise Online. Lorsque vous vous connectez à distance, vous travaillez sur votre ordinateur local et vous utilisez votre copie locale de Windows PowerShell, mais vous gérez les objets détectés sur un système distant (Skype Entreprise Online).

2.  Les applets de commande, scripts et autres éléments requis pour gérer Skype Entreprise Online sont téléchargés sur votre ordinateur. Ces éléments sont conservés en mémoire et sont disponibles uniquement dans la session à distance établie avec Skype Entreprise Online. Il est important de s’en rappeler. Lorsque vous établissez une connexion à distance à Skype Entreprise Online, les applets de commande Skype Entreprise Online, telles que [Get-CsTenant](get-cstenant.md), sont copiées dans la mémoire de votre ordinateur. Vous pourrez exécuter ces applets de commande dans votre session à distance. Celles-ci sont toutefois disponibles uniquement dans cette session à distance. Par exemple, vous pouvez démarrer une deuxième session de Windows PowerShell, sans vous connecter à Skype Entreprise Online dans cette session. Si vous essayez d’exécuter l’applet de commande **Get-CsTenant** à partir de cette session, vous recevrez le message d’erreur suivant :
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    Notez également que la recherche de l’applet de commande **Get-CsTenant** (ou toute autre applet de commande Skype Entreprise Online) sur votre disque dur ne donnera pas de résultat. En effet, aucun élément n’est enregistré sur votre disque dur lorsque vous créez une session à distance.

3.  Lorsque vous fermez votre session à distance, les éléments téléchargés sont supprimés de la mémoire de votre ordinateur. Par exemple, vous pouvez démarrer une session à distance de Windows PowerShell avec l’applet de commande **Get-CsTenant**, puis fermer cette session. Si vous redémarrez Windows PowerShell, l’applet de commande **Get-CsTenant** n’est plus disponible. Pour accéder à l’applet de commande **Get-CsTenant**, vous devez vous reconnecter à Skype Entreprise Online.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous travaillez avec un déploiement hybride, vous devez suivre les procédures décrites dans l’article <a href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">Utilisation de Windows PowerShell dans un déploiement hybride</a>.</td>
</tr>
</tbody>
</table>


Pour créer une connexion à distance à Skype Entreprise Online, commencez par démarrer une nouvelle session de Windows PowerShell sur votre ordinateur local. Si vous exécutez Windows 7, Windows Server 2008 R2, Windows Server 2012 ou Windows Server 2012 R2, procédez comme suit :

  - Cliquez sur **Démarrer**, **Tous les programmes**, **Accessoires**, **Windows PowerShell**, puis sur **Windows PowerShell**.

Si vous exécutez Windows 8 ou 8.1, procédez plutôt comme suit :

  - Accédez à la barre des icônes, cliquez sur **Rechercher**, puis sur **Windows PowerShell**. Vous pouvez accéder rapidement à la barre des icônes sur n’importe quel ordinateur Windows 8 ou 8.1 (écran tactile ou non) en maintenant la touche Windows enfoncée et en appuyant sur C.

Une fois la console Windows PowerShell affichée, vous devez créer un objet d’identification utilisateur Windows PowerShell. Celui-ci permet de transmettre de façon sécurisée vos nom d’utilisateur et mot de passe à Skype Entreprise Online. Pour créer un objet d’identification utilisateur, tapez la commande suivante à l’invite Windows PowerShell, puis appuyez sur Entrée :

    $credential = Get-Credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans cet exemple, vos nom d’utilisateur et mot de passe sont stockés dans la variable $credential. Vous pouvez nommer cette variable comme vous le souhaitez, dès lors que vous respectez les règles de nom de variable pour Windows PowerShell. Vous devez toutefois utiliser un certain type de variable pour stocker les nom d’utilisateur et mot de passe, sans quoi l’objet d’identification utilisateur que vous créez disparaîtra dès sa création.</td>
</tr>
</tbody>
</table>


Lorsque vous appuyez sur Entrée, la boîte de dialogue **Informations d’identification Windows PowerShell** s’affiche :

![Informations d’identification pour la connexion Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Informations d’identification pour la connexion Windows PowerShell")

Dans la zone **Nom d’utilisateur**, tapez votre nom d’utilisateur Skype Entreprise Online. Dans la zone **Mot de passe**, tapez votre mot de passe Skype Entreprise Online (celui-ci est masqué et n’est pas visible à l’écran). Par exemple, si votre nom d’utilisateur est kenmyer@litwareinc.com et votre mot de passe p@ssw0rd\!, la boîte de dialogue ressemblera à ce qui suit :

![Connexion avec les informations d’identification Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Connexion avec les informations d’identification Windows PowerShell")

Pour créer l’objet d’identification utilisateur, cliquez sur **OK**. Si vous voulez vérifier la création de l’objet, tapez simplement le nom de la variable à l’invite Windows PowerShell, puis appuyez sur Entrée :

    $credential

Windows PowerShell affiche alors un contenu semblable au suivant :

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>N’oubliez pas que l’applet de commande <strong>Get-Credential</strong> accepte les informations d’identification que vous tapez sans chercher à vérifier si les nom d’utilisateur et mot de passe entrés sont corrects. Cette validation n’est effectuée que lorsque vous tentez de vous connecter à Skype Entreprise Online.</td>
</tr>
</tbody>
</table>


Une fois que vous avez créé l’objet d’identification utilisateur, vous pouvez ensuite créer une session Windows PowerShell à distance afin d’établir une connexion à Skype Entreprise Online. Pour ce faire, tapez la commande suivante à l’invite Windows PowerShell, puis appuyez sur Entrée :

    $session = New-CsOnlineSession -Credential $credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La variable $session permet de conserver des informations (dans le cas présent, des informations sur la connexion à Skype Entreprise Online). Là encore, vous pouvez attribuer le nom de votre choix à cette variable dès lors que celui-ci respecte les recommandations relatives aux noms de variable Windows PowerShell (par exemple, le nom ne doit pas inclure d’espaces vides ou de marques de ponctuation).</td>
</tr>
</tbody>
</table>


Veillez à taper la commande telle qu’elle est indiquée (avec l’exception possible du nom de variable). Le nom de votre domaine Skype Entreprise Online n’a pas d’importance. Quel qu’il soit, l’applet de commande **New-CsOnlineSession** vous connecte à Office 365 et ouvre une session à l’aide des informations dֹ’identification fournies. Une fois la connexion établie et l’authentification effectuée, vous êtes redirigé automatiquement vers l’URI approprié sur la base des informations d’identification fournies.

Si la connexion est correctement établie, des messages semblables à ce qui suit sont affichés dans la console Windows PowerShell :

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

Vous ne pouvez pas encore utiliser Windows PowerShell pour gérer Skype Entreprise Online, pour autant. L’applet de commande **New-CsOnlineSession** se connecte à Skype Entreprise Online et crée automatiquement une session. Vous devez ensuite importer la nouvelle session dans la console Windows PowerShell. Pour ce faire, exécutez la commande suivante :

    Import-PSSession $session

Lorsque vous appuyez sur Entrée, une jauge de progression semblable à la suivante est affichée dans la console Windows PowerShell :

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

À ce stade, Windows PowerShell télécharge les applets de commande et d’autres éléments requis pour gérer Skype Entreprise Online. Une fois le téléchargement terminé, des informations semblables à celles-ci sont affichées dans la console Windows PowerShell :

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

Vous pouvez dès lors commencer à utiliser Windows PowerShell pour gérer Skype Entreprise Online. Pour vérifier que le téléchargement a réussi et afficher les applets de commande Skype Entreprise Online disponibles, vous devez commencer par déterminer le nom du module Windows PowerShell temporaire qui contient les applets de commande Skype Entreprise Online. Pour ce faire, exécutez cette commande à partir de l’invite Windows PowerShell :

    Get-Module

Des informations semblables à ce qui suit sont affichées à l’écran :

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Le module de type Script contient les applets de commande Skype Entreprise Online. Pour retourner la liste de ces applets de commande, exécutez l’applet de commande **Get-Command** en utilisant le nom du module Script comme nom de module :

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell doit ensuite afficher la liste des applets de commande Skype Entreprise Online.

Une fois que vous avez terminé vos tâches de gestion, vous devez toujours exécuter la commande suivante avant de fermer la console Windows PowerShell :

    Remove-PSSession $session

L’applet de commande **Remove-PSSession** vous déconnecte de Skype Entreprise Online et ferme la session à distance. Si vous tentez de réimporter la session (en exécutant l’applet de commande **Import-PSSession**), vous recevrez le message d’erreur suivant :

    Import-PSSession : State of runspace is not valid for this operation.

Ce message indique simplement que vous devez créer une session pour vous reconnecter à Skype Entreprise Online.

Si vous oubliez de supprimer la session avant de fermer la console Windows PowerShell (ou si la console se ferme de façon inattendue), rien de grave ne survient. Après 15 minutes d’inactivité, la session se déconnecte automatiquement. Toutefois, chaque administrateur Skype Entreprise Online n’est autorisé à utiliser que trois connexions simultanées à Skype Entreprise Online par défaut. Si vous fermez la console Windows PowerShell sans supprimer la session, cette session fermée compte toujours comme une connexion, même si elle n’est pas utilisée à ce moment (elle continue de compter pour une connexion jusqu’à son expiration). Par exemple, supposons que vous ouvrez et fermez la console Windows PowerShell à trois reprises, sans supprimer la session Skype Entreprise Online à chaque fois. Si vous ouvrez Windows PowerShell et essayez d’établir une quatrième connexion, votre commande est bloquée et aucune connexion n’est établie.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si Windows PowerShell reste en attente en essayant d’établir une connexion, appuyez sur Ctrl+C pour terminer la commande bloquée.</td>
</tr>
</tbody>
</table>


Si les administrateurs individuels ne peuvent avoir que trois connexions simultanées à un client Skype Entreprise Online, une organisation peut avoir jusqu’à neuf connexions simultanées. Trois administrateurs peuvent donc avoir trois connexions simultanées chacun, ou neuf administrateurs une connexion à Skype Entreprise Online, etc. Là encore, aucun administrateur ne peut avoir plus de trois sessions actives.

## Voir aussi

#### Concepts

[Configuration de votre ordinateur pour la gestion de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

