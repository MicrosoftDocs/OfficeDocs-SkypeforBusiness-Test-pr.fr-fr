---
title: L’utilisateur n’est pas autorisé à gérer ce client
TOCTitle: L’utilisateur n’est pas autorisé à gérer ce client
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56269611
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# L’utilisateur n’est pas autorisé à gérer ce client

 

_**Dernière rubrique modifiée :** 2015-06-22_

Vous ne pouvez pas établir de connexion Windows PowerShell distante à Skype Entreprise Online, à moins que vous ne soyez membre du groupe Administrateurs de clients. Si tel n’est pas le cas, votre tentative de connexion échouera et vous obtiendrez le message d’erreur suivant :

    New-PSSession : [admin.vdomain.com] le traitement des données provenant du serveur distant admin.vdomain.com a échoué avec le message d'erreur suivant : l'utilisateur « user@foo.com » n'est pas autorisé à géer ce client. Les autorisations peuvent être octroyées en affectant l'utilisateur au rôle RBAC approprié. Pour plus d'informations, voir la rubrique d'aide about_Remote_Troubleshooting (À propos du dépannage à distance).

Si vous pensez ou êtes censé être membre du groupe Administrateurs de clients, vous devez contacter le support technique Office 365.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

