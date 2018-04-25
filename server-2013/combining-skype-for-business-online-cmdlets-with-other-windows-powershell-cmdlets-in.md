---
title: Combinaison des applets de commande Lync Online avec d’autres applets de commande Windows PowerShell
TOCTitle: Combinaison des applets de commande Lync Online avec d’autres applets de commande Windows PowerShell
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56269629
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Combinaison des applets de commande Lync Online avec d’autres applets de commande Windows PowerShell

 

_**Dernière rubrique modifiée :** 2015-06-22_

Lorsque vous vous connectez à Skype Entreprise Online à l’aide de Windows PowerShell, vous pouvez utiliser environ 40 applets de commande Skype Entreprise Online. Vous n’êtes toutefois pas limité à l’utilisation de ces 40 applets de commande dans le cadre de la gestion de Skype Entreprise Online. Outre les applets de commande Skype Entreprise Online, vous pouvez également utiliser les autres applets de commande Windows PowerShell installées sur votre ordinateur. (Lorsque vous installez Windows PowerShell 3.0, des centaines d’applets de commande Windows PowerShell sont également installées.) Vos commandes peuvent combiner les applets de commande Skype Entreprise Online et celles disponibles sur votre ordinateur.

Si un cours complet dans Windows PowerShell 3.0 dépasse le cadre de cet article, voici toutefois quelques exemples qui montrent comment vous pouvez combiner des applets de commande. En premier lieu, aucune des applets de commande Skype Entreprise Online n’inclut de commande d’impression. Aucune commande de ce type n’est disponible non plus dans la console Windows PowerShell. Comment pouvez-vous imprimer les informations récupérées par une applet de commande ? Vous pouvez récupérer les informations, puis envoyer celles-ci à l’applet de commande **Out-Printer** :

    Get-CsTenant | Out-Printer

Comme aucun autre paramètre n’est inclus, les informations retournées par l’applet de commande **the Out-Printer** sont imprimées sur l’imprimante par défaut.

De même, aucune applet de commande Skype Entreprise Online n’inclut de paramètre vous permettant d’enregistrer des données dans un fichier. Grâce à la commande suivante qui utilise l’applet de commande **Out-File**, les informations retournées sont enregistrées dans le fichier texte C:\\Logs\\Tenants.txt :

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

Enfin, la commande suivante utilise l’applet de commande **Select-Object** pour limiter les données retournées et affichées à l’écran. Dans cet exemple, l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md) récupère des informations sur tous vos utilisateurs Skype Entreprise Online, puis l’applet de commande **Select-Object** limite les données affichées à la valeur Identity de l’utilisateur et à sa stratégie d’affichage :

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

Comme des centaines d’applets de commande peuvent être utilisées sur votre ordinateur, vous pouvez rencontrer des difficultés pour déterminer lesquelles sont des applets de commande Skype Entreprise Online et lesquelles ne le sont pas. Pour retourner la liste des applets de commande Skype Entreprise Online (et seulement des applets de commande Skype Entreprise Online), vous devez commencer par déterminer le nom du module Windows PowerShell temporaire qui contient toutes les applets de commande Skype Entreprise Online. Pour ce faire, exécutez cette commande à partir de l’invite Windows PowerShell :

    Get-Module

Des informations semblables à ce qui suit sont affichées à l’écran :

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Le module de type Script contient les applets de commande Skype Entreprise Online. Pour retourner la liste de ces applets de commande, exécutez l’applet de commande **Get-Command** en utilisant le nom du module Script comme nom de module :

    Get-Command -Module tmp_5astd3uh.m5v

Il est possible qu’il y ait plusieurs modules de type Script. Dans ce cas, vous pouvez exécuter la commande suivante pour identifier le module incluant l’applet de commande **Get-CsTenant** :

    Get-Command Get-CsTenant

Le module retourné pour l’applet de commande **Get-CsTenant** est celui contenant toutes les applets de commande Skype Entreprise Online :

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## Voir aussi

#### Concepts

[Présentation de Windows PowerShell et Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

