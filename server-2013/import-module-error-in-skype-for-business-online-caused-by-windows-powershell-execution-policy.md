---
title: Erreur d’importation de module due à une stratégie d’exécution Windows PowerShell
TOCTitle: Erreur d’importation de module due à une stratégie d’exécution Windows PowerShell
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56269587
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Erreur d’importation de module due à une stratégie d’exécution Windows PowerShell

 

_**Dernière rubrique modifiée :** 2016-12-08_

La stratégie d’exécution de Windows PowerShell permet de déterminer les fichiers de configuration pouvant être chargés dans la console Windows PowerShell et les scripts qu’un utilisateur peut exécuter à partir de cette console. Au minimum, le module Skype Entreprise Online Connector ne peut pas être importé sauf si la stratégie d’exécution a été définie sur RemoteSigned. Si ce n’est pas le cas, vous recevrez le message d’erreur suivant lorsque vous tentez d’importer le module :

    Import-Module : Impossible de charger le fichier C:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1, car l'exécution de scripts est désactivée sur ce système. Pour plus d'informations, consultez about_Execution_Policies à l'adresse http://go.microsoft.com/fwlink/?LinkID=135170.

Pour résoudre ce problème, démarrez Windows PowerShell en tant qu’administrateur, puis exécutez la commande suivante :

    Set-ExecutionPolicy RemoteSigned

Pour plus d’informations sur la stratégie d’exécution, voir la rubrique d’aide à l’adresse [http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170).

## Voir aussi

#### Concepts

[Diagnostic et résolution des problèmes de connexion avec Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

