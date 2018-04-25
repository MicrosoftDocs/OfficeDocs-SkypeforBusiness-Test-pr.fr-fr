---
title: Échec de la connexion au serveur Live ID
TOCTitle: Échec de la connexion au serveur Live ID
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56269608
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Échec de la connexion au serveur Live ID

 

_**Dernière rubrique modifiée :** 2015-06-22_

L’échec de votre tentative de connexion avec le message d’erreur suivant est généralement dû à l’une de ces trois raisons :

    Get-CsWebTicket : connexion impossible aux serveurs live id. Vérifiez que le proxy est activé ou que l'ordinateur est connecté aux serveurs live id.

Cette erreur signifie parfois que l’Assistant de connexion Microsoft Online Services n’est pas en cours d’exécution. Vous pouvez vérifier l’état de ce service en exécutant la commande suivante à partir de l’invite Windows PowerShell :

    Get-Service "msoidsvc"

Si le service n’est pas en cours d’exécution, démarrez-le à l’aide de cette commande :

    Start-Service "msoidsvc"

Si le service est en cours d’exécution, vous pourriez rencontrer des problèmes avec la connexion réseau entre votre ordinateur et le serveur d’authentification Microsoft Live ID. Pour procéder à une vérification, ouvrez Internet Explorer et accédez à la page <https://login.microsoftonline.com/.> Essayez de vous connecter à Office 365 à partir de là. Si l’opération échoue, vous rencontrez probablement des problèmes de connexion réseau.

Plus rarement, il arrive que l’URI de connexion pour le serveur d’authentification Microsoft Live ID soit configuré de manière incorrecte. Si vous avez déjà déterminé que l’Assistant de connexion est exécuté et que vous ne rencontrez pas de problèmes de connectivité réseau, le problème peut venir de là. Dans ce cas, contactez le support technique Office 365.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

