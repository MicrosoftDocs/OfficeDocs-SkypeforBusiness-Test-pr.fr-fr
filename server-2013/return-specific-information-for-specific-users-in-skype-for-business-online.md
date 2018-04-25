---
title: Retourner des informations spécifiques pour des utilisateurs donnés
TOCTitle: Retourner des informations spécifiques pour des utilisateurs donnés
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56269650
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Retourner des informations spécifiques pour des utilisateurs donnés

 

_**Dernière rubrique modifiée :** 2015-06-22_

Par défaut, l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md) retourne une grande quantité d’informations pour chaque compte d’utilisateur Skype Entreprise Online. Si vous êtes seulement intéressé par un sous-ensemble de ces informations, redirigez les données retournées vers l’applet de commande **Select-Object**. Par exemple, la commande suivante retourne toutes les données de l’utilisateur Ken Myer, puis utilise l’applet de commande **Select-Object** pour limiter les informations affichées à l’écran au nom complet des services de domaine Active Directory et au plan de numérotation de Ken :

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

La commande suivante retourne le nom complet et le plan de numérotation de tous les utilisateurs.

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

Pour rechercher les propriétés d’un compte d’utilisateur Skype Entreprise Online, utilisez la commande suivante :

    Get-CsOnlineUser | Get-Member

## Voir aussi

#### Concepts

[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

