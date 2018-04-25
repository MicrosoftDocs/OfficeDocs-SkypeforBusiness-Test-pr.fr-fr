---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398948(v=OCS.15)
ms:contentKeyID: 49299007
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur le service de parcage d’appel. Le parcage d’appel est un service qui permet à un utilisateur de « parquer » un appel téléphonique entrant. Le parcage d’appel a pour effet de transférer ce dernier vers une plage spécifique, puis de le placer en attente. N’importe qui (pas seulement la personne qui a répondu à l’appel) peut reprendre la conversation depuis le téléphone souhaité dans le système, en tapant le bon numéro. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 récupère une collection de toutes les configurations de service de parcage d’appel qui ont été définies pour un usage au sein de votre organisation.

    Get-CsCpsConfiguration

## EXEMPLE 2

L’exemple 2 récupère uniquement les configurations de service de parcage d’appel ayant l’identité site:Redmond1.

    Get-CsCpsConfiguration -Identity site:Redmond1

## EXEMPLE 3

Dans l’exemple 3, le paramètre Filter permet de retourner toutes les configurations de service de parcage d’appel qui ont été définies dans l’étendue Site. Le caractère générique site:\* indique à l’applet de commande **Get-CsCpsConfiguration** de retourner uniquement les paramètres dont l’identité commence par la valeur de chaîne site:.

    Get-CsCpsConfiguration -Filter site:*

## EXEMPLE 4

Tout comme dans l’exemple 3, cet exemple utilise le paramètre Filter pour récupérer un sous-ensemble de toutes les configurations de service de parcage d’appel définies. Dans ce cas, le filtre est appliqué sur la chaîne \*:re\* qui renvoie toutes les configurations de service de parcage d’appel pour tous les sites dont les noms commencent par les lettres « re » comme Redmond1, Redmond2 et RemoteComputer.

    Get-CsCpsConfiguration -Filter *:re*

## EXEMPLE 5

La commande affichée ci-dessus retourne tous les paramètres de service de parcage d’appel qui n’émettent aucune musique lorsqu’un appelant est mis en attente. Pour cela, la commande utilise d’abord l’applet de commande **Get-CsCpsConfiguration** afin de récupérer tous les paramètres de service de parcage d’appel qui ont été configurés pour être utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object**, puis celle-ci applique à son tour un filtre qui limite les données retournées aux éléments dans lesquels la propriété EnableMusicOnHold est égale à (-eq) False.

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## Description détaillée

Cette applet de commande permet de récupérer une ou plusieurs configurations de service de parcage d’appel. Une configuration de service de parcage d’appel spécifie l’action effectuée sur un appel une fois que celui-ci a été parqué. Par exemple, si un appel parqué reste sans réponse après un certain temps, il peut être automatiquement transféré à une autre personne, comme un administrateur ou un Response Group. Les appels peuvent également être configurés pour émettre une sonnerie après une certaine durée pour s’assurer qu’ils n’ont pas été oubliés. De plus, le service de parcage d’appel peut être configuré pour diffuser une musique d’attente à l’appelant pendant le parcage de l’appel.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsCpsConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p>Vous permet d’effectuer une recherche par caractères génériques afin d’extraire uniquement les configurations dont les valeurs Identity correspondent à la chaîne à caractère générique.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique de la configuration de service de parcage d’appel que vous souhaitez récupérer. Cet identificateur sera de type Global ou site:&lt;nom_site&gt;, où &lt;nom_site&gt; est le nom du site auquel la configuration s’applique.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les informations sur le service de parcage d’appel du réplica local du magasin central de gestion et non du magasin central de gestion proprement dit.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Récupère un ou plusieurs objets de type Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Voir aussi

#### Autres ressources

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

