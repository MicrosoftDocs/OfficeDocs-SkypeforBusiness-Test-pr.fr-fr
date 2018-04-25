---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425723(v=OCS.15)
ms:contentKeyID: 49296583
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet de demander des certificats à utiliser avec des serveurs exécutant Lync Server et des rôles serveur. Permet également de vérifier l’état des demandes de certificats en cours et, si nécessaire, d’annuler une ou l’ensemble de ces demandes. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 crée une nouvelle demande de certificat : elle contacte l’autorité de certification atl-ca-001.litwareinc.com\\myca et demande un nouveau certificat WebServicesExternal.

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## EXEMPLE 2

L’exemple 2 répertorie toutes les demandes de certificats en cours qui ont été soumises au moyen de l’applet de commande **Request-CsCertificate**.

    Request-CsCertificate -List

## EXEMPLE 3

L’exemple 3 utilise le paramètre Output pour créer une demande de certificat hors connexion.

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## EXEMPLE 4

L’exemple 4 est un exemple plus complet (et plus réaliste) de la manière d’utiliser l’applet de commande Request-CsCertificate. Cet exemple demande un certificat à utiliser avec l’édition standard de Lync Server.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## EXEMPLE 5

Dans l’exemple 5, un certificat de pool est demandé pour une utilisation avec Lync Server Enterprise Edition.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## EXEMPLE 6

L’exemple 6 vous indique comment demander un certificat pour le serveur Edge interne.

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## EXEMPLE 7

L’exemple 7 est une variante de la commande présentée dans l’exemple 6. Néanmoins, dans ce cas, la demande concerne le serveur Edge externe.

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## Description détaillée

Lync Server utilise des certificats pour vérifier l’identité des serveurs et des rôles serveur ; par exemple, un serveur Edge utilise des certificats pour vérifier que l’ordinateur avec lequel il communique est réellement un serveur frontal et inversement. Pour permettre une mise en place complète de Lync Server, les certificats appropriés devront être attribués aux rôles serveur adéquats.

Pour demander des certificats à utiliser avec Lync Server, vous pouvez appeler l’applet de commande **Request-CsCertificate**. Bien que vous puissiez utiliser d’autres outils Windows standard pour demander des certificats à utiliser avec Lync Server, l’un des atouts de l’utilisation de l’applet de commande **Request-CsCertificate** est qu’elle analysera votre topologie avant de contacter l’autorité de certification. En fonction de cette analyse, l’applet de commande **Request-CsCertificate** demandera automatiquement un certificat comportant les champs Nom de l’objet et Autre nom de l’objet appropriés.

L’applet de commande **Request-CsCertificate** est conçue pour demander des certificats à utiliser spécifiquement avec Lync Server. Elle n’est pas conçue pour servir d’outil de gestion de certificats multifonction.

Outre la possibilité de demander de nouveaux certificats, cette applet de commande peut également permettre de consulter les demandes de certificats en cours, à condition qu’elles aient été soumises au moyen de l’applet de commande **Request-CsCertificate**. L’applet de commande **Request-CsCertificate** peut également être utilisée pour supprimer des demandes de certificats en cours, à condition qu’elles aient été émises à l’aide de cette même applet de commande.

Lorsque vous essayez de récupérer des demandes de certificats, vous pouvez recevoir un message d’erreur si vous avez des demandes révoquées ; pour l’instant, l’applet de commande **Request-CsCertificate** ne prend en charge que les types de demande suivants : Issued, Denied et Pending. Si vous rencontrez des problèmes liés à un certificat révoqué, utilisez une commande similaire à celle-ci pour effacer la demande révoquée (où 224 est la valeur RequestID de la demande de certificat révoquée) :

Request-CsCertificate –Clear –RequestID 224

Après cela, vous devriez être en mesure de récupérer les demandes de certificats.

