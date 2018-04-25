---
title: Retourner une liste filtrée d’utilisateurs
TOCTitle: Retourner une liste filtrée d’utilisateurs
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56269671
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner une liste filtrée d’utilisateurs

 

_**Dernière rubrique modifiée :** 2015-06-22_

L’applet de commande [Get-CsOnlineUser](get-csonlineuser.md) et les paramètres LdapFilter ou Filter vous permettent de retourner aisément des informations sur un ensemble ciblé d’uitlisateurs. Par exemple, cette commande retourne tous les utilisateurs qui travaillent au sein du service Finance :

    Get-CsOnlineUser -LdapFilter "department=Finance"

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

