---
title: 'Tester une règle de flux de messagerie: Exchange 2013 Help'
TOCTitle: Tester une règle de flux de messagerie
ms:assetid: 3d949e2a-8ba4-4261-8cfb-736fd2446ea1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn831862(v=EXCHG.150)
ms:contentKeyID: 63145422
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Tester une règle de flux de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Chaque fois que vous créez une règle de flux de messagerie Exchange (également appelée règle de transport), vous devez la tester avant de l’activer. Ainsi, si vous créez accidentellement une condition qui ne fait pas exactement ce que vous voulez ou qui interagit avec d’autres règles de manière inattendue, vous ne subirez aucune conséquence inattendue.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Patientez 30 minutes après la création d’une règle avant de la tester. Si vous testez la règle immédiatement après l’avoir créée, vous risquez d’obtenir un comportement incohérent. Si vous utilisez Exchange Server et plusieurs serveurs Exchange, cela peut durer encore plus longtemps pour que tous les serveurs reçoivent la règle.</td>
</tr>
</tbody>
</table>


## Étape 1 : Créer une règle en mode test

Vous pouvez évaluer les conditions d’une règle sans entreprendre aucune action ayant un impact sur le flux de messagerie en optant pour un mode test. Vous pouvez configurer une règle de manière à obtenir une notification électronique à chaque correspondance avec la règle ; vous pouvez consulter le Observer le suivi des messages pour les messages susceptibles de correspondre à la règle. Il existe deux modes test :

  - **Test sans conseils de stratégie**   Utilisez ce mode avec une action de rapport d’incident, pour recevoir un message électronique à chaque fois qu’un courrier électronique correspond à la règle.

  - **Test avec conseils de stratégie**   Ce mode est disponible uniquement si vous utilisez la [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) (DLP), disponible avec certains plans d’abonnement Exchange Online et Exchange Online Protection (EOP). Dans ce mode, un message est envoyé à l’expéditeur lorsqu’un message qu’il envoie correspond à une stratégie, mais aucune action de flux de messagerie n’est entreprise.

Voici ce que vous voyez lorsqu’une règle trouve une correspondance si vous incluez l’action de rapport d’incident :

![Message envoyé lorsque la règle est détectée](images/Dn831862.c1a2db60-3fb9-4ddc-86d5-1757e2250f59(EXCHG.150).png "Message envoyé lorsque la règle est détectée")

**Utiliser un mode test avec une action de rapport d’incident**

1.  Dans le Centre d’administration Exchange (CAE), accédez à **Flux de messagerie** \> **Règles**.

2.  Créez une règle ou sélectionnez une règle existante, puis sélectionnez **Modifier**.

3.  Faites défiler l’affichage jusqu’à la section **Choisir un mode pour cette règle** et sélectionnez **Test sans conseils de stratégie** ou **Test avec conseils de stratégie**.

4.  Ajoutez une action de rapport d’incident :
    
    1.  Sélectionnez **Ajouter une action** ou, si cette option n’est pas visible, sélectionnez **Autres options**, puis sélectionnez **Ajouter une action**.
    
    2.  Sélectionnez **Générer un rapport d’incident et l’envoyer à**.
    
    3.  Cliquez sur **Sélectionner…** pour vous choisir vous-même ou choisir quelqu’un d’autre.
    
    4.  Sélectionnez **Inclure les propriétés du message**, puis sélectionnez les propriétés de message que vous souhaitez inclure dans le message électronique que vous recevrez. Si vous ne sélectionnez aucune propriété, vous recevez quand même un message lorsque la règle trouve une correspondance.

5.  Cliquez sur **Enregistrer**.

## Étape 2 : Vérifier que votre règle agit comme vous le souhaitez

Pour tester une règle, vous pouvez envoyer plusieurs messages test pour confirmer que ce que vous attendez se produit, ou examiner le suivi des messages concernant les messages envoyés par des personnes de votre organisation. Veillez à évaluer les types de messages suivants :

  - Messages dont vous pensez qu’ils correspondent à la règle

  - Messages dont vous ne pensez pas qu’ils correspondent à la règle

  - Messages envoyés à et par des personnes de votre organisation

  - Messages envoyés à et par des personnes extérieures à votre organisation

  - Réponses à des messages correspondant à la règle

  - Messages pouvant causer des interactions entre plusieurs règles

## Conseils pour l’envoi de messages de test

