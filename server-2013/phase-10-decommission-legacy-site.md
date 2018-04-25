---
title: 'Phase 10 : Mise hors service d’un site hérité'
TOCTitle: 'Phase 10 : Mise hors service d’un site hérité'
ms:assetid: d591a310-3b5c-4092-b19e-0349616e40df
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ205300(v=OCS.15)
ms:contentKeyID: 49298974
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Phase 10 : Mise hors service d’un site hérité

 

_**Dernière rubrique modifiée :** 2016-12-08_

Les rubriques suivantes donnent des conseils quant à la mise hors service de pools et à la désactivation et la suppression de serveurs et de pools d’un déploiement hérité de Office Communications Server 2007 R2. Certaines des procédures répertoriées dans cette section ne sont pas requises. Lisez les informations de chacune de ces rubriques pour déterminer la procédure de mise hors service à utiliser.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />Mise en garde :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous avez importé des annuaires des conférences pour la Conférence rendez-vous vers Lync Server 2013, il est important d’en transmettre la propriété à Lync Server 2013 avant de commencer à mettre hors service vos pools. Si vous mettez hors service un pool sans transmettre la propriété des annuaires des conférences au préalable, la fonctionnalité de conférence rendez-vous ne fonctionnera plus pour toutes les réunions migrées. Vous devez effectuer l’étape de transmission de propriété une fois pour chaque annuaire des conférences compris dans votre pool hérité.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour plus d’informations sur la migration et la mise à niveau des applications Microsoft Unified Communications Managed API (UCMA) avant la mise hors service de votre environnement hérité, reportez-vous à <a href="http://go.microsoft.com/fwlink/p/?linkid=269555">http://go.microsoft.com/fwlink/p/?LinkId=269555</a></td>
</tr>
</tbody>
</table>


## Dans cette section

  - [Déplacement des annuaires de conférences](move-conference-directories.md)

  - [Mise à jour des enregistrements SRV DNS](update-dns-srv-records_1.md)

  - [Désactivation des serveurs et des pools \[OCS 2007 R2 vers W15\]](decommissioning-servers-and-pools.md)

  - [Suppression de BackCompatSite](remove-backcompatsite.md)

