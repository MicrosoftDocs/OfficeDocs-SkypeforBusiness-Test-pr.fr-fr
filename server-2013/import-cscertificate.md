---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398688(v=OCS.15)
ms:contentKeyID: 49297965
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**Dernière rubrique modifiée :** 2015-03-09_

Importe un certificat à utiliser avec Lync Server. Si un certificat n’est pas acquis par l’utilisation de l’applet de commande **Request-CsCertificate**, il doit être importé pour pouvoir être affecté à un rôle serveur Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 importe le certificat C:\\Certificates\\WebServer.pfx. Après l’exécution de la commande, le certificat est disponible pour être affecté à un rôle serveur.

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## Description détaillée

Lync Server utilise des certificats pour vérifier l’identité des serveurs et des rôles serveur ; par exemple, un serveur Edge utilise des certificats pour vérifier que l’ordinateur avec lequel il communique est réellement un serveur frontal et inversement. Pour pouvoir implémenter complètement Lync Server, vous devez affecter les certificats appropriés aux rôles de serveur appropriés.

Pour pouvoir affecter des certificats à un rôle Lync Server, Lync Server doit avoir connaissance de ces certificats. L’applet de commande **Request-CsCertificate** vous permet d’effectuer des demandes en ligne et hors connexion de nouveaux certificats. Dans le cas d’une demande en ligne, le certificat est automatiquement téléchargé et enregistré dans le magasin de certificats local. Tout aussi important, il sera immédiatement mis à la disposition de Lync Server. S’il s’agit d’une demande hors connexion, un fichier de certificat vous sera envoyé. À ce stade, vous pouvez utiliser l’applet de commande **Import-CsCertificate** pour importer le certificat, un processus qui rend le certificat disponible pour l’affectation à un rôle serveur Lync Server.

Personnes autorisées à exécuter cette applet de commande : Seul un administrateur local peut exécuter localement l’applet de commande **Import-CsCertificate**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p>Quand la valeur est Global, le certificat peut fonctionner au niveau global. Les certificats globaux sont automatiquement copiés et distribués sur les ordinateurs appropriés.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Chemin complet d’accès au fichier de certificat à importer. Par exemple : –Path &quot;C:\Certificates\WebServer.cer&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Type du certificat demandé. Les types de certificat sont, entre autres, les suivants :</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
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
<td><p>Date et heure auxquelles le certificat peut être utilisé pour la première fois. Par exemple, pour configurer un certificat pour une première utilisation à 08 H 00 le 31 juillet 2012, utilisez cette syntaxe sur un serveur qui utilise les paramètres régionaux Anglais (États-Unis) :</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
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
<td><p>Mot de passe associé au fichier de certificat.</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Si vous définissez la valeur True, vérifiez que la partie de la clé privée du certificat peut être lue par le compte Service réseau.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Permet de mettre à jour le certificat spécifié à la date et à l’heure spécifiées par le paramètre EffectiveDate ; vous pouvez ainsi spécifier une date et une heure où le nouveau certificat deviendra le certificat principal. Notez que votre commande échouera si vous spécifiez le paramètre Roll sans inclure le paramètre EffectiveDate.</p></td>
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

Aucun. L’applet de commande **Import-CsCertificate** n’accepte pas les données redirigées.

## Types de retours

Aucun.

## Voir aussi

#### Autres ressources

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

