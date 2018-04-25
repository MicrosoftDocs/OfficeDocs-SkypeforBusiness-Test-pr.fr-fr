---
title: Paramètres obligatoires et facultatifs
TOCTitle: Paramètres obligatoires et facultatifs
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56269667
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Paramètres obligatoires et facultatifs

 

_**Dernière rubrique modifiée :** 2015-06-22_

Les paramètres Windows PowerShell appartiennent à une des deux catégories suivantes : paramètres obligatoires ou paramètres facultatifs. Un *paramètre obligatoire* doit être inclus lorsque vous exécutez la commande. Par exemple, l’applet de commande [Remove-CsUserAcp](remove-csuseracp.md) permet d’annuler l’affectation d’un fournisseur de services d’audioconférence précédemment affecté à un utilisateur. Lorsque vous exécutez l’applet de commande **the Remove-CsUserAcp**, vous devez inclure le paramètre Identity. Ce paramètre indique à l’applet de commande l’utilisateur pour lequel le fournisseur de services d’audioconférence doit être supprimé. Évidemment, l’exécution de cette commande sans paramètre n’a pas de sens :

    Remove-CsUserAcp

Dans un cas comme celui-ci, l’applet de commande ne pourrait pas identifier l’utilisateur pour lequel il convient de supprimer le fournisseur de services d’audioconférence. Vous devez donc spécifier l’identité de l’utilisateur :

    Remove-CsUserAcp -Identity "Ken Myer"

En général, Windows PowerShell affiche une invite si vous omettez un paramètre obligatoire lorsque vous tentez d’exécuter une commande. Par exemple, vous pouvez taper la commande suivante, puis appuyer sur Entrée :

    Remove-CsUserAcp

Si vous procédez ainsi, Windows PowerShell n’exécute pas cette commande incomplète, mais vous invite à entrer le paramètre obligatoire manquant :

    applet de commande Remove-CsUserAcp à la position 1 du pipeline de la commande
    Fournissez des valeurs pour les paramètres suivants :
    Identity :

Si vous entrez un paramètre Identity valide et appuyez sur Entrée, Windows PowerShell exécutera l’applet de commande **Remove-CsUserAcp** et supprimera le fournisseur de services d’audioconférence. Si vous changez d’avis et décidez de ne pas exécuter la commande, appuyez sur Ctrl-C pour terminer la commande.

Il ne s’agit pas d’un système infaillible : Windows PowerShell n’est pas toujours en mesure de vous demander l’ensemble des paramètres requis. Par exemple, certaines applets de commande sont construites de telle sorte que le paramètre A ou le paramètre B (mais pas les deux) sont obligatoires. Windows PowerShell peut vous demander de renseigner les paramètres A et B. Pour autant, la commande finira par échouer, car vous ne pouvez pas utiliser les paramètres A et B dans la même commande. En raison de cas comme celui-ci, il est recommandé d’inclure tous les paramètres obligatoires avant d’exécuter la commande, et de ne pas compter uniquement sur Windows PowerShell pour vous demander ceux-ci.

Notez également que la mise en forme de la valeur de paramètre peut parfois être un processus non intuitif. Par exemple, lorsque vous incluez une valeur de paramètre contenant un espace vide, vous devez entourer celle-ci de guillemets doubles :

    -Identity "Ken Myer"

Toutefois, l’utilisation de guillemets est nécessaire lorsque vous tapez le paramètre et la valeur de paramètre dans le cadre de la commande devant être exécutée. Si vous essayez d’exécuter l’applet de commande **Remove-CsUserAcp** sans renseigner le paramètre Identity, Windows PowerShell vous invite à indiquer l’identité de l’utilisateur :

    applet de commande Remove-CsUserAcp à la position 1 du pipeline de la commande
    Fournissez des valeurs pour les paramètres suivants :
    Identity :

Tapez ensuite Ken Myer avec le paramètre Identity entouré de guillemets doubles :

    applet de commande Remove-CsUserAcp à la position 1 du pipeline de la commande
    Fournissez des valeurs pour les paramètres suivants :
    Identity : "Ken Myer"

Si vous procédez ainsi, la commande échoue avec le message d’erreur suivant :

    Remove-CsUserAcp : Objet de gestion introuvable pour l'identité ""Ken Myer"".

Dans ce cas, recherchez l’utilisateur associé à l’identité "Ken Myer", avec les guillemets doubles inclus dans le cadre du paramètre Identity. Si vous êtes invité à entrer une valeur de paramètre, n’incluez pas les guillemets doubles :

    applet de commande Remove-CsUserAcp à la position 1 du pipeline de la commande
    Fournissez des valeurs pour les paramètres suivants :
    Identity : Ken Myer

En comparaison, un *paramètre facultatif* est exactement ce que son nom implique : il n’est pas impératif que le paramètre soit entré pour exécuter l’applet de commande. Par exemple, l’applet de commande Remove-CsUserAcp est associée au paramètre facultatif Name. Si le paramètre Name est inclus dans la commande, seul le fournisseur de services d’audioconférence spécifié est supprimé. La commande suivante supprime le fournisseur de services d’audioconférence nommé Fabrikam ACP, mais ne supprime pas les autres fournisseurs de services d’audioconférence affectés à Ken Myer :

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

Si vous ne renseignez pas ce paramètre facultatif, la commande est tout de même exécutée. Dans ce cas, l’applet de commande Remove-CsUserAcp supprime tous les fournisseurs de services d’audioconférence affectés à Ken Myer :

    Remove-CsUserAcp -Identity "Ken Myer"

## Voir aussi

#### Concepts

[Présentation de Windows PowerShell et Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

