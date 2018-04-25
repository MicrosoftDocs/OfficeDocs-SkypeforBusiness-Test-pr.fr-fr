---
title: Gestion du client Lync
TOCTitle: Gestion du client Lync
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56269656
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion du client Lync

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande suivantes permettent de gérer le client Lync :


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
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>Retourne des informations sur les restrictions d’URI utilisées dans votre organisation.</p>
<p>Lors de l’envoi de messages instantanés, les utilisateurs peuvent incorporer un URI dans le texte d’un message pour proposer aux autres participants de la conversation un site web ou un partage particulier. Skype Entreprise Online peut être configuré de sorte que les liens hypertexte comportant certains préfixes soient bloqués ou désactivés.Ainsi, les participants ne pourront pas cliquer sur le lien pour être redirigés vers le site référencé par l’URI, mais devront copier et coller le lien manuellement dans un navigateur.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>Retourne des informations sur deux aspects importants des abonnements aux informations de présence : les abonnés avertis et les abonnements aux catégories.</p>
<p>Lorsque vous êtes ajouté à la liste de contacts d’une autre personne, vous recevez par défaut une notification contextuelle vous informant que vous avez été ajouté à cette liste. Jusqu’à ce que cette boîte de dialogue soit fermée, chaque notification compte comme un abonné averti.</p>
<p>Les abonnements aux catégories représentent une demande de catégorie spécifique d’informations ; par exemple, une application qui demande des données de calendrier.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>Configure les valeurs de confidentialité par défaut dans Skype Entreprise Online, tout en permettant aux utilisateurs de modifier ces valeurs.</p>
<p>Skype Entreprise Online donne aux utilisateurs la possibilité de partager un large éventail d’informations de présence avec d’autres personnes. Les utilisateurs peuvent publier une photographie d’eux-mêmes, donner des informations détaillées sur leur zone géographique et partager automatiquement des informations de présence avec toute l’organisation (plutôt qu’uniquement avec les personnes de leur liste de contacts). Les applets de commande <strong>CsPrivacyConfiguration</strong> permettent aux administrateurs de configurer les valeurs de confidentialité par défaut dans Skype Entreprise Online, tout en laissant aux utilisateurs la possibilité de changer ces valeurs.</p></td>
</tr>
</tbody>
</table>


Vous pouvez également gérer un sous-ensemble de paramètres de configuration de la confidentialité à l’aide du centre d’administration Skype Entreprise Online :

![Paramètres du mode privé de présence du centre d’administration Lync](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Paramètres du mode privé de présence du centre d’administration Lync")

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

