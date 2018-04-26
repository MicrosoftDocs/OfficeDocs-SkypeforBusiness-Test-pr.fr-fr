---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398258(v=OCS.15)
ms:contentKeyID: 49296425
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**Dernière rubrique modifiée :** 2015-03-09_

Définit le point de contrôle de service Active Directory pour le magasin central de gestion. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 définit le point de contrôle de service Active Directory pour la magasin central de gestion Lync Server. Dans cet exemple, le point de contrôle de service pointe sur l’ordinateur atl-sql-001.litwareinc.com et sur l’instance de SQL Server Rtc.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## EXEMPLE 2

La commande présentée dans l’exemple 2 est une variante de celle présentée dans l’exemple 1. Elle définit également le point de contrôle de service Active Directory SCP pour la magasin central de gestion Lync Server. De plus, les informations sur la réussite (ou l’échec) de cette opération sont consignées dans le fichier C:\\Logs\\Store\_Location.html. Ce dernier est généré en incluant le paramètre Report suivi du chemin d’accès au fichier journal.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## Description détaillée

services de domaine Active Directory utilise des points de contrôle de service (SCP) pour faciliter la localisation de services sur les ordinateurs. Par exemple, lorsque vous installez Lync Server, un point de contrôle de service indiquant l’emplacement de cette magasin central de gestion est utilisé pour gérer les données Lync Server. Les ordinateurs qui doivent accéder à la base de données se connectent à Active Directory et utilisent les informations contenues dans le point de contrôle de service pour localiser l’ordinateur et l’instance SQL Server appropriés.

Comme nous l’avons souligné, lorsque vous installez Lync Server un point de contrôle de service est automatiquement créé pour la magasin central de gestion. Si vous souhaitez déplacer cette base de données vers un autre ordinateur ou une autre instance de SQL Server, vous devrez mettre le point de contrôle de service correspondant à jour. Cette tâche peut être exécutée à l’aide de l’applet de commande **Set-CsConfigurationStoreLocation**. Lorsque vous l’exécutez, l’applet de commande **Set-CsConfigurationStoreLocation** recherche dans Active Directory l’ordinateur spécifié par le paramètre SqlServer. Elle définit ensuite l’emplacement du magasin sur le nom de domaine complet de cet ordinateur.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsConfigurationStoreLocation** : RTCUniversalServerAdmins.

## Paramètres


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) de l’ordinateur sur lequel la magasin central de gestion a été installée. Par exemple : -SqlServer atl-sql-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un contrôleur de domaine dans lequel les paramètres globaux sont stockés. Si les paramètres globaux sont stockés dans le conteneur Système Active Directory, ce paramètre doit pointer sur le contrôleur de domaine racine. Si les paramètres globaux sont stockés dans le conteneur de configuration, tout contrôleur de domaine peut être utilisé et ce paramètre peut être omis.</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de l’instance SQL Server contenant les tables et les données de la base de données miroir Lync Server. Par exemple : -SqlInstanceName &quot;rtc&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet de l’ordinateur sur lequel le magasin central de gestion a été installé. Par exemple : -SqlServer atl-mirror-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Si ce paramètre est inclus, l’applet de commande <strong>Set-CsConfigurationStoreLocation</strong> ne vérifiera pas que l’ordinateur et l’instance de SQL Server spécifiés sont disponibles. Elle se limitera à modifier le point de contrôle de service.</p>
<p>Si ce paramètre n’est pas inclus, l’ordinateur et l’instance de SQL Server spécifiés doivent être disponibles avant que le point de contrôle de service ne soit modifié.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de l’instance SQL Server contenant les tables et les données Lync Server. Par exemple : -SqlInstanceName &quot;rtc&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Set-CsConfigurationStoreLocation** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Set-CsConfigurationStoreLocation** ne retourne aucun objet, ni aucune valeur.

## Voir aussi

#### Autres ressources

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

