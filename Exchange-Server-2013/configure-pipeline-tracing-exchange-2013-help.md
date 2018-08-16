---
title: 'Configuration du suivi du pipeline: Exchange 2013 Help'
TOCTitle: Configuration du suivi du pipeline
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52062938
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du suivi du pipeline

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Le suivi du pipeline capture des copies de messages électroniques pendant qu'ils transitent dans le pipeline de transport du service de transport ou du service de transport de boîtes aux lettres sur un serveur de boîtes aux lettres et sur des serveurs de transport Edge.

## Ce qu'il faut savoir avant de commencer

  - Durée estimée de la procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultezEntrées « Service de transport » et « Service de transport de boîtes aux lettres » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Le suivi du pipeline copie le contenu complet des messages électroniques envoyés depuis l'adresse de messagerie de l'expéditeur. Pour éviter une exposition involontaire d'informations confidentielles, vous devez définir les autorisations de sécurité appropriées pour l'emplacement du dossier de suivi du pipeline.

  - N'activez pas le suivi du pipeline pour de longues périodes. Le suivi du pipeline génère plusieurs fichiers instantanés de message qui s'accumulent rapidement. Surveillez toujours l'espace disque disponible quand le suivi du pipeline est activé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Activer et configurer le suivi du pipeline

## Étape 1 : utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer l'adresse d'expéditeur pour le suivi du pipeline

La syntaxe suivante permet de configurer l'adresse d'expéditeur pour le suivi du pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

Cet exemple permet de configurer le suivi du pipeline de manière à capturer des instantanés de tous les messages que l'expéditeur chris@contoso.com a envoyés dans le service de transport sur le serveur de boîtes aux lettres intitulé Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

Cet exemple permet de configurer le suivi du pipeline pour capturer des instantanés de tous les messages générés par le système que le service de transport a reçus sur le serveur de boîtes aux lettres Mailbox02.

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"

> [!CAUTION]
> La configuration du suivi du pipeline de manière à capturer tous les messages que le serveur a générés dans un service de transport peut augmenter la charge sur le serveur et rapidement consommer l'espace disque disponible. Surveillez toujours l'espace disque disponible quand le suivi du pipeline est activé.


## Étape 2 : (facultative) utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier un dossier de suivi du pipeline personnalisé

Le dossier de suivi du pipeline par défaut n'existe pas tant que vous n'avez pas activé le suivi du pipeline. Par ailleurs, les messages qui répondent aux critères que vous spécifiez à l'aide du paramètre *PipelineTracingSenderAddress* sont transmis via le service de transport sur le serveur. Pour le service de transport sur un serveur de boîtes aux lettres, l'emplacement par défaut est `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. Pour le service de transport de boîtes aux lettres sur un serveur de boîtes aux lettres, l'emplacement par défaut est `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. Si vous spécifiez un chemin d'accès personnalisé, ce dernier doit être situé sur le serveur Exchange local.

La syntaxe suivante permet de configurer le dossier de suivi du pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

Cet exemple permet de définir le dossier de suivi du pipeline pour le service de transport du serveur de boîtes aux lettres Mailbox01 sur D:\\Hub\\Pipeline Tracing.

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## Étape 3 : utiliser l'environnement de ligne de commande Exchange Management Shell pour activer le suivi du pipeline

Par défaut, le suivi du pipeline est désactivé sur tous les serveurs Exchange. Quand vous activez le suivi du pipeline, vous activez cette fonctionnalité uniquement dans le service de transport spécifié sur le serveur Exchange spécifié. Avant d'activer le suivi du pipeline, vous devez spécifier l'adresse d'expéditeur comme décrit dans l'étape 1.

La syntaxe suivante permet d'activer le suivi du pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

Cet exemple permet d'activer le suivi du pipeline dans le service de transport sur le serveur de boîtes aux lettres Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré le suivi du pipeline, procédez comme suit :

1.  Exécutez la commande suivante :
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

3.  Accédez au dossier de suivi du pipeline pour le service de transport ou pour le service de transport de boîtes aux lettres et vérifiez que les fichiers instantanés de messages sont créés dans le dossier.

## Désactiver le suivi du pipeline

En raison de l'espace disque et des problèmes de sécurité liés au suivi du pipeline, ce dernier constitue une action temporaire à des fins de diagnostic ou de dépannage. Quand vous activez le suivi du pipeline, n'oubliez pas de désactiver cette fonctionnalité lorsque vous avez terminé.

La syntaxe suivante permet de désactiver le suivi du pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

Cet exemple permet de désactiver le suivi du pipeline dans le service de transport sur le serveur de boîtes aux lettres Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement désactivé le suivi du pipeline, procédez comme suit :

1.  Exécutez la commande suivante :
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  Vérifiez que le paramètre *PipelineTracingEnabled* a la valeur $false.

3.  Accédez au dossier de suivi du pipeline et vérifiez que les fichiers instantanés de messages ne sont plus créés dans le dossier.

