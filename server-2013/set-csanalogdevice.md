---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412843(v=OCS.15)
ms:contentKeyID: 49298563
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un périphérique existant de la collection de périphériques analogiques pouvant être gérés à l’aide de Lync Server. Un périphérique analogique est un téléphone ou tout autre appareil connecté au réseau téléphonique commuté (PSTN). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 modifie la valeur de la propriété LineUri pour le périphérique analogique dont l’identité (paramètre Identity) est CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## EXEMPLE 2

La commande de l’exemple 2 modifie la passerelle de chaque périphérique analogique utilisant actuellement la passerelle 192.168.0.240. Pour exécuter cette tâche, l’applet de commande **Get-CsAnalogDevice** est appelée avec le paramètre Filter. La valeur de filtre {Gateway -eq « 192.168.0.240 »} garantit que seuls les périphériques comportant une passerelle égale à (-eq) 192.168.0.240 sont retournés. La collection filtrée est ensuite redirigée vers l’applet de commande **Set-CsAnalogDevice**, qui sélectionne chaque élément de la collection et remplace la valeur de la propriété Gateway par 192.168.1.100.

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## Description détaillée

Parmi les périphériques analogiques se trouvent les téléphones, les télécopieurs, les modems et les périphériques TTY/TDD (téléscripteur/appareil de télécommunications pour malentendants) connectés au réseau téléphonique commuté (PSTN). À l’inverse des périphériques tirant parti de Voix Entreprise (à savoir, l’implémentation par Microsoft de la voix sur IP, ou « VoIP »), les périphériques analogiques ne transmettent pas d’informations à l’aide de paquets numériques. Au lieu de cela, les informations sont transmises à l’aide d’un signal continu. Ce signal est connu sous le nom de signal analogique, d’où le terme « périphériques analogiques ».

Afin de permettre aux administrateurs de gérer les périphériques analogiques, Lync Server vous permet d’associer des périphériques analogiques à des objets contact Active Directory. Après l’association d’un périphérique à un objet contact, vous pouvez alors gérer le périphérique analogique en attribuant des stratégies et des plans de numérotation au contact.

L’applet de commande **Set-CsAnalogDevice** vous permet de modifier les propriétés des objets contact associés à des périphériques analogiques. Vous pouvez, par exemple, modifier le nom complet Active Directory du contact ou l’URI (Uniform Resource Identifier) de ligne associé au périphérique.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsAnalogDevice** : RTCUniversalUserAdmins. Les autorisations d’exécuter cette applet de commande pour des sites spécifiques ou des unités d’organisation Active Directory spécifiques peuvent être attribuées au moyen de l’applet de commande **Grant-CsOUPermission**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>UserIdParameter</p></td>
<td><p>Identificateur unique du périphérique analogique modifié. Les périphériques analogiques sont identifiés à l’aide d’un nom Active Directory unique de l’objet contact associé. Par défaut, les périphériques analogiques utilisent un identificateur global unique (GUID) comme nom commun et ont donc généralement un identificateur semblable à celui-ci : CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Par conséquent, vous pouvez trouver qu’il est plus facile de modifier les périphériques analogiques avec l’applet de commande <strong>Get-CsAnalogDevice</strong> pour retourner les objets de périphériques analogiques, puis de rediriger ces objets vers l’applet de commande <strong>Set-CsAnalogDevice</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>À définir sur True ($True) si le périphérique analogique est un télécopieur. À définir sur False ($False) si le périphérique n’est pas un télécopieur.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Configure le nom complet Active Directory du périphérique analogique.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Numéro de téléphone tel qu’il est affiché dans Lync. La propriété DisplayNumber peut prendre le format que vous souhaitez, par exemple 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234, etc.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Fqdn</p></td>
<td><p>Permet de se connecter au contrôleur de domaine spécifié, afin de modifier des informations de contact. Pour vous connecter à un contrôleur de domaine spécifique, incluez le paramètre DomainController suivi du nom de l’ordinateur (par exemple, atl-mcs-001) ou son nom de domaine complet (FDQN), par exemple, atl-mcs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Lorsqu’il est défini sur True ($True), le périphérique analogique peut être utilisé avec Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Indique si l’objet contact du périphérique analogique a été activé pour Voix Entreprise, l’implémentation par Microsoft de la voix sur IP, ou « VoIP ». Avec Voix Entreprise, les utilisateurs peuvent passer des appels téléphoniques via Internet au lieu d’utiliser le réseau téléphonique standard.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indique l’emplacement auquel les sessions de messagerie instantanée du contact sont archivées. Les valeurs autorisées sont les suivantes :</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>Gateway</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Fqdn</p></td>
<td><p>Adresse IP de la passerelle PSTN que doit utiliser le périphérique analogique.</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Numéro de téléphone pour le périphérique analogique. Vous devez entrer l’URI de ligne au format E.164 en utilisant le préfixe « TEL: ». Par exemple : TEL:+14255551297. Tout numéro de poste doit être ajouté à la fin de l’URI de ligne (par exemple : TEL:+14255551297; ext=51297.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facultatif</p></td>
<td><p>witchParameter</p></td>
<td><p>Retourne un objet représentant le téléphone de partie commune.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identificateur unique qui permet au périphérique analogique de communiquer avec des périphériques SIP, tels que Lync 2013. L’adresse SIP doit être précédée du préfixe « sip: ». Par exemple : sip:bldg14lobby@litwareinc.com.</p></td>
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

Objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact. L’applet de commande **Set-CsAnalogDevice** accepte les instances redirigées de l’objet du périphérique analogique.

## Types de retours

Par défaut, l’applet de commande **Set-CsAnalogDevice** ne retourne ni objet, ni valeur. Toutefois, si vous incluez le paramètre PassThru, l’applet de commande retourne des instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Voir aussi

#### Autres ressources

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

