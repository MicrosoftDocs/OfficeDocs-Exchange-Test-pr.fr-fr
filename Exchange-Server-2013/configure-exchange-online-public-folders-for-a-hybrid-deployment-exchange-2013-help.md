---
title: 'Configurer les dossiers publics Exchange Online pour un déploiement hybride: Exchange 2013 Help'
TOCTitle: Configurer les dossiers publics Exchange Online pour un déploiement hybride
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72840873
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les dossiers publics Exchange Online pour un déploiement hybride

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-15_

**Résumé** : Instructions permettant aux utilisateurs Exchange 2013 en local d’accéder aux dossiers publics dans Exchange Online.

Dans un déploiement hybride, vos utilisateurs peuvent être dans un environnement Exchange Online, en local ou les deux, et vos dossiers publics peuvent se situer dans Exchange Online ou en local. Parfois, les utilisateurs en ligne peuvent avoir besoin d’accéder aux dossiers publics situés dans votre environnement local Exchange Server 2013. De même, les utilisateurs d’Exchange 2013 peuvent avoir besoin d’accéder aux dossiers publics dans Office 365 ou Exchange Online.

Cet article décrit la façon de permettre aux utilisateurs dans votre environnement local Exchange 2013 d’accéder aux dossiers publics Exchange Online/Office 365. Pour permettre aux utilisateurs d’Exchange Online/Office 365 d’accéder aux dossiers publics dans Exchange 2013 en local, consultez [Configurer les dossiers publics Exchange 2013 pour un déploiement hybride](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous avez des dossiers publics Exchange 2010 ou Exchange 2007, voir <a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurer des dossiers publics locaux hérités dans le cadre d’un déploiement hybride</a>.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

1.  Ces instructions supposent que vous avez utilisé l’Assistant Configuration hybride pour configurer et synchroniser vos environnements locaux et Exchange Online, et que les enregistrements DNS utilisés pour la découverte automatique de la plupart des utilisateurs font référence à un point de terminaison local. Pour plus d'informations, consultez la rubrique [Assistant de configuration hybride](https://technet.microsoft.com/fr-fr/library/hh529921\(v=exchg.150\)).

2.  Ces instructions supposent qu’Outlook Anywhere est activé et opérationnel sur le ou les serveurs Exchange locaux. Pour plus d’informations sur l’activation d’Outlook Anywhere, consultez la rubrique [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md).

3.  Il est possible que la mise en œuvre de la coexistence avec des dossiers publics pour un déploiement hybride d’Exchange avec Office 365 vous oblige à résoudre les conflits au cours de la procédure d’importation. Des conflits peuvent survenir, car l’adresse de messagerie non routable affectée aux dossiers publics à extension messagerie entre en conflit avec d’autres utilisateurs et groupes dans Office 365, ainsi qu’avec d’autres attributs.

4.  Pour pouvoir accéder aux dossiers publics des différents sites, les utilisateurs doivent mettre à niveau leurs clients Outlook vers la mise à jour publique pour Outlook de novembre 2012 ou une version ultérieure.
    
    1.  Pour télécharger la mise à jour pour Outlook 2010 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Outlook 2010 (KB2687623) Édition 32 bits](https://www.microsoft.com/fr-fr/download/details.aspx?id=35702).
    
    2.  Pour télécharger la mise à jour pour Outlook 2007 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/fr-fr/download/details.aspx?id=35718).

5.  Outlook 2011 pour Mac et Outlook pour Mac pour Office 365 ne sont pas pris en charge pour les dossiers publics entre les sites. Les utilisateurs doivent se trouver au même emplacement que les dossiers publics pour pouvoir y accéder avec Outlook 2011 pour Mac ou Outlook pour Mac pour Office 365. En outre, les utilisateurs dont les boîtes aux lettres sont dans Exchange Online ne peuvent pas accéder aux dossiers publics locaux avec Outlook Web App.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook 2016 pour Mac est pris en charge pour les dossiers publics intersites. Si les clients de votre organisation utilisent Outlook 2016 pour Mac, assurez-vous qu’ils ont installé la mise à jour d’avril 2016. Dans le cas contraire, ces utilisateurs ne seront pas en mesure d’accéder aux dossiers publics dans une coexistence ou une topologie hybride. Pour plus d’informations, voir <a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Accès aux dossiers publics avec Outlook 2016 pour Mac</a>.</td>
    </tr>
    </tbody>
    </table>


