---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994046(v=OCS.15)
ms:contentKeyID: 53095460
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Utilisée dans un scénario hybride pour donner aux utilisateurs hébergés sur Microsoft Lync Online accès aux fonctionnalités Voix Entreprise locales telles que le contournement de média, Enhanced 9-1-1 et le parcage d’appels. Un scénario hybride (également appelé scénario de domaine séparé) est un déploiement Lync Server dans lequel certains utilisateurs ont leur compte hébergé localement, tandis que d’autres ont leur compte hébergé sur Lync Online.

Cette applet de commande peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## Exemples

## Exemple 1

La commande affichée dans l’exemple 1 définit l’URL de service interne pour la collection globale de paramètres de configuration hybride de client. Pour configurer un paramètre global, incluez le paramètre Identity avec la valeur de paramètre « global ».

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Exemple 2

Dans l’exemple 2, l’URL de service interne est configurée pour un client spécifique. Dans cet exemple, le client a le TenantID « bf19b7db-6960-41e5-a139-2aa373474354 ». Lorsqu’une valeur de propriété est attribuée explicitement à un client individuel, celui-ci est soumis à ses propres paramètres de configuration hybride de client, plutôt qu’aux paramètres globaux.

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Exemple 3

La commande affichée dans l’exemple 3 configure l’URL de service interne pour tous les clients de votre organisation. Pour ce faire, la commande commence par utiliser l’applet de commande **Get-CsTenant** pour retourner une collection des clients disponibles. Cette collection est ensuite transmise à l’applet de commande **ForEach-Object**. L’applet de commande **ForEach-Object** exécute ensuite l’applet de commande **Set-CsTenantHybridConfiguration** sur chaque client dans la collection et définit ainsi l’URL de service interne pour chacun de ces clients sur « https://internal.litwareinc.com ».

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## Description détaillée

Dans un déploiement hybride ou de « domaine séparé », certains utilisateurs d’une organisation ont leur compte hébergé sur Lync Online, tandis que d’autres ont leur compte hébergé sur Lync Server. Par défaut, les utilisateurs hébergés sur Lync Online n’ont pas accès à l’ensemble des fonctionnalités offertes par Voix Entreprise. En effet, les serveurs Lync Online n’ont pas d’accès direct au déploiement Lync Server local et aux informations de configuration du réseau. Les utilisateurs Lync Online n’ont pas d’accès par défaut aux fonctionnalités suivantes notamment :

  - Enhanced 9-1-1, le service Lync Server utilisé pour passer des appels d’urgence ;

  - parcage d’appels, le service Lync Server qui permet aux utilisateurs de mettre en attente un appel sur un téléphone A, puis de récupérer l’appel sur un téléphone B ;

  - contournement de média, qui permet aux appels échangés via le réseau public commuté (RTC) de passer outre le serveur de médiation, ce qui permet de minimiser le transcodage et la latence du réseau ;

  - appels entrants et sortants de conférence PSTN, qui permettent aux utilisateurs de participer à la partie audio d’une conférence en ligne à l’aide d’un téléphone PSTN ou d’un appareil mobile ;

  - application Response Group, qui offre une méthode d’acheminement automatique des appels téléphoniques vers diverses entités, telles que le support technique ou le service clientèle. Par défaut, les utilisateurs Lync Online ne peuvent pas fonctionner comme des agents Response Group.

Pour permettre aux utilisateurs Lync Online d’accéder à ces fonctionnalités Voix Entreprise, les administrateurs doivent affecter les valeurs appropriées aux paramètres de configuration hybride tels que les URL de service web internes et externes et le nom de domaine complet du serveur Edge d’accès de l’organisation. Ces valeurs, qui peuvent seulement être configurées à l’aide de l’applet de commande **Set-CsTenantHybridConfiguration**, offrent aux serveurs Lync Online les informations nécessaires à l’utilisation de ces fonctionnalités Voix Entreprise avancées.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>URL de service web externe.</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>URL de service web interne.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identité unique des paramètres de configuration hybride de client à modifier. Comme vous êtes limité à une seule collection globale de paramètres de configuration hybride, la seule collection qui peut être modifiée à l’aide du paramètre Identity est la collection globale :</p>
<p>-Identity global</p>
<p>Pour modifier les paramètres d’un client individuel, utilisez le paramètre Tenant au lieu du paramètre Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Permet de transmettre une référence à un objet à l’applet de commande plutôt que de définir des valeurs de paramètre individuelles.</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de domaine complet de votre serveur d’accès Edge local.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte client pour lequel les paramètres de configuration hybride sont modifiés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous utilisez une session à distance de Windows PowerShell et que vous êtes seulement connecté à Skype Entreprise Online, vous n’avez pas besoin d’inclure le paramètre Tenant. L’ID de client est renseigné automatiquement sur la base de vos informations de connexion. Le paramètre Tenant est principalement destiné à être utilisé dans un déploiement hybride.</p></td>
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

Aucun. L’applet de commande **Set-CsTenantHybridConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

Aucun. L’applet de commande **Set-CsTenantHybridConfiguration** modifie les instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

