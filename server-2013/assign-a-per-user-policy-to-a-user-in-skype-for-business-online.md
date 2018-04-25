---
title: Affecter une stratégie utilisateur à un utilisateur
TOCTitle: Affecter une stratégie utilisateur à un utilisateur
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56269574
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Affecter une stratégie utilisateur à un utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour affecter une stratégie utilisateur à un utilisateur, vous devez commencer par sélectionner l’applet de commande **Grant-Cs** appropriée (par exemple, [Grant-CsVoicePolicy](grant-csvoicepolicy.md) si vous voulez affecter une stratégie de voix utilisateur). Exécutez l’applet de commande en veillant à spécifier l’identité de l’utilisateur auquel la stratégie doit être affectée et le nom de la stratégie à affecter :

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

Si vous voulez affecter la même stratégie à tous vos utilisateurs, utilisez la syntaxe suivante :

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

En raison de différents contrats de licence et différentes restrictions régionales, il est possible que certaines stratégies de conférence, stratégies d’accès externes ou stratégies de mobilité ne puissent pas être affectées à un utilisateur particulier. Pour vérifier les stratégies utilisateur qui peuvent être affectées à un utilisateur donné (par exemple, kenmyer@litwareinc.com), utilisez une des commandes suivantes (et le paramètre ApplicableTo), selon le cas :

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La syntaxe précédente retourne uniquement les stratégies utilisateur qui peuvent effectivement être affectées à Ken Myer.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

