---
title: 'Créer une recherche dans le journal d’audit de la BAL: Exchange 2013 Help'
TOCTitle: Créer une recherche dans le journal d’audit de la boîte aux lettres
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50478026
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une recherche dans le journal d’audit de la boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-11_

Vous pouvez créer une recherche asynchrone des journaux d’audit d’une ou plusieurs boîtes aux lettres et demander l’envoi des résultats de la recherche par courrier électronique, sous forme de fichier XML, aux adresses désignées.

Pour effectuer une recherche dans les journaux d’audit d’une seule boîte aux lettres et afficher les résultats dans la fenêtre de l’environnement de ligne de commande Exchange Management Shell, voir [Rechercher une boîte aux lettres dans le journal d’audit de boîte aux lettres](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à l’enregistrement d’audit des boîtes aux lettres, voir [Procédures d'enregistrement d’audit des boîtes aux lettres](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Journaux d’audit de boîtes aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Par défaut, la fonctionnalité de journal d’audit de boîte aux lettres est désactivée pour toutes les boîtes aux lettres. Pour chaque boîte aux lettres à auditer, vous devez activer l’enregistrement d’audit et spécifier les actions du propriétaire de la boîte aux lettres, du délégué ou de l’administrer que vous voulez auditer. Pour plus d’informations, voir [Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le CAE pour rechercher l’accès du propriétaire dans des journaux d’audit de boîte aux lettres. La section d’audit du CAE comprend des rapports d’accès non-propriétaire à la boîte aux lettres et vous permet également de rechercher et d’exporter les événements d’accès non-propriétaire.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer une recherche de journaux d’audit de boîte aux lettres

1.  Accédez à **Gestion de la conformité** \> **Audit**.

2.  Dans la liste affichée, sélectionnez **Exporter les journaux d’audit de boîte aux lettres**.

3.  Dans **Exporter les journaux d’audit de boîte aux lettres**, renseignez les champs suivants, puis cliquez sur **Exporter** :
    
      - **Date de début**
    
      - **Date de fin**
    
      - **Rechercher dans ces boîtes aux lettres ou laisser vide pour rechercher toutes les boîtes aux lettres auxquelles des non-propriétaires ont accédé**
        
        > [!CAUTION]
        > Selon le nombre de boîtes aux lettres dans votre organisation et la quantité de données de journal d’audit de boîte aux lettres dans chacune, la recherche dans toutes les boîtes aux lettres peut prendre beaucoup de temps.
    
      - **Rechercher les accès par**
        
        Sélectionnez parmi les types suivants d’événements d’accès que vous souhaitez rechercher :
        
          - **Tous les non-propriétaires**
        
          - **Utilisateurs externes**
        
          - **Administrateurs et utilisateurs délégués**
        
          - **Administrateurs**
    
      - **Envoyer le rapport d’audit à**

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une recherche de journaux d’audit de boîtes aux lettres

Pour obtenir un exemple de procédure d’utilisation de l’environnement de ligne de commande Exchange Management Shell afin de créer une recherche de journal d’audit de boîte aux lettres, consultez l’[Example 1](https://technet.microsoft.com/fr-fr/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) dans **New-MailboxAuditLogSearch**.

