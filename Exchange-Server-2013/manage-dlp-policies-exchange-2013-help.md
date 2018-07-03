---
title: 'Gestion de stratégies de protection contre la perte de données (DLP): Exchange 2013 Help'
TOCTitle: Gestion de stratégies de protection contre la perte de données (DLP)
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 50479066
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de stratégies de protection contre la perte de données (DLP)

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-14_

Vous pouvez afficher, modifier ou supprimer des stratégies de protection contre la perte de données (DLP) dans Microsoft Exchange, via le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell.

Pour découvrir d’autres tâches de gestion relatives à la protection contre la perte de données, consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) ou [Procédures relatives à la protection contre la perte de données (DLP)](https://technet.microsoft.com/fr-fr/library/jj938003\(v=exchg.150\)) (Exchange Online).

Pour plus d'informations sur l'environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 15 à 60 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour toute stratégie DLP, vous pouvez sélectionner l'un des trois modes :
    
      -    **Appliquer**   Les règles au sein de la stratégie sont évaluées pour l'ensemble des messages et des types de fichiers pris en charge. Le flux de messagerie peut être interrompu si des données remplissant les conditions de la stratégie sont détectées. Toutes les actions décrites au sein de la stratégie sont entreprises.
    
      -    **Tester la stratégie DLP avec des conseils de stratégie**   Les règles au sein de la stratégie sont évaluées pour l'ensemble des messages et des types de fichiers pris en charge. Le flux de messagerie ne sera pas interrompu si des données remplissant les conditions de la stratégie sont détectées. Autrement dit, les messages ne sont pas bloqués. Si des conseils de stratégie sont configurés, ils apparaissent aux utilisateurs.
    
      -    **Tester la stratégie DLP sans les conseils de stratégie**   Les règles au sein de la stratégie sont évaluées pour l'ensemble des messages et des types de fichiers pris en charge. Le flux de messagerie ne sera pas interrompu si des données remplissant les conditions de la stratégie sont détectées. Autrement dit, les messages ne sont pas bloqués. Si des conseils de stratégie sont configurés, ils ne sont pas visibles pour les utilisateurs.

  - Une règle individuelle au sein d'une stratégie DLP peut avoir ses propres paramètres de mode. Quand le mode d'une stratégie diffère du mode d'une règle au sein de cette stratégie, la configuration de la règle est prioritaire et sera évaluée conformément à son mode.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher les détails d'une stratégie DLP existante

Vous pouvez avoir besoin d'afficher les règles et actions d'une stratégie DLP existante que vous avez déjà établie pour votre organisation. Cette possibilité peut être utile en cas de problèmes de flux de messagerie inattendus ou si votre organisation modifie la manière dont les informations sensibles doivent être surveillées.

## Utiliser le CAE pour afficher les détails dans une stratégie DLP existante

1.  Dans le CAE, accédez à **Gestion de la conformité**\>**Protection contre la perte de données**.

2.  Double-cliquez sur l'une des stratégies qui apparaissent dans votre liste de stratégies ou mettez en surbrillance un élément et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Modifier la stratégie DLP**, cliquez sur **Règles**.

> [!TIP]
> Vous pouvez créer une stratégie DLP et la laisser en mode non activé ou désactivé. Dans ce mode, la stratégie concernée n'est pas appliquée et vous pouvez modifier tous les prédicats, actions et valeurs associés à ses règles avant de la tester et de commencer à l'appliquer.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les détails dans une stratégie DLP existante

Dans cet exemple, des informations sur la stratégie DLP fictive nommée Employee Numbers sont renvoyées. La commande est canalisée vers la commande **Format-List** pour afficher la configuration détaillée de la stratégie de transport spécifiée.

    Get-DlpPolicy "Employee Numbers" | Format-List

Pour obtenir des informations sur la syntaxe et les paramètres, consultez la rubrique [Get-DlpPolicy](https://technet.microsoft.com/fr-fr/library/jj215752\(v=exchg.150\)).

## Modifier une stratégie DLP

Vous pouvez modifier une stratégie DLP en modifiant son nom ou les règles qui régissent les effets de cette stratégie. Par exemple, vous pouvez ajouter un texte personnalisé de clause d'exclusion de responsabilité à un corps de message et une protection RMS pour les messages envoyés au sein d'un domaine spécifique et dont le contenu est détecté comme étant sensible. Si vous utilisez des modèles de stratégie DLP, n'oubliez pas que ces derniers ne représentent que l'une des fonctionnalités d'Exchange 2013 qui peuvent vous aider à concevoir et appliquer un système solide de stratégies et de conformité pour votre environnement de messagerie.

## Utiliser le CAE pour modifier une stratégie DLP existante

1.  Dans le CAE, accédez à **Gestion de la conformité**\>**Protection contre la perte de données**.

2.  Double-cliquez sur l'une des stratégies basées sur des modèles qui apparaissent dans votre liste de stratégies ou mettez en surbrillance un élément et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Modifier la stratégie DLP**, cliquez sur **Règles**.

4.  Pour modifier une règle existante, sélectionnez la règle et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Pour ajouter une règle vierge à personnaliser entièrement, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

6.  Pour ajouter une règle relative à une notification d'expéditeur, à un blocage de messages ou à une autorisation de remplacements, cliquez sur la flèche en regard de l'icône **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

7.  Pour supprimer une règle, sélectionnez-la, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

8.  Cliquez sur **Enregistrer** pour terminer la modification de la stratégie et enregistrez vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier une stratégie DLP existante

Vous pouvez préciser le niveau de notification et d'action d'une stratégie via l'environnement de ligne de commande Exchange Management Shell. Dans cet exemple, le mode d'une stratégie DLP fictive nommée Employee Numbers est défini pour que les actions ne soient pas appliquées et que les messages de notification ne s'affichent pas.

    Set-DlpPolicy "Employee Numbers" -Mode Audit

Pour obtenir des informations sur la syntaxe et les paramètres, consultez la rubrique [Set-DlpPolicy](https://technet.microsoft.com/fr-fr/library/jj215778\(v=exchg.150\)).

## Supprimer une stratégie DLP

Vous pouvez supprimer définitivement une stratégie DLP à l'aide du CAE. Une fois la stratégie supprimée, elle ne peut plus être appliquée et aucune de ses règles ou actions ne sera sauvegardée.

Vous pouvez aussi choisir de configurer le mode ou l'état opérationnel d'une stratégie sur **Tester la stratégie DLP sans les conseils de stratégie**. Ainsi, elle ne sera plus appliquée dans votre environnement de messagerie, mais les paramètres de configuration détaillés de la stratégie seront conservés. Cette option peut être utile si vous pensez éventuellement appliquer de nouveau la stratégie ultérieurement.

## Utiliser le CAE pour supprimer une stratégie DLP existante

1.  Dans le CAE, accédez à **Gestion de la conformité**\>**Protection contre la perte de données**.

2.  Sélectionnez la stratégie à supprimer dans votre liste de stratégies, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une stratégie DLP existante

Cet exemple décrit la suppression de la stratégie DLP fictive nommée Employee Numbers.

    Remove-DlpPolicy "Employee Numbers"

Pour obtenir des informations sur la syntaxe et les paramètres, consultez la rubrique [Remove-DlpPolicy](https://technet.microsoft.com/fr-fr/library/jj215677\(v=exchg.150\)).

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

