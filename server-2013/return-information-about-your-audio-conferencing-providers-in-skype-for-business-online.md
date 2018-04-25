---
title: Retourner des informations sur vos fournisseurs de services d’audioconférence
TOCTitle: Retourner des informations sur vos fournisseurs de services d’audioconférence
ms:assetid: df9c8fc0-8bb6-4416-a5cc-aa9b1601a688
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362848(v=OCS.15)
ms:contentKeyID: 56269663
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner des informations sur vos fournisseurs de services d’audioconférence

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour retourner des informations sur les fournisseurs de services d’audioconférence affectés à un utilisateur, utilisez l’applet de commande [Get-CsUserAcp](get-csuseracp.md) et la syntaxe suivante :

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

