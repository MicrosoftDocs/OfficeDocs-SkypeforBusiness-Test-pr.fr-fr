---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412916(v=OCS.15)
ms:contentKeyID: 49298680
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une stratégie de bande passante en mémoire que vous pouvez appliquer au profil de stratégie de bande passante. Dans Lync Server, la stratégie s’applique soit à la bande passante audio, soit à la bande passante vidéo. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## Exemples

## EXEMPLE 1

Cet exemple crée une nouvelle stratégie de bande passante et l’affecte à la variable $bwp. Tous les paramètres de l’applet de commande **New-CsNetworkBWPolicy** sont obligatoires. Dans cet exemple, nous avons défini une limite de bande passante totale (BWLimit) de 2 000 Kbits/s et une limite de session de bande passante (BWSessionLimit) de 300 Kbits/s, puis avons appliqué ces limites à des sessions vidéo (-BWPolicyModality video).

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## EXEMPLE 2

L’exemple 2 étend l’exemple 1 en affectant la nouvelle stratégie de bande passante à un profil de stratégie. La commande dans la ligne 1 est identique à l’exemple 1 : elle crée des restrictions pour la bande passante vidéo. La ligne 2 appelle ensuite l’applet de commande **New-CsNetworkBandwidthPolicyProfile** pour ajouter cette stratégie à un nouveau profil. Le nouveau profil reçoit une valeur Identity définie sur LowBWLimit. Nous pouvons ensuite utiliser le paramètre BWPolicy et lui attribuer la valeur $bwp qui est la variable contenant la nouvelle stratégie de bande passante créée à la ligne 1.

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## Description détaillée

Cette applet de commande crée une nouvelle stratégie de bande passante. Une stratégie de bande passante permet de définir des restrictions de bande passante pour des modes bien précis. (Dans Lync Server, seuls les modes audio et vidéo peuvent être soumis à des restrictions en matière de bande passante.) La stratégie de bande passante est créée uniquement en mémoire de sorte que la sortie doit être affectée à une variable, puis transmise sous forme de valeur au paramètre BWPolicy de l’applet de commande **New-CsNetworkBandwidthPolicyProfile** ou **Set-CsNetworkBandwidthPolicyProfile**. Les stratégies de bande passante sont appliquées à des profils de stratégie dans lesquels peuvent être stockés les multiples stratégies d’un seul et unique profil et qui font partie intégrante de la configuration réseau globale pour le service Contrôle d’admission des appels.

Notez qu’il est conseillé d’affecter des stratégies audio et vidéo directement à un profil de stratégie de bande passante en appelant l’applet de commande **New-CsNetworkBandwidthPolicyProfile** ou **Set-CsNetworkBandwidthPolicyProfile** et en spécifiant des valeurs pour les paramètres AudioBWLimit, AudioBWSessionLimit, VideoBWLimit et VideoBWSessionLimit.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsNetworkBWPolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.UInt32</p></td>
<td><p>Bande passante maximale totale (en Kbits/s) pour toutes les sessions simultanées du type spécifié dans le paramètre BWPolicyModality.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>Détermine le type de bande passante visé par des restrictions.</p>
<p>Valeurs valides : Audio, Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.UInt32</p></td>
<td><p>Bande passante maximale totale (en Kbits/s) autorisée pour une session unique du type spécifié dans le paramètre BWPolicyModality.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType.

## Voir aussi

#### Autres ressources

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

