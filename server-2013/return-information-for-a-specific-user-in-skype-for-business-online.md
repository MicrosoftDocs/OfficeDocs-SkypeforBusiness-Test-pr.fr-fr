---
title: Retourner des informations pour un utilisateur spécifique
TOCTitle: Retourner des informations pour un utilisateur spécifique
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56269606
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner des informations pour un utilisateur spécifique

 

_**Dernière rubrique modifiée :** 2015-06-22_

Il est possible de référencer un compte d’utilisateur spécifique de plusieurs façons lorsque vous utilisez l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md). Vous pouvez utiliser le nom complet des services de domaine Active Directory de l’utilisateur :

    Get-CsOnlineUser -Identity "Ken Myer"

Vous pouvez utiliser l’adresse SIP de l’utilisateur :

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

Vous pouvez utiliser le nom d’utilisateur principal de l’utilisateur :

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

