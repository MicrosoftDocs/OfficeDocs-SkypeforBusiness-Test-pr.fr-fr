---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399011(v=OCS.15)
ms:contentKeyID: 49299139
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les paramètres de configuration de serveur proxy utilisés dans votre organisation. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 retourne une collection de tous les paramètres de configuration proxy actuellement utilisés dans votre organisation. Cela s’effectue par l’appel de l’applet de commande **Get-CsProxyConfiguration** sans paramètre.

    Get-CsProxyConfiguration

## EXEMPLE 2

L’exemple 2 retourne les informations relatives aux paramètres de configuration proxy dont la propriété Identity est service:EdgeServer:atl-cs-001.litwareinc.com. Tenant compte du caractère unique des identités, cette commande ne retourne jamais plus d’une collection de paramètres.

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## EXEMPLE 3

L’exemple 3 retourne des informations sur tous les paramètres proxy qui ont été configurés au niveau de l’étendue Service. Pour ce faire, la commande appelle l’applet de commande **Get-CsProxyConfiguration** avec le paramètre Filter ; la valeur de filtre « service:\* » garantit que seuls les paramètres dont l’identité commence par la valeur de chaîne « service: » sont retournés.

    Get-CsProxyConfiguration -Filter "service:*"

## EXEMPLE 4

L’exemple 4 retourne des informations sur les paramètres de configuration proxy qui n’autorisent pas l’utilisation des certificats clients comme un mécanisme d’authentification. Pour effectuer cette tâche, la commande utilise d’abord l’applet de commande **Get-CsProxyConfiguration** pour retourner une collection de tous les paramètres de configuration proxy actuellement utilisés. Cette collection est alors redirigée vers l’applet de commande **Where-Object**, qui sélectionne uniquement les paramètres dont la propriété UseCertificateForClientToProxyAuth est égale à False.

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## EXEMPLE 5

L’exemple 5 retourne tous les paramètres de configuration proxy dont la taille maximale du corps d’un message de client est inférieure à 5000 kilo-octets. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsProxyConfiguration** sans paramètre, ce qui retourne une collection de tous les paramètres de configuration proxy actuellement utilisés. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui choisit les paramètres dont la propriété MaxClientMessageBodySizeKb est inférieure à 5000 kilo-octets.

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## Description détaillée

Lync Server permet de gérer vos serveurs proxy via les paramètres de configuration de serveur proxy. Ces paramètres, qui peuvent être appliqués à la fois au niveau de l’étendue globale et au niveau de l’étendue Service (mais uniquement pour les services Serveur d’inscriptions et ceux liés au serveur Edge) permettent de contrôler, entre autres, les protocoles d’authentification pouvant être utilisés par les points de terminaison clients et l’utilisation ou non de la compression sur les connexions entrantes et sortantes du serveur proxy. Lorsque vous installez Lync Server, une collection globale des paramètres de configuration de serveur proxy est automatiquement créée pour vous. Comme nous l’avons souligné, vous pouvez également créer des collections supplémentaires au niveau de l’étendue Service.

L’applet de commande **Get-CsProxyConfiguration** vous permet de retourner des informations les paramètres de configuration de serveur proxy actuellement utilisés dans votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsProxyConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet d’utiliser des caractères génériques afin de spécifier les paramètres de configuration proxy à retourner. Par exemple, cette syntaxe retourne tous les paramètres configurés au niveau de l’étendue Service : -Filter &quot;service:*&quot;.</p>
<p>Vous ne pouvez pas utiliser à la fois les paramètres Filter et Identity dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique des paramètres de configuration de serveur proxy à retourner. Pour retourner les paramètres globaux, utilisez la syntaxe suivante : -Identity global. Pour retourner les paramètres configurés au niveau de l’étendue Service, utilisez une syntaxe du type : -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;. Notez que vous ne pouvez pas utiliser de caractères génériques lorsque vous spécifiez une identité. Si vous voulez (ou devez) utiliser des caractères génériques, servez-vous du paramètre Filter.</p>
<p>Si ce paramètre n’est pas inclus, l’applet de commande <strong>Get-CsProxyConfiguration</strong> retournera tous les paramètres de configuration de serveur proxy actuellement utilisés dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données de configuration proxy à partir du réplica local du magasin central de gestion et non depuis le magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsProxyConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsProxyConfiguration** retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Voir aussi

#### Autres ressources

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