Un moyen de test consiste à se connecter comme expéditeur et comme destinataire d’un message de test.

  - Si vous n’avez pas accès à plusieurs comptes dans votre organisation, vous pouvez faire le test dans un [compte d’évaluation Office 365](https://go.microsoft.com/fwlink/p/?linkid=402791) ou créer quelques utilisateurs factices temporaires au sein de votre organisation.

  - Comme un navigateur web ne vous permet généralement pas d’avoir plusieurs sessions ouvertes simultanément sur le même ordinateur en étant connecté à plusieurs comptes, vous pouvez utiliser la [navigation InPrivate d’Internet Explorer](https://go.microsoft.com/fwlink/p/?linkid=402784), ou un ordinateur, appareil ou navigateur web différent pour chaque utilisateur.

## Observer le suivi des messages

Le suivi des messages comprend une entrée pour chaque règle ayant une correspondance avec le message, et une entrée pour chaque action entreprise par la règle. C’est utile pour suivre le parcours des messages de test, mais également pour suivre ce qui se produit pour les vrais messages qui passent par votre organisation.

![Suivi des messages affichant les actions de règle de transport](images/Dn831862.64179f28-5c8c-421b-b630-cc1f7de9a34f(EXCHG.150).png "Suivi des messages affichant les actions de règle de transport")

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Suivi des messages**.

2.  Recherchez les messages que vous souhaitez suivre en utilisant des critères comme l’expéditeur et la date d’envoi. Pour obtenir de l’aide sur la spécification des critères, consultez la rubrique [Exécution d’un suivi de message et affichage des résultats](https://technet.microsoft.com/fr-fr/library/jj200712\(v=exchg.150\)).

3.  Après avoir localisé le message que vous souhaitez suivre, double-cliquez dessus pour afficher les détails du message.

4.  Dans la colonne **Événement**, recherchez l’option **Règle de transport**. La colonne **Action** indique l’action spécifique entreprise.

## Étape 3 : Une fois le test terminé, définir la règle à appliquer

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Règles**.

2.  Sélectionnez une règle, puis sélectionnez **Modifier**.

3.  Sélectionnez **Appliquer**.

4.  Si vous avez utilisé une action pour générer un rapport d’incident, sélectionnez l’action, puis sélectionnez **Supprimer**.

5.  Cliquez sur **Enregistrer**.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour éviter les surprises, informez vos utilisateurs des nouvelles règles.</td>
</tr>
</tbody>
</table>


## Suggestions de résolution des problèmes

Voici quelques problèmes courants et leurs solutions :

  - **Tout semble correct, mais la règle ne fonctionne pas.**
    
    Parfois, il faut plus de 15 minutes pour qu’une nouvelle règle de flux de messagerie soit disponible. Attendez quelques heures, puis testez-la à nouveau. Vérifiez également qu’aucune autre règle ne risque d’interférer avec la nouvelle règle. Essayez de passer cette règle en priorité 0 en la déplaçant vers le haut de la liste.

  - **Une clause d’exclusion de responsabilité est ajoutée au message d’origine et à toutes les réponses, à la place du message d’origine seul.**
    
    Pour éviter cela, vous pouvez ajouter une exception à votre règle de clause d’exclusion de responsabilité pour rechercher une expression unique dans la clause d’exclusion de responsabilité.

  - **Ma règle comporte deux conditions et je souhaite que l’action se produise lorsque l’une des conditions est remplie, mais elle ne trouve des correspondances que lorsque les deux conditions sont remplies.**
    
    Vous devez créer deux règles, une pour chaque condition. Vous pouvez facilement copier la règle en sélectionnant **Copier**, puis en supprimant l’une des conditions dans la règle d’origine et l’autre dans la copie.

  - **Je travaille avec des groupes de distribution et** **L’expéditeur est** (**SentTo**) **ne semble pas fonctionner.**
    
    **SentTo** trouve des correspondances avec des messages où l’un des destinataires est une boîte aux lettres, un utilisateur à extension messagerie ou un contact, mais vous ne pouvez pas indiquer un groupe de distribution avec cette condition. Utilisez plutôt **La zone À contient un membre de ce groupe** (**SentToMemberOf**).

## Autres options de test

Si vous utilisez Exchange Online ou Exchange Online Protection, vous pouvez vérifier le nombre de fois que chaque règle trouve une correspondance à l’aide d’un rapport de règles. Pour qu’une règle soit incluse dans les rapports, la case **Auditer cette règle avec le niveau de gravité** de cette règle doit être cochée. Ces rapports vous permettent d’identifier des tendances dans l’utilisation des règles et les règles qui n’ont aucune correspondance.

Pour afficher un rapport de règles, dans le Centre d’administration Office 365, sélectionnez **Rapports**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Alors que la plupart des données apparaissent dans le rapport dans les 24 heures, cela peut prendre 5 jours pour certaines données.</td>
</tr>
</tbody>
</table>


![Rapport présentant l’utilisation des règles](images/Dn831862.df5bf202-741d-432a-b71d-b37143f0ec0a(EXCHG.150).png "Rapport présentant l’utilisation des règles")

Pour en savoir plus, voir [Afficher les rapports de protection de courrier électronique](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Besoin d’aide supplémentaire ?

[Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md)

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Règles de flux de messagerie (règles de transport) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server)

