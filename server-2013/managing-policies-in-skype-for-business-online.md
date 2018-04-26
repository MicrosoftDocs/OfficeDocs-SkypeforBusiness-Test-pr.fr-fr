---
title: Gestion des stratégies
TOCTitle: Gestion des stratégies
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56269626
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion des stratégies

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande suivantes gèrent les stratégies Skype Entreprise Online. Celles-ci permettent de déterminer les fonctionnalités Skype Entreprise Online accessibles aux utilisateurs et à l’organisation dans son ensemble.


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
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>Les stratégies de clients permettent de déterminer les fonctionnalités client Lync accessibles aux utilisateurs. Par exemple, vous pouvez transférer des fichiers à certains utilisateurs, mais pas à d’autres.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>Les stratégies de conférence déterminent les fonctionnalités pouvant être utilisées durant une conférence, depuis l’intégration de la fonction IP audio et vidéo, jusqu’au nombre maximum de personnes pouvant participer à une réunion.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>Les stratégies d’accès externe permettent de déterminer si vos utilisateurs sont autorisés à communiquer avec des utilisateurs à partir de domaines fédérés, et/ou si vos utilisateurs peuvent communiquer avec des utilisateurs dont le compte est hébergé auprès d’un fournisseur de messagerie instantanée public, tel que Windows Live ou AOL.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>Les stratégies de voix permettent de gérer les fonctionnalités Voix Entreprise comme la sonnerie simultanée (possibilité d’avoir une deuxième sonnerie de téléphone chaque fois que quelqu’un appelle sur votre téléphone professionnel) et le transfert d’appel.</p></td>
</tr>
</tbody>
</table>


Vous pouvez également gérer certains paramètres de stratégie de conférence via le centre d’administration Skype Entreprise Online :

![Propriétés des options générales du centre d’administration Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Propriétés des options générales du centre d’administration Lync")

Vous pouvez également gérer les paramètres de stratégie d’accès externe via le centre d’administration Skype Entreprise Online :

![Options de communication externe du centre d’administration](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "Options de communication externe du centre d’administration")

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

