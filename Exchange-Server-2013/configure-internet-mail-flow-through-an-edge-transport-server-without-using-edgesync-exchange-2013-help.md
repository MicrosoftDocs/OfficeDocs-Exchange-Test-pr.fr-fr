---
title: 'Configurer le flux de messagerie Internet via un serveur de transport Edge sans utiliser EdgeSync: Exchange 2013 Help'
TOCTitle: Configurer le flux de messagerie Internet via un serveur de transport Edge sans utiliser EdgeSync
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61180540
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le flux de messagerie Internet via un serveur de transport Edge sans utiliser EdgeSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-01-23_

Nous vous recommandons d’utiliser le processus d’abonnement Edge pour établir le flux de messagerie entre votre organisation Exchange et un serveur de transport Edge. Toutefois, certaines situations peuvent vous empêcher d’abonner le serveur de transport Edge à votre organisation Exchange à l’aide du processus d’abonnement Edge. Pour établir manuellement le flux de messagerie entre votre organisation Exchange et un serveur de transport Edge, vous devez créer et configurer les connecteurs d’envoi et de réception sur le serveur de transport Edge et les serveurs de boîtes aux lettres dans l’organisation Exchange.

## Avant de commencer

  - Durée d’exécution estimée de cette tâche : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Connecteurs d’envoi », « Connecteurs d’envoi - Transport Edge » et « Connecteurs de réception - Transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Cette procédure utilise l’authentification de base sur TLS pour assurer le chiffrement et l’authentification. Si vous utilisez l’authentification de base sur TLS, le certificat de serveur SSL X.509 doit être installé sur le serveur de réception. La valeur du nom de domaine complet configurée sur le connecteur de réception doit correspondre au nom de domaine complet du certificat de serveur SSL. Par défaut, la valeur du FQDN sur le connecteur de réception est le FQDN du serveur contenant le connecteur de réception.

  - Vous pouvez également utiliser la méthode d’authentification sécurisée de l’extérieur. Toutefois, dans ce cas, la communication entre les serveurs de transport Edge et de boîtes aux lettres n’est ni authentifiée ni chiffrée par Exchange. Nous vous recommandons d’utiliser la méthode d’authentification sécurisée de l’extérieur uniquement lorsqu’une méthode de chiffrement supplémentaire est également utilisée. La méthode de chiffrement peut être une association IPSec (sécurité du protocole Internet) ou un réseau privé virtuel (VPN).

  - Un serveur de transport Edge dispose généralement de *plusieurs hébergements*. Le serveur de transport Edge dispose donc de cartes réseau connectées à plusieurs segments réseau. Chacune de ces cartes réseau possède une configuration IP unique. La carte réseau connectée au segment réseau externe ou public doit être configurée pour utiliser un serveur DNS public pour la résolution de nom. Cela permet au serveur de résoudre des noms de domaine de protocole SMTP (Simple Mail Transfer Protocol) vers les enregistrements de ressource MX et de router la messagerie sur Internet. La carte réseau connectée au segment réseau interne ou privé doit être configurée pour utiliser un serveur DNS dans le réseau de périmètre ou doit disposer d’un fichier Hôtes.

  - Vous devez créer un compte d’utilisateur dans Active Directory et ajouter le compte au groupe de sécurité universel sur l’ordinateur Exchange Server. Ce compte est utilisé par le connecteur d’envoi sur le serveur de transport Edge pour l’authentification auprès du serveur de boîtes aux lettres dans l’organisation Exchange.
    
    > [!NOTE]
    > Ce compte bénéficie des autorisations associées aux ordinateurs exécutant Exchange Server. Veillez à protéger les informations d’identification du compte afin d’éviter toute utilisation abusive de ce dernier. Vous pouvez configurer le compte pour ne permettre une ouverture de session que sur des ordinateurs spécifiques.


## Procédures relatives au serveur de transport Edge

