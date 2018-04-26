---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398800(v=OCS.15)
ms:contentKeyID: 49298322
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Importe votre topologie, vos stratégies et vos paramètres de configuration Lync Server dans le magasin central de gestion ou sur l’ordinateur local. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande indiquée dans l’exemple 1 importe la topologie, les stratégies et les paramètres de configuration actuels à partir d’un fichier C:\\Config.zip vers le magasin central de gestion.

    Import-CsConfiguration -FileName "C:\Config.zip"

## EXEMPLE 2

L’exemple 2 montre comment les données peuvent être initialement répliquées sur un ordinateur situé dans le réseau de périmètre. Dans cet exemple, les données de configuration sont exportées dans un fichier Config.zip. Ce fichier est ensuite copié dans le dossier C:\\ de l’ordinateur situé dans le réseau de périmètre. L’applet de commande Import-CsConfiguration permet ensuite d’importer ces données. Le paramètre LocalStore entraîne l’importation des données sur l’ordinateur local au lieu du magasin central de gestion.

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## EXEMPLE 3

Les deux commandes dévoilées dans l’exemple 3 exportent la topologie, les stratégies et les paramètres de configuration actuels, puis importent ces données sur l’ordinateur local sans recourir à un fichier .ZIP. Pour ce faire, la première commande utilise l’applet de commande **Export-CsConfiguration** et le paramètre AsBytes pour exporter la topologie, les paramètres de configuration et les stratégies actuels sous la forme d’un tableau d’octets stocké dans une variable $x. Dans la deuxième commande, l’applet de commande **Import-CsConfiguration** et le paramètre ByteInput servent à importer les informations stockées dans la variable  $x. L’utilisation du paramètre LocalStore permet d’importer les données sur l’ordinateur local au lieu du magasin central de gestion. Résultat : les données sont copiées du magasin central de gestion vers l’ordinateur local.

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## Description détaillée

Les ordinateurs qui exécutent des services ou des rôles serveur Lync Server doivent disposer entre autres d’une copie de la topologie, des stratégies et des paramètres de configuration actuels avant de pouvoir assumer le rôle qui leur a été attribué. Lync Server est responsable de la transmission de ces informations à chaque ordinateur qui en a besoin.

Les applets de commande Import-CsConfiguration et Export-CsConfiguration servent à sauvegarder et à restaurer votre topologie, vos stratégies et vos paramètres de configuration Lync Server pendant une mise à niveau du magasin central de gestion. L’applet de commande **Export-CsConfiguration** vous permet d’exporter les données dans un fichier .ZIP. Vous pouvez ensuite utiliser l’applet de commande **Import-CsConfiguration** pour lire ce fichier .ZIP et restaurer la topologie, les stratégies et les paramètres dans le magasin central de gestion. Ensuite, les services de réplication de Lync Server répliquent les informations restaurées sur les ordinateurs exécutant des services.

La possibilité d’exporter et d’importer les données de configuration est également utilisée lors de la configuration initiale des ordinateurs situés dans votre réseau de périmètre (par exemple, un serveur Edge). Lors de la configuration d’un ordinateur situé dans le réseau de périmètre, vous devez d’abord procéder à une réplication manuelle à l’aide des applets de commande CsConfiguration : vous devrez exporter les données de configuration au moyen de l’applet de commande **Export-CsConfiguration**, puis les copier dans le fichier .ZIP sur l’ordinateur du réseau de périmètre. Ensuite, vous pourrez utiliser l’applet de commande **Import-CsConfiguration** et le paramètre LocalStore pour importer les données. Cette opération ne nécessite qu’une seule exécution ; par la suite, la réplication s’effectuera automatiquement.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Import-CsConfiguration** : RTCUniversalServerAdmins. Pour pouvoir exécuter cette applet de commande, vous devez non seulement appartenir au groupe RTCUniversalServerAdmins, mais vous devez également être un administrateur local ou bénéficier localement des autorisations nécessaires pour la réplication de configurations. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Lit les informations de topologie dans un tableau d’octets stocké dans une variable. Ce tableau d’octets est créé par l’utilisation du paramètre ByteInput lors de l’appel de l’applet de commande <strong>Export-CsConfiguration</strong>.</p>
<p>Vous ne pouvez pas utiliser les paramètres ByteInput et FileName dans une même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Chemin d’accès au fichier .ZIP créé par l’applet de commande Export-CsConfiguration. Par exemple : -FileName &quot;C:\Config.zip&quot;. Notez que vous devez inclure soit le paramètre FileName, soit le paramètre ByteInput, mais pas les deux, lors de l’appel de l’applet de commande <strong>Import-CsConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ignore toutes les invites susceptibles d’apparaître lors de l’exécution de la commande en cas de survenue d’une erreur récupérable. Pour définir le paramètre Force sur True, utilisez la syntaxe suivante :</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Copie les données de configuration sur l’ordinateur local et non sur le magasin central de gestion.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Import-CsConfiguration** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **Import-CsConfiguration** ne retourne pas d’objets ni de valeurs.

## Voir aussi

#### Autres ressources

[Export-CsConfiguration](export-csconfiguration.md)

