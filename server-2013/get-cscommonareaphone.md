---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412934(v=OCS.15)
ms:contentKeyID: 49298701
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les téléphones de partie commune gérés par Lync Server. Les téléphones de partie commune sont des téléphones situés dans les halls d’accueil des immeubles, les espaces réservés aux employés ou d’autres zones où ils sont susceptibles de servir à plusieurs personnes et pour des usages différents. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 retourne des informations sur tous les téléphones de partie commune configurés pour être utilisés dans l’organisation. Cette opération s’effectue en appelant l’applet de commande **Get-CsCommonAreaPhone** sans aucun paramètre.

    Get-CsCommonAreaPhone

## EXEMPLE 2

Dans l’exemple 2, le téléphone de partie commune dont le nom complet Active Directory est « Building 14 Lobby » (Hall, Bâtiment 14) est retourné. Cette tâche s’effectue en incluant le paramètre Filter et la valeur de filtre {DisplayName -eq "Building 14 Lobby"} ; cette valeur de filtre limite les objets retournés aux téléphones de partie commune pour lesquels la propriété DisplayName est égale à « Building 14 Lobby ».

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## EXEMPLE 3

L’exemple 3 retourne tous les téléphones de partie commune dont le nom complet Active Directory commence par les caractères « Building 14 ». Pour ce faire, le système appelle l’applet de commande **Get-CsCommonAreaPhone** avec le paramètre Filter et la valeur de filtre {DisplayName -like "Building 14\*"}. La valeur de filtre utilise l’opérateur -like et la chaîne à caractère générique « Building 14\* » pour limiter les données retournées aux téléphones dont la propriété DisplayName commence par « Building 14 » (par exemple, « Building 14 Lobby », « Building 14 Cafeteria », etc.).

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## EXEMPLE 4

Dans l’exemple 4, un seul téléphone de partie commune est retourné : le téléphone dont la propriété LineUri est égale à « tel:+14255551234 ». Comme ces URI de ligne doivent être uniques, cette commande ne retourne jamais plusieurs éléments.

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## EXEMPLE 5

La commande de l’exemple 5 retourne des informations sur tous les téléphones de partie commune auxquels aucun plan de numérotation n’a été attribué. Cette tâche s’effectue en utilisant le paramètre Filter et la valeur de filtre {DialPlan -eq $Null} ; elle limite les données retournées aux téléphones dont la propriété DialPlan a une valeur Null. Si un téléphone de partie commune ne s’est pas vu explicitement attribuer un plan de numérotation, il utilise alors automatiquement le plan de numérotation global ou, le cas échéant, le plan attribué au site.

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## EXEMPLE 6

L’exemple 6 retourne la collection de tous les téléphones de partie commune ayant un objet contact au sein de l’unité d’organisation Telecommunications dans services de domaine Active Directory. Pour ce faire, le système appelle l’applet de commande **Get-CsCommonAreaPhone** avec le paramètre OU ; la valeur de paramètre limite les objets retournés aux téléphones ayant des objets contact dans l’unité d’organisation dont le nom unique est ou=Telecommunications,dc=litwareinc,dc=com.

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## Description détaillée

Les téléphones de partie commune sont des téléphones IP qui ne sont pas associés à un utilisateur individuel. Ils ne sont pas confinés au bureau d’une seule et unique personne mais généralement installés dans des halls d’accueil, des cafétérias, des espaces réservés aux employés, des salles de réunion et d’autres lieux où plusieurs personnes peuvent se rassembler et se retrouver. Pour les administrateurs, cette situation pose un défi en matière de gestion ; ceci parce que l’usage d’un téléphone dans Lync Server est généralement soumis à des stratégies de voix et des plans de numérotation qui sont attribués à des utilisateurs individuels. Aucun utilisateur individuel n’est affecté aux téléphones de partie commune.

La solution à ce défi consiste à créer des objets contact Active Directory pour l’ensemble de vos téléphones de partie commune. (Ces objets contact peuvent être créés à l’aide de l’applet de commande **New-CsCommonAreaPhone**.) À l’instar des comptes d’utilisateur, des stratégies et des plans de numérotation peuvent être attribués à des objets contact. Vous pourrez par conséquent garder le contrôle de vos téléphones de partie commune, même s’ils ne sont pas associés à un utilisateur individuel. Par exemple, si vous ne souhaitez pas que des gens puissent transférer ou parquer des appels à partir d’un téléphone de partie commune, vous pouvez créer une stratégie de voix pour empêcher tout transfert ou parcage des appels, puis attribuer cette stratégie au téléphone de partie commune. (ou, plus précisément, à l’objet contact qui représente ce dernier). Par exemple, cette commande attribue la stratégie de voix CommonAreaPhoneVoicePolicy à tous vos téléphones de partie commune :

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

