---
title: 'Accès à Active Directory: Exchange 2013 Help'
TOCTitle: Accès à Active Directory
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50478212
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Accès à Active Directory

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Microsoft Exchange Server 2013 stocke toutes les informations sur la configuration et les destinataires dans la base de données du service d'annuaire Active Directory. Quand un ordinateur exécutant Exchange 2013 demande des informations sur les destinataires et sur la configuration de l'organisation Exchange, il doit interroger Active Directory pour avoir accès aux informations. Des serveurs Active Directory doivent être disponibles pour qu'Exchange 2013 fonctionne correctement.

Cette rubrique explique comment Exchange 2013 stocke et extrait des informations dans Active Directory, afin que vous puissiez planifier l'accès à Active Directory. Elle aborde également les problèmes dont vous devez avoir connaissance si vous essayez de récupérer des objets Exchange 2013 Active Directory supprimés.

## Informations sur Exchange stockées dans Active Directory

La base de données Active Directory stocke les informations dans trois types de partitions logiques décrites dans les sections suivantes :

  - Partition de schéma

  - Partition de configuration

  - Partition de domaine

## Partition de schéma

La partition de schéma stocke les deux types d'informations suivants :

  - Les **classes de schéma** définissent tous les types d'objets qui peuvent être créés et stockés dans Active Directory.

  - Les **attributs de schéma** définissent toutes les propriétés qui peuvent être utilisées pour décrire les objets stockés dans Active Directory.

Quand vous installez le premier rôle serveur Exchange 2013 dans la forêt ou exécutez le processus de préparation Active Directory, ce processus Active Directory ajoute un grand nombre de classes et attributs au schéma Active Directory. Les classes ajoutées au schéma sont utilisées pour créer des objets Exchange spécifiques, tels que des agents et des connecteurs. Les attributs ajoutés au schéma sont utilisés pour configurer les objets spécifiques à Exchange et les utilisateurs et groupes à extension messagerie. Ces attributs incluent des propriétés telles que des paramètres Microsoft Office Outlook Web Access et des paramètres de messagerie unifiée Microsoft Exchange. Chaque contrôleur de domaine et serveur de catalogue global dans la forêt contient un réplica complet de la partition de schéma.

Pour plus d'informations sur les modifications de schéma dans Exchange 2013, consultez la rubrique [Modifications apportées au schéma Active Directory d’Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Partition de configuration

La partition de configuration stocke des informations sur la configuration de la forêt entière. Ces informations de configuration incluent la configuration de sites Active Directory, des paramètres globaux d'Exchange, des paramètres de transport et des stratégies de boîte aux lettres. Chaque type d'informations de configuration est stocké dans un conteneur dans la partition de configuration. Les informations de configuration d'Exchange sont stockées dans un sous-dossier du conteneur Services de la partition de configuration. Les informations stockées dans ce conteneur sont les suivantes :

  - Listes d'adresses

  - Stratégies de carnet d'adresses

  - Groupes d'administration

  - Paramètres d'accès au client

  - Connexions

  - Paramètres de boîte aux lettres mobile

  - Paramètres globaux

  - Paramètres de surveillance

  - Stratégies système

  - Conteneur de stratégies de rétention

  - Paramètres de transport

Chaque contrôleur de domaine et serveur de catalogue global dans la forêt contient un réplica de la partition de configuration.

## Partition de domaine

La partition de domaine stocke les informations dans les conteneurs par défaut et dans les unités d'organisation créées par l'administrateur Active Directory. Ces conteneurs détiennent des objets spécifiques au domaine. Ces données incluent des objets Exchange du système et des informations sur les ordinateurs, les utilisateurs et les groupes dans ce domaine. Quand Exchange 2013 est installé, Exchange met à jour les objets dans cette partition pour prendre en charge la fonctionnalité Exchange. Cette fonctionnalité affecte la manière dont les informations de destinataire sont stockées et accédées.

Chaque contrôleur de domaine contient une réplication complète de la partition de domaine pour le domaine pour lequel elle fait autorité. Chaque serveur de catalogue global dans la forêt contient un sous-ensemble d'informations dans chaque partition de domaine dans la forêt.

## Comment Exchange 2013 accède-t-il aux informations dans Active Directory ?

Exchange 2013 utilise une API Active Directory pour accéder aux informations stockées dans Active Directory. Le service de topologie Microsoft ExchangeActive Directory s'exécute sur tous les rôles serveur d'Exchange 2013. Ce service lit les informations à partir de toutes les partitions Active Directory. Les données extraites sont mises en cache et utilisées par les serveurs Exchange 2013 pour découvrir l'emplacement du site Active Directory pour tous les services Exchange de l'organisation.

Pour plus d'informations sur la découverte de topologie et de service, consultez la rubrique [Planification de l’utilisation de sites Active Directory pour le routage de messages](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md).

Exchange 2013 est une application sensible au site Active Directory qui préfère communiquer avec les serveurs d'annuaire localisés dans le même site que le serveur Exchange pour optimiser le trafic réseau. Chaque rôle serveur organisationnel Exchange 2013 doit communiquer avec Active Directory pour récupérer les informations sur les destinataires et les informations sur les autres rôles serveur Exchange 2013. Les données que chaque rôle de serveur obtient sont décrites dans les sections suivantes.

