---
title: 'Configurer des dossiers publics locaux hérités dans le cadre d’un déploiement hybride: Exchange 2013 Help'
TOCTitle: Configurer des dossiers publics locaux hérités dans le cadre d’un déploiement hybride
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54915091
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des dossiers publics locaux hérités dans le cadre d’un déploiement hybride

 

_**Sapplique à :** Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2018-05-22_

**Résumé** : Suivez les étapes décrites dans cet article pour synchroniser les dossiers publics entre Office 365 et votre déploiement local Exchange 2007 ou Exchange 2010.

Dans un déploiement hybride, vos utilisateurs peuvent être dans un environnement Exchange Online, Exchange local ou les deux, et vos dossiers publics peuvent se situer dans Exchange Online ou localement. Les dossiers publics ne pouvant résider que dans un seul emplacement, vous devez choisir entre Exchange Online ou Exchange local. Ils ne peuvent pas se trouver aux deux emplacements. Les boîtes aux lettres de dossiers publics sont synchronisées sur Exchange Online par le service de synchronisation d’annuaires. En revanche, les dossiers à extension messagerie ne sont pas synchronisés entre les différents sites.

Cette rubrique décrit comment synchroniser des dossiers publics à extension messagerie lorsque vos utilisateurs opèrent dans un environnement Office 365, alors que vos dossiers publics Exchange 2010 SP3 ou Exchange 2007 SP3 RU10 sont locaux. Toutefois, un utilisateur Office 365 qui n’est pas représenté par un objet MailUser local (propre à la hiérarchie de dossier public cible) ne peut pas accéder aux dossiers publics hérités ou Exchange 2013 locaux.

> [!NOTE]
> Cette rubrique fait référence aux serveurs Exchange 2010 SP3 et Exchange 2007 SP3 RU10 en tant que <em>serveurs Exchange hérités</em>.


Vous allez synchroniser vos dossiers publics à extension messagerie à l'aide des scripts suivants, qui sont démarrés par une tâche Windows exécutée dans l'environnement local :

1.  `Sync-MailPublicFolders.ps1`   Ce script synchronise les objets de dossier public à extension messagerie de votre déploiement local d’Exchange avec Office 365. Il utilise le déploiement local d’Exchange comme maître pour déterminer les modifications à appliquer à O365. Le script crée, met à jour ou supprime des objets de dossier public à extension messagerie sur O365 Active Directory en fonction de ce qui existe dans le déploiement d’Exchange local.

2.  `SyncMailPublicFolders.strings.psd1`   Il s’agit d’un fichier de support utilisé par le script de synchronisation précédent. Il doit être copié dans le même emplacement que le script précédent.

Lorsque vous exécutez cette procédure, vos utilisateurs locaux et Office 365 peuvent accéder à la même infrastructure de dossiers publics locale.

## Quelles versions hybride d'Exchange fonctionnent avec les dossiers publics ?

Le tableau suivant décrit les combinaisons de version et d'emplacement de boîtes aux lettres utilisateur et de dossiers publics prises en charge. La mention « Hybride non applicable » indique un scénario toujours pris en charge, mais qui n'est pas considéré comme hybride pace que les dossiers publics et les utilisateurs résident au même emplacement.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>   </th>
<th>Boîte aux lettres utilisateur Exchange 2007 ou Exchange 2010 locale</th>
<th>Boîte aux lettres utilisateur Exchange 2013 locale</th>
<th>Boîte aux lettres utilisateur Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dossiers publics Exchange 2007 ou Exchange 2010 locaux</p></td>
<td><p>Hybride non applicable</p></td>
<td><p>Hybride non applicable</p></td>
<td><p>Pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Dossiers publics Exchange 2013 locaux</p></td>
<td><p>Hybride non applicable</p></td>
<td><p>Hybride non applicable</p></td>
<td><p>Pris en charge</p></td>
</tr>
<tr class="odd">
<td><p>Dossiers publics Exchange Online</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Hybride non applicable</p></td>
</tr>
</tbody>
</table>


