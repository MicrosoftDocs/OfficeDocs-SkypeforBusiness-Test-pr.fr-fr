---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412751(v=OCS.15)
ms:contentKeyID: 49298405
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée un modèle et une traduction d’expression régulière pour la traduction des numéros de téléphones dans différents formats. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Exemples

## EXEMPLE 1

Cet exemple crée un modèle et une traduction d’expression régulière. Cette expression inclut un modèle devant contenir exactement 7 caractères (-ExactLength 7) et supprime les trois premiers chiffres du numéro correspondant (-DigitsToStrip 3). Le modèle créé par cette expression régulière est ^\\d{3}(\\d{4})$. La traduction est $1. Par exemple, le numéro 5551212 correspond à ce modèle et la traduction qui en résulte est 1212 : le numéro à 7 chiffres et les 3 chiffres supprimés.

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## EXEMPLE 2

Cet exemple créé également un modèle et une traduction d’expression régulière, mais utilise ensuite ces valeurs pour créer une règle de normalisation vocale. Dans la première ligne, nous appelons l’applet de commande **New-CsVoiceRegEx** afin de créer une expression régulière dans laquelle le nombre correspondant doit comporter au moins 7 caractères (-AtLeastLength 7) et doit commencer par 1 (-StartsWith "1"). Aux résultats de cette commande sont affectés la variable $regex.

Dans la deuxième ligne, nous appelons l’applet de commande **New-CsVoiceNormalizationRule**. Nous attribuons à la nouvelle règle un nom unique, dans ce cas, règle global/internal. Nous affectons ensuite en tant que modèle de la règle de normalisation le modèle que nous avons créé en appelant l’applet de commande **New-CsVoiceRegex** : -Pattern $regex.Pattern. Nous procédons de même avec la traduction, en affectant la traduction créée avec l’appel de l’applet de commande **New-CsVoiceRegex** : -Translation $regex.Translation.

Remarque : le modèle créé dans cet exemple est ^(1\\d{5}\\d+)$. Ce dernier peut être déchiffré comme étant un nombre commençant par 1 (1) suivi de cinq chiffres (\\d{5}), suivi par n’importe quel nombre de chiffres (\\d+). Cela constitue un nombre d’au moins 7 chiffres (1 plus 5 plus 1 ou plus) commençant par 1, comme souhaité.

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## Description détaillée

Les expressions régulières servent à faire correspondre des modèles de caractères. Lync Server utilise des expressions régulières afin de convertir des numéros de téléphone depuis et vers divers formats (numéros composés, E.164, autocommutateur privé (PBX) local et réseau téléphonique commuté \[RTC\]). Nous vous conseillons d’apprendre les règles de syntaxe et de format de travail des expressions régulières afin de pouvoir définir correctement les règles de conversion. L’applet de commande **New-CsVoiceRegex** fournit des paramètres permettant de spécifier certains critères, puis génère pour vous l’expression régulière.

Cette applet de commande vous aide à générer des expressions régulières qui seront utilisées comme valeurs Pattern et Translation pour les règles de normalisation (l’applet de commande **New-CsVoiceNormalizationRule**) et les règles de traduction sortantes (l’applet de commande **New-CsOutboundTranslationRule**), et comme valeurs NumberPattern pour les itinéraires de communications vocales (l’applet de commande **New-CsVoiceRoute**).

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsVoiceRegex** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Int32</p></td>
<td><p>Longueur minimale obligatoire pour que la chaîne (numéro de téléphone) corresponde à l’expression. Par exemple, si vous définissez une règle de normalisation affectant seulement les numéros devant avoir 7 chiffres (ou caractères) au moins, spécifiez la valeur 7 pour ce paramètre.</p>
<p>Vous devez entrer une valeur pour ce paramètre ou pour le paramètre ExactLength. Vous ne pouvez pas entrer de valeur pour les deux.</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Int32</p></td>
<td><p>Longueur que la chaîne (numéro de téléphone) doit avoir pour correspondre à l’expression régulière. Par exemple, si vous souhaitez qu’une règle de normalisation affecte les numéros à 10 caractères seulement, spécifiez la valeur 10 pour ce paramètre.</p>
<p>Vous devez entrer une valeur pour ce paramètre ou pour le paramètre AtLeastLength. Vous ne pouvez pas entrer de valeur pour les deux.</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Chaîne spécifiant les caractères ou nombres à ajouter au début du numéro de téléphone. La valeur entrée pour ce paramètre a une incidence sur la valeur Translation, en ce qu’elle ajoute des caractères au nombre correspondant au modèle d’expression régulière. Par exemple, si le nombre correspondant au modèle est 5551212 et que la valeur DigitsToPrepend est de 425, le numéro traduit sera 4255551212 (dans l’hypothèse où aucune autre traduction n’a été appliquée).</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Nombre de caractères à supprimer à partir du début de la chaîne (numéro de téléphone). Par exemple, si le numéro 2065551212 est entré et que la valeur DigitsToStrip est de 3, le numéro sera traduit en 5551212.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Premier caractère de la chaîne (numéro de téléphone). La chaîne ne correspond pas à l’expression régulière, à mois de commencer par la chaîne spécifiée dans le paramètre StartsWith. Par exemple, si la valeur +1 est spécifiée pour StartsWith, seuls les nombres commençant par +1 correspondent au modèle et sont traduites. Notez que le nombre de caractères de la chaîne StartsWith est inclus dans les totaux de ExactLength et AtLeastLength. Par exemple, si vous spécifiez une valeur ExactLength de 10 et une chaîne StartsWith de +1, le numéro de téléphone correspondant comporte 8 caractères et est précédé de +1, pour un total de 10 chiffres en tout.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.Voice.OcsVoiceRegex.

## Voir aussi

#### Autres ressources

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

