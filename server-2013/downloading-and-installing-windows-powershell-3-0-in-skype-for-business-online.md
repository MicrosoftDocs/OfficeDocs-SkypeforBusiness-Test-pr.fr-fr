---
title: 'Lync Online : téléchargement et installation de Windows PowerShell 3.0'
TOCTitle: Téléchargement et installation de Windows PowerShell 3.0
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56269575
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Téléchargement et installation de Windows PowerShell 3.0 dans Lync Online

 

_**Dernière rubrique modifiée :** 2016-12-08_

Si vous utilisez Windows Server 2012, Windows Server 2012 R2, Windows 8 ou Windows 8.1, vous devez déjà disposer de Windows PowerShell 3.0. En effet, cette application est préinstallée avec ces systèmes d'exploitation.

Si vous utilisez Windows 7 ou Windows Server 2008 R2, il est également possible que vous exécutiez Windows PowerShell 3.0. Il peut toutefois s’agir de la version 2.0 (version incluse à l’origine sur ces systèmes d’exploitation). Pour déterminer la version de Windows PowerShell que vous utilisez, procédez comme suit sur votre ordinateur Windows 7 ou Windows Server 2008 R2 :

1.  Cliquez sur **Démarrer**, Tous les programmes, **Accessoires**, **Windows PowerShell**, puis sur **Windows PowerShell**.

2.  Dans la console Windows PowerShell, tapez la commande suivante, puis appuyez sur Entrée :
    
        Get-Host | Select-Object Version

3.  Des informations semblables à ce qui suit doivent être affichées dans la fenêtre de la console :
    
        Version
        -------
        3.0

Si le numéro de version 3.0 est retourné, vous disposez de Windows PowerShell 3.0. Sinon, vous devez installer Windows PowerShell 3.0. Vous pouvez télécharger Windows Management Framework 3.o, qui inclut Windows PowerShell 3.0, à partir du [Centre de téléchargement Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=34595).

Une fois que vous avez vérifié que Windows PowerShell 3.0 est installé, vous devez vérifier que Windows PowerShell a été configuré pour exécuter des scripts à distance. Pour ce faire, démarrez Windows PowerShell en tant qu'administrateur. Sur Windows 7, Windows Server 2008 R2, Windows Server 2012 ou Windows Server 2012 R2, procédez comme suit :

1.  Cliquez sur **Démarrer**, **Tous les programmes**, **Accessoires**, puis sur **Windows PowerShell**, cliquez avec le bouton droit sur **Windows PowerShell**, puis cliquez sur **Exécuter en tant qu'administrateur**.

2.  Si la boîte de dialogue **Contrôle de compte d'utilisateur** apparaît, cliquez sur **Oui** pour confirmer que vous voulez exécuter Windows PowerShell avec des informations d'identification administrateur.

Si vous utilisez Windows 8, procédez comme suit :

1.  Accédez à la barre des icônes, cliquez sur **Rechercher**, puis cliquez avec le bouton droit sur **Windows PowerShell**. Vous pouvez accéder rapidement à la barre des icônes sur un ordinateur Windows 8 (écran tactile ou normal) en maintenant la touche Windows enfoncée, puis en appuyant sur C.

2.  Dans la barre d'outils au bas de l'écran, cliquez sur **Exécuter en tant qu'administrateur**.

3.  Si la boîte de dialogue **Contrôle de compte d'utilisateur** apparaît, cliquez sur **Oui** pour confirmer que vous voulez exécuter Windows PowerShell avec des informations d'identification administrateur.

Une fois que Windows PowerShell est exécuté, vous devez modifier la stratégie d'exécution pour autoriser l'exécution des scripts à distance. Dans la console Windows PowerShell, tapez la commande suivante, puis appuyez sur Entrée :

    Set-ExecutionPolicy RemoteSigned -Force

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous exécutez la commande précédente, vous pouvez recevoir le message d'erreur suivant :<br />
Set-ExecutionPolicy : l'accès à la clé de Registre « HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell » est refusé.<br />
Ce message d'erreur s'affiche généralement si vous n'exécutez pas Windows PowerShell avec des informations d'identification administrateur. Fermez votre session Windows PowerShell et démarrez une nouvelle session en tant qu'administrateur.</td>
</tr>
</tbody>
</table>


