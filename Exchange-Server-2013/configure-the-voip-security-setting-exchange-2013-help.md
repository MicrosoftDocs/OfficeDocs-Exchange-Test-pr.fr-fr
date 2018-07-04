---
title: 'Configuration du paramètre de sécurité VoIP: Exchange 2013 Help'
TOCTitle: Configuration du paramètre de sécurité VoIP
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50478907
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration du paramètre de sécurité VoIP

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2014-10-16_

Vous pouvez activer la sécurité VoIP (Voice over IP) pour un plan de numérotation de messagerie unifiée. Par défaut, lorsqu'un plan de numérotation de messagerie unifiée est créé, il utilise un mode non sécurisé ou aucun chiffrement. Les serveurs Exchange peuvent répondre à des appels pour un ou plusieurs plans de numérotation de messagerie unifiée et peuvent répondre à des appels pour des plans de numérotation qui disposent de paramètres de sécurité VoIP différents. Dans Office 365 et Exchange Online, le mode sécurisé est obligatoire et ne peut pas être désactivé.

Lorsque vous configurez un plan de numérotation de messagerie unifiée afin qu'il utilise le mode sécurisé ou SIP (Session Initiation Protocol) sécurisé, les serveurs Exchange qui répondent aux appels pour le plan de numérotation de messagerie unifiée chiffrent le trafic de signalisation SIP (pour le mode Sécurisé SIP), ou à la fois les canaux de support RTP et le trafic de signalisation SIP (pour le mode sécurisé).

> [!NOTE]
> Pour les déploiements locaux et hybrides, quand vous configurez SipTCPListeningPort, SipTLSListeningPort ou UMStartUpMode sur un serveur d'accès au client qui exécute le service routeur des appels de messagerie unifiée de Microsoft Exchange ou sur un serveur de boîtes aux lettres qui exécute le service de messagerie unifiée de Microsoft Exchange, vous devez configurer les règles du pare-feu Windows correctement pour permettre le trafic réseau SIP et RTP.


Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer la sécurité VoIP sur un plan de numérotation de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée**\>**Plans de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation de messagerie unifiée dont vous voulez modifier la sécurité VoIP, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Nouveau plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

3.  Dans **Général**, sous **Mode de sécurité VoIP**, activez l'une des options suivantes :
    
      - **SIP secured**
    
      - **Non sécurisé(e)** (par défaut)
    
      - **Sécurisé**

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la sécurité VoIP sur un plan de numérotation de messagerie unifiée

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MySecureDialPlan` pour le chiffrement du trafic SIP et RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MySecureDialPlan` pour le chiffrement du trafic SIP mais pas celui du trafic RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

Cet exemple montre comment configurer un plan de numérotation de messagerie unifiée nommé `MySecureDialPlan` afin de ne pas chiffrer le trafic SIP et RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

