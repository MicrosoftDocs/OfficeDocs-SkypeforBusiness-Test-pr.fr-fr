---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412721(v=OCS.15)
ms:contentKeyID: 49298310
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une collection de paramètres de service de parcage d’appel. Le parcage d’appel est un service qui permet à un utilisateur de « parquer » un appel téléphonique entrant. Le parcage d’appel a pour effet de transférer ce dernier vers une plage spécifique (ou numéro), puis de le placer en attente. N’importe qui (et pas seulement la personne qui a répondu à l’appel) peut reprendre la conversation depuis le téléphone souhaité en entrant simplement le chiffre correct. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 modifie la configuration du service de parcage d’appel portant l’identité site:Redmond1 en définissant, pour l’appel parqué, le nombre maximum de rappels du téléphone ayant répondu sur 2. Pour cela, le paramètre MaxCallPickupAttempts est inclus et sa valeur est définie sur 2.

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## EXEMPLE 2

L’exemple 2 est une variation de la commande illustrée dans l’exemple 1. Dans ce cas, toutefois, la propriété MaxCallPickupAttempts de toutes les configurations du service de parcage d’appel est définie sur 2. Pour ce faire, l’applet de commande **Get-CsCpsConfiguration** est utilisée pour récupérer une collection de tous les paramètres du service de parcage d’appel utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Set-CsCpsConfiguration**, qui extrait chaque élément de la collection et définit à 2 la valeur de la propriété MaxCallPickupAttempts.

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## EXEMPLE 3

Cet exemple modifie la configuration du parcage d’appel pour le site Redmond1 en définissant sur 45 secondes la durée d’attente avant le rappel d’un appel parqué (contenu dans la propriété CallPickupTimeoutThreshold).

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## Description détaillée

Cette applet de commande permet de modifier une configuration de service de parcage d’appel. Une configuration de service de parcage d’appel spécifie l’action effectuée sur un appel une fois que celui-ci a été parqué. Par exemple, si un appel parqué reste sans réponse après un certain temps, il peut être automatiquement transféré à une autre personne, comme un administrateur ou un Response Group. Les appels peuvent être configurés pour émettre une sonnerie après une certaine durée, afin qu’on ne les oublie pas. De plus, le service de parcage d’appel peut être configuré pour diffuser une musique d’attente à l’appelant pendant le parcage de l’appel.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsCpsConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>Facultatif</p></td>
<td><p>TimeSpan</p></td>
<td><p>Temps qui s’écoule à partir du parcage d’un appel, avant que ce dernier soit de nouveau émis à destination du téléphone sur lequel l’appel a été répondu.</p>
<p>Ce paramètre doit être entré au format hh:mm:ss (hh = heures, mm = minutes, ss = secondes).</p>
<p>Valeur minimale : 10 secondes (00:00:10) ; valeur maximale : 10 minutes (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Détermine si une musique doit être diffusée à l’appelant pendant le parcage d’un appel.</p>
<p>Lync Server est fourni avec un fichier d’attente musicale par défaut. Vous pouvez modifier ce fichier (et donc la musique qu’entend l’appelant pendant la durée de parcage) au moyen de l’applet de commande <strong>Set-CsCallParkServiceMusicOnHoldFile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique de la configuration que vous souhaitez modifier. L’identité spécifie le niveau de l’étendue d’application de la configuration, c’est-à-dire au niveau global ou au niveau d’un site spécifique (au format site:&lt;nom_site&gt;, tel que site:Redmond).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>CallParkServiceSettings</p></td>
<td><p>Référence à un objet de configuration de service de parcage d’appel, de type Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Cet objet peut être récupéré avec l’applet de commande <strong>Get-CsCpsConfiguration</strong>. L’objet peut alors être modifié et les modifications peuvent être enregistrées en renvoyant l’objet vers l’applet de commande <strong>Set-CsCpsConfiguration</strong> dans ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Nombre de tentatives de rappel effectuées pour un appel parqué vers le téléphone qui a répondu avant que l’appel soit abandonné et transféré vers l’URI (Uniform Resource Identifier) de secours. L’URI de secours est définie à l’aide du paramètre OnTimeoutURI.</p>
<p>Valeur minimale : 1 ; valeur maximale : 10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP de l’utilisateur ou du Response Group vers lequel les appels parqués restés sans réponse sont routés. L’appel parqué sera routé après avoir défini le nombre de rappels à l’aide du paramètre MaxCallPickupAttempts. Si ce paramètre a la valeur Null, le paramètre OnTimeoutURI sera ignoré et l’appel parqué sera déconnecté après les tentatives de rappel infructueuses.</p>
<p>Les valeurs doivent être des URI SIP et commencer par la chaîne sip:. Par exemple : sip:rgs1@litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Accepte les données redirigées pour les objets de configuration de service de parcage d’appel.

## Types de retours

Modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Voir aussi

#### Autres ressources

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