Pour vérifier que la stratégie d'exécution a été correctement configurée, tapez ce qui suit à l'invite de commandes Windows PowerShell, puis appuyez sur Entrée :

    Get-ExecutionPolicy

Si vous obtenez la valeur suivante, tout est correctement configuré :

    RemoteSigned

Si vous n'exécutez pas Windows PowerShell actuellement, vous devez également télécharger et installer Windows Management Framework 3.0 à partir du Centre de téléchargement Microsoft. Ce package d'installation inclut Windows PowerShell 3.0 et Windows Remote Management (WinRM) 3.0. Il peut être requis si vous exécutez Windows 7 mais que vous n'avez pas effectué de mise à jour vers Windows PowerShell 3.0. Si vous exécutez Windows Server 2012, Windows Server 2012 R2, Windows 8 ou Windows 8.1, vous n'avez pas besoin d'installer Windows PowerShell 3.0. Windows PowerShell 3.0 est préinstallé sur ces systèmes d'exploitation.

Avant d'installer Windows Management Framework 3.0 :

  - Vérifiez que vous avez téléchargé la version correcte du package d'installation. Si vous exécutez la version 64 bits de Windows 7, téléchargez le fichier Windows6.1-KB2506143-x64.msu. Si vous exécutez la version 32 bits de Windows 7, téléchargez le fichier Windows6.1-KB2506143-x86.msu.

  - Si vous exécutez Windows 7 sur votre ordinateur, vérifiez que vous avez installé Windows 7 Service Pack 1.

Si vous ne savez pas quelle version de Windows vous utilisez ou si vous n'êtes pas certain d'avoir installé Windows 7 Service Pack 1, cliquez sur **Démarrer**, cliquez avec le bouton droit sur **Ordinateur**, puis cliquez sur **Propriétés**. Les informations suivantes apparaîtront dans la boîte de dialogue Système :

![Boîte de dialogue système montrant les paramètres](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "Boîte de dialogue système montrant les paramètres")

Pour installer Windows Management Framework 3.0, procédez comme suit :

1.  Double-cliquez sur le fichier d'installation .MSU ( **Windows6.1-KB2506143-x64.msu** ou **Windows6.1-KB2506143-x86.msu**).

2.  Dans l'Assistant Télécharger et installer les mises à jour, sur la page **Veuillez lire les termes du contrat de la licence (1 sur 1)**, cliquez sur **J'accepte**.

3.  Une fois l'installation terminée, cliquez sur **Redémarrer maintenant** pour redémarrer votre ordinateur.

Une fois l'ordinateur redémarré, vérifiez que Windows PowerShell peut démarrer et que l'application peut être exécutée avec des informations d'identification administrateur. Pour ce faire :

1.  Cliquez sur **Démarrer**, **Tous les programmes**, **Accessoires**, puis sur **Windows PowerShell**, cliquez avec le bouton droit sur **Windows PowerShell**, puis cliquez sur **Exécuter en tant qu'administrateur**.

2.  Si la boîte de dialogue Contrôle de compte d'utilisateur apparaît, cliquez sur **Oui** pour confirmer que vous voulez exécuter Windows PowerShell avec des informations d'identification administrateur.

Lorsque la console Windows PowerShell apparaît, vous devez vérifier que le service WinRM est exécuté et a été correctement configuré. Pour vérifier que le service est exécuté, tapez la commande suivante à l'invite de commandes Windows PowerShell, puis appuyez sur Entrée :

    Get-Service winrm

Des informations sur le service WinRM sont affichées à l'écran :

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

Si le service n'est pas dans l'état « En cours d'exécution », démarrez le service WinRM en tapant la commande suivante, puis en appuyant sur Entrée :

    Start-Service winrm

Une fois le service démarré, exécutez la commande suivante pour vérifier que WinRM utilise l'authentification de base :

    winrm set winrm/config/client/auth '@{Basic="True"}'

Des informations semblables à ce qui suit sont affichées à l'écran :

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

Si l'authentification de base est définie sur true, vous pouvez utiliser Windows PowerShell pour vous connecter à Skype Entreprise Online.

