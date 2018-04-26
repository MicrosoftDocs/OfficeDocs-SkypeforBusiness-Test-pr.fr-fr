---
title: Cmdlets pour le serveur de carnet d’adresses
TOCTitle: Cmdlets pour le serveur de carnet d’adresses
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg415643(v=OCS.15)
ms:contentKeyID: 49296822
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets pour le serveur de carnet d’adresses

 

_**Dernière rubrique modifiée :** 2016-12-08_

Les serveurs de carnet d’adresses sont des intermédiaires entre les services de domaine Active Directory et Microsoft Lync Server 2013. Le serveur de carnet d’adresses veille à ce que les informations utilisateur stockées dans Lync Server 2013 soient synchronisées avec celles stockées dans Active Directory. Pour ce faire, les fichiers de carnet d’adresses sont régulièrement synchronisés avec les informations contenues dans la base de données utilisateur. À son tour, Lync Server inclut des applets de commande de gestion des serveurs de carnet d’adresses.

## Applets de commande pour le serveur de carnet d’adresses

Vous ne pouvez pas configurer les paramètres de serveur de carnet d’adresses dans le Panneau de configuration Lync Server. Windows PowerShell est le principal outil de gestion de ces paramètres. La liste suivante indique les applets de commande directement associées à la gestion des serveurs de carnet d’adresses :

**Serveur de carnet d’adresses**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## Voir aussi

#### Autres ressources

[Blog PowerShell Lync Server](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x40c)

