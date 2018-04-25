---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398298(v=OCS.15)
ms:contentKeyID: 49297124
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne les informations sur les paramètres d’enregistrement des détails des appels. L’enregistrement des détails des appels permet d’assurer le suivi des sessions de messagerie instantanée d’égal à égal, des appels téléphoniques VoIP (Voice over Internet Protocol) et des téléconférences. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Cet exemple utilise l’applet de commande **Get-CsCdrConfiguration** pour retourner une collection de tous les paramètres de l’enregistrement des détails des appels configurés pour être utilisés dans votre organisation.

    Get-CsCdrConfiguration

## EXEMPLE 2

L’exemple 2 utilise le paramètre Identity pour retourner une collection unique des paramètres de l’enregistrement des détails des appels : les paramètres dont l’identité est site:Redmond.

    Get-CsCdrConfiguration -Identity site:Redmond

## EXEMPLE 3

Dans l’exemple 3, le paramètre Filter permet de retourner tous les paramètres de l’enregistrement des détails des appels configurés au niveau du site. La valeur de filtre « site:\* » retourne tous les paramètres de l’enregistrement des détails des appels ayant une identité qui commence par la valeur de chaîne « site: ». Par définition, ces paramètres sont ceux qui ont été configurés au niveau du site.

    Get-CsCdrConfiguration -Filter site:*

## EXEMPLE 4

L’exemple 4 retourne une collection de tous les paramètres de l’enregistrement des détails des appels pour lesquels la propriété KeepCallDetailForDays est inférieure à 30 jours. Pour ce faire, la commande utilise d’abord l’applet de commande **Get-CsCdrConfiguration** pour retourner une collection de tous les paramètres de l’enregistrement des détails des appels configurés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui ne sélectionne que les paramètres pour lesquels la valeur KeepCallDetailForDays est inférieure à 30 jours.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## Description détaillée

L’enregistrement des détails des appels offre un moyen de suivre l’utilisation des fonctionnalités de Lync Server, comme les appels téléphoniques VoIP (Voice over Internet Protocol), la messagerie instantanée, les transferts de fichiers, les conférences audio/vidéo et les sessions de partage d’applications. L’enregistrement des détails des appels (qui n’est disponible que si vous avez déployé le service d’analyse) garde en mémoire les informations d’utilisation : il consigne des informations telles que les parties impliquées dans l’appel, la durée de l’appel et le transfert éventuel de fichiers. (Toutefois, l’enregistrement des détails des appels n’enregistre pas l’appel lui-même.)

L’enregistrement des détails des appels garde également en mémoire les informations sur les erreurs relatives aux appels : données de diagnostic détaillées des sessions d’égal à égal et des téléconférences.

En tant qu’administrateur, vous pouvez décider si l’enregistrement des détails des appels est utilisé dans votre organisation. En effet, si vous avez déployé le service de surveillance, vous pouvez activer/désactiver l’enregistrement des détails des appels. De plus, vous avez la possibilité de prendre une décision globalement (auquel cas l’enregistrement des détails des appels pourra soit être activé ou désactivé dans toute l’organisation) ou par site. Par exemple, vous pouvez utiliser l’enregistrement des détails des appels sur le site Redmond, mais pas sur le site Paris.

L’applet de commande **Get-CsCdrConfiguration** fournit le moyen de retourner des informations détaillées sur la manière dont l’enregistrement des détails des appels est utilisé dans votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsCdrConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet d’utiliser des caractères génériques afin de retourner une collection de paramètres de configuration de l’enregistrement des détails des appels. Par exemple, pour renvoyer une collection de tous les paramètres configurés dans l’étendue Site, utilisez la syntaxe suivante : -Filter site:*. Pour retourner une collection de tous les paramètres ayant la valeur de chaîne « Western » dans leur identité, utilisez cette syntaxe : -Filter *Western*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indique l’identificateur unique de la collection de paramètres de configuration de l’enregistrement des détails des appels que vous voulez retourner. Pour vous référer aux paramètres globaux, utilisez cette syntaxe : -Identity global. Pour renvoyer à une collection configurée au niveau du site, utilisez une syntaxe similaire à celle-ci : -Identity site:Redmond. Notez que vous ne pouvez pas utiliser de caractères génériques lorsque vous spécifiez une identité. Si vous souhaitez utiliser des caractères génériques, utilisez plutôt le paramètre Filter.</p>
<p>Si ce paramètre n’est pas spécifié, alors l’applet de commande <strong>Get-CsCdrConfiguration</strong> retourne la collection de tous les paramètres de configuration de l’enregistrement des détails des appels utilisée dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données de configuration de l’enregistrement des détails des appels à partir du réplica local du magasin central de gestion et non depuis le magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsCdrConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsCdrConfiguration** retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Voir aussi

#### Autres ressources

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

