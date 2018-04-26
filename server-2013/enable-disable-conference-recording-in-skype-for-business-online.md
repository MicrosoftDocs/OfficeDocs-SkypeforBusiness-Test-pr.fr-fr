---
title: Activer/désactiver l’enregistrement de conférence
TOCTitle: Activer/désactiver l’enregistrement de conférence
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56269678
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Activer/désactiver l’enregistrement de conférence

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si vous ne souhaitez pas que les utilisateurs puissent enregistrer les conférences en ligne, utilisez l’applet de commande [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) et définissez la valeur du paramètre AllowConferenceRecording sur False ($False) :

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

Pour rétablir la possibilité d’enregistrer les conférences en ligne, définissez la valeur du paramètre AllowConferenceRecording sur True ($True) :

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

