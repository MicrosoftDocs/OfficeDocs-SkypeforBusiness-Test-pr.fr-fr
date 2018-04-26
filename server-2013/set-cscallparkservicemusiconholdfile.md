---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412836(v=OCS.15)
ms:contentKeyID: 49298524
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie le fichier audio qui sera lu aux appelants en attente dans un appel parqué. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple définit le fichier SoothingMusic.wma et le désigne comme le fichier audio qui sera lu aux personnes dont les appels ont été parqués. La première ligne de cet exemple est un appel à l’applet de commande **Get-Content**. Cette applet de commande lit le contenu d’un fichier et l’affecte, dans le cas présent, à la variable $a. Une valeur 0 est transmise au paramètre ReadCount afin que l’applet de commande **Get-Content** puisse lire immédiatement le fichier tout entier (plutôt que d’essayer de le lire ligne après ligne, ce qui n’est pas possible dans le cas d’un fichier audio). Le paramètre Encoding (codage) est défini avec la valeur « byte » (octet). Ceci indique à l’applet de commande **Get-Content** que le contenu que nous cherchons à lire dans la variable $a est un tableau d’octets et non le fichier audio au format .wma.

La ligne 2 de cet exemple désigne le site auquel le fichier audio est réellement affecté. Il reste à appeler l’applet de commande **Set-CsCallParkServiceMusicOnHoldFile** et à préciser l’ID du service dans lequel le service de parcage d’appel est exécuté. Le contenu du fichier audio lu dans la variable $a est ensuite transmis au paramètre Content (contenu). N’oubliez pas que ce contenu doit être affiché en octets.

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## Description détaillée

Le parcage d’appel est un service qui permet à un utilisateur de « parquer » un appel téléphonique entrant. Le parcage d’un appel a pour effet de transférer ce dernier dans une plage définie et de le mettre immédiatement en attente. En fonction des paramètres de configuration spécifiés pour le service de parcage d’appel, une attente musicale peut être proposée à l’appelant pendant le parcage de l’appel. Cette applet de commande vous permet de modifier le fichier audio (attente musicale) qui est lu à un appelant mis en garde pendant qu’il patiente.

L’attente musicale est jouée uniquement si la propriété EnableMusicOnHold du service de parcage d’appel a la valeur True. Vous pouvez vérifier cette propriété en appelant l’applet de commande **Get-CsCpsConfiguration**. Vous pouvez définir la propriété soit au moment de créer la configuration du parcage d’appel au moyen de l’applet de commande **New-CsCpsConfiguration**, soit une fois cette configuration créée en appelant l’applet de commande **Set-CsCpsConfiguration**. Par défaut, cette propriété a la valeur True.

Lync Server est fourni avec un fichier de service de parcage d’appel par défaut pour l’attente musicale. Le fichier par défaut sera utilisé si vous n’attribuez aucun fichier audio.

Les fichiers audio doivent adopter l’un des formats suivants : Windows Media Audio 9, 44 kHz, 16 bits, Mono, CBR (taux binaire constant) ou 32 Kbits/s.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsCallParkServiceMusicOnHoldFile** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

## Paramètres


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Content</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Contenu du fichier audio en octets.</p>
<p>Utilisez l’applet de commande <strong>Get-Content</strong> pour extraire le contenu du fichier audio sous forme d’octets. (Pour plus d’informations, consultez les exemples de cette rubrique.)</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>L’ID du service où réside le service de parcage d’appel (par exemple, ApplicationServer:pool0.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Byte\[\]. Accepte l’entrée redirigée d’un tableau d’octets contenant le fichier d’attente musicale.

## Types de retours

Cette applet de commande ne retourne aucune valeur.

## Voir aussi

#### Autres ressources

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

