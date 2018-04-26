---
title: Supprimer un domaine de la liste des domaines autorisés
TOCTitle: Supprimer un domaine de la liste des domaines autorisés
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56269558
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supprimer un domaine de la liste des domaines autorisés

 

_**Dernière rubrique modifiée :** 2015-06-22_

La suppression d’un domaine de la liste des domaines autorisés implique plusieurs étapes. Vous devez commencer par utiliser une commande semblable à la suivante pour récupérer l’ensemble des domaines de la liste :

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

Exécutez ensuite la commande suivante pour examiner ces domaines :

``` 
$x
```

Notez la position numérique du domaine devant être supprimé. Si le domaine apparaît en premier dans la liste, il a la valeur d’index 0, s’il apparaît en deuxième, il a la valeur d’index 1, etc.

Une fois que vous avez identifié le numéro d’index, utilisez une commande comme celle qui suit pour supprimer le domaine spécifié. Vérifiez que vous utilisez le numéro d’index correct. Cette commande supprime le premier domaine de la liste (numéro d’index 0) :

    $x.AllowedDomain.RemoveAt(0)

Pour finir, appelez l’applet de commande [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) pour écrire vos modifications dans Skype Entreprise Online :

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