Les connecteurs suivants sont requis sur le serveur de transport Edge :

  - un connecteur d’envoi configuré pour envoyer des messages vers Internet ;

  - un connecteur d’envoi configuré pour envoyer des messages aux serveurs de boîtes aux lettres dans l’organisation Exchange ;

  - un connecteur de réception configuré pour recevoir des messages de serveurs de boîtes aux lettres uniquement dans l’organisation Exchange ;

  - un connecteur de réception configuré pour accepter les messages provenant d’Internet uniquement.

Par défaut, un connecteur de réception unique est créé lors de l’installation du rôle serveur de transport Edge. Ce connecteur peut être utilisé à la fois pour les messages Internet entrants et les messages entrants provenant des serveurs de boîtes aux lettres. En général, le processus d’abonnement Edge configure automatiquement les autorisations et l’authentification correctes sur le connecteur de réception par défaut. Si le processus d’abonnement Edge n’est pas utilisé, il est recommandé de modifier le connecteur de réception par défaut sur le serveur de transport Edge pour accepter les messages d’Internet uniquement. Vous devez ensuite créer un connecteur de réception sur le serveur de transport Edge configuré pour accepter les messages des serveurs de boîtes aux lettres internes uniquement.

Les sections suivantes vous guident au cours du processus de configuration requis pour préparer votre serveur de transport Edge à communiquer avec votre organisation Exchange.

> [!NOTE]
> Vous pouvez utiliser uniquement l’environnement Exchange Management Shell pour effectuer ces procédures sur les serveurs de transport Edge.


## Étape 1 : Créer un connecteur d’envoi configuré pour envoyer des messages vers Internet

Ce connecteur d’envoi requiert la configuration suivante :

  - **Nom**   Vers Internet (ou tout autre nom descriptif)

  - **Type d’utilisation**   Internet.

  - **Espaces d’adressage**   "\*" (tous les domaines)

  - **Paramètres réseau**   Les enregistrements MX DNS permettent de router les messages automatiquement. En fonction de la configuration de votre réseau, vous pouvez également router les messages via un hôte actif. L’hôte actif route alors les messages vers Internet.

Pour créer un connecteur d’envoi configuré pour l’envoi de messages à Internet, exécutez la commande suivante.

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [New-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998936\(v=exchg.150\)).

## Étape 2 : Créer un connecteur d’envoi configuré pour envoyer des messages à l’organisation Exchange

Utilisez la cmdlet **New-SendConnector** pour créer un connecteur d’envoi.

> [!NOTE]
> Avant de créer un connecteur d’envoi, vous devez d’abord exécuter la commande <strong>Get-Credential</strong> pour enregistrer le nom d’utilisateur et le mot de passe que vous utiliserez dans une variable temporaire. Vous devez effectuer cette opération car la cmdlet <strong>New-SendConnector</strong> n’acceptera pas les informations d’identification de l’utilisateur en texte brut.


Ce connecteur d’envoi requiert la configuration suivante :

  - **Nom**   Vers l’organisation interne (ou tout autre nom descriptif)

  - **Nom**   Interne

  - **Espaces d’adressage**   Tous les domaines acceptés pour l’organisation Exchange. Par exemple, \*.contoso.com.

  - Routage DNS désactivé (routage d’hôte actif activé)

  - **Hôtes actifs**   Nom de domaine complet d’un ou de plusieurs serveurs de boîtes aux lettres en tant qu’hôtes actifs. Par exemple, mbxserver01.contoso.com et mbxserver02.contoso.com.

  - **Méthodes d’authentification de l’hôte actif**   Authentification de base sur TLS

  - **Informations d’authentification de l’hôte actif**   Informations d’identification pour le compte d’utilisateur dans le domaine interne. Vous devez d’abord enregistrer le nom d’utilisateur et le mot de passe dans une variable temporaire, car la cmdlet **New-SendConnector** n’acceptera pas les informations d’identification de l’utilisateur en texte brut.

Pour créer un connecteur d’envoi configuré pour l’envoi de messages à l’organisation Exchange, exécutez les commandes suivantes.

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998936\(v=exchg.150\)).

## Étape 3 : Modifier le connecteur de réception par défaut pour accepter les messages provenant d’Internet uniquement

