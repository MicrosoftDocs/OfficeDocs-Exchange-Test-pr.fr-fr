---
title: 'Procédure : nouveau modèle de stratégie de protection contre la perte de données (DLP)'
TOCTitle: Création d'une stratégie DLP à partir d'un modèle
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50477244
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création d'une stratégie DLP à partir d'un modèle

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-14_

Dans Microsoft Exchange Server 2013, vous pouvez utiliser des modèles de stratégie de protection contre la perte de données (DLP) pour mieux répondre aux besoins de conformité et de stratégie de messagerie de votre organisation. Ces modèles contiennent des ensembles de règles prégénérés qui peuvent vous aider à gérer les données des messages associées à plusieurs exigences légales et réglementaires communes. Pour voir une liste de tous les modèles fournis par Microsoft, consultez la rubrique [Modèles de stratégies DLP fournis dans Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Exemples de modèles DLP fournis pour vous aider à gérer :

  - Les données Gramm-Leach-Bliley Act (GLBA)

  - La norme Payment Card Industry Data Security Standard (PCI-DSS)

  - Les informations d'identification personnelle aux États-Unis (U.S. PII)

Vous pouvez personnaliser tous ces modèles DLP ou les utiliser tels quels. Les modèles de stratégie DLP reposent sur des règles de transport qui incluent de nouvelles conditions ou prédicats et des actions. Les stratégies DLP prennent en charge l'ensemble des règles de transport traditionnelles, auxquelles vous pouvez ajouter des règles supplémentaires après avoir établi une stratégie DLP. Pour plus d'informations sur les modèles de stratégie, consultez la rubrique [Modèles de stratégies de protection contre la perte de données (DLP)](dlp-policy-templates-exchange-2013-help.md). Pour plus d'informations sur les capacités des règles de transport, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) ou [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online). Une fois l’activation d’une stratégie démarrée, découvrez comment observer les résultats en passant en revue les rubriques suivantes :

Exchange 2013: [Afficher les rapports de détection de stratégies DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [Afficher les rapports de détection de stratégies DLP](https://technet.microsoft.com/fr-fr/library/dn904484\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez activer vos stratégies DLP en mode Test avant de les exécuter dans votre environnement de production. Au cours de ces tests, nous vous recommandons de configurer des boîtes aux lettres d'exemple d'utilisateur et d'envoyer des messages de test qui appellent vos stratégies de test afin de confirmer les résultats.</td>
</tr>
</tbody>
</table>


Pour d'autres tâches de gestion relatives à la création d'une stratégie DLP à partir d'un modèle, consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md)Exchange Server 2013 ou [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\))Exchange Online.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 30 minutes

  - Veillez à ce que Exchange 2013 soit configuré comme décrit dans [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Configurer les comptes administrateur et utilisateur dans votre organisation et valider le flux de messagerie de base.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le CAE pour configurer une stratégie DLP à partir d'un modèle

1.  Dans le Centre d'administration Exchange, accédez à **Gestion de la conformité**\>**Protection contre la perte de données**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").
    
    > [!NOTE]
    > Vous pouvez également sélectionner cette action en cliquant sur la flèche en regard de l'icône <strong>Ajouter</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /> et en sélectionnant <strong>Nouvelle stratégie DLP à partir d'un modèle</strong> dans le menu déroulant.


2.  Dans la page **Créer une nouvelle stratégie DLP à partir d'un modèle**, complétez les champs suivants :
    
    1.  **Nom**   Ajoutez un nom qui distinguera cette stratégie des autres.
    
    2.  **Description**   Ajoutez une description facultative qui résume cette stratégie.
    
    3.  **Choisir un modèle**   Sélectionnez le modèle approprié pour commencer à créer une stratégie.
    
    4.  **Plus d'options**   Sélectionnez le mode ou l'état. La nouvelle stratégie n'est pas activée tant que vous ne l'avez pas spécifié. Le mode par défaut d'une stratégie est test sans notifications.
    
    5.  Cliquez sur **Enregistrer** pour terminer la création de la stratégie.

> [!NOTE]
> Outre les règles dans un modèle spécifique, votre organisation peut avoir d'autres attentes ou stratégies d'entreprise qui s'appliquent aux données réglementées dans votre environnement de messagerie. Exchange 2013 facilite la modification du modèle de base afin d'ajouter des actions qui adaptent l'environnement de messagerie Exchange à vos besoins.


Pour adapter des stratégies, vous en modifiez les règles une fois que la stratégie a été enregistrée dans votre environnement Exchange 2013. Un exemple de changement de règle serait de désigner des personnes particulières exemptes d'une stratégie ou l'envoi d'un avis et le blocage de la remise d'un message s'il contient des informations sensibles. Pour plus d'informations sur la modification des stratégies et des règles, consultez la rubrique [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md).

Vous devez accéder à l’ensemble des règles de la stratégie en question sur la page **Modifier une stratégie DLP** et utiliser les outils disponibles sur cette page pour modifier une stratégie DLP que vous avez préalablement créée dans Exchange 2013.

Certaines stratégies permettent l'ajout de règles qui appellent RMS pour des messages. RMS doit être préalablement configuré sur votre serveur Exchange pour pouvoir ajouter des actions faisant appel à ce type de règles.

Pour toutes les stratégies DLP, vous pouvez modifier les règles, les actions, les exceptions, la période d'application ou l'application ou non d'autres règles dans la stratégie. Vous pouvez également ajouter vos propres conditions personnalisées pour chacune.

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Modèles de stratégies de protection contre la perte de données (DLP)](dlp-policy-templates-exchange-2013-help.md)

