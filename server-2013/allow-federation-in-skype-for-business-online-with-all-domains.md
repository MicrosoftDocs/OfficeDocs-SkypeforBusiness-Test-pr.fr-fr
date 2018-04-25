---
title: Autoriser la fédération avec tous les domaines
TOCTitle: Autoriser la fédération avec tous les domaines
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56269657
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Autoriser la fédération avec tous les domaines

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si vous voulez autoriser vos utilisateurs à communiquer avec les utilisateurs d’un domaine quelconque, vous devez effectuer deux opérations. Commencez par utiliser l’applet de commande [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md) pour créer une instance de l’objet AllowAllKnownDomains :

    $x = New-CsEdgeAllowAllKnownDomains

Appelez ensuite l’applet de commande [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) et définissez la valeur de la propriété AllowedDomains sur la variable (dans cet exemple, $x) qui contient l’objet AllowAllKnownDomains :

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

