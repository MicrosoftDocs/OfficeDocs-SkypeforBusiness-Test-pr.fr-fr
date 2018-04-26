---
title: Gestion de Lync Online et Microsoft Exchange à partir de la même session Windows PowerShell à distance
TOCTitle: Gestion de Lync Online et Microsoft Exchange à partir de la même session Windows PowerShell à distance
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56269580
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion de Lync Online et Microsoft Exchange à partir de la même session Windows PowerShell à distance

 

_**Dernière rubrique modifiée :** 2015-06-22_

Votre abonnement à Office 365 vous permet non seulement d’accéder à Skype Entreprise Online, mais aussi à Exchange Online. Vous pouvez utiliser une session à distance de Windows PowerShell pour gérer Skype Entreprise Online. Vous pouvez également utiliser une session à distance de Windows PowerShell pour gérer Exchange. Skype Entreprise Online et Exchange Online n’utilisent toutefois pas le même URI, ni la même méthode de connexion. Vous devez donc utiliser des sessions distinctes pour gérer Skype Entreprise Online et Exchange. Y’a-t-il une autre façon de gérer les deux produits à l’aide d’une seule session à distance de Windows PowerShell ?

Il s’avère que non seulement vous ne pouvez pas gérer les deux produits à partir de la même instance de Windows PowerShell, mais que la configuration de cette double session de gestion est relativement simple. Pour commencer, démarrez Windows PowerShell et connectez-vous à Skype Entreprise Online comme vous le faites habituellement : créez un objet d’identification utilisateur, puis une session se connectant à Skype Entreprise Online :

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

Utilisez ensuite un processus similaire pour vous connecter à Exchange Online. Notez que vous n’avez pas besoin de créer un objet d’identification utilisateur. Vous pouvez continuer à utiliser le même objet ($credential) que vous avez utilisé pour la connexion à Skype Entreprise Online :

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

Vous devez toujours utiliser l’URI https://outlook.office365.com/powershell-liveid/ lorsque vous vous connectez à Exchange Online, quel que soit votre URI Office 365 par ailleurs. Une fois que vous êtes authentifié, vous serez automatiquement redirigé vers l’URI approprié. Il est donc particulièrement important d’inclure le paramètre AllowRedirection. Si ce paramètre est omis, vous serez authentifié, mais la redirection échouera et vous ne serez pas connecté à Exchange Online :

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

À ce stade, deux sessions à distance distinctes doivent être exécutées sur votre ordinateur. Pour le vérifier, tapez la commande suivante à partir de l’invite Windows PowerShell :

    Get-PSSession

Des informations semblables à celles-ci doivent s’afficher à l’écran :

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

Vous avez à présent deux sessions à distance pouvant être importées dans votre session locale de Windows PowerShell. Pour ce faire, exécutez ces deux commandes :

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

À ce stade, vous devez pouvoir utiliser les applets de commande Skype Entreprise Online et Exchange Online. Pour le vérifier, exécutez la commande suivante et assurez-vous de recevoir les informations sur les utilisateurs :

    Get-CsOnlineUser -ResultSize 1

Exécutez ensuite la commande Exchange suivante et vérifiez que vous recevez les informations sur les boîtes aux lettres :

    Get-Mailbox -ResultSize 1

Lorsque vous voulez mettre fin à votre session de gestion, veillez à fermer les deux sessions à distance :

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## Voir aussi

#### Concepts

[Configuration de votre ordinateur pour la gestion de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

