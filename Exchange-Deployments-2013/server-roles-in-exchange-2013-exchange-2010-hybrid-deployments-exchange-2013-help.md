---
title: 'Rôles serveur dans les déploiements hybrides Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Rôles serveur dans les déploiements hybrides Exchange 2013/Exchange 2010
ms:assetid: 7d774948-94f9-4405-af2b-0c67c0405c0f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn393966(v=EXCHG.150)
ms:contentKeyID: 59634356
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rôles serveur dans les déploiements hybrides Exchange 2013/Exchange 2010

Cette rubrique est en cours de rédaction.  

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Dernière rubrique modifiée :</strong>2017-02-16_

Lors de la configuration d’un déploiement hybride dans une organisation Exchange 2010, vous devez installer au moins un serveur Exchange 2013 avec les rôles serveur d’accès au client et serveur de boîtes aux lettres dans votre organisation Exchange 2010 existante. Les serveurs d’accès au client et de boîtes aux lettres Exchange 2013 coordonnent les communications entre votre organisation Exchange 2010 sur site existante et l’organisation Exchange Online. Cette communication englobe le transport des messages et les caractéristiques de messagerie entre l’organisation sur site et l’organisation Exchange Online.

Nous vous recommandons vivement d’installer plusieurs serveurs Exchange 2013 dans votre organisation sur site pour renforcer la fiabilité et la disponibilité des fonctionnalités de déploiement hybride.

## Rôles serveur dans un déploiement hybride

