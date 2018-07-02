---
title: 'Connecteurs de réception: Exchange 2013 Help'
TOCTitle: Connecteurs de réception
ms:assetid: 17751a60-39fe-433f-84d2-bfc14ff4ba51
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996395(v=EXCHG.150)
ms:contentKeyID: 50477581
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connecteurs de réception

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les connecteurs de réception contrôlent le flux de messages entrants à destination de votre organisation Exchange. Ils sont configurés sur des ordinateurs exécutant Microsoft Exchange Server 2013 avec le service de transport ou dans le service frontal d’un serveur d’accès au client. Ils peuvent être créés dans le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell.

Par défaut, les connecteurs de réception requis pour le flux de messagerie interne sont créés automatiquement lors de l’installation d’un serveur d’accès au client ou d’un serveur de boîtes aux lettres.

Les serveurs Exchange 2013 qui exécutent le service de transport nécessitent des connecteurs de réception pour recevoir des messages provenant d’Internet, de clients de messagerie et d’autres serveurs de messagerie. Un connecteur de réception contrôle les connexions entrantes de l’organisation Exchange.

Chaque connecteur de réception écoute les connexions entrantes correspondant aux paramètres du connecteur de réception. Un connecteur de réception écoute les connexions reçues via une adresse IP et un port locaux particuliers et à partir d’une plage d’adresses IP spécifiée. Vous créez un connecteur de réception pour déterminer quels serveurs reçoivent des messages d’une adresse IP ou d’une plage d’adresses IP particulière et pour configurer des propriétés de connecteur spéciales pour les messages transmis via une adresse IP donnée, telles qu’une taille de message plus importante ou un nombre plus élevé de destinataires. Vous pouvez également définir l’étendue du connecteur de réception à l’aide du paramètre *TlsCertificateName* de la cmdlet **Set-ReceiveConnector** qui vous permet de spécifier le certificat à utiliser pour le connecteur.

La portée des connecteurs de réception s’étend à un serveur unique et détermine la manière dont ce dernier écoute les connexions. Lorsque vous créez un connecteur de réception sur un serveur de boîtes aux lettres exécutant le service de transport, le connecteur de réception est stocké dans Active Directory comme un objet enfant du serveur sur lequel il est créé.

Si vous avez besoin d’autres connecteurs de réception pour des scénarios spécifiques, vous pouvez les créer à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell. Chaque connecteur de réception doit utiliser une combinaison unique de liaisons d’adresses IP, d’affectations de numéro de port et de plages d’adresses IP distantes à partir desquelles le courrier électronique est accepté.

Pour plus d’informations sur la création d’un connecteur de réception, consultez la rubrique [Recevoir des procédures de connecteur](receive-connector-procedures-exchange-2013-help.md).

**Contenu de cette rubrique**

Connecteurs de réception par défaut créés lors de l’installation

Connecteurs de réception par défaut créés sur un serveur de boîtes aux lettres exécutant le service de transport

Connecteurs de réception par défaut créés sur un serveur de transport frontal

Types de connecteurs de réception

Groupes d’autorisations du connecteur de réception

Spécifications des types de connecteurs de réception

Autorisations du connecteur de réception

Paramètres d’authentification des connecteurs de réception

Nouvelles fonctionnalités des connecteurs de réception dans Exchange 2013

## Connecteurs de réception par défaut créés lors de l’installation

Certains connecteurs de réception sont créés par défaut lorsque vous installez le rôle serveur de boîtes aux lettres.

## Connecteurs de réception par défaut créés sur un serveur de boîtes aux lettres exécutant le service de transport

Lorsque vous installez un serveur de boîtes aux lettres qui exécute le service de transport, deux connecteurs de réception sont créés. Aucun connecteur de réception supplémentaire n’est nécessaire pour une opération standard. Aussi, dans la plupart des cas, les connecteurs de réception par défaut ne requièrent aucun changement de configuration. Ces connecteurs sont les suivants :

  - **\<nom du serveur\> par défaut**    Accepte des connexions des serveurs de boîtes aux lettres exécutant le service de transport et de serveurs Edge.

  - **\<nom du serveur\> proxy client**   Accepte les connexions provenant de serveurs frontaux. En règle générale, les messages sont envoyés à un serveur frontal via SMTP.

Chaque connecteur se voit affecter une valeur *TransportRole*. Vous pouvez l’utiliser pour déterminer le rôle dans lequel le connecteur est exécuté. Cela peut être utile lorsque vous exécutez plusieurs rôles sur un serveur. La valeur *TransportRole* de chaque connecteur de réception susmentionné est **HubTransport**.

Pour afficher les connecteurs de réception par défaut et les valeurs de leurs paramètres, utilisez la cmdlet [Get-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/aa998618\(v=exchg.150\)).

## Connecteurs de réception par défaut créés sur un serveur de transport frontal

Pendant l’installation, trois connecteurs de réception sont créés sur le serveur d’accès au client ou de transport frontal. Le connecteur de réception frontal par défaut est configuré pour accepter des communications SMTP provenant de toutes les plages d’adresses IP. En outre, un connecteur de réception peut agir comme un proxy sortant pour les messages envoyés au serveur frontal à partir de serveurs de boîtes aux lettres. Enfin, un connecteur de réception sécurisé est configuré pour accepter des messages chiffrés via le protocole TLS (Transport Layer Security). Ces connecteurs sont les suivants :

  - **\<nom de serveur\> frontal par défaut**   Accepte les connexions provenant d’expéditeurs SMTP via le port 25. C’est le point d’entrée habituel des messages à destination de votre organisation.

  - **\<nom du serveur\> frontal proxy sortant**   Accepte les messages provenant d’un connecteur d’envoi sur un serveur principal, le proxy frontal étant activé.

  - **\<nom du serveur\> frontal client**   Accepte les connexions sécurisées lorsque le protocole TLS (Transport Layer Security) est appliqué.

