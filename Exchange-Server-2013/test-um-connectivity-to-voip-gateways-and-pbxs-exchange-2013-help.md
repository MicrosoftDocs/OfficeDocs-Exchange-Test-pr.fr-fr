---
title: 'Tester la connectivité de messagerie unifiée à des passerelles VoIP et des PBX: Exchange 2013 Help'
TOCTitle: Tester la connectivité de messagerie unifiée à des passerelles VoIP et des PBX
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56269362
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tester la connectivité de messagerie unifiée à des passerelles VoIP et des PBX

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2014-09-17_

Vous pouvez tester le fonctionnement de la messagerie unifiée (MU) et l’équipement téléphonique connecté associé. Quand vous exécutez la procédure suivante, le serveur de boîtes aux lettres et d’accès au client teste le fonctionnement de bout en bout complet du système de messagerie vocale. Cela inclut les composants téléphoniques connectés aux serveurs de boîtes aux lettres et d’accès au client, notamment les passerelles VoIP, les PBX (autocommutateurs privés), les PBX IP et le câblage.

Pour découvrir d’autres tâches de gestion relatives au dépannage de la messagerie unifiée, voir [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Serveur de boîtes aux lettres (service de messagerie unifiée) » et « Serveur d’accès au client (service de routeur d’appel de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Pour exécuter les procédures suivantes, vous devez vous connecter au serveur de boîtes aux lettres à l’aide d’un compte appartenant au groupe Administrateurs local.

  - Vérifiez que le serveur de boîtes aux lettres est installé sur le même ordinateur que le serveur d’accès au client ou sur un ordinateur séparé.

  - Vérifiez que le serveur d’accès au client est installé sur le même ordinateur que le serveur de boîtes aux lettres ou sur un ordinateur séparé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement Shell pour tester le fonctionnement de la messagerie unifiée et des composants téléphoniques

Cet exemple teste la capacité de la passerelle IP de messagerie unifiée à écouter les requêtes SIP sur le port TCP 4060.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

Cet exemple teste la capacité du serveur de boîtes aux lettres local à utiliser une connexion TCP (Transmission Control Protocol) non sécurisée au lieu d’une connexion MTLS (Mutual Transport Layer Security) sécurisée pour établir un appel via une passerelle IP de messagerie unifiée nommée `MyUMIPGateway` à l’aide du numéro de téléphone 56780.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

Cet exemple teste le numéro Outlook Voice Access dans un plan de numérotation à l’aide d’un URI SIP. Cet exemple peut être utilisé dans un environnement qui inclut Lync Server.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"

> [!NOTE]
> Vous pouvez définir ce paramètre <code>-Timeout</code> avec une valeur inférieure à 5 secondes. Il est toutefois recommandé de toujours configurer ce paramètre avec une valeur minimale de 5 secondes. Utilisez le mode 2 lorsque le paramètre <code>­UMIPGateway</code> est spécifié dans la syntaxe de ligne de commande.

