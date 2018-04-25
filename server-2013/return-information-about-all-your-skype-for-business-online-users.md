---
title: Retourner des informations sur tous vos utilisateurs de Lync Online
TOCTitle: Retourner des informations sur tous vos utilisateurs de Lync Online
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56269562
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner des informations sur tous vos utilisateurs de Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour retourner des informations sur tous vos utilisateurs activés pour Skype Entreprise Online, appelez l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md) sans aucun paramètre supplémentaire :

    Get-CsOnlineUser

Pour retourner les informations d’un seul utilisateur sélectionné de façon aléatoire (pour utiliser son compte à des fins de test, par exemple), appelez l’applet de commande **Get-CsOnlineUser** et définissez le paramètre ResultSize sur 1 :

    Get-CsOnlineUser -ResultSize 1

L’applet de commande **Get-CsOnlineUser** retourne alors les informations d’un seul utilisateur, quel que soit le nombre d’utilisateurs dans votre organisation. Pour retourner les informations de cinq utilisateurs, définissez la valeur du paramètre ResultSize sur 5 :

    Get-CsOnlineUser -ResultSize 5

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

