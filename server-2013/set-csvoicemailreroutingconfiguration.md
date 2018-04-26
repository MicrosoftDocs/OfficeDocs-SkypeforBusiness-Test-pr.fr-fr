---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412948(v=OCS.15)
ms:contentKeyID: 49298726
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les paramètres qui fournissent les numéros de téléphone du réseau téléphonique commuté (RTC) permettant d’accéder aux fonctionnalités Accès abonné et Standard automatique de la messagerie unifiée Exchange. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple active les paramètres de configuration du réacheminement des messages vocaux pour le site Redmond1.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## EXEMPLE 2

Cet exemple modifie les paramètres de réacheminement des messages vocaux qui s’appliquent au site Redmond1, en définissant le numéro de téléphone de l’accès abonné à +14255551213.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## Description détaillée

Cette applet de commande vous permet de modifier les paramètres qui déterminent l’emplacement vers lequel les appels Standard automatique et Accès abonné sont redirigés en cas de perte de la connectivité IP vers un serveur de messagerie unifiée Exchange.

Les services Standard automatique et Accès abonné sont des outils de la messagerie unifiée Exchange. Le service Standard automatique fournit la reconnaissance vocale et le contrôle de tonalité (DTMF) permettant aux appelants extérieurs de naviguer dans le système téléphonique d’une entreprise pour accéder au service ou à l’employé souhaité ou, en mode de prise de message, d’accepter les messages des utilisateurs. (Le réacheminement des communications vocales est recommandé en mode de prise de message.) Le service Accès abonné permet aux utilisateurs internes d’accéder à leur boîte aux lettres Microsoft Outlook depuis un téléphone. Les numéros fournis par ces paramètres permettent aux appelants de laisser des messages vocaux aux utilisateurs Voix Entreprise (paramètre AutoAttendantNumber) et permettent à ces derniers de récupérer leurs messages vocaux même si la connectivité IP du déploiement de Lync Server sur un site distant vers messagerie unifiée Exchange dans le centre de données est indisponible (paramètre SubscriberAccessNumber).

Veuillez noter que ces paramètres ne sont pas disponibles tant que la propriété Enabled n’a pas été définie sur True.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoicemailReroutingConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Numéro de téléphone du standard automatique vers lequel les tentatives de dépôt de messages vocaux doivent être réacheminées.</p>
<p>Le numéro fourni à ce paramètre doit être un LineUri d’un objet contact existant.</p>
<p>La valeur doit être un nombre commençant par le chiffre 1 à 9, qui peut être éventuellement précédé du signe plus (+) et suivi de tous les chiffres souhaités.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Indique si les tentatives d’accès à la messagerie vocale doivent être réacheminées via RTC lorsque la connectivité IP est interrompue.</p></td>
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
<td><p>Identificateur unique de la configuration que vous souhaitez modifier. Pour cette applet de commande, la propriété Identity sera Global ou Site:&lt;nom du site&gt;, où &lt;nom du site&gt; est le nom du site auquel les paramètres s’appliquent.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles.</p>
<p>Cet objet doit être du type Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration (qui peut être récupéré en appelant l’applet de commande <strong>Get-CsVoicemailReroutingConfiguration</strong>).</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Numéro d’accès abonné vers lequel les tentatives de récupération des messages vocaux doivent être réacheminées.</p>
<p>Le numéro fourni à ce paramètre doit être un LineUri d’un objet contact existant.</p>
<p>La valeur doit être un nombre commençant par le chiffre 1 à 9, qui peut être éventuellement précédé du signe plus (+) et suivi de tous les chiffres souhaités.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration. Accepte l’entrée redirigée pour les objets de configuration de réacheminement de messagerie vocale.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Voir aussi

#### Autres ressources

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

