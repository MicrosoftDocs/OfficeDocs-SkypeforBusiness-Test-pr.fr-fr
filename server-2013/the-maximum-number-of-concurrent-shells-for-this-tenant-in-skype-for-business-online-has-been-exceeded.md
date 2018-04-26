---
title: Dépassement du nombre maximal de shells simultanés pour ce client
TOCTitle: Dépassement du nombre maximal de shells simultanés pour ce client
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56269633
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Dépassement du nombre maximal de shells simultanés pour ce client

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si chaque administrateur est autorisé à utiliser jusqu’à trois connexions simultanées à un client Skype Entreprise Online, aucun client n’est autorisé à utiliser jusqu’à neuf connexions simultanées. Par exemple, trois administrateurs peuvent avoir chacun trois sessions ouvertes. Si un quatrième administrateur tente d’établir une connexion (soit un total de 10 connexions simultanées), cette tentative échoue avec le message d’erreur suivant :

    New-PSSession : [admin.vdomain.com] La connexion au serveur distant admin.vdomain.com a échoué avec le message d'erreur suivant : Le service Gestion des services Web ne peut pas traiter la demande. Le nombre maximal de shells simultanés pour ce client a été dépassé. Fermez les shells existants ou augmentez le quota pour ce client. Pour plus d'informations, voir la rubrique d'aide about_Remote_Troubleshooting (À propos du dépannage à distance).

La seule façon de résoudre ce problème consiste à fermer une ou plusieurs des connexions précédentes. Lorsque vous avez terminé avec une session Skype Entreprise Online, il est recommandé d’utiliser l’applet de commande **Remove-PSSession** pour mettre fin à cette session. Ceci vous permet d’éviter ce problème.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