Une configuration hybride avec des dossiers publics Exchange 2003 n'est pas prise en charge. Si vous exécutez Exchange 2003 au sein de votre organisation, vous devez déplacer l’ensemble des bases de données de dossiers publics et des réplicas vers Exchange 2007 SP3 RU10 ou une version ultérieure. Aucun réplica de dossier public ne peut être conservé dans Exchange 2003.

> [!NOTE]
> Outlook 2016 ne prend pas en charge l’accès aux dossiers publics hérités Exchange 2007. Si certains de vos utilisateurs se servent d’Outlook 2016, vous devrez déplacer vos dossiers publics vers une version plus récente d’Exchange. Pour plus d’informations sur la compatibilité d’Outlook 2016 et d’Office 2016 avec Exchange 2007 et versions antérieures, consultez <a href="https://go.microsoft.com/fwlink/p/?linkid=849053">cet article</a>.


## Étape 1 : ce qu’il faut savoir avant de commencer

1.  Ces instructions supposent que vous avez utilisé l’Assistant Configuration hybride pour configurer et synchroniser vos environnements locaux et Exchange Online, et que les enregistrements DNS utilisés pour la découverte automatique de la plupart des utilisateurs font référence à un point de terminaison local. Pour plus d'informations, consultez la rubrique [Assistant de configuration hybride](https://technet.microsoft.com/fr-fr/library/hh529921\(v=exchg.150\)).

2.  Ces instructions supposent qu’Outlook Anywhere est activé et opérationnel sur le ou les serveurs Exchange hérités locaux. Pour plus d’informations sur l’activation d’Outlook Anywhere, consultez la rubrique [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md).

3.  Il est possible que la mise en œuvre de la coexistence avec des dossiers publics hérités pour un déploiement hybride d’Exchange avec Office 365 vous oblige à résoudre les conflits au cours de la procédure d’importation. Des conflits peuvent survenir, car l’adresse de messagerie non-routable affectée aux dossiers publics à extension messagerie entre en conflit avec d’autres utilisateurs et groupes dans Office 365, ainsi qu’avec d’autres attributs.

4.  Ces instructions supposent que votre organisation Exchange Online a été mise à niveau vers une version prenant en charge les dossiers publics.

5.  Dans Exchange 2010, vous devez être membre du groupe de rôles Gestion de l'organisation. Ce groupe de rôles diffère des autorisations qui vous sont attribuées quand vous vous abonnez à Exchange Online. Pour plus de détails sur l'activation du groupe de rôles Gestion de l'organisation, consultez la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

