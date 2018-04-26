---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412895(v=OCS.15)
ms:contentKeyID: 49298619
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un certificat précédemment marqué comme disponible par Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 supprime tous les certificats WebServicesExternal pouvant être utilisés par Lync Server. Si l’un de ces certificats est utilisé, vous serez invité à confirmer sa suppression pour que l’applet de commande **Remove-CsCertificate** puisse être exécutée. Pour ignorer l’invite de confirmation, utilisez le paramètre Force :

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## Description détaillée

Lync Server utilise des certificats pour vérifier l’identité des serveurs et des rôles serveur ; par exemple, un serveur Edge utilise des certificats pour vérifier que l’ordinateur avec lequel il communique est réellement un serveur frontal et inversement. Afin de mettre en œuvre Lync Server, vous devez avoir assigné les certificats qui conviennent aux rôles serveur appropriés.

L’applet de commande **Remove-CsCertificate** permet de supprimer les certificats actuellement utilisés dans Lync Server. L’applet de commande **Remove-CsCertificate** ne supprime pas le certificat lui-même. En revanche, le certificat ne peut plus être utilisé par Lync Server, ses liaisons sont supprimées et les autorisations d’accès sont annulées (à condition qu’aucun autre service n’utilise le certificat). Cela signifie notamment que le certificat n’apparaîtra plus lorsque vous exécuterez l’applet de commande **Get-CsCertificate**.

Pour réutiliser le certificat avec Lync Server, vous devrez réattribuer le certificat à Lync Server à l’aide de l’applet de commande **Set-CsCertificate**.

Si vous essayez de supprimer un certificat en cours d’utilisation, vous serez invité à confirmer sa suppression pour que l’applet de commande **Remove-CsCertificate** puisse être exécutée. Pour ignorer cette invite et supprimer un certificat sans assistance, même s’il est utilisé, ajoutez le paramètre Force à votre commande :

Remove-CsCertificate –Type WebServicesExternal -Force

Personnes autorisées à exécuter cette applet de commande : Vous devez être un administrateur local et un membre du domaine pour pouvoir exécuter localement l’applet de commande **Remove-CsCertificate**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Type de certificat à supprimer. Les types de certificats incluent notamment :</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (Microsoft Lync Online 2010 uniquement)</p>
<p>ProvisionService (Microsoft Lync Online 2010 uniquement)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>L’exemple suivant supprime le certificat Default : -Type Default.</p>
<p>Vous pouvez supprimer plusieurs types dans une seule et même commande en séparant les types de certificat par des virgules :</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ignore l’invite de confirmation qui s’affiche généralement lorsque vous essayez de supprimer un certificat en cours d’utilisation.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Quand sa valeur est Global, supprime le certificat de l’étendue globale. En l’absence de spécification, les certificats sont supprimés de l’ordinateur local.</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sa spécification permet de supprimer le certificat préalablement affecté au lieu du certificat actuellement affecté.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet d’enregistrer des informations détaillées sur les procédures exécutées par l’applet de commande <strong>Remove-CsCertificate</strong>. La valeur de ce paramètre doit indiquer le chemin d’accès complet au fichier HTML à générer (par exemple : -Report C:\Logs\Certificates.html). Si le fichier spécifié existe déjà, il sera automatiquement remplacé par les nouvelles informations.</p></td>
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

Aucun. L’applet de commande Remove-CsCertificate n’accepte pas l’entrée redirigée.

## Types de retours

Aucun. L’applet de commande **Remove-CsCertificate** supprime plutôt les instances de l’objet Microsoft.Rtc.Management.Deployment.CertificateReference.

## Voir aussi

#### Autres ressources

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

