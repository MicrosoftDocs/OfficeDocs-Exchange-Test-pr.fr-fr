---
title: 'Gestion de la haute disponibilité et de la résilience de site: Exchange 2013 Help'
TOCTitle: Gestion de la haute disponibilité et de la résilience de site
ms:assetid: f9677392-88d2-457f-a488-245771a8c1f2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638215(v=EXCHG.150)
ms:contentKeyID: 50479595
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion de la haute disponibilité et de la résilience de site

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-05_

Après avoir créé, validé et déployé une solution de haute disponibilité ou de résilience de site Microsoft Exchange Server 2013, la solution passe de la phase de déploiement à la phase opérationnelle du cycle de vie de la solution globale. La phase opérationnelle se compose de plusieurs tâches. Toutes les tâches sont liées à l’un des domaines suivants : groupes de disponibilité de base de données (DAG), copies de base de données de boîte aux lettres, réalisation de la surveillance proactive, et gestion des switchovers et des basculements.

**Contenu de cette rubrique**

Gestion du groupe de disponibilité de la base de données

Gestion des copies de base de données de boîtes aux lettres

Surveillance proactive

Switchovers et basculements

## Gestion des groupes de disponibilité de base de données

Les tâches de gestion des opérations associées aux DAG sont les suivantes :

  - **Création d'un ou de plusieurs DAG**   La création d'un DAG s'effectue généralement en une seule fois lors de la phase de déploiement du cycle de vie de la solution. Il est cependant possible de créer des groupes de disponibilité de base de données (DAG) pendant la phase opérationnelle, par exemple :
    
      - Le DAG est configuré pour un mode de réplication tiers mais vous souhaitez revenir à la réplication continue. Vous ne pouvez pas faire revenir un DAG à la réplication continue, vous devez en créer un autre.
    
      - Vous disposez de serveurs dans plusieurs domaines. Tous les membres d'un même DAG doivent également être membres du même domaine.

  - **Gestion de l'appartenance au DAG**   La gestion des membres d'un DAG est une tâche peu fréquente, généralement exécutée durant la phase de déploiement du cycle de vie de la solution. Toutefois, en raison de la flexibilité offerte par le déploiement incrémentiel, la gestion de l'appartenance au DAG peut aussi avoir lieu tout au long du cycle de vie de la solution.

  - **Configuration des propriétés du DAG**   Chaque DAG comporte plusieurs propriétés configurables selon les besoins. Ces propriétés sont les suivantes :
    
      - **Serveur témoin et répertoire témoin**   Le serveur témoin est situé à l'extérieur du DAG et agit en tant que votant du quorum lorsque le DAG contient un nombre pair de membres. Le répertoire témoin est créé et partagé sur le serveur témoin afin d'être utilisé par le système lors de la gestion du quorum.
    
      - **Adresses IP**   Chaque DAG possède une ou plusieurs adresses IPv4 et, en option, une ou plusieurs adresses IPv6. Les adresses IP attribuées au DAG sont utilisées par le cluster sous-jacent du DAG. Le nombre d'adresses IPv4 affectées au DAG est égal au nombre de sous-réseaux qui incluent le réseau MAPI utilisé par le DAG. Vous pouvez configurer le DAG pour qu'il utilise des adresses IP statiques ou pour qu'il obtienne des adresses automatiquement à l'aide du protocole DHCP.
    
      - **Mode de coordination de l’activation du centre de données**   Ce mode est un paramètre de propriété d’un DAG conçu pour prévenir des conditions de « split-brain » au niveau de la base de données, dans un scénario où vous restaurez un service pour un centre de données principal après qu’un basculement de centre de données a été effectué. Pour plus d’informations sur le mode de coordination de l’activation du centre de données, voir l’article [Mode de coordination de l’activation du centre de données](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
      - **Serveur témoin secondaire et répertoire témoin secondaire**   Le serveur témoin secondaire et le répertoire témoin secondaire sont des valeurs que vous pouvez préalablement configurer dans le cadre du processus de planification pour un basculement de centre de données. Ces valeurs font référence au serveur témoin et au répertoire témoin qui sera utilisé lorsqu'un basculement de centre de données a eu lieu.
    
      - **Port de réplication**   Par défaut, tous les DAG utilisent le port TCP 64327 pour la réplication continue. Vous pouvez modifier le DAG afin d’utiliser un autre port TCP pour la réplication à l'aide du paramètre *ReplicationPort* de la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)).
    
      - **Découverte du réseau**   Vous pouvez forcer le DAG à redécouvrir les réseaux et les interfaces réseau. Cette opération permet d'ajouter ou de supprimer des réseaux ou d'introduire de nouveaux sous-réseaux. Vous pouvez forcer la redécouverte de tous les réseaux du DAG à l'aide du paramètre *DiscoverNetworks* de la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)).
    
      - **Compression du réseau**   Par défaut, la compression est utilisée uniquement entre les réseaux du DAG sur différents sous-réseaux. Vous pouvez activer la compression pour tous les réseaux du DAG ou pour des opérations d'amorçage uniquement, ou désactiver la compression pour tous les réseaux du DAG.
    
      - **Chiffrement du réseau**   Par défaut, le chiffrement est utilisé uniquement entre les réseaux du DAG sur différents sous-réseaux. Vous pouvez activer le chiffrement pour tous les réseaux du DAG ou pour des opérations d'amorçage uniquement, ou désactiver le chiffrement pour tous les réseaux du DAG.

  - **Arrêt des membres du DAG**   La solution haute disponibilité Exchange 2013 est intégrée au processus d'arrêt de Windows. Si un administrateur ou une application arrête un serveur Windows dans un DAG qui a une base de données montée répliquée sur un ou plusieurs membres du DAG, le système tentera d’activer une autre copie des bases de données montées avant de terminer le processus d’arrêt. Toutefois, ce nouveau comportement ne garantit pas que toutes les bases de données sur le serveur en cours de fermeture bénéficieront d’une activation sans perte. C’est pourquoi il est préférable d’effectuer un basculement de serveur avant d’arrêter un serveur membre d’un DAG.

Pour obtenir la procédure détaillée de création d’un DAG, voir [Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md). Pour obtenir la procédure détaillée de configuration des DAG et des propriétés de DAG, voir l’article [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md). Pour plus d'informations sur chaque tâche de gestion évoquée précédemment et sur la gestion des DAG en général, voir l’article [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

Retour au début

## Gestion des copies de base de données de boîtes aux lettres

Les tâches de gestion des opérations associées aux copies de base de données de boîte aux lettres sont les suivantes :

  - **Ajout de copies de base de données de boîtes aux lettres**   Lorsque vous ajoutez une copie de base de données de boîtes aux lettres, la réplication continue est automatiquement activée entre la base de données existante et la copie de la base de données.

  - **Configuration des propriétés de copie de base de données**   Vous pouvez configurer un grand nombre de propriétés, comme la stratégie d'activation de la base de données, la durée (le cas échéant) d'attente de relecture et le délai d'attente de troncation, ainsi que la préférence d'activation pour la copie de base de données.

  - **Interruption ou reprise de la copie de base de données de boîtes aux lettres**   Vous pouvez suspendre la copie d'une base de données de boîtes aux lettres en préparation pour l'amorçage ou pour d'autres formes de maintenance. Vous pouvez également interrompre la copie de base de données de boîte aux lettres pour l'activation uniquement. Cette configuration empêche le système d'activer automatiquement la copie suite à une défaillance, mais permet néanmoins au système de conserver la copie de la base de données à jour par rapport à l'envoi des journaux et à leur relecture.

  - **Mise à jour d’une copie de base de données de boîtes aux lettres**   La mise à jour, également appelée *amorçage*, est le processus par lequel une copie de base de données de boîtes aux lettres est ajoutée à un autre serveur de boîtes aux lettres. Elle devient la base de données de base pour la copie. Après le premier amorçage de la copie de la base de données de base, ce n'est que dans de très rares circonstances que la base de données nécessitera un nouvel amorçage.

  - **Activation d’une copie de base de données de boîtes aux lettres**   Ce processus consiste à désigner une copie passive spécifique comme nouvelle copie active d'une base de données de boîtes aux lettres. Ce processus est parfois appelé *switchover*. Pour plus d'informations, voir « Switchovers et basculements » plus loin dans cette rubrique.

  - **Suppression d'une copie d'une base de données de boîtes aux lettres**   Vous pouvez supprimer une copie d'une base de données de boîtes aux lettres à tout moment. Occasionnellement, il peut s'avérer nécessaire de supprimer une copie de base de données de boîtes aux lettres. Par exemple, vous ne pouvez pas supprimer une copie de base de données de boîtes aux lettres d'un DAG tant que toutes les copies de base de données de boîtes aux lettres n'ont pas été supprimées du serveur. Par ailleurs, vous devez supprimer toutes les copies d'une base de données de boîtes aux lettres avant de pouvoir modifier le chemin d'accès d'une base de données de boîtes aux lettres.

Pour obtenir la procédure détaillée d’ajout d’une copie de base de données de boîtes aux lettres, voir [Ajout d’une copie de base de données de boîtes aux lettres](add-a-mailbox-database-copy-exchange-2013-help.md). Pour obtenir la procédure détaillée de configuration des copies de base de données de boîtes aux lettres, voir [Configurer les propriétés des copies de la base de données de boîtes aux lettres](configure-mailbox-database-copy-properties-exchange-2013-help.md). Pour plus d'informations sur chaque tâche de gestion évoquée précédemment et sur la gestion des copies de base de données de boîtes aux lettres, voir [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md). Pour obtenir la procédure détaillée de suppression d’une copie de base de données de boîtes aux lettres, voir [Supprimer une copie de base de données de boîtes aux lettres](remove-a-mailbox-database-copy-exchange-2013-help.md).

Retour au début

## Surveillance proactive

Vérifier que vos serveurs fonctionnent correctement et que vos copies de base de données sont saines est un objectif essentiel pour les opérations de messagerie quotidiennes. Exchange 2013 comprend plusieurs fonctionnalités qui peuvent servir à effectuer diverses tâches d’analyse du fonctionnement pour les DAG et les copies de base de données de boîte aux lettres, y compris :

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/fr-fr/library/bb691314\(v=exchg.150\))

  - Journalisation des événements du canal Crimson

