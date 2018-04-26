---
title: Retourner la liste des stratégies utilisateur
TOCTitle: Retourner la liste des stratégies utilisateur
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56269669
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner la liste des stratégies utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour retourner la liste des stratégies utilisateur disponibles, commencez par sélectionner l’applet de commande **Get-Cs** appropriée (par exemple, [Get-CsVoicePolicy](get-csvoicepolicy.md) si vous voulez retourner les stratégies vocales utilisateur). Utilisez ensuite la syntaxe suivante pour retourner l’identité de chaque stratégie utilisateur :

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

En raison de différents contrats de licence et différentes restrictions régionales, il est possible que certaines stratégies de conférence, stratégies d’accès externes ou stratégies de mobilité ne puissent pas être affectées à un utilisateur particulier. Pour vérifier les stratégies utilisateur qui peuvent être affectées à un utilisateur donné (par exemple, kenmyer@litwareinc.com), utilisez une des commandes suivantes (et le paramètre ApplicableTo), selon le cas :

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La syntaxe précédente retourne uniquement les stratégies utilisateur qui peuvent effectivement être affectées à Ken Myer.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

