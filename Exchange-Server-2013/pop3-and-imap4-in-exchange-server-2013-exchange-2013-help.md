---
title: 'POP3 et IMAP4 dans Exchange Server 2013: Exchange 2013 Help'
TOCTitle: POP3 et IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50478837
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 et IMAP4 dans Exchange Server 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-08-16_

Découvrez les différences entre les protocoles POP3 et IMAP4 dans Exchange Server 2013 et comment configurer des options afin d’accéder aux boîtes aux lettres Exchange 2013 de divers programmes de messagerie électronique.

Par défaut, les protocoles POP3 et IMAP4 sont désactivés dans Exchange Server 2013. Pour prendre en charge les clients POP3 qui utilisent encore ces protocoles, vous devez lancer deux services POP3 : le service Microsoft Exchange POP3 et le service du serveur principal Microsoft Exchange POP3. Pour prendre en charge les clients IMAP4 qui utilisent encore ces protocoles, vous devez lancer deux services IMAP4 : le service Microsoft Exchange IMAP4 et le service du serveur principal Microsoft Exchange IMAP4.

Pour obtenir la procédure détaillée d'activation des services POP3 et IMAP4, consultez les rubriques [Activation de POP3 dans Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md) et [Activation d’IMAP4 dans Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md).

Par défaut, les utilisateurs disposant de boîtes aux lettres sur des ordinateurs exécutant Exchange 2013 peuvent accéder à celles-ci avec Outlook ou Outlook Web App, Exchange ActiveSync ou Outlook Voice Access. Outlook, Outlook Web App et Outlook Voice Access permettent aux utilisateurs de messagerie d’utiliser l’ensemble complet des fonctionnalités accessibles aux utilisateurs disposant de boîtes aux lettres sur des serveurs Exchange 2016.

**Contenu de cette rubrique**

Vue d'ensemble des fonctionnalités des protocoles POP3 et IMAP4

Connectivité intersite POP3 et IMAP4

Utilisation de comptes non standard avec POP3 et IMAP4

Différences entre les protocoles POP3 et IMAP4

Options d'envoi et de réception des applications de messagerie POP3 et IMAP4

Applications POP3 et IMAP4

Paramètres utilisateur pour configurer l’accès POP3 ou IMAP4 aux boîtes aux lettres Exchange 2013

## Vue d'ensemble des fonctionnalités des protocoles POP3 et IMAP4

Cette section décrit les fonctionnalités des protocoles POP3 et IMAP4 pour Exchange 2013.

Les avantages et inconvénients des protocoles POP3 et IMAP4 sont les suivants :

  - **POP3**   POP3 a été conçu pour prendre en charge le traitement du courrier en mode hors connexion. Avec POP3, les messages électroniques sont supprimés du serveur et stockés sur le client POP3 local, sauf si ce dernier a été configuré de façon à laisser le courrier sur le serveur. L'utilisateur est donc responsable de la sécurité et de la gestion des données. POP3 n'offre pas de fonctionnalités de collaboration avancées telle que la planification à l'aide d'un calendrier et la gestion des contacts et des tâches.

  - **IMAP4**   IMAP4 offre un accès en ligne et hors ligne, mais, comme POP3, IMAP4 n'offre pas de fonctionnalités de collaboration avancées telles que la planification à l'aide d'un calendrier et la gestion des contacts et des tâches.

Les applications de messagerie POP3 et IMAP4 n’utilisent pas les protocoles POP3 et IMAP4 pour envoyer des messages au serveur de messagerie. Elles reposent sur le protocole SMTP pour l’envoi de messages. Le connecteur de réception des messages déposés par des applications clientes utilisant le protocole POP3 ou IMAP4 est créé automatiquement lors de l’installation d’Exchange. Pour plus d’informations sur les connecteurs, consultez la rubrique [Connecteurs de réception](receive-connectors-exchange-2013-help.md).

> [!NOTE]
> Chaque fois qu'un utilisateur utilise un programme de messagerie basé sur POP ou IMAP pour ouvrir ses messages Office 365, il peut constater un retard de quelques secondes. Ce retard est dû à un serveur proxy, qui introduit une étape supplémentaire pour l’authentification. Le serveur proxy recherche d’abord le serveur attribué (serveur d’accès au client), puis s’authentifie par rapport à celui-ci.


