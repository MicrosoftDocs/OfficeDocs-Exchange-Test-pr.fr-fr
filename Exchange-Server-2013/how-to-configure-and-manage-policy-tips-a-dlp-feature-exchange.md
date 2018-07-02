---
title: 'Gérer les conseils de stratégie: Exchange 2013 Help'
TOCTitle: Gérer les conseils de stratégie
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 50477383
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les conseils de stratégie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les conseils de stratégie sont des notes d’information qui apparaissent lorsque vous composez un message électronique. L’objectif du conseil de stratégie est d’avertir les utilisateurs qu’ils sont peut-être en train de violer les pratiques ou les stratégies professionnelles que vous appliquez dans le cadre des stratégies de protection contre la perte de données (DLP) que vous avez définies. Les procédures suivantes vous aideront à commencer à utiliser les conseils de stratégie. Pour en savoir plus, regardez cette vidéo.

> [!VIDEO https://www.microsoft.com/fr-fr/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 30 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Les conseils de stratégie s'affichent uniquement aux expéditeurs de messages électroniques lorsque les conditions suivantes sont remplies :
    
    1.  Le programme client de messagerie de l’expéditeur est Microsoft  Outlook 2013. Si votre organisation a déployé Exchange 2013 SP1 ou utilise Exchange Online, des conseils de stratégie apparaissent également dans Outlook Web App et OWA pour les périphériques.
    
    2.  Il existe une règle de transport qui appelle des notifications de conseil de stratégie. Vous pouvez créer ce type de règle de transport en configurant une stratégie DLP qui inclut l'action **Avertir l'expéditeur à l'aide d'un conseil de stratégie**.
    
    3.  Le contenu d'un en-tête de message, d'un corps de message ou d'une pièce jointe analysé par votre agent de transport remplit les conditions définies au sein des stratégies DLP ou des règles qui incluent aussi les règles de notification de conseil de stratégie. Autrement dit, le conseil de stratégie s'affiche si les utilisateurs finaux agissent de façon à ce que la règle associée entreprenne l'action qui s'impose.

  - Le texte par défaut du conseil de stratégie s’affichera si vous ne modifiez pas les paramètres de conseils de stratégie pour le personnaliser. Pour plus d'informations sur la portée du destinataire, consultez la rubrique [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Créer ou modifier un conseil de stratégie en notification seule

Cette procédure permet d'afficher un conseil de stratégie à titre informatif à l'expéditeur d'un message lorsque les conditions d'une règle spécifique sont réunies. Dans Microsoft Outlook, l'expéditeur peut empêcher l'affichage de ce conseil en utilisant la boîte de dialogue d'options d'un conseil de stratégie. Pour configurer le texte personnalisé du conseil de stratégie, consultez la rubrique Créer un texte de notification de conseil de stratégie personnalisé.

## Utiliser le Centre d'administration Exchange (CAE) pour configurer des conseils de stratégie en notification seule

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Double-cliquez sur l’une des stratégies qui apparaissent dans votre liste de stratégies ou mettez en surbrillance un élément et sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Modifier la stratégie DLP**, sélectionnez **Règles**.

4.  Pour ajouter des conseils de stratégie à une règle existante, mettez la règle en surbrillance puis sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    Pour ajouter une nouvelle stratégie vierge que vous pouvez entièrement personnaliser, sélectionnez **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Créer une nouvelle règle**.

5.  Dans **Appliquer cette règle si**, sélectionnez, **Le message contient des informations sensibles**. Cette condition est obligatoire.

6.  Sélectionnez ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") puis les types d’informations sensibles, sélectionnez **Ajouter**, **OK** et enfin **OK**.

7.  Dans la zone **Procédez comme suit**, sélectionnez **Notifier l’expéditeur à l’aide d’un conseil concernant la stratégie** et sélectionnez une option dans la liste déroulante **Choisir de bloquer ou d’envoyer le message**, puis sélectionnez **OK**.

8.  Si vous voulez ajouter des conditions ou des actions supplémentaires, au bas de la fenêtre, sélectionnez **Plus d’options**.
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Seules les conditions suivantes peuvent être utilisées :
    <ul>
    <li><p><strong>SentTo (Le destinataire est)</strong></p></li>
    <li><p><strong>SentToScope (Le destinataire est situé)</strong></p></li>
    <li><p><strong>From (L’expéditeur est)</strong></p></li>
    <li><p><strong>FromMemberOf (L’expéditeur est membre de)</strong></p></li>
    <li><p><strong>FromScope (L’expéditeur est situé)</strong></p></li>
    </ul>
    Les actions suivantes ne peuvent pas être utilisées :
    <ul>
    <li><p><strong>RejectMessageReasonText (Rejeter le message et inclure une explication)</strong></p></li>
    <li><p><strong>RejectMessageEnhancedStatusCode (Rejeter le message avec le code d’état amélioré de)</strong></p></li>
    <li><p><strong>DeletedMessage (Supprimer le message sans avertir personne)</strong></p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


9.  Dans la liste **Choisir un mode pour cette règle**, indiquez si vous souhaitez que la règle soit appliquée. Nous vous recommandons de tester la règle d’abord.

10. Cliquez sur **Enregistrer** pour terminer la modification de la règle et enregistrer vos modifications.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un conseil de stratégie qui avertira uniquement un expéditeur, procédez comme suit :

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Sélectionnez la stratégie censée contenir le message de notification.

3.  Cliquez sur **Modifier**, puis cliquez sur ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier")**Règles**.

4.  Sélectionnez la règle spécifique censée contenir un message de notification.

5.  Confirmez que votre action **Informer l'expéditeur** s'affiche dans la partie inférieure du résumé des règles.

## Créer ou modifier un conseil de stratégie de message de bloc

Cette procédure entraîne l'affichage d'un conseil de stratégie indiquant le rejet d'un message et sa non-remise tant que la condition problématique existe. L'expéditeur a la possibilité d'indiquer que son message électronique ne contient pas la condition problématique. Il s'agit également d'un remplacement faux positif. Si l’expéditeur l’indique, le message peut quitter la boîte d’envoi et le rapport peut être analysé. Toutefois, Exchange bloquera l'envoi du message. Pour configurer le texte personnalisé du conseil de stratégie, consultez la rubrique Créer un texte de notification de conseil de stratégie personnalisé.

## Utiliser le Centre d'administration Exchange (CAE) pour configurer des conseils de stratégie de message de bloc

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Double-cliquez sur l’une des stratégies qui apparaissent dans votre liste de stratégies ou mettez en surbrillance un élément et sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Modifier la stratégie DLP**, sélectionnez **Règles**.

4.  Pour ajouter des conseils de stratégie à une règle existante, mettez la règle en surbrillance, puis sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Pour ajouter une nouvelle règle vierge entièrement personnalisable, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

6.  Pour ajouter une action qui divulguera un conseil de stratégie, cliquez sur **Plus d’options…**, puis sur le bouton **Ajoutez une action**.

7.  Dans la liste déroulante, sélectionnez **Avertir l'expéditeur à l'aide d'un conseil de stratégie**, puis **Bloquer le message**.

8.  Cliquez sur **OK**, puis cliquez sur **Enregistrer** pour terminer la modification de la règle et enregistrez vos modifications.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un conseil de stratégie de rejet de message, procédez comme suit :

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Cliquez une fois pour sélectionner la stratégie censée contenir un message de notification.

3.  Cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis cliquez sur **Règles**.

4.  Cliquez une fois pour sélectionner la règle censée contenir un message de notification.

5.  Vérifiez que l’action **Avertir l’expéditeur que le message ne peut pas être envoyé** apparaît dans la partie inférieure du résumé de la règle.

## Créer ou modifier un conseil de stratégie de blocage sauf remplacement

Il existe quatre options de conseils de stratégie permettant de rejeter des messages ou d’empêcher leur envoi à partir de la boîte d’envoi de l’expéditeur. Pour en savoir plus sur ces options, consultez la rubrique [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Utiliser le Centre d'administration Exchange (CAE) pour configurer des conseils de stratégie de blocage sauf remplacement

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Double-sélectionnez l’une des stratégies qui apparaissent dans votre liste de stratégies ou mettez en surbrillance un élément et sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **modifier la stratégie DLP**, sélectionnez **Règles**.

4.  Pour ajouter des conseils de stratégie à une règle existante, mettez la règle en surbrillance, puis sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    Pour ajouter une nouvelle règle vierge entièrement personnalisable, sélectionnez **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Plus d’options….**.

5.  Pour ajouter l’action qui révélera un conseil de stratégie, sélectionnez le bouton **Ajoutez une action**.

6.  Dans la liste déroulante, sélectionnez **Avertir l'expéditeur à l'aide d'un conseil de stratégie**, puis **Bloquer le message, mais autoriser l'expéditeur à le remplacer et à l'envoyer**.

7.  Cliquez sur **OK**, puis cliquez sur **Enregistrer** pour terminer la modification de la règle et enregistrez vos modifications.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un conseil de stratégie de rejet sauf remplacement, procédez comme suit :

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Cliquez une fois pour sélectionner la stratégie censée contenir un message de notification.

3.  Cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), puis cliquez sur **Règles**.

4.  Cliquez une fois pour sélectionner la règle censée contenir un message de notification.

5.  Confirmez que votre action **Bloquer le message, mais autoriser l'expéditeur à le remplacer et à l'envoyer** s'affiche dans la partie inférieure du résumé des règles.

## Créer un texte de notification de conseil de stratégie personnalisé

Cette procédure facultative vous aidera à personnaliser le texte de notification du conseil de stratégie que les expéditeurs de messages électroniques voient dans leur programme de messagerie. Si vous procédez ainsi, votre texte de notification de conseil de stratégie personnalisé ne s'affichera pas, sauf si vous configurez également une règle de stratégie DLP avec une action qui entraînera l'affichage de la notification. Souvenez-vous que des notifications de conseils de stratégie du système par défaut peuvent être affichées si vous ne personnalisez pas le texte de vos notifications. Pour plus d'informations sur la portée du destinataire, consultez la rubrique [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Utiliser le Centre d'administration Exchange (CAE) pour créer et gérer le texte de notification du conseil de stratégie personnalisé

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Sélectionnez **Paramètres de conseil de stratégie**![Paramètres Conseil de stratégie](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Paramètres Conseil de stratégie").

3.  Pour ajouter un nouveau conseil de stratégie avec votre propre message personnalisé, sélectionnez **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour plus d'informations sur les choix d'action disponibles, consultez la rubrique [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
    
    Pour modifier un conseil de stratégie existant, mettez le conseil en surbrillance et sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    Pour supprimer un conseil de stratégie existant, mettez-le en surbrillance, sélectionnez **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer") et confirmez.

4.  Sélectionnez **Enregistrer** pour terminer la modification du conseil de stratégie et enregistrer vos modifications.

5.  Sélectionnez **Fermer** pour terminer la gestion de vos conseils de stratégie et enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un texte de notification de conseil de stratégie personnalisé

L'exemple suivant crée un nouveau conseil de stratégie en langue anglaise qui bloquera l'envoi d'un message. Le texte de ce conseil de stratégie personnalisée est remplacé par la valeur : "This message appears to contain restricted content and will not be delivered."

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

Pour plus d'informations sur les cmdlets DLP, consultez la rubrique [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier un texte de notification de conseil de stratégie personnalisé

L'exemple suivant modifie un conseil de stratégie en langue anglaise existant en notification seule. Le texte de ce conseil de stratégie personnalisé est remplacé par « Sending bank account numbers in email is not recommended. »

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

Pour plus d'informations sur les cmdlets DLP, consultez la rubrique [Cmdlets de stratégie et de conformité](https://technet.microsoft.com/fr-fr/library/dd298082\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé un texte de conseil de stratégie personnalisé, procédez comme suit :

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Sélectionnez **Paramètres de conseil de stratégie**![Paramètres Conseil de stratégie](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Paramètres Conseil de stratégie").

3.  Sélectionnez **Actualiser**![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser").

4.  Vérifiez que votre action, les paramètres régionaux et le texte relatif à ces derniers s'affichent dans la liste.

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))Exchange Online

[Exchange 2010 MailTips](https://go.microsoft.com/fwlink/?linkid=265179)

