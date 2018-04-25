---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59602879
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**Dernière rubrique modifiée :** 2015-03-09_

Met à jour l’URL de réunion pour le client Skype Entreprise Online spécifié. L’URL mise à jour utilise un format simplifié et standardisé qui permet aux clients de localiser les réunions et de s’y connecter.

Cette applet de commande est destinée à être utilisée uniquement avec Skype Entreprise Online.

## Syntaxe

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## Exemples

## Exemple 1

La commande incluse dans l’exemple 1 met à jour l’URL de la réunion pour le client associé à l’ID 38aad667-af54-4397-aaa7-e94c79ec2308. (Notez que vous devez fournir l’ID du client pour que cette commande puisse être exécutée.) Une fois que vous avez appuyé sur Entrée pour exécuter la commande, vous êtes invité à confirmer la mise à jour de l’URL de la réunion. Vous devez répondre oui à cette invite avant que Update-CsTenantMeetingUrl ne modifie vos paramètres de configuration Skype Entreprise Online.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## Exemple 2

L’exemple 2 met également à jour l’URL de la réunion pour le client associé à l’ID 38aad667-af54-4397-aaa7-e94c79ec2308. Dans ce cas, le paramètre Force est inclus. Il permet de contourner l’invite de confirmation qui apparaît généralement lorsque vous exécutez Update-CsTenantMeetingUrl. Dans ce cas, dès que vous appuyez sur Entrée, la commande est exécutée et vos paramètres de configuration Skype Entreprise Online sont modifiés.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## Description détaillée

L’applet de commande Update-CsTenantMeetingUrl met à jour l’URL de la réunion Skype Entreprise Online en utilisant un format simplifié et standardisé. Ceci permet d’éliminer les problèmes qui peuvent survenir avec l’URL d’origine de la réunion. Par exemple, supposons qu’une organisation définisse un domaine Office 365 avec le nom contoso.onmicrosoft.com. Dans ce cas, les réunions ont des URL semblables à celle-ci :

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

À présent, supposons que l’organisation applique quelques modifications et décide d’utiliser l’URL personnalisée litwareinc.com à la place de l’URL onmicrosoft.com. L’organisation modifie les adresses de messagerie des utilisateurs afin d’utiliser le domaine litwareinc.com. Toutefois, les URL de réunion utilisent toujours l’ancien nom de domaine :

https://meet.lync.com/contoso/user1/45GZFH99

Pour résoudre ce problème, les administrateurs doivent exécuter l’applet de commande Update-CsTenantMeetingUrl. Celle-ci permet de remplacer l’ancienne URL de la réunion par une nouvelle incluant l’URL personnalisée :

https://meet.lync.com/litwareinc.com/user1/37JYLP71

L’exécution de l’applet de commande Update-CsTenantMeetingUrl est la seule façon d’apporter cette modification.

Notez que, lorsque vous exécutez Update-CsTenantMeetingUrl, votre client Skype Entreprise Online bascule vers la nouvelle URL après un court délai de synchronisation. Ceci ne crée pas de problème pour les nouvelles réunions que vos utilisateurs peuvent programmer : ces réunions sont automatiquement planifiées avec la nouvelle URL. En revanche, les réunions précédemment planifiées rencontreront des problèmes, car celles-ci ont été planifiées à l’aide de l’ancienne URL de réunion devenue obsolète. La seule façon de résoudre ce problème consiste à demander à vos utilisateurs de modifier l’horaire de ces réunions.

Comme ceci peut potentiellement créer des problèmes dans certaines organisations (notamment les organisations dans lesquelles un grand nombre de réunions sont déjà planifiées), par défaut Update-CsTenantMeetingUrl transmet une invite avant de mettre à jour l’URL de la réunion :

AVERTISSEMENT : ceci constitue une modification avec rupture pour les utilisateurs dans ce client. La configuration de l’URL de la réunion sera mise à jour \! Les anciennes URL de réunion ne fonctionneront plus. Cette modification ne peut pas être annulée.  
Voulez-vous vraiment continuer ?  
\[Y\] Oui \[A\] Oui pour tout \[N\] Non \[L\] Non pour tout \[S\] Suspendre \[?\] Aide (« Y » est la valeur par défaut) :

Vous devez répondre « Oui » ou « Oui pour tout » avant que la commande ne soit exécutée. Si vous répondez « Non », la commande est annulée et l’URL de la réunion n’est pas mise à jour. Rappelez-vous qu’une fois l’URL de la réunion modifiée, il n’est pas possible de rétablir l’URL d’origine. Une fois que la commande est exécutée, l’URL est modifiée et toutes les réunions précédemment planifiées doivent être reprogrammées. Vous devez seulement exécuter cette commande une fois par client. Il n’est pas utile d’exécuter périodiquement la commande et de mettre à nouveau à jour l’URL de la réunion.

Si vous préférez exécuter la commande sans répondre à l’invite de confirmation, vous pouvez inclure le paramètre Force. Dans ce cas, Update-CsTenantMeetingUrl est exécutée sans afficher l’invite de confirmation :

AVERTISSEMENT : ceci constitue une modification avec rupture pour les utilisateurs dans ce client. La configuration de l’URL de la réunion sera mise à jour \!

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
<td><p><strong>Client</strong></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID du compte de client dont les paramètres de fédération sont retournés. Par exemple :</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Vous pouvez retourner l’ID de chacun de vos clients en exécutant la commande suivante :</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Si vous n’incluez par le paramètre Tenant, Update-CsMeetingUrl vous invite à entrer ce paramètre avant de continuer.</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirm</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p>
<p>Notez que la comportement par défaut de l’applet de commande Update-CsMeetingUrl consiste à afficher l’invite de confirmation avant d’effectuer des modifications. Aussi, si vous voulez afficher l’invite de confirmation, vous n’avez pas besoin d’inclure le paramètre Confirm.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de l’invite de confirmation qui apparaîtrait sinon avant que Update-CsMeetingUrl n’apporte des mises à jour.</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. Update-CsMeetingUrl n’accepte pas la saisie de données redirigées.

## Types de retours

Aucun.

## Voir aussi

#### Autres ressources

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

