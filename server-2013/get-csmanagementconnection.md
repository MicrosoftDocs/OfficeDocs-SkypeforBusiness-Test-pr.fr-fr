---
title: Get-CsManagementConnection
TOCTitle: Get-CsManagementConnection
ms:assetid: b0e2377c-6aab-45d8-b71d-0d37c6f6dae3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412849(v=OCS.15)
ms:contentKeyID: 49298537
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsManagementConnection

 

_**Dernière rubrique modifiée :** 2015-03-09_

Returns information about the management connection to the magasin central de gestion. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsManagementConnection

## Examples

## EXAMPLE 1

The command in Example 1 returns information about the management connection to the magasin central de gestion.

    Get-CsManagementConnection

## Detailed Description

Configuration data for Lync Server is stored in the magasin central de gestion; it is crucial that both Windows PowerShell and the management replica services be able to locate this database. When you install Lync Server, a service control point is created in services de domaine Active Directory that provides location information for this database. Typically, computers rely on this service control point in order to connect to the magasin central de gestion. To see the details behind this connection (that is, if you want to know which computer the magasin central de gestion is running on, as well information about the SQL Server connection to that magasin central de gestion) you can run the **Get-CsManagementConnection** cmdlet.

If you have used the **Set-CsManagementConnection** cmdlet to set up a temporary management connection for your current instance of Windows PowerShell (for example, in order to work from the local replica), the **Get-CsManagementConnection** cmdlet will report back information for that temporary connection. By comparison, the **Get-CsConfigurationStoreLocation** cmdlet always returns information for the service control point in Active Directory, regardless of where the local management connection is pointed.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsManagementConnection** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsManagementConnection"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>This cmdlet provides only common Windows PowerShell parameters.</p></td>
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


## Input Types

None. The **Get-CsManagementConnection** cmdlet does not accept pipelined input.

## Return Types

The **Get-CsManagementConnection** cmdlet returns instances of the Microsoft.Rtc.Management.Xds.ManagementConnection object.

## Voir aussi

#### Autres ressources

[Remove-CsManagementConnection](remove-csmanagementconnection.md)  
[Set-CsManagementConnection](set-csmanagementconnection.md)

