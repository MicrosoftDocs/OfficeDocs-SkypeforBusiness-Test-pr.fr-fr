---
title: Gestion de la messagerie unifiée Exchange et de la messagerie vocale hébergée
TOCTitle: Gestion de la messagerie unifiée Exchange et de la messagerie vocale hébergée
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56269621
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestion de la messagerie unifiée Exchange et de la messagerie vocale hébergée

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande suivantes permettent de gérer la messagerie unifiée Exchange et les stratégies de messagerie vocale hébergée :


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
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>Crée et gère les objets contact utilisés pour les services Standard automatique et Accès abonné, lorsque la messagerie unifiée Exchange est un service hébergé.</p>
<p>Skype Entreprise Online fonctionne avec la messagerie unifiée Exchange pour offrir plusieurs fonctionnalités vocales, dont le standard automatique et l’accès abonné. Le standard automatique permet de répondre aux appels et de les acheminer vers la personne correcte de façon automatique. L’accès abonné permet aux utilisateurs de se connecter à la messagerie unifiée Exchange et de récupérer les messages électroniques, les messages vocaux, les contacts et les informations de calendrier.</p>
<p>Lorsque la messagerie unifiée Exchange est fournie comme un service hébergé, les objets contact utilisés pour les services Standard automatique et Accès abonné doivent être créés à l’aide de Windows PowerShell. Ces objets sont créés et gérés à l’aide des applets de commande CsExUmContact.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>Gère les stratégies de messagerie vocale hébergée utilisées dans l’organisation. Celles-ci spécifient le mode d’acheminement des appels sans réponse vers le service de messagerie unifiée Exchange. Ces stratégies affectent uniquement les utilisateurs activés pour la messagerie vocale hébergée par la messagerie unifiée Exchange. Pour vérifier si un utilisateur est activé pour la messagerie vocale hébergée, exécutez une commande semblable à celle-ci à partir de l’invite Windows PowerShell :</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


Vous ne pouvez pas gérer les paramètres de la messagerie unifiée Exchange et les stratégies de messagerie vocale hébergée à l’aide du centre d’administration Skype Entreprise Online.

## Voir aussi

#### Concepts

[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)  
[Aide-mémoire : utilisation de Windows PowerShell pour effectuer les tâches de gestion courantes de Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

