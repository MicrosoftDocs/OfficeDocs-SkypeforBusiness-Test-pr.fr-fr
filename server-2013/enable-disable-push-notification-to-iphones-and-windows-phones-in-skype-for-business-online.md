---
title: Activer/désactiver les notifications push sur les iPhone et Windows Phone
TOCTitle: Activer/désactiver les notifications push sur les iPhone et Windows Phone
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56269593
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Activer/désactiver les notifications push sur les iPhone et Windows Phone

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour désactiver l’envoi des notifications push vers les iPhone et Windows Phone, utilisez l’applet de commande [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) et définissez les valeurs des propriétés EnableApplePushNotificationService et EnableMicrosoftPushNotificationService sur False ($False) :

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Notez que les iPhone et Windows Phone peuvent être configurés indépendamment. Par exemple, la commande suivante désactive les notifications push sur les iPhone, mais active ces notifications sur les Windows Phone :

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

