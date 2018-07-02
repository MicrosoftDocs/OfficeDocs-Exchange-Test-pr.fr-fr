---
title: 'Serveurs de transport Edge avec déploiements hybrides: Exchange 2013 Help'
TOCTitle: Serveurs de transport Edge avec déploiements hybrides
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50479661
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Serveurs de transport Edge avec déploiements hybrides

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2018-04-16_

Généralement, le rôle serveur de transport Edge est un rôle facultatif déployé sur un ordinateur dans un réseau de l’organisation Exchange. Il est conçu pour minimiser la surface d’attaque de l’organisation. Le rôle serveur de transport Edge gère tout le flux de messagerie côté Internet, qui offre des services de relais SMTP et d’hôte actif pour les serveurs Exchange locaux internes de votre organisation.

## Serveurs de transport Edge dans des organisations avec un déploiement hybride basé sur Exchange

Les organisations Exchange 2016 souhaitant utiliser les serveurs de transport Edge ont la possibilité de déployer des serveurs de transport Edge exécutant la dernière version des produits Exchange 2016 et des versions plus récentes, Exchange 2013 ou Exchange 2010. Utilisez les serveurs de transport Edge si vous ne souhaitez pas exposer les serveurs Exchange internes directement sur Internet. Lorsque vous déployez un serveur de transport Edge dans un déploiement hybride, Exchange Online, via le service Exchange Online Protection, se connecte à votre serveur de transport Edge pour remettre les messages. Le serveur de transport Edge doit ensuite remettre les messages au serveur de boîtes aux lettres Exchange local dans lequel se trouve la boîte aux lettres du destinataire.

> [!IMPORTANT]
> Ne placez aucun serveur, service ou périphérique entre vos serveurs Exchange locaux et Office 365 traitant ou modifiant le trafic SMTP. Le flux de messagerie sécurisée entre votre organisation Exchange locale et Office 365 dépend des informations contenues dans les messages envoyés au sein de l’organisation. Les pare-feu autorisant le trafic SMTP sur le port TCP 25 sans modification sont pris en charge. Si un serveur, un service ou un périphérique traite un message envoyé entre votre organisation Exchange locale et Office 365, ces informations sont supprimées. Dans ce cas, le message n’est plus considéré comme interne à votre organisation et est soumis à un filtrage anti-courrier indésirable, aux règles de journal et de transport, ainsi qu’à d’autres stratégies ne s’appliquant normalement pas à celui-ci.


> [!IMPORTANT]
> Si vous utilisez d’autres serveurs de transport Edge Exchange dans d’autres emplacements qui ne géreront pas de transport hybride, il n’est pas nécessaire de les mettre à niveau afin de prendre en charge un déploiement hybride. Toutefois, si à l’avenir vous souhaitez qu’EOP se connecte à d’autres serveurs de transport Edge pour le transport hybride, ceux-ci doivent exécuter la dernière version du produit Exchange 2016 et des versions plus récentes, Exchange 2010 ou Exchange 2013.


## Ajout d'un serveur de transport Edge à un déploiement hybride

Le déploiement d’un serveur de transport Edge dans votre organisation locale quand vous configurez un déploiement hybride est une étape facultative. Lors de la configuration de votre déploiement hybride, l’Assistant Configuration hybride vous permet soit de sélectionner un ou plusieurs serveurs Exchange locaux internes, soit de sélectionner un ou plusieurs serveurs de transport Edge locaux pour gérer le transport de courrier hybride avec l’organisation Exchange Online.

Lorsque vous ajoutez un serveur de transport Edge à votre déploiement hybride, il communique avec EOP de la part des serveurs Exchange internes. Le serveur de transport Edge fait office de relais entre les serveurs Exchange internes et EOP pour les messages sortants entre l’organisation locale et l’organisation Exchange Online. Le serveur de transport Edge fait également office de relais entre les serveurs Exchange internes pour les messages entrants provenant de l’organisation Exchange Online et à destination de l’organisation locale. L’intégration de la sécurité de la connexion précédemment gérée par les serveurs Exchange internes est gérée par le serveur de transport Edge. La recherche du destinataire, les stratégies de conformité et l’inspection d’autres messages continuent d’être effectuées sur les serveurs Exchange internes.

Si vous ajoutez un serveur de transport Edge à votre déploiement hybride, il n’est pas nécessaire d’acheminer le courrier électronique envoyé entre les utilisateurs locaux et les destinataires Internet via ce dernier. Seuls les messages envoyés entre l’organisation locale et l’organisation Exchange Online seront acheminés via le serveur de transport Edge.

## Flux de messagerie sans serveur de transport Edge

Le processus et le schéma qui suivent décrivent l’itinéraire emprunté par les messages entre une organisation locale et Exchange Online lorsqu’aucun serveur de transport Edge n’est déployé :

1.  Les messages sortants provenant de l’organisation locale et à destination de l’organisation Exchange Online sont envoyés à partir d’une boîte aux lettres sur un serveur Exchange interne.

2.  Les serveurs Exchange envoient le message directement à EOP.

3.  EOP remet le message à l’organisation Exchange Online.

Les messages envoyés de l'organisation Exchange Online aux destinataires de l'organisation locale suivent le chemin inverse.

**Flux de messagerie dans un déploiement hybride sans serveur de transport Edge déployé**

![Flux de messagerie hybride sans serveur de transport Edge](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "Flux de messagerie hybride sans serveur de transport Edge")

## Flux de messagerie avec serveur de transport Edge

Le processus suivant décrit l’itinéraire emprunté par les messages entre une organisation locale et Exchange Online quand un serveur de transport Edge est déployé. Les messages de l’organisation locale vers des destinataires de l’organisation Exchange Online sont envoyés à partir du serveur Exchange interne :

1.  Les messages provenant de l’organisation locale et à destination de l’organisation Exchange Online sont envoyés à partir d’une boîte aux lettres sur un serveur Exchange interne.

2.  Le serveur Exchange envoie le message à un serveur de transport Edge exécutant une version prise en charge du produit Exchange.

3.  Le serveur de transport Edge envoie le message à EOP.

4.  EOP remet le message à l’organisation Exchange Online.

Les messages envoyés de l'organisation Exchange Online aux destinataires de l'organisation locale suivent le chemin inverse.

**Flux de messagerie dans un déploiement hybride avec serveur de transport Edge déployé**

![Flux de messagerie hybride avec serveur de transport Edge](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "Flux de messagerie hybride avec serveur de transport Edge")

