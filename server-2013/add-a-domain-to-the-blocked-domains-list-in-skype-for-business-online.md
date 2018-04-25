---
title: 'Lync Online : Ajout d’un domaine à la liste des domaines bloqués'
TOCTitle: Ajout d’un domaine à la liste des domaines bloqués
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56269670
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ajout d’un domaine à la liste des domaines bloqués dans Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour ajouter un domaine à la liste des domaines bloqués, utilisez une syntaxe semblable à celle-ci :

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

Comme vous pouvez le voir, cette commande se fait en deux étapes. Vous devez d’abord utiliser [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) pour créer un objet domaine représentant le domaine à ajouter à la liste des domaines bloqués. Ensuite, utilisez l’applet de commande [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) et la méthode Add pour ajouter ce domaine (dans cet exemple, le domaine stocké dans la variable $x) à la liste.

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

