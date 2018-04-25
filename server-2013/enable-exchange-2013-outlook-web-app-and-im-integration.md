---
title: Activation d’Exchange 2013 Outlook Web App et intégration à la messagerie instantanée
TOCTitle: Activation d’Exchange 2013 Outlook Web App et intégration à la messagerie instantanée
ms:assetid: 44d08cf0-b17d-46e1-a4f0-fcc2fe96a958
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ204857(v=OCS.15)
ms:contentKeyID: 49297056
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Activation d’Exchange 2013 Outlook Web App et intégration à la messagerie instantanée

 

_**Dernière rubrique modifiée :** 2012-10-19_

Pour activer l’intégration de la messagerie instantanée et d’Exchange 2013 Outlook Web Access (OWA) à Lync Server 2013, vous devez ajouter le serveur d’accès au client Exchange 2013 à la topologie de Lync Server 2013 sous forme de serveur d’applications approuvées.

## Pour créer un pool d’applications approuvées

1.  Démarrez Lync Server 2013 Management Shell.

2.  Exécutez l’applet de commande suivante :
    
        Get-CsSite
    
    Celle-ci renvoie la valeur siteID correspondant à la valeur siteName dans laquelle vous créez le pool. Pour plus d’informations, reportez-vous à [Get-CsSite](get-cssite.md) dans la documentation de Lync Server 2013 Management Shell.

3.  Exécutez l’applet de commande suivante :
    
        New-CsTrustedApplicationPool -Identity <E14 CAS FQDN> -ThrottleAsServer $true -TreatAsAuthenticated $true -ComputerFQDN <E14 CAS FQDN> -Site <Site> -Registrar <Pool FQDN in the site> -RequiresReplication $false
    
    Pour plus d’informations, reportez-vous à [New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md) dans la documentation de Lync Server 2013 Management Shell.
    
    Le nom de domaine complet du serveur Exchange Server doit être configuré en tant que nom d’objet du certificat Exchange OWA ou en tant qu’autre nom de l’objet.
    
    Dans Exchange OWA, assurez-vous que le nom de domaine complet du pool est également approuvé.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg425917.important(OCS.15).gif" title="important" alt="important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si votre serveur d’accès au client n’est <em>pas</em> colocalisé sur le serveur qui exécute la messagerie unifiée Exchange 2013, ignorez les étapes restantes de cette procédure et effectuez la procédure « Créer une application approuvée pour le serveur d’accès au client Exchange 2013 » décrite dans la suite de cette rubrique. Si votre serveur d’accès au client est colocalisé sur le serveur qui exécute la messagerie unifiée Exchange 2013, effectuez les étapes de cette procédure et ignorez la procédure « Créer une application approuvée pour le serveur d’accès au client Exchange 2013 » décrite dans la suite de cette rubrique.</td>
    </tr>
    </tbody>
    </table>


4.  Exécutez **Enable-CsTopology** .

5.  Ouvrez le générateur de topologie et téléchargez la topologie existante.

6.  Dans le volet gauche, développez l’arborescence jusqu’à ce que vous atteigniez **Serveurs d’applications approuvées** .

7.  Développez le nœud **Serveurs d’applications approuvés** .

8.  Vous devriez voir maintenant le serveur d’accès au client Exchange 2013 répertorié en tant que serveur d’applications approuvées.

## Pour créer une application approuvée pour le serveur d’accès au client Exchange 2013

1.  Démarrez Lync Server 2013 Management Shell.

2.  Si votre serveur d’accès au client n’est *pas* colocalisé sur le serveur qui exécute la messagerie unifiée Exchange 2013, exécutez l’applet de commande suivante :
    
        New-CsTrustedApplication -ApplicationId <AppID String> -TrustedApplicationPoolFqdn <E14 CAS FQDN> -Port <available port number>
    
    Pour plus d’informations, reportez-vous à la rubrique [New-CsTrustedApplication](new-cstrustedapplication.md) dans la documentation de Lync Server 2013 Management Shell.

3.  Exécutez **Enable-CsTopology** .

4.  Dans le générateur de topologie, dans le volet gauche, développez l’arborescence jusqu’à ce que vous atteigniez **Serveurs d’applications approuvées** .

5.  Développez le nœud **Serveurs d’applications approuvés** .

6.  Vous devriez voir maintenant le serveur d’accès au client Exchange 2013 répertorié en tant que serveur d’applications approuvées.

