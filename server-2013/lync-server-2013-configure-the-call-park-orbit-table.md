---
title: 'Lync Server 2013 : Configuration de la table d’orbites de parcage d’appel'
TOCTitle: Configuration de la table d’orbites de parcage d’appel
ms:assetid: e5cc0c19-7b2c-48e7-a21d-cfb23c842f0f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399020(v=OCS.15)
ms:contentKeyID: 49299153
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configuration de la table d’orbites de parcage d’appel dans Lync Server 2013

 

_**Dernière rubrique modifiée :** 2012-09-10_

L’parcage d’appel utilise des orbites pour parquer les appels. Pour permettre aux utilisateurs de parquer et de récupérer des appels, vous devez configurer le tableau des orbites de parcage d’appel. Vous devez spécifier les plages de numéros de poste (orbites) que votre entreprise réservera au parcage d’appel et définir le routage de ces plages en indiquant le pool de parcage d’appel qui gère chacune d’elles. Lorsque vous définissez des plages d’orbites, l’objectif est de disposer de suffisamment d’orbites pour éviter d’avoir à réutiliser trop rapidement une orbite, mais sans que leur nombre soit trop élevé afin de pouvoir limiter le nombre de postes disponibles pour les utilisateurs ou d’autres services. Vous pouvez créer plusieurs plages d’orbites de parcage d’appel pour chaque pool Lync Server dans lequel le application de parcage d’appel est déployé. Chacune des plages d’orbites de parcage d’appel doit être pourvue d’un nom global unique et d’un ensemble unique de postes.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une plage d’orbites comprend généralement au moins 100 orbites. Chaque plage peut être plus importante à condition qu’elle contienne moins de 10 000 orbites et que chaque pool comporte moins de 50 000 orbites. Si une plage est trop petite, les orbites sont réutilisées plus rapidement.</td>
</tr>
</tbody>
</table>


Utilisez des blocs de postes virtuels (postes attribués à aucun utilisateur ni téléphone) pour vos plages d’orbites.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il n’est pas possible d’affecter des numéros SDA (sélection directe à l’arrivée, Direct Inward Dialing [DID]) comme numéros d’orbites dans la table des orbites de parcage d’appel.</td>
</tr>
</tbody>
</table>


## Dans cette section

[Création ou modification d’une plage d’orbites de parcage d’appel dans Lync Server 2013](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)

