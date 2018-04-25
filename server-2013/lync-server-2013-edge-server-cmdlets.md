---
title: Applets de commande de serveur Edge
TOCTitle: Applets de commande de serveur Edge
ms:assetid: 1a5427f4-a0d1-4652-8135-91333158ffc8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg415635(v=OCS.15)
ms:contentKeyID: 49296405
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applets de commande de serveur Edge

 

_**Dernière rubrique modifiée :** 2016-12-08_

Les serveurs Edge vous permettent d’étendre les fonctionnalités de Microsoft Lync Server 2013 aux personnes qui ne sont pas connectées à votre réseau interne. Par exemple, si des utilisateurs distants ou authentifiés ouvrent une session Lync Server 2013 sur Internet plutôt que sur votre réseau interne, vous devez configurer un serveur Edge qui exécute le service Edge d’accès de Lync Server. Par ailleurs, les serveurs Edge sont indispensables si vous voulez vous fédérer à une autre organisation ou donner à vos utilisateurs le droit de communiquer avec des personnes disposant de comptes de messagerie instantanée publics comme en proposent Yahoo\!, AOL ou MSN.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Depuis le 1er septembre 2012, la licence Microsoft Lync « PIC USL » (Public IM Connectivity User Subscription License) n’est plus disponible et ne peut pas être achetée ou renouvelée. Les clients disposant de licences actives pourront continuer à assurer la fédération avec Yahoo! Messenger jusqu’à la date d’arrêt du service. Une date de fin de vie de juin 2014 a été annoncée pour AOL et Yahoo! Pour plus d’informations, voir <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Prise en charge de la connectivité PIC (Public IM Connectivity) dans Lync Server 2013</a>.</p></li>
<li><p>La licence PIC USL est une licence d’abonnement mensuel par utilisateur requise pour la fédération de Lync Server ou Office Communications Server avec Yahoo! Messenger. La capacité de Microsoft à fournir ce service est liée au soutien de Yahoo!, dont le contrat sous-jacent arrive à expiration.</p></li>
<li><p>Lync est un outil puissant permettant aux organisations et aux individus du monde entier de rester connectés. La fédération avec Windows Live Messenger ne nécessite aucune licence utilisateur/appareil supplémentaire en plus de la licence d’accès client (CAL) standard Lync. La fédération avec Skype sera prochainement ajoutée à cette liste, ce qui permettra aux utilisateurs Lync d’entrer en contact avec des centaines de millions de personnes à l’aide des fonctionnalités vocales et de messagerie instantanée.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Applets de commande de serveur Edge

La liste suivante indique les applets de commande qui sont directement associées à la gestion des serveurs Edge :

**Serveur Edge**

  -   
    [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  -   
    [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  -   
    [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  -   
    [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  -   
    [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  -   
    [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  -   
    [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  -   
    [Set-CsEdgeServer](set-csedgeserver.md)

## Voir aussi

#### Autres ressources

[Blog PowerShell Lync Server](http://go.microsoft.com/fwlink/?linkid=203150)

