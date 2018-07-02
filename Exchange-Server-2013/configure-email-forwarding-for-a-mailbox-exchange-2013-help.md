---
title: 'Configurer le transfert du courrier pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Configurer le transfert du courrier pour une boîte aux lettres
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50555489
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le transfert du courrier pour une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Le transfert du courrier vous permet de configurer une boîte aux lettres pour transférer les messages électroniques qu’elle reçoit vers la boîte aux lettres d’un autre utilisateur, appartenant ou non à votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez Office 365 pour les entreprises, vous devez configurer le transfert d’e-mail dans le <a href="https://go.microsoft.com/fwlink/p/?linkid=834774">Centre d’administration Office 365 : Configurer le transfert du courrier dans Office 365</a></td>
</tr>
</tbody>
</table>


Si votre organisation utilise un environnement Exchange local ou Exchange hybride, vous devez utiliser le Centre d’administration Exchange (CAE) local pour créer et gérer des boîtes aux lettres partagées.

## Utiliser le Centre d’administration Exchange pour configurer le transfert de messages

Vous pouvez utiliser leCentre d’administration Exchange (CAE) pour configurer le transfert du courrier électronique vers un seul destinataire interne, un seul destinataire externe (à l’aide d’un contact de messagerie) ou plusieurs destinataires (à l’aide d’un groupe de distribution).

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez ou appuyez sur la boîte aux lettres pour laquelle vous souhaitez configurer le transfert du courrier, puis cliquez ou appuyez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Flux de messagerie**, sélectionnez **Afficher les détails** pour afficher ou modifier les paramètres de transfert des messages électroniques.
    
    Cette page vous permet également de définir le nombre maximal de destinataires auquel l’utilisateur peut envoyer un message. Pour les organisations Exchange locales, il n’existe pas de limite de destinataire. Pour les organisations Exchange Online, la limite est de 500 destinataires.

5.  Cochez la case **Activer le transfert**, puis cliquez ou appuyez sur **Parcourir**.

6.  Sur la page **Sélectionner un destinataire**, choisissez l’utilisateur auquel vous voulez transférer l’intégralité du courrier électronique. Cochez la case **Envoyer le message à l’adresse de transfert et à la boîte aux lettres** si vous voulez que les messages électroniques envoyés soient copiés à la fois dans la boîte aux lettres du destinataire et la boîte aux lettres de transfert. Cliquez ou appuyez sur **OK**, puis cliquez ou appuyez sur **Enregistrer**.

Et si vous voulez transférer du courrier électronique à une adresse externe à votre organisation ? Ou transférer du courrier électronique à plusieurs destinataires ? Vous pouvez également le faire.

  - **Adresses externes** Créez un contact de messagerie, puis, dans les étapes ci-dessus, sélectionnez-le sur la page **Sélectionner un destinataire**. Vous ne savez pas créer un contact de messagerie ? Consultez la rubrique [Gérer les contacts de messagerie](manage-mail-contacts-exchange-2013-help.md).

  - **Plusieurs destinataires**Créez un groupe de distribution, ajoutez-y des destinataires, puis, dans les étapes ci-dessus, sélectionnez le contact de messagerie sur la page **Sélectionner un destinataire**. Vous ne savez pas créer un contact de messagerie ? Consultez la rubrique [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md).

## Comment savoir si cela a fonctionné ?

Pour vérifier que le transfert de messages a été correctement configuré, procédez de l’une des façons suivantes :

1.  Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres d’utilisateurs, cliquez ou appuyez sur la boîte aux lettres pour laquelle vous avez configuré le transfert de courrier électronique, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page de propriétés de boîte aux lettres, cliquez ou appuyez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Flux de messagerie**, cliquez ou appuyez sur **Afficher les détails** pour afficher les paramètres de transfert de messages.

## Informations supplémentaires

Cette rubrique est adressée aux administrateurs. Si vous voulez transférer votre propre courrier électronique à un autre destinataire, consultez les rubriques suivantes :

  - [Transférer du courrier vers un autre compte de messagerie](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [Gérer les courriers électroniques à l’aide de règles](https://go.microsoft.com/fwlink/p/?linkid=510869)

Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

