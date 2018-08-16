---
title: 'Config. un standard auto. pour les utilisateurs ayant des noms similaires'
TOCTitle: Configurer un standard automatique pour les utilisateurs ayant des noms similaires
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52057056
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer un standard automatique pour les utilisateurs ayant des noms similaires

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-16_

Vous pouvez configurer la méthode à utiliser pour les utilisateurs dotés de noms similaires dans les options **Accès au carnet d'adresses et à l'opérateur** du standard automatique, ou vous pouvez conserver le paramètre par défaut sur le standard automatique et configurer ce dernier sur le plan de numérotation associé au standard automatique. Par défaut, un standard automatique peut supprimer l'ambiguïté entre plusieurs utilisateurs ayant le même nom ou un nom similaire, car le paramètre par défaut sur le standard automatique est **Hériter du plan de commutation des appels**.

> [!NOTE]
> Pour que les informations incluses relatives aux utilisateurs dont les noms sont similaires fonctionnent correctement, vous devez indiquer les informations concernant le titre, le service et l'emplacement des destinataires au sein de votre organisation Microsoft Exchange.


Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) afin de configurer un standard automatique de messagerie unifiée pour des utilisateurs dont les noms sont similaires

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée**, cliquez sur **Accès au carnet d'adresses et à l'opérateur**, puis sous **Informations à inclure pour les utilisateurs portant le même nom**, activez l'une des options suivantes :
    
      - **Titre**   Le standard automatique inclut le titre de chaque utilisateur quand il affiche des correspondances.
    
      - **Service**   Le standard automatique inclut le service de chaque utilisateur quand il affiche des correspondances.
    
      - **Emplacement**   Le standard automatique inclut l'emplacement de chaque utilisateur quand il affiche des correspondances.
    
      - **Aucun**   Le standard automatique n'inclut aucune information supplémentaire quand il affiche des correspondances.
    
      - **Demander un alias**   Le standard automatique invite l'appelant à indiquer l'alias de l'utilisateur.
    
      - **Hériter du plan de commutation des appels**   Le standard automatique utilise le paramètre par défaut du plan de numérotation associé au standard automatique.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell afin de configurer un standard automatique de messagerie unifiée pour des utilisateurs dont les noms sont similaires

Cet exemple permet de définir les informations à inclure avec des utilisateurs portant des noms similaires sur Demander un alias pour un standard automatique de messagerie unifiée intitulé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

Cet exemple définit les informations à inclure avec des utilisateurs portant des noms similaires sur le titre des utilisateurs, active la recherche de noms et permet aux appelants qui téléphonent au standard automatique d'appuyer sur \* pour être présentés avec le message d'accueil Outlook Voice Access d'un standard automatique de messagerie unifiée intitulé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

