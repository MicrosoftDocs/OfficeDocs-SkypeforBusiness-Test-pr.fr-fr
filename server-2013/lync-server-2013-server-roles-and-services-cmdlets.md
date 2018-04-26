---
title: Cmdlets de rôles serveur et de services
TOCTitle: Cmdlets de rôles serveur et de services
ms:assetid: ff3561de-043e-4071-88f7-8de3cded52f6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg415683(v=OCS.15)
ms:contentKeyID: 49299456
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de rôles serveur et de services

 

_**Dernière rubrique modifiée :** 2016-12-08_

De nombreux composants Microsoft Lync Server 2013 s’exécutent en tant que rôles serveur ou que services. Lync Server 2013 est fourni avec un certain nombre de cmdlets qui vous permettent de gérer ces rôles de serveur et ces services.

## Cmdlets de rôles serveur et de services

Plusieurs tâches de gestion (mais pas toutes) qui s’appliquent aux serveurs et aux rôles de serveur peuvent être effectuées à partir du Panneau de configuration Lync Server. Par exemple, vous pouvez gérer les paramètres du serveur d’archivage mais pas les paramètres du serveur de carnet d’adresses à l’aide du Panneau de configuration Lync Server. Toutefois, toutes ces tâches peuvent être effectuées à l’aide des cmdlets depuis Lync Server Management Shell ou depuis un script ; l’utilisation d’un script vous permet d’automatiser certaines tâches. La liste suivante contient les cmdlets qui sont directement associées à la gestion des rôles serveur et des services :

**[Cmdlets pour le serveur de carnet d’adresses](lync-server-2013-address-book-server-cmdlets.md)**

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

