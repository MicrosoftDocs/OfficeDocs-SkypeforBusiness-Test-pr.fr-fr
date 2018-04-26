---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412944(v=OCS.15)
ms:contentKeyID: 49298747
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un objet contact Standard automatique ou Accès abonné existant pour le service de messagerie unifiée Exchange hébergé. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple définit sur True la propriété AutoAttendant du contact de messagerie unifiée Exchange avec l’adresse SIP exumsa4@fabrikam.com. Il nous faut d’abord appeler l’applet de commande **Get-CsExUmContact** pour récupérer l’objet de contact. (Nous aurions pu utiliser le nom complet Active Directory du contact, son nom d’utilisateur principal ou son nom d’ouverture de session.) Cette commande récupère le contact pertinent avec l’identité fournie. Ce contact est ensuite transmis à l’applet de commande **Set-CsExUmContact** pour laquelle nous avons défini le paramètre AutoAttendant sur True.

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## EXEMPLE 2

Cet exemple est identique à l’exemple 1 mais au lieu de récupérer le contact en appelant l’applet de commande **Get-CsExUmContact**, puis en redirigeant cet objet vers l’applet de commande **Set-CsExUmContact**, nous allons préciser à l’applet de commande **Set-CsExUmContact** l’identité du contact à modifier. Notez le format de l’identité : dans ce cas, nous avons utilisé le nom unique complet de l’objet de contact qui comprend un GUID généré automatiquement lors de la création du contact. Il nous faut ensuite définir le paramètre AutoAttendant du contact sur True.

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## Description détaillée

Lync Server agit de concert avec la messagerie unifiée Exchange pour fournir plusieurs fonctionnalités vocales dont Standard automatique et Accès abonné. Lorsque la messagerie unifiée Exchange est fournie en tant que service hébergé (plutôt que local), des objets contact doivent être créés à l’aide de Windows PowerShell pour appliquer les fonctionnalités Standard automatique et Accès abonné. Ces objets sont créés en appelant l’applet de commande **New-CsExUmContact** et peuvent être modifiés par la suite à l’aide de l’applet de commande **Set-CsExUmContact**.

Le moyen le plus simple d’utiliser cette applet de commande est souvent d’appeler d’abord l’applet de commande **Get-CsExUmContact** pour récupérer une instance de l’objet de contact que vous souhaitez modifier. Redirigez simplement le résultat de l’applet de commande **Get-CsExUmContact** vers l’applet de commande **Set-CsExUmContact** et affectez des valeurs aux paramètres pour les propriétés que vous souhaitez modifier. (Pour plus d’informations, consultez la section Exemples de cette rubrique.) Vous pouvez également appeler l’applet de commande **Set-CsExUmContact** en lui transmettant l’identité de l’objet de contact à modifier.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsExUmContact** : RTCUniversalUserAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>Identificateur unique de l’objet contact que vous souhaitez modifier. Les identités de contact peuvent être spécifiées dans l’un des quatre formats suivants : 1) l’adresse SIP du contact ; 2) le nom d’utilisateur principal (UPN) du contact ; 3) le nom de domaine et le nom d’ouverture de session du contact, sous la forme domaine\ouverture de session (par exemple, litwareinc\exum1) ; et 4) le nom complet Active Directory du contact (par exemple, Standard automatique d’équipe).</p>
<p>Type de données complet : Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Définissez le paramètre sur True si l’objet de contact est un standard automatique. Ce paramètre a la valeur False par défaut.</p></td>
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
<td><p>Chaîne</p></td>
<td><p>Description de ce contact. La description permet aux administrateurs d’identifier le type de contact (Standard automatique ou Accès abonné), l’emplacement, le fournisseur ou toute autre information qui identifiera l’objectif de chaque contact de messagerie unifiée Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Numéro de téléphone du contact. Les numéros affichés pour chaque contact doivent être unique (deux contacts messagerie unifiée Exchange ne peuvent pas avoir le même numéro de téléphone affiché). Toute modification de cette valeur entraînera aussi une modification de la valeur de la propriété LineURI.</p>
<p>Cette valeur peut commencer par un signe plus (+) et contenir autant de chiffres que nécessaire. Le premier chiffre doit être différent de zéro.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Fqdn</p></td>
<td><p>Permet de spécifier un contrôleur de domaine. Si aucun contrôleur de domaine n’est spécifié, le système utilisera le premier disponible.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Indique si le contact a été activé pour Lync Server. Si vous définissez ce paramètre sur False, le contact sera désactivé et le standard automatique ou l’accès abonné qui lui est associé ne fonctionnera plus.</p>
<p>Si vous désactivez un compte au moyen du paramètre Enabled, les informations associées à ce compte (y compris les stratégies de messagerie vocale hébergée) sont conservées. Si, par la suite, vous réactivez le compte à l’aide du paramètre Enabled, les informations de compte associées seront restaurées.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Indique si le contact a été activé pour Voix Entreprise. Si vous définissez cette valeur sur False, le standard automatique ou l’accès abonné associé à ce contact ne sera plus disponible.</p></td>
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
<td><p><em>PassThru</em></p></td>
<td><p>Facultatif</p></td>
<td><p>witchParameter</p></td>
<td><p>Retourne les résultats de la commande. Par défaut, cette applet de commande ne génère aucune sortie.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Adresse SIP du contact. Il doit s’agir d’une nouvelle adresse qui n’existe pas encore comme utilisateur ou contact dans services de domaine Active Directory.</p>
<p>Toute modification de cette valeur modifie également l’adresse SIP stockée dans la propriété OtherIpPhone.</p>
<p>La valeur SipAddress peut servir d’identité permettant aux commandes de l’applet de commande <strong>Get-CsExUmContact</strong> d’extraire des contacts spécifiques. Lors de l’appel de cette applet de commande, la nouvelle valeur SipAddress sera utilisée ; les requêtes de l’ancienne adresse SIP ne renverront aucun objet.</p></td>
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

Objet Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Accepte l’entrée redirigée pour les objets contact de messagerie unifiée Exchange.

## Types de retours

Cette applet de commande modifie un objet de type Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Si le paramètre PassThru est utilisé, elle renvoie également un objet de même type.

## Voir aussi

#### Autres ressources

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

