---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399046(v=OCS.15)
ms:contentKeyID: 49299242
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**Dernière rubrique modifiée :** 2015-03-09_

Ajoute de nouvelles options aux stratégies de clients Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsClientPolicyEntry -Name <String> -Value <String>

## Exemples

## EXEMPLE 1

Les commandes présentées dans l’exemple 1 montrent comment une nouvelle entrée de stratégie peut être ajoutée à la stratégie globale de clients. Cet exemple ajoute une nouvelle option de commentaires à Lync. Notez que cet exemple est fourni uniquement à des fins de démonstration. Ne vous attendez pas à pouvoir exécuter ces commandes et ajouter une option de commentaires similaire à votre copie de Lync.

Pour ajouter la nouvelle entrée de stratégie, la première commande dans l’exemple utilise l’applet de commande **New-CsClientPolicyEntry** pour créer une entrée avec le nom OnlineFeedbackURL et la valeur http://www.litwareinc.com/feedback. L’objet d’entrée de stratégie qui en résulte est stocké dans une variable appelée $x.

Dans la deuxième commande, l’applet de commande **Get-CsClientPolicy** est utilisée pour créer une référence d’objet ($y) à la stratégie globale de clients. Une fois la référence d’objet créée, la méthode Add est utilisée pour ajouter la nouvelle entrée de stratégie à la propriété PolicyEntry. Si la propriété PolicyEntry est déjà munie d’une ou de plusieurs entrées, la nouvelle valeur sera simplement ajoutée à la fin de cette collection.

Enfin, la dernière commande de l’exemple utilise l’applet de commande **Set-CsClientPolicy** pour écrire ces modifications dans la stratégie globale proprement dite. Si vous n’appelez pas l’applet de commande **Set-CsClientPolicy**, vos modifications existeront en mémoire uniquement et disparaîtront au moment même où vous fermerez votre session Windows PowerShell ou supprimerez la variable $x.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## EXEMPLE 2

L’exemple 2 est une variante des commandes présentées dans l’exemple 1. En revanche, dans ce cas, la nouvelle entrée de stratégie remplace tous les éléments qui figurent actuellement dans la propriété PolicyEntry de la stratégie globale. Pour ce faire, la première commande dans l’exemple crée une nouvelle entrée de stratégie qui est stockée dans une variable appelée $x. La deuxième commande utilise ensuite l’applet de commande **Set-CsClientPolicy** pour définir la valeur de la propriété PolicyEntry sur $x. Une fois la commande terminée, le seul élément restant dans la propriété PolicyEntry sera la nouvelle entrée. Tous les éléments inclus dans la propriété avant l’appel de l’applet de commande **Set-CsClientPolicy** seront remplacés par la nouvelle entrée.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## EXEMPLE 3

L’exemple 3 montre comment supprimer une entrée de stratégie de clients à partir de la stratégie globale. Pour cela, la première commande de l’exemple extrait la stratégie globale de clients et stocke les informations dans une variable appelée $y.

Une fois la stratégie globale extraite, la deuxième commande de l’exemple a recours à la méthode RemoveAt() pour supprimer la première entrée dans cette stratégie. L’entrée de stratégie à supprimer est signalée par son numéro d’index : le numéro d’index de la première entrée de stratégie est 0, celui de la deuxième entrée est 1, et ainsi de suite. La syntaxe RemoveAt(0) signifie que la première entrée de stratégie sera supprimée.

Aussitôt l’entrée de stratégie supprimée de l’instance en mémoire de la stratégie globale, l’applet de commande **Set-CsClientPolicy** est appelée pour écrire les modifications dans l’instance réelle de la stratégie globale de clients.

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## EXEMPLE 4

La commande présentée dans l’exemple 4 supprime toutes les entrées de stratégie de clients configurées pour la stratégie globale. Pour cette opération, le paramètre PolicyEntry est utilisé et sa valeur définie sur Null ($Null).

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## Description détaillée

Les stratégies de clients constituent le mécanisme principal employé par Lync Server pour gérer des logiciels clients comme Lync. Lorsque vous créez ou configurez une stratégie de client, vous disposez de plusieurs options à votre disposition. L’une d’elles vous permet de préciser si des photos doivent être utilisées dans Lync, si des émoticônes sont autorisées ou non dans les messages instantanés et si Lync enregistre automatiquement des transcriptions des sessions de messagerie instantanée. Ces options couvrent de nombreux paramètres liés aux clients dont la gestion incombe aux administrateurs.

Toutefois, elles ne couvrent peut-être pas tous les paramètres des clients que les administrateurs doivent gérer. Pour bénéficier d’une souplesse et d’une marge accrues en matière de gestion, les stratégies de clients sont pourvues d’une propriété appelée PolicyEntry. Cette propriété à multiples valeurs permet aux administrateurs d’ajouter de nouvelles options de gestion qui ne sont pas explicitement appelées dans les stratégies de clients. Par exemple, avant la publication de Lync Server, les testeurs de la version bêta ont eu la possibilité d’ajouter une option de commentaires à Lync. Cette option a été ajoutée en tant que nouvelle entrée de stratégie et a été créée à l’aide de l’applet de commande **New-CsClientPolicyEntry**.

Notez que vous ne pouvez pas, de manière arbitraire, créer de nouvelles entrées de stratégie et vous attendre à ce que ces entrées gèrent Lync ou une autre application cliente. Au lieu de cela, vous devrez attendre un avis officiel de Microsoft concernant les noms et les valeurs qu’il est possible d’utiliser pour concevoir de nouvelles entrées de stratégies de clients.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsClientPolicyEntry** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Nom de la nouvelle entrée de stratégie. Par exemple : -Name &quot;OnlineFeedbackURL&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Valeur à attribuer à la nouvelle entrée de stratégie. Par exemple : -Value http://www.litwareinc.com/feedback.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande New-CsClientPolicyEntry n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **New-CsClientPolicyEntry** crée de nouvelles instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType.

## Voir aussi

#### Autres ressources

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

