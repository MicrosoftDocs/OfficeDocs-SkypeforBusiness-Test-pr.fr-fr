---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399023(v=OCS.15)
ms:contentKeyID: 49299179
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Désactive un service ou un rôle serveur qui a été supprimé d’un ordinateur exécutant Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 désactive l’ordinateur local.

    Disable-CsComputer 

## EXEMPLE 2

La commande présentée dans l’exemple 2 désactive elle aussi l’ordinateur local. Toutefois, outre la désactivation de l’ordinateur, cette commande enregistre des informations relatives au succès (ou à l’échec) de cette tâche dans le fichier C:\\Disable.html. Ce fichier journal est généré en ajoutant le paramètre Report suivi du chemin d’accès au fichier journal dans lequel vous souhaitez enregistrer les informations.

    Disable-CsComputer -Report C:\Logs\Disable.html

## Description détaillée

La suppression d’un service ou d’un rôle serveur d’un ordinateur n’entraîne pas une mise à jour automatique de la topologie Lync Server. En réalité, le service ou le rôle en question doit être désactivé avant que les changements de mise à jour ne soient entièrement réalisés dans la topologie. L’applet de commande **Disable-CsComputer** fournit aux administrateurs un moyen de désactiver des services ou des rôles serveur qui ont été supprimés de l’ordinateur local.

À moins d’utiliser le paramètre Scorch, l’applet de commande **Disable-CsComputer** ne désinstalle pas le logiciel Lync Server ; au lieu de cela, elle interrompt simplement le fonctionnement de l’ordinateur dans son rôle précédemment attitré.

Personnes autorisées à exécuter cette applet de commande : Pour exécuter localement l’applet de commande **Disable-CsComputer**, vous devez être un administrateur local ou un membre du domaine.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un serveur de catalogue global dans votre domaine. Ce paramètre n’est pas obligatoire si vous exécutez l’applet de commande <strong>Disable-CsComputer</strong> sur un ordinateur possédant un compte dans votre domaine.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un contrôleur de domaine dans lequel les paramètres globaux sont stockés. Si les paramètres globaux sont stockés dans le conteneur Système dans services de domaine Active Directory, ce paramètre doit pointer sur le contrôleur de domaine racine. Si les paramètres globaux sont stockés dans le conteneur de configuration, tout contrôleur de domaine peut être utilisé et ce paramètre peut être omis.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\DisableComputer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Désinstalle tous les services et rôles serveur Lync Server pour l’ordinateur local.</p></td>
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

Aucun. L’applet de commande **Disable-CsComputer** n’accepte pas l’entrée redirigée.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Disable-CsComputer** désactive les instances de l’objet Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology.

## Voir aussi

#### Autres ressources

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

