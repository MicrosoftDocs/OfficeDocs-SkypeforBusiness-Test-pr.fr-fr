---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425732(v=OCS.15)
ms:contentKeyID: 49296593
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Extrait les paramètres qui fournissent les numéros de téléphone RTC (réseau téléphonique commuté) permettant d’accéder aux fonctionnalités Accès abonné et Standard automatique de la messagerie unifiée Exchange. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Cet exemple extrait tous les paramètres de configuration du réacheminement de la messagerie vocale définis dans ce déploiement de Lync Server. Par exemple, s’il existe trois filiales dans lesquelles un dispositif de secours pour succursales est déployé, cette commande retournera les trois jeux de configuration du réacheminement de la messagerie vocale.

    Get-CsVoicemailReroutingConfiguration

## EXEMPLE 2

Cet exemple récupère les paramètres de configuration du réacheminement de la messagerie vocale pour le site BranchOffice\_Portland.

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## EXEMPLE 3

Cet exemple récupère tous les paramètres de réacheminement de la messagerie vocale pour tous les sites dont le nom commence par la chaîne BranchOffice (par ex., BranchOffice\_Portland, BranchOffice\_Sacramento).

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## EXEMPLE 4

Cet exemple récupère toutes les configurations du réacheminement de la messagerie vocale qui ne sont pas activées. La première partie de cette commande est un appel à l’applet de commande **Get-CsVoicemailReroutingConfiguration**, qui récupère une collection de toutes les configurations du réacheminement de la messagerie vocale. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object**. **Where-Object** restreint cette collection pour n’inclure que les configurations dont une propriété Enabled est égale à (-eq) False.

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## Description détaillée

Cette applet de commande extrait les paramètres qui déterminent où sont transférés les appels aux services Standard automatique et Accès abonné lorsque la connectivité IP entre Lync Server sur le site affilié et le messagerie unifiée Exchange du centre de données n’est pas disponible.

Les services Standard automatique et Accès abonné sont des outils de la messagerie unifiée Exchange. Le service Standard automatique fournit la reconnaissance vocale et le contrôle de tonalité (DTMF) permettant aux appelants extérieurs de naviguer dans le système téléphonique d’une entreprise pour accéder au service ou à l’employé souhaité ou, en mode de prise de message, d’accepter les messages des utilisateurs. (Le réacheminement des communications vocales est recommandé en mode de prise de message.) Le service Accès abonné permet aux utilisateurs internes d’accéder à leur boîte aux lettres Microsoft Outlook depuis un téléphone. Les numéros fournis par ces paramètres permettent aux appelants de laisser des messages vocaux aux utilisateurs Voix Entreprise (paramètre AutoAttendantNumber) et permettent à ces derniers de récupérer leurs messages vocaux même si la connectivité IP du déploiement de Lync Server sur un site distant vers la messagerie unifiée Exchange dans le centre de données est indisponible (paramètre SubscriberAccessNumber).

L’appel à cette applet de commande sans paramètre retournera toutes les configurations de réacheminement de la messagerie vocale.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsVoicemailReroutingConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

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
<td><p>Le paramètre Filter vous permet de récupérer les paramètres de configuration pour un ensemble de sites particulier, en fonction des correspondances des caractères génériques.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique de la configuration que vous souhaitez récupérer. Pour cette applet de commande, la propriété Identity sera Global ou Site:&lt;nom du site&gt;, où &lt;nom du site&gt; est le nom du site auquel les paramètres s’appliquent.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère la configuration du réacheminement de la messagerie vocale à partir du réplica local du magasin central de gestion et non du magasin central de gestion proprement dit.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Récupère un ou plusieurs objets de type Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Voir aussi

#### Autres ressources

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

