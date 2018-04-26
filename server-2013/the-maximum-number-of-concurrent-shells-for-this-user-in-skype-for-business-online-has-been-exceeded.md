---
title: Dépassement du nombre maximal de shells simultanés pour cet utilisateur
TOCTitle: Dépassement du nombre maximal de shells simultanés pour cet utilisateur
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56269645
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Dépassement du nombre maximal de shells simultanés pour cet utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Chaque administrateur est autorisé à utiliser jusqu’à trois connexions à distance simultanées à Skype Entreprise Online. Si vous avez établi trois connexions Windows PowerShell, toute tentative d’établissement d’une quatrième connexion échouera avec le message d’erreur suivant :

    New-PSSession : [admin.vdomain.com] La connexion au serveur distant admin.vdomain.com a échoué avec le message d'erreur suivant : Le service Gestion des services Web ne peut pas traiter la demande. Le nombre maximal de shells simultanés pour cet utilisateur a été dépassé. Fermez les shells existants ou augmentez le quota pour ce client. Pour plus d'informations, voir la rubrique d'aide about_Remote_Troubleshooting (À propos du dépannage à distance).

La seule façon de résoudre ce problème consiste à fermer une ou plusieurs des connexions précédentes. Lorsque vous avez terminé avec une session Skype Entreprise Online, il est recommandé d’utiliser l’applet de commande **Remove-PSSession** pour mettre fin à la session. Ceci vous permet d’éviter ce problème.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

