---
title: 'Options de transport dans les déploiements hybrides Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Options de transport dans les déploiements hybrides Exchange 2013/Exchange 2007
ms:assetid: 92d9e3ca-8d79-4872-9ff7-0067fcdbd434
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn151301(v=EXCHG.150)
ms:contentKeyID: 54651606
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Options de transport dans les déploiements hybrides Exchange 2013/Exchange 2007

Cette rubrique est en cours de rédaction.  

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Les déploiements hybrides peuvent comporter des boîtes aux lettres qui résident dans votre organisation Exchange locale, mais également dans une organisation Exchange Online. Un composant essentiel conférant à ces deux organisations distinctes l’apparence d’une seule et même organisation pour les utilisateurs et les messages qu’ils s’échangent est le transport hybride. Dans un transport hybride, les messages envoyés entre des destinataires d’une organisation sont authentifiés, chiffrés et transférés via le protocole TLS (Transport Layer Security) et apparaissent comme « internes » à des composants d’Exchange, tels que les règles de transport, la journalisation et les stratégies anti-courrier indésirable. Le transport hybride est automatiquement configuré par l’assistant Configuration hybride dans Exchange 2013.

Pour que la configuration du transport hybride fonctionne avec l’Assistant Configuration hybride, le point de terminaison SMTP local qui accepte les connexions depuis Microsoft Exchange Online Protection (EOP) et qui gère le transport pour l’organisation Exchange Online doit être un serveur d’accès au client Exchange 2013, un serveur de transport Edge Exchange 2013 ou un serveur de transport Edge Exchange Server 2010 Service Pack 3 (SP3).

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il ne peut y avoir aucun autre hôte SMTP ou service entre, les serveurs d’accès au client Exchange 2013 ou les serveurs de transport Edge Exchange 2013/Exchange 2010 SP3 et EOP. Les informations ajoutées aux messages et qui activent les fonctions de transport hybride sont supprimées lorsqu'elles passent par un serveur non Exchange 2013, des serveurs de versions antérieures à Exchange 2010 SP3 ou un hôte SMTP. Si des serveurs de transport Edge Exchange 2010 SP2 sont déployés dans votre organisation et que vous souhaitez les utiliser pour le transport hybride, vous devez les mettre à niveau vers Exchange 2010 SP3.</td>
</tr>
</tbody>
</table>


Les messages entrants envoyés aux destinataires des deux organisations par des expéditeurs Internet externes suivent un itinéraire entrant commun. Les messages sortants envoyés depuis les organisations à des destinataires Internet externes peuvent suivre un itinéraire sortant commun ou emprunter des itinéraires indépendants.

Vous devrez choisir le mode d’acheminement du courrier entrant et sortant lors de la planification et de la configuration de votre déploiement hybride. L’itinéraire emprunté par les messages entrants et sortants envoyés à et par des destinataires de l’organisation locale et de l’organisation Exchange Online varie en fonction des facteurs suivants :

  - Souhaitez-vous acheminer les messages Internet entrants des boîtes aux lettres locales et Exchange Online via Microsoft Office 365 et EOP ou via votre organisation locale ?
    
    Vous pouvez décider d’acheminer le courrier Internet entrant pour les deux organisations via votre organisation locale ou via EOP et l’organisation Exchange Online. L’itinéraire emprunté par les messages entrants des deux organisations dépend du fait que vous activiez ou non le transport de courrier centralisé dans votre déploiement hybride.

  - Souhaitez-vous acheminer le courrier sortant à des destinataires externes provenant de votre organisation Exchange Online par le biais de votre organisation locale (transport de courrier centralisé), ou l’acheminer directement vers Internet ?
    
    Grâce au transport de courrier centralisé, vous pouvez acheminer l’ensemble du courrier des boîtes aux lettres de l’organisation Exchange Online via l’organisation locale avant qu’il ne soit remis sur Internet. Cette approche est utile dans les scénarios de mise ne conformité, dans lesquels l’ensemble du courrier en provenance et à destination d’Internet doit être traité par des serveurs locaux. Vous pouvez également configurer Exchange Online pour remettre les messages destinés à des destinataires externes directement sur Internet.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le transport de courrier centralisé est recommandé uniquement pour les organisations qui présentent des besoins de transport spécifiques liés à la conformité. Nous recommandons aux organisations Exchange types de ne pas activer le transport de courrier centralisé.</td>
    </tr>
    </tbody>
    </table>


  - Souhaitez-vous déployer un serveur de transport Edge dans votre organisation locale ?
    
    Si vous ne souhaitez pas exposer vos serveurs Exchange 2013 internes liés à un domaine directement sur Internet, vous pouvez déployer des serveurs de transport Edge Exchange 2013 ou Exchange 2010 SP3 dans votre réseau de périmètre. Pour plus d'informations sur l'ajout d'un serveur de transport Edge à votre déploiement hybride, consultez la rubrique [Serveurs de transport Edge dans les déploiements hybrides Exchange 2013/Exchange 2007](edge-transport-servers-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

