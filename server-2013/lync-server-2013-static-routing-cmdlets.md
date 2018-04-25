---
title: Cmdlets de routage statique
TOCTitle: Cmdlets de routage statique
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg416492(v=OCS.15)
ms:contentKeyID: 49297698
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets de routage statique

 

_**Dernière rubrique modifiée :** 2016-12-08_

Grâce aux itinéraires statiques, les administrateurs peuvent déterminer à l’avance les itinéraires réseau empruntés par les messages SIP. Quand un message est reçu par un serveur, le serveur contrôle l’adresse du message puis transfère le message au serveur du tronçon suivant préconfiguré par un administrateur. S’ils sont configurés correctement, les itinéraires statiques contribuent à assurer une remise précise et en temps voulu des messages, tout en garantissant une charge minime sur les serveurs.

## Applets de commande de routage statique

Sauf mention contraire du personnel du support technique Microsoft, les itinéraires statiques configurés pour Microsoft Lync Server 2013 doivent être créés à l’aide de l’applet de commande [New-CsStaticRoute](new-csstaticroute.md). Une fois qu’un itinéraire a été créé, vous pouvez alors utiliser les applets de commande CsStaticRoutingConfiguration pour l’ajouter à la collection de routage statique.

**Routage statique**

  -   
    [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  -   
    [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  -   
    [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  -   
    [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  -   
    [New-CsStaticRoute](new-csstaticroute.md)

  -   
    [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  -   
    [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  -   
    [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  -   
    [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  -   
    [New-CsSipProxyCustom](new-cssipproxycustom.md)

  -   
    [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  -   
    [New-CsSipProxyTCP](new-cssipproxytcp.md)

  -   
    [New-CsSipProxyTLS](new-cssipproxytls.md)

  -   
    [New-CsSipProxyTransport](new-cssipproxytransport.md)

  -   
    [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  -   
    [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  -   
    [New-CsIssuedCertId](new-csissuedcertid.md)

## Voir aussi

#### Autres ressources

[Blog Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x40c)