6.  Dans Exchange 2010, vous devez être membre du groupe de rôles RBAC Gestion de l’organisation ou Gestion du serveur. Pour plus d’informations, consultez la rubrique [Ajouter des membres à un groupe de rôles](https://go.microsoft.com/fwlink/?linkid=299212).

7.  Dans Exchange 2007, vous devez posséder le rôle d’administrateur de l’organisation Exchange ou d’administrateur d’Exchange Server. En outre, le rôle Administrateur de dossiers publics et le groupe Administrateurs local pour le serveur cible doivent vous être attribués. Pour plus d’informations, consultez la page [Procédure d’ajout d’un utilisateur ou d’un groupe à un rôle d’administrateur](https://go.microsoft.com/fwlink/p/?linkid=81779).

8.  Si vous disposez d’Exchange Server 2007 s’exécutant sur Windows Server 2008 x64, vous devez procéder à une mise à niveau vers [Windows PowerShell 2.0 et WinRM 2.0 pour Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930). Si vous disposez d’Exchange Server 2007 s’exécutant sur Windows Server 2003 x64, vous devez procéder à une mise à niveau vers Windows PowerShell 2.0. Pour plus d’informations, consultez la rubrique [Mise à jour pour Windows Server 2003 Édition x64](https://www.microsoft.com/fr-fr/download/details.aspx?id=10512).

9.  Pour pouvoir accéder aux dossiers publics des différents sites, les utilisateurs doivent mettre à niveau leurs clients Outlook vers la mise à jour publique pour Outlook de novembre 2012 ou une version ultérieure.
    
    1.  Pour télécharger la mise à jour pour Outlook 2010 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Outlook 2010 (KB2687623) Édition 32 bits](https://www.microsoft.com/fr-fr/download/details.aspx?id=35702).
    
    2.  Pour télécharger la mise à jour pour Outlook 2007 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/fr-fr/download/details.aspx?id=35718).

10. Outlook 2016 pour Mac (et versions antérieures) et Outlook pour Mac pour Office 365 ne sont pas pris en charge pour les dossiers publics hérités entre les sites. Les utilisateurs doivent se trouver au même emplacement que les dossiers publics pour pouvoir y accéder avec Outlook pour Mac ou Outlook pour Mac pour Office 365. En outre, les utilisateurs dont les boîtes aux lettres sont dans Exchange Online ne peuvent pas accéder aux dossiers publics locaux avec Outlook Web App.

11. Une fois que vous aurez configuré vos dossiers publics locaux pour un déploiement hybride à l’aide des instructions données dans cet article, les utilisateurs externes à votre organisation ne pourront pas envoyer de messages à vos dossiers publics locaux, sauf si réalisez une configuration plus avancée. Vous pouvez définir le domaine accepté pour les dossiers publics sur le relais interne (reportez-vous à [Gestion des domaines acceptés dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj945194\(v=exchg.150\)) pour plus d’informations) ou vous pouvez désactiver le blocage du périmètre basé sur l'annuaire, comme décrit dans [Utiliser le blocage du périmètre basé sur l’annuaire pour rejeter les messages envoyés à des destinataires non valides](https://technet.microsoft.com/fr-fr/library/dn600322\(v=exchg.150\)).

## Étape 2 : détectabilité des dossiers publics

1.  Si vos dossiers publics sont sur des serveurs Exchange 2010 ou version ultérieure, vous devez installer le rôle serveur d’accès au client sur tous les serveurs de boîtes aux lettres disposant d’une base de données de dossiers publics. Cela permet l’exécution du service RpcClientAccess de Microsoft Exchange qui permet à tous les clients d’accéder aux dossiers publics. Le rôle d’accès client n’étant pas requis pour les serveurs de dossiers publics Exchange 2007, cette étape n’est pas nécessaire. Pour plus d’informations, consultez la rubrique [Installer Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Cette étape n’est pas obligatoire pour les dossiers publics Exchange 2007.
    
    > [!NOTE]
    > Il n’est pas utile que ce serveur prenne part à l’équilibrage de la charge d’accès au client. Pour plus d'informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/ff625247(v=exchg.141).aspx">Présentation de l'équilibrage de la charge dans Exchange 2010</a>.


2.  Créez une base de données de boîtes aux lettres vide sur chaque serveur de dossiers publics.
    
    Pour Exchange 2010, exécutez la commande suivante : Cette commande exclut la base de données de boîtes aux lettres du programme d’équilibrage de la charge pour l’ajout de boîtes aux lettres. Cela évite l'ajout automatique de nouvelles boîtes aux lettres à cette base de données.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    Pour Exchange 2007, exécutez la commande suivante :
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    
    > [!NOTE]
    > Nous vous recommandons d’ajouter à cette base de données uniquement la boîte aux lettres proxy que vous allez créer à l’étape 3. Aucune autre boîte aux lettres ne devrait être créée dans cette base de données de boîtes aux lettres.


3.  Créez une boîte aux lettres proxy à l'intérieur de la nouvelle base de données de boîtes aux lettres, puis masquez-la dans le carnet d'adresses. Le SMTP de cette boîte aux lettres sera renvoyé par la découverte automatique comme SMTP *DefaultPublicFolderMailbox*, de sorte qu'en résolvant ce SMTP, le client pourrait atteindre le serveur Exchange hérité pour l'accès aux dossiers publics.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Pour Exchange 2010, activez la découverte automatique de façon à ce qu’elle renvoie les boîtes aux lettres de dossiers publics proxy. Cette étape n’est pas nécessaire pour Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Répétez les étapes précédentes pour chaque serveur de dossiers publics au sein de votre organisation.

## Étape 3 : téléchargement des scripts

1.  Téléchargez les fichiers suivants à partir de la page relative au [script de synchronisation d’annuaires des dossiers publics à extension messagerie](https://www.microsoft.com/en-us/download/details.aspx?id=46381) :
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Enregistrez-les sur l’ordinateur local sur lequel vous allez exécuter PowerShell. Par exemple, C:\\PFScripts.

## Étape 4 : configuration de la synchronisation d’annuaires

Le service de synchronisation d’annuaires ne synchronise pas les dossiers publics à extension messagerie. Les scripts suivants synchronisent les dossiers publics à extension messagerie dans plusieurs sites. Les autorisations particulières attribuées aux dossiers publics à extension messagerie doivent être recréées dans le cloud, car les autorisations inter-sites ne sont pas prises en charge dans les scénarios de déploiement hybride. Pour plus d’informations, voir [Déploiements hybrides Exchange Server 2013](https://technet.microsoft.com/fr-fr/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).

> [!NOTE]
> Les dossiers publics à extension messagerie synchronisés apparaissent en tant qu’objets de contact de messagerie à des fins de flux de messagerie et ne sont pas consultables dans le Centre d’administration Exchange. Reportez-vous à la commande Get-MailPublicFolder. Pour recréer les autorisations SendAs dans le cloud, utilisez la commande Add-RecipientPermission.


1.  Sur le serveur Exchange hérité, exécutez la commande suivante pour synchroniser les dossiers publics à extension messagerie à partir de votre annuaire Active Directory local vers O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Où `Credential` est votre nom d’utilisateur et votre mot de passe Office 365 et `CsvSummaryFile` est le chemin d’accès de l’emplacement où vous voulez journaliser les opérations et les erreurs de synchronisation au format .csv.

> [!NOTE]
> Avant d’exécuter le script, nous vous recommandons de commencer par simuler les actions du script dans votre environnement en l’exécutant comme décrit ci-dessus avec le paramètre <code>-WhatIf</code>.
> Nous vous recommandons également d’exécuter ce script quotidiennement pour synchroniser vos dossiers publics à extension messagerie.


## Étape 5 : configuration des utilisateurs Exchange Online pour l’accès aux dossiers publics locaux

La dernière étape de cette procédure consiste à configurer l’organisation Exchange Online afin d’autoriser l’accès aux dossiers publics locaux hérités.

Activez l’organisation Exchange Online pour accéder aux dossiers publics locaux. Il faut qu’elle pointe sur toutes les boîtes aux lettres de dossiers publics proxy que vous avez créées à l’étape 2, Détectabilité des dossiers publics.

Exécutez la commande suivante dans **Windows PowerShell** :

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

Pour voir les modifications, vous devez attendre que la synchronisation ActiveDirectory soit terminée. Ce processus peut prendre jusqu’à 3 heures. Si vous ne souhaitez pas attendre les synchronisations récurrentes qui se produisent toutes les trois heures, vous pouvez forcer la synchronisation d’annuaire à tout moment. Pour obtenir des instructions détaillées permettant de forcer la synchronisation d’annuaire, consultez la rubrique [Synchroniser vos annuaires](http://technet.microsoft.com/fr-fr/library/jj151771.aspx). Office 365 sélectionne de manière aléatoire l’une des boîtes aux lettres de dossiers publics fournies dans cette commande.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un utilisateur Office 365 qui n’est pas représenté par un objet MailUser local (propre à la hiérarchie de dossier public cible) ne peut pas accéder aux dossiers publics hérités ou Exchange 2013 locaux. Pour obtenir une solution, consultez l’article de la base de connaissances sur les <a href="https://go.microsoft.com/fwlink/p/?linkid=699451">utilisateurs Exchange Online ne pouvant pas accéder aux dossiers publics locaux hérités</a>.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

1.  Connectez-vous à Outlook en tant qu'utilisateur Exchange Online, puis effectuez les tests de dossiers publics suivants :
    
      - Affichez la hiérarchie.
    
      - Vérifiez les autorisations.
    
      - Créez et supprimez des dossiers publics.
    
      - Publiez ou effacez du contenu dans un dossier public.

## Vous débutez avec Office 365 ?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icône rapide pour LinkedIn Learning" alt="Icône rapide pour LinkedIn Learning" /> <strong>Vous débutez avec Office 365 ?</strong><br />
Découvrez les cours vidéo gratuits pour <a href="https://support.office.com/fr-fr/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> proposés par LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

