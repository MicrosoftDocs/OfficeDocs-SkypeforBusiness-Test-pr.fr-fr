---
title: Supprimer un domaine de la liste des domaines bloqués
TOCTitle: Supprimer un domaine de la liste des domaines bloqués
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56269631
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supprimer un domaine de la liste des domaines bloqués

 

_**Dernière rubrique modifiée :** 2015-06-22_

La suppression d’un domaine de la liste des domaines bloqués inclut deux étapes. Vous devez commencer par utiliser l’applet de commande [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) pour créer un objet domaine pour le domaine à supprimer :

    $x = New-CsEdgeDomainPattern "fabrikam.com"

Une fois cet objet créé, utilisez la syntaxe suivante pour supprimer le domaine (dans cet exemple, le domaine stocké dans la variable $x) de la liste des domaines bloqués :

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

Pour supprimer tous les domaines de la liste des domaines bloqués, définissez la propriété BlockedDomains sur la valeur null ($Null) :

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

