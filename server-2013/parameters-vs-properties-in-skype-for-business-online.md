---
title: Paramètres et propriétés
TOCTitle: Paramètres et propriétés
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56269594
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Paramètres et propriétés

 

_**Dernière rubrique modifiée :** 2015-06-22_

En consultant les rubriques d’aide sur les applets de commande Skype Entreprise Online, vous verrez parfois les termes *paramètre* et *propriété* utilisés de façon interchangeable. Ne vous laissez pas troubler par cette terminologie : si les deux termes sont techniquement différents, dans Skype Entreprise Online, ils font référence au même concept.

D’un point de vue technique, les paramètres sont utilisés lorsque vous exécutez une applet de commande. Par exemple, dans l’applet de commande Windows PowerShell, EnableMicrosoftPushNotificationService et EnableApplePushNotificationService sont les paramètres de l’applet de commande [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) :

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

Une propriété est un attribut d’un objet Skype Entreprise Online (par exemple, une collection de paramètres de configuration des notifications push). Supposons que vous exécutez la commande suivante :

    Set-CsPushNotificationConfiguration

Vous obtenez ainsi une collection de propriétés et leurs valeurs associées, lesquelles incluent les éléments suivants :

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

Comme vous pouvez le voir, les propriétés et paramètres partagent le même nom : vous utilisez le paramètre EnableMicrosoftPushNotificationService pour configurer la valeur de la propriété EnableMicrosoftPushNotificationService.

## Voir aussi

#### Concepts

[Présentation de Windows PowerShell et Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

