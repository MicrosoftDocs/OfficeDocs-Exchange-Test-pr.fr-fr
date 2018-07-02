---
title: 'Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell: Exchange 2013 Help'
TOCTitle: Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50477813
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-11-22_

**Résumé:**  Apprenez à gérer les déplacements de boîtes aux lettres de forêt croisée et les migrations de Exchange 2013 à l’aide du script MoveRequest.ps1-préparer dans le Environnement de ligne de commande Exchange Management Shell.

Microsoft Exchange 2013 prend en charge les déplacements de boîtes aux lettres et de migrations à l’aide des applets de commande **New-MoveRequest** et **New-MigrationBatch** . Vous pouvez également déplacer la boîte aux lettres via Exchange Administration Center (EAC). Vous pouvez déplacer un Exchange 2010 ou une boîte aux lettres de Exchange 2013 d’une forêt de Exchange source pour une forêt de Exchange 2013 cible.

Pour exécuter les cmdlets **New-MoveRequest** et **New-MigrationBatch**, un utilisateur de messagerie doit exister dans la forêt Exchange cible et disposer d’un ensemble d’attributs Active Directory obligatoires minimum.

Le script Windows PowerShell décrit en exemple dans cette rubrique prend en charge cette tâche en synchronisant les utilisateurs de boîtes aux lettres d’une forêt source Exchange 2013 avec des forêts cibles Exchange 2013 en tant qu’utilisateurs à extension messagerie. Le script copie les attributs Active Directory des utilisateurs de boîtes aux lettres de la forêt source vers la forêt cible, puis utilise la cmdlet **Update-Recipient** pour changer les objets cibles en utilisateurs à extension messagerie.

