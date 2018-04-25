---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399021(v=OCS.15)
ms:contentKeyID: 49299155
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une stratégie de voix existante. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple définit la propriété AllowSimulRing sur False pour la stratégie utilisateur UserVoicePolicy2, ce qui signifie que tous les utilisateurs auxquels cette stratégie est affectée ne sont pas activés pour la sonnerie simultanée, fonction qui détermine si un deuxième téléphone (comme un téléphone mobile) peut être défini pour sonner chaque fois que le téléphone du bureau de l’utilisateur sonne. Cette commande supprime aussi « Local » de la liste des utilisations PSTN pour cette stratégie. (Notez que le paramètre Identity n’est pas explicitement spécifié. Le paramètre Identity est un paramètre positionnel. Par conséquent, si vous spécifiez d’abord la valeur d’identité dans la liste des paramètres, vous ne devez pas indiquer explicitement qu’il s’agit de Identity.)

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## EXEMPLE 2

Cet exemple modifie la stratégie de voix du site de Redmond de sorte que toutes les utilisations PSTN définies pour l’organisation soient appliquées à cette stratégie. La première ligne de cet exemple appelle l’applet de commande **Get-CsPstnUsage** pour récupérer l’ensemble global des utilisations PSTN de l’organisation, puis l’enregistrer dans la variable $a. La deuxième ligne appelle l’applet de commande **Set-CsVoicePolicy** pour modifier la stratégie de voix pour le site de Redmond. Une valeur est transmise au paramètre PstnUsages pour remplacer la liste actuelle des utilisations de la stratégie par la liste contenue dans cet ensemble global d’utilisations PSTN. Veuillez noter la syntaxe de la valeur remplacée : $a.Usage. Cela fait référence à la propriété Usage des paramètres d’utilisation PSTN qui renferme la liste des utilisations PSTN.

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## Description détaillée

