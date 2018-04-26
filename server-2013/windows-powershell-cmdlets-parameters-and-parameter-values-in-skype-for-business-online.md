---
title: Applets de commande Windows PowerShell, paramètres et valeurs de paramètre
TOCTitle: Applets de commande Windows PowerShell, paramètres et valeurs de paramètre
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56269556
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applets de commande Windows PowerShell, paramètres et valeurs de paramètre

 

_**Dernière rubrique modifiée :** 2015-06-22_

Si vous savez utiliser la fenêtre de commandes accessible dans toutes les versions de Windows (ou si vous êtes familiarisé avec MS-DOS), vous aurez déjà une base importante pour apprendre à utiliser Windows PowerShell. Dans la fenêtre de commandes, vous tapez une commande, puis vous appuyez sur Entrée. En réponse, l’ordinateur exécute une commande ou un fichier exécutable. Par exemple, pour retourner des informations sur les fichiers et dossiers du répertoire actuel, vous devez taper la commande suivante dans une invite de commandes, puis appuyer sur Entrée :

    dir

Vous recevez alors des informations sur les fichiers et dossiers du répertoire actuel :

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/13/2013  02:53 PM                 117   pldok.log
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/21/2013  03:37 PM            207   setup.doc
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Cet exemple montre le résultat obtenu lorsque vous tapez seulement le nom d’une commande ou d’un fichier exécutable. Toutefois, de nombreuses commandes exécutées à partir de la fenêtre de commandes acceptent également des *arguments*. Les arguments sont des informations supplémentaires transmises à la commande qui permettent de modifier le comportement de celle-ci. Par exemple, si vous voulez seulement afficher le nom des fichiers et dossiers du répertoire actuel (sans autre information telle que la tailles des fichiers et dossiers, ou les date et heure de création des fichiers et dossiers), vous devez ajouter l’argument **/b** lors de l‘exécution de la commande dir :

    dir /b

Lorsque vous incluez l’argument **/b**, la commande **dir** ne retourne que le nom des dossiers et fichiers inclus dans le répertoire actuel :

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

Dans la commande précédente, l’argument **/b** est la seule information requise pour limiter les données retournées aux seuls noms des fichiers et dossiers. C’est souvent le cas avec les commandes de ligne de commande : la simple présence d’un argument suffit à changer le comportement de la commande. Dans le cas présent, vous incluez l’argument **/b** pour masquer les informations supplémentaires ou vous excluez l’argument **/b** pour afficher les informations supplémentaires. En d’autres occasions, vous devez toutefois spécifier une *valeur d’argument*. Une valeur d’argument est une autre information transmise à l’argument lui-même. Par exemple, l’argument **/o** vous permet de spécifier les modalités de tri des données retournées par la commande dir. Vous pouvez notamment utiliser la valeur d’argument **e** pour effectuer un tri selon l’extension des fichiers ou la valeur d’argument **s** pour effectuer un tri selon la taille des fichiers. Par exemple, la commande suivante trie les données retournées selon l’extension des fichiers. Notez comment la valeur d’argument **e** est incluse immédiatement après l’argument **/o** :

    dir /oe

Pour notre exemple de dossier, les données retournées ressemblent à ce qui suit, les fichiers étant triés dans l’ordre alphabétique des extensions de fichier :

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/21/2013  03:37 PM            207   setup.doc
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/13/2013  02:53 PM                 117   pldok.log
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Soit, pour vous permettre de repérer plus précisément ce dont nous parlons :

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

Bien que Windows PowerShell utilise une autre terminologie, l’approche de base relative à l’utilisation de Windows PowerShell est semblable à l’utilisation de la fenêtre de commandes : vous tapez des commandes, vous incluez des arguments et des valeurs d’argument si nécessaire, puis vous appuyez sur Entrée pour exécuter ces commandes. Comme nous l’avons souligné, Windows PowerShell utilise une terminologie différente de celle de l’interface de commande. Dans Windows PowerShell, les commandes que vous exécutez sont appelées *applets de commande*. De même, les arguments transmis à une applet de commande sont appelés *paramètres*, tandis que les valeurs transmises à un paramètre sont appelées *valeurs de paramètre*.

Les définitions précédentes sont quelque peu simplifiées. Pour l’essentiel, les applets de commande sont des mini-applications pouvant être exécutées à partir de l’environnement Windows PowerShell uniquement. Vous pouvez également exécuter d’autres commandes et applications à partir de Windows PowerShell (notamment la plupart des commandes et applications exécutables à partir d’une fenêtre de commandes). Par exemple, si vous voulez démarrer le Bloc-notes à partir de Windows PowerShell, vous devez taper la commande suivante, puis appuyer sur Entrée :

    notepad.exe

Pour ce qui est des opérations de gestion de Skype Entreprise Online, la plupart des administrateurs utilisent des applets de commande Windows PowerShell pour effectuer des tâches d’administration. Pour le moment, quelques autres types de commandes ou applications permettent de gérer Skype Entreprise Online. Les applets de commande Skype Entreprise Online peuvent être utilisées sans arguments supplémentaires (comme indiqué précédemment, les arguments sont appelés paramètres dans Windows PowerShell). Par exemple, la commande suivante appelle l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md) sans paramètre supplémentaire. Utilisée seule, la commande retourne des informations sur tous vos utilisateurs Skype Entreprise Online :

    Get-CsOnlineUser

La plupart des applets de commande Skype Entreprise Online acceptent également des paramètres (et valeurs de paramètre). Examinez la commande suivante :

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Cette commande est constituée de trois éléments :

  - l’applet de commande **Get-CsOnlineUser**.

  - le paramètre Identity. Notez que dans Windows PowerShell, les paramètres sont toujours précédés d’un tiret (-). Ainsi, pour la même applet de commande, le paramètre UnassignedUser serait indiqué à l’aide de la syntaxe suivante :
    
        -UnassignedUser
    
    Il est utile de savoir ceci, car les paramètres doivent être précédés dֹ’un tiret d’une part, et cette syntaxe diffère de celle de la fenêtre de commandes (dans laquelle les arguments sont précédés d’une barre oblique (/)) d’autre part :
    
    ``` 
    /b
    ```

  - la valeur de paramètre **kenmyer@litwareinc.com**.

Cette commande retourne des informations sur un utilisateur spécifique : l’utilisateur ayant l’identité kenmyer@litwareinc.com.

## Voir aussi

#### Concepts

[Présentation de Windows PowerShell et Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