Indépendamment du mode d'acheminement des messages vers et depuis Internet, tous les messages envoyés entre l'organisation locale et l'organisation Exchange Online utilisent le transport sécurisé. Pour plus d'informations, consultez la section [Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md) plus loin dans cette rubrique.

Pour plus d'informations sur la façon dont ces options affectent le routage des messages dans votre organisation, consultez la rubrique [Routage de transport dans les déploiements hybrides Exchange 2013/Exchange 2007](transport-routing-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

## Exchange Online Protection dans les déploiements hybrides

EOP est un service en ligne fourni par Microsoft et employé par de nombreuses entreprises pour protéger leurs organisations locales des virus, du courrier indésirable, des tentatives de hameçonnage et des violations de stratégie. Dans Office 365, EOP est utilisé pour protéger les organisations Exchange Online des mêmes menaces. Lorsque vous vous inscrivez à Office 365, une société EOP liée à votre organisation Exchange Online est automatiquement créée.

Une société EOP contient plusieurs paramètres de transport de messagerie pouvant être configurés pour votre organisation Exchange Online. Vous pouvez indiquer quels domaines SMTP doivent provenir d'adresses IP spécifiques, requièrent un certificat SSL (Secure Sockets Layer), peuvent contourner les stratégies de mise en conformité du courrier indésirable, et bien plus. EOP est la porte d'entrée de votre organisation Exchange Online. Tous les messages, quelle que soit leur origine, doivent passer par EOP avant d'atteindre les boîtes aux lettres de votre organisation Exchange Online. De plus, tous les messages envoyés depuis votre organisation Exchange Online doivent transiter par EOP avant d'atteindre Internet.

Lorsque vous configurez un déploiement hybride à l'aide de l'Assistant Configuration hybride, tous les paramètres de transport sont automatiquement configurés dans votre organisation locale et dans la société EOP intégrée à votre organisation Exchange Online. L'Assistant Configuration hybride configure tous les connecteurs entrants et sortants et d'autres paramètres de cette société EOP pour sécuriser les messages envoyés entre l'organisation locale et l'organisation Exchange Online et acheminer les messages vers la bonne destination. Si vous souhaitez configurer des paramètres de transport personnalisés pour votre organisation Exchange Online, vous devez également les configurer dans cette société EOP.

## Communication sécurisée

Afin d’optimiser la protection des destinataires de l’organisation locale et de l’organisation Exchange Online et faire en sorte que les messages envoyés entre ces organisations ne soient pas interceptés et lus, le transport entre l’organisation locale et EOP est configuré pour utiliser TLS forcé. Le transport TLS utilise les certificats SSL (Secure Sockets Layer) fournis par une autorité de certification tierce approuvée (CA). Les messages entre EOP et l’organisation Exchange Online utilisent également TLS.

Lorsque le transport TLS forcé est utilisé, les serveurs d’envoi et de réception examinent le certificat configuré sur l’autre serveur. Le nom de l’objet, ou l’un des autres noms d’objets (SAN), configurés sur les certificats doit correspondre au nom de domaine complet qu’un administrateur a explicitement spécifié sur l’autre serveur. Par exemple, si EOP est configuré pour accepter et sécuriser les messages envoyés depuis le nom de domaine complet mail.contoso.com, le nom de l’objet ou l’autre nom d’objet du serveur de transport Edge ou d’accès au client local entrant doit avoir un certificat SSL avec mail.contoso.com. Si cette condition n’est pas remplie, la connexion est refusée par EOP.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il n’est pas nécessaire que le nom de domaine complet utilisé corresponde au nom de domaine de messagerie des destinataires. La seule condition est que le nom de domaine complet du nom d’objet du certificat ou de l’autre nom de l’objet corresponde au nom de domaine complet que les serveurs de réception ou d’envoi doivent accepter.</td>
</tr>
</tbody>
</table>


Outre l’utilisation de TLS, les messages échangés entre les organisations sont traités comme des messages « internes ». Cette approche permet aux messages de contourner les paramètres anti-courrier indésirable et d’autres services.

Pour plus d’informations sur les certificats SSL et la sécurité de domaine, consultez les rubriques [Conditions requises pour les certificats dans le cadre de déploiements hybrides](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) et [Présentation des certificats TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

