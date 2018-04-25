---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56269561
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Indique si les informations de licence du client spécifié sont disponibles dans le centre d’administration Lync.

Cette applet de commande peut seulement être utilisée avec Lync Online.

## Syntaxe

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## Description détaillée

L’applet de commande Get-CsTenantLicensingConfiguration indique si les informations de licence du client spécifié sont disponibles dans le centre d’administration Lync. L’applet de commande retourne des informations semblables à ce qui suit :

Identity : Global  
Status : Enabled

Si la valeur Status est définie sur Enabled, les informations de licence sont disponibles dans le centre d’administration Lync. Sinon, elles ne sont pas disponibles dans le centre d’administration Lync.

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
<td><p><strong>Filter</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet d’utiliser des caractères génériques afin de retourner une collection de paramètres de configuration des licences de client. Comme chaque client est limité à une collection unique et globale de paramètres de configuration des licences, il n’y a pas besoin d’utiliser le paramètre Filter.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Spécifie la collection de paramètres de configuration des licences de client à retourner. Comme chaque client est limité à une collection unique et globale de paramètres de licence, il n’y a pas besoin d’inclure ce paramètre lors de l’appel de l’applet de commande Get-CsTenantLicensingConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données de configuration des licences de client du réplica local du magasin central de gestion et non du magasin central de gestion proprement dit.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID du compte de client dont les paramètres de licence sont retournés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

L’applet de commande Get-CsTenantLicensingConfiguration n’accepte pas les entrées redirigées.

## Types de retours

L’applet de commande Get-CsTenantLicensingConfiguration retourne les instances de l’objet Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration.

## Exemple

La commande illustrée dans l’exemple 1 retourne les informations de configuration des licences pour le client :

    Get-CsTenantLicensingConfiguration

