---
title: 'Configurer un nom de domaine complet: Exchange 2013 Help'
TOCTitle: Configurer un nom de domaine complet
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 50478870
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer un nom de domaine complet

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-09_

Vous pouvez configurer une passerelle IP de messagerie unifiée soit avec une adresse IP soit avec un nom de domaine complet. Lorsque vous créez une passerelle IP de messagerie unifiée, vous devez définir l’adresse IP ou le nom de domaine complet configuré sur la passerelle VoIP, le PBX IP ou le contrôleur de frontière de session (SBC) que vous utilisez. Vous pouvez modifier l'adresse IP ou le nom de domaine complet après la création de la passerelle IP de messagerie unifiée.

Si vous créez une passerelle IP de messagerie unifiée à l'aide d'un nom de domaine complet, vous devez créer les enregistrements d'hôte (A) appropriés dans votre zone de recherche directe de DNS. Si vous créez une passerelle IP de messagerie unifiée à l’aide d’un nom de domaine complet et que la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver, puis réactiver la passerelle IP de messagerie unifiée pour vous assurer que ses informations de configuration sont correctement mises à jour.

Si vous souhaitez utiliser une sécurité de la couche de transport mutuelle (TLS mutuelle) entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode SIP sécurisé ou en mode sécurisé, vous devez configurer la passerelle IP de messagerie unifiée avec un nom de domaine complet. Vous devez également la configurer pour écouter le port 5061 et vérifier que la passerelle VoIP, le PBX IP ou le SBC a également été configuré(e) pour écouter les demandes TLS mutuelles sur le port 5061. Pour configurer une passerelle IP de messagerie unifiée, exécutez la commande suivante : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, voir [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour configurer un nom de domaine complet

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Passerelle IP de la messagerie unifiée**, dans **Adresse**, saisissez le nom de domaine complet pour la passerelle VoIP, le PBX compatible SIP, le PBX IP ou le SBC.

3.  Cliquez sur **Enregistrer**.

> [!NOTE]
> Quand vous utilisez un nom de domaine complet, et non une adresse IP, pour la passerelle IP de messagerie unifiée, vérifiez que les enregistrements DNS corrects ont été créés.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer un nom de domaine complet

Dans cet exemple, une passerelle IP de messagerie unifiée nommée `MyUMIPGateway` est configurée avec le nom complet passerellevoip.contoso.com.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

Dans cet exemple, une passerelle IP de messagerie unifiée nommée `MySBC` est configurée avec le nom de domaine complet sbc.contoso.com et écoute les requêtes SIP sur le port TCP 5061.

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

