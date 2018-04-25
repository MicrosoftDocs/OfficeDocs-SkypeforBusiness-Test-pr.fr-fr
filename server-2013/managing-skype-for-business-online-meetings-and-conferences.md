---
title: Gestion des réunions et conférences Lync Online
TOCTitle: Gestion des réunions et conférences Lync Online
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56269634
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion des réunions et conférences Lync Online

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande suivantes permettent de gérer les paramètres des réunions et des conférences :


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
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>Gère les appareils de point de terminaison pour les salles de réunion.</p>
<p>Dans Skype Entreprise Online, les salles de réunion sont des ordinateurs autonomes installés dans des salles de conférence et qui fournissent des fonctionnalités de réunion avancées. Afin de gérer ces nouveaux appareils de point de terminaison, vous devez, entre autres choses, créer et activer un compte de boîte aux lettres de ressource Exchange pour l’appareil, puis activer ce compte pour Skype Entreprise Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>Retourne des informations sur les fournisseurs de services d’audioconférence avec lesquels votre organisation a mis en place des contrats.</p>
<p>Un fournisseur de services d’audioconférence est une entreprise tierce qui propose aux organisations des services de conférence, notamment des services haut de gamme en direct tels que la traduction, la transcription et une assistance opérateur par conférence.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>Contrôle le type des réunions que les utilisateurs peuvent créer et détermine les modalités de gestion des utilisateurs anonymes et de conférence rendez-vous par les réunions.</p>
<p>Les réunions (également appelées conférences) font partie intégrante de Skype Entreprise Online. Avec ces applets de commande, par exemple, vous pouvez configurer les réunions de sorte que les utilisateurs s’y connectant ne soient pas automatiquement admis, mais plutôt acheminés vers la salle d’attente de la réunion. Les utilisateurs qui se connectent demeurent dans la salle d’attente jusqu’à ce qu’un présentateur les admette à la réunion.</p></td>
</tr>
</tbody>
</table>


Vous pouvez également gérer un petit sous-ensemble de propriétés de configuration de réunion à l’aide du centre d’administration Skype Entreprise Online :

![Propriétés des options générales du centre d’administration Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Propriétés des options générales du centre d’administration Lync")

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

