---
title: 'Config. manuelle du flux de messag. du srv de transp. Edge: Exchange 2013 Help'
TOCTitle: Configuration manuelle du flux de messagerie du serveur de transport Edge
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61180546
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration manuelle du flux de messagerie du serveur de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-21_

Cette rubrique décrit les procédures à suivre pour apporter manuellement des modifications à la configuration concernant la façon dont un serveur de transport Edge gère le flux de messagerie. Ces procédures sont conçues pour répondre à des scénarios spécifiques. À moins que votre organisation ait des besoins spécifiques impliquant la modification manuelle de la configuration, il est recommandé d’utiliser la configuration par défaut lors de l’abonnement aux serveurs de transport Edge.

**Contenu de cette rubrique**

Configurer manuellement des connecteurs d’envoi

Connecteurs d’envoi intra-organisationnels

Créer des connecteurs d’envoi supplémentaires après l’abonnement Edge

Motifs de suppression de la création automatique des connecteurs d’envoi

Flux de messagerie de partition

Router le courrier électronique sortant vers un hôte actif

Configurer des connecteurs d’envoi pour les domaines de relais externes

## Configurer manuellement des connecteurs d’envoi

Vous pouvez modifier manuellement la configuration d’un connecteur d’envoi. Par exemple, si vous devez router un message électronique sortant via un hôte actif, vous pouvez supprimer la création automatique d’un connecteur d’envoi et configurer manuellement un connecteur d’envoi vers Internet.

## Connecteurs d’envoi intra-organisationnels

Le connecteur d’envoi intra-organisationnel est un connecteur d’envoi implicite et masqué, créé automatiquement par Exchange. Il permet au service de transport sur les serveurs de boîtes aux lettres d’une même organisation de relayer des messages entre eux sans utiliser de connecteurs d’envoi explicites. Comme un objet de configuration associé à un site Active Directory existe dans Active Directory pour un abonnement Edge, le connecteur d’envoi intra-organisationnel est également utilisé pour relayer des messages vers ce serveur de transport Edge.

Seuls les serveurs de boîtes aux lettres situés dans le site Active Directory abonné peuvent transférer les messages électroniques directement depuis ou vers le serveur de transport Edge abonné. Si vous avez une forêt Active Directory multi-sites et si Exchange est déployé dans plusieurs sites, les serveurs de boîtes aux lettres dans les sites non abonnés routent le courrier électronique sortant vers le site abonné. Un serveur de boîtes aux lettres du site abonné route le courrier électronique sortant vers le serveur de transport Edge.

## Créer des connecteurs d’envoi supplémentaires après l’abonnement Edge

Une fois un serveur de transport Edge abonné à un site Active Directory, les cmdlets de création et de modification des connecteurs d’envoi sont désactivées sur le serveur de transport Edge. Si vous voulez créer un connecteur d’envoi dont le serveur source est le serveur de transport Edge, vous pouvez créer le connecteur d’envoi au sein de l’organisation Exchange. Vous pouvez spécifier un ou plusieurs abonnements Edge comme serveur source pour un connecteur d’envoi. Vous ne pouvez pas spécifier à la fois des serveurs de boîtes aux lettres et des abonnements Edge comme serveurs sources pour un même connecteur d’envoi. Le connecteur d’envoi sera répliqué dans l’instance AD LDS du serveur de transport Edge configuré comme serveur source lors de la prochaine synchronisation des données de configuration par EdgeSync. Si vous spécifiez plusieurs abonnements Edge comme serveur source, la charge liée aux connexions à ce connecteur d’envoi sera équilibrée entre les serveurs de transport Edge abonnés. Les serveurs de transport Edge doivent être abonnés au même site Active Directory pour que la charge soit équilibrée. Si des abonnements Edge dans différents sites Active Directory sont configurés comme serveurs sources sur le même connecteur d’envoi, les serveurs de transport Edge routent les messages vers le serveur source le plus proche uniquement.

