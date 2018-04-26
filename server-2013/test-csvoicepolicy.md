---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398310(v=OCS.15)
ms:contentKeyID: 49297158
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Teste un numéro de téléphone par rapport à une stratégie de voix et détermine l’itinéraire vocal qui doit être utilisé en fonction de la stratégie de numérotation correspondante. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## Exemples

## EXEMPLE 1

Cet exemple exécute une stratégie de voix basée sur l’identité site:Redmond. C’est l’applet de commande **Get-CsVoicePolicy** qui est d’abord exécutée pour récupérer la stratégie avec l’identité site:Redmond. L’objet de cette stratégie est ensuite acheminé vers l’applet de commande **Test-CsVoicePolicy** où la stratégie est testée pour le numéro +14255559999. Le résultat est le premier itinéraire vocal (basé sur la propriété prioritaire de l’itinéraire) ayant un modèle de numéro correspondant à la valeur cible du numéro et une utilisation téléphonique correspondant à l’utilisation du téléphone dans le cadre de la stratégie. Si aucun itinéraire correspondant n’est trouvé (par exemple, si le modèle de numéro correspond au modèle d’un numéro à 11 chiffres et que vous fournissez un numéro à 7 chiffres), une valeur nulle vous sera renvoyée.

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## EXEMPLE 2

L’exemple 2 est identique à l’exemple 1, mais au lieu de rediriger les résultats de l’opération Get directement vers l’applet de commande **Test-CsVoicePolicy**, l’objet est d’abord enregistré dans la variable $a, puis transmis comme valeur au paramètre VoicePolicy à utiliser comme configuration de test.

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## EXEMPLE 3

Cet exemple exécute un test de stratégie de voix pour comparer toutes les stratégies vocales définies dans le déploiement Lync Server. L’applet de commande **Get-CsVoicePolicy** est d’abord exécutée (sans aucun paramètre) pour récupérer toutes les stratégies de voix. La collection de stratégies renvoyée est ensuite acheminée vers l’applet de commande **Test-CsVoicePolicy** où chaque stratégie de la collection est contrôlée pour savoir si un itinéraire correspond au numéro de téléphone cible fourni (+12065559999) et aux utilisations du téléphone. Le résultat est une liste des itinéraires correspondants avec les utilisations de téléphone afférentes.

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## Description détaillée

Les stratégies de voix sont associées aux itinéraires de communications vocales par l’intermédiaire des utilisations du réseau téléphonique commuté (PSTN). L’appel d’un utilisateur auquel a été assignée une stratégie de voix particulière ne peut être envoyé que sur un itinéraire dont l’utilisation PSTN correspond à une utilisation de la stratégie ainsi qu’à un modèle de numérotation correspondant au numéro composé. Appelez l’applet de commande **Test-CsVoicePolicy** pour connaître l’itinéraire utilisé pour le routage de l’appel d’un utilisateur ayant une stratégie de voix spécifique, ainsi que l’utilisation du téléphone associé à la stratégie de cet itinéraire.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Test-CsVoicePolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Le numéro de téléphone qui doit être utilisé pendant le test. Le numéro doit être au format E.164 (tel que +14255551212).</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Référence à un objet de configuration de stratégie de voix à partir duquel le test doit être exécuté. Vous pouvez extraire des objets de stratégie de voix en appelant l’applet de commande <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation ou les messages d’erreur récupérable qui peuvent s’afficher lors de l’exécution de l’applet de commande.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Paramètres d’itinéraire pour lequel le test doit être exécuté. Les paramètres d’itinéraire peuvent être récupérés par un appel à l’applet de commande <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Accepte l’entrée redirigée pour les objets de stratégie de voix.

## Types de retours

Retourne un objet de type Microsoft.Rtc.Management.Voice.VoicePolicyTestResult.

## Voir aussi

#### Autres ressources

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

