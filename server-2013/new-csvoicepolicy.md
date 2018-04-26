---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425856(v=OCS.15)
ms:contentKeyID: 49296880
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une nouvelle stratégie de voix. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple crée une nouvelle stratégie vocale par utilisateur avec des paramètres par défaut, dont l’identité est UserVoicePolicy1.

    New-CsVoicePolicy -Identity UserVoicePolicy1

## EXEMPLE 2

Cet exemple crée une nouvelle stratégie de voix utilisateur avec une valeur Identity « UserVoicePolicy2 » et définit la propriété AllowSimulRing sur False. Cela signifie que tous les utilisateurs auxquels cette stratégie est affectée ne sont pas activés pour la sonnerie simultanée, fonction qui détermine si un deuxième téléphone (comme un téléphone mobile) peut être défini pour sonner à chaque fois que le téléphone de bureau de l’utilisateur sonne. Cette commande ajoute également la valeur « Local » à la liste des utilisations du réseau PSTN en associant cette stratégie à un itinéraire vocal qui utilise également le réseau PSTN local. (Notez que le paramètre Identity n’est pas spécifié explicitement. Le paramètre Identity est un paramètre positionnel. Par conséquent, si vous spécifiez d’abord la valeur d’identité dans la liste des paramètres, vous ne devez pas indiquer explicitement qu’il s’agit de la valeur Identity.)

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## EXEMPLE 3

Cet exemple crée une nouvelle stratégie de voix pour le site Redmond et applique à cette stratégie toutes les utilisations PSTN définies pour l’organisation. La première ligne de cet exemple appelle l’applet de commande **Get-CsPstnUsage** pour récupérer l’ensemble global des utilisations du réseau PSTN de l’organisation, puis l’enregistrer dans la variable $a. La deuxième ligne appelle l’applet de commande **New-CsVoicePolicy** afin de créer la nouvelle stratégie de voix pour le site Redmond. Une valeur est affectée au paramètre PstnUsages pour ajouter la liste contenue dans l’ensemble global des utilisations PSTN à cette stratégie. Veuillez noter la syntaxe de la valeur ajoutée : $a.Usage. Cela fait référence à la propriété Usage des paramètres d’utilisation du réseau PSTN qui contient la liste des utilisations du réseau.

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## Description détaillée

Cette applet de commande crée une nouvelle stratégie de voix. Les stratégies de voix permettent de gérer les fonctionnalités Voix Entreprise comme la sonnerie simultanée (possibilité d’avoir une deuxième sonnerie de téléphone chaque fois que quelqu’un appelle sur votre téléphone professionnel) et le transfert d’appel. La stratégie créée par cette applet de commande détermine si un grand nombre de ces fonctions sont activées ou désactivées.

