---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398393(v=OCS.15)
ms:contentKeyID: 49297321
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les règles de normalisation vocale utilisées dans votre organisation. Les règles de normalisation vocale convertissent des exigences de numérotation téléphonique (par exemple, le fait de composer le 9 pour accéder à une ligne externe) au format de numéro de téléphone E.164 utilisé par Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Cet exemple retourne toutes les règles de normalisation vocale définies pour l’organisation.

    Get-CsVoiceNormalizationRule

## EXEMPLE 2

L’exemple 2 récupère toutes les règles de normalisation vocale spécifiées pour l’ensemble des sites.

    Get-CsVoiceNormalizationRule -Filter site*

## EXEMPLE 3

L’exemple 3 récupère toutes les règles de normalisation vocale avec la lettre « s » à n’importe quelle position dans l’étendue. Par exemple, cela renverra toutes les règles au niveau du site et du service ainsi que les règles de la configuration par utilisateur avec un « s » dans le nom de l’étendue, comme RedmondEastUsers.

    Get-CsVoiceNormalizationRule -Filter *s*

## EXEMPLE 4

Le paramètre Filter utilisé dans les exemples 2 et 3 correspond uniquement à la partie étendue de l’identité. Cet exemple établit une correspondance avec la partie nom pour retourner toutes les règles dont le nom contient la chaîne « seattle ». Pour ce faire, nous appelons d’abord l’applet de commande **Get-CsVoiceNormalizationRule** pour récupérer toutes les règles de normalisation de l’organisation. Nous redirigeons ensuite cette collection vers l’applet de commande **Where-Object** afin de rechercher tous les éléments de la collection pour lesquels la propriété Name correspond à la chaîne « seattle ».

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## Description détaillée

Cette applet de commande retourne une règle de normalisation vocale nommée ou une collection de règles de normalisation vocale. Ces règles sont un élément obligatoire de l’autorisation téléphonique et du routage des appels. Elles définissent les exigences de conversion (traduction) des numéros de format Lync Server interne au format (E.164) standard. Il est bon de savoir comment fonctionne les expressions régulières pour définir les modèles de numéro qui seront traduits.

Les mêmes règles auxquelles accède cette applet de commande sont également accessibles via la propriété NormalizationRules renvoyée par un appel à l’applet de commande **Get-CsDialPlan**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsVoiceNormalizationRule** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p>Utilisez des caractères génériques pour retourner une collection de règles de normalisation basées sur l’identité. Notez que le filtre ne fonctionne que sur la portion étendue de l’identité, pas sur le nom. Par exemple, la valeur de filtre *lob* renverra toutes les règles au niveau de l’étendue globale (étendues contenant les lettres lob), mais pas une règle avec l’identité site:Redmond/lobby où lob ne se trouve que dans la partie identité du nom et pas dans la partie étendue.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique de la règle. Si une valeur est spécifiée pour ce paramètre, elle doit être au format étendue/nom, par exemple, site:Redmond/Rule1 où site:Redmond est l’étendue et Rule1, le nom.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère la règle de normalisation vocale à partir du réplica local du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Get-CsVoiceNormalizationRule** retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Voir aussi

#### Autres ressources

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

