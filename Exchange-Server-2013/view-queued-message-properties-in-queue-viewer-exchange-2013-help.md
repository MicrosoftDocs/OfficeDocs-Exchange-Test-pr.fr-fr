---
title: 'Affich. des propr. des msg en file d’attente dans l’afficheur des files d’att.'
TOCTitle: Affichage des propriétés des messages mis en file d’attente dans l’Afficheur des files d’attente
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 50478880
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# Affichage des propriétés des messages mis en file d’attente dans l’Afficheur des files d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-01-17_

Vous pouvez utiliser l'Afficheur des files d'attente de la Boîte à outils Exchange pour afficher les propriétés d'un message mis en file d'attente en vue de sa remise.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Files d'attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez également utiliser la cmdlet Get-Message dans l'environnement de ligne de commande Exchange Management Shell pour afficher d'autres propriétés du message qui ne figurent pas dans l'Afficheur des files d'attente. Pour plus d'informations, consultez les rubriques [Filtres de messages](message-filters-exchange-2013-help.md) et [Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que voulez-vous faire ?

## Utiliser l'Afficheur des files d'attente de la Boîte à outils Exchange pour afficher les propriétés d'un message

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Microsoft Exchange 2013** \> **Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, sélectionnez l'onglet **Messages** pour afficher la liste des messages qui sont actuellement en attente de remise au sein de votre organisation.

4.  Cliquez avec le bouton droit sur les propriétés que vous voulez afficher, puis cliquez sur **Propriétés**.

5.  L'onglet **Général** affiche les informations détaillées suivantes sur le message :
    
      - **Identité**   Ce champ affiche le nombre entier représentant un message particulier. L'identité de message est attribuée par la base de données des files d'attente lorsque le message est reçu pour traitement. Vous pouvez inclure une identité de serveur et de file d'attente facultative pour identifier une instance unique du message.
    
      - **Objet**   Ce champ affiche l'objet du message, exprimé comme une chaîne de texte. La valeur est extraite du champ d'en-tête `Subject:`.
    
      - **Identificateur du message Internet**   Ce champ affiche la valeur du champ d'en-tête `MessageID:`. La valeur de cette propriété est exprimée comme un GUID, suivi de l'adresse SMTP du serveur d'envoi, comme dans l'exemple suivant : 67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **À partir de l'adresse**   Ce champ affiche l'adresse SMTP de l'expéditeur du message. Cette valeur est tirée de MAIL FROM: dans l'enveloppe du message.
    
      - **État**   Ce champ affiche l'état actuel du message. Un message peut avoir l'une des valeurs d'état suivantes :
        
          - **Actif** Si le message figure dans une file d'attente de remise, il est remis à sa destination. Si le message se trouve dans la file d'attente de soumission, il est traité par le catégoriseur.
        
          - **Suppression en attente**   Le message a été supprimé par l'administrateur mais était déjà en cours de remise. Le message est supprimé si la remise se solde par une erreur ayant pour effet de réintroduire le message dans la file d'attente. Sinon, la remise continue.
        
          - **Suspension en attente**   Le message a été suspendu par l'administrateur mais était déjà en cours de remise. Le message est suspendu si la remise se solde par une erreur ayant pour effet de réintroduire le message dans la file d'attente. Sinon, la remise continue.
        
          - **Prêt** Le message se trouve dans la file d'attente, prêt à être traité.
        
          - **Nouvelle tentative**   La dernière tentative de connexion de la file d'attente dans laquelle se trouve le message a échoué. Le message attend la prochaine tentative de la file d'attente.
        
          - **Suspendu**   Le message a été suspendu par l'administrateur.
    
      - **Taille (Ko)**   Ce champ indique la taille du message arrondie au kilo-octet (Ko) le plus proche.
    
      - **Nom de la source du message**   Ce champ affiche le nom du composant ayant soumis ce message à la file d'attente.
    
      - **IP source**   Ce champ affiche l'adresse IP du serveur externe ayant soumis le message à l'organisation Exchange.
    
      - **Seuil de probabilité de courrier indésirable**   Ce champ affiche la valeur du seuil de probabilité de courrier indésirable du message. Les entrées de seuil de probabilité de courrier indésirable valides sont des entiers compris entre 0 et 9, ou -1. Une entrée de seuil de probabilité de courrier indésirable vide indique que le message n'a pas été traité par l'agent de filtrage de contenu.
    
      - **Date de réception**   Ce champ affiche l'horodateur indiquant le moment où le message a été reçu par le serveur sur lequel se trouve la file d'attente dans laquelle figure le message.
    
      - **Heure d'expiration**   Ce champ affiche l'horodateur indiquant le moment où le message expirera et sera supprimé de la file d'attente si le message ne peut pas être remis.
    
      - **Dernière erreur**   Ce champ affiche la dernière erreur enregistrée pour un message.
    
      - **Identificateur de file d'attente**   Ce champ affiche l'identité de la file d'attente dans laquelle figure le message. L'identité de file d'attente est exprimée sous la forme *Serveur\\destination*, où *destination* est un groupe de remise, une destination de routage, un nom de file d'attente persistante ou l'identificateur de la base de données des files d'attente. L'identificateur de la base de données des files d'attente est représenté par un nombre entier et il est possible de le déterminer en affichant les propriétés du message.
    
      - **Destinataires**   Ce champ affiche la liste des destinataires auxquels le message est destiné.
    
      - **Nombre de nouvelles tentatives**   Ce champ affiche le nombre de fois que la remise d'un message à une destination a été tentée.

6.  L'onglet **Informations sur le destinataire**affiche les informations détaillées suivantes sur les destinataires du message :
    
      - **Adresse**   Ce champ affiche l'adresse SMTP du destinataire du message. Cette valeur est extraite de `RCPT TO:` dans l'enveloppe du message.
    
      - **État**   Ce champ affiche l'état actuel du message. Les valeurs d'état d'un message peuvent être les suivantes :
        
          - **Actif** Si le message figure dans une file d'attente de remise, il est remis à sa destination. Si le message se trouve dans la file d'attente de soumission, il est traité par le catégoriseur.
        
          - **Suppression en attente**   Le message a été supprimé par l'administrateur mais était déjà en cours de remise. Le message est supprimé si la remise se solde par une erreur ayant pour effet de réintroduire le message dans la file d'attente. Sinon, la remise continue.
        
          - **Suspension en attente**   Le message a été suspendu par l'administrateur mais était déjà en cours de remise. Le message est suspendu si la remise se solde par une erreur ayant pour effet de réintroduire le message dans la file d'attente. Sinon, la remise continue.
        
          - **Prêt** Le message se trouve dans la file d'attente, prêt à être traité.
        
          - **Nouvelle tentative**   La dernière tentative de connexion de la file d'attente dans laquelle se trouve le message a échoué. Le message attend la prochaine tentative de la file d'attente.
        
          - **Suspendu**   Le message a été suspendu par l'administrateur.
    
      - **Dernière erreur**   Ce champ affiche la dernière erreur enregistrée pour un message.

## Utiliser le shell pour afficher les propriétés d'un message

La cmdlet **Get-Message** permet d'afficher les propriétés d'un message actuellement en attente de remise. L'exemple suivant tabule l'adresse de l'expéditeur, les destinataires, l'objet et la date de réception pour tous les messages actuellement en état de nouvelle tentative :

    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-Message](https://technet.microsoft.com/fr-fr/library/bb124738\(v=exchg.150\)).

