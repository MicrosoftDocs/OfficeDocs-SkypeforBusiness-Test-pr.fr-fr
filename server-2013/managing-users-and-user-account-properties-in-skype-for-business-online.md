---
title: Gestion des utilisateurs et des propriétés de compte d’utilisateur
TOCTitle: Gestion des utilisateurs et des propriétés de compte d’utilisateur
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56269595
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion des utilisateurs et des propriétés de compte d’utilisateur

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande suivantes permettent de gérer les comptes d’utilisateur Skype Entreprise Online.


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
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>Retourne des informations sur les utilisateurs dont les comptes sont hébergés auprès de votre client Skype Entreprise Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>Permet d’affecter, de modifier ou d’annuler l’affectation d’un fournisseur de services d’audioconférence auprès d’utilisateurs individuels.</p>
<p>Un fournisseur de services d’audioconférence est une entreprise tierce qui propose aux organisations des services de conférence, notamment des services haut de gamme en direct tels que la traduction, la transcription et une assistance opérateur par conférence.</p>
<p>Ces applets de commande ne retournent pas des informations sur les fournisseurs de services d’audioconférence pouvant être affectés à ces utilisateurs. Pour obtenir ces informations, exécutez la commande suivante :</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412910.warning(OCS.15).gif" title="warning" alt="warning" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’applet de commande Set-CsUser est également incluse dans l’ensemble d’applets de commande disponible pour les administrateurs Skype Entreprise Online. Il n’est toutefois pas possible de l’utiliser pour gérer Skype Entreprise Online pour le moment, sauf pour la définition du paramètre AudioVideoDisabled. Si vous tentez de l’exécuter avec n’importe quel autre paramètre, la commande échouera avec un message d’erreur semblable à ce qui suit :<br />
Impossible de définir « SipAddress ». Ce paramètre est limité dans la session PowerShell distante du client.</td>
</tr>
</tbody>
</table>


Les fournisseurs de services d’audioconférence peuvent également être affectés à des comptes d’utilisateur (ou l’affectation existante annulée) à l’aide du centre d’administration Skype Entreprise Online :

![Propriétés des téléconférences du centre d’administration Lync](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Propriétés des téléconférences du centre d’administration Lync")

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

