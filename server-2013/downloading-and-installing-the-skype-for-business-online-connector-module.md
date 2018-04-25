---
title: Téléchargement et installation du module Lync Online Connector
TOCTitle: Téléchargement et installation du module Lync Online Connector
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56269641
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Téléchargement et installation du module Lync Online Connector

 

_**Dernière rubrique modifiée :** 2016-12-08_

Le module Skype Entreprise Online Connector inclut l’applet de commande **New-CsOnlineSession** qui vous permet de créer une session Windows PowerShell à distance qui se connecte à Skype Entreprise Online. Ce module, pris en charge sur les ordinateurs 64 bits uniquement (pour plus d’informations, voir [Configuration de votre ordinateur pour la gestion de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)) peut être téléchargé à partir du Centre de téléchargement Microsoft à l’adresse [http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688). Téléchargez le fichier LyncOnlinePowershell.exe, puis effectuez la procédure suivante :

1.  Double-cliquez sur le fichier **LyncOnlinePowershell.exe**.

2.  Dans l’Assistant Configuration PowerShell du client Skype Entreprise Online, sur la page **Microsoft Software License Terms**, sélectionnez **I accept the terms in the License Agreement**, puis cliquez sur **Install**. Si la boîte de dialogue **User Account Control** apparaît, cliquez sur **Yes** pour continuer l’installation.

3.  Sur la page **Completed the Microsoft Lync Online, Tenant PowerShell Setup**, cliquez sur **Finish**.

Le programme d’installation copie le module Skype Entreprise Online Connector (et l’applet de commande **New-CsOnlineSession**) sur votre ordinateur local. Pour accéder au module, démarrez une session Windows PowerShell avec des informations d’identification d’administrateur, puis exécutez la commande suivante :

    Import-Module LyncOnlineConnector

Si vous ne voulez pas taper cette commande chaque fois que vous démarrez Windows PowerShell, vous pouvez ajouter la commande à votre profil Windows PowerShell. Pour ce faire, tapez la commande suivante à l’invite de commandes Windows PowerShell, puis appuyez sur Entrée :

    notepad.exe $profile

Lorsque le Bloc-notes apparaît, ajoutez la ligne suivante au bas des commandes déjà présentes dans le profil (le cas échéant) :

    Import-Module LyncOnlineConnector

Enregistrez le fichier. La prochaine fois que vous démarrez Windows PowerShell, le module Skype Entreprise Online Connector est importé automatiquement. Notez que vous recevrez un message d’erreur et que le module ne sera pas chargé si vous n’exécutez pas Windows PowerShell avec des informations d’identification d’administrateur.

Outre l’installation du module Skype Entreprise Online Connector, LyncOnlinePowershell.exe installe également deux composants supplémentaires : .NET Framework 4.5 et le package Microsoft Visual C++ 2012 Redistributable (x64) (version 11.0.50727). .NET Framework 4.5 fournit l’infrastructure utilisée pour la création et l’exécution des applications .NET, y compris Windows PowerShell. Le package Visual C++ Redistributable installe les composants d’exécution Visual C++ pour les ordinateurs sur lesquels Microsoft Visual Studio 2012 n’est pas installé.

## Voir aussi

#### Concepts

[Configuration de votre ordinateur pour la gestion de Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

