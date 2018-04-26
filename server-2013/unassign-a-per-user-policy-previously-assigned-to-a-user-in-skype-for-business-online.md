---
title: Annuler l’affectation d’une stratégie utilisateur précédemment affectée à un utilisateur
TOCTitle: Annuler l’affectation d’une stratégie utilisateur précédemment affectée à un utilisateur
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56269646
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Annuler l’affectation d’une stratégie utilisateur précédemment affectée à un utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si vous voulez annuler l’affectation d’une stratégie utilisateur précédemment affectée à un utilisateur, exécutez à nouveau l’applet de commande **Grant-Cs** (par exemple, l’applet de commande [Grant-CsVoicePolicy](grant-csvoicepolicy.md) pour annuler l’affectation d’une stratégie de voix), et définissez le paramètre PolicyName sur une valeur null ($Null) :

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

Pour annuler l’affectation des stratégies de voix pour tous vos utilisateurs, utilisez la commande suivante :

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

Une fois que l’affectation d’une stratégie à un utilisateur est annulée, celui-ci est géré par la stratégie globale.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