Pour plus d’informations sur l’utilisation et l’écriture de scripts, voir [Scripts dans Exchange Management Shell](https://technet.microsoft.com/fr-fr/library/bb123798\(v=exchg.150\)). Pour plus d’informations sur la préparation pour les déplacements inter-forêts, voir [Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux demandes de déplacement à distance ? Consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Localisez le script à l’emplacement suivant : Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - Pour exécuter l’exemple de script, vous avez besoin des éléments suivants :
    
      - Une forêt source Exchange, où se trouve la boîte aux lettres. Cela peut être une boîte aux lettres Exchange 2010 ou Exchange 2013.
    
      - Une forêt cible dans laquelle Exchange 2013 est installé, à l’endroit où la boîte aux lettres sera déplacée.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser le script Prepare-MoveRequest.ps1 pour préparer les boîtes aux lettres en vue de déplacements inter-forêts

Exécutez le script depuis l’environnement de ligne de commande sur un rôle serveur exécutant Exchange 2013 dans la forêt Exchange 2013 cible. Le script copie les attributs de boîte aux lettres à partir de la forêt source.

Pour affecter des informations spécifiques d’identification d’authentification pour le contrôleur de domaine de forêt distant, vous devez tout d’abord exécuter la cmdlet Windows PowerShell **Get-Credential**, puis stocker l’entrée de l’utilisateur dans une variable temporaire. Lorsque vous exécutez la cmdlet **Get-Credential**, celle-ci demande le nom d’utilisateur et le mot de passe du compte utilisé durant l’authentification auprès du contrôleur de domaine de forêt distant. Vous pouvez ensuite utiliser la variable temporaire dans le script Prepare-MoveRequest.ps1. Pour plus d’informations à propos de la cmdlet **Get-Credential**, voir [Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Assurez-vous d’utiliser deux informations d’identification distinctes pour la forêt locale et la forêt distante lors de l’appel de ce script.</td>
</tr>
</tbody>
</table>


1.  Exécutez les commandes suivantes pour obtenir les informations d’identification de la forêt locale et de la forêt distante.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Exécutez les commandes pour transmettre les informations d’identification aux paramètres *LocalForestCredential* et *RemoteForestCredential* dans le script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## Ensemble des paramètres du script

Le tableau suivant décrit l’ensemble des paramètres associés au script.

### Ensemble de paramètres du script Prepare-MoveRequest.ps1

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Le paramètre <em>Identity</em> identifie de façon unique une boîte aux lettres dans la forêt source. L’identité peut être :</p>
<ul>
<li><p>Nom commun (CN)</p></li>
<li><p>Alias</p></li>
<li><p>Propriété <strong>proxyAddress</strong></p></li>
<li><p>Propriété <strong>objectGuid</strong></p></li>
<li><p>Propriété <strong>DisplayName</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Le paramètre <em>RemoteForestCredential</em> spécifie l’administrateur ayant les autorisations de copier des données depuis le Active Directory de la forêt source.</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Le paramètre <em>RemoteForestDomainController</em> spécifie un contrôleur de domaine dans la forêt source où réside la boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>DisableEmailAddressPolicy</em> spécifie si le protocole EAP (Email Address Policy) doit être désactivé à la création d’un objet <strong>MailUser</strong> dans la forêt cible.</p>
<p>Lorsque vous spécifiez ce paramètre, l’EAP dans la forêt cible ne sera pas appliqué.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous spécifiez ce paramètre, l’objet <strong>MailUser</strong> n’aura pas de mappage d’adresse de messagerie dans le domaine de forêt locale identifié. Ceci est généralement identifié par l’EAP.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le commutateur <em>LinkedMailUser</em> permet de créer un utilisateur de messagerie lié dans la forêt locale pour l’utilisateur de boîte aux lettres dans la forêt distante.</p>
<p>Si le commutateur est fourni, le script crée un objet <strong>MailUser</strong> cible lié à la boîte aux lettres source. Si le commutateur est omis, le script crée un objet <strong>MailUser</strong> cible ordinaire.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>LocalForestCredential</em> spécifie l’administrateur ayant les autorisations d’écrire des données vers le Active Directory de la forêt cible.</p>
<p>Il est conseillé de spécifier explicitement ce paramètre pour éviter les problèmes d’autorisation Active Directory.</p>
<p>Si une relation d’approbation est configurée sur la forêt distante et la forêt locale, n’utilisez pas de compte utilisateur de la forêt distante en tant qu’information d’identification de forêt locale, même si l’utilisateur distant pourrait avoir l’autorisation de modifier Active Directory dans la forêt locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>LocalForestDomainController</em> spécifie un contrôleur de domaine dans la forêt cible où l’utilisateur à extension messagerie sera créé.</p>
<p>Il est conseillé de spécifier ce paramètre pour éviter les éventuels problèmes de retard de réplication de contrôleur de domaine dans la forêt locale qui pourraient se produire si un contrôleur de domaine aléatoire est sélectionné.</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>MailboxDeliveryDomain</em> spécifie un domaine faisant autorité de la forêt source pour que le script puisse sélectionner la bonne propriété <strong>proxyAddress</strong> de l’utilisateur de boîte aux lettres source comme propriété <strong>targetAddress</strong> de l’utilisateur à extension messagerie cible.</p>
<p>Par défaut, l’adresse SMTP principale de l’utilisateur de boîte aux lettres source est définie comme la propriété <strong>targetAddress</strong> de l’utilisateur à extension messagerie cible.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>OverWriteLocalObject</em> est utilisé pour les utilisateurs créés par l’outil de migration Active Directory. Les propriétés sont copiées du contact de messagerie existant dans le nouvel utilisateur de messagerie. Cependant, une fois cette copie effectuée, le script copie également les propriétés de l’utilisateur de forêt source dans le nouvel utilisateur de messagerie.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>TargetMailuserOU</em> spécifie l’unité d’organisation (OU) sous laquelle l’utilisateur à extension messagerie cible sera créé.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Le paramètre <em>UseLocalObject</em> spécifie s’il faut convertir l’objet local existant en utilisateur à extension messagerie cible obligatoire si le script détecte un objet dans la forêt locale qui entre en conflit avec l’utilisateur à extension messagerie à créer.</p></td>
</tr>
</tbody>
</table>


## Exemples

Cette section contient plusieurs exemples d’utilisation du script Prepare-MoveRequest.ps1.

## Exemple : Utilisateur unique à extension messagerie lié

Cet exemple fournit un seul utilisateur à extension messagerie lié dans la forêt locale, lorsqu’il y a une approbation forêt entre la forêt distante et la forêt locale.

1.  Exécutez les commandes suivantes pour obtenir les informations d’identification de la forêt locale et de la forêt distante.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Exécutez la commande suivante pour transmettre les informations d’identification aux paramètres *LocalForestCredential* et *RemoteForestCredential* dans le script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## Exemple : Traitement en pipeline

Cet exemple prend en charge le traitement en pipeline si vous fournissez une liste des identités de boîtes aux lettres.

1.  Exécutez la commande suivante.
    
        $UserCredentials = Get-Credential

2.  Exécutez la commande suivante pour transmettre les informations d’identification au paramètre *RemoteForestCredential* dans le script Prepare-MoveRequest.ps1.
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Exemple : Utiliser un fichier .csv pour créer en bloc des utilisateurs à extension messagerie

Vous pouvez générer un fichier .csv contenant une liste des identités de boîtes aux lettres de la forêt source, qui vous permet de canaliser le contenu de ce fichier dans le script pour créer en bloc des utilisateurs à extension messagerie cible.

Par exemple, le contenu du fichier .csv peut être :

Identity

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

Cet exemple appelle un fichier .csv pour créer en bloc les utilisateurs à extension messagerie cible.

1.  Exécutez la commande suivante permettant d’obtenir les informations d’identification pour la forêt distante.
    
        $UserCredentials = Get-Credential

2.  Exécutez la commande suivante pour transmettre les informations d’identification au paramètre *RemoteForestCredential* dans le script Prepare-MoveRequest.ps1.
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Comportement de script par objet cible

Cette section décrit la façon dont le script s’exécute par rapport un différents scénarios pour les objets cible.

## Objet à extension messagerie cible en double

Lorsque le script tente de créer un utilisateur à extension messagerie cible depuis l’utilisateur de boîte aux lettres source et qu’il détecte un objet à extension messagerie local en double, il utilise la logique suivante :

  - Si l’attribut **masterAccountSid** de l’utilisateur de la boîte aux lettres source équivaut à l’attribut **objectSid** ou **masterAccountSid** de l’objet cible :
    
      - Si l’objet cible n’est pas à extension messagerie, le script renvoie une erreur car il ne prend pas en charge la conversion d’un objet qui n’est pas à extension messagerie en un utilisateur à extension messagerie.
    
      - Si l’objet cible est à extension messagerie, l’objet cible est un doublon.

  - Si une adresse des propriétés **proxyAddress** (smtp/x500 seulement) de l’utilisateur de boîtes aux lettres source équivaut à une adresse des propriétés **proxyAddress** (smtp/x500 seulement) d’un objet cible, alors l’objet cible est un doublon.

Le script interroge l’utilisateur sur les objets en double.

Si l’objet à extension messagerie cible est un utilisateur ou un contact à extension messagerie, qui est très probablement créé par un déploiement de la synchronisation de la liste d’adresses globale inter-forêts (basé sur Identity Lifecycle Management 2007 Service Pack 1), l’utilisateur peut à nouveau exécuter le script avec le paramètre *UseLocalObject* pour utiliser l’objet à extension messagerie cible pour la migration de boîtes aux lettres.

## Utilisateur à extension messagerie

Si l’objet cible est un utilisateur à extension messagerie, le script copie les attributs suivants de l’utilisateur de boîte aux lettres source vers l’utilisateur à extension messagerie cible :

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

Si le paramètre *LinkedMailUser* est défini, le script copie l’attribut **objectSid**/**masterAccountSid** source.

## Contact à extension messagerie

Si l’objet cible est un contact à extension messagerie, le script supprime le contact existant et copie l’ensemble de ses attributs vers un nouvel utilisateur à extension messagerie. Le script copie également les attributs suivants à partir de l’utilisateur de boîte aux lettres source :

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl** (défini sur 514 //équivalent à 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

Si le paramètre *LinkedMailUser* est défini, le script copie l’attribut **objectSid**/**masterAccountSid** source.

## Attribut LegacyExchangeDN

Lorsque la cmdlet **Update-Recipient** est appelée pour convertir l’objet cible en un utilisateur à extension messagerie, un nouvel attribut **LegacyExchangeDN** est généré pour l’utilisateur à extension messagerie cible. Le script copie l’attribut **LegacyExchangeDN** de l’utilisateur à extension messagerie cible sous forme d’adresse x500 vers les propriétés **proxyAddress** de l’utilisateur de boîte aux lettres source.

