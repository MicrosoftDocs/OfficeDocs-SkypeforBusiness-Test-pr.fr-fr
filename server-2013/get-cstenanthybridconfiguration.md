---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994034(v=OCS.15)
ms:contentKeyID: 53095413
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des valeurs pour les paramètres de configuration hybride qui permettent aux utilisateurs hébergés dans Microsoft Lync Online d’accéder aux fonctions de Voix Entreprise, comme la déviation du trafic multimédia, Enhanced 9-1-1 et le parcage d’appels. Un scénario hybride (également appelé « scénario à domaine séparé ») est un déploiement Lync Server dans lequel les utilisateurs possèdent des comptes hébergés en local, tandis que les autres utilisateurs possèdent des comptes hébergés dans Lync Online.

L’applet de commande Get-CsTenantHybridConfiguration ne peut être utilisée qu’avec Skype Entreprise Online.

## Syntaxe

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 renvoie les valeurs de propriété pour la collection globale de paramètres de configuration hybride du client.

    Get-CsTenantHybridConfiguration -Identity "Global"

## Exemple 2

Dans l’exemple 2, les valeurs de propriété sont renvoyées pour les paramètres de configuration hybride du client personnalisés appliqués au client avec le paramètre TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ».

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## Exemple 3

L’exemple 3 renvoie des informations de configuration hybride du client pour tous les clients disponibles. À cet effet, la commande appelle d’abord l’applet de commande **Get-CsTenant** pour renvoyer une collection de tous ces clients. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object**, qui sélectionne chaque client de la collection un par un et effectue deux tâches. Tout d’abord, l’applet de commande note le nom d’affichage Active Directory du client. Cela permet de s’assurer que chaque collection de paramètres est identifiée facilement. Ensuite, l’applet de commande **ForEach-Object** exécute l’applet de commande **Get-CsTenantHybridConfiguration** pour renvoyer les paramètres de configuration hybride du client pour le client en question.

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## Description détaillée

Dans un déploiement « à domaine séparé », une organisation comporte des utilisateurs possédant des comptes hébergés dansLync Online, tandis que d’autres utilisateurs possèdent des comptes hébergés dans une version locale de Lync Server. Par défaut, les utilisateurs hébergés dans Lync Online n’ont pas accès à la plage complète des fonctions proposées par Voix Entreprise, car les serveurs Lync Online n’ont pas accès directement aux informations de déploiement Lync Server et de configuration du réseau. Entre autres, les utilisateurs de Lync Online ne bénéficient pas d’un accès par défaut à des éléments comme :

  - Enhanced 9-1-1, le service Lync Server utilisé pour passer des appels d’urgence ;

  - parcage d’appels, le service Lync Server qui permet aux utilisateurs de mettre en attente un appel sur un téléphone A, puis de récupérer l’appel sur un téléphone B ;

  - contournement de média, qui permet aux appels échangés via le réseau public commuté (RTC) de passer outre le serveur de médiation, ce qui permet de minimiser le transcodage et la latence du réseau ;

  - appels entrants et sortants de conférence PSTN, qui permettent aux utilisateurs de participer à la partie audio d’une conférence en ligne à l’aide d’un téléphone PSTN ou d’un appareil mobile ;

  - application Response Group, qui offre une méthode d’acheminement automatique des appels téléphoniques vers diverses entités, telles que le support technique ou le service clientèle. Par défaut, les utilisateurs de Lync Server ne peuvent pas fonctionner comme des agents Response Group.

Pour permettre aux utilisateurs de Lync Online d’accéder à ces fonctionnalités Voix Entreprise, les administrateurs doivent affecter les valeurs appropriées aux paramètres de configuration hybride tels que les URL de service web internes et externes et le nom de domaine complet du serveur Edge d’accès de l’organisation. Ces valeurs, qui peuvent seulement être configurées à l’aide de l’applet de commande **Set-CsTenantHybridConfiguration**, offrent aux serveurs Lync Online les informations nécessaires à l’utilisation de ces fonctionnalités Voix Entreprise avancées.

Vous pouvez renvoyer des informations sur les paramètres de configuration hybride du client utilisés actuellement en utilisant l’applet de commande **Get-CsTenantHybridConfiguration**.

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
<td><p>Permet d’utiliser des caractères génériques pour renvoyer une collection de paramètres de configuration hybride du client. Comme vous êtes limité à une seule collection globale de paramètres de configuration hybride, il n’est pas nécessaire d’utiliser le paramètre Filter. En revanche, voici une syntaxe valide pour l’applet de commande <strong>Get-CsTenantHybridConfiguration</strong> :</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identité unique des paramètres de configuration hybride du client à renvoyer. Comme vous êtes limité à une seule collection globale de paramètres de configuration hybride, la seule collection qui peut être renvoyée en utilisant le paramètre Identity est la collection globale :</p>
<p>-Identity global</p>
<p>Pour modifier les paramètres d’un client individuel, utilisez le paramètre Tenant au lieu du paramètre Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données de configuration hybride du client à partir de la réplique locale du magasin de gestion centralisée, plutôt que du magasin de gestion centralisée proprement dit.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificateur global unique (GUID) du compte du client pour lequel les paramètres de configuration hybride sont renvoyés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de client de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous utilisez une session à distance de Windows PowerShell et que vous êtes seulement connecté à Skype Entreprise Online, vous n’avez pas besoin d’inclure le paramètre Tenant. L’ID de client est renseigné automatiquement sur la base de vos informations de connexion. Le paramètre Tenant est principalement destiné à être utilisé dans un déploiement hybride.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsTenantHybridConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsTenantHybridConfiguration** renvoie des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration.

## Voir aussi

#### Autres ressources

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