## Connectivité intersite POP3 et IMAP4

Dans les versions antérieures d'Exchange, vous deviez configurer manuellement les clients POP3 et IMAP4 pour qu'ils se connectent à leur messagerie à partir d'un site de votre organisation lorsque leur boîte aux lettres se trouvait dans un autre site. Par défaut, Exchange 2013 transmet automatiquement le courrier d'un serveur d'accès au client d'un site au serveur approprié.

## Utilisation de comptes non standard avec POP3 et IMAP4

Vous ne pouvez pas utiliser le compte Anonyme ni le compte Invité pour vous connecter à une boîte aux lettres Exchange 2016 via un accès POP3 ou IMAP4. Les comptes Anonyme sont bloqués à cause de failles de sécurité lorsque vous utilisez des comptes non standard pour l’accès POP3 et IMAP4. En outre, vous ne pouvez pas vous connecter à la boîte aux lettres de l’administrateur via un accès POP3 ou IMAP4. Cette restriction a été incluse intentionnellement dans Exchange 2013 pour améliorer la sécurité de la boîte aux lettres de l’administrateur. Pour accéder à la boîte aux lettres de l’administrateur, vous devez utiliser Outlook ou Outlook Web App.

## Différences entre les protocoles POP3 et IMAP4

**POP3** POP3 est un protocole Internet de messagerie fréquemment utilisé. Par défaut, lorsque des applications de messagerie POP3 téléchargent des messages sur un ordinateur client, ces derniers sont supprimés du serveur. Quand aucune copie du courrier d'un utilisateur n'est conservée sur le serveur de messagerie, l'utilisateur ne peut pas accéder à ses messages électroniques à partir de plusieurs ordinateurs. Toutefois, certaines applications de messagerie POP3 peuvent être configurées pour conserver des copies des messages sur le serveur afin que ces derniers soient accessibles à partir d'un autre ordinateur. Les applications clientes POP3 peuvent être utilisées uniquement pour télécharger des messages du serveur de messagerie vers un dossier unique (généralement la boîte de réception) sur l'ordinateur client. Le protocole POP3 ne peut pas synchroniser plusieurs dossiers sur le serveur de messagerie avec plusieurs dossiers sur l'ordinateur client.

**IMAP4** Les applications clientes de messagerie utilisant IMAP4 sont plus flexibles et offrent généralement davantage de fonctionnalités que celles utilisant POP3. Par défaut, lorsque les applications de messagerie IMAP4 téléchargent des messages électroniques sur un ordinateur client, une copie de ces derniers est conservée sur le serveur de messagerie. Étant donné qu’une copie des messages électroniques de l’utilisateur est conservée sur le serveur de messagerie, l’utilisateur peut accéder aux mêmes messages à partir de plusieurs ordinateurs. La messagerie IMAP4 permet à l'utilisateur de créer plusieurs dossiers de messagerie sur le serveur de messagerie et d'y accéder. Les utilisateurs peuvent ensuite accéder à leurs messages sur le serveur à partir d'ordinateurs se trouvant à différents emplacements. Par exemple, la plupart des applications IMAP4 peuvent être configurées pour conserver une copie des éléments envoyés d'un utilisateur sur le serveur afin qu'il puisse y accéder à partir de n'importe quel autre ordinateur. IMAP4 prend en charge des fonctionnalités supplémentaires prises en charge par la plupart des applications IMAP4. Par exemple, certaines applications IMAP4 incluent une fonctionnalité qui permet aux utilisateurs d'afficher uniquement les en-têtes de leurs messages sur le serveur (expéditeur et objet), puis de télécharger uniquement les messages qu'ils veulent lire. IMAP4 ne prend pas non plus en charge l’accès aux dossiers publics.

> [!NOTE]
> Les clients IMAP4 et POP3 ont un accès limité aux informations de calendrier d'Exchange. Pour plus d'informations, consultez les rubriques <a href="configure-calendar-options-for-pop3-exchange-2013-help.md">Configurer les options de calendrier pour POP3</a> et <a href="configure-calendar-options-for-imap4-exchange-2013-help.md">Configurer les options de calendrier pour IMAP4</a>.


