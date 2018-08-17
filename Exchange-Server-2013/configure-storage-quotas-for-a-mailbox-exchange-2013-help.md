---
title: 'Config. de quotas de stockage pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Configuration de quotas de stockage pour une boîte aux lettres
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50555400
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de quotas de stockage pour une boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-07-07_

**Résumé** : Utilisez le CAE ou Shell pour définir des quotas de stockage pour des boîtes aux lettres spécifiques.

Les quotas de stockage vous permettent de contrôler la taille des boîtes aux lettres et de gérer la croissance des bases de données de boîtes aux lettres. Lorsqu’une boîte aux lettres atteint ou dépasse un quota de stockage défini, Exchange envoie une notification au propriétaire de la boîte aux lettres.

> [!NOTE]
> Les quotas de stockage s’appliquent à la taille d’une boîte aux lettres donnée, tel que défini par la propriété <code>TotalItemSize</code> lorsque vous exécutez la cmdlet <code>Get-MailboxStatistics</code>. Pour plus d’informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/bb124612(v=exchg.150)">Get-MailboxStatistics</a>.


Des quotas de stockage sont généralement configurés pour chaque base de données. Autrement dit, les quotas configurés pour une base de données de boîtes aux lettres s’appliquent à toutes les boîtes aux lettres de cette base de données. Pour plus d’informations sur la gestion des paramètres de boîtes aux lettres pour chaque base de données, consultez la rubrique [Gestion des bases de données de boîtes aux lettres dans Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Cette rubrique vous explique comment personnaliser les paramètres de stockage d’une boîte aux lettres spécifique au lieu d’utiliser les paramètres de stockage de la base de données de boîtes aux lettres. Pour connaître les tâches de gestion supplémentaires relatives aux boîtes aux lettres utilisateur, consultez la rubrique [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Configuration des quotas de stockage d’une boîte aux lettres à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres dont vous souhaitez modifier les quotas de stockage, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés de la boîte aux lettres, cliquez sur **Utilisation de la boîte aux lettres**, puis sur **Plus d’options**.

4.  Cliquez sur **Personnaliser les paramètres de cette boîte aux lettres**, puis configurez les champs suivants. La plage de valeurs de tous les paramètres de quota de stockage s’étend de 0 à 2047 gigaoctets (Go).
    
      - **Émettre un avertissement à (Go)**   Ce champ affiche la limite de stockage maximale avant qu’un avertissement ne soit présenté à l’utilisateur. Si la taille de la boîte aux lettres atteint ou dépasse la valeur spécifiée, Exchange envoie un message d’avertissement à l’utilisateur.
        
        > [!IMPORTANT]
        > Le message associé au quota <strong>Émettre un avertissement</strong> ne sera pas envoyé à l’utilisateur, sauf si la valeur de ce paramètre est supérieure à 50 % de la valeur spécifiée dans le quota <strong>Interdire l’envoi</strong>. Si vous définissez par exemple le quota <strong>Interdire l’envoi</strong> sur 8 Mo, vous devez définir le quota <strong>Émettre un avertissement</strong> sur au moins 4 Mo. Dans le cas contraire, le message de quota <strong>Émettre un avertissement</strong> ne sera pas envoyé.
    
      - **Interdire l’envoi à (Go)**   Ce champ affiche la limite d’*interdiction d’envoi* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l’utilisateur d’envoyer de nouveaux messages et affiche un message d’erreur descriptif.
    
      - **Interdire l’envoi et la réception à (Go)**   Ce champ affiche la limite d’*interdiction d’envoi et de réception* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l’utilisateur de la boîte aux lettres d’envoyer de nouveaux messages et ne remettra plus de nouveaux messages dans la boîte aux lettres. Tous les messages envoyés à cette boîte aux lettres seront renvoyés à l’expéditeur avec un message d’erreur descriptif.

5.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utilisez l’environnement de ligne de commande Exchange Management Shell pour configurer des quotas de stockage pour une boîte aux lettres

Cet exemple montre comment définir les quotas d’avertissement, d’interdiction d’envoi et d’interdiction d’envoi et de réception pour la boîte aux lettres de Joe Healy sur 24,5 Go, 24,75 Go et 25 Go respectivement.

> [!NOTE]
> Pour vous assurer que les paramètres personnalisés de la boîte aux lettres sont utilisés à la place des paramètres par défaut de la base de données, vous devez définir le paramètre <em>UseDatabaseQuotaDefaults</em> sur <code>$false</code>.


    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

Cet exemple montre comment définir les quotas d’avertissement, d’interdiction d’envoi et d’interdiction d’envoi et de réception pour la boîte aux lettres d’Ayla Kol sur 900 mégaoctets (Mo), 950 Mo et 1 Go respectivement, et configurer la boîte aux lettres pour utiliser les paramètres personnalisés.

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les quotas de stockage d’une boîte aux lettres, procédez de l’une des manières suivantes :

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez vérifier les quotas de stockage, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés de la boîte aux lettres, cliquez sur **Utilisation de la boîte aux lettres**, puis sur **Plus d’options**.

4.  Vérifiez que l’option **Personnaliser les paramètres de cette boîte aux lettres** est sélectionnée.

5.  Vérifiez les paramètres de quota de stockage.

Ou

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

