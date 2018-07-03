---
title: "Création d'une stratégie personnalisée de protection contre la perte de données (DLP): Exchange 2013 Help"
TOCTitle: Création d'une stratégie personnalisée de protection contre la perte de données (DLP)
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50477374
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d'une stratégie personnalisée de protection contre la perte de données (DLP)

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-03-18_

Une stratégie personnalisée de protection contre la perte de données (DLP) vous permet d'établir des conditions, règles et actions qui vous aident à répondre aux besoins spécifiques de votre organisation, et qui peuvent ne pas être traitées dans l'un des modèles DLP préexistants.

Les conditions de règle à votre disposition dans une stratégie unique incluent toutes les règles de transport traditionnelles en plus des types d'informations sensibles présentés dans [Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). Pour plus d'informations sur les règles de transport, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) ou [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez activer vos stratégies DLP en mode Test avant de les exécuter dans votre environnement de production. Au cours de ces tests, nous vous recommandons de configurer des boîtes aux lettres d'exemple d'utilisateur et d'envoyer des messages de test qui appellent vos stratégies de test afin de confirmer les résultats. Pour plus d'informations sur les tests, consultez <a href="test-a-mail-flow-rule-exchange-2013-help.md">Tester une règle de flux de messagerie</a>.</td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion liées à la création d'une stratégie DLP personnalisée, consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md)(Exchange 2013) ou [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\)) (Exchange Online).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 60 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour créer une stratégie DLP personnalisée, vous devez suivre les instructions d'installation d'Exchange 2013. Pour plus d'informations sur le déploiement, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!NOTE]
> En raison des variances des environnements des clients, les services de support technique Microsoft (CSS) ne peuvent pas participer au développement ou au test de scripts personnalisés d’expressions régulières (« scripts RegEx »). Pour le développement, le test et le débogage de scripts personnalisés RegEx, les clients Office 365 doivent s’appuyer sur des ressources informatiques internes. Par ailleurs, les clients Office 365 peuvent choisir d’utiliser une ressource de conseil externe, telle que les services de conseil Microsoft (MCS). Quelle que soit la ressource de développement de script, les ingénieurs de support technique CSS EXO et EOP ne sont pas disponibles pour aider les clients à résoudre des demandes relatives à des scripts RegEx personnalisés.


> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le CAE pour créer une stratégie DLP personnalisée sans règles existantes

1.  Dans le CAE, accédez à **Gestion de la conformité**\>**Protection contre la perte de données**. Toutes les stratégies existantes que vous avez configurées s'affichent dans une liste.

2.  Cliquez sur la flèche en regard de l'icône **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") et sélectionnez **Nouvelle stratégie personnalisée**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous cliquez sur l'icône <strong>Ajouter</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /> au lieu de cliquer sur la flèche, vous créerez une stratégie basée sur un modèle. Pour plus d'informations sur l'utilisation des modèles, consultez la rubrique <a href="how-to-new-dlp-data-loss-prevention-policy-template.md">Création d'une stratégie DLP à partir d'un modèle</a>.</td>
    </tr>
    </tbody>
    </table>


3.  Dans la page **Nouvelle stratégie personnalisée**, complétez les champs suivants :
    
    1.  **Nom**   Ajoutez un nom qui distinguera cette stratégie des autres.
    
    2.  **Description**   Ajoutez une description facultative qui résume cette stratégie.
    
    3.  **Choisir un état**   Sélectionnez le mode ou l'état de cette stratégie. La nouvelle stratégie n'est pas activée tant que vous ne l'avez pas spécifié. Le mode par défaut d'une stratégie est test sans notifications.

4.  Cliquez sur **Enregistrer** pour finir de créer les informations de référence de la stratégie. La stratégie est ajoutée à la liste de toutes les stratégies que vous avez configurées, bien qu'aucune règle ou action ne lui soit encore associée.

5.  Double-cliquez sur la stratégie que vous venez de créer ou sélectionnez-la et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

6.  Dans la page **Modifier la stratégie DLP**, cliquez sur **Règles**.
    
    Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une règle vierge. Vous pouvez établir des conditions à l'aide de toutes les règles de transport classiques en plus des types d'informations sensibles.
    
    Pour éviter toute confusion, attribuez un nom unique à chaque partie de votre stratégie ou règle quand vous avez la possibilité de fournir votre propre chaîne de caractères. Plusieurs options supplémentaires sont à votre disposition :
    
    1.  Cliquez sur la flèche en regard de l'icône **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une règle relative à une notification d'expéditeur ou permettant des remplacements.
    
    2.  Pour supprimer une règle, sélectionnez-la, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").
    
    3.  Cliquez sur **Plus d'options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") pour ajouter d'autres conditions et actions à cette règle, notamment des limites temporelles d'application et des effets sur d'autres règles de cette stratégie.

7.  Cliquez sur **Enregistrer** pour terminer la modification de la stratégie et enregistrez vos modifications.

Les modèles de stratégie DLP représentent un type de fonctionnalité Microsoft Exchange qui peut vous aider à concevoir et à appliquer un système solide de stratégies et de conformité pour votre environnement de messagerie. Pour plus d'informations sur les fonctionnalités de conformité, consultez la rubrique [Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) ou [Sécurité et conformité pour Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200706\(v=exchg.150\)).

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))Exchange Online

[Intégration des règles d'informations sensibles aux règles de transport](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

