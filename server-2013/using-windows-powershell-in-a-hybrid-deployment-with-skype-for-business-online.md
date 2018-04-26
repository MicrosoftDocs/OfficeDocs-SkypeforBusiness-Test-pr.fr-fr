---
title: Utilisation de Windows PowerShell dans un déploiement hybride
TOCTitle: Utilisation de Windows PowerShell dans un déploiement hybride
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56269643
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilisation de Windows PowerShell dans un déploiement hybride

 

_**Dernière rubrique modifiée :** 2015-06-22_

Dans un déploiement hybride, certains utilisateurs d’une organisation sont hébergés sur la version locale de Lync Server 2013, tandis que d’autres sont hébergés sur Skype Entreprise Online. Vous pouvez utiliser une seule session de Windows PowerShell pour gérer simultanément votre version locale de Lync Server et votre client Skype Entreprise Online. Pour ce faire, vous devez comprendre deux aspects essentiels :

1.  Comment établir une connexion simultanée à Lync Server et Skype Entreprise Online.

2.  Comment référencer les paramètres Skype Entreprise Online de cette connexion simultanée.

L’établissement d’une connexion simultanée à Lync Server et Skype Entreprise Online est relativement simple. Pour ce faire, commencez par connecter le serveur Lync Server comme vous le faites habituellement, en démarrant Lync Server Management Shell ou en créant une connexion à distance à un serveur frontal. Une fois que vous vous êtes connecté à la version locale de Lync Server, vous pouvez ensuite vous connecter à Skype Entreprise Online en utilisant la même procédure que si vous vous connectiez uniquement à Skype Entreprise Online. Pour établir cette connexion, vous devez commencer par créer un objet d’identification utilisateur Windows PowerShell à l’aide de vos informations d’ouverture de session Office 365. Pour ce faire, tapez ce qui suit à l’invite Windows PowerShell, puis appuyez sur Entrée :

    $credential = Get-Credential

Lorsque vous appuyez sur Entrée, la boîte de dialogue **Informations d’identification Windows PowerShell** s’affiche :

