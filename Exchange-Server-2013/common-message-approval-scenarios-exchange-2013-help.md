---
title: 'Scénarios courants d’approbation des messages: Exchange 2013 Help'
TOCTitle: Scénarios courants d’approbation des messages
ms:assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298007(v=EXCHG.150)
ms:contentKeyID: 50478171
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Scénarios courants d’approbation des messages

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-09-29_

Votre organisation peut exiger que certains types de messages soient approuvés pour répondre aux exigences légales ou de conformité, ou pour mettre en œuvre un flux de travail d’entreprise spécifique. Voici quelques exemples de scénarios courants que vous pouvez configurer à l’aide d’Exchange :

  - Exemple 1 : Éviter les avalanches de messages dans un grand groupe de distribution

  - Exemple 2 : Transférer les messages vers le responsable d’un expéditeur pour approbation

  - Exemple 3 : Configurer une chaîne d’approbation des messages

  - Exemple 4 : Transférer les messages qui correspondent à l’un des critères

  - Exemple 5 : Transférer un message qui contient des informations sensibles

## Exemple 1 : Éviter les avalanches de messages dans un grand groupe de distribution

Pour contrôler les messages d’un grand groupe de distribution, vous pouvez exiger qu’un modérateur approuve les messages qui sont envoyés à ce groupe. S’il n’existe pas de critères pour définir les messages exigeant une approbation, la façon la plus simple de mettre ceci en place est de configurer le groupe de sorte qu’il exige une approbation des messages.

Dans cet exemple, tous les messages envoyés au groupe All Employees doivent être approuvés, sauf si les expéditeurs sont membres du groupe de distribution appelé Legal Team.

![Paramètres d’approbation de message pour un groupe de distribution](images/Dd298007.77721509-93f9-4a90-8d77-986db2b0acf4(EXCHG.150).png "Paramètres d’approbation de message pour un groupe de distribution")

Pour exiger que les messages envoyés à un groupe de distribution spécifique soient approuvés, dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Groupes**, modifiez le groupe de distribution, puis sélectionnez **Approbation des messages**.

## Exemple 2 : Transférer les messages vers le responsable d’un expéditeur pour approbation

Voici quelques types communs de messages pour lesquels vous pourriez vouloir exiger l’approbation du responsable :

  - Messages envoyés par un utilisateur à certains groupes de distribution ou destinataires

  - Messages envoyés à des utilisateurs externes ou à des partenaires

  - Messages envoyés entre deux groupes

  - Messages envoyés avec un contenu spécifique, comme le nom d’un client donné

  - Messages envoyés par un stagiaire

Pour exiger qu’un message soit envoyé pour approbation, créez d’abord une règle à l’aide du modèle **Envoyer des messages à un modérateur** et sélectionnez l’option indiquant que les messages doivent être dirigés vers le responsable de l’expéditeur, comme le montrent les captures d’écran suivantes.

![Utiliser un modèle pour créer une règle](images/Dd298007.051a5653-1a09-4db4-908f-48b56cc8d13f(EXCHG.150).png "Utiliser un modèle pour créer une règle")

Ensuite, définissez les messages qui doivent être approuvés.

Voici un exemple dans lequel tous les messages envoyés par un stagiaire, Garth Fort, à des destinataires n’appartenant pas à l’organisation exigent l’approbation du responsable.

![Règle qui transfère des messages au responsable de l’utilisateur](images/Dd298007.7f94c22e-b5ba-45a3-9ccd-31996b6c863a(EXCHG.150).png "Règle qui transfère des messages au responsable de l’utilisateur")

Pour commencer, accédez au CAE \> **Flux de messagerie** \> **Règles**, puis créez une règle à l’aide du modèle **Envoyer des messages à un modérateur**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Certaines conditions et actions, y compris le transfert vers le responsable de l’expéditeur, sont masquées par défaut sur la page <strong>Nouvelle règle</strong>. Pour voir toutes les conditions et actions, sélectionnez <strong>Plus d’options</strong>.</td>
</tr>
</tbody>
</table>


## Exemple 3 : Configurer une chaîne d’approbation des messages

Vous pouvez exiger plusieurs niveaux d’approbation pour les messages. Par exemple, vous pouvez exiger que les messages destinés à un client spécifique soient d’abord approuvés par un responsable de la relation client, puis par un responsable de la mise en conformité, ou vous pouvez exiger que les rapports de dépenses soient approuvés par deux niveaux de responsables.

