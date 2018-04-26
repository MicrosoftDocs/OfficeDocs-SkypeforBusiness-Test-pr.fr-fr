---
title: La possibilité de se connecter au client a été désactivée
TOCTitle: La possibilité de se connecter au client a été désactivée
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56269614
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# La possibilité de se connecter au client a été désactivée

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour utiliser Windows PowerShell en vue de gérer Skype Entreprise Online, la propriété EnableRemotePowerShellAccess de votre stratégie Windows PowerShell cliente doit être définie sur True. Si tel n’est pas le cas, votre connexion échouera et vous recevrez le message d’erreur suivant :

    New-PSSession : [admin.vdomain.com] le traitement des données provenant du serveur distant admin.vdomain.com  a échoué avec le message d'erreur suivant : la possibilité de connexion à ce client à l'aide d'une session PowerShell distante a été désactivée. Veuillez contacter l'assistance de Lync pour vérifier la stratégie Powershell de ce client. Pour plus d'informations, voir la rubrique d'aide about_Remote_Troubleshooting (À propos du dépannage à distance).

Si vous voyez ce message d’erreur, vous devez contacter le support technique Office 365 et faire activer l’accès à Windows PowerShell distant.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

