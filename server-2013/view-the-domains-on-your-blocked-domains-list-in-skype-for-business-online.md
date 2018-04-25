---
title: Afficher les domaines dans votre liste des domaines bloqués
TOCTitle: Afficher les domaines dans votre liste des domaines bloqués
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56269597
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Afficher les domaines dans votre liste des domaines bloqués

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour afficher les domaines dans votre liste des domaines bloqués, utilisez l’applet de commande [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md), puis redirigez les données retournées vers l’applet de commande **Select-Object** :

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

