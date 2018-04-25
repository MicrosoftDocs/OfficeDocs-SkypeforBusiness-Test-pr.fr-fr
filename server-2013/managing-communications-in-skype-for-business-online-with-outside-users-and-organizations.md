---
title: Gestion des communications avec des utilisateurs et des organisations externes
TOCTitle: Gestion des communications avec des utilisateurs et des organisations externes
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56269628
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion des communications avec des utilisateurs et des organisations externes

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande peuvent être utilisées pour gérer la fédération avec des domaines externes et des fournisseurs de messagerie instantanée publics :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Applet de commande</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>Permet aux utilisateurs de communiquer avec tous les domaines à l’exception de ceux spécifiés dans la liste des domaines bloqués.</p>
<p>La fédération est un service qui permet aux utilisateurs d’échanger des messages instantanés et des informations de présence avec les utilisateurs d’autres domaines. En général, les administrateurs utilisent des listes de domaines autorisés et bloqués pour spécifier les domaines extérieurs avec lesquels les utilisateurs peuvent communiquer.</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>Limite la communication des utilisateurs à une collection de domaines spécifiée.</p>
<p>Les utilisateurs pourront communiquer uniquement avec les domaines qui apparaissent dans la liste des domaines autorisés.</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>Modifie les listes des domaines autorisés ou bloqués.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>Active et désactive la fédération avec d’autres domaines et la fédération avec des fournisseurs publics.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>Affecte les valeurs appropriées aux paramètres de configuration hybride.</p>
<p>Dans un déploiement hybride ou de « domaine séparé », certains utilisateurs d’une organisation ont leur compte hébergé sur Skype Entreprise Online, tandis que d’autres ont leur compte hébergé sur Lync Server 2013. Par défaut, les utilisateurs hébergés sur Skype Entreprise Online n’ont pas accès à l’ensemble des fonctionnalités offertes par Voix Entreprise. Pour permettre aux utilisateurs Skype Entreprise Online d’accéder à ces fonctionnalités Voix Entreprise, les administrateurs doivent affecter les valeurs appropriées aux paramètres de configuration hybride. Ces valeurs peuvent seulement être gérées à l’aide des applets de commande <strong>CsTenantHybridConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>Gère la fédération avec des fournisseurs publics.</p>
<p>Les fournisseurs publics sont des organisations offrant des services de communication SIP au grand public. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez la fédération avec les utilisateurs dont le compte est hébergé par ce fournisseur.</p></td>
</tr>
</tbody>
</table>


Vous pouvez également gérer les paramètres de fédération, pour les domaines fédérés et les fournisseurs publics, à l’aide du centre d’administration Skype Entreprise Online :

![Paramètres de l’organisation du centre d’administration de Lync Online](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Paramètres de l’organisation du centre d’administration de Lync Online")

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