Pour créer ce type d’approbation sur plusieurs niveaux, créez une règle de transport pour chaque niveau d’approbation. Chaque règle détecte les mêmes modèles dans les messages, comme suit :

  - La première règle transmet le message au premier approbateur. Lorsque le premier approbateur accepte le message, ce dernier est automatiquement transmis à l’approbateur dans la deuxième règle.

  - Si tous les approbateurs de la chaîne sélectionnent **Approuver** pour la demande d’approbation, lorsque la dernière approbation de la chaîne est effectuée, le message d’origine est envoyé aux destinataires souhaités.

  - Si une personne de la chaîne d’approbation sélectionne **Rejeter** lorsqu’elle reçoit la demande d’approbation, l’expéditeur reçoit un message de rejet.

  - Si aucune des demandes d’approbation n’est approuvée avant le délai d’expiration (2 jours pour Exchange Online, 5 jours pour Exchange Server 2013), l’expéditeur reçoit un message d’expiration.

L’exemple suivant suppose que vous avez un client appelé Blue Yonder Airlines et que vous voulez que le responsable de la relation client et le responsable de la mise en conformité approuvent tous les messages destinés à ce client. Vous créez deux règles, une pour chaque approbateur. La première règle est dirigée vers l’approbateur de premier niveau. La deuxième règle est dirigée vers l’approbateur de deuxième niveau.

![Deux règles utilisées pour deux niveaux d’approbation](images/Dd298007.29686c05-eaa0-42b9-86ad-d577f656392c(EXCHG.150).png "Deux règles utilisées pour deux niveaux d’approbation")

La première règle identifie tous les messages portant le nom de la société Blue Yonder Airlines dans l’objet ou le corps du message et envoie ces messages au responsable interne de la relation client de Blue Yonder Airlines, Garret Vargas.

![Règle pour un approbateur de premier niveau](images/Dd298007.e22d1c04-85c5-4227-88e6-b118d5593350(EXCHG.150).png "Règle pour un approbateur de premier niveau")

La deuxième règle envoie ces messages au responsable de la mise en conformité, Tony Krijnen.

![Règle d’approbation de deuxième niveau, avec les mêmes critères](images/Dd298007.5d888786-8e48-4459-ab86-8a4b9a016d58(EXCHG.150).png "Règle d’approbation de deuxième niveau, avec les mêmes critères")

## Exemple 4 : Transférer les messages qui correspondent à l’un des critères

Dans une règle de transport, toutes les conditions configurées dans la règle doivent être vérifiées pour que la règle corresponde. Si vous voulez que les mêmes actions s’appliquent à l’une des conditions, vous devez créer une règle distincte pour chacune d’elles.

Pour ce faire, sur la page **Règles** du CAE, créez une règle pour la première condition. Ensuite, sélectionnez la règle, sélectionnez **Copier**, puis modifiez les conditions de la nouvelle règle pour qu’elle corresponde à la deuxième condition.

Soyez prudent lorsque vous créez plusieurs règles avec des conditions « OR », pour ne pas finir par envoyer plusieurs fois un message à l’approbateur. Pour éviter cela, ajoutez une exception à la deuxième règle de sorte qu’elle ignore les messages qui correspondent à la première règle.

Par exemple, une règle unique ne peut pas vérifier si un message contient le terme « sales quote » dans l’objet ou dans le titre de la pièce jointe. Pour éviter que le message soit envoyé plusieurs fois à l’approbateur, si la première règle vérifie la présence de « sales quote » dans l’objet ou le corps du message, la deuxième règle qui vérifie la présence de « sales quote » dans le contenu de la pièce jointe a besoin d’une exception contenant les critères de la première règle.

![Utiliser une exception pour la deuxième règle](images/Dd298007.c39bbdcf-c619-4f84-8922-114ad1da824d(EXCHG.150).png "Utiliser une exception pour la deuxième règle")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les exceptions sont masquées par défaut sur la page <strong>Nouvelle règle</strong>. Pour voir toutes les conditions et actions, sélectionnez <strong>Plus d’options</strong>.</td>
</tr>
</tbody>
</table>


## Exemple 5 : Transférer un message qui contient des informations sensibles

Si vous disposez de la fonctionnalité de [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) (DLP), de nombreux types d’informations sensibles sont prédéfinis. Avec la DLP, vous voyez que le message contient une condition sur les informations sensibles. Que vous disposiez ou non de la DLP, vous pouvez créer des conditions qui identifient des modèles d’informations sensibles spécifiques propres à votre organisation.

Voici un exemple dans lequel les messages contenant des informations sensibles doivent être approuvés. Dans cet exemple, les messages qui contiennent un numéro de carte de crédit doivent être approuvés.

![Règle qui transfère les messages contenant des informations sensibles](images/Dd298007.7ec1ca74-5d20-42ea-a9ee-3a8b25beb7df(EXCHG.150).png "Règle qui transfère les messages contenant des informations sensibles")

## Voir aussi


[Gérer l’approbation des messages](manage-message-approval-exchange-2013-help.md)

