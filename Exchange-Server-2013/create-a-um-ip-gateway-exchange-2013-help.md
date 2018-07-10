---
title: 'Créer une passerelle IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer une passerelle IP de messagerie unifiée
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50478214
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: HT
---

# Créer une passerelle IP de messagerie unifiée: Exchange 2013 Help

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-16_

Quand vous créez une passerelle IP de messagerie unifiée, vous autorisez les serveurs Exchange à se connecter à une nouvelle passerelle VoIP (Voix sur IP), un PBX (Private Branch eXchange) à extension SIP (Session Initiation Protocol), un PBX IP ou un contrôleur de frontière de session (SBC). Immédiatement après avoir créé une passerelle IP de messagerie unifiée, vous devez créer un groupement de postes de messagerie unifiée, puis associez ce dernier à la passerelle IP de messagerie unifiée. Vous pouvez associer la passerelle IP de messagerie unifiée à un ou plusieurs plans de numérotation de messagerie unifiée en créant un ou plusieurs groupements de postes de messagerie unifiée.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utilisation du Centre d'administration Exchange pour créer une passerelle IP de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, puis cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouvelle passerelle IP de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Cette zone de texte permet de spécifier un nom unique pour la passerelle IP de messagerie unifiée. Il s'agit du nom complet qui apparaît dans le CAE. Si vous devez modifier le nom complet de la passerelle IP de messagerie unifiée après sa création, vous devez d'abord supprimer la passerelle IP de messagerie unifiée existante, puis en créer une autre avec le nom souhaité. Le nom de passerelle IP de messagerie unifiée est obligatoire mais utilisé à des fins d'affichage uniquement. Dans la mesure où votre organisation peut utiliser plusieurs passerelles IP de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour ces passerelles. La longueur maximale d'un nom de passerelle IP de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Adresse**   Vous pouvez configurer une passerelle IP de messagerie unifiée soit avec une adresse IP soit avec un nom de domaine complet. Utilisez cette boîte de dialogue pour spécifier l'adresse IP configurée sur la passerelle VoIP, au standard privé (PBX) SIP, PBX IP ou SBC ou un nom de domaine complet. Cette boîte de dialogue n'accepte que des noms de domaine complets valides et correctement mis en forme.
        
        Vous pouvez entrer des caractères alphabétiques et numériques dans cette zone. Les adresses IPv4, IPv6 et les adresses avec un nom de domaine complet sont prises en charge. Si vous souhaitez utiliser l'authentification TLS (Transport Layer Security) mutuelle entre une passerelle IP de messagerie unifiée et un plan de numérotation fonctionnant en mode Sécurisé SIP ou en mode Sécurisé, vous devez configurer la passerelle IP de messagerie unifiée avec un nom de domaine complet. Vous devez également la configurer pour écouter le port 5061 et vérifier que les passerelles VoIP ou les PBX IP ont également été configurés pour écouter les demandes TLS mutuelles sur le port 5061. Pour configurer une passerelle IP de messagerie unifiée, exécutez la commande suivante : `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Si vous utilisez un nom de domaine complet, vous devez également vous assurer que vous avez correctement configuré un enregistrement d'hôte DNS pour la passerelle VoIP afin de résoudre correctement le nom d'hôte en adresse IP. De même, si vous utilisez un nom de domaine complet à la place d'une adresse IP et si la configuration DNS de la passerelle IP de messagerie unifiée est modifiée, vous devez désactiver la passerelle IP de messagerie unifiée, puis l'activer pour garantir une mise à jour correcte des informations de configuration de cette passerelle IP de messagerie unifiée.
    
      - **Plan de numérotation de messagerie unifiée**   Cliquez sur le bouton **Parcourir** pour sélectionner le plan de numérotation de messagerie unifiée que vous voulez associer à la passerelle IP de messagerie unifiée. Lorsque vous sélectionnez un plan de numérotation de messagerie unifiée à associer à une passerelle IP de messagerie unifiée, un groupement de postes de messagerie unifiée est également créé par défaut et associé au plan de numérotation de messagerie unifiée que vous avez sélectionné. Si vous ne sélectionnez pas de plan de numérotation de messagerie unifiée, vous devez créer manuellement un groupement de postes de messagerie unifiée, puis l'associer à la passerelle IP de messagerie unifiée que vous avez créée.

3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une passerelle IP de messagerie unifiée

Cet exemple crée une passerelle IP de messagerie unifiée intitulée `MyUMIPGateway` qui permet aux serveurs Exchange de démarrer des appels acceptés depuis une passerelle VoIP, un PBX à extension SIP, un PBX IP ou un contrôleur de frontière de session doté de l'adresse IP 10.10.10.1.

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

Cet exemple crée une passerelle IP de messagerie unifiée intitulée `MyUMIPGateway` qui permet aux serveurs Exchange de démarrer des appels acceptés depuis une passerelle VoIP, un PBX à extension SIP, un PBX IP ou un SBC avec pour nom de domaine complet MyUMIPGateway.contoso.com et écoute sur le port 5061.

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

Cet exemple crée une passerelle IP de messagerie unifiée intitulée `MyUMIPGateway`, empêche cette dernière d'accepter les appels entrants et d'effectuer des appels sortants, définit une adresse IPv6 et autorise la passerelle IP de messagerie unifiée à utiliser les adresses IPv4 et IPV6.

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

