---
title: 'Créer une règle de protection de transport: Exchange 2013 Help'
TOCTitle: Créer une règle de protection de transport
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50477914
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une règle de protection de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez utiliser des règles de protection de transport pour appliquer une protection de droits permanente aux messages en fonction de leurs propriétés, telles que l’expéditeur, le destinataire, l’objet et le contenu du message.

> [!CAUTION]
> Avant de créer des règles de transport dans votre environnement de production, il est recommandé de les créer dans un environnement de test et de les tester de manière approfondie. Les règles de transport créées dans cette rubrique sont des exemples. Vous pouvez créer des règles de transport en utilisant les prédicats et valeurs de règles de transport appropriés en fonction de vos besoins.


Pour les autres tâches de gestion liées à la Gestion des droits relatifs à l’information (IRM), voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez - Entrée « Règles de transport » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un serveur exécutant les [services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/fr-fr/library/hh831364.aspx) doit être disponible dans votre organisation et contenir des modèles RMS existants.

  - Si vous configurez des règles de protection de transport pour protéger les messages à l’aide des droits relatifs à l’information (IRM) et que vous utilisez également la journalisation, pensez à activer le déchiffrement des rapports de journal pour permettre à l’agent de journalisation d’enregistrer une copie non chiffrée du message dans le rapport de journal. Pour en savoir plus, consultez la rubrique [Déchiffrement de l'état de journal](journal-report-decryption-exchange-2013-help.md).

  - Après avoir créé une règle de protection de transport, si elle ne peut pas être appliquée aux messages en raison d’un serveur AD RMS indisponible, les messages sont mis en attente par le service de transport sur les serveurs de boîtes aux lettres. Selon le volume de ces messages, de l’espace disque supplémentaire peut être occupé sur les serveurs de boîtes aux lettres. Exchange tente de protéger par IRM le message à trois reprises. Après ces tentatives, si le serveur AD RMS est injoignable ou si la protection IRM du message est impossible, une notification d’échec de remise est envoyée à l’expéditeur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer une règle de protection de transport

1.  Accédez à **Flux de messagerie** \> **Règles**.

2.  Dans la liste affichée, cliquez sur **Nouvelle**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **Nouvelle règle**, cliquez d’abord sur **Plus d’options**, puis renseignez les champs suivants :
    
      - **Nom**   Donnez un nom à la règle de transport.
    
      - **Appliquer cette règle si**   Sélectionnez une condition et entrez les valeurs requises pour celle-ci. Pour ajouter des conditions supplémentaires, cliquez sur **Ajouter une condition**.
        
        > [!IMPORTANT]
        > Si vous ne sélectionnez aucune condition lors de la création d’une règle de protection de transport, tous les messages traités par les serveurs Exchange 2013 avec le service de transport de votre organisation seront protégés par IRM. La protection IRM de tous les messages requiert plus de ressources. Par conséquent, nous vous recommandons de planifier votre serveur de messagerie et déploiement AD RMS en conséquence.
    
      - **Effectuez les opérations suivantes**   Sélectionnez **Appliquer la protection des droits au message avec**, puis sélectionnez un modèle à l’aide de la boîte de dialogue **Sélectionner un modèle RMS**.
    
      - **Sauf si**   (facultatif) Cliquez sur **Ajouter une exception** pour spécifier une exception à la règle.

4.  Cliquez sur **Enregistrer** pour créer la règle de transport.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une règle de protection de transport

  - Pour créer une règle de protection de transport, vous devez avoir des modèles RMS existants dans votre déploiement AD RMS. Cet exemple extrait les modèles disponibles à partir de votre cluster AD RMS.
    
    ```powershell
Get-RMSTemplate | format-list
```
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-RMSTemplate](https://technet.microsoft.com/fr-fr/library/dd297960\(v=exchg.150\)).

  - Cet exemple montre comment créer la règle de protection de transport Protect-BusinessCriticalProject. La règle confère une protection IRM aux messages contenant la phrase « Critique pour l’entreprise » dans le champ Objet avec le modèle **Ne pas transférer**.
    
    > [!NOTE]
    > Le prédicat <code>SubjectContainsWords</code> est utilisé dans cet exemple. Vous pouvez utiliser une combinaison quelconque de prédicats de règle de transport pour former les conditions et les exceptions de la règle. Pour plus d’informations sur les prédicats disponibles, consultez la rubrique <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Conditions de règles de transport (prédicats)</a>.
    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une règle de protection de transport, procédez comme suit :

  - Utilisez le CAE pour vérifier que la règle a été créée, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour consulter les propriétés de la règle.

  - Utilisez la cmdlet [Get-TransportRule](https://technet.microsoft.com/fr-fr/library/aa998585\(v=exchg.150\)) pour récupérer la règle. Pour obtenir un exemple de récupération d’une règle, consultez les [Examples](https://technet.microsoft.com/fr-fr/aa998585\(exchg.150\)#examples) dans **Get-TransportRule**.

  - Avec Outlook, Outlook Web App ou un périphérique mobile, envoyez un message de test qui remplit les conditions de la règle et vérifiez si le message reçu par le destinataire est protégé par IRM.