Personnes autorisées à exécuter cette applet de commande : par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsVoicePolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p>Identificateur unique spécifiant l’étendue ou le nom de la stratégie. Les valeurs valides pour l’applet de commande sont site:&lt;nom site&gt; (où &lt;nom du site&gt; est le nom du site Lync Server auquel s’applique la stratégie, par exemple, site:Redmond), et une chaîne qui désigne une stratégie utilisateur, par exemple, RedmondVoicePolicy. Une stratégie globale existe par défaut.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Si ce paramètre a la valeur True, les appels peuvent être transférés. Si ce paramètre a la valeur False, les appels ne peuvent pas être transférés.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsque ce paramètre est défini sur True, les appels effectués vers des numéros internes sur un autre pool seront acheminés via le réseau téléphonique commuté lorsque le pool ou le WAN ne sont pas disponibles.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La sonnerie simultanée est une fonction qui permet de faire sonner plusieurs téléphones en composant un seul numéro. Définissez ce paramètre sur True pour activer cette fonction. Si ce paramètre est défini sur False, la sonnerie simultanée ne peut être configurée pour aucun utilisateur affecté à cette stratégie.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Facultatif</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Fournit un moyen aux administrateurs de gérer le transfert d’appel et la sonnerie simultanée. Les valeurs autorisées sont les suivantes :</p>
<p>* VoicePolicyUsage – La stratégie voix par défaut permet de gérer le transfert d’appel et la sonnerie simultanée sur tous les appels. Il s’agit de la valeur par défaut.</p>
<p>* InternalOnly – Le transfert d’appel et la sonnerie simultanée sont limités aux appels entre un utilisateur Lync et un autre utilisateur.</p>
<p>* CustomUsage – L’utilisation PSTN personnalisée permet de gérer le transfert d’appel et la sonnerie simultanée. Cet emploi doit être spécifié à l’aide du paramètre CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>L’utilisation PSTN personnalisée permet de gérer le transfert d’appel et la sonnerie simultanée. Pour ajouter une utilisation personnalisée à la stratégie de voix, utilisez la syntaxe suivante :</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Pour supprimer une utilisation personnalisée, utilisez la syntaxe suivante :</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Notez que l’utilisation doit exister avant de pouvoir être employée avec le paramètre CustomCallForwardingSimulRingUsages.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Description de la stratégie de voix.</p>
<p>Longueur maximale : 1040 caractères.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Il est possible de définir des stratégies pour gérer la configuration réseau, notamment pour limiter la largeur de bande. Définissez ce paramètre sur True pour autoriser le remplacement de ces stratégies. En d’autres termes, si ce paramètre est défini sur True, aucune vérification de bande passante ne se fera et les appels passeront indépendamment des paramètres de contrôle d’admission des appels (CAC).</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>L’application de parcage d’appel permet de mettre un appel en attente (ou encore de le parquer) sur un numéro particulier dans une plage de numéros en vue d’une récupération ultérieure. Définissez ce paramètre sur True pour activer l’application. Si ce paramètre est défini sur False, les utilisateurs affectés à cette stratégie ne pourront pas parquer les appels destinés à leur numéro de téléphone.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Détermine si les appels peuvent être transférés vers un autre numéro. Si ce paramètre est défini sur True, les appels peuvent être transférés ; si ce paramètre est défini sur False, les appels ne peuvent pas être transférés.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La délégation d’appels permet à un utilisateur de répondre ou de passer des appels pour un autre utilisateur. Par exemple, un responsable peut configurer la délégation d’appels pour que tous les appels entrants sonnent à la fois sur le téléphone du responsable et sur le téléphone d’un administrateur. Définissez ce paramètre sur True pour permettre aux utilisateurs disposant de cette stratégie de configurer la délégation d’appels. Définissez ce paramètre sur False pour désactiver la délégation d’appels.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Le suivi des appels malveillants est une norme permettant d’effectuer un suivi des appels qu’un utilisateur désigne comme malveillants. Ces appels peuvent être suivis même si l’ID d’appelant est bloqué. Le suivi est uniquement accessible aux responsables adéquats, pas à l’utilisateur. Définissez cette propriété sur True pour autoriser la mise en place du suivi des appels malveillants.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>L’appel d’équipe permet à un utilisateur de désigner un groupe d’autres utilisateurs dont les téléphones sonneront lorsqu’un appel sera adressé au numéro de cet utilisateur. Cette fonction est utile dans les équipes où, par exemple, tous les membres peuvent répondre aux appels entrants des clients. Définissez ce paramètre sur True pour activer cette fonction.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, les appels passés à un appareil mobile qui ne répond pas sont acheminés vers la boîte vocale de l’entreprise, et non vers celle du fournisseur de l’appareil mobile. S’il est répondu « trop tôt » à un appel (à savoir, avant que la valeur configurée pour la propriété PSTNVoicemailEscapeTimer se soit écoulée), l’appareil mobile est considéré comme indisponible et l’appel est transféré vers la boîte vocale de l’entreprise.</p>
<p>La valeur par défaut est False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom affichable décrivant cette stratégie.</p>
<p>Valeur par défaut : DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Les frais de réseau téléphonique commuté (PSTN) sont plus communément appelés des frais d’appel longue distance. Les organisations peuvent parfois éviter ces frais en implémentant une solution VoIP (Voice over Internet Protocol) qui permet aux succursales de se connecter via des appels réseau. Si vous définissez ce paramètre sur True, vos appels passeront par le réseau téléphonique commuté (PSTN) et impliqueront des frais, ce qui n’est pas le cas via le réseau.</p>
<p>Valeur par défaut : False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste des utilisations PSTN disponibles pour cette stratégie. Une utilisation PSTN lie une stratégie de voix à un itinéraire téléphonique.</p>
<p>Toute valeur de chaîne peut être placée dans cette liste, tant que la valeur existe dans la liste globale des utilisations PSTN. (Les chaînes dupliquées ne sont pas autorisées ; chaque chaîne doit être unique.) La liste des utilisations PSTN peut être récupérée en appelant l’applet de commande <strong>Get-CsPstnUsage</strong>.</p>
<p>Par défaut, cette liste est vide. Si vous ne fournissez pas de valeur pour ce paramètre, vous recevrez un message de mise en garde stipulant que les utilisateurs qui ont ratifié cette stratégie ne sont pas en mesure de passer des appels sortants via le réseau PSTN.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int64</p></td>
<td><p>Durée (en millisecondes) utilisée pour déterminer s’il a été répondu « trop tôt » à un appel. En cas de réception de la réponse au cours de cette durée, Lync Server présume que l’appareil mobile n’est pas disponible et bascule automatiquement l’appel sur la boîte vocale de l’organisation. Si aucune réponse n’est reçue avant que la durée ne se soit écoulée, l’appel est autorisé à se poursuivre. La valeur par défaut est 1500 millisecondes.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte client Skype Entreprise Online pour lequel la nouvelle stratégie de voix est créée. Exemple :</p>
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

Aucun.

## Types de retours

Cette applet de commande crée une instance de l’objet Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy.

## Voir aussi

#### Autres ressources

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

