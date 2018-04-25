---
title: Activer/désactiver un fournisseur de messagerie instantanée public spécifique
TOCTitle: Activer/désactiver un fournisseur de messagerie instantanée public spécifique
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56269639
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Activer/désactiver un fournisseur de messagerie instantanée public spécifique

 

_**Dernière rubrique modifiée :** 2015-06-22_

Skype Entreprise Online vous permet d’établir la fédération avec des utilisateurs liés à un ou plusieurs des fournisseurs de messagerie instantanée publics suivants :

  - Réseau Windows Live de services sur Internet

  - Yahoo\!

  - AOL

Pour permettre la fédération avec un ou plusieurs de ces fournisseurs, utilisez l’applet de commande [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) et définissez la valeur de la propriété Provider sur une ou plusieurs des valeurs suivantes :

  - Windows Live

  - Yahoo

  - AOL

Par exemple, cette commande établit la fédération avec Windows Live et AOL :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Notez que chaque fois que vous voulez ajouter ou supprimer un fournisseur, vous devez inclure tous les fournisseurs fédérés appropriés dans la commande. Par exemple, pour ajouter Yahoo\!, exécutez la commande suivante :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

Cette commande définit Yahoo\! comme seul fournisseur fédéré, car il est spécifié dans la commande. Pour établir la fédération avec les trois fournisseurs de messagerie instantanée publics, vous devez tous les inclure :

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

Notez que vous devez inclure le paramètre Tenant lorsque vous appelez l’applet de commande Set-CsTenantPublicProvider, sans quoi vous serez invité à entrer l‘ID du client. Vous pouvez retourner l‘ID de votre client Skype Entreprise Online à l’aide de la commande suivante :

    Get-CsTenant | Select-Object TenantID

Utilisez la commande suivante pour stocker l’ID de client dans une variable :

    $tenantID = (Get-CsTenant | Select-Object TenantID)

Vous pouvez ensuite utiliser cette variable (dans cet exemple, $tenantID) lorsque vous appelez Set-CsTenantPublicProvider :

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