Voici un rapide résumé des rôles serveur Exchange 2013 dans un déploiement hybride :

  - **Rôle serveur d’accès au client**   Le rôle serveur d’accès au client Exchange 2013 fournit toujours de nombreuses fonctionnalités généralement offertes par les serveurs d’accès au client Exchange 2010 dans votre organisation, auxquelles ont été ajoutés des éléments nécessaires pour prendre en charge un déploiement hybride et une coexistence avec Exchange 2010. Le serveur d’accès au client traite également les messages sécurisés envoyés de l’organisation Exchange Online vers l’organisation sur site, ainsi que les règles de transport, les stratégies de journalisation et la remise de messages aux serveurs de boîtes aux lettres dans un déploiement hybride. Un connecteur de réception dédié est configuré sur le serveur d’accès au client pour gérer le transport de courrier hybride sécurisé. L’ensemble des connexions au client, y compris l’accès au client Outlook, Outlook Web App et Outlook Anywhere, passe par le rôle serveur d’accès au client. Les fonctions des relations organisationnelles entre les organisations sur site et Exchange Online, telles que le partage de disponibilité, sont également gérées par le rôle serveur d’accès au client.
    
    Pour plus d’informations, consultez la rubrique [Serveur d’accès au client](https://technet.microsoft.com/fr-fr/library/dd298114\(v=exchg.150\)).

  - **Rôle serveur de boîtes aux lettres**   Le rôle serveur de boîtes aux lettres Exchange 2013 traite les messages sécurisés envoyés à l’organisation Exchange Online à partir de l’organisation sur site. Bien que ce ne soit pas une utilisation classique, il peut aussi héberger les boîtes aux lettres de destinataires sur site et communiquer avec l’organisation Exchange Online par proxy via le serveur d’accès au client sur site. Un connecteur d’envoi dédié est configuré par défaut sur le rôle serveur de boîte aux lettres pour prendre en charge le transport de courrier hybride sécurisé.
    
    Pour plus d’informations, consultez la rubrique [Serveur de boîtes aux lettres](https://technet.microsoft.com/fr-fr/library/jj150491\(v=exchg.150\)).

Selon la configuration de déploiement hybride souhaitée, un serveur Exchange 2013 requiert l'installation de l'un des deux rôles serveur ou des deux :

  - **Serveur Exchange unique**   Si vous décidez d’installer un serveur Exchange unique dans votre organisation locale, vous devrez installer les deux rôles serveur d’accès au client et de boîte aux lettres sur ce serveur.

  - **Plusieurs serveurs Exchange**   Si vous décidez d'installer plusieurs serveurs Exchange dans votre organisation locale, vous pouvez installer les rôles serveur sur des serveurs distincts dans votre organisation locale. Par exemple, vous pouvez installer un serveur Exchange 2013 doté de rôles de boîtes aux lettres et d'accès au client, et installer un autre serveur Exchange possédant uniquement le rôle serveur d'accès au client. Toutefois, la meilleure configuration de serveur recommandée consiste à installer les deux rôles serveur d'accès au client et de boîtes aux lettres sur *chaque* serveur Exchange 2013 déployé dans votre organisation locale.

Pour en savoir plus sur la planification de la capacité d’Exchange, consultez la page [Présentation des configurations de rôle serveur multiples dans la planification des capacités](https://go.microsoft.com/fwlink/?linkid=266576).

## Fonctionnalités Exchange Server dans des déploiements hybrides

Les serveurs Exchange permettent de doter votre organisation sur site de plusieurs fonctions importantes au sein d’un déploiement hybride :

  - **Fédération**   Les serveurs Exchange 2013 et Exchange 2010 vous permettent de créer une approbation de fédération pour votre organisation sur site à l’aide de Microsoft Federation Gateway. Microsoft Federation Gateway est un service informatique gratuit proposé par Microsoft qui agit comme un courtier d’approbation entre votre organisation sur site et l’organisation cliente Office 365. La fonction de fédération est un élément nécessaire à la création d’une relation organisationnelle entre l’organisation sur site et l’organisation Exchange Online.
    
    Pour plus d’informations, consultez la rubrique [Fédération](https://technet.microsoft.com/fr-fr/library/dd335047\(v=exchg.150\)).

  - **Relations d'organisation**   Les serveurs Exchange 2013 dotés du rôle serveur d'accès au client permettent de créer des relations d'organisation entre les organisations locale et Exchange Online. Les relations d'organisation sont nécessaires pour de nombreux autres services dans un déploiement hybride, tels que le partage des informations de disponibilité du calendrier, le suivi des messages et les déplacements de boîtes aux lettres entre l'organisation locale et l'organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

  - **Transport de messages**   Les serveurs Exchange 2013 dotés des rôles serveur d'accès au client et de boîtes aux lettres sont chargés d'assurer le transport des messages dans un déploiement hybride. À l'aide des connecteurs d'envoi et de réception, ils servent de points de terminaison de connexion pour les messages externes entrants et assurent également la remise des messages sortants sur Internet et dans l'organisation Exchange Online.
    
    Pour plus d’informations, consultez la rubrique [Options de transport dans les déploiements hybrides Exchange 2013/Exchange 2010](transport-options-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md).

  - **Sécurité du transport des messages**   Les serveurs Exchange 2013 dotés des rôles serveur d'accès au client et de boîtes aux lettres contribuent à la sécurisation des messages échangés entre l'organisation locale et l'organisation Exchange Online à l'aide de la fonctionnalité Sécurité du domaine d'Exchange 2013. La sécurité peut être renforcée par l'authentification TLS (Transport Layer Security) mutuelle et le chiffrement des messages échangés.
    
    Pour en savoir plus, consultez la rubrique [Présentation de la sécurité de domaine](https://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook Web App**   Les serveurs Exchange 2013 dotés du rôle serveur d'accès au client prennent en charge la configuration d'un point de terminaison URL unique pour les connexions externes aux boîtes aux lettres locales et Exchange Online. Pour les boîtes aux lettres locales, les serveurs d'accès au client sont configurés pour traiter des demandes Outlook Web App. Pour les boîtes aux lettres de l'organisation Exchange Online, les serveurs d'accès au client sont configurés pour afficher automatiquement un lien vers le point de terminaison Outlook Web App dans l'organisation Exchange Online.
    
    Pour plus d'informations, consultez la rubrique [Outlook Web App](https://technet.microsoft.com/fr-fr/library/jj657718\(v=exchg.150\)).

## Topologie du serveur Exchange

Si vous décidez d’ajouter des serveurs Exchange 2013 supplémentaires à votre déploiement hybride, le serveur Exchange est déployé de la même manière que tout autre serveur Exchange dans votre organisation Exchange 2010 existante. La configuration de votre organisation Exchange 2010 sur site existante pour un déploiement hybride ne requiert pas de topologie de serveur Exchange spéciale. Cependant, vous devez installer Exchange 2010 Service Pack 3 (SP3) sur vos serveurs Exchange 2010, ainsi que la mise à jour cumulative 1 (CU1) ou supérieure d’Exchange 2013 pour activer la compatibilité et la totalité des fonctionnalités hybrides avec Office 365.

Le tableau suivant décrit brièvement les changements apportés aux services une fois le déploiement hybride configuré.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Service</th>
<th>Avant le déploiement hybride</th>
<th>Après le déploiement hybride</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transport des messages (entrants et sortants)</p></td>
<td><p>Serveur d’accès au client Exchange 2010</p></td>
<td><p>Serveur d’accès au client Exchange 2013 ou Exchange Online Protection (EOP) intégré à Office 365</p></td>
<td><p>L'enregistrement MX (Mail Exchanger) pour le domaine peut rester inchangé ou être mis à jour pour pointer vers EOP.</p></td>
</tr>
<tr class="even">
<td><p>URL publique Outlook Web App</p></td>
<td><p>Serveur d’accès au client Exchange 2010</p></td>
<td><p>Serveur d’accès au client Exchange 2013</p></td>
<td><p>Les serveurs d’accès au client Exchange 2013 transfèrent les demandes Outlook Web App par proxy pour des boîtes aux lettres sur site vers les serveurs d’accès au client Exchange 2010. Les demandes Outlook Web App pour les boîtes aux lettres hébergées sur Exchange Online contiennent un lien vers l’URL Exchange Online Outlook Web App.</p></td>
</tr>
</tbody>
</table>


## Configuration logicielle pour les serveurs Exchange

Exchange 2013 CU1 ou supérieur active la fonctionnalité de déploiement hybride avec l’Assistant de configuration hybride. Vous pouvez utiliser tout support Exchange 2013 CU1 ou supérieur lors de l’installation de serveurs Exchange 2013 supplémentaires.

Pour en savoir plus sur le téléchargement de la dernière version d’Exchange 2013, voir [Mises à jour pour Exchange 2013](https://technet.microsoft.com/library/jj907309).

> [!IMPORTANT]
> Vous devez obtenir une licence pour votre serveur hybride lorsque vous configurez un déploiement hybride avec Exchange 2013 ou 2010 et Office 365. Pour obtenir une clé de produit Exchange Server gratuite pour utilisation dans la configuration de votre déploiement hybride, utilisez l’<a href="https://aka.ms/hybridkey">outil de clé de produit édition hybride</a>.

