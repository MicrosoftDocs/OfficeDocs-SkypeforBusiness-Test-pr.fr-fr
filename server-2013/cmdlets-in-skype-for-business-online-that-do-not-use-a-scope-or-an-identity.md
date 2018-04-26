---
title: Applets de commande n’utilisant pas une étendue ou une identité
TOCTitle: Applets de commande n’utilisant pas une étendue ou une identité
ms:assetid: 9c50c732-3c64-4b6a-96fd-8f528eb739ce
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362824(v=OCS.15)
ms:contentKeyID: 56269638
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applets de commande n’utilisant pas une étendue ou une identité

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les applets de commande utilisées pour modifier les listes de domaines autorisés et bloqués (listes déterminant les organisations externes avec lesquelles vos utilisateurs peuvent communiquer) n’utilisent ni étendue, ni identité. En réalité, l’applet de commande **New-CsEdgeAllowAllKnownDomains** n’inclut aucun paramètre. Les applets de commande suivantes n’utilisent ni étendue, ni identité :

  - [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)

  - [New-CsEdgeAllowList](new-csedgeallowlist.md)

  - [New-CsEdgeDomainPattern](new-csedgedomainpattern.md)

Notez que vous devez inclure le paramètre Domaine avec les applets de commande **New-CsEdgeAllowList** et **New-CsEdgeDomainPattern**. Par exemple :

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

## Voir aussi

#### Concepts

[Identités, étendues et clients](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Applets de commande de Lync Online](the-skype-for-business-online-cmdlets.md)

