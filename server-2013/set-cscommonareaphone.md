---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398579(v=OCS.15)
ms:contentKeyID: 49297756
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les valeurs de propriété d’un téléphone de partie commune géré par Lync Server. Les téléphones de partie commune sont des téléphones qui se trouvent dans les halls d’accueil des immeubles, dans des espaces réservés aux employés ou d’autres zones où ils sont susceptibles de servir à plusieurs personnes et pour des usages différents. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 modifie le nom complet Active Directory du téléphone de partie commune dont le numéro est 1-425-555-6710. Pour ce faire, l’applet de commande **Get-CsCommonAreaPhone** est d’abord appelée avec le paramètre Filter ; la valeur de filtre {LineUri -eq "tel:+14255556710"} limite les données retournées au téléphone de partie commune dont la propriété LineUri est égale à tel:+14255556710. L’objet retourné est ensuite redirigé vers l’applet de commande **Set-CsCommonAreaPhone** qui définit la valeur de la propriété DisplayName sur « Employee Lounge ».

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## EXEMPLE 2

La commande illustrée dans l’exemple 2 active tous les téléphones de partie commune actuellement configurés dans l’organisation. Pour effectuer cette tâche, la commande appelle l’applet de commande **Get-CsCommonAreaPhone** sans aucun paramètre afin de retourner une collection contenant tous les téléphones de partie commune. Cette collection est ensuite redirigée vers l’applet de commande **Set-CsCommonAreaPhone** qui prend chaque élément dans la collection et définit la propriété Enabled sur True.

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## EXEMPLE 3

La commande de l’exemple 3 ajoute une description générique à tous les téléphones de partie commune pour lesquels aucune valeur n’est attribuée à la propriété Description. Pour ce faire, l’applet de commande **Get-CsCommonAreaPhone** est d’abord appelée avec le paramètre Filter ; la valeur de filtre {Description -eq $Null} garantit que les seuls éléments retournés correspondent à des téléphones de partie commune dont la propriété Description est égale à une valeur null. Cette collection filtrée est ensuite redirigée vers l’applet de commande **Set-CsCommonAreaPhone** qui attribue la description générique « Common area phone » (téléphone de partie commune) à chaque élément au sein de la collection.

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## Description détaillée

Les téléphones de partie commune sont des téléphones IP qui ne sont pas associés à un utilisateur individuel. Ils ne sont pas confinés au bureau d’une seule et unique personne mais généralement installés dans des halls d’accueil, des cafétérias, des espaces réservés aux employés, des salles de réunion et d’autres lieux où plusieurs personnes peuvent se rassembler et se retrouver. Pour les administrateurs, cette situation pose un défi en matière de gestion ; ceci parce que l’usage d’un téléphone dans Lync Server est généralement soumis à des stratégies de voix et des plans de numérotation qui sont attribués à des utilisateurs individuels. Aucun utilisateur individuel n’est affecté aux téléphones de partie commune.

