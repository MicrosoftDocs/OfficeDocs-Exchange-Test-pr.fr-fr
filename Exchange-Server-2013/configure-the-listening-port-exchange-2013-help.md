---
title: "Configuration du port d'écoute: Exchange 2013 Help"
TOCTitle: Configuration du port d'écoute
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50555368
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du port d'écoute

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez configurer le port TCP qui est utilisé pour écouter les requêtes SIP (Session Initiation Protocol) sur une passerelle IP de messagerie unifiée. Par défaut, lors de la création d'une passerelle IP de messagerie unifiée, le numéro du port d'écoute SIP TCP est défini sur 5060. Le port d'écoute SIP TCP ne peut pas être configuré ou modifié à l'aide du Centre d'administration Exchange (CAE). Vous devez configurer le numéro du port d'écoute TCP SIP à l'aide de la cmdlet **Set-UMIPGateway**.

Vous devrez éventuellement configurer le numéro du port d'écoute TCP sur 5061 si vous souhaitez :

  - définir le paramètre de sécurité VoIP d'un plan de numérotation de messagerie unifiée sur Sécurisé SIP ;

  - définir le paramètre de sécurité VoIP d'un plan de numérotation de messagerie unifiée sur Sécurisé ;

  - intégrer à MicrosoftOffice Communications Server 2007 R2 ou Microsoft Lync Server ;

  - utiliser l'authentification TLS (Transport Layer Security) mutuelle pour chiffrer les données réseau entre les serveurs Exchange et une passerelle VoIP, un PBX (Private Branch eXchange) compatible SIP, un PBX IP ou un contrôleur de frontière de session (SBC).

Pour utiliser Mutual TLS entre une passerelle IP de messagerie unifiée et un plan de numérotation en mode Sécurisé SIP ou Sécurisé, lors de la création de la passerelle IP de messagerie unifiée, vous devez la configurer avec un nom de domaine complet, puis utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la passerelle IP de messagerie unifiée afin qu'elle écoute sur le port TCP 5061. Vous devez également vérifier que l'ensemble des passerelles VoIP, PBX compatibles SIP, PBX IP et SBC ont été configurés pour écouter les requêtes Mutual TLS sur le port 5061.

> [!NOTE]
> Lorsque vous créez une passerelle IP de messagerie unifiée à l'aide d'un nom de domaine complet, vous devez créer les enregistrements d'hôte (A) appropriés dans votre zone de recherche directe de DNS. Si vous créez une passerelle IP de messagerie unifiée à l'aide d'un nom de domaine complet et que la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver puis réactiver la passerelle IP de messagerie unifiée pour garantir que ses informations de configuration soient correctement mises à jour.


Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d'effectuer cette procédure, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le port d'écoute TCP

Cet exemple montre comment configurer la passerelle IP de messagerie unifiée `MyUMIPGateway` avec le nom de domaine complet mTLS.MyUMIPGateway.contoso.com et écouter les requêtes SIP sur le port TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

Cet exemple montre comment configurer la passerelle IP de messagerie unifiée `MyUMIPGateway` avec le nom de domaine complet SIPSecured.MyUMIPGateway.contoso.com et écouter les requêtes SIP sur le port TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

Cet exemple montre comment configurer la passerelle IP de messagerie unifiée `MyUMIPGateway` avec le nom de domaine complet MyOCSUMIPGateway.contoso.com et écouter les requêtes SIP sur le port TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

