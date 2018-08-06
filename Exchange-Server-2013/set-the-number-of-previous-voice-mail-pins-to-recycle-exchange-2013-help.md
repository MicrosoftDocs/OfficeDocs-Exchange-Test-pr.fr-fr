---
title: 'Déf. nbre codes conf. de messag. voc. préc. à recycler : Exchange 2013 Help | Microsoft Docs'
TOCTitle: Définir le nombre de codes confidentiels recycler la messagerie vocale précédente
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50555461
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir le nombre de codes confidentiels recycler la messagerie vocale précédente

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Lorsque les utilisateurs d'Outlook Voice Access composent un numéro Outlook Voice Access, ils sont invités à entrer leur code confidentiel qui permet au système de messagerie vocale de les authentifier. Une fois authentifiés, ils peuvent accéder à la messagerie vocale, à la messagerie électronique, au calendrier et aux informations de contact personnelles de leur boîte aux lettres à partir de n'importe quel téléphone.

Une stratégie de boîte aux lettres de messagerie unifiée permet de configurer plusieurs paramètres relatifs au code confidentiel. Le paramètre **Nombre de recyclages du code confidentiel** indique le nombre de codes confidentiels uniques que des utilisateurs doivent utiliser avant de se servir à nouveau d'un ancien code confidentiel. Vous pouvez définir la valeur de ce paramètre entre 1 et 20. Pour la plupart des organisations, il convient de définir cette valeur sur 5 codes confidentiels, ce qui est la valeur par défaut. Un paramétrage trop élevé de cette valeur peut incommoder les utilisateurs car il peut être difficile de créer et de mémoriser plusieurs codes confidentiels. Un paramétrage trop faible peut introduire une menace de sécurité dans votre réseau.

> [!NOTE]
> Le nombre de recyclages du code confidentiel ne peut pas être désactivé.


Pour découvrir d'autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour modifier le nombre de recyclages du code confidentiel

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Stratégies de code confidentiel**, puis en regard de **Nombre de recyclages du code confidentiel**, entrez une valeur comprise entre 1 et 20.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le nombre de recyclages du code confidentiel

Cet exemple définit le nombre de recyclages du code confidentiel sur 10 dans la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

