---
title: 'Agents de remise et connecteurs d’agent de remise: Exchange 2013 Help'
TOCTitle: Agents de remise et connecteurs d’agent de remise
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50477900
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agents de remise et connecteurs d’agent de remise

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Un agent de remise peut remettre des messages à partir de votre environnement Exchange Server SMTP à un système qui n’utilise pas le protocole SMTP. Chaque agent de remise est associé à un connecteur d’agent de remise qui place en attente les messages acheminés à un agent de remise pour le traitement et la livraison au système ou périphérique non-SMTP.

> [!TIP]
> Tant que l’architecture du connecteur étranger reste dans Microsoft Exchange 2013, il est conseillé d’utiliser les agents de remise pour le routage des messages vers des systèmes autres que SMTP chaque fois que possible. Les principales raisons de cette opération sont que vous pouvez utiliser la gestion de la file d’attente pour les messages, qu’il est inutile de gérer le transfert de fichiers dans un répertoire de dépôt, et que vous pouvez vérifier la remise des messages.


**Contenu de cette rubrique**

Fonction et avantages des agents de remise

Ajout des agents de remise à votre organisation

Connecteurs d’agent de remise

Connecteur d’agent de remise de messagerie texte par défaut

## Fonction et avantages des agents de remise

Un agent de remise est un composant installé dans le service de Transport d’un serveur de boîtes aux lettres capable d’effectuer les tâches suivantes :

  - Établir une connexion avec le système étranger pour la remise des messages.

  - Récupérer des messages depuis les files d’attente de remise sur des serveurs de boîtes aux lettres.

  - Remettre les messages au système étranger.

  - Confirmer chaque remise de message réussie.

Tant que l’architecture du connecteur étranger reste dans Microsoft Exchange Server 2013, il est conseillé d’utiliser les agents de remise pour le routage des messages vers des systèmes autres que SMTP chaque fois que possible. Les agents de remise offrent les avantages suivants :

  - Ils permettent la gestion de la file d’attente des messages acheminés vers des systèmes étrangers.

  - Étant donné que les messages n’ont plus besoin d’être écrits sur et lus depuis le système de fichiers, les performances en termes de remise de message sont améliorées.

  - Ils donnent accès aux propriétés des messages avec des événements complets pour les développeurs de l’agent.

  - Le développement d’un agent de remise est plus rapide que la mise en œuvre d’un connecteur étranger, car l’agent de remise peut utiliser les fonctionnalités de gestion et de représentation des messages d’Exchange.

  - Vous pouvez vérifier que les messages sont remis au système étranger plutôt que simplement écrits dans le répertoire de dépôt.

  - L’utilisation des connecteurs d’agent de remise permet d’analyser le contrat de niveau de service, car il est possible de suivre la latence de la remise des messages au système étranger.

## Ajout des agents de remise à votre organisation

Pour utiliser un agent de remise au sein de votre organisation, vous devez procéder comme suit :

1.  Obtenez l’agent de remise. En général, les agents de remise sont écrits par des tiers. Exchange 2013 est fourni avec un seul connecteur d’agent de remise par défaut : le connecteur d’agent de remise de messagerie texte.

2.  Installez l’agent de remise dans le service de transport de vos serveurs de boîtes aux lettres qui agissent comme des serveurs sources pour les connecteurs d’agent de remise.

3.  Créez un connecteur d’agent de remise pour le protocole spécifique.

Une fois toutes ces étapes terminées, les messages seront routés vers les systèmes étrangers par l’intermédiaire des connecteurs d’agent de remise et traités par l’agent de remise.

[Espaces de noms Microsoft.Exchange.Data.Transport.Delivery](https://go.microsoft.com/fwlink/?linkid=262690) fournit des informations supplémentaires sur le développement d’un agent de remise.

## Connecteurs d’agent de remise

Un connecteur d’agent de remise dans Exchange 2013 est semblable au connecteur d’agent de remise introduit dans Exchange 2010. Ils acheminent des messages adressés à des systèmes étrangers qui n’utilisent pas le protocole SMTP. Lorsqu’un message est routé vers un connecteur d’agent de remise, l’agent de remise associé effectue la conversion du contenu et la remise du message. En général, les agents de remise sont créés par un tiers et configurés pour fonctionner avec un connecteur d’agent de remise dans votre organisation.

Il n’est pas possible de créer un connecteur d’agent de remise dans le Centre d’administration Exchange. Au lieu de cela, vous créez un connecteur d’agent de remise dans l’environnement de ligne de commande Exchange Management Shell avec la cmdlet [New-DeliveryAgentConnector](https://technet.microsoft.com/fr-fr/library/dd351063\(v=exchg.150\)) et vous modifiez les propriétés du connecteur d’agent de remise avec [Set-DeliveryAgentConnector](https://technet.microsoft.com/fr-fr/library/dd351159\(v=exchg.150\)). Vous pouvez spécifier un ou plusieurs serveurs de boîtes aux lettres hôtes pour le connecteur à l’aide du paramètre optionnel *SourceTransportServers*.

## Connecteur d’agent de remise de messagerie texte par défaut

Vous pouvez utiliser le connecteur d’agent de remise de messagerie texte pour acheminer des messages vers des périphériques mobiles. Sur votre serveur Exchange, exécutez `Get-DeliveryAgentConnector | fl` pour afficher le connecteur et tous ses paramètres. Notez que le paramètre *DeliveryProtocol* est défini sur `MOBILE`.