Personnes autorisées à exécuter cette applet de commande : Vous devez être un administrateur local et disposer des droits d’accès à l’autorité de certification spécifiée pour exécuter localement l’applet de commande **Request-CsCertificate**. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, ce paramètre supprime toutes les demandes de certificats en cours soumises à l’aide de l’applet de commande <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, ce paramètre répertorie toutes les demandes de certificats en cours et soumises au moyen de l’applet de commande <strong>Request-CsCertificate</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, ce paramètre indique que vous souhaitez demander un nouveau certificat.</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, ce paramètre récupère les demandes de certificats en cours et soumises au moyen de l’applet de commande <strong>Request-CsCertificate</strong>, puis il tente de mener à terme l’opération et d’importer le certificat demandé.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Type du certificat demandé. Les types de certificat sont notamment les suivants :</p>
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
<p>Par exemple, cette syntaxe demande un nouveau certificat de type Default : -Type Default.</p>
<p>Vous pouvez spécifier plusieurs types dans une seule et même commande en séparant les types de certificat par des virgules :</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>S’il est présent, ce paramètre indique que tous vos domaines SIP sont automatiquement ajoutés au champ Autre nom du sujet des certificats. S’il est absent, seul le domaine SIP principal est ajouté par défaut. Toutefois, il est possible de spécifier des domaines supplémentaires à l’aide du paramètre DomainName.</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de domaine complet (FQDN) pointant sur l’autorité de certification. Par exemple : -CA &quot;atl-ca-001.litwareinc.com\myca&quot;. Pour obtenir une liste des autorités de certification connues, tapez ce qui suit à l’invite Windows PowerShell, puis appuyez sur Entrée :</p>
<p>certutil</p>
<p>La propriété Config retournée par Certutil indique l’emplacement d’une autorité de certification.</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom du compte de l’utilisateur demandant le nouveau certificat, au format nom_domaine\nom_utilisateur. Par exemple : -CaAccount &quot;litwareinc\kenmyer&quot;. Si rien n’est spécifié, l’applet de commande <strong>Request-CsCertificate</strong> utilisera les informations d’identification de l’utilisateur connecté lors de la demande du nouveau certificat.</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Mot de passe de l’utilisateur demandant le nouveau certificat (spécifié à l’aide du paramètre CaAccount).</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Ville dans laquelle le certificat sera déployé.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Définissez la valeur de ce paramètre sur True si le certificat doit être utilisé pour l’authentification client. Ce type d’authentification est requis si vous souhaitez que vos utilisateurs puissent échanger des messages instantanés avec des personnes disposant de comptes AOL. La portion EKU du nom du paramètre est l’abréviation d’Extended Key Usage (utilisation améliorée de la clé) ; le champ EKU dresse l’inventaire des usages autorisés du certificat.</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet de l’ordinateur pour lequel le certificat est demandé. S’il est présent, ce paramètre force l’applet de commande <strong>Request-CsCertificate</strong> à se connecter au magasin central de gestion pour localiser l’ordinateur spécifié. Vous devriez toujours utiliser le nom de l’ordinateur lors de vos demandes de certificats, même pour un certificat de pool. L’applet de commande <strong>Request-CsCertificate</strong> ajoutera automatiquement le nom du pool au champ du nom de l’objet pour chaque certificat obtenu au moyen de cette applet de commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Pays/région dans lequel/laquelle le certificat sera déployé.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Liste de valeurs (séparées par des virgules) de noms de domaines complets devant être ajoutés au champ Autre nom du sujet du certificat. Par exemple :</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom attribué par l’utilisateur pour faciliter l’identification du certificat.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN) d’un serveur de catalogue global dans votre domaine. Ce paramètre n’est pas obligatoire si vous exécutez l’applet de commande <strong>Request-CsCertificate</strong> sur un ordinateur disposant d’un compte dans votre domaine.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet d’un contrôleur de domaine dans lequel les paramètres globaux sont stockés. Si les paramètres globaux sont stockés dans le conteneur Système des services de domaine Active Directory, ce paramètre doit pointer sur le contrôleur de domaine racine. Si les paramètres globaux sont stockés dans le conteneur de configuration, tout contrôleur de domaine peut être utilisé et ce paramètre peut être omis.</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>Indique le type d’algorithme de chiffrement à utiliser lors de la génération de clés publiques et privées pour le nouveau certificat. Les algorithmes de clés valides incluent :</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Indique la taille (en bits) de la clé privée utilisée par le certificat. Les clés de grande taille sont plus sécurisées, mais sont plus difficiles à déchiffrer.</p>
<p>Les tailles de clés valides sont 1024, 2048 et 4096. Par exemple : -KeySize 2048.</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Nom de l’organisation demandant le nouveau certificat. Par exemple : -Organization &quot;Litwareinc&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Unité d’organisation Active Directory de l’ordinateur auquel le nouveau certificat sera attribué.</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Chemin d’accès au fichier de certificat. Si vous souhaitez créer une demande de certificat hors connexion, utilisez le paramètre Output et spécifiez un chemin d’accès au fichier pour la demande de certificat (par exemple : -Output C:\Certificates\NewCertificate.pfx). Ce paramètre créera un fichier de demande de certificat que vous pourrez transmettre ensuite à une autorité de certification pour traitement.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Définissez la valeur de ce paramètre sur True si vous souhaitez exporter la clé privée du certificat. Lorsqu’une clé privée est exportable, le certificat peut être copié et utilisé sur plusieurs ordinateurs.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet de spécifier un chemin d’accès au fichier journal créé lors de l’exécution de l’applet de commande. Par exemple : -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Numéro d’identification associé à une demande de certificat. Le paramètre RequestID vous permet de répertorier, récupérer ou supprimer un certificat individuel.</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>État des États-Unis dans lequel le certificat sera déployé. Par exemple : -State WA.</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Indique le modèle de certificat à utiliser lors de la génération du nouveau certificat (par exemple : -Template &quot;WebServer&quot;). Le modèle demandé doit être installé sur l’autorité de certification. Notez que la valeur saisie doit correspondre au nom du modèle, et non au nom complet du modèle.</p></td>
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

Aucun. L’applet de commande **Request-CsCertificate** n’accepte pas l’entrée redirigée.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Request-CsCertificate** aide à gérer les instances de l’objet Microsoft.Rtc.Management.Deployment.CertificateReference.

## Voir aussi

#### Autres ressources

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

