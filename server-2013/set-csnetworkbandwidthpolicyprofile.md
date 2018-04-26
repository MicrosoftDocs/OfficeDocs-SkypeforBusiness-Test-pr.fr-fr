---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398338(v=OCS.15)
ms:contentKeyID: 49297204
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un profil de stratégie de bande passante du réseau. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie la description du profil de stratégie de bande passante avec l’identité LowBWProfile. Pour ce faire, il appelle l’applet de commande **Set-CsNetworkBandwidthPolicyProfile** avec deux paramètres : Identity qui spécifie le nom du profile à modifier, et Description qui spécifie la nouvelle description du profil.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## EXEMPLE 2

L’exemple 2 modifie la limite globale et la limite de session des transmissions vidéo du profil de stratégie de bande passante avec l’identité LowBWLimit. Après avoir spécifié l’identité du profil à modifier, il faut utiliser le paramètre VideoBWLimit pour définir la limite vidéo à 2500. Il faut ensuite utiliser le paramètre VideoBWSessionLimit pour définir la limite de session individuelle à 300. Cette commande ajoutera un profil vidéo ou mettra à jour le profil vidéo existant pour la stratégie de bande passante LowBWLimit. Tous les profils audio existants ne seront pas affectés.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## EXEMPLE 3

Dans cet exemple, une nouvelle stratégie de bande passante est créée et affectée au profil de stratégie de bande passante avec l’identité LowBWLimit. La première ligne de l’exemple appelle l’applet de commande **New-CsNetworkBWPolicy**. Cette applet de commande crée un nouveau profil (dans le cas présent le profil vidéo « -BWPolicyModality video ») avec une limite de 5 000 Kbits/s (-BWLimit 5000) et une limite de 200 Kbits/s pour la session (-BWSessionLimit 200). Ce nouvel objet de profil est stocké dans la variable $bp. La ligne suivante de l’exemple appelle l’applet de commande **Set-CsNetworkBandwidthPolicyProfile** pour modifier le profil LowBWLimit (-Identity LowBWLimit). Le paramètre BWPolicy est utilisé avec une valeur de $bp. Ceci remplace toutes les stratégies de profil existantes par un nouveau profil récemment créé qui sera stocké dans la variable $bp.

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## EXEMPLE 4

L’exemple 4 ajoute une nouvelle stratégie de bande passante audio à l’ensemble des stratégies existantes dans le profil LowBWProfile. Dans la ligne 1, nous appelons l’applet de commande **Get-CsNetworkBandwidthPolicyProfile** pour récupérer le profil avec l’identité LowBWProfile. Nous enregistrons ce profil dans une variable $a. Dans la ligne suivante, nous appelons l’applet de commande **New-CsNetworkBWPolicy** pour créer une nouvelle stratégie de bande passante. Cette stratégie est une stratégie audio (-BWPolicyModality audio) avec une limite de 2000 Kbits/s (-BWLimit 2000) et une limite de 300 Kbits/s pour la session (-BWSessionLimit 300). Cette nouvelle stratégie est enregistrée dans une variable $ap.

À la ligne 3, nous ajoutons une nouvelle stratégie audio (enregistrée dans $ap) dans le profil que nous récupérons à la ligne 1 (et qui a été enregistré dans la variable $a). Nous réalisons cela en appelant la méthode Add de la propriété BWPolicy du profil pour transférer une valeur $ap. Ceci revient à ajouter une nouvelle stratégie stockée dans la variable $ap à la stratégie BWPolicy du profil LowBWProfile (stockée dans la variable $a).

Enfin, nous appelons l’applet de commande **Set-CsNetworkBandwidthPolicyProfile** pour mettre à jour le profil LowBWProfile. Nous utilisons le paramètre d’instance en transférant une valeur de la variable $a qui contient justement notre profil modifié.

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## EXEMPLE 5

L’exemple 5 offre les mêmes fonctions que l’exemple 4. Il ajoute une nouvelle stratégie audio à la liste des stratégies existantes pour le profil LowBWProfile. Cette méthode utilise moins de lignes, mais n’est pas aussi claire. Nous l’avons inclus ici simplement pour démontrer qu’il existe différentes manières de faire la même chose.

À la ligne 1, nous avons créé une nouvelle stratégie de bande passante audio, en configurant une limite de bande passante (2000) et une limite de session (300), puis en enregistrant un nouvel objet dans la variable $ap. Ensuite, nous appelons l’applet de commande **Set-CsNetworkBandwidthPolicyProfile** pour modifier le profil avec l’identité LowBWProfile. Nous avons utilisé le paramètre BWPolicy pour modifier la liste des stratégies à l’intérieur du profil. Notez la valeur transmise à ce paramètre : @{add=$ap}. Il s’agit tout simplement d’une manière d’ajouter un élément à une liste dans Windows PowerShell. Vous commencez par la saisie du signe @ suivi d’accolades {}. À l’intérieur de ces accolades, vous spécifiez l’action que vous souhaitez effectuer dans la liste (soit, dans le cas présent, un ajout). (Vous pouvez également supprimer ou remplacer un élément.) Nous faisons suivre l’action (ajout) d’un signe égal, suivi de l’objet que nous voulons ajouter à la liste soit, dans ce cas, la nouvelle stratégie stockée dans la variable $ap.

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## Description détaillée

