---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398647(v=OCS.15)
ms:contentKeyID: 49297881
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les certificats Lync Server utilisés sur l’ordinateur local. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsCertificateConfiguration [-Report <String>]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 retourne des informations sur les certificats actuellement utilisés (sur l’ordinateur local) par Lync Server.

    Test-CsCertificateConfiguration

## EXEMPLE 2

La commande de l’exemple 2 est une variante de la commande de l’exemple 1. Dans ce cas, toutefois, le paramètre Report permet de définir le chemin (C:\\Logs\\Certificates.xml) du fichier de sortie généré lorsque vous exécutez l’applet de commande **Test-CsCertificateConfiguration**.

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## Description détaillée

L’applet de commande **Test-CsCertificateConfiguration** est un exemple de « transaction synthétique ». Les transactions synthétiques utilisées dans Lync Server permettent de vérifier que les utilisateurs peuvent exécuter les tâches courantes, notamment se connecter au système, échanger des messages instantanés ou appeler un numéro de téléphone sur le réseau téléphonique commuté (PSTN). Ces tests peuvent être réalisés manuellement par un administrateur ou exécutés automatiquement par une application telle que Microsoft System Center Operations Manager (anciennement Microsoft Operations Manager).

L’applet de commande **Test-CsCertificateConfiguration** retourne des informations sur les certificats utilisés par Lync Server. L’applet de commande **Test-CsCertificateConfiguration** est principalement destinée à être utilisée par l’Assistant Certificat. Il est recommandé aux administrateurs d’utiliser l’applet de commande **Get-CsCertificate** pour extraire les informations de certificat.

Personnes autorisées à exécuter cette applet de commande : Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\Certificates.html&quot;. Si le fichier existe déjà, il sera remplacé lors de l’exécution de l’applet de commande.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Test-CsCertificateConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Test-CsCertificateConfiguration** renvoie des instances de l’objet Microsoft.Rtc.Management.Deployment,CertificateExists.

## Voir aussi

#### Autres ressources

[Get-CsCertificate](get-cscertificate.md)

