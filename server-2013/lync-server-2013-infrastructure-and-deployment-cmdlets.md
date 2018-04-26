---
title: Cmdlets d’infrastructure et de déploiement
TOCTitle: Cmdlets d’infrastructure et de déploiement
ms:assetid: 0a6e872a-9f70-4f23-a4a5-8820dbf55370
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398153(v=OCS.15)
ms:contentKeyID: 49296210
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets d’infrastructure et de déploiement

 

_**Dernière rubrique modifiée :** 2016-12-08_

Les applets de commande d’infrastructure et de déploiement incluses dans Microsoft Lync Server 2013 peuvent s’avérer utiles lors de la configuration et du déploiement du produit ; une fois que Lync Server a été déployé, ces applets de commande peuvent servir à d’autres tâches, comme vérifier que les composants fonctionnent comme prévu, gérer les paramètres de réplication et sauvegarder et restaurer les topologies, les stratégies et les paramètres de configuration de Lync Server.

## Applets de commande d’infrastructure et de déploiement

Les administrateurs auront rarement besoin d’appeler des applets de commande d’infrastructure et de déploiement. En effet, ces applets de commande sont automatiquement invoquées lorsque vous exécutez l’Assistant Configuration ou le Générateur de topologie. (Une exception majeure étant l’applet de commande **Export-CsConfiguration**, qui vous permet de créer une copie de sauvegarde des topologies, stratégies et paramètres de configuration Lync Server.) Cependant, les applets de commande d’infrastructure et de déploiement peuvent le cas échéant être exécutées depuis Lync Server Management Shell ou directement à l’aide d’un script. Notez que l’utilisation d’un script vous permet d’automatiser certaines tâches. La liste suivante indique les applets de commande qui sont directement associées à l’infrastructure et au déploiement :

**[Cmdlets Active Directory](lync-server-2013-active-directory-cmdlets.md)**

  -   
    [Disable-CsAdDomain](disable-csaddomain.md)

  -   
    [Enable-CsAdDomain](enable-csaddomain.md)

  -   
    [Get-CsAdDomain](get-csaddomain.md)

  -   
    [Disable-CsAdForest](disable-csadforest.md)

  -   
    [Enable-CsAdForest](enable-csadforest.md)

  -   
    [Get-CsAdForest](get-csadforest.md)

  -   
    [Get-CsAdServerSchema](get-csadserverschema.md)

  -   
    [Install-CsAdServerSchema](install-csadserverschema.md)

**[Cmdlets de réplication](lync-server-2013-replication-cmdlets.md)**

  -   
    [Debug-CsInterPoolReplication](debug-csinterpoolreplication.md)

  -   
    [Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

  -   
    [Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

  -   
    [Enable-CsReplica](enable-csreplica.md)

  -   
    [Test-CsReplica](test-csreplica.md)

  -   
    [Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)

  -   
    [New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)

  -   
    [Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

  -   
    [Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

**[Cmdlets de topologie](lync-server-2013-topology-cmdlets.md)**

  -   
    [Get-CsPool](get-cspool.md)

  -   
    [Get-CsSite](get-cssite.md)

  -   
    [Set-CsSite](set-cssite.md)

  -   
    [Enable-CsTopology](enable-cstopology.md)

  -   
    [Get-CsTopology](get-cstopology.md)

  -   
    [Publish-CsTopology](publish-cstopology.md)

  -   
    [Test-CsTopology](test-cstopology.md)

  -   
    [Export-CsConfiguration](export-csconfiguration.md)

  -   
    [Import-CsConfiguration](import-csconfiguration.md)

  -   
    [Get-CsServerVersion](get-csserverversion.md)

  -   
    [Disable-CsComputer](disable-cscomputer.md)

  -   
    [Enable-CsComputer](enable-cscomputer.md)

  -   
    [Get-CsComputer](get-cscomputer.md)

  -   
    [Test-CsComputer](test-cscomputer.md)

  -   
    [Get-CsNetworkInterface](get-csnetworkinterface.md)

**[Applets de commande pour la sauvegarde et la haute disponibilité](lync-server-2013-backup-and-high-availability-cmdlets.md)**

  - [Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

  - [Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

  - [Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

  - [Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

  - [Invoke-CsBackupServiceSync](invoke-csbackupservicesync.md)

  - [Debug-CsIntraPoolReplication](debug-csintrapoolreplication.md)

  - [Backup-CsPool](backup-cspool.md)

  - [Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

  - [Get-CsPoolFabricState](get-cspoolfabricstate.md)

  - [Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

  - [Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

  - [Get-CsPoolUpgradeReadinessState](get-cspoolupgradereadinessstate.md)

  - [Invoke-CsStorageServiceFlush](invoke-csstorageserviceflush.md)

  - [Sync-CsUserData](sync-csuserdata.md)

  - [Remove-CsUserStoreBackupData](remove-csuserstorebackupdata.md)

## Voir aussi

#### Autres ressources

[Blog PowerShell Lync Server](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x40c)