## Étape 1 : téléchargement des scripts

1.  Téléchargez les fichiers suivants à partir des [dossiers publics à extension messagerie - script de synchronisation d’annuaire de EXO vers local](https://go.microsoft.com/fwlink/p/?linkid=797795).
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  Enregistrez-les sur l’ordinateur local sur lequel vous allez exécuter PowerShell. Par exemple, C:\\PFScripts.

## Étape 2 : configuration de la synchronisation d’annuaires

Le script `Sync-MailPublicFoldersCloudToOnprem.ps1` synchronise les dossiers publics à extension messagerie entre Exchange Online et votre environnement local Exchange 2013. Les autorisations particulières attribuées aux dossiers publics à extension messagerie doivent être recréées dans le cloud, car les autorisations intersites ne sont pas prises en charge dans les scénarios de déploiement hybride. Pour plus d’informations, voir [Déploiements hybrides Exchange Server 2013](https://technet.microsoft.com/fr-fr/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les dossiers publics à extension messagerie synchronisés apparaissent en tant qu’objets de contact de messagerie à des fins de flux de messagerie et ne sont pas consultables dans le Centre d’administration Exchange. Reportez-vous à la commande Get-MailPublicFolder. Pour recréer les autorisations SendAs dans le cloud, utilisez la commande Add-RecipientPermission.</td>
</tr>
</tbody>
</table>


1.  Sur le serveur Exchange 2013, exécutez la commande suivante pour synchroniser les dossiers publics à extension messagerie à partir de Exchange Online/Office 365 vers votre annuaire Active Directory local.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    Où `Credential` est votre nom d’utilisateur Office 365 et votre mot de passe.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous recommandons d’exécuter ce script quotidiennement pour synchroniser vos dossiers publics à extension messagerie.</td>
</tr>
</tbody>
</table>


## Étape 3 : configuration des utilisateurs locaux pour l’accès aux dossiers publics Exchange Online

La dernière étape de cette procédure consiste à configurer l’organisation locale Exchange 2013 pour autoriser l’accès aux dossiers publics Exchange Online.

Le script `Import-PublicFolderMailboxes.ps1` importe les objets de boîtes aux lettres des dossiers publics à partir du cloud en tant qu’utilisateurs à extension messagerie vers votre environnement local. Le script configure également les objets importés en tant que boîtes aux lettres de dossiers publics à distance.

1.  Sur le serveur Exchange 2013, exécutez la commande suivante pour importer des objets de boîtes aux lettres de dossiers publics à partir du cloud dans votre annuaire Active Directory local.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    Où `Credential` est votre nom d’utilisateur Office 365 et votre mot de passe.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Nous vous conseillons d’exécuter ce script quotidiennement pour importer les objets de votre boîte aux lettres de dossier public, car à chaque fois que les boîtes aux lettres de dossier public atteignent leur capacité maximale, elles se décomposent automatiquement en plusieurs nouvelles boîtes aux lettres. Par conséquent, vérifiez toujours que vous avez importé les boîtes aux lettres de dossier public les plus récentes à partir du cloud.</td>
    </tr>
    </tbody>
    </table>


2.  Activez l'organisation locale Exchange 2013 pour l'accès aux dossiers publics Exchange Online.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour voir les modifications, vous devez attendre que la synchronisation ActiveDirectory soit terminée. Ce processus peut prendre jusqu’à 3 heures. Si vous ne souhaitez pas attendre les synchronisations récurrentes qui se produisent toutes les trois heures, vous pouvez forcer la synchronisation d’annuaire à tout moment. Pour obtenir des instructions détaillées permettant de forcer la synchronisation d’annuaire, consultez la rubrique <a href="http://technet.microsoft.com/fr-fr/library/jj151771.aspx">Synchroniser mes annuaires</a>.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

1.  Connectez-vous à Outlook en tant qu'utilisateur Exchange Online, puis effectuez les tests de dossiers publics suivants :
    
      - Affichez la hiérarchie.
    
      - Vérifiez les autorisations.
    
      - Créez et supprimez des dossiers publics.
    
      - Publiez ou effacez du contenu dans un dossier public.

