---
title: 'Filtrer les destinataires sur les serveurs de transp. Edge: Exchange 2013 Help'
TOCTitle: Filtrage des destinataires sur les serveurs de transport Edge
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 50478777
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrage des destinataires sur les serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-05-07_

Le filtrage des destinataires est une fonctionnalité anti-courrier indésirable de Microsoft Exchange Server 2013 qui s'appuie sur l'en-tête RCPT TO SMTP pour déterminer quelle action entreprendre sur un message entrant, si nécessaire. Le filtrage des destinataires est effectué par l'agent de filtrage des destinataires.

L’agent de filtrage des destinataires bloque les messages en fonction des caractéristiques du destinataire concerné au sein de l’organisation. L’agent de filtrage des destinataires peut vous aider à empêcher l’acceptation des messages dans les scénarios suivants :

  - **Destinataires inexistants**   Vous pouvez empêcher la remise à des destinataires qui ne figurent pas dans le carnet d’adresses de l’organisation. Par exemple, vous pouvez arrêter la remise à des noms de comptes souvent mal utilisés, tels que administrateur@contoso.com ou support@contoso.com.

  - **Listes de distribution restreintes**   Vous pouvez empêcher la remise de messages provenant d’Internet à des listes de distribution réservées aux utilisateurs internes.

  - **Boîtes aux lettres qui ne doivent jamais recevoir de messages en provenance d’Internet**   Vous pouvez empêcher la remise de messages provenant d’Internet à une boîte aux lettres spécifique ou un alias généralement utilisé au sein de l’organisation, tel que « Helpdesk ».

L’agent de filtrage des destinataires agit sur les destinataires figurant dans l’une des sources de données suivantes :

  - **Liste rouge de destinataires**   Liste définie par un administrateur qui répertorie les destinataires qui ne doivent jamais recevoir de messages d'Internet.

  - **Recherche de destinataire**   Interroge Active Directory pour vérifier si le destinataire existe dans l'organisation. Sur un serveur de transport Edge, la recherche de destinataire requiert l'accès aux informations Active Directory fournies par EdgeSync à l'instance locale des services AD LDS (Active Directory Lightweight Directory Services).

Lorsque vous activez l’agent de filtrage des destinataires, l’une des actions suivantes est appliquée aux messages entrants en fonction des caractéristiques des destinataires. Ces destinataires sont indiqués par l’en-tête RCPT TO.

  - Si le message entrant contient un destinataire qui figure sur la liste rouge de destinataires, le serveur Exchange envoie une erreur de session SMTP `550 5.1.1 User unknown` au serveur d'envoi.

  - Si le message entrant contient un destinataire qui ne correspond à aucun destinataire de la recherche de destinataire, le serveur Exchange envoie une erreur de session SMTP `550 5.1.1 User unknown` au serveur d'envoi.

  - Si le destinataire ne figure pas sur la liste rouge de destinataires, mais bien dans la recherche de destinataire, le serveur Exchange envoie une réponse SMTP `250 2.1.5 Recipient OK` au serveur d'envoi et l’agent de blocage du courrier indésirable suivant dans la chaîne traite le message.

**Contenu de cette rubrique**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## Configuration de la recherche de destinataire

