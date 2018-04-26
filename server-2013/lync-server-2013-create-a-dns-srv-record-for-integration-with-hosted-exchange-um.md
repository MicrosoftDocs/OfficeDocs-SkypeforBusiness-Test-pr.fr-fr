---
title: 'Lync Server 2013 : Création d’un enregistrement SRV DNS pour l’intégrer à la messagerie unifiée Exchange hébergée'
TOCTitle: Création d’un enregistrement SRV DNS pour l’intégrer à la messagerie unifiée Exchange hébergée
ms:assetid: 8ea590ae-58ea-4ca5-9853-e0708b3ea760
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh500728(v=OCS.15)
ms:contentKeyID: 49298036
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Création d’un enregistrement SRV DNS pour l’intégrer à la messagerie unifiée Exchange hébergée

 

_**Dernière rubrique modifiée :** 2016-12-08_

Cette rubrique décrit comment configurer l’enregistrement SRV DNS (Domain Name System) requis pour qu’un  serveur EdgeLync Server 2013 effectue un routage vers un service Exchange hébergé tel que Microsoft Exchange Online.

## Pour créer un enregistrement SRV DNS pour le service Exchange hébergé

1.  Ouvrez une session sur le serveur DNS externe en tant que membre du groupe DnsAdmins.

2.  Cliquez sur **Démarrer**, sur **Outils d’administration**, puis sur **DNS**.

3.  Dans l’arborescence de la console pour votre domaine SIP, développez **Zones de recherche directes** et sélectionnez le domaine SIP dans lequel Lync Server 2013 sera installé.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous devez créer l’enregistrement SRV DNS dans le domaine SIP dans lequel Lync Server est ou sera installé. Lorsque vous créez l’enregistrement SRV, le nom de domaine complet mentionné dans le champ Hôte offrant ce service doit être le nom de domaine externe du pool Edge. Par exemple, si le nom de domaine complet externe de votre pool Edge est edge01.contoso.net, entrez cette valeur. Il doit également être dans le même domaine que l’enregistrement d’hôte (A) DNS.</td>
    </tr>
    </tbody>
    </table>


4.  Cliquez avec le bouton droit sur le domaine sélectionné, puis cliquez sur **Nouveaux enregistrements**.

5.  Dans **Type d’enregistrement de ressource**, cliquez sur **Emplacement du service (SRV)**, puis sur **Créer un enregistrement**.

6.  Dans **Nouvel enregistrement de ressource**, cliquez sur **Service**, puis tapez **\_sipfederationtls** .

7.  Cliquez sur **Protocole**, puis saisissez **\_tcp**.

8.  Cliquez sur **Numéro de port**, puis saisissez **5061**.

9.  Cliquez sur **Hôte offrant ce service**, puis saisissez le nom de domaine complet (FQDN) du Lync Server 2013 pool de serveurs Edge permettant aux clients externes approuvés d’accéder à votre système Lync Server 2013.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le domaine doit également être configuré comme domaine accepté et faisant autorité dans vos paramètres Exchange Online. Pour plus d’informations, reportez-vous à « Créer des domaines acceptés » à l’adresse <a href="http://go.microsoft.com/fwlink/p/?linkid=229762">http://go.microsoft.com/fwlink/p/?linkId=229762</a>.</td>
    </tr>
    </tbody>
    </table>


10. Cliquez sur **OK**, puis sur **Terminé**.

## Pour vérifier que l’enregistrement SRV DNS a bien été créé

1.  Ouvrez une session sur un ordinateur client du domaine.

2.  Cliquez sur **Démarrer**, puis sur **Exécuter**.

3.  Dans la ligne de commande, exécutez la commande suivante :
    
        nslookup <FQDN Lync Edge Pool>

4.  Vérifiez que vous recevez une réponse résolue en adresse IP appropriée pour le nom de domaine complet.

## Voir aussi

#### Concepts

[Création des enregistrements DNS pour les serveurs proxy inverses dans Lync Server 2013](lync-server-2013-create-dns-records-for-reverse-proxy-servers.md)

