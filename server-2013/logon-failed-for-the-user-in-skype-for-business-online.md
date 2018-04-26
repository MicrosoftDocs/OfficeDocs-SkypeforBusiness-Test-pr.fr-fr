---
title: Échec de la connexion de l’utilisateur
TOCTitle: Échec de la connexion de l’utilisateur
ms:assetid: 006020cd-34d0-4a78-b5b4-e382d95ef04d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn329053(v=OCS.15)
ms:contentKeyID: 56269555
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Échec de la connexion de l’utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Lorsque vous tentez d’établir une connexion distante à Skype Entreprise Online, vous devez fournir les nom d’utilisateur et mot de passe d’un compte d’utilisateur Skype Entreprise Online valide, sans quoi la connexion échoue avec un message d’erreur semblable à ce qui suit :

    Get-CsWebTicket : Échec de l'ouverture de session de l'utilisateur « kenmyer@litwareinc.com ». Créez un nouvel objet PSCredential, en vérifiant que vous utilisez un nom d'utilisateur et un mot de passe corrects.

Si vous pensez utiliser un compte d’utilisateur valide avec le mot de passe correct, réessayez de vous connecter. Si la connexion échoue, utilisez les mêmes informations d’identification et essayez de vous connecter à l’adresse <https://login.microsoftonline.com/>. Si vous ne parvenez pas à vous connecter sur ce site, contactez le support technique d’Office 365.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

