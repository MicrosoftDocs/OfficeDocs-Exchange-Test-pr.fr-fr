---
title: 'Config. un plan de num. pour des utilisateurs dont les noms sont similaires'
TOCTitle: Configuration d’un plan de numérotation pour des utilisateurs dont les noms sont similaires
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51407158
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration d’un plan de numérotation pour des utilisateurs dont les noms sont similaires

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Vous pouvez configurer un plan de numérotation de messagerie unifiée pour spécifier les informations fournis aux appelants quand les utilisateurs possèdent des noms identiques ou similaires. La messagerie unifiée utilise ce paramètre pour différencier les utilisateurs dont les noms sont identiques ou similaires et pour fournir ces informations aux appelants. Quand un appelant ou un utilisateur d'Outlook Voice Access est invité à entrer des lettres pour rechercher un utilisateur particulier, il arrive parfois que plus d'un nom corresponde à la saisie de l'appelant. Vous pouvez utiliser l'une des options disponibles pour fournir à un appelant davantage d'informations lui permettant de localiser l'utilisateur qu'il tente de contacter.

Vous pouvez définir ce paramètre à la fois sur des plans de numérotation de messagerie unifiée et des standards automatiques de messagerie unifiée. Quand un standard automatique de messagerie unifiée est créé, ce dernier hérite de ce paramètre du plan de numérotation associé au standard automatique. Par défaut, ce paramètre n'est pas configuré pour des plans de numérotation. Par conséquent, aucune information complémentaire n'est fournie aux appelants afin de les aider à trouver l'utilisateur recherché.

> [!NOTE]
> Pour que les informations incluses relatives aux utilisateurs dont les noms sont similaires fonctionnent correctement, vous devez indiquer les informations concernant le titre, le service et l'emplacement des destinataires au sein de votre organisation Microsoft Exchange.


Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) afin de configurer un plan de numérotation de messagerie unifiée pour des utilisateurs dont les noms sont similaires

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer** \> **Transfert et recherche**, puis sous **Informations à inclure pour les utilisateurs portant le même nom**, activez l'une des options suivantes :
    
      - **Titre**   Le plan de numérotation inclut le titre de chaque utilisateur quand il trouve deux ou plusieurs utilisateurs portant des noms similaires.
    
      - **Service**   Le plan de numérotation inclut le service de chaque utilisateur quand il trouve deux ou plusieurs utilisateurs portant des noms similaires.
    
      - **Emplacement**   Le plan de numérotation inclut l'emplacement de chaque utilisateur quand il trouve deux ou plusieurs utilisateurs portant des noms similaires.
    
      - **Aucun**   Le plan de numérotation n'inclut pas d'informations complémentaires quand des utilisateurs portent des noms similaires. Bien qu'il s'agisse du paramètre par défaut, nous vous recommandons d'inclure l'une des options disponibles pour les appelants. Dans le cas contraire, ces derniers ne pourront pas faire la différence entre deux ou plusieurs utilisateurs portant des noms similaires.
    
      - **Demander un alias**   Le plan de numérotation invite l'appelant à entrer l'alias de l'utilisateur. Un alias représente la partie de l'adresse de messagerie d'un utilisateur ou d'une adresse SMTP précédant l'arobase (@).

3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell afin de configurer un plan de numérotation de messagerie unifiée pour des utilisateurs portant des noms similaires

Cet exemple permet de définir les informations à inclure relatives aux utilisateurs portant des noms similaires qui vous sont demandées pour rechercher l'alias de l'utilisateur sur un plan de numérotation intitulé `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

Cet exemple permet de définir les informations à inclure relatives aux utilisateurs portant des noms similaires sur le service sur un plan de numérotation intitulé `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

Cet exemple permet de définir les informations à inclure relatives aux utilisateurs portant des noms similaires sur l'emplacement sur un plan de numérotation intitulé `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

