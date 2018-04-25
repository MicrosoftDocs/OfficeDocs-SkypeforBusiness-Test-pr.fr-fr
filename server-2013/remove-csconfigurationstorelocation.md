---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398214(v=OCS.15)
ms:contentKeyID: 49296332
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime le point de contrôle de service Active Directory pour le magasin central de gestion. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 supprime le point de contrôle de service Active Directory pour le magasin central de gestion. Pour le restaurer (ou pour en créer un nouveau), vous devez exécuter l’applet de commande **Set-CsConfigurationStoreLocation**.

    Remove-CsConfigurationStoreLocation

## EXEMPLE 2

L’exemple 2 supprime également le point de contrôle de service Active Directory pour le magasin central de gestion. Outre la suppression du point de contrôle de service, cette commande enregistre des informations sur la réussite (ou l’échec) de l’opération dans le fichier journal C:\\Logs\\Store\_Location.html. Pour créer ce fichier, la commande utilise le paramètre Report suivi du chemin d’accès au fichier journal dans lequel les informations doivent être enregistrées. Si ce fichier existe déjà, le contenu sera remplacé lors de l’exécution de la commande. S’il n’existe pas, il est créé lors de l’exécution de la commande.

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## Description détaillée

services de domaine Active Directory utilise des points de contrôle de service (SCP) pour faciliter la localisation de services sur les ordinateurs. Par exemple, lorsque vous installez Lync Server, un point de contrôle de service indiquant l’emplacement de ce magasin central de gestion est utilisé pour gérer les données Lync Server. Les ordinateurs qui doivent accéder à la base de données se connectent à Active Directory et utilisent les informations contenues dans le point de contrôle de service pour les aider à localiser le bon ordinateur et l’instance SQL Server appropriée.

Comme nous l’avons souligné, lorsque vous installez Lync Server, un point de contrôle de service est automatiquement créé pour le magasin central de gestion. En règle générale, vous ne voulez pas supprimer ce point de contrôle de service ; si vous le faites, les ordinateurs ne seront plus en mesure de localiser la base de données. Cependant, dans certains cas (éventuellement lors de la résolution d’un problème), il est possible que vous deviez supprimer le point de contrôle de service. Pour cela, utilisez l’applet de commande **Remove-CsConfigurationStoreLocation**. Une fois le point de contrôle de service supprimé, vous pouvez le recréer (ou en créer un) à l’aide de l’applet de commande **Set-CsConfigurationStoreLocation**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter l’applet de commande **Remove-CsConfigurationStoreLocation** : RTCUniversalServerAdmins.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un contrôleur de domaine dans lequel les paramètres globaux sont stockés. Si les paramètres globaux sont stockés dans le conteneur Système Active Directory, ce paramètre doit pointer sur le contrôleur de domaine racine. Si les paramètres globaux sont stockés dans le conteneur de configuration, tout contrôleur de domaine peut être utilisé et ce paramètre peut être omis.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Remove-CsConfigurationStoreLocation** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Remove-CsConfigurationStoreLocation** ne renvoie ni valeur ni objet.

## Voir aussi

#### Autres ressources

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

