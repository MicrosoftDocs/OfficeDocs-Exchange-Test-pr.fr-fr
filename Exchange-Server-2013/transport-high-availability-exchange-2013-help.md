---
title: 'Haute disponibilité du transport: Exchange 2013 Help'
TOCTitle: Haute disponibilité du transport
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 50479481
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Haute disponibilité du transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-15_

Dans Microsoft Exchange Server 2013, la haute disponibilité du transport est chargée de conserver les copies redondantes des messages avant et après leur remise réussie. Exchange 2013 améliore les fonctionnalités de haute disponibilité du transport introduites dans Exchange Server 2010, avec notamment la redondance des clichés instantanés et la benne de transport pour veiller à ce que les messages ne se perdent pas pendant le transit.

Voici un résumé des principales améliorations apportées à la haute disponibilité du transport dans Exchange 2013 :

  - La redondance des clichés instantanés crée une copie redondante du message sur un autre serveur avant que le message ne soit accepté ou reconnu. Peu importe que le serveur d'envoi prenne en charge ou non la redondance des clichés instantanés.

  - La redondance des clichés instantanés reconnaît les groupes de disponibilité de base de données (DAG) et les sites Active Directory comme limites de la haute disponibilité du transport. Cela réduit le nombre de serveurs pouvant contenir des copies redondantes des messages, et élimine le trafic inutile de maintenance des messages redondants sur les DAG et les sites Active Directory.
    
    Pour plus d’informations, consultez la rubrique [Redondance des clichés instantanés](shadow-redundancy-exchange-2013-help.md).

  - La benne de transport a également fait l'objet d'améliorations et s'appelle maintenant *Safety Net*. Safety Net enregistre les messages correctement traités par le service de transport sur les serveurs de boîtes aux lettres. Safety Net fonctionne mieux pour les serveurs de boîtes aux lettres dans un DAG, mais fonctionne également pour plusieurs serveurs de boîtes aux lettres sur le même site Active Directory n'appartenant pas à un DAG.

  - Safety Net est maintenant redondant sur un autre serveur. Ce détail est important pour éviter un point de défaillance unique dans Exchange 2013, car le service de transport et les bases de données de boîtes aux lettres sont situés sur le serveur de boîtes aux lettres.
    
    Pour plus d’informations, consultez la rubrique [Safety Net](safety-net-exchange-2013-help.md).

Le schéma suivant présente un aperçu détaillé de la façon dont la haute disponibilité du transport fonctionne dans Exchange 2013.

![Vue d’ensemble de la haute disponibilité du transport](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "Vue d’ensemble de la haute disponibilité du transport")

1.  Un serveur de boîtes aux lettres Exchange 2013 appelé Mailbox01 reçoit un message d'un serveur SMTP situé hors des limites de la haute disponibilité du transport. La *limite de la haute disponibilité du transport* est un DAG ou un site Active Directory au sein d'environnements dépourvus de DAG. Le message peut provenir d'un serveur SMTP tiers, d'un serveur SMTP Internet utilisant un proxy via le serveur d'accès au client, ou d'un autre serveur Exchange 2013.

2.  Avant d'accuser réception du message, Mailbox01 démarre une nouvelle session SMTP sur un autre serveur de boîtes aux lettres Exchange 2013 appelé Mailbox03 qui se situe dans les limites de la haute disponibilité du transport, et Mailbox03 réalise un cliché instantané du message. Dans les environnements DAG, un serveur de clichés instantanés au sein d'un site Active Directory constitue l'option préférée. Mailbox01 est le serveur principal contenant le message principal, et Mailbox3 est le serveur de clichés instantanés contenant le message de cliché instantané.

3.  Le service de Transport sur Mailbox01 traite le message principal.
    
    1.  Dans cet exemple, la boîte aux lettres du destinataire se situe sur Mailbox01, pour que le service de transport transmette le message au serveur de transport de la boîte aux lettres locale.
    
    2.  Le service de transport de la boîte aux lettres remet le message à la base de données de boîtes aux lettres locales.
    
    3.  Mailbox01 met en file d'attente un état de suppression pour Mailbox03 qui indique que le message principal a été traité correctement, et Mailbox01 déplace une copie du message principal dans le Safety Net principal local. Notez que le message se déplace entre les files d'attente au sein de la même base de données de file d'attente.

4.  Mailbox03 interroge périodiquement Mailbox01 afin d'obtenir l'état de suppression du message principal.

5.  Lorsque Mailbox03 détermine que Mailbox01 a traité correctement le message principal, Mailbox03 déplace le message de cliché instantané dans le Safety Net de cliché instantané local. Notez que le message se déplace entre les files d'attente au sein de la même base de données de file d'attente.

Le message est conservé dans le Safety Net principal et Safety Net de cliché instantané jusqu'à ce que le message expire suite à l'écoulement d'un délai d'attente configurable. Si un basculement de base de données de boîtes aux lettres se produit avant l'expiration du message, le Safety Net principal sur Mailbox01 renvoie le message. Si Mailbox01 n'est pas disponible, le Safety Net de cliché instantané sur Mailbox03 recommence et renvoie le message.

## Redondance des messages dans le service de transport frontal sur des serveurs d'accès au client

Un serveur d'accès au client n'a pas de files d'attente de messages. Il s'agit d'un service proxy dépourvu d'état qui utilise le service de transport frontal pour accepter les connexions SMTP entrantes et qui les transmet par proxy au service de transport sur un serveur de boîtes aux lettres. Le service de transport frontal maintient ouverte la session STMP avec le serveur d'envoi pendant que le message principal est transmis au service de transport sur un serveur de boîtes aux lettres, et un cliché instantané du message est réalisé par le service de transport sur un serveur de boîtes aux lettres différent au sein des limites de la haute disponibilité du transport. La fin de la commande SMTP de données est renvoyée au serveur SMTP d'envoi via le serveur d'accès au client uniquement lorsque le message principal et le message de cliché instantané sont correctement créés.

