---
title: 'Suivre les messages avec des rapports de remise: Exchange 2013 Help'
TOCTitle: Suivre les messages avec des rapports de remise
ms:assetid: a14e4e62-08ca-4a7b-92e1-d39fe3e0a9e5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150554(v=EXCHG.150)
ms:contentKeyID: 50477294
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suivre les messages avec des rapports de remise

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-13_

La fonction Rapports de remise est un outil de suivi des messages du Centre d'administration Exchange qui permet d'obtenir l'état de remise de messages électroniques qui ont été envoyés ou reçus par des utilisateurs inclus dans le carnet d'adresses de votre organisation et qui se référaient à un objet donné. Vous pouvez suivre les informations de remise des messages envoyés ou reçus par une boîte aux lettres spécifique dans votre organisation. Le contenu relatif au corps du message n'est pas retourné dans un rapport de remise ; toutefois, la ligne d'objet est affichée dans les résultats. Vous pouvez suivre les messages jusqu'à 14 jours après leur envoi ou leur réception.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les rapports de remise suivent les messages envoyés par les utilisateurs à l'aide de Microsoft Outlook ou de clients de messagerie électronique Outlook Web App. Ils ne traitent pas les messages envoyés à partir de clients de messagerie POP ou IMAP tels que Windows Mail, Outlook Express ou Mozilla Thunderbird.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : La durée d'exécution variera en fonction de l'étendue de votre recherche.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Suivi de messages » à la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Que souhaitez-vous faire ?

Utiliser le Centre d'administration Exchange pour assurer le suivi des messages

Utiliser le Centre d'administration Exchange pour examiner un rapport de remise

## Utiliser le Centre d'administration Exchange pour assurer le suivi des messages

1.  Dans le Centre d'administration Exchange, accédez à **Flux de messagerie** \> **Rapports de remise**.

2.  Entrez les informations suivantes :
    
      - **\* Boîte aux lettres sur laquelle faire porter la recherche :** Cliquez sur **Parcourir** pour sélectionner la boîte aux lettres dans le carnet d'adresses, puis cliquez sur **OK**. La sélection de la boîte aux lettres sur laquelle faire porter la recherche est obligatoire.
    
      - Sélectionnez l'une des options suivantes :
        
          - **Rechercher les messages envoyés à   **Sélectionnez cette option pour rechercher les messages envoyés à des utilisateurs spécifiques. Cliquez sur **Sélectionner des utilisateurs**, choisissez des utilisateurs dans le carnet d'adresses, puis cliquez sur **Ajouter**. Vous pouvez sélectionner plusieurs utilisateurs. Lorsque vous avez terminé votre sélection, cliquez sur **OK** pour revenir à la page **Rapports de remise**. Si vous sélectionnez cette option, vous pouvez également laisser le champ vide pour rechercher les messages envoyés à tous les utilisateurs.
        
          - **Rechercher les messages reçus de   ** Utilisez cette option pour limiter votre recherche aux messages provenant d'un utilisateur spécifique. Là encore, sélectionnez l'utilisateur voulu dans le carnet d'adresses et cliquez sur **OK** pour revenir à la page **Rapports de remise**. Si vous sélectionnez cette option, vous devez spécifier un expéditeur.
    
      - **Rechercher ces termes dans la ligne d'objet   **Entrez les informations concernant la ligne d'objet ou laissez ce champ vide pour élargir la recherche.

3.  Lorsque vous avez terminé, cliquez sur **Rechercher**. Si vous voulez recommencer, cliquez sur **Effacer**.

## Utiliser le Centre d'administration Exchange pour examiner un rapport de remise

Pour afficher des informations de remise, sélectionnez un message dans le volet **Résultats de la recherche**, puis cliquez sur **Détails**.

Le rapport de remise affiche l'état de remise et les informations de remise détaillées du message que vous avez sélectionné dans le volet **Résultats de la recherche**. En haut du rapport, vous pouvez voir les champs suivants :

  - **Objet   **La ligne Objet du message s'affiche comme en-tête du rapport.

  - **De   **Alias, nom d'affichage ou adresse de messagerie de la personne qui a envoyé le message.

  - **À**   Alias, nom d'affichage ou adresse de messagerie de chaque destinataire du message.

  - **Envoyé   **Date et heure d'envoi du message.

## Section Résumé à ce jour

Cette section s'affiche dans le rapport de remise si un message a été envoyé à plusieurs personnes ou destinataires. Le haut de cette section vous indique le nombre total de destinataires auxquels le message a été envoyé et donne de brèves informations de remise pour chaque destinataire.

  - **Résumé à ce jour   **Affiche le nombre total de destinataires et indique s'il y a des messages dont l'état est En attente, Remis ou Échec. Cliquez sur les liens hypertexte pour effectuer un tri par état.

  - **Zone de recherche**   La zone de recherche est utile si vous avez envoyé le message à un groupe de plus de 30 destinataires. Dans la zone de recherche, tapez l'adresse de messagerie pour laquelle vous souhaitez obtenir les informations de remise et cliquez sur la loupe.

  - **À   **Indique l'adresse de messagerie du destinataire.

  - **État   **Cette colonne affiche l'état du message pour chaque destinataire.

## Informations détaillées du rapport

Cette section contient les informations de remise détaillées concernant un message envoyé au destinataire que vous sélectionnez dans la section Résumé à ce jour.

  - **Rapport de remise pour**   L'adresse de messagerie du destinataire sélectionné s'affiche ici.

  - **Envoyé**   Date et heure de soumission du message pour remise par le système.

Selon l'état de remise du message, vous pouvez voir divers messages d'état, notamment :

  - **Remis   **Indique une remise réussie.

  - **Différé   **Indique qu'un message est différé.

  - **En attente   **Si la remise du message est en attente parce qu'un message répond aux critères d'une règle ou d'une stratégie à l'échelle de l'organisation ou parce qu'il est soumis à approbation, le message d'état explique l'action exécutée par une règle ou indique que le message doit être approuvé par un modérateur avant la remise.

  - **Modérateur**   L'état indique si le message a été approuvé ou rejeté par le modérateur.

  - **Groupes développés   **Si un message a été envoyé à un groupe, les utilisateurs individuels sont affichés dans la section **Résumé à ce jour** afin que vous puissiez voir l'état de remise pour chaque destinataire. Si vous devez supprimer ou ajouter un utilisateur à un groupe pendant une recherche de rapport de remise, vous pouvez modifier le groupe en cliquant sur **Modifier les groupes**.

  - **Échec**   Affiche la date, l'heure et le motif de l'échec de remise d'un message. Par exemple, une règle à l'échelle de l'organisation peut bloquer la remise de messages ou le message n'a pas pu être remis.

Lorsque vous avez fini de consulter le rapport, cliquez sur **Fermer**. Les rapports de remise ne sont pas enregistrés, mais vous pouvez réexécuter un rapport à tout moment. Souvenez-vous qu'il y a une fenêtre de recherche sur deux semaines.

## Comment savoir si cela a fonctionné ?

Si votre recherche a réussi, les messages qui correspondent aux critères de recherche sont répertoriés dans le volet **Résultats de la recherche**. Pour afficher les informations de remise d'un message précis, sélectionnez-le et cliquez sur **Détails**. Si aucun message ne s'affiche dans le volet **Résultats de la recherche**, modifiez les critères de recherche et relancez la recherche.

