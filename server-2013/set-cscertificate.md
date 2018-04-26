---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398518(v=OCS.15)
ms:contentKeyID: 49297555
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet d’affecter un certificat à un serveur ou un rôle serveur Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée à l’exemple 1 affecte le certificat à l’empreinte numérique B142918E463981A76503828BB1278391B716280987B au rôle WebServicesExternal sur l’ordinateur local.

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## EXEMPLE 2

L’exemple 2 assigne le certificat avec l’empreinte numérique B142918E463981A76503828BB1278391B716280987B à trois rôles différents sur l’ordinateur local : Default, WebServicesInternal et WebServicesExternal.

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## Description détaillée

Lync Server utilise des certificats pour vérifier l’identité des serveurs et des rôles serveur ; par exemple, un serveur Edge utilise des certificats pour vérifier que l’ordinateur avec lequel il communique est réellement un serveur frontal et inversement. Afin de mettre en œuvre Lync Server à part entière, vous devez avoir assigné les certificats qui conviennent aux rôles serveur appropriés.

L’applet de commande **Set-CsCertificate** permet aux administrateurs d’assigner un certificat à un serveur ou un rôle serveur. Notez que vous ne pouvez assigner que des certificats qui ont déjà été configurés pour être utilisés avec Lync Server. Pour identifier les certificats disponibles qui doivent être assignés, utilisez l’applet de commande **Get-CsCertificate**.

Personnes autorisées à exécuter cette applet de commande : Vous devez être administrateur local pour pouvoir exécuter localement l’applet de commande **Set-CsCertificate**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Lorsqu’il est défini sur Global, le certificat peut fonctionner au niveau global. Les certificats globaux sont automatiquement copiés et distribués sur les ordinateurs appropriés.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Chemin complet d’accès au fichier de certificat .PFX.</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>Référence d’objet à un certificat configuré pour être utilisé avec Lync Server. La commande suivante retourne une référence d’objet (la variable $x) qui représente un certificat avec l’empreinte numérique B142918E463981A76503828BB1278391B716280987B:</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Identificateur unique du certificat. Une empreinte numérique de certificat ressemble à ceci : B142918E463981A76503828BB1278391B716280987B.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Type du certificat affecté. Les types de certificats incluent notamment :</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>Externe</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (Microsoft Lync Online 2010 uniquement)</p>
<p>ProvisionService (Microsoft Lync Online 2010 uniquement)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Par exemple, cette syntaxe affecte le certificat Default : -Type Default.</p>
<p>Vous pouvez spécifier plusieurs types dans une seule et même commande en séparant les types de certificat par des virgules :</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.DateTime</p></td>
<td><p>Date et heure de première utilisation du certificat. Par exemple, pour configurer un certificat utilisable pour la première fois au 31 juillet 2012 à 08 h, utilisez la syntaxe suivante sur un serveur ayant comme paramètres régionaux et linguistiques Anglais (États-Unis) :</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Mot de passe du certificat.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet d’enregistrer des informations détaillées concernant les procédures mises en œuvre par l’applet de commande <strong>Set-CsCertificate</strong>. La valeur de paramètre doit être le chemin complet au fichier HTML à générer, par exemple : -Report C:\Logs\Certificates.html. Si le fichier spécifique existe déjà, il sera automatiquement supprimé et remplacé par les nouvelles informations.</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Permet de mettre à jour le certificat spécifié à la date et à l’heure spécifiées par le paramètre EffectiveDate ; vous pouvez ainsi spécifier une date et une heure où le nouveau certificat deviendra le certificat principal. Notez que votre commande échouera si vous spécifiez le paramètre Roll sans inclure le paramètre EffectiveDate.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Microsoft.Rtc.Management.Deployment.CertificateReference.

## Types de retours

L’applet de commande **Set-CsCertificate** ne retourne ni valeur ni objet.

## Voir aussi

#### Autres ressources

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

