---
title: 'Gérer l’approbation des messages: Exchange 2013 Help'
TOCTitle: Gérer l’approbation des messages
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50477999
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer l’approbation des messages

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-05-04_

Parfois, il est logique d’avoir une deuxième opinion sur un message avant de le remettre. En tant qu’administrateur Exchange, vous pouvez configurer cela. Ce processus est appelé *modération* et l’approbateur est appelé *modérateur*. En fonction du type de message qui requiert une approbation, vous pouvez utiliser l’une des deux approches suivantes :

  - Modifier les propriétés de groupe de distribution

  - Créer une règle de flux de messagerie

Cet article vous donne les explications suivantes :

  - Comment déterminer l’approche d’approbation à utiliser

  - Fonctionnement du processus d’approbation

Pour découvrir comment mettre en œuvre les scénarios courants, voir [Scénarios courants d’approbation des messages](common-message-approval-scenarios-exchange-2013-help.md).

## Comment déterminer l’approche d’approbation à utiliser

Voici une comparaison des deux approches concernant l’approbation des messages.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Que souhaitez-vous faire ?</th>
<th>Approche</th>
<th>Première étape</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Créer un groupe de distribution modéré dans lequel tous les messages envoyés au groupe doivent être approuvés.</p></td>
<td><p>Configurer l’approbation des messages pour le groupe de distribution.</p></td>
<td><p>Accéder au Centre d’administration Exchange (CAE) &gt; <strong>Destinataires</strong> &gt; <strong> Groupes</strong>, modifiez le groupe de distribution, puis sélectionnez <strong>Approbation des messages</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Exiger une approbation pour les messages qui répondent à des critères spécifiques ou qui sont envoyés à une personne spécifique.</p></td>
<td><p>Créer une règle de transport à l’aide de l’action <strong>Transférer le message pour approbation</strong>.</p>
<p>Vous pouvez spécifier des critères de message, y compris des modèles de texte, des expéditeurs et des destinataires. Vos critères peuvent également contenir des exceptions.</p></td>
<td><p>Accéder au Centre d’administration Exchange (CAE) &gt; <strong>Flux de messagerie</strong> &gt; <strong>Règles</strong>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Fonctionnement du processus d’approbation

Lorsque quelqu’un envoie un message à une personne ou à un groupe exigeant une approbation et que cette personne utilise Outlook Web Access, elle est informée que la remise de son message sera peut-être différée.

![Message affichant une notification d’approbation de message](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "Message affichant une notification d’approbation de message")

Le modérateur reçoit un courrier électronique contenant une demande d’approbation ou de rejet du message. Le texte du message comprend des boutons pour approuver ou rejeter le message et la pièce jointe comporte le message d’origine à vérifier.

![Message de demande d’approbation, y compris les pièces jointes](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "Message de demande d’approbation, y compris les pièces jointes")

Le modérateur peut effectuer l’une des trois actions suivantes :

![Flux de travail affichant les options pour l’approbation d’un message](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "Flux de travail affichant les options pour l’approbation d’un message")

1.  S’il est approuvé, le message est remis aux destinataires auxquels il était originalement destiné. L’expéditeur d’origine ne reçoit pas de notification.

2.  Si le message est rejeté, un message de rejet est envoyé à l’expéditeur. Le modérateur peut ajouter une explication :
    
    ![Avis de refus, comportant les commentaires de modérateur](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "Avis de refus, comportant les commentaires de modérateur")  

3.  Si l’approbateur supprime ou ignore le message d’approbation, un message d’expiration est envoyé à l’expéditeur. Cela se produit au bout de deux jours dans Exchange Online et de cinq jours dans Exchange Server 2013. (Dans Exchange Server 2013, vous pouvez modifier ce délai).

Le message qui est en attente d’approbation est stocké temporairement dans une boîte aux lettres système appelée *boîte aux lettres d’arbitrage*. Jusqu’à ce que le modérateur décide d’approuver ou de rejeter le message, de supprimer le message d’approbation ou de le laisser expirer, le message d’origine est conservé dans la boîte aux lettres d’arbitrage.

Retour au début

## Questions et réponses

**Quelle est la différence entre l’approbateur et le propriétaire d’un groupe de distribution ?**

Le propriétaire d’un groupe de distribution est responsable de la gestion de l’appartenance au groupe, mais il peut ne pas être en mesure de modérer les messages qui sont envoyés au groupe. Par exemple, une personne travaillant dans le service informatique peut être propriétaire d’un groupe de distribution appelé Tous les employés, mais seul le directeur des ressources humaines peut être défini en tant que modérateur.

**Que se passe-t-il lorsqu’un modérateur ou un approbateur envoie un message au groupe de distribution ?**

Le message est directement envoyé au groupe, sans passer par le processus d’approbation.

**Que se passe-t-il lorsqu’un sous-ensemble de destinataires requiert une approbation ?**

Vous pouvez envoyer un message à un groupe de destinataires où seul un sous-ensemble de destinataires requiert une approbation. Prenons le cas d’un message envoyé à 12 destinataires, l’un d’entre eux étant un groupe de distribution modéré. Le message est automatiquement dupliqué. Un message est immédiatement remis aux 11 destinataires qui ne requièrent pas d’approbation et le second message est soumis au processus d’approbation pour le groupe de distribution modéré. Si un message est destiné à plus d’un destinataire modéré, une copie distincte du message est automatiquement créée pour chaque destinataire modéré et chaque copie est soumise au processus d’approbation approprié.

**Que faire si mon groupe de distribution contient des destinataires modérés qui requièrent une approbation ?**

Un groupe de distribution peut inclure des destinataires modérés qui requièrent également une approbation. Dans ce cas, une fois que le message destiné au groupe de distribution est approuvé, un autre processus d’approbation est utilisé pour chaque destinataire modéré membre du groupe de distribution. Toutefois, vous pouvez également activer l’approbation automatique des membres du groupe de distribution une fois que le message destiné au groupe de distribution modéré est approuvé. Pour ce faire, utilisez le paramètre *BypassNestedModerationEnabled* sur la cmdlet [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\)).

**Ce processus est-il différent si nous possédons nos propres serveurs Exchange ?**

Par défaut, une boîte aux lettres d’arbitrage est utilisée pour chaque organisation Exchange. Si vous possédez vos propres serveurs Exchange et que vous avez besoin de plus de boîtes aux lettres d’arbitrage pour l’équilibrage de charge, suivez les instructions relatives à l’ajout de boîtes aux lettres d’arbitrage dans [Gestion de l’approbation des messages et résolution des problèmes](manage-and-troubleshoot-message-approval-exchange-2013-help.md). Les boîtes aux lettres d’arbitrage sont des boîtes aux lettres système ne nécessitant pas de licence Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous disposez d’Exchange 2007 : Microsoft Exchange Server 2007 ne prend pas en charge les destinataires modérés. Si un message adressé à un groupe de distribution modéré est développé sur un serveur de transport Hub Exchange 2007, le message contourne la modération et est distribué à tous les membres du groupe de distribution. Si vous disposez de serveurs de transport Hub Exchange 2007 dans votre organisation Exchange, veillez à désigner un serveur de boîtes aux lettres Exchange Server 2013 en tant que serveur d’expansion pour les groupes de distribution modérés. Vous vous assurez ainsi que tous les messages envoyés au groupe de distribution sont modérés.</td>
</tr>
</tbody>
</table>


Retour au début

## Besoin d’informations supplémentaires ?

[Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md)

[Référence rapide concernant l’environnement de ligne de commande Exchange Management Shell pour Exchange 2013](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/fr-fr/library/jj200677\(v=exchg.150\))

