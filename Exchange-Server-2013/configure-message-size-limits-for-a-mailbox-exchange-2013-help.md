---
title: 'Configurer des limites de taille de messages pour une BAL: Exchange 2013 Help'
TOCTitle: Configurer des limites de taille de messages pour une boîte aux lettres
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50555498
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des limites de taille de messages pour une boîte aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-12_

Le Centre d’administration Exchange (EAC) et l’environnement de ligne de commande Exchange Management Shell vous permettent de configurer des limites de taille de messages pour une boîte aux lettres utilisateur. Ces limites permettent de contrôler la taille des messages qu’un utilisateur peut envoyer et recevoir. Par défaut, lorsqu’une boîte aux lettres est créée, aucun limite de tailles pour les messages envoyés ou reçus n’est définie.

Gardez à l'esprit que, dans une organisation Exchange, il existe d’autres paramètres qui permettent de déterminer la taille maximale de message qu’une boîte aux lettres peut envoyer et recevoir (par exemple, la taille maximale de message configurée sur un serveur de boîtes aux lettres). Pour en savoir plus sur les restrictions de taille de message dans Exchange, notamment les types de limites de tailles de messages, leur portée et l’ordre de priorité, voir [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

Pour connaître les tâches de gestion supplémentaires relatives aux boîtes aux utilisateur, consultez la rubrique [Gestion des boîtes aux lettres utilisateur](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).

> [!NOTE]
> Vous pouvez également contrôler la taille des messages envoyés et reçus par des utilisateurs de messagerie et provenant de boîtes aux lettres partagées.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour configurer des limites de taille de messages

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres pour laquelle vous souhaitez modifier les limites de taille de messages, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Restrictions de taille des messages**, cliquez sur **Afficher les détails** pour afficher et modifier les limites de taille de message suivantes :
    
      - **Messages envoyés**   Pour spécifier une taille maximale de messages envoyés par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l’utilisateur envoie un message dont la taille est supérieure à la taille spécifiée, il est renvoyé à l’utilisateur avec un message d’erreur descriptif.
    
      - **Messages reçus**   Pour spécifier une taille maximale de messages reçus par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l’utilisateur reçoit un message dont la taille est supérieure à la taille spécifiée, le message sera renvoyé à l’expéditeur accompagné d’un message de description de l’erreur.

5.  Cliquez sur **OK**, puis sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les tailles limites des messages

Dans cet exemple, nous établissons la taille maximale pour des messages envoyés à 25 Mo et la taille maximale pour des messages reçus à 35 Mo pour la boîte aux lettres de Debra Garcia.

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la configuration des limites de taille de messages a été correctement effectuée pour une boîte aux lettres, effectuez l’une des opérations suivantes :

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres pour laquelle vous voulez vérifier les limites de tailles de messages, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Restrictions de taille des messages**, cliquez sur **Afficher les détails** pour vérifier les limites de taille de messages pour la boîte aux lettres :

Ou

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

