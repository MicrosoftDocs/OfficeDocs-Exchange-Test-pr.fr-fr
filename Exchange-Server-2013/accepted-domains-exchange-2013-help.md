---
title: 'Domaines acceptés: Exchange 2013 Help'
TOCTitle: Domaines acceptés
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50479135
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domaines acceptés

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-06-16_

Un domaine accepté est un espace de noms SMTP quel qu’il soit pour lequel une organisation Microsoft Exchange Server 2013 envoie ou reçoit du courrier électronique. Les domaines acceptés incluent les domaines pour lesquels l’organisation Exchange fait autorité. Une organisation Exchange fait autorité lorsqu’elle gère la remise des messages pour les destinataires dans le domaine accepté. Les domaines acceptés incluent également les domaines pour lesquels l’organisation Exchange reçoit des messages et les relaie vers un serveur de messagerie situé en dehors de l’organisation pour la remise au destinataire.

**Contenu de cette rubrique**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## Configuration des domaines acceptés

Les domaines acceptés sont configurés en tant que paramètres globaux pour l’organisation Exchange. Vous devez configurer en tant que domaine accepté de votre organisation chacun des domaines pour lesquels votre organisation Exchange relaie ou remet des messages.

Il existe trois types de domaines acceptés : domaines faisant autorité, relais internes et relais externes. Ces types de domaines acceptés sont décrits dans les sections suivantes.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous disposez d’un serveur de transport Edge abonné dans votre réseau de périmètre, vous configurez les domaines acceptés sur un serveur de boîtes aux lettres dans votre organisation Exchange. La configuration des domaines acceptés est répliquée sur le serveur de transport Edge lors de la synchronisation EdgeSync. Pour plus d’informations, consultez la rubrique <a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a>.</td>
</tr>
</tbody>
</table>


## Domaines faisant autorité

Une organisation peut avoir plusieurs domaines SMTP. Les domaines de messagerie d’une organisation sont les domaines faisant autorité. Dans Exchange 2013, un domaine accepté est considéré comme faisant autorité lorsque l’organisation Exchange héberge des boîtes aux lettres pour des destinataires dans ce domaine SMTP.

Par défaut, lorsque le premier serveur de boîtes aux lettres Exchange 2013 est installé, un domaine accepté est configuré comme faisant autorité pour l’organisation Exchange. Le domaine accepté par défaut est le nom de domaine complet de votre domaine racine de la forêt. Souvent, le nom de domaine interne diffère du nom de domaine externe. Par exemple, votre nom de domaine interne peut être contoso.local, alors que votre nom de domaine externe est contoso.com. L’enregistrement du serveur de messagerie (MX) DNS (Domain Name System) de votre organisation fait référence à contoso.com. Contoso.com est l’espace de noms SMTP que vous affectez aux utilisateurs lorsque vous créez une stratégie d’adresse de messagerie. Vous devez créer un domaine accepté qui correspond à votre nom de domaine externe.

Pour plus d’informations, voir :

  - [Configurer un domaine accepté dans votre organisation Exchange comme autorité](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [Configuration d’Exchange de manière à accepter des messages électroniques pour plusieurs domaines faisant autorité](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## Domaines de relais

En général, la plupart des serveurs de messagerie Internet sont configurés pour ne pas autoriser le relais des autres domaines par leur biais. Cependant, il existe des scénarios dans lesquels vous voudrez peut-être laisser des partenaires ou des filiales relayer des messages électroniques via vos serveurs Exchange. Dans Exchange 2013, vous pouvez configurer les domaines acceptés comme des domaines de relais. Votre organisation reçoit les messages électroniques, puis les relaie vers un autre serveur de messagerie.

Vous pouvez configurer un domaine de relais comme un domaine de relais interne ou un domaine de relais externe. Ces deux types de domaine de relais sont décrits dans les sections suivantes.

## Domaine de relais interne

Lorsque vous configurez un domaine de relais interne, tout ou partie des destinataires de ce domaine n’ont pas de boîtes aux lettres dans cette organisation Exchange. Les messages en provenance d’Internet sont relayés pour ce domaine via les serveurs de transport de cette organisation Exchange. Cette configuration est utilisée dans les scénarios décrits dans cette section.

Une organisation peut avoir besoin de partager un même espace d’adressage SMTP entre plusieurs systèmes de messagerie différents. Par exemple, vous pouvez avoir besoin de partager l’espace d’adressage SMTP entre Exchange et un système de messagerie tiers ou entre des environnements Exchange configurés dans différentes forêts Active Directory. Dans ces scénarios, les utilisateurs de chaque système de messagerie ont un suffixe de domaine identique dans leurs adresses de messagerie.

Pour prendre en charge ces scénarios, vous devez créer un domaine accepté configuré comme domaine de relais interne. Vous devez également ajouter un connecteur d’envoi issu d’un serveur de boîtes aux lettres et configuré pour envoyer des messages électroniques à l’espace d’adressage partagé. Si un domaine accepté est configuré comme domaine faisant autorité et aucun destinataire n’est trouvé dans le service d’annuaire Active Directory, une notification d’échec de remise est renvoyée à l’expéditeur. Le domaine accepté configuré comme domaine de relais interne tente d’abord de remettre le message à un destinataire dans l’organisation Exchange. Si le destinataire est introuvable, le message est routé vers le connecteur d’envoi avec l’espace d’adressage correspondant le plus proche.

Si une organisation contient plusieurs forêts et a configuré une synchronisation de liste d'adresses globale (GAL), le domaine SMTP de l’une des forêts peut être configuré comme domaine de relais interne dans la deuxième forêt. Les messages en provenance d’Internet adressés à des destinataires dans des domaines de relais interne sont relayés aux serveurs de boîtes aux lettres dans la même organisation. Les serveurs de boîtes aux lettres de réception routent ensuite les messages vers les serveurs de boîtes aux lettres de la forêt destinataire. Vous configurez le domaine SMTP comme domaine de relais interne pour vous assurer que le courrier électronique qui est adressé à ce domaine est accepté par l’organisation Exchange. La configuration de connecteur de votre organisation détermine la manière dont les messages sont routés.

Pour en savoir plus, consultez la rubrique [Configurer un domaine accepté pour une unité commerciale avec des boîtes aux lettres à l’extérieur de votre organisation Exchange](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md).

## Domaine de relais externe

Lorsque vous configurez un domaine de relais externe, les messages sont relayés vers un serveur de messagerie qui se trouve à l’extérieur de votre organisation Exchange et à l’extérieur du périmètre du réseau de l’organisation.

Pour plus d’informations, consultez la rubrique [Configurer un domaine accepté pour une division indépendante](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md).

## Domaines acceptés et stratégies d’adresses de messagerie

Vous devez configurer un domaine accepté pour pouvoir utiliser un espace d’adressage SMTP dans une stratégie d’adresse de messagerie. Lorsque vous créez un domaine accepté, vous pouvez utiliser un caractère générique (\*) dans l’espace d’adressage pour indiquer que tous les sous-domaines de l’espace d’adressage SMTP sont également acceptés par l’organisationExchange. Par exemple, pour configurer contoso.com et tous ses sous-domaines comme domaines acceptés, entrez l’espace d’adressage SMTP **\*.contoso.com**. Les entrées de domaine accepté sont automatiquement disponibles pour utilisation dans une stratégie d’adresse de messagerie.

Si vous supprimez un domaine accepté qui est utilisé dans une stratégie d’adresse de messagerie, la stratégie n’est plus valide et les destinataires ayant des adresses de messagerie dans ce domaine SMTP ne peuvent plus envoyer ni recevoir de messages électroniques.