L’une des manières les plus efficaces de réduire le courrier indésirable consiste à valider des destinataires avant d’accepter les messages entrants en provenance d’Internet. Vous activez le blocage des messages envoyés aux destinataires qui n'existent pas dans l'organisation Exchange et le blocage de destinataires spécifiques à l'aide de la cmdlet **Set-RecipientFilterConfig** dans l'environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, voir [Gérer le filtrage des destinataires sur les serveurs de transport Edge](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Si un serveur de transport Edge est installé dans votre réseau de périmètre, vous pouvez configurer l'instance des services AD LDS qui s'exécute sur ce serveur pour qu'elle se synchronise avec Active Directory. Par défaut, AD LDS est installé et configuré sur le serveur de transport Edge. Toutefois, vous devez configurer les services AD LDS pour qu'ils communiquent avec un serveur de catalogue global joint au domaine Active Directory en abonnant le serveur de transport Edge à votre organisation. Pour plus d’informations, voir [Utilisation d’un serveur de transport Edge Exchange 2010 ou 2007 dans Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md).

Retour au début

## Fonctionnalité de répulsion

La fonctionnalité de recherche de destinataire permet au serveur d'envoi de déterminer la validité d’une adresse électronique. Comme mentionné précédemment, lorsque le destinataire d’un message entrant est un destinataire connu, le serveur Exchange renvoie une réponse SMTP `250 2.1.5 Recipient OK` au serveur d'envoi. Cette fonctionnalité fournit un environnement idéal pour une attaque visant à recueillir des informations d’annuaire.

Une *attaque visant à recueillir des informations d’annuaire* est une tentative de collecte d'adresses électroniques valides d’une organisation particulière dans le but de pouvoir les ajouter à une base de données de courrier indésirable. Dans la mesure où les revenus du courrier indésirable sont générés par l’ouverture de messages électroniques par les destinataires, des adresses connues pour être actives sont des informations pour lesquelles des individus mal intentionnés, ou *expéditeurs de courrier indésirable*, sont prêts à payer. Comme le protocole SMTP fournit un feed-back sur les expéditeurs connus et les expéditeurs inconnus, un expéditeur de courrier indésirable peut écrire un programme automatisé qui utilise des noms communs ou des termes d’un dictionnaire pour générer des adresses de messagerie pour un domaine spécifique. Le programme collecte toutes les adresses de messagerie qui retournent une réponse SMTP `250 2.1.5 Recipient OK` et efface toutes celles qui retournent une erreur de session SMTP `550 5.1.1 User unknown`. L’expéditeur de courrier indésirable peut ensuite vendre les adresses valides ou les utiliser comme destinataires de messages non sollicités.

Pour lutter contre les attaques visant à recueillir des informations d’annuaire, Exchange 2013 inclut une fonctionnalité de répulsion. La *répulsion* est la pratique consistant à retarder artificiellement les réponses du serveur pour des profils de communication SMTP spécifiques qui indiquent des volumes importants de courrier indésirable ou d’autres messages malvenus. Le but de la répulsion est de ralentir le processus de communication pour un tel trafic de messages de façon à ce que le coût d’expédition du courrier indésirable augmente pour la personne ou l’organisation émettrice. La répulsion rend une automatisation efficace des attaques visant à recueillir des informations d’annuaire trop coûteuse.

Si la répulsion n'est pas configurée, le serveur Exchange retourne immédiatement une erreur de session SMTP `550 5.1.1 User unknown` à l'émetteur lorsqu'un destinataire ne figure pas dans la recherche de destinataire. En revanche, si la répulsion est configurée, le protocole SMTP attend un nombre précis de secondes avant de renvoyer l’erreur `550 5.1.1 User unknown`. Cette pause dans la session SMTP rend l’automatisation d’une attaque visant à recueillir des informations d’annuaire plus compliquée et moins rentable pour l’expéditeur de courrier indésirable. Par défaut, la répulsion est configurée pour 5 secondes sur les connecteurs de réception.

Pour configurer le délai d'attente avant que le protocole SMTP ne retourne l'erreur `550 5.1.1 User unknown`, vous définissez l'intervalle de répulsion à l'aide du paramètre *TarpitInterval* sur la cmdlet **Set-ReceiveConnector**. La syntaxe est la suivante :

```powershell
Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>
```

La valeur par défaut est `00:00:05`, soit 5 secondes. Le nom du connecteur de réception par défaut sur un serveur de transport Edge est `Default internal receive connector <server name>`.

Modifiez cet intervalle de répulsion avec prudence. Un intervalle trop long pourrait interrompre le flux de messages normal, tandis qu’un intervalle trop court peut être insuffisant pour contrarier une attaque visant à recueillir des informations d’annuaire. Si vous modifiez l’intervalle de répulsion, faites-le par petits incréments et vérifiez les résultats. Par exemple, si la valeur de 5 secondes n’est pas efficace, essayez de passer à un intervalle de 10 secondes.

Retour au début

## Espaces de noms multiples

L'agent de filtrage des destinataires effectue des recherches de destinataires uniquement pour les domaines faisant autorité. Si votre organisation accepte et transfère des messages pour un autre domaine configuré en tant que domaine de relais interne ou externe, l'agent de filtrage des destinataires n'effectue pas de recherche de destinataire sur les destinataires de ces domaines. Toutefois, si le destinataire figure sur la liste rouge de destinataires, il sera bloqué par l'agent de filtrage des destinataires.

Notez que vous pouvez également configurer des domaines acceptés localement sur un serveur de transport Edge. Si le domaine est configuré en tant que domaine de relais interne ou externe, l'agent de filtrage des destinataires sur le serveur de transport Edge n'effectue pas non plus de recherche de destinataire sur les destinataires de ces domaines.

Retour au début

