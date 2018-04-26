---
title: Connexion automatique à Lync Online au démarrage de Windows PowerShell
TOCTitle: Connexion automatique à Lync Online au démarrage de Windows PowerShell
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56269600
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connexion automatique à Lync Online au démarrage de Windows PowerShell

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si vous ne vous souvenez pas de toutes les commandes requises pour vous connecter à Skype Entreprise Online, vous pouvez définir une configuration grâce à laquelle il vous suffira de double-cliquer sur un fichier de raccourci et d’entrer votre mot de passe Skype Entreprise Online pour vous connecter à Skype Entreprise Online.

Pour ce faire, commencez par ouvrir le Bloc-notes (ou un autre éditeur de texte), puis collez les commandes suivantes, en remplaçant kenmyer@litwareinc.com par votre nom de compte Skype Entreprise Online :

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

Enregistrez le fichier avec une extension .PS1 (par exemple, C:\\Scripts\\LyncOnline.ps1).

Une fois que vous avez enregistré le fichier, effectuez la procédure suivante pour créer un raccourci Bureau qui lance Windows PowerShell et exécute le script au démarrage :

1.  Cliquez avec le bouton droit sur le Bureau, cliquez sur **Nouveau**, puis sur **Raccourci**.

2.  Dans l’Assistant **Créer un raccourci**, tapez ce qui suit dans la zone **Entrez l’emplacement de l’élément**, puis cliquez sur **Suivant** (veillez à utiliser le chemin d’accès au fichier de script que vous venez de créer) :
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  Dans la zone **Entrez un nom pour ce raccourci**, tapez un nom pour le raccourci (par exemple, **Skype Entreprise Online**), puis cliquez sur **Terminer**.

4.  La prochaine fois que vous voulez utiliser Windows PowerShell pour gérer Skype Entreprise Online, il vous suffit de double-cliquer sur le nouveau raccourci et d’entrer votre mot de passe. Le script établit alors la connexion et configure la nouvelle session à distance.

Cette nouvelle session n’est généralement pas stockée dans la variable $session. L’ID de session 1 lui est attribué. Ceci n’affecte votre session d’aucune manière, du moins tant que vous ne devez pas fermer celle-ci. Pour ce faire, vous devrez référencer l’ID de session lorsque vous utilisez l’applet de commande **Remove-PSSession** :

    Remove-PSSession 1

Vous pouvez vérifier l’ID attribué à votre session Skype Entreprise Online en exécutant cette commande à partir de l’invite Windows PowerShell :

    Get-PSSession

## Voir aussi

#### Concepts

[Configuration de votre ordinateur pour la gestion de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

