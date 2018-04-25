---
title: New-CsTrunkConfiguration
TOCTitle: New-CsTrunkConfiguration
ms:assetid: f3958f86-3313-4929-9f9d-f796a2669aea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg413021(v=OCS.15)
ms:contentKeyID: 49299347
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrunkConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une configuration de tronçon qui décrit les paramètres d’une entité de tronçons couplés, comme une passerelle PSTN (réseau téléphonique commuté), un système IP-PBX ou un contrôleur de session en périphérie (SBC), chez le fournisseur de services. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsTrunkConfiguration -Identity <XdsIdentity> [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-InMemory <SwitchParameter>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple crée une nouvelle configuration de tronçon comportant le paramètre Identity site:Redmond. Les propriétés restantes de cette nouvelle configuration adopteront les valeurs par défaut.

    New-CsTrunkConfiguration -Identity site:Redmond

## EXEMPLE 2

Cet exemple crée une nouvelle configuration de tronçon comportant le paramètre Identity site:Redmond et il active la déviation du trafic multimédia. La déviation du trafic multimédia est activée en affectant la valeur $True au paramètre EnableBypass. Les propriétés restantes de cette nouvelle configuration adopteront les valeurs par défaut.

    New-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## EXEMPLE 3

Cet exemple crée une nouvelle configuration de tronçon comportant le paramètre Identity site:Redmond, puis affecte une nouvelle traduction sortante à ce tronçon. La première ligne de cet exemple appelle l’applet de commande **New-CsTrunkConfiguration** pour créer la nouvelle configuration de tronçon avec les paramètres par défaut. La deuxième ligne appelle l’applet de commande **New-CsOutboundTranslationRule**. Notez la valeur affectée au paramètre Identity : site:Redmond/OTR1. La première partie du paramètre Identity (site:Redmond) définit l’étendue dans laquelle s’applique la règle. Cette étendue correspond au paramètre Identity de la nouvelle configuration de tronçon ; cela signifie que cette règle sera automatiquement appliquée à cette configuration. L’étendue est suivie d’une barre oblique (/) puis d’une chaîne : il s’agit d’un nom unique pour cette règle (il peut exister plus d’une règle par étendue). Après cela, nous transmettons simplement les valeurs aux paramètres Pattern et Translation afin de définir cette règle.

    New-CsTrunkConfiguration -Identity site:Redmond
    New-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Pattern '^\+(\d{8})$' -Translation '9$1'

## Description détaillée

Utilisez cette applet de commande pour créer une nouvelle configuration de tronçon applicable à des passerelles PSTN. Chaque configuration contient les paramètres spécifiques d’une entité de tronçons couplés existante, comme une passerelle PSTN, un système IP-PBX ou un contrôleur de session en périphérie (SBC), chez le fournisseur de services. Ces paramètres déterminent, entre autres, si la fonctionnalité de déviation du trafic multimédia est activée sur ce tronçon, si les paquets RTCP (Real-time Transport Control Protocol) sont envoyés dans certaines conditions et si un chiffrement SRTP (Secure Real-time Transport Protocol) est nécessaire.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsTrunkConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrunkConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique qui inclut l’étendue de la configuration de tronçon. La configuration de tronçon peut être créée au niveau de l’étendue globale ou de l’étendue Site, voire au niveau de l’étendue Service pour un service de passerelle PSTN. (Une configuration globale existe par défaut et ne peut être ni supprimée, ni recréé.) Exemple : site:Redmond (pour le site) ou PstnGateway:Redmond.litwareinc.com (pour le service).</p></td>
</tr>
<tr class="even">
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La valeur de ce paramètre détermine s’il existe un point de terminaison multimédia connu (une passerelle PSTN où la terminaison multimédia possède la même adresse IP que la terminaison de signalisation est un exemple de point de terminaison multimédia connu). Définissez cette valeur sur False si le tronçon ne comporte pas de point de terminaison multimédia connu.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Chaîne décrivant l’objectif de la configuration de tronçon.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si le protocole 3pcc peut être utilisé pour autoriser les appels transférés à ignorer le site hébergé. 3pcc est également connu sous le nom de « contrôle tiers », et se produit quand un tiers est utilisé pour connecter une paire d’appelants (par exemple, un opérateur passant un appel d’une personne A à une personne B). La méthode REFER est une méthode SIP standard qui indique que le destinataire doit contacter un tiers en utilisant les informations fournies par l’émetteur. La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBypass</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La valeur de ce paramètre détermine si la fonctionnalité de déviation du trafic multimédia est activée pour ce tronçon. Définissez cette valeur sur True pour activer la déviation du trafic multimédia. Notez que pour que la déviation du trafic multimédia fonctionne correctement, les passerelles PSTN, les contrôleurs de session en périphérie (SBC) et les autocommutateurs privés (PBX) doivent prendre en charge certaines fonctionnalités, parmi lesquelles :</p>
<p>- La possibilité de recevoir des réponses dirigées à une invitation.</p>
<p>- Les clients Lync Server et le point de terminaison multimédia doivent pouvoir communiquer directement entre eux sans passer par un serveur de médiation.</p>
<p>- Le sous-réseau de la passerelle doit être défini comme étant situé sur le même site que celui du sous-réseau du client. S’il est situé sur un autre site, les sites ne doivent pas être séparés par des liaisons réseau étendu (WAN) munies d’une bande passante restreinte.</p>
<p>La déviation du trafic multimédia ne peut être activée que dans les circonstances suivantes :</p>
<p>- Le paramètre ConcentratedTopology est défini sur True.</p>
<p>- Le paramètre EnableReferSupport est défini sur False, RTCPActiveCalls et RTCPCallsOnHold sont définis sur False ou EnableReferSupport est défini sur True.</p>
<p>Notez que si EnableBypass est True et EnableReferSupport est False, les appels déviés et transférés par la suite deviennent non déviés.</p>
<p>Pour que la déviation du trafic multimédia fonctionne pour un tronçon en particulier, vous devez l’activer globalement et individuellement pour le tronçon en question. Utilisez l’applet de commande <strong>New-CsNetworkMediaBypassConfiguration</strong> pour activer globalement la déviation du trafic multimédia.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Quand la valeur est True, les appels sortants auxquels la passerelle ne répond pas dans les 10 secondes seront routés vers la jonction suivante disponible ; s’il n’existe aucune jonction supplémentaire, l’appel est automatiquement abandonné. Dans une organisation avec des réponses de passerelle ou réseau lentes, cela peut entraîner l’abandon de nombreux appels.</p>
<p>La valeur par défaut est True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, le routage des communications vocales basé sur l’emplacement est activé pour les appels transmis par le biais des jonctions SIP gérées par la collection spécifiée de paramètres de configuration de jonction SIP. Dans le cadre du routage des communications vocales basé sur l’emplacement, l’emplacement de l’utilisateur qui passe l’appel et l’emplacement de l’utilisateur qui reçoit l’appel sont pris en compte lors de l’acheminement des appels. Si cette propriété a la valeur True (la valeur par défaut est False), vous devez également définir la propriété NetworkSiteId.</p>
<p>Ce paramètre a été introduit dans la version publiée en février 2013 de Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Définit si le fournisseur de services est un opérateur mobile.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si les jonctions SIP prennent en charge la Voix en ligne. Avec la Voix en ligne, les utilisateurs disposent d’un compte Lync Server local, mais leur messagerie vocale est hébergée par Office 365. La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Définit si les appels d’urgence doivent être acheminés avec un objet PIDF-LO (Presence Information Data Format Location Object) via la passerelle définie. Définissez ce paramètre sur True si les appels d’urgence sont à acheminer vers un fournisseur de services d’urgence certifié. (L’emplacement sera transmis avec l’appel.)</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Détermine si ce tronçon prend en charge la réception de demandes de référencement en provenance du serveur de médiation.</p>
<p>La déviation du trafic multimédia ne peut être activée que dans les circonstances suivantes :</p>
<p>- Le paramètre ConcentratedTopology est défini sur True.</p>
<p>- Le paramètre EnableReferSupport est défini sur False, RTCPActiveCalls et RTCPCallsOnHold sont définis sur False ou EnableReferSupport est défini sur True.</p>
<p>Notez que si EnableBypass est True et EnableReferSupport est False, les appels déviés et transférés par la suite deviennent non déviés.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si les jonctions SIP prennent en charge l’accrochage RTP. L’accrochage RTP est une technologie qui permet la connectivité RTP/RTCP via un appareil ou un pare-feu NAT (traduction d’adresses réseau). La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si le temporisateur de session est activé. Les temporisateurs de session sont utilisés pour déterminer si une session particulière est toujours active.</p>
<p>Notez que même si ce paramètre est défini sur False, des temporisateurs de session peuvent être appliqués si un temporisateur de session est activé pour la connexion distante. Dans un cas comme celui-ci, le serveur de médiation répond aux sondages du temporisateur de session à partir de l’entité distante.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsque ce paramètre est défini sur True, la passerelle PSTN, le système IP-PBX ou le contrôleur de session en périphérie (SBC) chez le fournisseur de services gonfle le volume audio en flux vocaux qui sont transmis au serveur de médiation ou aux clients Lync Server. Si cette valeur est définie sur False, le volume audio sera augmenté soit sur le serveur de médiation (pour les appels non déviés), soit sur les clients Lync Server (pour les appels déviés).</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si les informations d’historique d’appel sont transférées via la jonction. La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si l’en-tête P-Asserted-Identity (PAI) sera transféré avec l’appel. L’en-tête PAI permet de vérifier l’identité de l’appelant. La valeur par défaut est False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Facultatif</p></td>
<td><p>UInt32</p></td>
<td><p>Nombre maximal de réponses dirigées qu’une passerelle PSTN, un système IP-PBX ou un contrôleur de session en périphérie (SBC), chez le fournisseur de services, peut recevoir pour une invitation qui est envoyée au serveur de médiation.</p>
<p>Valeur par défaut : 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>ID de site du site réseau associé à la nouvelle collection de paramètres de configuration de jonction. Si la propriété EnableLocationRestriction a la valeur True, le routage des communications vocales basé sur l’emplacement par le biais de cette jonction est géré à l’aide des paramètres configurés pour le site spécifié. Vous pouvez récupérer les ID de site réseau à l’aide de cette commande :</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p>
<p>Ce paramètre a été introduit dans la version publiée en février 2013 de Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection de règles de traduction de numéro d’appel sortant assignées à la jonction. Vous pouvez extraire ces informations sur les règles disponibles avec la commande :</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection de règles de traduction de numéros de téléphone qui s’appliquent aux appels gérés par le routage sortant (appels acheminés vers les destinations PBX ou PSTN).</p>
<p>Même si cette liste et ces règles peuvent être créées directement avec cette applet de commande, il est recommandé de créer les règles de traduction sortante avec l’applet de commande <strong>New-CsOutboundTranslationRule</strong> qui crée la règle et l’attribue à la configuration de tronçon avec l’étendue correspondante.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection d’utilisations PSTN assignées à la jonction. Vous pouvez extraire ces informations sur les utilisations disponibles avec la commande :</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La définition de ce paramètre sur True entraînera la suppression des signes plus (+) à gauche des URI (Uniform Resource Identifier) par le serveur de médiation avant de les envoyer au fournisseur de services.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Ce paramètre détermine si des paquets RTCP sont transmis à la passerelle PSTN, au système IP-PBX ou au contrôleur de session en périphérie (SBC) côté fournisseur de services pour les appels actifs. Un appel actif dans ce contexte désigne un appel qui est autorisé à voyager dans au moins une direction. Si le paramètre RTCPActiveCalls est défini sur True, le serveur de médiation ou le client Lync Server peut mettre fin à un appel s’il ne reçoit aucun paquet RTCP dans un délai de plus de 30 secondes.</p>
<p>Notez que toute désactivation des contrôles du trafic multimédia RTCP reçu pour les appels actifs dans les éléments de Lync Server vous prive d’un garde-fou important lors de la détection d’une paire supprimée. Cette opération ne doit donc être effectuée que si elle est vraiment nécessaire.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Ce paramètre détermine si des paquets RTCP continuent d’être envoyés sur le tronçon pour les appels qui ont été mis en attente et si aucun paquet multimédia n’est supposé prendre une direction quelconque. Si une attente musicale est activée sur le client Lync Server ou sur le tronçon, l’appel sera considéré comme étant actif et cette propriété sera ignorée. Dans ces circonstances, utilisez le paramètre RTCPActiveCalls.</p>
<p>Notez que toute désactivation des contrôles du trafic multimédia RTCP reçu pour les appels actifs dans les éléments de Lync Server vous prive d’un garde-fou important lors de la détection d’une paire supprimée. Cette opération ne doit donc être effectuée que si elle est vraiment nécessaire.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste de règles de traduction de codes de réponse SIP applicables aux codes de réponse reçus d’une passerelle PSTN, d’un système IP-PBX ou d’un contrôleur de session en périphérie (SBC) chez le fournisseur de services. Ces règles permettent à l’administrateur de mapper les codes de réponse SIP ayant des valeurs comprises entre 400 et 699 reçues dans un tronçon avec des nouvelles valeurs plus cohérentes avec Lync Server.</p>
<p>Vous pouvez créer cette liste et les règles qui y correspondent directement à l’aide de cette applet de commande. Néanmoins, nous vous recommandons de créer les règles de traduction de codes de réponse SIP en appelant l’applet de commande <strong>New-CsSipResponseCodeTranslationRule</strong>. Celle-ci crée la règle et l’attribue à la configuration de tronçon avec l’étendue correspondante.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SRTPMode</p></td>
<td><p>La valeur de ce paramètre détermine le niveau de prise en charge du chiffrement SRTP pour la protection du trafic multimédia entre le serveur de médiation et la passerelle PSTN, le système IP-PBX ou le contrôleur de session en périphérie (SBC) chez le fournisseur de services. Dans les cas de déviation du trafic multimédia, cette valeur doit être compatible avec le paramètre EncryptionLevel de la configuration multimédia. La configuration multimédia est définie à l’aide de l’applet de commande <strong>New-CsMediaConfiguration</strong> et de l’applet de commande <strong>Set-CsMediaConfiguration</strong>.</p>
<p>Valeurs valides :</p>
<p>- Required : le chiffrement SRTP doit être utilisé.</p>
<p>- Optional : le chiffrement SRTP sera utilisé s’il est pris en charge par la passerelle.</p>
<p>- NotSupported : le chiffrement SRTP n’est pas pris en charge et ne sera donc pas utilisé.</p>
<p>Remarque : SRTPMode est utilisé uniquement si la passerelle est configurée en vue d’un recours au protocole de transport TLS (Transport Layer Security). Si la passerelle est configurée avec le protocole de transport TCP, SRTPMode est défini en interne sur NotSupported.</p>
<p>Valeur par défaut : Obligatoire</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Voir aussi

#### Autres ressources

[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)