**[Cmdlets d’archivage et de surveillance](lync-server-2013-archiving-and-monitoring-cmdlets.md)**

  -   
    [Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

  -   
    [New-CsArchivingConfiguration](new-csarchivingconfiguration.md)

  -   
    [Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)

  -   
    [Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)

  -   
    [Export-CsArchivingData](export-csarchivingdata.md)

  -   
    [Invoke-CsArchivingDatabasePurge](invoke-csarchivingdatabasepurge.md)

  -   
    [Get-CsArchivingPolicy](get-csarchivingpolicy.md)

  -   
    [Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)

  -   
    [New-CsArchivingPolicy](new-csarchivingpolicy.md)

  -   
    [Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)

  -   
    [Set-CsArchivingPolicy](set-csarchivingpolicy.md)

  -   
    [Set-CsArchivingServer](set-csarchivingserver.md)

  -   
    [Get-CsCdrConfiguration](get-cscdrconfiguration.md)

  -   
    [New-CsCdrConfiguration](new-cscdrconfiguration.md)

  -   
    [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

  -   
    [Set-CsCdrConfiguration](set-cscdrconfiguration.md)

  -   
    [Set-CsMonitoringServer](set-csmonitoringserver.md)

  -   
    [Get-CsQoEConfiguration](get-csqoeconfiguration.md)

  -   
    [New-CsQoEConfiguration](new-csqoeconfiguration.md)

  -   
    [Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)

  -   
    [Set-CsQoEConfiguration](set-csqoeconfiguration.md)

[Invoke-CsCdrDatabasePurge](invoke-cscdrdatabasepurge.md)

  -   
    [Export-CsArchivingData](export-csarchivingdata.md)

  -   
    [Invoke-CsQoEDatabasePurge](invoke-csqoedatabasepurge.md)

  -   
    [Get-CsReportingConfiguration](get-csreportingconfiguration.md)

  -   
    [New-CsReportingConfiguration](new-csreportingconfiguration.md)

  -   
    [Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)

  -   
    [Set-CsReportingConfiguration](set-csreportingconfiguration.md)

  -   
    [Get-CsTestUserCredential](get-cstestusercredential.md)

  -   
    [Remove-CsTestUserCredential](remove-cstestusercredential.md)

  -   
    [Set-CsTestUserCredential](set-cstestusercredential.md)

  -   
    [Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)

  -   
    [New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)

  -   
    [Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)

  -   
    [Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

  -   
    [Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

  -   
    [New-CsExtendedTest](new-csextendedtest.md)

**[Cmdlets de base de données et du serveur d’administration](lync-server-2013-database-and-management-server-cmdlets.md)**

  -   
    [Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)

  -   
    [Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

  -   
    [Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

  -   
    [Install-CsDatabase](install-csdatabase.md)

  -   
    [Test-CsDatabase](test-csdatabase.md)

  -   
    [Uninstall-CsDatabase](uninstall-csdatabase.md)

  - [Invoke-CsDatabaseFailover](invoke-csdatabasefailover.md)

  - [Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)

  - [Install-CsMirrorDatabase](install-csmirrordatabase.md)

  - [Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

  -   
    [Get-CsUserDatabaseState](get-csuserdatabasestate.md)

  -   
    [Set-CsUserDatabaseState](set-csuserdatabasestate.md)

  -   
    [Update-CsUserDatabase](update-csuserdatabase.md)

  -   
    [Move-CsManagementServer](move-csmanagementserver.md)

  -   
    [Set-CsManagementServer](set-csmanagementserver.md)

  - [Invoke-CsManagementServerFailover](invoke-csmanagementserverfailover.md)

**[Applets de commande de serveur Edge](lync-server-2013-edge-server-cmdlets.md)**

  -   
    [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  -   
    [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  -   
    [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  -   
    [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  -   
    [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  -   
    [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  -   
    [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  -   
    [Set-CsEdgeServer](set-csedgeserver.md)

**[Autres cmdlets de rôle serveur](lync-server-2013-other-server-role-cmdlets.md)**

  -   
    [Set-CsConferenceServer](set-csconferenceserver.md)

  -   
    [Set-CsUserServer](set-csuserserver.md)

**[Cmdlets des serveurs d’inscriptions et directeurs](lync-server-2013-registrar-and-director-cmdlets.md)**

  -   
    [Set-CsDirector](set-csdirector.md)

  -   
    [Reset-CsPoolRegistrarState](reset-cspoolregistrarstate.md)

  -   
    [Set-CsRegistrar](set-csregistrar.md)

  -   
    [Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)

  -   
    [New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)

  -   
    [Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)

  -   
    [Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

  -   
    [Test-CsRegistration](test-csregistration.md)

**[Cmdlets de services](lync-server-2013-services-cmdlets.md)**

  -   
    [Get-CsService](get-csservice.md)

  -   
    [Get-CsWindowsService](get-cswindowsservice.md)

  -   
    [Start-CsWindowsService](start-cswindowsservice.md)

  -   
    [Stop-CsWindowsService](stop-cswindowsservice.md)

**[Cmdlets de résolution des problèmes relatifs aux rôles serveur et aux services](lync-server-2013-troubleshooting-server-roles-and-services-cmdlets.md)**

  -   
    [Get-CsAudioTestServiceApplication](get-csaudiotestserviceapplication.md)

  -   
    [Set-CsAudioTestServiceApplication](set-csaudiotestserviceapplication.md)

  -   
    [Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)

  -   
    [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)

  -   
    [Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)

  -   
    [Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)

  -   
    [Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)

  -   
    [New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)

  -   
    [Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)

  -   
    [Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

  -   
    [New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)

  -   
    [Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)

  -   
    [New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)

  -   
    [Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)

  -   
    [Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

**[Cmdlets de serveur et de service Web](lync-server-2013-web-server-and-services-cmdlets.md)**

  -   
    [New-CsSimpleUrl](new-cssimpleurl.md)

  -   
    [Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

  -   
    [New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)

  -   
    [Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)

  -   
    [Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

  -   
    [New-CsSimpleUrlEntry](new-cssimpleurlentry.md)

  -   
    [Set-CsWebServer](set-cswebserver.md)

  -   
    [Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)

  -   
    [New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)

  -   
    [Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)

  -   
    [Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

  -   
    [New-CsWebTrustedCACertificate](new-cswebtrustedcacertificate.md)

  -   
    [New-CsKerberosAccount](new-cskerberosaccount.md)

  -   
    [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  -   
    [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  -   
    [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  -   
    [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  - [Test-CsWebApp](test-cswebapp.md)

  - [Test-CsWebAppAnonymous](test-cswebappanonymous.md)

## Voir aussi

#### Autres ressources

[Blog Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x40c)

