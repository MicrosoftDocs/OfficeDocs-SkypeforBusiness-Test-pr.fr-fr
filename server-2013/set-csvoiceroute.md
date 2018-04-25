---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412893(v=OCS.15)
ms:contentKeyID: 49298618
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un itinéraire de communications vocales. Les itinéraires de communications vocales contiennent des instructions qui indiquent à Lync Server comment acheminer les appels des utilisateurs Voix Entreprise vers des numéros de téléphone sur le réseau téléphonique commuté (RTC) ou un autocommutateur privé (PBX). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cette commande définit la description de l’itinéraire de communications vocales Route1 sur « Test Route » (Itinéraire de test).

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## EXEMPLE 2

La commande présentée dans cet exemple modifie l’itinéraire de communications vocales avec l’identité Route1 pour ajouter l’utilisation PSTN « Long Distance » (Longue distance) à la liste des utilisations de l’itinéraire en question. « Long Distance » doit figurer dans la liste des utilisations PSTN globales (récupérable par appel de l’applet de commande **Get-CsPstnUsage**).

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## EXEMPLE 3

Cet exemple modifie l’itinéraire de communications vocales appelé Route1 et peuple la liste des utilisations PSTN de cet itinéraire avec toutes les utilisations existantes pour l’organisation. La première commande de cet exemple récupère la liste des utilisations PSTN globales. Veuillez noter que l’appel de l’applet de commande **Get-CsPstnUsage** apparaît entre parenthèses ; cela signifie que nous récupérons d’abord un objet contenant les informations d’utilisation PSTN. (Puisqu’il n’existe qu’une seule utilisation PSTN (globale), un seul objet sera récupéré.) La commande récupère ensuite la propriété Usage de cet objet. Cette propriété qui contient la liste des utilisations PSTN est affectée à la variable $x. Sur la deuxième ligne de cet exemple, l’applet de commande **Set-CsVoiceRoute** est appelée pour modifier l’itinéraire de communications vocales avec l’identité Route1. Veuillez noter la valeur transmise au paramètre PstnUsages : @{replace=$x}. Cette valeur permet de remplacer tous les éléments de la liste PstnUsages pour cet itinéraire par le contenu de $x, qui comporte la liste des utilisations PSTN récupérée à la ligne 1.

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## EXEMPLE 4

Cette série de commandes modifie la propriété Name de l’itinéraire de communications vocales et remplace son identité Route1 par RouteA. Toute modification automatique de la propriété Name modifie également la propriété Identity qui devient RouteA dans ce cas précis.

Sur la première ligne, l’applet de commande **Get-CsVoiceRoute** est appelée dans le but de récupérer l’itinéraire de communications vocales avec l’identité Route1. L’objet renvoyé est stocké dans la variable $x, puis la valeur de chaîne « RouteA » est affectée à la propriété Name de cet objet. Enfin, l’objet (stocké dans la variable $x) est transmis au paramètre d’instance de l’applet de commande **Set-CsVoiceRoute** pour effectuer la modification.

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## EXEMPLE 5

Cet exemple modifie l’itinéraire de communications vocales appelé Route1 et remplit la liste des passerelles PSTN (PstnGatewayList) de cet itinéraire avec le rôle serveur de la passerelle dont l’identité est PstnGateway:192.168.0.100. Dans la première ligne de cet exemple, l’applet de commande **Get-CsVoiceRoute** est appelé afin de récupérer l’itinéraire de communications vocales que nous cherchons à modifier, soit dans le cas présent Route1. La méthode Add dans la propriété PstnGatewayList de l’itinéraire Route1 est alors appelée. Cette méthode est transmise au paramètre Identity (identité) du service à ajouter. Pour finir, il nous suffit d’appeler l’applet de commande **Set-CsVoiceRoute** et de transmettre le paramètre d’instance à la variable $y, ce qui permet de mettre à jour l’itinéraire Route1 (stocké dans $y) avec la passerelle PSTN récemment ajoutée.

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## Description détaillée