## Options d'envoi et de réception des applications de messagerie POP3 et IMAP4

Les applications de messagerie POP3 et IMAP4 permettent aux utilisateurs de décider quand ils veulent se connecter au serveur pour envoyer et recevoir des messages. Cette section présente certaines des options de connectivité les plus courantes, ainsi que certains facteurs que vos utilisateurs doivent prendre en considération quand ils sélectionnent des options de connexion disponibles dans leurs applications de messagerie POP3 et IMAP4.

## Paramètres de configuration courants

Voici trois des principaux paramètres de connexion qui peuvent être définis dans les applications de messagerie POP3 et IMAP4 :

  - Envoyer et recevoir des messages à chaque démarrage de l’application de messagerie. Lorsque cette option est utilisée, le courrier électronique est envoyé et reçu uniquement lorsque l’utilisateur démarre l’application de messagerie.

  - Envoyer et recevoir les messages manuellement. Lorsque cette option est utilisée, les messages sont uniquement envoyés et reçus lorsque l’utilisateur clique sur l’option « Envoyer et recevoir » dans l’interface utilisateur client.

  - Envoyer et recevoir les messages à un intervalle de minutes défini. Lorsque l’utilisateur définit cette option, l’application cliente se connecte au serveur à un intervalle de minutes défini pour envoyer les messages et télécharger les nouveaux.

Pour plus d'informations sur la configuration de ces paramètres pour l'application de messagerie utilisée, consultez la documentation d'aide fournie avec l'application.

## Considérations relatives à la sélection des options d’envoi et de réception

Si le périphérique ou l’ordinateur qui exécute l’application de messagerie POP3 ou IMAP4 est toujours connecté à Internet, les utilisateurs peuvent souhaiter configurer l’application de messagerie de manière à envoyer et recevoir des messages selon un intervalle exprimé en minutes. Une connexion au serveur à intervalles réguliers permet aux utilisateurs de tenir leur application de messagerie à jour avec les informations les plus récentes sur le serveur. Toutefois, si le périphérique ou l’ordinateur qui exécute l’application de messagerie POP3 ou IMAP4 n’est pas connecté à Internet en permanence, les utilisateurs peuvent configurer l’application de messagerie pour envoyer et recevoir des messages manuellement.

> [!NOTE]
> Si l'utilisateur utilise une application de messagerie IMAP4 prenant en charge la commande IDLE IMAP4, il peut envoyer et recevoir des messages à partir de sa boîte aux lettres Exchange pratiquement en temps réel. Pour que cette méthode de connexion fonctionne, l'application du serveur de messagerie et l'application cliente doivent prendre en charge la commande IDLE IMAP4. Dans la plupart des cas, les utilisateurs n'ont à configurer aucun paramètre de l'application de messagerie IMAP4.


## Applications POP3 et IMAP4

Étant donné qu'Exchange 2013 prend en charge POP3 et IMAP4, les utilisateurs peuvent utiliser n'importe quelle application prenant en charge les applications clientes POP3 et IMAP4 pour se connecter à Exchange 2013. Il peut s'agir, par exemple, de Outlook, Outlook Web App, Windows Live Mail, Outlook Express, Entourage et de nombreuses applications tierces (telles que Gmail, Mozilla Thunderbird et Eudora). Les fonctionnalités prises en charge varient selon l'application de messagerie cliente. Pour plus d'informations sur les fonctionnalités spécifiques des applications clientes POP3 et IMAP4, consultez la documentation de chaque application.

## Paramètres utilisateur pour configurer l’accès POP3 ou IMAP4 aux boîtes aux lettres Exchange 2013

Après avoir activé l’accès client POP3 et IMAP4, vous devez fournir aux utilisateurs les informations dont ils ont besoin pour connecter leurs programmes de messagerie à leurs boîtes aux lettres Exchange 2016.

