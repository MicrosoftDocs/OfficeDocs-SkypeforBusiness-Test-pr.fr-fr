---
title: Afficher les domaines dans votre liste des domaines autorisés
TOCTitle: Afficher les domaines dans votre liste des domaines autorisés
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56269565
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Afficher les domaines dans votre liste des domaines autorisés

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour afficher tous les domaines dans votre liste des domaines autorisés, utilisez l’applet de commande [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) avec la syntaxe suivante :

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

