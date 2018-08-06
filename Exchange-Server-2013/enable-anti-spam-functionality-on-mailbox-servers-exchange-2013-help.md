---
title: 'Activ. fonction de blocage du courr. ind. sur un srv de BAL: Exchange 2013 | Microsoft Docs'
TOCTitle: Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50478151
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-01-23_

Dans Microsoft Exchange Server 2013, les agents anti-spam suivants sont disponibles dans le service de transport des serveurs de boîtes aux lettres, mais ils ne sont pas installés par défaut :

  - Agent de filtrage du contenu

  - Agent d'ID de l'expéditeur

  - Agent de filtrage des expéditeurs

  - Agent de filtrage des destinataires

  - Agent d’analyse de protocole pour la réputation de l’expéditeur

Toutefois, vous pouvez installer ces agents anti-spam sur un serveur de boîtes aux lettres à l'aide d'un script dans l'environnement Exchange Management Shell. En règles générales, vous installerez les agents anti-spam sur un serveur de boîtes aux lettres uniquement lorsque votre organisation accepte tout le courrier entrant sans filtrage anti-spam préalable.

Que se passe-t-il si vous installez les agents anti-spam disponibles dans le service de transport d'un serveur de boîtes aux lettres avec d'autres agents anti-spam Exchange en cours d'exécution sur les massages avant d'atteindre le serveur de boîtes aux lettres ? Par exemple, que se passe-t-il si un serveur de transport Edge Microsoft Exchange 2007 ou Exchange 2010 est présent dans le réseau le réseau de périmètre et fournit le courrier entrant directement au service de transport sur le serveur de boîtes aux lettres ? Les agents anti-spam sur le serveur de boîtes aux lettres reconnaissent les valeurs d'en-têtes X anti-spam ajoutées aux messages par d'autres agents anti-spam Exchange, et les messages qui contiennent ces en-têtes X transitent sans être de nouveau analysées. Cependant, les recherches de destinataires exécutées par l'agent de filtrage des destinataires se produisent de nouveau sur le serveur de boîtes aux lettres.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Configuration du transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - L'agent de filtrage des connexions et l'agent de filtrage des pièces jointes ne sont pas disponibles sur les serveurs de boîtes aux lettres. Ils sont uniquement disponibles sur un serveur de Transport Edge. Cependant, l'agent anti-programme malveillant est installé et activé par défaut sur un serveur de boîtes aux lettres. Pour plus d’informations, consultez la rubrique [Détection anti-programmes malveillants](anti-malware-protection-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Utilisez le Shell pour exécuter le script Install-AntispamAgents.ps1

Exécutez la commande suivante :

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## Comment savoir si cette étape a fonctionné ?

Vous savez que cette étape fonctionne lorsque le script s'exécute sans erreur et vous demande de redémarrer le service de transport Microsoft Exchange.

## Étape 2 : Utilisez le Shell pour redémarrer le service de transport Microsoft Exchange

Exécutez la commande suivante :

    Restart-Service MSExchangeTransport

## Comment savoir si cette étape a fonctionné ?

Vous savez que cette étape fonctionne lorsque le service de transport Microsoft Exchange redémarre sans erreur.

## Étape 3 : Utilisez le Shell pour spécifier les serveurs SMTP internes dans votre organisation

Vous devez spécifier les adresses IP de tous les serveurs SMTP internes qui doivent être ignorés par l'agent ID de l'expéditeur. En fait, vous devez spécifier les adresses IP d'au moins un serveur SMTP interne. Si le serveur de boîtes aux lettres sur lequel vous exécutez les agents anti-spam est le seul serveur SMTP de votre organisation, spécifiez l’adresse IP de cet ordinateur.

Pour ajouter des adresses IP des serveurs SMTP internes sans affecter aucune valeur existante, exécutez la commande suivante :

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

Cet exemple montre comment ajouter les adresses 10.0.1.10 et 10.0.1.11 d’un serveur SMTP interne à la configuration de transport de votre organisation.

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez spécifier l'adresse IP avec succès d'au moins un serveur SMTP interne, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  Vérifiez que l'adresse IP d'au moins un serveur SMTP interne valide est affiché.