Vous devrez créer manuellement des connecteurs d’envoi dans les cas suivants :

  - Vous avez supprimé la création automatique des connecteurs d’envoi entrants ou Internet.

  - Vous avez des domaines acceptés dans votre organisation qui sont configurés comme domaines de relais externes.

## Motifs de suppression de la création automatique des connecteurs d’envoi

Selon la topologie de votre organisation Exchange, vous pouvez décider de supprimer la création automatique des connecteurs d’envoi. Les exemples suivants décrivent des scénarios pour lesquels vous devez supprimer la création automatique des connecteurs d’envoi.

## Flux de messagerie de partition

Si vous décidez de partitionner le traitement du courrier entrant et sortant entre deux serveurs de transport Edge, un serveur de transport Edge est chargé du traitement du flux de messagerie sortant et le second serveur de transport Edge est chargé du traitement du flux de messagerie entrant. Pour ce faire, configurez les abonnements Edge comme suit :

  - Pour le serveur de transport Edge sortant, exécutez la commande suivante sur le serveur de boîtes aux lettres.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - Pour le serveur de transport Edge entrant, exécutez la commande suivante sur le serveur de boîtes aux lettres.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## Router le courrier électronique sortant vers un hôte actif

Si votre organisation Exchange route l’ensemble du courrier électronique sortant via un hôte actif, le connecteur d’envoi créé automatiquement ne sera pas correctement configuré.

Exécutez la commande suivante sur le serveur de boîtes aux lettres pour supprimer la création automatique du connecteur d’envoi vers Internet.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

À la fin du processus d’abonnement Edge, créez manuellement un connecteur d’envoi vers Internet. Créez le connecteur d’envoi au sein de l’organisation Exchange et sélectionnez l’abonnement Edge comme serveur source pour le connecteur. Sélectionnez le type d’utilisation `Custom` et configurez un ou plusieurs hôtes actifs. Le nouveau connecteur d’envoi est répliqué dans l’instance AD LDS du serveur de transport Edge lors de la prochaine synchronisation des données de configuration par le service EdgeSync. Vous pouvez forcer la synchronisation EdgeSync immédiate en exécutant la cmdlet **Start-EdgeSynchronization** sur un serveur de boîtes aux lettres.

Exemple : utilisation de l’environnement de ligne de commande Exchange Management Shell pour configurer un connecteur d’envoi pour un serveur de transport Edge abonné afin de router les messages vers tous les espaces d’adressage Internet via un hôte actif. Exécutez cette tâche sur un serveur de boîtes aux lettres dans l’organisation Exchange, et non sur le serveur de transport Edge.

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName

> [!IMPORTANT]
> Aucun mécanisme d’authentification de l’hôte actif n’est spécifié dans cet exemple. Veillez à configurer le bon mécanisme d’authentification et d’indiquer toutes les informations d’identification nécessaires lors de la création du connecteur d’hôte actif dans votre propre organisation Exchange.


## Configurer des connecteurs d’envoi pour les domaines de relais externes

Si vous avez des domaines acceptés configurés comme domaines de relais externes au sein de votre organisation Exchange, vous devez créer manuellement un connecteur d’envoi pour ces espaces d’adressage. Les messages en cours de remise aux domaines de relais externes sont relayés par le serveur de transport Edge. Le processus d’abonnement Edge n’assure pas la création et la configuration automatiques des connecteurs d’envoi pour les domaines de relais externes. Par conséquent, vous devez configurer les connecteurs d’envoi pour ces domaines et spécifier un ou plusieurs abonnements Edge comme serveur source pour ces connecteurs d’envoi.

L’enregistrement de ressource MX DNS pour un domaine de relais externe est résolu sur votre serveur de transport Edge. Vous pouvez configurer un connecteur d’envoi qui transmet le courrier électronique vers un domaine de relais externe pour utiliser un hôte actif pour le routage. La configuration du connecteur d’envoi pour un domaine de relais externe afin d’utiliser un routage DNS crée une boucle de routage. Pour plus d’informations sur les domaines de relais externes, voir [Domaines acceptés](accepted-domains-exchange-2013-help.md).

Retour au début

