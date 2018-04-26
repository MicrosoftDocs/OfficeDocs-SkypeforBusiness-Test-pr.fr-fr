---
title: Restauration d’un serveur membre Enterprise Edition
TOCTitle: Restauration d’un serveur membre Enterprise Edition
ms:assetid: d960b19c-2104-4719-b736-0d940f254d42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh202191(v=OCS.15)
ms:contentKeyID: 53095542
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Restauration d’un serveur membre Enterprise Edition

 

_**Dernière rubrique modifiée :** 2013-02-18_

Si un serveur exécutant l’un des rôles serveur suivants est défaillant, appliquez la procédure indiquée dans cette section pour le restaurer. Si plusieurs serveurs subissent une défaillance indépendamment, appliquez la procédure pour chacun d’eux.

  - Serveur frontal

  - Serveur de médiation

  - Directeur

  - Serveur de conversation permanente

  - Serveur Edge

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous recommandons de faire une image du système avant de démarrer la restauration. Vous pourrez utiliser cette copie comme point de restauration au cas où un problème surviendrait lors de la restauration. Il peut être préférable de créer cette copie instantanée après avoir installé le système d’exploitation et SQL Server et après avoir restauré ou réinscrit les certificats.</td>
</tr>
</tbody>
</table>


## Pour restaurer un serveur membre

1.  Démarrez avec un nouveau serveur ayant le même nom de domaine complet que le serveur ayant subi une défaillance, installez le système d’exploitation, puis restaurez ou réinscrivez les certificats.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Suivez les procédures de déploiement de serveur de votre organisation pour effectuer cette étape.</td>
    </tr>
    </tbody>
    </table>


2.  À partir d’un compte d’utilisateur membre du groupe RTCUniversalServerAdmins, ouvrez une session sur le serveur que vous restaurez.

3.  Accédez au dossier ou support d’installation de Lync Server, puis démarrez l’Assistant Déploiement de Lync Server situé à l’emplacement \\setup\\amd64\\Setup.exe.

4.  Suivez l’Assistant Déploiement pour effectuer ce qui suit :
    
    1.  Exécutez l’**Étape 1 : Installer le magasin de configurations local** pour installer les fichiers de configuration locaux.
    
    2.  Exécutez l’**Étape 2 : Installer ou supprimer des composants Lync Server** pour installer les rôles serveur Lync Server.
    
    3.  Exécuter l’**Étape 3 : Demander, installer ou assigner les certificats** pour assigner les certificats.
    
    4.  Exécutez l’**Étape 4 : Démarrer les services** pour démarrer les services sur le serveur.
    
    Pour plus d’informations sur l’exécution de l’Assistant Déploiement, voir la documentation de déploiement relative au rôle serveur que vous restaurez.

