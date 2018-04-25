---
title: 'Lync Online : applets de commande de création de rapports Lync Online et service web REST'
TOCTitle: Applets de commande de création de rapports Lync Online et service web REST
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56269655
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applets de commande de création de rapports Lync Online et service web REST

 

_**Dernière rubrique modifiée :** 2016-12-08_

Conjointement aux fonctionnalités de création de rapports, Skype Entreprise Online offre un accès à cinq applets de commande Windows PowerShell qui permettent de générer ces rapports. Celles-ci peuvent être utilisées par les administrateurs pour retourner des données de rapport personnalisées. Skype Entreprise Online inclut également REST (Representational State Transfer) qui permet aux développeurs de récupérer des informations de rapport personnalisées.

Les applets de commande de création de rapports suivantes sont disponibles pour les administrateurs :

  - Get-CsActiveUserReport fournit des informations sur le nombre d’utilisateurs actifs (utilisateurs qui se sont connectés à Skype Entreprise Online et ont participé à au moins une session de conférence ou de communication d’égal à égal).

  - Get-CsAVConferenceTimeReport fournit des informations sur la durée (en minutes) pendant laquelle des utilisateurs ont participé à des conférences A/V.

  - Get-CsConferenceReport fournit des informations sur le nombre et le type des conférences auxquelles des utilisateurs ont participé.

  - Get-CsP2PAVTimeReport fournit des informations sur la durée (en minutes) pendant laquelle des utilisateurs ont participé à des sessions d’égal à égal ayant inclus du son et/ou de la vidéo.

  - Get-CsP2PSessionReport fournit des informations sur le nombre et le type des sessions d’égal à égal auxquelles les utilisateurs ont participé.

La plupart des administrateurs utilisent les rapports disponibles dans le centre d’administration Office 365 : non seulement ces rapports sont générés automatiquement, mais ils fournissent une représentation graphique des données plus simple à interpréter que les valeurs numériques brutes renvoyées par les applets de commande de création de rapports. Cependant, les administrateurs qui connaissent bien Windows PowerShell peuvent utiliser les applets de commande de création de rapports pour renvoyer des données qui ne sont pas immédiatement disponibles dans les rapports Lync Online. Par exemple, les applets de commande de création de rapports renvoient des informations sur la durée des sessions (durée en minutes de chaque session). La durée des sessions individuelles n’est pas disponible dans les rapports Lync Online. De même, en mode d’affichage quotidien, les rapports Lync Online proposent des informations sur les 14 jours précédents uniquement. Si vous voulez consulter les totaux d’un autre jour (par exemple, une date qui remonte à quatre mois), utilisez les applets de commande de création de rapports.

Les administrateurs peuvent également être intéressés par l’article [Utilisation d’Excel pour récupérer des données de création de rapports Office 365](http://msdn.microsoft.com/fr-fr/library/dn781442.aspx), qui explique comment utiliser la fonction d’interrogation de données OData de Microsoft Excel pour créer un rapport Office 365 personnalisé. Les rapports personnalisés vous permettent de déterminer quelles données (et quelle quantité de données) sont renvoyées par le service de création de rapports Office 365. Ils permettent aussi d’effectuer d’autres tâches, comme spécifier le mode de tri et de regroupement des données, et accéder à des informations non disponibles dans le centre d’administration Office 365.

Les administrateurs ayant des notions de développement peuvent également utiliser le service web REST pour obtenir les informations non disponibles dans le centre d’administration Skype Entreprise Online. Le service REST est semblable au service SOAP, dans la mesure où chaque technologie permet de transférer des données XML entre un client et un serveur. Toutefois, le service REST présente au moins deux avantages par rapport au service SOAP. D’une part, REST effectue des transferts de données XML via un format standardisé appelé format de syndication ATOM, tandis que SOAP utilise un format non standard lors du transfert de données. D’autre part, REST peut transférer des données entre plusieurs réseaux qui bloquent les verbes HTTP autres que GET et POST.

## Voir aussi

#### Autres ressources

[Création de rapports Lync Online](https://technet.microsoft.com/fr-fr/library/dn362827\(v=ocs.15\))  
[Service web de création de rapports Office 365](http://msdn.microsoft.com/fr-fr/library/office/jj984325.aspx)  
[En savoir plus sur le service web de création de rapports Office 365](http://msdn.microsoft.com/fr-fr/library/office/jj984321.aspx)  
[Cmdlets Exchange Online](http://technet.microsoft.com/fr-fr/library/jj200780\(v=exchg.150\).aspx)  
[Utilisation d’Excel pour récupérer des données de création de rapports Office 365](http://msdn.microsoft.com/fr-fr/library/dn781442.aspx)

