---
title: Utilisation des paramètres
TOCTitle: Utilisation des paramètres
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56269571
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilisation des paramètres

 

_**Dernière rubrique modifiée :** 2015-06-22_

Lorsque vous utilisez le paramètre Identity, vous remarquerez que la valeur de paramètre kenmyer@litwareinc.com est entourée de guillemets doubles :

    -Identity "kenmyer@litwareinc.com"

Les personnes qui débutent avec Windows PowerShell s’interrogent invariablement sur l’utilisation des guillemets doubles. S’il n’y a pas de réponse simple à cette question, vous pouvez tout de même suivre quelques règles générales :

  - Les guillemets doubles ne sont généralement pas requis lorsque la valeur de paramètre est un nombre. Par exemple, pour limiter le nombre d’utilisateurs retournés par l’applet de commande [Get-CsOnlineUser](get-csonlineuser.md), utilisez la syntaxe suivante :
    
        -ResultSize 100
    
    En fait, vous ne devez jamais placer des guillemets doubles autour d’un nombre, sans quoi Windows PowerShell peut rencontrer des difficultés à interpréter la valeur en tant que nombre.
    
    De même, vous devez veiller à ne pas inclure de virgules dans un nombre. Par exemple, si vous voulez définir une taille des résultats de 10,000, la syntaxe suivante serait incorrecte :
    
        -ResultSize 10,000
    
    Cette syntaxe crée une erreur, car Windows PowerShell utilise la virgule pour séparer les valeurs d’argument. Dans ce cas, Windows PowerShell suppose que vous transmettez deux valeurs de paramètre distinctes : 10 et 000. Comme vous ne pouvez pas définir une taille de résultat sur 10 et 0 simultanément, une erreur se produit. Vous devez utiliser la syntaxe suivante sans virgule à la place :
    
        -ResultSize 10000

  - Les guillemets doubles ne sont généralement pas requis lorsque la valeur de paramètre est une date :
    
        -StartDate 6/1/2013
    
    Ceci ne s’applique toutefois que lorsque l’heure n’est pas incluse. Si vous incluez l’heure (ce qui implique de placer un espace vide entre la date et l’heure), la valeur de paramètre doit être entourée de guillemets doubles :
    
        -StartDate "6/1/2013 10:00AM"
    
    Rappelez-vous que la commande précédente est mise en forme pour les ordinateurs qui utilisent la valeur Anglais (États-Unis) comme options régionales. Si vous n’utilisez pas l’Anglais (États-Unis), vous devez mettre en forme les dates et heures sur la base des paramètres de votre ordinateur. Pour vérifier les options régionales utilisées par Windows PowerShell, exécutez cette commande à partir de l’invite Windows PowerShell :
    
        Get-Host | Select-Object CurrentUICulture

  - Les valeurs de chaîne (telles que le nom d’une personne) ne requièrent généralement pas de guillemets doubles. Les exceptions principales surviennent lorsque cette valeur de chaîne inclut des caractères interdits, tels qu’un espace vide, une virgule ou d’autres marques de ponctuation. Par exemple, cette syntaxe fonctionne parce que l’identité de l’utilisateur n’inclut aucun caractère interdit :
    
        -Identity "kenmyer@litwareinc.com"
    
    Par contre, la commande suivante échouera, car le paramètre Identity inclut un espace vide :
    
        -Identity Ken Myer
    
    La commande précédente échoue, car Windows PowerShell utilise des espaces vides pour séparer les paramètres individuels. Windows PowerShell suppose alors que le paramètre Identity est Ken et que Myer est un nouveau paramètre. Vous recevrez donc le message d’erreur suivant :
    
        Get-CsOnlineUser : Impossible de trouver un paramètre positionnel acceptant l'argument « Myer ».
    
    Pour utiliser une valeur de paramètre incluant un espace vide (ou une virgule ou tout autre caractère interdit), placez la valeur entre des guillemets doubles :
    
        -Identity "Ken Myer"
    
    Le plus souvent, Windows PowerShell vous permet d’utiliser des guillemets simples plutôt que des guillemets doubles. Par exemple, ceci est une syntaxe Windows PowerShell valide :
    
        -Identity 'Ken Myer'
    
    Notez que vous devez toutefois utiliser le même type de guillemet au début et à la fin de la chaîne. Ceci n’est pas une syntaxe Windows PowerShell valide :
    
        -Identity "Ken Myer'
    
    Si vous essayez d’exécuter cette commande, la console Windows PowerShell affiche ce qui suit :
    
    ``` 
    >>
    ```
    
    La double flèche vous invite à compléter votre commande : comme vous avez commencé avec des guillemets doubles, Windows PowerShell s’attend à ce que vous finissiez de la même façon. Si vous recevez l’invite \>\>, appuyez sur Ctrl-C pour annuler votre commande, puis réessayez.

  - Les guillemets doubles ne doivent pas être utilisés avec des valeurs booléennes (True/False). Notez également que vous devez utiliser les variables Windows PowerShell $True et $False lorsque vous spécifiez les valeurs True/False, par exemple :
    
        -EnterpriseVoiceEnabled $True

