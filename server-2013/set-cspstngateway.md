---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398408(v=OCS.15)
ms:contentKeyID: 49297343
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les propriétés d’une passerelle PSTN (réseau téléphonique commuté). Les passerelles PSTN facilitent le routage des appels entre les périphériques du réseau téléphonique commuté externe et les périphériques de votre réseau Voix Entreprise interne. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 configure la passerelle PstnGateway:192.168.0.240 en tant que passerelle par défaut, ce qui signifie que la passerelle PstnGateway:192.168.0.240 peut servir à la gestion des appels en provenance d’Office Communications Server 2007 R2.

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## EXEMPLE 2

L’exemple 2 configure toutes les passerelles PSTN dans l’organisation pour que chacune d’elles puisse être utilisée pour le routage du trafic sortant. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsService** et le paramètre PstnGateway pour retourner une collection de toutes les passerelles PSTN actuellement utilisées. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object**. L’applet de commande **ForEach-Object** exécute l’applet de commande **Set-CsPstnGateway** sur chaque passerelle de la collection, en modifiant la valeur de la propriété Routable de chacune d’elles sur True.

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## Description détaillée

Les passerelles PSTN permettent aux utilisateurs Voix Entreprise d’effectuer et de recevoir des appels de personnes en provenance du réseau téléphonique commuté. Ces passerelles agissent comme un pont entre le serveur de médiation et le réseau téléphonique commuté.

Les passerelles PSTN sont généralement requises lorsque vous utilisez un système téléphonique TDM PBX (Time Division Multiplex Public Branch Exchange). Dans ce cas, vous devrez utiliser à la fois une passerelle STN et un serveur de médiation pour acheminer les appels Voix Entreprise vers le réseau téléphonique commuté. En revanche, si vous utilisez un système IP-PBX, vous pouvez créer une connexion SIP directe entre le PBX et le serveur de médiation, éliminant ainsi tout recours nécessaire à la passerelle PSTN.

Une fois vos passerelles PSTN installées et configurées, vous pouvez les gérer à l’aide de l’applet de commande **Set-CsPstnGateway**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsPstnGateway** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

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
<td><p><em>AlternateByPassId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Identificateur global unique (GUID) représentant un autre ID de déviation. Ce dernier, automatiquement généré par Lync Server, permet d’éliminer les appels « hairpin ». Selon la configuration de votre système, les appels « hairpin » ignorent automatiquement le serveur de médiation sans avoir à définir et associer des sous-réseaux individuels avec l’ensemble de vos sites et régions.</p>
<p>Pour ce faire, vous devez activer la déviation de manière globale pour utiliser les sites et les régions de configuration réseau, puis activer la déviation sur la configuration de tronçon de votre passerelle PSTN.</p>
<p>Un appel « hairpin » se produit quand un appel entrant sur le réseau téléphonique commuté est renvoyé vers ce réseau via un transfert d’appel ou une sonnerie simultanée.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, la passerelle gère les appels envoyés à partir d’Office Communications Server 2007 R2. Il ne peut y avoir qu’une passerelle par défaut dans la collection des passerelles gérées par un serveur de médiation unique.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation ou les messages d’erreur récupérable qui peuvent s’afficher lors de l’exécution de l’applet de commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port d’écoute utilisé pour communiquer avec les serveurs de médiation via le protocole TCP (Transmission Control Protocol). La valeur par défaut est 5066.</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port d’écoute utilisé pour communiquer avec les serveurs de médiation via le protocole TLS (Transport Layer Security). La valeur par défaut est 5067.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identité du service de la passerelle PSTN à modifier. Par exemple : -Identity &quot;PstnGateway:192.168.0.240&quot;.</p>
<p>Notez que vous pouvez supprimer le préfixe « PstnGatewayServer: » pour spécifier une passerelle PSTN. Par exemple : -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Identité de service du serveur de médiation à associer à la passerelle PSTN. Par exemple : -MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Adresse IP du processeur multimédia associé à la passerelle si l’emplacement du processeur est différent de l’adresse de signalisation. La déviation du trafic multimédia et le contrôle d’admission des appels dépendent de l’emplacement du processeur multimédia de la passerelle. Par défaut, il s’agit du même emplacement que l’adresse de signalisation. Si les deux emplacements diffèrent (avec, par exemple, un processeur multimédia sur un site distant et un composant homologue de signalisation sur le site central), alors RepresentativeMediaIP doit être configuré avec l’adresse IP du processeur multimédia.</p>
<p>Si vous avez déployé plusieurs processeurs multimédias sur le même site avec chacun une adresse IP différente, vous pouvez utiliser ces adresses IP au moment de configurer la propriété RepresentativeMediaIP.</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si la valeur est True, la passerelle peut être utilisée pour les itinéraires de routage du trafic sortant.</p></td>
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

Aucun. L’applet de commande **Get-CsPstnGateway** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Set-CsPstnGateway** ne retourne ni objet ni valeur. Au lieu de cela, l’applet de commande modifie les instances de l’objet Microsoft.Rtc.Management.Xds.DisplayPstnGateway.

## Voir aussi

#### Autres ressources

[Get-CsService](get-csservice.md)

