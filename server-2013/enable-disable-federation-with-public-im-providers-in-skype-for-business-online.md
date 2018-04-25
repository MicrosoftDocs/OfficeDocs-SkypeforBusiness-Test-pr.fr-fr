---
title: Activer/désactiver la fédération avec des fournisseurs de messagerie instantanée publics
TOCTitle: Activer/désactiver la fédération avec des fournisseurs de messagerie instantanée publics
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56269623
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Activer/désactiver la fédération avec des fournisseurs de messagerie instantanée publics

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour permettre à vos utilisateurs de communiquer avec des utilisateurs dont le compte est hébergé auprès d’un fournisseur de messagerie instantanée public, utilisez l’applet de commande [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) et définissez la propriété AllowPublicUsers sur True ($True) :

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

Vous devez ensuite utiliser l’applet de commande [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) pour spécifier les fournisseurs de messagerie instantanée publics avec lesquels vos utilisateurs seront autorisés à communiquer.

Pour désactiver la fédération avec des fournisseurs publics, redéfinissez la propriété AllowPublicUsers sur False ($False) :

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