Vous devez apporter les modifications de configuration suivantes pour le connecteur de réception par défaut :

  - Modifier le nom pour indiquer que le connecteur sera utilisé uniquement pour recevoir des messages électroniques provenant d’Internet. Le nom du connecteur de réception par défaut est « Default internal Receive connector \<Nom du serveur de transport Edge\> ».

  - Modifier les liaisons réseau pour accepter les messages provenant uniquement de la carte réseau accessible depuis Internet. Par exemple, 10.1.1.1 et la valeur standard de port SMTP TCP de 25.

Pour modifier le connecteur de réception par défaut pour accepter uniquement les messages provenant d’Internet, exécutez la commande suivante.

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [Set-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125140\(v=exchg.150\)).

## Étape 4 : Créer un connecteur de réception configuré pour accepter uniquement les messages provenant de l’organisation Exchange

Ce connecteur de réception requiert la configuration suivante :

  - **Nom**   À partir de l’organisation interne (ou tout autre nom descriptif)

  - **Type d’utilisation**   Interne

  - **Liaisons réseau locales**   Carte réseau interne accessible par le réseau. Par exemple, 10.1.1.2 et la valeur standard de port SMTP TCP de 25.

  - **Paramètres du réseau distant**   Adresse IP d’un ou de plusieurs serveurs de boîtes aux lettres dans l’organisation Exchange Par exemple, 192.168.5.10 et 192.168.5.20.

  - **Méthodes d’authentification**   TLS, authentification de base, authentification de base sur TLS et authentification Exchange Server.

Pour créer un connecteur de réception configuré pour accepter uniquement les messages provenant de l’organisation Exchange, exécutez la commande suivante.

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement configuré les connecteurs d’envoi et de réception requis, exécutez les commandes suivantes sur le serveur de transport Edge et vérifiez que les valeurs affichées correspondent à celles configurées.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## Procédures de serveur de boîtes aux lettres

Les serveurs de boîtes aux lettres de votre organisation nécessitent un connecteur d’envoi configuré pour l’envoi de messages vers le serveur de transport Edge pour le relais vers Internet.

Par défaut, deux connecteurs de réception sont créés lors de l’installation du rôle serveur de boîtes aux lettres. Le connecteur « Client *Nom\_serveur* » est configuré pour accepter les messages des clients de messagerie POP3 et IMAP. Le connecteur « *Nom\_serveur* par défaut » est configuré pour accepter les messages d’un serveur de transport Edge. Aucune modification de ces connecteurs n’est requise.

## Étape 5 : Créer un connecteur d’envoi configuré pour envoyer des messages sortants au serveur de transport Edge

Ce connecteur d’envoi requiert la configuration suivante :

  - **Nom**   Vers Edge (ou tout autre nom descriptif)

  - **Type d’utilisation**   Interne

  - **Espaces d’adressage**   "\*" (tous les domaines)

  - Routage DNS désactivé (routage d’hôte actif activé)

  - **Hôtes actifs**   Adresse IP ou nom de domaine complet du serveur de transport Edge. Par exemple, edge01.contoso.net

  - **Serveurs de boîtes aux lettres source**   Nom de domaine complet d’un ou de plusieurs serveurs de boîtes aux lettres Par exemple, mbxserver01.contoso.com et mbxserver02.contoso.com.

  - **Méthode d’authentification de l’hôte actif**   Authentification de base sur TLS.

  - **Informations d’authentification d’hôte actif**   Informations d’identification du compte d’utilisateur sur le serveur de transport Edge Vous devez d’abord enregistrer le nom d’utilisateur et le mot de passe dans une variable temporaire, car la cmdlet **New-SendConnector** n’acceptera pas les informations d’identification de l’utilisateur en texte brut

Pour créer un connecteur d’envoi configuré pour l’envoi de messages sortants vers le serveur de transport Edge, exécutez les commandes suivantes.

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998936\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez créé un connecteur d’envoi configuré pour l’envoi de messages sortants vers le serveur de transport Edge, exécutez la commande suivante sur un serveur de boîtes aux lettres et vérifiez que les valeurs affichées correspondent à celles configurées.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