Cette applet de commande vous permet de modifier un itinéraire de communications vocales existant. Les itinéraires de communications vocales sont associés aux stratégies de voix par l’intermédiaire des utilisations du réseau téléphonique commuté (PSTN). Un itinéraire de communications vocales inclut une expression régulière identifiant les numéros de téléphone qui seront acheminés via un itinéraire de communications vocales donné : les numéros de téléphone qui correspondent à l’expression régulière seront acheminés via cet itinéraire.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoiceRoute** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p><em>AlternateCallerId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Si le paramètre SuppressCallerId est défini sur True, les destinataires visualiseront la valeur du paramètre AlternateCallerId à la place du numéro réel de l’appelant. Ce numéro doit être valide et peut être utilisé pour représenter une division au sein d’une organisation, comme le Support technique ou les Ressources humaines.</p>
<p>Si le paramètre SuppressCallerId est défini sur False, le paramètre AlternateCallerId est ignoré.</p>
<p>Cette valeur doit correspondre à l’expression régulière (\+)?[1-9]\d*(;ext=[1-9]\d*)?. En d’autres termes, la valeur peut commencer par un signe plus (+), sans que cela soit obligatoire ; elle peut comporter autant de chiffres que vous le souhaitez ; elle peut être suivie d’un numéro de poste qui commence par ;ext= suivi d’autant de chiffres que nécessaire. (Veuillez noter que si vous incluez un numéro de poste, la chaîne doit être placée entre guillemets.)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Description de la fonction de cet itinéraire téléphonique.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identité unique de l’itinéraire de communications vocales. (Si l’itinéraire de communications vocales contient un espace (par exemple, Itinéraire de test), vous devez mettre toute la chaîne entre parenthèses.)</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Itinéraire</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles. Cet objet doit être de type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route et peut être récupéré en appelant l’applet de commande <strong>Get-CsVoiceRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Expression régulière qui spécifie les numéros de téléphone auxquels cet itinéraire s’applique. Les numéros correspondant à ce modèle seront acheminés en fonction du reste des paramètres de routage. Par exemple, le modèle de numéro par défaut, [0-9]{10}, dévoile un numéro à dix chiffres allant de 0 à 9.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Un numéro peut aboutir à plusieurs itinéraires de communications vocales. La priorité détermine l’ordre dans lequel les itinéraires de communications vocales seront appliqués si plusieurs itinéraires sont possibles.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un serveur de médiation peut être associé à plusieurs passerelles. Ce paramètre contient une liste des passerelles associées à cet itinéraire de communications vocales. Chaque membre de cette liste doit correspondre à l’identité de service de la passerelle PSTN ou du serveur de médiation. La valeur peut concerner un serveur de médiation uniquement si le serveur de médiation est configuré pour Microsoft Office Communications Server 2007 ou Microsoft Office Communications Server 2007 R2. Une passerelle PSTN doit être utilisée pour Lync Server. L’identité de service est une chaîne au format « ServiceRole:FQDN » où ServiceRole désigne le nom du rôle de service (PSTNGateway) et FQDN correspond au nom de domaine complet du pool ou à l’adresse IP du serveur (par exemple, PSTNGateway:redmondpool.litwareinc.com). Vous pouvez extraire des identités de service en appelant la commande Get-CsService | Select-Object Identity.</p>
<p>Si vous apportez des modifications à un itinéraire de communications vocales et laissez la liste PstnGatewayList vide, ou si la modification que vous apportez supprime tous les éléments dans la liste, vous recevrez un message d’avertissement signalant que les utilisateurs ne pourront pas effectuer des appels PSTN.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Liste des utilisations PSTN (telles que Local ou Long Distance) pouvant être appliquées à cet itinéraire de communications vocales. L’utilisation PSTN doit être une utilisation existante. (Les utilisations PSTN peuvent être récupérées en appelant l’applet de commande <strong>Get-CsPstnUsage</strong>.)</p>
<p>Si vous apportez des modifications à un itinéraire de communications vocales et laissez la liste PstnUsages vide, ou si la modification que vous apportez supprime toutes les utilisations PSTN dans la liste, vous recevrez un message d’avertissement signalant que les utilisateurs ne pourront pas effectuer des appels PSTN.</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Détermine si l’ID d’un appelant sera affiché pour les appels sortants. Si ce paramètre est défini sur True, l’ID d’appelant sera supprimé. La valeur de AlternateCallerId apparaîtra à la place de l’ID. Lorsque SuppressCallerId est défini sur True, vous devez fournir une valeur pour AlternateCallerId.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route. L’applet de commande **Set-CsVoiceRoute** accepte l’entrée redirigée pour les objets d’itinéraires de communications vocales.

## Types de retours

L’applet de commande **Set-CsVoiceRoute** ne retourne ni valeur, ni objet. Au lieu de cela, l’applet de commande configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Voir aussi

#### Autres ressources

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