L’applet de commande **Get-CsCommonAreaPhone** permet de récupérer des informations sur les téléphones de partie commune configurés pour être utilisés au sein de votre organisation. Si vous appelez l’applet de commande **Get-CsCommonAreaPhone** sans aucun paramètre, l’applet de commande retournera des informations sur tous vos téléphones de partie commune. Des paramètres facultatifs offrent différents moyens de filtrer les informations ; par exemple, vous pouvez retourner tous les téléphones de partie commune qui ont des objets contact dans une unité d’organisation (OU) spécifiée ou tous les objets contact situés dans un bâtiment donné.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsCommonAreaPhone** : RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Les autorisations d’exécuter cette applet de commande pour des sites spécifiques ou des unités d’organisation Active Directory spécifiques peuvent être attribuées au moyen de l’applet de commande **Grant-CsOUPermission**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p><em>Credential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Permet d’exécuter l’applet de commande <strong>Get-CsCommonAreaPhone</strong> avec d’autres informations d’identification. Ceci peut être requis si le compte que vous avez utilisé pour vous connecter à Windows ne dispose pas des privilèges nécessaires pour manipuler les objets contact.</p>
<p>Pour utiliser le paramètre Credential, vous devez d’abord créer un objet PSCredential à l’aide de l’applet de commande <strong>Get-Credential</strong>. Pour plus d’informations, consultez la rubrique d’aide relative à l’applet de commande <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Permet de vous connecter au contrôleur de domaine spécifié, afin de récupérer des informations de contact. Pour vous connecter à un contrôleur de domaine spécifique, incluez le paramètre DomainController suivi du nom de domaine complet (FQDN) de cet ordinateur (par exemple, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet de limiter les données retournées en filtrant les attributs spécifiques de Lync Server. Par exemple, vous pouvez limiter les données retournées aux objets contact de téléphone de partie commune auxquels une stratégie de voix spécifique a été attribuée ou aux contacts auxquels aucune stratégie de voix spécifique n’a été attribuée.</p>
<p>Le paramètre Filter utilise la même syntaxe de filtrage Windows PowerShell que celle employée par l’applet de commande <strong>Where-Object</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificateur unique du téléphone de partie commune. Les téléphones de partie commune sont identifiés à l’aide du nom unique Active Directory de l’objet contact associé. Par défaut, les téléphones de partie commune utilisent un identificateur global unique (GUID) comme nom commun et ont donc généralement un identificateur similaire à celui-ci : CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de limiter les données retournées en filtrant les attributs Active Directory génériques (c’est-à-dire les attributs qui ne sont pas spécifiques à Lync Server). Ainsi, vous pouvez limiter les données retournées aux objets contact attribués à un service spécifique, ou encore situés dans un bâtiment en particulier.</p>
<p>Le paramètre LdapFilter utilise le langage de requête LDAP lors de la création des filtres. Par exemple, un filtre qui retourne uniquement les objets contact représentant les téléphones de partie commune dans la ville de Redmond se présente comme suit :</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>Dans le filtre ci-dessus, « l » (L minuscule) correspond à l’attribut Active Directory (locality, ou ville), « = » correspond à l’opérateur de comparaison (égal à) et « Redmond » correspond à la valeur de filtre.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Permet de retourner les objets contact à partir d’une unité d’organisation (OU) Active Directory spécifique. Le paramètre OU retourne les données provenant de l’unité d’organisation (OU) spécifiée et de toutes ses unités d’organisation enfants. Par exemple, si l’unité d’organisation Finance a deux unités d’organisation enfants, AccountsPayable et AccountsReceivable, les informations de téléphone de partie commune seront retournées depuis chacune de ces unités d’organisation.</p>
<p>Lors de la spécification d’une unité d’organisation, utilisez le nom unique de ce conteneur, par exemple : -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Permet de limiter le nombre d’enregistrements retournés par une commande. Par exemple, pour retourner sept téléphones de partie commune (quel que soit le nombre de téléphones de partie commune présents dans votre forêt), incluez le paramètre ResultSize et définissez sa valeur à 7. Notez qu’il est impossible de savoir quels seront les sept téléphones de partie commune retournés. Si vous définissez ResultSize à 7, mais que votre forêt ne compte que trois téléphones de partie commune, la commande renverra ces trois téléphones et se terminera sans erreur.</p>
<p>La taille des résultats peut être définie sur n’importe quel entier compris entre 0 et 2147483647 (inclus). Si le paramètre est défini sur 0, la commande sera exécutée, mais aucune donnée ne sera retournée.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Chaîne. L’applet de commande **Get-CsCommonAreaPhone** accepte une valeur de chaîne transmise par pipeline représentant l’identité du téléphone de partie commune.

## Types de retours

L’applet de commande **Get-CsCommonAreaPhone** retourne des instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Voir aussi

#### Autres ressources

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

