---
title: Retourner des informations sur les fournisseurs de services dƾaudioconférence affectés à un utilisateur
TOCTitle: Retourner des informations sur les fournisseurs de services dƾaudioconférence affectés à un utilisateur
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56269620
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner des informations sur les fournisseurs de services dƾaudioconférence affectés à un utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour retourner des informations sur les fournisseurs de services d’audioconférence affectés à un utilisateur, utilisez l’applet de commande [Get-CsUserAcp](get-csuseracp.md) et la syntaxe suivante :

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