Cette applet de commande modifie une stratégie de voix existante. Les stratégies de voix permettent de gérer les fonctionnalités Voix Entreprise comme la sonnerie simultanée (possibilité d’avoir une deuxième sonnerie de téléphone chaque fois que quelqu’un appelle sur votre téléphone professionnel) et le transfert d’appel. Utilisez cette applet de commande pour modifier les paramètres qui activent et désactivent un grand nombre de ces fonctions.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoicePolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Si ce paramètre est défini sur True, les utilisateurs affectés à cette stratégie peuvent transférer des appels. Si ce paramètre a la valeur False, les appels ne peuvent pas être transférés.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsque ce paramètre est défini sur True, les appels effectués vers des numéros internes hébergés dans un autre pool seront acheminés via le réseau téléphonique commuté (PSTN) lorsque le pool ou le réseau étendu (WAN) ne sont pas disponibles.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La sonnerie simultanée est une fonction qui permet de faire sonner plusieurs téléphones en composant un seul numéro. Définissez ce paramètre sur True pour activer la sonnerie simultanée. Si ce paramètre est défini sur False, la sonnerie simultanée ne peut être configurée pour aucun utilisateur affecté à cette stratégie.</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Facultatif</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Permet aux administrateurs de gérer le transfert d’appel et la sonnerie simultanée. Les valeurs autorisées sont les suivantes :</p>
<p>* VoicePolicyUsage – L’utilisation de stratégie voix par défaut est utilisée pour gérer le transfert d’appel et la sonnerie simultanée pour tous les appels. Il s’agit de la valeur par défaut.</p>
<p>* InternalOnly – Le transfert d’appel et la sonnerie simultanée sont limités aux appels passés d’un utilisateur Lync à un autre.</p>
<p>* CustomUsage. Une utilisation PSTN personnalisée sera utilisée pour gérer le transfert d’appel et la sonnerie simultanée. Cet utilisateur doit être spécifié avec le paramètre CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Utilisation PSTN personnalisée pour gérer le transfert d’appel et la sonnerie simultanée. Pour ajouter une utilisation personnalisée à la stratégie voix utilisez une syntaxe telle que :</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Pour supprimer une utilisation personnalisée, utilisez la syntaxe suivante :</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Notez que l’utilisation doit exister avant d’être utilisée avec le paramètre CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Description de la stratégie de voix.</p>
<p>Longueur maximale : 1040 caractères.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Des stratégies peuvent être définies pour restreindre la bande passante et définir des propriétés diverses liées à la configuration du réseau. Définissez ce paramètre sur True pour autoriser le remplacement de ces stratégies. En d’autres termes, si ce paramètre est défini sur True, aucune vérification de bande passante ne se fera et les appels passeront quels que soient les paramètres de contrôle d’admission des appels (CAC) définis.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>L’application de parcage d’appel permet de mettre un appel en attente (ou encore de le parquer) sur un numéro particulier dans une plage de numéros en vue d’une récupération ultérieure. Définissez ce paramètre sur True pour activer cette application pour les utilisateurs affectés à cette stratégie. Si ce paramètre est défini sur False, les utilisateurs affectés à cette stratégie ne pourront pas parquer les appels destinés à leur numéro de téléphone.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Détermine si les appels peuvent être transférés vers un autre numéro. Si ce paramètre est défini sur True, les appels peuvent être transférés ; si ce paramètre est défini sur False, les appels ne peuvent pas être transférés.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La délégation d’appels permet à un utilisateur de répondre ou de passer des appels pour un autre utilisateur. Par exemple, un responsable peut configurer la délégation d’appels pour que tous les appels entrants sonnent à la fois sur son téléphone et sur le téléphone d’un administrateur. Définissez ce paramètre sur True pour permettre aux utilisateurs disposant de cette stratégie de configurer la délégation d’appels. Définissez ce paramètre sur False pour désactiver la délégation d’appels.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Le suivi des appels malveillants est une norme permettant d’effectuer un suivi des appels qu’un utilisateur désigne comme malveillants. Ces appels peuvent être suivis même si l’ID d’appelant est bloqué. Le suivi est uniquement accessible aux responsables adéquats mais pas à l’utilisateur. Définissez cette propriété sur True pour autoriser la mise en place du suivi des appels malveillants.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>L’appel d’équipe permet à un utilisateur de désigner un groupe d’autres utilisateurs dont les téléphones sonneront lorsqu’un appel sera adressé au numéro de cet utilisateur. Cette fonction est utile dans les équipes où, par exemple, tous les membres peuvent répondre aux appels entrants des clients. Définissez ce paramètre sur True pour activer cette fonction.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Quand il a la valeur True, les appels sans réponse à un appareil mobile seront routés vers la messagerie vocale de l’organisation au lieu de la messagerie vocale du fournisseur de l’appareil mobile. S’il est répondu à un appel « trop tôt » (c’est-à-dire, avant que la valeur configurée pour la propriété PSTNVoicemailEscapeTimer ne soit passée) il est considéré que l’appareil mobile n’est pas disponible et l’appel est routé vers la messagerie vocale de l’organisation.</p>
<p>La valeur par défaut est False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique spécifiant l’étendue et, dans certains cas, le nom de la stratégie.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles. Cet objet doit être de type VoicePolicy et peut être récupéré en appelant l’applet de commande <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom convivial décrivant cette stratégie.</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Les frais de réseau téléphonique commuté (PSTN) sont plus communément appelés « frais d’appel longue distance ». Les organisations peuvent parfois éviter ces frais en implémentant une solution VoIP (Voice over Internet Protocol) qui permet aux succursales de se connecter via des appels réseau. Si vous définissez ce paramètre sur True, vos appels passeront par le réseau téléphonique commuté (PSTN) et entraîneront des frais, ce qui n’est pas le cas via le réseau.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste des utilisations PSTN disponibles pour cette stratégie. Une utilisation PSTN lie une stratégie de voix à un itinéraire téléphonique.</p>
<p>Toute valeur de chaîne peut être placée dans cette liste, tant que la valeur existe dans la liste globale des utilisations PSTN. (Les chaînes dupliquées ne sont pas autorisées ; chaque chaîne doit être unique.) La liste des utilisations PSTN peut être récupérée en appelant l’applet de commande <strong>Get-CsPstnUsage</strong>.</p>
<p>Gardez à l’esprit que si vous utilisez ce paramètre pour supprimer toutes les utilisations PSTN de la stratégie, les utilisateurs auxquels cette stratégie a été accordée ne pourront pas effectuer des appels PSTN sortants.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int64</p></td>
<td><p>Temps (en millisecondes) utilisé pour déterminer si la réponse à un appel est intervenue « trop tôt ». Si une réponse est reçue dans cet intervalle de temps Lync Server considère que l’appareil mobile n’est pas disponible et transfère automatiquement l’appel vers la messagerie vocale de l’organisation. Si aucune réponse n’est reçue avant l’intervalle de temps soit atteint, l’appel se poursuit.</p>
<p>La valeur par défaut est 1500 millisecondes.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte client Skype Entreprise Online dont la stratégie voix doit être modifiée. Exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>Facultatif</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>Les valeurs autorisées sont les suivantes :</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>La valeur par défaut est OnPrem.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Accepte l’entrée redirigée pour les objets de stratégie de voix.

## Types de retours

Cette applet de commande ne retourne ni valeur, ni objet. Au lieu de cela, elle configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Voir aussi

#### Autres ressources

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

