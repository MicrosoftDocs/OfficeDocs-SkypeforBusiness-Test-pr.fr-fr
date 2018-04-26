---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399024(v=OCS.15)
ms:contentKeyID: 49299181
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste un numéro de téléphone par rapport à un plan de numérotation (anciennement appelé « profil d’emplacement ») et retourne la règle de normalisation qui sera appliquée au numéro, ainsi que le numéro traduit après application de la règle de normalisation. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## Exemples

## EXEMPLE 1

Cet exemple exécute un test en partant du plan de numérotation dont l’identité est site:Redmond. L’applet de commande **Get-CsDialPlan** est d’abord exécutée pour récupérer le plan de numérotation dont l’identité est site:Redmond. Cet objet de plan de numérotation est ensuite redirigé vers l’applet de commande **Test-CsDialPlan** où le plan de numérotation est une nouvelle fois testé par rapport au numéro de téléphone 14255559999. Le résultat obtenu est le paramètre DialedNumber après application d’une règle de normalisation vocale au modèle correspondant. S’il existe plusieurs règles de normalisation dotées d’un modèle correspondant sur le site, la règle qui affiche la valeur de priorité la plus faible est appliquée. Si aucune règle avec un modèle correspondant à la valeur DialedNumber n’existe (par exemple, si la règle de normalisation est conforme à un modèle de numéro à 11 chiffres mais que vous utilisez un numéro à 7 chiffres), aucune valeur ne sera retournée.

Le résultat de cette commande comprend un numéro de téléphone et une règle de normalisation. La règle de normalisation dispose de nombreuses propriétés et, par défaut, le résultat est tronqué par des points de suspension (...). Pour consulter l’ensemble des propriétés et des valeurs de la règle de normalisation vocale retournée, il nous faut rediriger le résultat vers l’applet de commande **Format-List** avant de l’afficher à l’écran. Le numéro de téléphone et la règle de normalisation apparaîtront dans la liste sur des lignes séparées et les propriétés et les valeurs de la règle de normalisation seront renvoyées à la ligne afin de tenir sur l’écran.

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## EXEMPLE 2

L’exemple 2 est identique à l’exemple 1, mais au lieu de rediriger les résultats de l’opération Get directement vers l’applet de commande **Test-CsDialPlan**, l’objet est d’abord stocké dans la variable $a, puis transmis en tant que valeur au paramètre Dialplan à utiliser comme plan de numérotation de test.

Comme pour l’exemple 1, nous achevons la commande en redirigeant le résultat obtenu vers l’applet de commande **Format-List** dans le but d’obtenir plus d’informations sur la règle de normalisation vocale que celles dévoilées par défaut.

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## EXEMPLE 3

Cet exemple exécute un plan de numérotation de test en comparaison avec tous les plans de numérotation définis dans le déploiement Lync Server. L’applet de commande **Get-CsDialPlan** est d’abord exécutée (sans aucun paramètre) afin de récupérer tous les plans de numérotation. La collection de plans de numérotation retournée est ensuite redirigée vers l’applet de commande **Test-CsDialPlan** et chacun de ses plans de numérotation y est testé avec le numéro de téléphone 2065559999. Le résultat obtenu est une liste de numéros traduits avec la règle de normalisation vocale appliquée, une pour chaque plan de numérotation dans la collection. Si aucune règle de normalisation vocale dans un plan de numérotation ne s’applique à la valeur DialedNumber pour un plan de numérotation en particulier (par exemple, si la règle de normalisation est conforme à un modèle de numéro à 11 chiffres mais que vous utilisez un numéro à 7 chiffres), une ligne vide apparaîtra dans la liste à la place du plan de numérotation.

Par défaut, le résultat tronque l’affichage complet de la règle de normalisation vocale qui a été appliquée. Dans les exemples 1 et 2, nous avons pu afficher le résultat tout entier en redirigeant les données obtenues par le test vers l’applet de commande **Format-List**. Dans cet exemple, nous redirigeons le résultat vers l’applet de commande **Format-Table** et incluons le paramètre Wrap. Chaque entrée apparaît dans un tableau (une colonne pour le numéro traduit, une pour la règle de normalisation vocale appliquée) mais le résultat fait l’objet d’un renvoi à la ligne afin que la règle de normalisation soit entièrement visible dans la colonne.

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## Description détaillée

Cette applet de commande vous permet de voir les résultats de l’application d’un plan de numérotation à un numéro de téléphone donné. Les plans de numérotation apportent des informations, y compris sur le mode d’application des règles de normalisation, nécessaires aux utilisateurs Voix Entreprise pour effectuer des appels téléphoniques. Dotée d’un numéro composé et d’un plan de numérotation, cette applet de commande vérifiera la règle de normalisation qui sera appliquée au sein du plan de numérotation et quel sera le numéro traduit.

Vous pouvez recourir à cette applet de commande pour résoudre des problèmes liés à la traduction de numéros ou pour vérifier l’application des règles conformément à certains numéros.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsDialPlan** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Numéro de téléphone en fonction duquel vous souhaitez tester le plan de numérotation spécifié dans le paramètre Dialplan.</p>
<p>Type de données complet : Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>LocationProfile</p></td>
<td><p>Objet contenant une référence au plan de numérotation en fonction duquel vous souhaitez tester le numéro précisé dans le paramètre DialedNumber.</p>
<p>Type de données complet : Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile. Accepte l’entrée redirigée pour les objets de plan de numérotation.

## Types de retours

Retourne un objet de type Microsoft.Rtc.Management.Voice.LocationProfileTestResult.

## Voir aussi

#### Autres ressources

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

