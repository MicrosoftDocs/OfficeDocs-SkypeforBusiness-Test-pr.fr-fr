---
title: Affecter un fournisseur de services d’audioconférence à un utilisateur
TOCTitle: Affecter un fournisseur de services d’audioconférence à un utilisateur
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56269598
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Affecter un fournisseur de services d’audioconférence à un utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

L’applet de commande [Set-CsUserAcp](set-csuseracp.md) permet d’affecter un fournisseur de services d’audioconférence à un utilisateur :

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

Cette affectation n’aura pas de sens si vous n’avez pas déjà mis en place des contrats avec le fournisseur spécifié.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

