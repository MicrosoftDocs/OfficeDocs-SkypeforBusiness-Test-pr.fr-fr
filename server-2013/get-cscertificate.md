---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398227(v=OCS.15)
ms:contentKeyID: 49296358
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les certificats des ordinateurs locaux qui ont été configurés pour être utilisés avec Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 renvoie des informations sur tous les certificats actuellement affectés aux composants de Lync Server. Cette opération est effectuée en appelant l’applet de commande **Get-CsCertificate** sans aucun paramètre supplémentaire.

    Get-CsCertificate

## EXEMPLE 2

L’exemple 2 illustre l’extraction de tous les certificats Lync Server utilisés pour les services web internes. Pour ce faire, on inclut le paramètre Type, conjointement avec la valeur de paramètre WebServicesInternal.

    Get-CsCertificate -Type WebServicesInternal

## EXEMPLE 3

L’exemple 3 renvoie tous les certificats Lync Server qui expirent avant le 1er septembre 2012. Pour exécuter cette tâche, la commande utilise d’abord l’applet de commande **Get-CsCertificate** pour renvoyer un ensemble de tous les certificats Lync Server actuellement utilisés. Cet ensemble est ensuite redirigé vers l’applet de commande **Where-Object**, qui sélectionne uniquement les certificats qui expirent avant le 1er septembre 2012. La date spécifiée dans cet exemple (9/1/2012) utilise le format de date anglais américain. Le format des dates doit être compatible avec votre langue et vos paramètres régionaux.

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## EXEMPLE 4

L’exemple 4 renvoie des informations sur tous les certificats Lync Server émis par l’autorité de certification (CA) MyCa. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsCertificate** sans aucun paramètre afin de renvoyer un ensemble de tous les certificats actuellement utilisés. Cet ensemble est ensuite redirigé vers l’applet de commande **Where-Object**, qui sélectionne tous les certificats dont la propriété Issuer est égale à (-eq) « Cn=MyCa ».

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## EXEMPLE 5

La commande illustrée dans l’exemple 5 renvoie tous les certificats Lync Server dont la propriété Subject a été définie sur CN=atl-cs-001.litwareinc.com. Cette opération est effectuée en utilisant l’applet de commande **Get-CsCertificate** pour renvoyer un ensemble de tous les certificats Lync Server, puis en redirigeant ce dernier vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** sélectionne ensuite uniquement les certificats dont la propriété Subject est égale à CN=atl-cs-001.litwareinc.com.

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## Description détaillée

Lync Server utilise des certificats pour vérifier l’identité des serveurs et des rôles serveur ; par exemple, un serveur Edge utilise des certificats pour vérifier que l’ordinateur avec lequel il communique est réellement un serveur frontal et inversement. Pour que vous puissiez implémenter intégralement Lync Server, les certificats appropriés doivent être attribués aux rôles serveur adéquats.

L’applet de commande **Get-CsCertificate** vous permet d’extraire des informations détaillées sur les certificats qui ont été configurés pour être utilisés avec Lync Server. Notez que l’applet de commande renvoie uniquement des informations sur les certificats Lync Server. Si un certificat n’a pas été configuré pour être utilisé avec Lync Server (via l’applet de commande **Set-CsCertificate**), il ne sera pas renvoyé lors de l’exécution de l’applet de commande **Get-CsCertificate**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsCertificate** : RTCUniversalServerAdmins.

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
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Permet d’extraire des certificats configurés dans l’étendue globale (les certificats globaux sont copiés et distribués sur les ordinateurs appropriés). Utilisez cette syntaxe pour retourner des informations sur les certificats globaux :</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet d’enregistrer des informations détaillées sur les procédures exécutées par l’applet de commande <strong>Get-CsCertificate</strong>. La valeur de ce paramètre doit indiquer le chemin d’accès complet au fichier HTML à générer (par exemple : -Report C:\Logs\Certificates.html). Si le fichier spécifié existe déjà, il sera automatiquement remplacé par les nouvelles informations.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Type du certificat demandé. Les types de certificats incluent notamment :</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (Microsoft Lync Online 2010 uniquement)</p>
<p>ProvisionService (Microsoft Lync Online 2010 uniquement)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Par exemple, cette syntaxe retourne des informations sur le certificat Default : -Type Default.</p>
<p>Vous pouvez spécifier plusieurs types dans une seule et même commande en séparant les types de certificat par des virgules :</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsCertificate** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsCertificate** renvoie des instances de l’objet Microsoft.Rtc.Management.Deployment.CertificateReference.

## Voir aussi

#### Autres ressources

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