Pour se connecter depuis l'intérieur du réseau d'entreprise, les utilisateurs ont besoin des informations suivantes :

  - Nom du serveur POP3 ou IMAP4 interne

  - Numéro de port POP3 ou IMAP4 interne

  - Méthode de chiffrement POP3 ou IMAP4 interne

  - Nom SMTP (serveur sortant) interne

  - Numéro de port SMTP (serveur sortant) interne

  - Méthode de chiffrement SMTP (serveur sortant) interne

Pour se connecter depuis Internet, les utilisateurs ont besoin des informations suivantes :

  - Nom du serveur POP3 ou IMAP4 externe

  - Numéro de port POP3 ou IMAP4 externe

  - Méthode de chiffrement POP3 ou IMAP4 externe

  - Nom SMTP (serveur sortant) externe

  - Numéro de port SMTP (serveur sortant) externe

  - Méthode de chiffrement SMTP (serveur sortant) externe

Vous pouvez fournir ces paramètres aux utilisateurs par courrier électronique ou via toute autre méthode de communication manuelle. Vous pouvez également configurer Exchange pour que vos utilisateurs puissent utiliser Outlook Web App pour rechercher leurs propres paramètres.

**Configuration d'Exchange afin que les utilisateurs puissent consulter leurs paramètres de serveurs POP3, IMAP4 et SMTP**

Par défaut, les utilisateurs ne peuvent pas rechercher les paramètres de serveurs POP3, IMAP4 et SMTP via Outlook Web App. Pour offrir cette possibilité à vos utilisateurs, vous devez utiliser les cmdlets **Set-PopSettings** et **Set-ImapSettings**. Pour permettre à vos utilisateurs de consulter leurs paramètres de serveurs (sortants) SMTP, vous devez utiliser la cmdlet **Set-ReceiveConnector**.

Pour permettre aux utilisateurs de consulter leurs propres paramètres POP3, IMAP4 et SMTP, procédez comme suit :

  - **Paramètres POP3**   Exécutez la cmdlet **Set-POPSettings** avec le paramètre *ExternalConnectionSettings*. Utilisez le format `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`. Par exemple, exécutez `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}` si vous voulez que les clients qui se connectent via le serveur avec le nom de domaine complet Dublin01.Contoso.com puissent consulter leurs propres paramètres POP.
    
    Vous devez redémarrer IIS après avoir appliqué ce paramètre.

  - **Paramètres IMAP4**   Exécutez la cmdlet **Set-IMAPSettings** avec le paramètre *ExternalConnectionSettings*. Utilisez le format `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`. Par exemple, exécutez `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}` si vous voulez que les clients qui se connectent via le serveur avec le nom de domaine complet Dublin01.Contoso.com soient en mesure de consulter leurs propres paramètres IMAP.
    
    Vous devez redémarrer IIS après avoir appliqué ce paramètre.

  - **Paramètres SMTP**   Exécutez la cmdlet **Set-ReceiveConnector** avec le paramètre *AdvertiseClientSettings*. Utilisez le format `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`. Par exemple, exécutez `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com` si vous voulez que les clients qui se connectent via le serveur avec le nom de domaine complet Dublin01.Contoso.com puissent rechercher leur propre paramètre SMTP.
    
    Vous devez redémarrer IIS après avoir appliqué ce paramètre.

Après avoir modifié vos paramètres par défaut en exécutant les cmdlets **Set-POPSettings**, **Set-IMAPSettings** et **Set-ReceiveConnector**, vos utilisateurs peuvent consulter leurs paramètres de serveurs POP, IMAP et SMTP externes dans Outlook Web App en cliquant sur **Paramètres** \> **Options** \> **Compte** \> **Mon compte** \> **Paramètres d'accès POP ou IMAP**.

**Conservation d’une copie des messages sur le serveur**

Sur certains programmes de messagerie, le paramètre par défaut consiste à supprimer les messages sur le serveur après leur récupération. Veillez à recommander aux utilisateurs de configurer leur programme de messagerie de façon à conserver sur le serveur une copie de tous les messages récupérés par le client. Quand une copie des messages est conservée sur le serveur, les utilisateurs peuvent accéder à leurs messages à partir d’un autre programme de messagerie.

