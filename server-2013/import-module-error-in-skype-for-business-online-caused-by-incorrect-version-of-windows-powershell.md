---
title: Erreur d’importation de module due à une version incorrecte de Windows PowerShell
TOCTitle: Erreur d’importation de module due à une version incorrecte de Windows PowerShell
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56269605
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Erreur d’importation de module due à une version incorrecte de Windows PowerShell

 

_**Dernière rubrique modifiée :** 2015-06-22_

Le module Skype Entreprise Online Connector ne peut être exécuté que sous Windows PowerShell 3.0. Si vous essayez d’importer le module sous une version précédente de Windows PowerShell, le processus d’importation échouera avec un message d’erreur semblable à ce qui suit :

    Import-Module : La version de PowerShell chargée est « 2.0 ». Le module « D:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1 » nécessite au minimum la version « 3.0 » de PowerShell pour s'exécuter. Vérifiez l'installation de PowerShell et réessayez.

La seule façon de résoudre ce problème consiste à installer Windows PowerShell 3.0, disponible via le Centre de téléchargement Microsoft à l’adresse <http://www.microsoft.com/en-us/download/details.aspx?id=29939>.

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

