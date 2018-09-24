---
title: 'Déplacer une BDD de BAL avec la portabilité de BDD: Exchange 2013 Help'
TOCTitle: Déplacer une base de données de boîtes aux lettres à l’aide de la portabilité de base de données
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51407214
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Déplacer une base de données de boîtes aux lettres à l’aide de la portabilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-16_

Vous pouvez utiliser la fonctionnalité de portabilité de base de données pour déplacer une base de données de boîtes aux lettres Microsoft Exchange Server 2013 entre des serveurs de boîtes aux lettres Exchange 2013 de la même organisation. Cela permet de réduire la durée globale de récupération pour certains scénarios de défaillance. Pour plus d'informations, consultez la rubrique [Portabilité des bases de données](database-portability-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes, plus le temps nécessaire pour restaurer les données, déplacer les fichiers de base de données et patienter le temps de terminer la réplication Active Directory.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Récupération de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour déplacer des boîtes aux lettres utilisateur vers une base de données de tonalité ou récupérée à l'aide de la fonctionnalité de portabilité de base de données.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer des boîtes aux lettres d'utilisateur vers une base de données de tonalité à l'aide de la fonction de portabilité de base de données

1.  Vérifiez que l’état de la base de données à déplacer est correct. Si tel n'est pas le cas, procédez à une récupération logicielle.
    
    > [!NOTE]
    > Lorsque vous effectuez une récupération logicielle, tout fichier journal non validé est validé dans la base de données. Si vous ne disposez pas de tous les fichiers journaux requis, vous ne pouvez pas exécuter le processus de récupération logicielle. Passez à l'étape 2.
    
    Pour valider tous les fichiers journaux non validés dans la base de données, à partir d'une invite de commandes, exécutez la commande suivante :
    
    ```powershell
    ESEUTIL /R <Enn>
    ```
    
    > [!NOTE]
    > Les lettres &lt;E<em>nn</em>&gt; spécifient le préfixe de fichier journal pour la base de données dans laquelle vous voulez relire les fichiers journaux. Le préfixe de fichier journal spécifié par &lt;E<em>nn</em>&gt; est un paramètre obligatoire pour Eseutil /r.


2.  Créez une base de données sur un serveur à l’aide de la syntaxe suivante :
    
    ```powershell
    New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>
    ```

3.  Définissez l’attribut *This database can be over written by restore* à l’aide de la syntaxe suivante :
    
    ```powershell
    Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true
    ```

4.  Déplacez les fichiers de base de données d’origine (fichier.edb, fichiers journaux et catalogue de recherche Exchange) dans le dossier de base de données que vous avez spécifié lorsque vous avez créé la base de données ci-dessus.

5.  Montez la base de données à l’aide de la syntaxe suivante :
    
    ```powershell
    Mount-Database <DatabaseName>
    ```

6.  Une fois la base de données montée, modifiez les paramètres du compte d'utilisateur avec la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) de façon à ce que le compte pointe vers la boîte aux lettres sur le nouveau serveur de boîtes aux lettres. Pour déplacer l'ensemble des utilisateurs de l'ancienne base de données vers la nouvelle base de données, utilisez la syntaxe suivante :
    
    ```powershell
    Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>
    ```

7.  Déclenchez la remise de tous les messages restants dans les files d’attente à l’aide de la syntaxe suivante.
    
    ```powershell
    Get-Queue <QueueName> | Retry-Queue -Resubmit $true
    ```

Une fois la réplication Active Directory terminée, tous les utilisateurs peuvent accéder à leurs boîtes aux lettres sur le nouveau serveur Exchange. La plupart des clients sont redirigés via la découverte automatique. Les utilisateurs de Microsoft Office Outlook Web App sont également automatiquement redirigés.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien déplacé une boîte aux lettres, procédez comme suit :

  - Ouvrez la boîte aux lettres à l'aide d'Outlook Web App.

  - Ouvrez la boîte aux lettres à l'aide de Microsoft Outlook.

