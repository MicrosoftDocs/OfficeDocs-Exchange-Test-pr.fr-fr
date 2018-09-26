---
title: 'Ajout d’une copie de base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Ajout d’une copie de base de données de boîtes aux lettres
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50478507
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajout d’une copie de base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-30_

Lorsque vous ajoutez une copie de base de données de boîtes aux lettres, la réplication continue est automatiquement activée entre la base de données existante et la copie de la base de données. Une identité sous la forme \<*DatabaseName*\>\\\<*HostMailboxServerName*\> est automatiquement attribuée aux copies de base de données. Par exemple, la copie de la base de données DB1 hébergée sur le serveur MBX3 doit être DB1\\MBX3.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux copies de base de données de boîtes aux lettres ? Consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 2 minutes sont nécessaires, plus le temps d'amorçage de la copie de base de données, en fonction d'une grande variété de facteurs, tels que la taille de la base de données, la vitesse, la bande passante disponible et le temps de réponse du réseau ainsi que les vitesses de stockage.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrée « Copies de bases de données de boîtes aux lettres » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copie active de la base de données doit être montée.

  - Le serveur de boîte aux lettres spécifié ne doit pas déjà héberger une copie de base de données.

  - Le chemin d’accès à la copie de base de données et à ses fichiers journaux doit être disponible sur le serveur de boîtes aux lettres sélectionné.

  - Le serveur hébergeant la copie active et le serveur qui hébergera la copie passive doivent appartenir au même groupe de disponibilité de base de données (DAG). Le DAG doit avoir quorum et être sain.

  - Si vous ajoutez la deuxième copie d’une base de données (par exemple, la création de la première copie passive de la base de données), l’enregistrement circulaire ne doit pas être activé pour la base de données de boîtes aux lettres spécifiée. Si elle est activée, vous devez d’abord la désactiver. La journalisation circulaire pourra être activée après l’ajout de la copie de la base de données de boîtes aux lettres. Après activation de l’enregistrement circulaire pour une base de données de boîtes aux lettres répliquée, l’enregistrement circulaire de réplication continue est utilisé à la place de l’enregistrement circulaire JET. Si vous ajoutez la troisième copie ou copie subséquente d’une base de données, la connexion CRCL peut rester activée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour ajouter une copie de la base de données de boîtes aux lettres

1.  Dans la CCE, accédez à **Serveurs** \> **Bases de données**.

2.  Sélectionnez la base de données à copier, puis cliquez sur ![Ajouter une copie de base de données](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "Ajouter une copie de base de données").

3.  Sur la page **Ajouter une copie de base de données de boîtes aux lettres**, cliquez sur **Parcourir...**, sélectionnez le serveur de boîtes aux lettres qui hébergera la copie de base de données, puis cliquez sur **OK**.

4.  Vous pouvez également configurer le **Numéro de préférence d’activation** pour la copie de base de données.

5.  Cliquez sur **Plus d’options…** pour désigner la copie de base de données comme copie de base de données calorifugée en configurant un délai d’attente de relecture ou pour reporter l’amorçage automatique de la copie de base de données.

6.  Cliquez sur **Enregistrer** pour enregistrer les modifications apportées à la configuration et ajouter la copie de base de données de boîtes aux lettres.

7.  Cliquez sur **OK** pour accepter les messages qui s’affichent.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour ajouter une copie de base de données de boîtes aux lettres

Cet exemple ajoute une copie de la base de données de boîte aux lettres DB1 au serveur de boîtes aux lettres nommé MBX3. Le retard de relecture et le retard de troncation restent configurés à leurs valeurs par défaut de zéro et les préférences d’activation sont configurées avec la valeur 2.

```powershell
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2
```

Dans cet exemple, nous ajoutons une copie de la base de données de boîte aux lettres DB2 au serveur de boîtes aux lettres MBX4. Le retard de relecture et le retard de troncation sont conservés à leurs valeurs par défaut de zéro et les préférences d’activation sont configurées avec la valeur `5`. En outre, l’amorçage est différé pour cette copie afin de pouvoir l’amorcer à l’aide d’un serveur source local au lieu d’utiliser la copie active actuelle de la base de données qui est géographiquement éloignée de MBX4.

```powershell
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed
```

Dans cet exemple, nous ajoutons une copie de la base de données de boîtes aux lettres DB3 au serveur de boîtes aux lettres MBX5. Le retard de relecture est défini à 3 jours et le retard de troncation est maintenu à sa valeur par défaut de zéro ; les préférences d’activation sont configurées avec la valeur `4`.

```powershell
Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une copie de base de données de boîtes aux lettres, procédez de l’une des façons suivantes :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**. Sélectionnez la base de données qui a été copiée. Dans le volet Détails, l’état de la copie de la base de données et son index de contenu sont affichés avec la longueur de la file d’attente de copie actuelle.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier la création d’une copie saine de la base de données des boîtes aux lettres.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    ```
    
    Le statut et l’état de l’index de contenu doivent être sains.

## Pour plus d’informations

[Copies de bases de données de boîtes aux lettres](mailbox-database-copies-exchange-2013-help.md)

[Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md)

