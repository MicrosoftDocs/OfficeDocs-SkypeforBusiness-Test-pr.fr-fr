---
title: 'Lync Online : Ajout d’un domaine à la liste des domaines autorisés'
TOCTitle: Ajout d’un domaine à la liste des domaines autorisés
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56269618
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ajout d’un domaine à la liste des domaines autorisés dans Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

L’ajout d’un premier domaine à la liste des domaines autorisés est un processus en trois étapes. Vous devez commencer par utiliser l’applet de commande [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) pour créer un objet domaine pour le domaine devant être ajouté :

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

Utilisez ensuite l’applet de commande [New-CsEdgeAllowList](new-csedgeallowlist.md) pour créer une liste de domaines autorisés incluant l’objet domaine :

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

Enfin, utilisez l’applet de commande [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) pour écrire la nouvelle liste de domaines autorisés dans Skype Entreprise Online :

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