Dans une installation classique, aucun connecteur de réception supplémentaire n’est nécessaire.

## Types de connecteurs de réception

Le type détermine les paramètres de sécurité par défaut de chaque connecteur de réception.

Les paramètres de sécurité d’un connecteur de réception spécifie les autorisations attribuées aux sessions qui se connectent au connecteur de réception et les mécanismes d’authentification pris en charge.

Lorsque vous utilisez le Centre d’administration Exchange pour configurer un connecteur de réception, la page du nouveau connecteur de réception vous invite à sélectionner le type de connecteur. Selon votre sélection, les paramètres sont définis conformément à la configuration que vous avez choisie. Vous trouverez davantage d’informations sur les paramètres des types de connecteurs de réception dans des procédures spécifiques. Voici des exemples de procédures : [Créez un connecteur de réception pour recevoir des courriers électroniques depuis l'Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md) et [Créer un connecteur de réception sécurisé pour recevoir le message électronique d’un partenaire](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md).

## Groupes d’autorisations du connecteur de réception

Un groupe d’autorisations est un ensemble prédéfini d’autorisations attribuées à des principaux de sécurité bien connus et à un connecteur de réception. Les principaux de sécurité incluent des utilisateurs, des ordinateurs et des groupes de sécurité. L’utilisation d’un groupe d’autorisations simplifie la configuration des autorisations sur les connecteurs de réception. La propriété **PermissionGroups** définit les groupes ou les rôles pouvant soumettre des messages au connecteur de réception et les autorisations attribuées à ces groupes.

Parmi les groupes d’autorisations, on compte *Anonymous*, *ExchangeUsers*, *ExchangeServers*, *ExchangeLegacyServers* et *Partner*.

## Spécifications des types de connecteurs de réception

Le type détermine les groupes d’autorisations par défaut attribués au connecteur de réception et les mécanismes d’authentification par défaut disponibles pour l’authentification de la session. La liste suivante décrit les types disponibles :

1.  **Client**   Habituellement utilisé pour les connexions aux clients qui n’utilisent pas Microsoft Office Outlook. Il peut utiliser l’authentification TLS.

2.  **Personnalisé**   Habituellement utilisé dans un scénario inter-forêts ou un scénario dans le cadre duquel votre organisation reçoit des messages provenant d’un agent de transfert de messages SMTP.

3.  **Interne**   Utilisé pour les communications entre les serveurs qui exécutent le service de transport ou entre des serveurs de boîtes aux lettres qui exécutent le service de transport et des agents de transfert tiers.

4.  **Internet**   Utilisé pour recevoir des messages SMTP d’Internet.

5.  **Partenaire**   Utilisez ce type pour configurer des communications sécurisées avec un partenaire.

Chaque type est adapté à un scénario de connexion spécifique. Sélectionnez le type dont les paramètres par défaut sont les plus adaptés à la configuration de votre choix. Vous pouvez modifier les autorisations à l’aide des cmdlets **Add-ADPermission** et **Remove-ADPermission**. Pour plus d’informations, consultez les rubriques suivantes :

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/fr-fr/library/aa996048\(v=exchg.150\))

## Autorisations du connecteur de réception

Les autorisations du connecteur de réception sont attribuées à des principaux de sécurité lorsque vous spécifiez les groupes d’autorisations pour le connecteur. Quand un principal de sécurité établit une session avec un connecteur de réception, les autorisations du connecteur de réception déterminent si la session est acceptée et la manière dont les messages reçus sont traités. Vous pouvez définir les autorisations du connecteur de réception à l’aide du Centre d’administration Exchange ou du paramètre *PermissionGroups* avec la cmdlet **Set-ReceiveConnector** dans le Shell. Pour modifier les autorisations par défaut d’un connecteur de réception, vous pouvez également utiliser la cmdlet **Add-ADPermission**.

[Autorisations du connecteur de réception](receive-connector-permissions-exchange-2013-help.md) contient une table qui répertorie en détail les principaux de sécurité et les types d’autorisations.

## Paramètres d’authentification des connecteurs de réception

Dans le CAE, vous utilisez les paramètres d'authentification pour un connecteur de réception pour spécifier les mécanismes d'authentification pris en charge par le serveur de transport Exchange 2013. Dans l’environnement de ligne de commande, vous utilisez le paramètre *AuthMechanisms* pour spécifier les mécanismes d’authentification pris en charge. Vous pouvez configurer plusieurs mécanismes d’authentification pour un connecteur de réception. Pour plus d'informations, voir [Mécanismes d’authentification du connecteur de réception](receive-connector-authentication-mechanisms-exchange-2013-help.md).

## Nouvelles fonctionnalités des connecteurs de réception dans Exchange 2013

Les fonctionnalités suivantes ont été ajoutées à Exchange 2013 :

  - Grâce au paramètre *TlsCertificateName*, vous pouvez désigner le certificat émis par l’autorité de certification locale à utiliser pour protéger la messagerie. Elle contribue à réduire les risques de certificats frauduleux.

  - Le paramètre *TransportRole* désigne le rôle de serveur associé à ce connecteur. En général, il permet de définir le rôle de serveur lorsque vous en hébergez plusieurs sur un ordinateur.

Consultez la rubrique [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)) pour plus d’informations sur ces paramètres et d’autres paramètres de connecteurs de réception.