Certains paramètres Windows PowerShell appelés *paramètres de commutateur* n’acceptent pas de valeur de paramètre :

    -WhatIf

Non seulement les valeurs de paramètre ne sont pas requises lorsque vous utilisez un paramètre de commutateur, mais l’inclusion d’une valeur de paramètre entraîne une erreur. Par exemple, si vous essayez d’exécuter la commande suivante :

    -WhatIf $True

Celle-ci échouera avec un message d’erreur semblable à celui-ci :

    Set-CsUserAcp : Impossible de trouver un paramètre positionnel acceptant l'argument « True ».

La possibilité de gérer Skype Entreprise Online à l’aide de Windows PowerShell nécessite que vous connaissiez les applets de commande pouvant être utilisées. Vous devez également connaître les paramètres disponibles pour chaque applet de commande, ainsi que le *type de données* de chaque paramètre (c’est à dire, si le paramètre accepte une valeur de date, une valeur de chaîne, un nombre, etc.). Ces informations (ainsi que divers exemples d’utilisation des applets de commande) sont disponibles dans les rubriques d’aide sur les applets de commande Skype Entreprise Online. Voici par exemple les paramètres utilisables avec l’applet de commande [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) :

![Paramètres d’une applet de commande PowerShell spécifique](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "Paramètres d’une applet de commande PowerShell spécifique")

Comme vous pouvez le voir, le tableau des paramètres fournit une description de l’applet de commande : il précise si le paramètre est obligatoire ou facultatif, et spécifie le type de données de chaque paramètre. Notez que le type de données indiqué dans le tableau est le type de données officiel utilisé par .NET Framework : celui-ci est donc indiqué en tant que paramètre System.Management.Automation.SwitchParameter et non de paramètre de commutateur simplement. Voici un guide rapide des types de données les plus fréquemment utilisés par les applets de commande Skype Entreprise Online :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Valeur de chaîne représentant l’identité d’un utilisateur. Il s’agit généralement du nom principal ou de l’adresse SIP de l’utilisateur :</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nom de domaine complet (FQDN est l'acronyme de fully qualified domain name). Par exemple :</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>Une valeur booléenne est une valeur True/False. Rappelez-vous que vous devez utiliser les variables Windows PowerShell $True et $False lorsque vous spécifiez des valeurs booléennes :</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>System.Guid</p></td>
<td><p>GUID est l’acronyme de <em>globally unique identifier</em>. Cet identificateur global unique est affecté dans Skype Entreprise Online à chaque client Skype Entreprise Online. Voici un exemple :</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>Vous pouvez récupérer le GUID affecté à vos clients Skype Entreprise Online à l’aide de la commande suivante :</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Les paramètres de commutateur sont nommés ainsi, car ils sont activés ou désactivés. Si le paramètre est présent, le commutateur est activé. S’il est absent, le commutateur est désactivé. Par exemple, pour utiliser le paramètre Confirm pour demander une confirmation avant l’exécution d’une commande, incluez le paramètre Confirm (sans valeur de paramètre) dans la commande. Voici un exemple :</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>Si vous ne voulez pas demander de confirmation, n’incluez pas le paramètre Confirm :</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>Une valeur de chaîne est une valeur alphanumérique. Elle peut donc inclure (en général) tous les caractères pouvant être tapés sur le clavier. Voici un exemple :</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>Il est recommandé de placer les valeurs de chaîne entre guillemets doubles. Si ce n’est pas toujours une obligation, il convient de le faire si votre valeur de chaîne inclut un espace vide ou une virgule, ou s’il s’agit d’un mot clé Windows PowerShell (un mot clé est une commande ou un autre élément faisant partie du langage Windows PowerShell lui-même). Par exemple, « If » et « End » sont tous les deux des mots clés Windows PowerShell. Pour plus d’informations, tapez la commande suivante à partir de l’invite de commandes Windows PowerShell :</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## Voir aussi

#### Concepts

[Présentation de Windows PowerShell et Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