Outre l’analyse du fonctionnement et de l’état, il est également essentiel de surveiller des situations risquant de compromettre la disponibilité. Par exemple, nous vous conseillons de surveiller la redondance de vos bases de données répliquées. Il est essentiel d’éviter des situations dans lesquelles il ne vous reste qu’une seule copie d’une base de données. Ce scénario doit être prioritaire et résolu le plus tôt possible.

Pour obtenir des informations plus détaillées sur l’analyse du fonctionnement et de l’état des DAG et des copies de base de données de boîtes aux lettres, voir [Surveillance des groupes de disponibilité des bases de données](monitoring-database-availability-groups-exchange-2013-help.md).

Retour au début

## Switchovers et basculements

Un *switchover* est un processus manuel par lequel un administrateur active manuellement une ou plusieurs copies de base de données de boîtes aux lettres. Les switchovers peuvent avoir lieu au niveau de la base de données ou du serveur et sont généralement exécutés dans le cadre de la préparation des activités de maintenance. La gestion des switchovers implique l'exécution de switchovers de base de données ou de serveur selon les besoins. Par exemple, si vous devez effectuer des opérations de maintenance sur un serveur de boîtes aux lettres de votre DAG, il est préférable d'exécuter en premier lieu un switchover de serveur afin que ce dernier n'héberge aucune copie active de base de données de boîtes aux lettres. Pour connaître la procédure détaillée d’exécution d’un basculement de base de données, consultez la rubrique [Activer une copie de la base de données de boîtes aux lettres](activate-a-mailbox-database-copy-exchange-2013-help.md). Les switchovers peuvent également être effectués au niveau du centre de données.

Un *basculement* est l'activation automatique par le système d'une ou de plusieurs copies de base de données en réaction à une défaillance. Par exemple, la perte d'un disque dans un environnement non-RAID déclenche un basculement de base de données. La perte d'un réseau MAPI ou une panne d'électricité déclenche un basculement de serveur.

Retour au début

