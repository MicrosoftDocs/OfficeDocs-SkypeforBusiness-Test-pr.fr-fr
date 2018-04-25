---
title: Présentation de Windows PowerShell et Lync Online
TOCTitle: Présentation de Windows PowerShell et Lync Online
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56269578
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Présentation de Windows PowerShell et Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

Interface de commande et langage de script, Windows PowerShell permet de gérer Skype Entreprise Online. Plutôt que d’utiliser le centre d’administration Skype Entreprise Online graphique pour gérer Skype Entreprise Online, vous pouvez exécuter des commandes en ligne de commande semblables à celle-ci :

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Outre l’exécution de commandes simples telles que celle de l’exemple précédent (qui retourne des informations sur l’utilisateur ayant le nom d’utilisateur principal kenmyer@litwareinc.com), les utilisateurs familiarisés avec l’utilisation de Windows PowerShell peuvent également organiser ces commandes au sein de scripts. Ces scripts peuvent être utilisés pour automatiser des processus et/ou effectuer des tâches répétitives.

En règle générale, les tâches que vous pouvez effectuer à l’aide du centre d’administration Skype Entreprise Online peuvent également être exécutées à l’aide de Windows PowerShell. Par exemple, vous pouvez utiliser le centre d’administration pour gérer les notifications par téléphone mobile (ou *notifications push*). Celles-ci vous permettent d’envoyer des notifications sur des événements (par exemple, nouveaux messages instantanés ou messages vocaux) aux appareils mobiles tels que les iPhone et les Windows Phone. Elles peuvent être reçues sur l’appareil mobile même si l’application Lync sur ces appareils est exécutée en arrière-plan.

Comment pouvez-vous gérer les notifications push ? Une méthode consiste à utiliser le centre d’administration Skype Entreprise Online pour activer ou désactiver les notifications push en sélectionnant l’option appropriée sous l’onglet **organisation** :

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362807.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

Vous pouvez également activer ou désactiver les notifications push à l’aide d’une session Windows PowerShell à distance et de l’applet de commande [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md). Par exemple, la commande suivante désactive les notifications push pour les iPhone et Windows Phone :

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Comme vous pouvez le voir, les paramètres (EnableApplePushNotificationService et EnableMicrosoftPushNotificationService) utilisés avec l’applet de commande **Set-CsPushNotificationConfiguration** correspondent aux options disponibles dans le centre d’administration Skype Entreprise Online :

![Association montrée entre les options Lync / l’applet de commande](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Association montrée entre les options Lync / l’applet de commande")

En résumé, vous pouvez utiliser le centre d’administration ou une applet de commande Windows PowerShell et les paramètres appropriés pour gérer les notifications push. Les deux approches sont équivalentes en termes d’efficacité.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour consulter la définition des termes spécifiques liés à Windows PowerShell (<em>applet de commande</em>, <em>paramètre</em>, <em>valeur de paramètre</em>, <em>argument</em>, etc.), voir <a href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Applets de commande Windows PowerShell, paramètres et valeurs de paramètre</a>.</td>
</tr>
</tbody>
</table>


Ceci soulève une question basique : si le centre d’administration Skype Entreprise Online et Windows PowerShell offrent les mêmes fonctionnalités, pourquoi choisir d’utiliser l’un plutôt que l’autre ? De même, pourquoi choisir de taper des commandes dans Windows PowerShell, plutôt que d’activer ou de désactiver des options dans le centre d’administration ?

Pour un cas simple comme l’exemple précédent, le choix de l’approche à utiliser dépend des préférences personnelles de chacun : certaines personnes préfèrent utiliser une interface graphique utilisateur, tandis que d’autres préfèrent un outil en ligne de commande, tel que Windows PowerShell. Pour autant, dans certains cas, Windows PowerShell offre une plus grande efficacité pour l’exécution d’une tâche de gestion, voire la seule façon d’effectuer une tâche de gestion. Par exemple, le centre d’administration Skype Entreprise Online vous permet de personnaliser les invitations aux réunions :

![Paramètres d’invitation à la réunion du centre d’administration Lync](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Paramètres d’invitation à la réunion du centre d’administration Lync")

Vous pouvez apporter ces personnalisations à l’aide de l’applet de commande [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md). L’applet de commande **Set-CsMeetingConfiguration** inclut des options non disponibles dans le centre d’administration Skype Entreprise Online. Par exemple, si une personne de votre organisation rejoint une réunion, il est configuré automatiquement comme présentateur de la réunion. Ce paramètre ne peut pas être modifié à l’aide du centre d’administration Skype Entreprise Online, mais en utilisant Windows PowerShell et l’applet de commande **Set-CsMeetingConfiguration**. Plus spécifiquement, cette commande définit la propriété DesignateAsPresenter sur None. Cela signifie que seul l’organisateur de la réunion est configuré comme présentateur lorsqu’il rejoint la réunion :

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

Pour plus d’informations sur l’utilisation de Windows PowerShell, voir les rubriques suivantes :

  - [Applets de commande Windows PowerShell, paramètres et valeurs de paramètre](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [Utilisation des paramètres](working-with-parameters-in-skype-for-business-online.md)

  - [Paramètres obligatoires et facultatifs](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [Paramètres et propriétés](parameters-vs-properties-in-skype-for-business-online.md)

  - [Combinaison des applets de commande Lync Online avec d’autres applets de commande Windows PowerShell](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [Aide supplémentaire sur l’utilisation de Windows PowerShell](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