Une solution à ce défi consiste à créer des objets contact Active Directory pour l’ensemble de vos téléphones de partie commune. (Ces objets contact peuvent être créés à l’aide de l’applet de commande **New-CsCommonAreaPhone**. À l’instar des comptes d’utilisateur, des stratégies et des plans de numérotation peuvent être attribués à des objets contact. Vous pourrez par conséquent garder le contrôle de vos téléphones de partie commune même s’ils ne sont pas associés à un utilisateur individuel. Par exemple, si vous ne souhaitez pas que des gens puissent transférer ou parquer des appels à partir d’un téléphone de partie commune, vous pouvez créer une stratégie de voix pour empêcher tout transfert ou parcage des appels, puis attribuer cette stratégie au téléphone de partie commune. (Ou, plus précisément, à l’objet contact qui représente ce dernier.) Cette commande attribue la stratégie de voix CommonAreaPhoneVoicePolicy à tous vos téléphones de partie commune :

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

L’applet de commande **Set-CsCommonAreaPhone** vous offre la possibilité de modifier les propriétés des objets contact associés à des téléphones de partie commune. Vous pouvez notamment modifier le nom complet Active Directory du contact ou l’URI (Uniform Resource Identifier) de ligne associée au téléphone. Vous pouvez aussi vous servir du paramètre Enabled pour activer et désactiver le compte utilisé dans Lync Server.

En outre, vous pouvez configurer la fonctionnalité téléphone « rouge » pour les téléphones de partie commune à l’aide des applets de commande CsClientPolicy. Lorsqu’un téléphone sert de téléphone « rouge », les utilisateurs peuvent se connecter à ce téléphone à l’aide de leurs informations d’identification Lync Server. Cela permet notamment aux utilisateurs d’accéder facilement à leurs contacts. Pour plus d’informations, consultez la rubrique d’aide relative à l’applet de commande [Set-CsClientPolicy](set-csclientpolicy.md).

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsCommonAreaPhone** : RTCUniversalUserAdmins. Les autorisations d’exécuter cette applet de commande pour des sites spécifiques ou des unités d’organisation Active Directory spécifiques peuvent être attribuées au moyen de l’applet de commande **Grant-CsOUPermission**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p>Identificateur unique du téléphone de partie commune. Les téléphones de partie commune sont identifiés à l’aide du nom unique Active Directory de l’objet contact associé. Ils utilisent par défaut un identificateur global unique (GUID) comme nom commun et affichent donc généralement une valeur Identity (identité) semblable à la suivante : CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Pour cette raison, il vous paraîtra peut-être plus simple d’extraire des téléphones de partie commune à l’aide de l’applet de commande <strong>Get-CsCommonAreaPhone</strong>, puis en redirigeant les objets retournés vers l’applet de commande <strong>Set-CsCommonAreaPhone</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Permet de modifier un attribut de description Active Directory pour le téléphone de partie commune. Cette option offre un moyen de fournir des informations supplémentaires concernant le téléphone. Par exemple, vous pouvez apporter des détails sur la personne à contacter en cas de problèmes avec le téléphone.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Permet de modifier le nom complet Active Directory du téléphone de partie commune.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Numéro de téléphone tel qu’il est affiché dans Lync. La propriété DisplayNumber peut prendre le format que vous souhaitez, par exemple 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234, et ainsi de suite. Lors du choix d’un numéro complet, n’oubliez pas que celui-ci sera affiché sur l’écran du téléphone de partie commune seulement s’il peut être normalisé. (La normalisation est le processus de traduction de chaînes de numéros en un format de numéro de téléphone standard.) S’il n’existe pas de règle de normalisation pour le format de numéro de téléphone utilisé lors de la configuration du numéro complet, l’écran du téléphone de partie commune affichera la valeur de la propriété LineUri plutôt que la valeur de la propriété DisplayNumber.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Fqdn</p></td>
<td><p>Permet de se connecter au contrôleur de domaine spécifié afin de modifier des informations de contact. Pour vous connecter à un contrôleur de domaine spécifique, incluez le paramètre DomainController suivi du nom de l’ordinateur (par exemple, atl-mcs-001) ou de son nom de domaine complet ; par exemple : atl-mcs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si l’objet contact du téléphone de partie commune a été activé ou non pour Lync Server.</p>
<p>Si vous désactivez un contact à l’aide du paramètre Enabled, les informations associées à ce compte (notamment les stratégies attribuées et l’activation/désactivation du contact pour Voix Entreprise, le contrôle d’appels distants et/ou l’intégration de la messagerie vocale) sont conservées. Si, par la suite, vous réactivez le compte en utilisant le paramètre Enabled, les informations associées à ce compte seront restaurées.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Indique si l’objet contact du téléphone de partie commune a été activé pour Voix Entreprise, la solution de protocole VoIP (Voice over Internet Protocol) proposée par Microsoft. Avec Voix Entreprise, les utilisateurs peuvent passer des appels téléphoniques via Internet au lieu d’utiliser le réseau téléphonique standard.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indique où les sessions de messagerie instantanée des contacts sont archivées. Les valeurs autorisées sont les suivantes :</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Numéro téléphonique du téléphone de partie commune. L’URI (Uniform Resource Identifier) de la ligne doit être précisée au format E.164 et munie du préfixe « TEL: » . Par exemple : TEL:+14255551297. Tout numéro de poste doit être ajouté à la fin de l’URI de ligne ; par exemple : TEL:+14255551297; ext=51297.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Retourne un objet représentant le téléphone de partie commune.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identificateur unique permettant au téléphone de partie commune de communiquer avec des périphériques SIP, tels que Lync. L’adresse SIP doit être précédée du préfixe sip: et inclure un domaine SIP valide. Par exemple : sip:bldg14lobby@litwareinc.com.</p>
<p></p></td>
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

Objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Types de retours

Par défaut, l’applet de commande **Set-CsCommonAreaPhone** ne retourne ni objet, ni valeur. Toutefois, si vous incluez le paramètre PassThru, l’applet de commande retourne des instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Voir aussi

#### Autres ressources

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

