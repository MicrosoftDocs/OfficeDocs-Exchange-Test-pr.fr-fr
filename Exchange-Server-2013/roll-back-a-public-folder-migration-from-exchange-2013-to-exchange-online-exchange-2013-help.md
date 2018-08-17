---
title: 'Restaurer une migr. de dossiers publics d’Exchange 2013 vers Exchange Online'
TOCTitle: Restauration d’une migration de dossiers publics à partir d’Exchange 2013 vers Exchange Online
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432745
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Restauration d’une migration de dossiers publics à partir d’Exchange 2013 vers Exchange Online

 

_**Dernière rubrique modifiée :** 2017-03-20_

**Résumé** : Suivez ces étapes pour redonner à votre infrastructure de dossiers publics son état pré-migration dans votre organisation Exchange 2013 locale.

Si vous rencontrez des problèmes avec la migration de dossiers publics sur Exchange Online, ou que vous avez besoin de réactiver vos dossiers publics Exchange 2013 pour toute autre raison, suivez les étapes ci-dessous.

## Annulation de la migration

Si vous restaurez la migration, vous perdrez tout le contenu qui a été ajouté aux dossiers publics dans Exchange Online après la migration, via les clients ou par courrier électronique pour les dossiers publics à extension messagerie. Pour enregistrer ce contenu, vous pouvez exporter le contenu des dossiers publics post-migration vers un fichier .pst, que vous pouvez ensuite importer dans les dossiers publics locaux une fois la restauration terminée.

1.  Dans votre environnement local Exchange, exécutez la commande suivante pour déverrouiller vos dossiers publics Exchange 2013 (le déverrouillage peut prendre plusieurs heures) :
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Dans votre environnement local Exchange, rétablissez l’élément `ExternalEmailAddress` pour tous les dossiers publics à extension messagerie mis à jour par SetMailPublicFolderExternalAddress.ps1 (le script utilisé dans *Étape 8 : Tester et déverrouiller des dossiers publics dans Exchange Online* de la rubrique [Utilisation de la migration par lot pour migrer des dossiers publics Exchange 2013 vers Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)). Vous pouvez vous reporter au fichier de résumé créé par le script pour identifier ceux qui ont été modifiés ou utiliser le fichier OnPrem\_MEPF.xml généré précédemment dans le même processus de migration par lots pour obtenir les propriétés d’origine de tous les dossiers publics à extension messagerie.

3.  Dans Exchange Online PowerShell, exécutez les commandes suivantes pour supprimer tous les dossiers publics et les boîtes aux lettres Exchange Online :
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  Dans votre environnement Exchange Online, exécutez la commande suivante pour rediriger le trafic de dossiers publics vers l’environnement local (Exchange 2013) :
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Reportez-vous à l’article [Configurer les dossiers publics Exchange 2013 pour un déploiement hybride](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md) pour obtenir des instructions sur la reconfiguration de l’accès à vos dossiers publics locaux, afin que les utilisateurs Exchange Online puissent y accéder.