Par défaut, lorsqu'un serveur Exchange 2013 démarre, il est lié à un contrôleur de domaine et un serveur de catalogue global sélectionnés de manière aléatoire dans son propre site. Vous pouvez afficher les serveurs de répertoires sélectionnés à l'aide de la cmdlet **Get-ExchangeServer** dans l'environnement de ligne de commande Exchange Management Shell. Vous pouvez également utiliser la cmdlet **Set-ExchangeServer** pour configurer une liste statique de contrôleurs de domaine auxquels un serveur Exchange 2013 doit être lié ou une liste de contrôleurs de domaine à exclure.

> [!IMPORTANT]
> Il est possible de configurer un contrôleur de domaine Windows Server 2008 en tant que serveur d'annuaire en lecture seule. Cette configuration est utile pour le déploiement d'un contrôleur de domaine ou d'un serveur de catalogue global dans un site distant à des fins d'authentification et d'autorisation, sans que les administrateurs de ce site ne soient autorisés à apporter des modifications à Active Directory. Toutefois, vous ne pouvez pas déployer un serveur Exchange 2013 dans un site ne contenant que des serveurs d'annuaire en lecture seule.


## Rôle serveur de boîtes aux lettres

Le rôle du serveur de la boîte aux lettres stocke les informations de configuration sur les utilisateurs de la boîte aux lettres et les stocke dans Active Directory. En outre, pour Exchange 2013, le serveur de boîtes aux lettres contient tous les composants de serveurs traditionnels trouvés dans Exchange 2010 : les protocoles d'accès au client, le service de transport, les bases de données de boîtes aux lettres et la messagerie unifiée. Le serveur de boîtes aux lettres gère toutes les activités des boîtes aux lettres actives sur ce serveur.

## Rôle serveur d'accès au client

Dans Exchange 2013, le serveur d'accès au client fournit l'authentification, la redirection limitée et les services proxy. Le serveur d'accès au Client lui-même ne fait pas de rendu de données. Le serveur d'accès au Client est un serveur léger et sans état. Il n'y a jamais rien en file d'attente ni stockés sur le serveur d'accès au Client. Le serveur d'accès au client offre tous les protocoles d'accès au client habituels : HTTP, POP et IMAP et SMTP.

## Récupération d'objets Exchange supprimés

La Corbeille Active Directory permet de réduire le temps d'arrêt du service d'annuaire en facilitant la conservation et la récupération des objets Active Directory accidentellement supprimés sans restaurer les données Active Directory à partir de sauvegardes, redémarrer AD DS (Active Directory Domain Services) ou redémarrer les contrôleurs de domaine.

Ce qu'il est important de comprendre à propos de la récupération des objets Exchange liés à Active Directory, c'est que les objets Exchange ne sont pas isolés. Par exemple, lorsque vous activez la messagerie d'un utilisateur, plusieurs stratégies et liens sont calculés pour cet utilisateur en fonction de votre configuration Exchange actuelle. Les deux problèmes suivants sont susceptibles de survenir lorsque vous restaurez un objet configuration ou destinataire Exchange supprimé :

  - **Conflits**   Certains attributs Exchange doivent être uniques dans une forêt. Par exemple, les adresses (de messagerie électronique) proxy de deux utilisateurs différents ne doivent pas être identiques. Active Directory n'applique pas de caractère unique aux adresses proxy alors que les outils d'administration d'Exchange vérifient le caractère unique. Les stratégies d'adresse de messagerie Exchange résolvent automatiquement les éventuels conflits d'attribution d'adresses proxy en fonction de règles déterministes. Ainsi, il est possible de restaurer un objet utilisateur Exchange et, par conséquent, de créer un conflit entre les adresses proxy ou autres attributs qui doivent être uniques.

  - **Configurations incorrectes**   Exchange comporte des règles automatiques qui attribuent plusieurs stratégies ou paramètres. Si vous supprimez un destinataire et que vous modifiez ensuite les règles ou stratégies, la restauration d'un objet utilisateur Exchange risque d'entraîner l'affectation de l'utilisateur à une stratégie non appropriée (ou même à une stratégie qui n'existe plus).

Les instructions suivantes vous permettent de minimiser les problèmes lorsque vous récupérez les objets liés à Exchange supprimés :

  - Si vous avez supprimé un objet de configuration Exchange à l'aide des outils de gestion Exchange, ne restaurez pas l'objet. Recréez plutôt l'objet à l'aide des outils de gestion Exchange (par exemple, le Centre d'administration Exchange ou l'environnement de ligne de commande Exchange Management Shell).

  - Si vous avez supprimé un objet de configuration Exchange sans utiliser les outils de gestion Exchange, récupérez-le le plus rapidement possible. Plus il y aura de changements administratifs et de configuration dans le système suite à la suppression, plus la restauration des objets entraînera des problèmes de configuration.

  - Si vous récupérez des destinataires Exchange supprimés (contacts, utilisateurs ou groupes de distribution), contrôlez attentivement les conflits et erreurs relatifs aux objets récupérés. Si les stratégies ou autre configuration Exchange relatives aux destinataires ont été modifiées depuis la suppression, appliquez de nouveau les stratégies actuelles aux destinataires récupérés pour vous assurer qu'ils sont configurés correctement.

## Pour plus d'informations

[Guide étape par étape de la corbeille Active Directory](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Introduction aux améliorations du Centre d'administration Active Directory (niveau 100)](https://go.microsoft.com/fwlink/p/?linkid=267641)

[Gestion AD DS avancée à l'aide du Centre d'administration Active Directory (niveau 200)](https://go.microsoft.com/fwlink/p/?linkid=267642)