La stratégie de bande passante utilisée dans le cadre du contrôle d’admission des appels (CAC) permet de définir des restrictions de bande passante pour des modes bien précis. (Dans Lync Server, seuls les modes audio et vidéo peuvent être soumis à des restrictions en matière de bande passante.) Cette applet de commande modifie le profil de ces stratégies au sein du conteneur.

IMPORTANT : Si un profil contient plusieurs stratégies (par exemple, une stratégie audio et une stratégie vidéo), lorsque vous modifiez le profil à l’aide des propriétés AudioBWLimit, AudioBWSessionLimit, VideoBWLimit ou VideoBWSessionLimit, toutes les stratégies de profil existantes seront supprimées et remplacées par de nouvelles valeurs. Si le profil contient une stratégie qui limite la vidéo et que vous ne configurez que le paramètre AudioBWLimit, la stratégie vidéo sera supprimée et une stratégie audio sera créée.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkBandwidthPolicyProfile** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Quantité maximale de bande passante à allouer pour toutes les connexions audio. Si une seule session audio dépasse la limite de bande passante, cette session ne sera pas autorisée à démarrer.</p>
<p>Valeur exprimée en Kbits/s. Par exemple, une valeur de 1000 signifie 1 000 Kbits/s.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : Si vous affectez une valeur au paramètre Get-AudioBWSessionLimit et non au paramètre AudioBWLimit, la valeur par défaut de AudioBWLimit sera 0.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Largeur maximale de bande passante allouée par session audio. Valeur exprimée en Kbits/s. La valeur doit être égale ou supérieure à 40.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : Si vous affectez une valeur au paramètre AudioBWLimit et non au paramètre AudioBWSessionLimit, la valeur par défaut de AudioBWSessionLimit sera 175.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste d’objets contenant les profils de stratégie de bande passante. Chaque objet de la liste comprend un mode de bande passante (audio ou vidéo), une limite de bande passante et une limite pour la session de bande passante.</p>
<p>Si vous affectez une valeur à ce paramètre, vous ne pouvez pas affecter de valeur au paramètre AudioBWLimit, AudioBWSessionLimit, VideoBWLimit ou VideoBWSessionLimit.</p>
<p>Les objets de la liste doivent être du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType. Les objets de ce type peuvent être créés en appelant l’applet de commande <strong>New-CsNetworkBWPolicy</strong> et le profil résultant pourra ensuite être ajouté au profil en l’attribuant comme la valeur affectée à ce paramètre.</p></td>
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
<td><p>Description du profil de stratégie de bande passante. Par exemple, vous pouvez utiliser ce paramètre pour clarifier l’utilisation du profil souhaité.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Cette valeur de chaîne identifie uniquement le profil de stratégie de bande passante que vous voulez modifier. Ce principe est le même pour la propriété BWPolicyProfileID du profil et peut être modifié en changeant la valeur de cette propriété. Cela revient à réaliser une opération « copier-coller » : toutes les propriétés du profil restent les mêmes, seuls les noms changent. Cependant, cette valeur ne peut pas être modifiée si le profil est affecté à un site réseau.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>Référence à l’objet de profil de stratégie de bande passante (un objet du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType) qui contient les paramètres que vous voulez utiliser pour modifier le profil. Cette référence d’objet peut être récupérée en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Quantité maximale de bande passante à allouer pour toutes les connexions vidéo. Si une seule session vidéo dépasse la limite de bande passante vidéo, cette session ne sera pas autorisée à démarrer.</p>
<p>Valeur exprimée en Kbits/s. Par exemple, une valeur de 1000 signifie 1 000 Kbits/s.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : Si vous affectez une valeur au paramètre VideoBWSessionLimit et non au paramètre VideoBWLimit, la valeur par défaut de VideoBWLimit sera 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Largeur maximale de bande passante allouée par session vidéo. Valeur exprimée en Kbits/s. La valeur doit être égale ou supérieure à 100.</p>
<p>Si vous fournissez une valeur pour ce paramètre, vous ne pouvez pas spécifier de valeur pour le paramètre BWPolicy.</p>
<p>Valeur par défaut : Si vous affectez une valeur au paramètre VideoBWLimit et non au paramètre VideoBWSessionLimit, la valeur par défaut de VideoBWSessionLimit sera 700.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Accepte l’entrée redirigée pour les objets de profil de stratégie.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Voir aussi

#### Autres ressources

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

