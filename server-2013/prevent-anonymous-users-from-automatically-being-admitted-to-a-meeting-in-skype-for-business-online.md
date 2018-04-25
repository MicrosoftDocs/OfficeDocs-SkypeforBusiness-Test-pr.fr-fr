---
title: Empêcher l’admission automatique des utilisateurs anonymes à une réunion
TOCTitle: Empêcher l’admission automatique des utilisateurs anonymes à une réunion
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56269568
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Empêcher l’admission automatique des utilisateurs anonymes à une réunion

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour empêcher l’admission automatique des utilisateurs anonymes à une réunion en ligne, utilisez l’applet de commande [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) et définissez la propriété AdmitAnonymousUsersByDefault sur False ($False) :

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

Pour activer l’admission automatique, redéfinissez la propriété AdmitAnonymousUsersByDefault sur True ($True) :

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

