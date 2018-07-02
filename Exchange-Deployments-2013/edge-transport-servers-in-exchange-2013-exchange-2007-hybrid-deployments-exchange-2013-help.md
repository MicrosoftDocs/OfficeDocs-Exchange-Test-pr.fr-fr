---
title: 'Serveurs de transport Edge dans les déploiements hybrides Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Serveurs de transport Edge dans les déploiements hybrides Exchange 2013/Exchange 2007
ms:assetid: 4e4d7c19-78b8-44bb-bdff-3ea97ea59a5d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn151300(v=EXCHG.150)
ms:contentKeyID: 54651599
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serveurs de transport Edge dans les déploiements hybrides Exchange 2013/Exchange 2007

Cette rubrique est en cours de rédaction.  

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Les serveurs de transport Edge dans Microsoft Exchange sont déployés dans le réseau de périmètre local d’une organisation. Ce sont des ordinateurs non liés à un domaine qui gèrent le flux de messagerie côté Internet et font office de relais SMTP et d’hôte actif pour les serveurs Exchange de votre réseau interne.

Les organisations Exchange 2013 qui souhaitent utiliser des serveurs de transport Edge ont la possibilité de déployer des serveurs de transport Edge Exchange Server 2013 ou des serveurs de transport Edge Exchange 2010 exécutant Service Pack 3 (SP3) pour Exchange 2010. Utilisez des serveurs de transport Edge si vous ne voulez pas exposer les serveurs de boîtes aux lettres ou d’accès au client Exchange 2013 internes directement à Internet.

Pour plus d’informations sur le rôle serveur de transport Edge Exchange 2013, consultez la rubrique [Serveurs de transport Edge](https://technet.microsoft.com/fr-fr/library/bb124701\(v=exchg.150\)).

Pour plus d'informations sur le rôle serveur de transport Edge Exchange 2010, consultez la rubrique [Vue d'ensemble du rôle serveur de transport Edge](http://go.microsoft.com/fwlink/p/?linkid=183473).

## Serveurs de transport Edge dans des organisations avec un déploiement hybride basé sur Exchange 2013

Les messages acheminés entre une organisation locale et une organisation Exchange Online dans un déploiement hybride requièrent que le service Microsoft Exchange Online Protection (EOP) se connecte directement de la part d’Exchange Online aux serveurs de transport Edge exécutant Exchange 2013 ou Exchange 2010 SP3.

> [!IMPORTANT]
> Si vous utilisez d’autres serveurs de transport Edge Exchange 2010 dans d’autres emplacements qui ne géreront pas de transport hybride, il n’est pas nécessaire de les mettre à niveau vers Exchange 2010 SP3. Toutefois, si à l’avenir vous souhaitez qu’EOP se connecte à d’autres serveurs de transport Edge pour le transport hybride, ceux-ci doivent être mis à niveau vers Exchange 2010 SP3 ou vers les serveurs de transport Edge Exchange 2013.


## Ajout d'un serveur de transport Edge à un déploiement hybride

Le déploiement d'un serveur de transport Edge dans votre organisation locale quand vous configurez un déploiement hybride est une étape facultative. Lors de la configuration de votre déploiement hybride, l'Assistant Configuration hybride vous permet soit de sélectionner un ou plusieurs serveurs d'accès au client et de boîtes aux lettres pour le transport de courrier hybride, soit de sélectionner un ou plusieurs serveurs de transport Edge locaux pour gérer le transport de courrier hybride avec l'organisation Exchange Online.

Quand vous ajoutez un serveur de transport Edge à votre déploiement hybride, il communique avec EOP de la part des serveurs d'accès au client et de boîtes aux lettres Exchange 2013 internes. Le serveur de transport Edge fait office de relais entre le serveur de boîtes aux lettres local et EOP pour les messages sortants entre l'organisation locale et l'organisation Exchange Online. Le serveur de transport Edge fait également office de relais pour le serveur d'accès au client local pour les messages entrants entre l'organisation Exchange Online et l'organisation locale. L'intégralité de la sécurité de connexion précédemment gérée par le serveur d'accès au client est gérée par le serveur de transport Edge. La recherche du destinataire, les stratégies de conformité et l'inspection d'autres messages sont toujours effectuées sur le serveur d'accès au client.

## Flux de messagerie sans serveur de transport Edge

Le processus et le schéma ci-dessous décrivent l’itinéraire emprunté par les messages entre une organisation locale et Exchange Online quand aucun serveur de transport Edge n’est déployé :

1.  Les messages sortants provenant de l'organisation locale et à destination de l'organisation Exchange Online sont envoyés d'une boîte aux lettres d'un serveur de boîtes aux lettres Exchange 2007 vers un serveur de transport Hub Exchange 2007.

2.  Le serveur de transport Hub Exchange 2007 envoie le message au serveur de boîtes aux lettres Exchange 2013.

3.  Le serveur de boîtes aux lettres Exchange 2013 envoie le message directement à l'organisation EOP Exchange Online.

4.  EOP remet le message à l'organisation Exchange Online. Dans cet exemple, les rôles serveur d'accès au client et de boîte aux lettres sont installés sur le même serveur Exchange 2013.

Les messages envoyés de l'organisation Exchange Online aux destinataires de l'organisation locale suivent le chemin inverse.

**Flux de messagerie dans un déploiement hybride sans serveur de transport Edge déployé**

![Organisation sur site sans le serveur Edge](images/Dn151300.e7206c51-b61c-41e3-a446-9270f131fbaa(EXCHG.150).png "Organisation sur site sans le serveur Edge")

## Flux de messagerie avec serveur de transport Edge

Le processus suivant décrit l'itinéraire emprunté par les messages entre une organisation locale et Exchange Online quand un serveur de transport Edge est déployé. Les messages de l'organisation locale vers des destinataires de l'organisation Exchange Online sont envoyés du serveur de boîtes aux lettres Exchange 2007 :

1.  Les messages sortants provenant de l'organisation locale et à destination de l'organisation Exchange Online sont envoyés d'une boîte aux lettres d'un serveur de boîtes aux lettres Exchange 2007 vers un serveur de transport Hub Exchange 2007.

2.  Le serveur de transport Hub Exchange 2007 envoie le message au serveur de boîtes aux lettres Exchange 2013.

3.  Le serveur de boîtes aux lettres Exchange 2013 envoie le message à un serveur de transport Edge Exchange 2013 ou Exchange 2010 SP3.

4.  Le serveur de transport Edge envoie le message à l’organisation EOP Exchange Online.

5.  EOP remet le message à l'organisation Exchange Online. Dans cet exemple, les rôles serveur d'accès au client et de boîte aux lettres sont installés sur le même serveur Exchange 2013.

Les messages envoyés de l'organisation Exchange Online aux destinataires de l'organisation locale suivent le chemin inverse.

**Flux de messagerie dans un déploiement hybride avec un serveur de transport Edge Exchange 2013 ou 2010 SP3 déployé**

![Organisation sur site avec le serveur Edge](images/Dn151300.91bf5390-c4d7-4aa9-b911-0c1c559d4365(EXCHG.150).png "Organisation sur site avec le serveur Edge")

