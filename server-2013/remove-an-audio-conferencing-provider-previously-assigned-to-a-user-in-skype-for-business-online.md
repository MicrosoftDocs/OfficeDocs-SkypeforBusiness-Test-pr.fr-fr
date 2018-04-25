---
title: Supprimer un fournisseur de services d’audioconférence précédemment affecté à un utilisateur
TOCTitle: Supprimer un fournisseur de services d’audioconférence précédemment affecté à un utilisateur
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56269622
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supprimer un fournisseur de services d’audioconférence précédemment affecté à un utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour supprimer les fournisseurs de services d’audioconférence affectés à un utilisateur, exécutez l’applet de commande [Remove-CsUserAcp](remove-csuseracp.md) sans paramètre (à l’exception du paramètre Identity qui indique l’utilisateur concerné) :

    Remove-CsUserAcp -Identity "Ken Myer"

Si plusieurs fournisseurs de services d’audioconférence ont été affectés à un utilisateur, vous pouvez supprimer un seul fournisseur en incluant le paramètre Name, suivi du nom du fournisseur devant être supprimé :

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

