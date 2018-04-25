---
title: Obtenir des informations sur votre client Lync Online
TOCTitle: Obtenir des informations sur votre client Lync Online
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56269559
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obtenir des informations sur votre client Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

Pour retourner des informations sur votre client Skype Entreprise Online, appelez l’applet de commande [Get-CsTenant](get-cstenant.md) sans aucun paramètre supplémentaire :

    Get-CsTenant

Pour retourner seulement le nom du client et l’ID (la valeur du paramètre TenantID est nécessaire lors de l’exécution des applets de commande telles que [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) et [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)), utilisez la commande suivante :

    Get-CsTenant | Select-Object Name, TenantID

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

