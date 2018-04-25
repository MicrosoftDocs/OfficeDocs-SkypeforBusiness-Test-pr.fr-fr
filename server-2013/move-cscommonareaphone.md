---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412837(v=OCS.15)
ms:contentKeyID: 49298525
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**Dernière rubrique modifiée :** 2015-04-02_

Déplace un ou plusieurs téléphones de partie commune vers un nouveau pool de serveurs d’inscriptions. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 déplace le téléphone de partie commune dont l’identité est CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com vers le pool de serveurs d’inscriptions atl-cs-001.litwareinc.com.

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## EXEMPLE 2

Dans l’exemple 2, le téléphone de partie commune dont le nom complet Active Directory est « Building 31 Cafeteria » est déplacé vers le pool de serveurs d’inscriptions atl-cs-001.litwareinc.com. Pour ce faire, l’applet de commande **Get-CsCommonAreaPhone** est d’abord appelée sans aucun paramètre, afin de retourner une collection de tous les téléphones de partie commune actuellement utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui choisit uniquement les téléphones dont l’attribut DisplayName est égal à « Building 31 Cafeteria ». La collection filtrée est ensuite redirigée vers l’applet de commande **Move-CsCommonAreaPhone**, qui déplace chaque téléphone de la collection vers atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## EXEMPLE 3

L’exemple 3 déplace tous les téléphones de partie commune actuellement hébergés sur le pool de serveurs d’inscriptions dublin-cs-001.litwareinc.com vers le pool de serveurs d’inscriptions atl-cs-001.litwareinc.com. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsCommonAreaPhone** sans paramètre ; cet appel retourne la collection de tous les téléphones de partie commune configurés pour être utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object**, qui choisit tous les téléphones de partie commune dont la propriété RegistrarPool est égale à dublin-cs-001.litwareinc.com. Cette collection est ensuite redirigée vers l’applet de commande **Move-CsCommonAreaPhone**, qui déplace chaque téléphone de la collection vers le nouveau pool de serveurs d’inscriptions atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## EXEMPLE 4

L’exemple 4 est une variante de la commande de l’exemple 3. Dans ce cas toutefois, les téléphones de partie commune ne sont pas uniquement déplacés vers un nouveau pool de serveurs d’inscriptions, mais ils se voient également attribuer une nouvelle stratégie de voix utilisateur. Pour cela, le paramètre PassThru est inclus lors de l’appel de l’applet de commande **Move-CsCommonAreaPhone** afin que les objets de téléphone de partie commune puissent être transmis via le pipeline. (Par défaut, l’applet de commande **Move-CsCommonAreaPhone** ne transmet aucun objet via le pipeline.) Une fois les téléphones déplacés, les objets de téléphone sont redirigés vers l’applet de commande **Grant-CsVoicePolicy**, qui attribue la stratégie de voix AtlantaVoicePolicy à chacun des téléphones déplacés.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## Description détaillée

Les téléphones de partie commune sont des téléphones IP qui ne sont pas associés à un utilisateur individuel. Ils ne sont pas confinés au bureau d’une seule et unique personne mais généralement installés dans des halls d’accueil, des cafétérias, des espaces réservés aux employés, des salles de réunion et d’autres lieux où plusieurs personnes peuvent se rassembler et se retrouver. Pour les administrateurs, cette situation pose un défi en matière de gestion ; ceci parce que l’usage d’un téléphone dans Lync Server est généralement soumis à des stratégies de voix et des plans de numérotation qui sont attribués à des utilisateurs individuels. Aucun utilisateur individuel n’est affecté aux téléphones de partie commune.

La solution à ce défi consiste à créer des objets contact Active Directory pour l’ensemble de vos téléphones de partie commune. (Ces objets contact peuvent être créés à l’aide de l’applet de commande **New-CsCommonAreaPhone**.) À l’instar des comptes d’utilisateur, des stratégies et des plans de numérotation peuvent être attribués à des objets contact. Vous pourrez par conséquent garder le contrôle de vos téléphones de partie commune, même s’ils ne sont pas associés à un utilisateur individuel. Par exemple, si vous ne souhaitez pas que des gens puissent transférer ou parquer des appels à partir d’un téléphone de partie commune, vous pouvez créer une stratégie de voix pour empêcher tout transfert ou parcage des appels, puis attribuer cette stratégie au téléphone de partie commune. (ou, plus précisément, à l’objet contact qui représente ce dernier).

L’applet de commande **Move-CsCommonAreaPhone** vous permet de déplacer un téléphone de partie commune vers un nouveau pool de serveurs d’inscriptions.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Move-CsCommonAreaPhone** : RTCUniversalUserAdmins. Les autorisations d’exécuter cette applet de commande pour des sites spécifiques ou des unités d’organisation Active Directory spécifiques peuvent être attribuées au moyen de l’applet de commande **Grant-CsOUPermission**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificateur unique du téléphone de partie commune. Les téléphones de partie commune sont identifiés à l’aide du nom unique Active Directory de l’objet contact associé. Par défaut, les téléphones de partie commune utilisent un identificateur global unique (GUID) comme nom commun et ont donc généralement un identificateur similaire à celui-ci : CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FDQN) du pool de serveurs d’inscriptions vers lequel le téléphone de partie commune doit être déplacé, par exemple : atl-cs-001.litwareinc.com. En plus du pool de serveurs d’inscriptions, la cible peut également être le nom de domaine complet d’un fournisseur d’hébergement.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Permet de vous connecter au contrôleur de domaine spécifié afin de déplacer le téléphone de partie commune. Pour vous connecter à un contrôleur de domaine spécifique, incluez le paramètre DomainController suivi du nom de l’ordinateur (par exemple, atl-cs-001) ou de son nom de domaine complet (par exemple, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, il déplace le téléphone de partie commune, mais supprime toutes les données associées (telles que les stratégies qui ont été attribuées au périphérique). S’il est absent, le téléphone est déplacé avec toutes les données associées.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Lorsque ce paramètre est présent, il oblige l’ordinateur à ignorer toutes les erreurs pouvant se produire avec la base de données principale et essaie de déplacer le téléphone de partie commune malgré ces erreurs.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Permet de transmettre un objet utilisateur via le pipeline qui représente le compte d’utilisateur déplacé. Par défaut, l’applet de commande <strong>Move-CsCommonAreaPhone</strong> ne transmet aucun objet via le pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Ce paramètre est utilisé uniquement pour Lync Online. Il ne doit pas être utilisé avec une implémentation locale de Lync Server.</p></td>
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

Chaîne. L’applet de commande **Move-CsCommonAreaPhone** accepte une valeur de chaîne transmise par pipeline représentant l’identité du téléphone de partie commune.

## Types de retours

Par défaut, l’applet de commande **Move-CsCommonAreaPhone** ne retourne ni objet, ni valeur. Toutefois, si vous incluez le paramètre PassThru, l’applet de commande retourne des instances de l’objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Voir aussi

#### Autres ressources

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

