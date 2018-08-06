---
title: "Autoriser/empêcher répondeur auto. sur srv d’accès client: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Autoriser ou empêcher de répondeur automatique sur un serveur d'accès au Client
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50555420
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser ou empêcher de répondeur automatique sur un serveur d'accès au Client

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-18_

Vous pouvez autoriser le service Microsoft Exchange Unified Messaging routeur d'appels sur un serveur d'accès au Client pour répondre aux nouveaux appels ou l'empêcher de cette opération. Par défaut, un serveur d'accès au Client est dans un état activé après son installation. Lorsque vous configurez le serveur d'accès Client d'accepter des messages vocaux entrants, télécopie, standard automatique et les appels Outlook Voice Access, vous utilisez l'applet de commande **Set-ServerComponentState** .

Configuration du Mode de Maintenance pour un serveur d'accès Client vous permet de prendre le serveur hors service. Pour un serveur d'accès au Client, out-of-service signifie que le serveur n'accepte pas les appels entrants à partir des passerelles VoIP, PBX IP, PBX compatible SIP ou contrôleurs de frontière de session (SBC).

Dans Exchange 2007 et Exchange 2010, un paramètre d'état pouvait être utilisé pour contrôler l'état de fonctionnement d'un serveur de messagerie unifiée. Dans Exchange 2013, aucun paramètre d'état n'est proposé à cette fin avec la cmdlet **Set-UMCallRouterSettings** sur un serveur d'accès au client.

> [!NOTE]
> Il n'est pas nécessaire que les serveurs d'accès au Client et boîte aux lettres doit être ajouté à un plan de numérotation de messagerie unifiée avant qu'ils peuvent traiter les appels pour la messagerie unifiée, sauf lorsque vous êtes intégration de la messagerie unifiée et Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Par défaut, tous les accès au Client et boîte aux lettres de serveurs dans une organisation sont disponibles pour répondre aux appels entrants.


Pour les tâches de gestion supplémentaires relatives aux serveurs d'accès au client, consultez la rubrique [Procédures de services de messagerie unifiée](um-services-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Paramètres de configuration du serveur Exchange » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur d'accès au client est installé, soit sur le même ordinateur que le serveur de boîtes aux lettres, soit sur un ordinateur distinct.

  - Si vous placez un serveur d'accès Client en Mode Maintenance, vérifiez qu'il existe une capacité suffisamment saine dans le tableau d'accès au Client pour autoriser le serveur à la mise hors service.

  - Avant de passer à un serveur en mode Maintenance, vérifier l'intégrité du serveur et assurez-vous qu'il est prêt à passer en service.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour autoriser ou interdire un répondeur automatique sur un serveur d'accès au client

Cet exemple autorise un serveur d'accès au client `UMCallRouter-05x.contoso.com` à répondre à des appels vocaux, de télécopie, de standard automatique et Outlook Voice Access entrants à partir de passerelles VoIP, de PBX IP, de PBX compatibles SIP et de contrôleurs SBC, et écrit les modifications dans le Registre du serveur UMCallRouter-05x.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

Cet exemple empêche un serveur d'accès au client `UMCallRouter-05x.contoso.com` de répondre à des appels vocaux, de télécopie, de standard automatique et Outlook Voice Access entrants à partir de passerelles VoIP, de PBX IP, de PBX compatibles SIP et de contrôleurs SBC, et écrit les modifications uniquement dans Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

