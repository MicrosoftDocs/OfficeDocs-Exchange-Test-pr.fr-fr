---
title: 'Réalisation d’une récupération de tonalité: Exchange 2013 Help'
TOCTitle: Réalisation d’une récupération de tonalité
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51407161
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Réalisation d’une récupération de tonalité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-27_

À l'aide de la portabilité de tonalité, les utilisateurs peuvent disposer d'une boîte aux lettres temporaire pour envoyer et recevoir des messages pendant que leur boîte aux lettres est restaurée ou réparée. La boîte aux lettres temporaire peut se trouver sur le même serveur de boîtes aux lettres Exchange 2013 ou sur tout autre serveur de boîtes aux lettres Exchange 2013 de votre organisation. Le processus d'utilisation de la portabilité de tonalité est appelé « récupération de tonalité » et implique la création d'une base de données vide sur un serveur de boîtes aux lettres pour remplacer la base de données endommagée. Pour plus d'informations, consultez la rubrique [Portabilité de tonalité](dial-tone-portability-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes, plus le temps nécessaire pour restaurer et déplacer les données.

  - Vous devez disposer d'un nombre de bases de données inférieur au nombre maximal déployé pour créer une base de données de tonalité. Exchange 2013 Standard Edition prend en charge au maximum cinq bases de données par serveur. Exchange 2013 Enterprise Edition prend en charge un maximum de 50 bases de données par serveur dans RTM et CU1, et 100 bases de données par serveur dans CU2 et les versions ultérieures.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Récupération de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer une récupération de tonalité sur un serveur unique

> [!NOTE]
> Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour effectuer une récupération de tonalité sur un serveur unique.


1.  Assurez-vous que tous les fichiers existants pour la base de données en cours de récupération sont préservés au cas où ils seraient nécessaires pour d'autres opérations de récupération.

2.  Utilisez la cmdlet [New-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997976\(v=exchg.150\)) pour créer une base de données de tonalité, comme indiqué dans cet exemple.
    
        New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB

3.  Utilisez la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) pour déplacer les boîtes aux lettres des utilisateurs hébergés sur la base de données en cours de récupération, comme indiqué dans cet exemple.
    
        Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1

4.  Utilisez la cmdlet [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\)) pour monter la base de données afin que les ordinateurs clients puissent accéder à la base de données ainsi qu'envoyer et recevoir des messages, comme indiqué dans cet exemple.
    
        Mount-Database -Identity DTDB1

5.  Créez une base de données de récupération (RDB) et restaurez ou copiez la base de données et les fichiers journaux contenant les données que vous souhaitez récupérer dans la RDB. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une base de données de récupération](create-a-recovery-database-exchange-2013-help.md).

6.  Après avoir copié la base de données de récupération mais avant de monter la base de données restaurée, copiez tous les fichiers journaux de la base de données endommagée dans le dossier journal de la base de données pour qu'ils puissent être lus dans la base de données restaurée.

7.  Montez la base de données de récupération, puis utilisez la cmdlet [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\)) pour la démonter, comme indiqué dans cet exemple.
    
        Mount-Database -Identity RDB1
        Dismount-Database -Identity RDB1

8.  Après avoir démonté la base de données de récupération, déplacez la base de données en cours et les fichiers journaux du dossier de base de données de récupération vers un emplacement sûr. Cette opération est effectuée en préparation de l'échange de la base de données récupérée avec la base de données de tonalité.

9.  Démontez la base de données de tonalité, comme illustré dans cet exemple. Notez que vos utilisateurs finaux vont connaître une interruption dans le service lors du démontage de cette base de données.
    
        Dismount-Database -Identity DTDB1

10. Déplacez la base de données et les fichiers journaux du dossier de base de données de tonalité vers le dossier de base de données de récupération.

11. Déplacez la base de données et les fichiers journaux d'un emplacement sûr contenant la base de données récupérée dans le dossier de base de données de tonalité, puis montez la base de données, comme indiqué dans cet exemple.
    
        Mount-Database -Identity DTDB1
    
    Cela met fin à l'interruption de service pour vos utilisateurs finaux. Ils pourront accéder à leur base de données de production d'origine, puis envoyer et recevoir des messages.

12. Montez la base de données de récupération, comme indiqué dans cet exemple.
    
        Mount-Database -Identity RDB1

13. Utilisez les cmdlets [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) et [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)) pour exporter les données de la base de données de récupération et les importer dans la base de données récupérée, comme indiqué dans l'exemple. Cette opération permet d'importer tous les messages envoyés et reçus à l'aide de la base de données de tonalité dans la base de données de production.
    
        $mailboxes = Get-Mailbox -Database DTDB1
    
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }

14. Après que l'opération de restauration est terminée, vous pouvez démonter et supprimer la base de données de récupération, comme indiqué dans cet exemple.
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997931\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien déplacé une boîte aux lettres, procédez comme suit :

  - Ouvrez la boîte aux lettres à l'aide de Microsoft Office Outlook Web App.

  - Ouvrez la boîte aux lettres à l'aide de Microsoft Outlook.

