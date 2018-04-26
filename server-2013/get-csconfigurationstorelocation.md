---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412814(v=OCS.15)
ms:contentKeyID: 49298492
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne l’emplacement du point de contrôle du service Active Directory pour le magasin central de gestion. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 retourne le chemin SQL Server à l’ordinateur (ou au pool) hébergeant le magasin central de gestion.

    Get-CsConfigurationStoreLocation

## EXEMPLE 2

L’exemple 2 est une variation de la commande présentée à l’exemple 1. Dans ce cas, toutefois, le paramètre Report est inclus pour permettre d’indiquer le chemin du rapport qui sera généré à l’exécution de l’applet de commande **Get-CsConfigurationStoreLocation**.

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## Description détaillée

Les services de domaine Active Directory utilisent des points de contrôle de service (SCP) pour faciliter la localisation de services sur les ordinateurs. Par exemple, lorsque vous installez Lync Server, un point de contrôle de service indiquant l’emplacement de ce magasin central de gestion est utilisé pour gérer les données Lync Server. Les ordinateurs qui doivent accéder à la base de données se connectent à Active Directory et utilisent les informations contenues dans le point de contrôle de service pour localiser le bon ordinateur et l’instance SQL Server appropriée.

L’applet de commande **Get-CsConfigurationStoreLocation** permet de retourner le chemin SQL Server (par exemple, atl-sql-001.litwareinc.com/rtc) à l’ordinateur exécutant le magasin central de gestion.

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un contrôleur de domaine dans lequel les paramètres globaux sont stockés. Si les paramètres globaux sont stockés dans le conteneur Système Active Directory, ce paramètre doit pointer sur le contrôleur de domaine racine. Si les paramètres globaux sont stockés dans le conteneur Configuration, tout contrôleur de domaine peut être utilisé et ce paramètre peut être omis.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\ConfigurationStore.html&quot;.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsConfigurationStoreLocation** n’accepte pas les données redirigées.

## Types de retours

Chaîne. L’applet de commande **Get-CsConfigurationStoreLocation** retourne l’emplacement du magasin de configuration.

## Voir aussi

#### Autres ressources

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

