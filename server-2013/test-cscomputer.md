---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398162(v=OCS.15)
ms:contentKeyID: 49296207
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**Dernière rubrique modifiée :** 2015-03-09_

L’applet de commande **Test-CsComputer** vérifie l’état des services Lync Server exécutés sur l’ordinateur local. L’applet de commande vérifie également que les groupes Active Directory Lync Server appropriés ont été ajoutés aux groupes locaux correspondants sur l’ordinateur et que les ports de pare-feu d’ordinateur nécessaires ont été ouverts. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsComputer [-Report <String>]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 vérifie l’état d’activation du service sur l’ordinateur local. Le paramètre Verbose est inclus dans la commande pour s’assurer que la réussite (ou l’échec) de l’opération est clairement indiquée à l’écran.

    Test-CsComputer -Verbose

## EXEMPLE 2

L’exemple 2 vérifie également l’état d’activation des services de l’ordinateur local. En outre, cette commande écrit des informations détaillées sur l’état d’activation dans le fichier C:\\Logs\\Computer.html. Ce journal est généré en ajoutant le paramètre Report, suivi du chemin d’accès complet au fichier journal dans lequel les informations doivent être enregistrées.

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## Description détaillée

L’applet de commande **Test-CsComputer** est un exemple de « transaction synthétique » de Lync Server. Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment pour se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

L’applet de commande **Test-CsComputer**, qui peut être exécutée uniquement sur l’ordinateur local, vérifie l’état de tous les services Lync Server sur cet ordinateur. L’applet de commande vérifie également si les ports de pare-feu appropriés ont été ouverts sur l’ordinateur et détermine si les groupes Active Directory créés lors de l’installation de Lync Server ont été ajoutés aux groupes locaux correspondants. Par exemple, **Test-CsComputer** vérifie que le groupe Active Directory RTCUniversalUserAdmins a été ajouté au groupe Administrateurs local.

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
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report « C:\Logs\Computer.html ». Si le fichier existe déjà, il sera remplacé lors de l’exécution de l’applet de commande.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsComputer** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsComputer** retourne une instance de l’objet Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Voir aussi

#### Autres ressources

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

