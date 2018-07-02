---
title: 'Configurer les dossiers publics Exchange 2013 pour un déploiement hybride: Exchange 2013 Help'
TOCTitle: Configurer les dossiers publics Exchange 2013 pour un déploiement hybride
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65452457
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les dossiers publics Exchange 2013 pour un déploiement hybride

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

**Résumé** : Instructions permettant aux utilisateurs Exchange Online d’accéder aux dossiers publics en local dans votre environnement Exchange 2013.

Dans un déploiement hybride, vos utilisateurs peuvent être dans un environnement Exchange Online, en local ou les deux, et vos dossiers publics peuvent se situer dans Exchange Online ou en local. Parfois, les utilisateurs en ligne peuvent avoir besoin d’accéder aux dossiers publics situés dans votre environnement local Exchange Server 2013. De même, les utilisateurs d’Exchange 2013 peuvent avoir besoin d’accéder aux dossiers publics dans Office 365 ou Exchange Online.

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


Cet article décrit la façon de permettre à vos utilisateurs Exchange Online/Office 365 d’accéder aux dossiers publics dans Exchange 2013. Pour permettre aux utilisateurs Exchange 2013 en local d’accéder aux dossiers publics dans Exchange Online, voir [Configurer les dossiers publics Exchange Online pour un déploiement hybride](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).

Un utilisateur Exchange Online/Office 365 doit être représenté par un objet MailUser dans l’environnement local Exchange pour accéder aux dossiers publics Exchange 2013. Cet objet MailUser doit également être en local par rapport à la hiérarchie de dossiers publics Exchange 2013 cible. Si vous avez des utilisateurs Office 365 qui ne sont pas actuellement représentés en local par les objets MailUser, reportez-vous à l’article de la base de connaissances Microsoft n° 3106618 relatif aux [utilisateurs Exchange Online ne pouvant pas accéder aux dossiers publics hérités en local](https://go.microsoft.com/fwlink/p/?linkid=699451) pour créer des entités locales correspondantes.

## Ce qu'il faut savoir avant de commencer

1.  Ces instructions supposent que vous avez utilisé l’Assistant Configuration hybride pour configurer et synchroniser vos environnements locaux et Exchange Online, et que les enregistrements DNS utilisés pour la découverte automatique de la plupart des utilisateurs font référence à un point de terminaison local. Pour plus d'informations, consultez la rubrique [Assistant de configuration hybride](https://technet.microsoft.com/fr-fr/library/hh529921\(v=exchg.150\)).

2.  Ces instructions supposent qu’Outlook Anywhere est activé et opérationnel sur le ou les serveurs Exchange locaux. Pour plus d’informations sur l’activation d’Outlook Anywhere, consultez la rubrique [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md).

3.  Il est possible que la mise en œuvre de la coexistence avec des dossiers publics pour un déploiement hybride d’Exchange avec Office 365 vous oblige à résoudre les conflits au cours de la procédure d’importation. Des conflits peuvent survenir, car l’adresse de messagerie non routable affectée aux dossiers publics à extension messagerie entre en conflit avec d’autres utilisateurs et groupes dans Office 365, ainsi qu’avec d’autres attributs.

4.  Pour pouvoir accéder aux dossiers publics des différents sites, les utilisateurs doivent mettre à niveau leurs clients Outlook vers la mise à jour publique pour Outlook de novembre 2012 ou une version ultérieure.
    
    1.  Pour télécharger la mise à jour pour Outlook 2010 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Outlook 2010 (KB2687623) Édition 32 bits](https://www.microsoft.com/fr-fr/download/details.aspx?id=35702).
    
    2.  Pour télécharger la mise à jour pour Outlook 2007 de novembre 2012, consultez la rubrique [Mise à jour pour Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/fr-fr/download/details.aspx?id=35718).

5.  Outlook 2011 pour Mac et Outlook pour Mac pour Office 365 ne sont pas pris en charge pour les dossiers publics entre les sites. Les utilisateurs doivent se trouver au même emplacement que les dossiers publics pour pouvoir y accéder avec Outlook 2011 pour Mac ou Outlook pour Mac pour Office 365. De plus, les utilisateurs dont les boîtes aux lettres sont dans Exchange Online ne peuvent pas accéder aux dossiers publics locaux avec Outlook Web App.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook 2016 pour Mac est pris en charge pour les dossiers publics intersites. Si les clients de votre organisation utilisent Outlook 2016 pour Mac, assurez-vous qu’ils ont installé la mise à jour d’avril 2016. Dans le cas contraire, ces utilisateurs ne seront pas en mesure d’accéder aux dossiers publics dans une topologie hybride. Pour plus d’informations, voir <a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Accès aux dossiers publics avec Outlook 2016 pour Mac</a>.</td>
    </tr>
    </tbody>
    </table>


## Étape 1 : téléchargement des scripts

1.  Téléchargez les fichiers suivants à partir de la page relative au [script de synchronisation d’annuaires des dossiers publics à extension messagerie](https://www.microsoft.com/en-us/download/details.aspx?id=46381) :
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Enregistrez-les sur l’ordinateur local sur lequel vous allez exécuter PowerShell. Par exemple, C:\\PFScripts.

## Étape 2 : configuration de la synchronisation d’annuaires

Le service de synchronisation d’annuaires ne synchronise pas les dossiers publics à extension messagerie. Les scripts suivants synchronisent les dossiers publics à extension messagerie dans plusieurs sites et Office 365. Les autorisations particulières attribuées aux dossiers publics à extension messagerie doivent être recréées dans le cloud, car les autorisations inter-sites ne sont pas prises en charge dans les scénarios de déploiement hybride. Pour plus d’informations, voir [Déploiements hybrides Exchange Server 2013](https://technet.microsoft.com/fr-fr/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).

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


1.  Sur le serveur Exchange 2013, exécutez la commande suivante pour synchroniser les dossiers publics à extension messagerie à partir de votre annuaire Active Directory local vers O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Où `Credential` est votre nom d’utilisateur et votre mot de passe Office 365 et `CsvSummaryFile` est le chemin d’accès de l’emplacement où vous voulez journaliser les opérations et les erreurs de synchronisation au format .csv.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant d’exécuter le script, nous vous recommandons de commencer par simuler les actions du script dans votre environnement en l’exécutant comme décrit ci-dessus avec le paramètre <code>-WhatIf</code>.<br />
Nous vous recommandons également d’exécuter ce script quotidiennement pour synchroniser vos dossiers publics à extension messagerie.</td>
</tr>
</tbody>
</table>


## Étape 3 : configuration des utilisateurs Exchange Online pour l’accès aux dossiers publics locaux Exchange 2013

La dernière étape de cette procédure consiste à configurer l’organisation Exchange Online et d’autoriser l’accès aux dossiers publics Exchange 2013.

Autorisez l’organisation Exchange Online à accéder aux dossiers publics en local. Vous pointerez vers l’ensemble de vos boîtes aux lettres de dossiers publics locales.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

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

