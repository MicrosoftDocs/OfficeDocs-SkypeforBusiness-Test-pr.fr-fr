---
title: Unpublish-CsLisConfiguration
TOCTitle: Unpublish-CsLisConfiguration
ms:assetid: 7fcba482-e1cc-46fa-8b39-fba549eb0fec
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398639(v=OCS.15)
ms:contentKeyID: 49297870
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Unpublish-CsLisConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Removes the Location Information Server (LIS) configuration from the magasin central de gestion. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Unpublish-CsLisConfiguration [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This command removes the LIS configuration from the magasin central de gestion.

    Unpublish-CsLisConfiguration

## Detailed Description

In order to implement Enhanced 9-1-1 (E9-1-1) in Lync Server, you must create a location mapping (called a wiremap). This mapping includes matching physical addresses to ports, subnets, switches, and wireless access points so emergency calls made over an Enterprise Voice connection will reach the nearest emergency operator and provide that operator with the correct location of the caller. This mapping configuration, created by calling cmdlets such as the **Set-CsLisPort** cmdlet and the **Set-CsLisSubnet** cmdlet, is stored in the location configuration database. A configuration can be committed from the location configuration database to the magasin central de gestion by calling the **Publish-CsLisConfiguration** cmdlet, which allows for replication of the data to the Location Information Server. The **Unpublish-CsLisConfiguration** cmdlet removes the LIS configuration from the magasin central de gestion.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Unpublish-CsLisConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Unpublish-CsLisConfiguration"}

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
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Input Types

None.

## Return Types

This cmdlet does not return a value.

## Voir aussi

#### Autres ressources

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

