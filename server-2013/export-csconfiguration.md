---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398627(v=OCS.15)
ms:contentKeyID: 49297850
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Exporte votre topologie, vos stratégies et paramètres de configuration Lync Server dans un fichier. Ce fichier peut ensuite être utilisé, entre autres, pour restaurer ces données dans le magasin central de gestion après une mise à niveau, une défaillance matérielle ou tout autre problème ayant entraîné une perte de données. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande affichée dans l’exemple 1 exporte les données Lync Server du magasin central de gestion dans le fichier C:\\Config.zip.

    Export-CsConfiguration -FileName "C:\Config.zip"

## Description détaillée

Les ordinateurs qui exécutent des services ou des rôles serveur Lync Server doivent disposer d’une copie de la topologie, des paramètres de configuration et des stratégies actuelles avant de pouvoir fonctionner dans le rôle qui leur a été attribué. Lync Server est responsable de la transmission de ces informations à chaque ordinateur qui en a besoin.

Les applets de commande **Export-CsConfiguration** et l’applet de commande **Import-CsConfiguration** servent à sauvegarder et à restaurer votre topologie, vos paramètres de configuration et vos stratégies Lync Server pendant une mise à niveau du magasin central de gestion. L’applet de commande **Export-CsConfiguration** vous permet d’exporter les données dans un fichier .ZIP. Vous pouvez ensuite utiliser l’applet de commande **Import-CsConfiguration** pour lire ce fichier .ZIP et restaurer la topologie, les paramètres de configuration et les stratégies dans le magasin central de gestion. Ensuite, les services de réplication de Lync Server dupliquent les informations restaurées sur les autres ordinateurs exécutant les services Lync Server.

La possibilité d’exporter et d’importer les données de configuration est également utilisée lors de la configuration initiale des ordinateurs situés dans votre réseau de périmètre (par exemple, les serveurs de périphérie). Lors de la configuration d’un ordinateur dans le réseau de périmètre, vous devez d’abord effectuer une réplication manuelle à l’aide des applets de commande CsConfiguration : vous devrez exporter les données de configuration au moyen de l’applet de commande **Export-CsConfiguration**, puis les copier dans le fichier .ZIP sur l’ordinateur du réseau de périmètre. Ensuite, vous pourrez utiliser l’applet de commande **Import-CsConfiguration** et le paramètre LocalStore pour importer les données. Cette opération ne nécessite qu’une seule exécution ; par la suite, la réplication s’effectuera automatiquement.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Export-CsConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Chemin d’accès au fichier .ZIP à créer lors de l’exécution de l’applet de commande <strong>Export-CsConfiguration</strong>. Par exemple : -FileName &quot;C:\Config.zip&quot;. Notez que vous devez inclure le paramètre FileName ou AsBytes, mais pas les deux, lorsque vous appelez <strong>Export-CsConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retourne les informations de topologie dans un tableau d’octets. Les données retournées doivent être ensuite stockées dans une variable pour que l’applet de commande <strong>Import-CsConfiguration</strong> puisse les utiliser. Vous ne pouvez pas utiliser AsBytes et FileName dans une même commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande. Pour définir le paramètre Force sur True, utilisez la syntaxe suivante :</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données de configuration de l’ordinateur local et non du magasin central de gestion.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Export-CsConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

Si l’applet de commande **Export-CsConfiguration** est appelée avec le paramètre AsBytes, elle retourne les informations de configuration sous la forme d’un tableau d’octets.

## Voir aussi

#### Autres ressources

[Import-CsConfiguration](import-csconfiguration.md)