![Informations d’identification pour la connexion Windows PowerShell](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Informations d’identification pour la connexion Windows PowerShell")

Dans la zone **Nom d’utilisateur**, tapez votre nom d’utilisateur Skype Entreprise Online. Dans la zone **Mot de passe**, tapez votre mot de passe Skype Entreprise Online (celui-ci est masqué et n’est pas visible à l’écran). Par exemple, si votre nom d’utilisateur est kenmyer@litwareinc.com et votre mot de passe p@ssw0rd\!, la boîte de dialogue ressemblera à ce qui suit :

![Connexion avec les informations d’identification Windows PowerShell](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Connexion avec les informations d’identification Windows PowerShell")

Pour créer l’objet d’identification utilisateur, cliquez sur **OK**. Une fois que vous avez créé l’objet d’identification utilisateur, vous pouvez vous connecter à Skype Entreprise Online en exécutant la commande suivante :

    $session = New-CsOnlineSession -Credential $credential

Veillez à taper la commande telle qu’elle est indiquée. Le nom de votre domaine Skype Entreprise Online n’a pas d’importance. L’applet de commande **New-CsOnlineSession** vous connecte à Office 365 et ouvre une session à l’aide des informations d’identification fournies. Une fois la connexion établie et l’authentification effectuée, vous êtes redirigé automatiquement vers l’URI approprié.

Si votre connexion est correctement établie, un message semblable au suivant apparaît dans la console Windows PowerShell :

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

Une fois que vous avez correctement établi une connexion à Skype Entreprise Online, importez cette session en exécutant une commande semblable à la suivante :

    Import-PSSession $session -AllowClobber

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398920.note(OCS.15).gif" title="note" alt="note" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le paramètre AllowClobber garantit que toutes les applets de commande Skype Entreprise Online sont importées, y compris les applets de commande qui ont le même nom que les applets de commande Lync Server normales. Un grand nombre d’entre elles apparaîtront, car la plupart des applets de commande Skype Entreprise Online, y compris <a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a>, <a href="new-csexumcontact.md">New-CsExUmContact</a>, <a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a>, etc., ont un équivalent local. Les applets de commande jumelées (par exemple, Lync Server<strong>Get-CsMeetingConfiguration</strong> et Skype Entreprise Online<strong>Get-CsMeetingConfiguration</strong>) sont identiques : peu importe l’applet de commande que vous utilisez. La seule raison pour laquelle vous utilisez le paramètre AllowClobber est d’empêcher l’affichage de messages d’avertissement à l’écran.</td>
</tr>
</tbody>
</table>


À ce stade, vous êtes prêt à gérer la version locale de Lync Server et Skype Entreprise Online. Il est également possible que vous vous interrogiez : comment faire la différence entre les stratégies et paramètres de Lync Server et Skype Entreprise Online ? Par exemple, vous pouvez modifier les paramètres globaux de configuration de la réunion. Pour ce faire, vous devez exécuter la commande suivante :

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

Cette commande modifie les paramètres globaux. Mais lesquels ? Ceux de la version locale de Lync Server ? De Skype Entreprise Online ? Des deux ? Aucun des deux ?

Dans ce cas spécifique, les paramètres de la version locale sont modifiés. En effet, le paramètre Tenant n’a pas été inclus dans la commande. Si vous êtes connecté simultanément à la version locale de Lync Server et à Skype Entreprise Online, les applets de commande qui peuvent fonctionner sur l’une ou l’autre des plateformes sont exécutées sur Lync Server, sauf instruction contraire de votre part. La seule façon de transmettre cette instruction est d’inclure le paramètre Tenant lors de l’exécution de la commande. Par exemple, la commande suivante met à jour les paramètres globaux du client Skype Entreprise Online avec l’ID de client bf19b7db-6960-41e5-a139-2aa373474354 :

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

Le paramètre Tenant est la clé. Cette commande retourne la stratégie d’accès externe globale pour la version locale de Lync Server :

    Get-CsExternalAccessPolicy -Identity "global"

La commande suivante retourne la stratégie d’accès externe globale pour votre client Skype Entreprise Online :

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Rappelez-vous qu’il y a plus de 700 applets de commande locales. Pour autant, la plupart de ces applets de commande n’ont pas de paramètre Tenant. Elles ne peuvent donc pas être utilisées avec Skype Entreprise Online. Notez également que les quelques applets de commande incluant le paramètre Tenant ne peuvent pas être utilisées avec Skype Entreprise Online pour le moment. Pour récupérer l’ensemble exact d’applets de commande qui peuvent être utilisées avec Skype Entreprise Online, exécutez la commande suivante à partir de l’invite Windows PowerShell :

    Get-Module

Des informations semblables à ce qui suit sont affichées à l’écran :

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Le module de type Script contient les applets de commande Skype Entreprise Online. Pour retourner la liste de ces applets de commande, exécutez l’applet de commande **Get-Command** en utilisant le nom du module Script comme nom de module :

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell affiche ensuite la liste des applets de commande Skype Entreprise Online.

**Résolution des problèmes de connexion dans un déploiement hybride**

Dans certains cas, les administrateurs peuvent rencontrer des problèmes lors de la connexion à Office 365 en cas d’utilisation d’un compte local (par exemple, administrator@litwareinc.net) plutôt que d’un compte Office 365 (tel que administrator@litwareinc.onmicrosoft.com). Si la synchronisation de répertoire fonctionne correctement, vous devriez pouvoir vous connecter avec l’un de ces comptes ; c’est l’un des avantages d’un déploiement hybride. Mais il est parfois arrivé qu’un administrateur soit incapable de se connecter à l’aide de son compte local. Ceci est généralement dû à une découverte automatique pointant l’effort de connexion sur l’installation locale de Lync Server au lieu de Office 365.

Heureusement, il existe une manière simple de contourner ce problème. Lors de l’utilisation de l’applet de commande **New-CsOnlineSession** pour se connecter à Office 365, il suffit d’inclure le paramètre OverrideAdminDomain suivi du nom de domaine Office 365. Par exemple, pour se connecter à Office 365 à l’aide du compte administrator@litwareinc.net, il faut inclure le paramètre OverrideAdminDomain suivi du nom de domaine litwareinc.onmicrosoft.com :

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

Cette commande dirigera explicitement la tentative de connexion sur les serveurs Office 365 et le domaine litwareinc.onmicrosoft.com.

