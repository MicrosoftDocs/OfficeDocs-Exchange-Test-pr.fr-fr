---
title: 'Étudier la qlé audio des appels vocaux pr un utilisateur: Exchange 2013 Help'
TOCTitle: Étude de la qualité audio des appels vocaux pour un utilisateur
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50555343
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Étude de la qualité audio des appels vocaux pour un utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Si un utilisateur signale des problèmes de qualité audio au niveau de ses appels de messagerie unifiée, vous pouvez utiliser le rapport des journaux des appels des utilisateurs pour mieux comprendre l'origine des problèmes.

> [!NOTE]
> La qualité audio d'un appel peut être affectée par des facteurs qui ne sont pas couverts dans les rapports. Par exemple, si vos serveurs Exchange rencontrent une charge élevée de mémoire ou d'unité centrale, les utilisateurs peuvent signaler une qualité d'appel médiocre même si les rapports indiquent une qualité audio excellente.


Pour d'autres tâches relatives aux rapports de messagerie unifiée, consultez la rubrique [Procédures de rapports de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/um-reports-procedures)

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Données d'appel de messagerie unifiée et cmdlets de rapport de synthèse » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser le Centre d'administration Exchange (CAE) pour obtenir des journaux d'appels pour un utilisateur à extension messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Journaux des appels des utilisateurs**.

2.  Cliquez sur **Sélectionner un utilisateur**, puis sélectionnez l'utilisateur sur lequel vous souhaitez obtenir des données.

3.  Pour obtenir plus de détails sur la qualité audio pour une ligne du rapport, sélectionnez la ligne et cliquez sur **Détails de la qualité audio**. Les informations suivantes sont disponibles :
    
      - **DATE ET HEURE**   Date et heure de l'appel, dans le fuseau horaire que l'utilisateur sélectionné a défini dans Outlook Web App.
    
      - **UTILISATEUR**  Utilisateur sélectionné.
    
      - **PLAN DE NUMÉROTATION DE MESSAGERIE UNIFIÉE**   Plan de numérotation de l'appel.
    
      - **PASSERELLE IP DE MESSAGERIE UNIFIÉE**   Passerelle IP de messagerie unifiée qui a été utilisée pour l'appel.
    
      - **CODEC AUDIO**   Codec audio qui a été utilisé pendant un appel.
    
      - **NMOS**   Note moyenne d'opinion de réseau NMOS pour cet appel. Le score NMOS évalue la qualité audio de l'appel, sur une échelle de 1 à 5, 5 indiquant une excellente qualité.
        
        > [!NOTE]
        > Le score NMOS maximal possible pour un appel dépend du codec audio utilisé. Il est possible que le score NMOS ne soit pas disponible pour des appels très courts d'une durée inférieure à 10 secondes.
    
      - **DÉGRADATION NMOS**   Niveau de dégradation audio du score NMOS, à partir de la valeur la plus élevée possible pour le codec audio utilisé. Par exemple, si la valeur de dégradation NMOS d'un appel est égale à 1,2 et que le score NMOS signalé de l'appel est égal à 3,3, le score NMOS maximal de cet appel en particulier est de 4,5 (1,2 + 3,3).
    
      - **INSTABILITÉ**   Variation moyenne de l'arrivée des paquets de données pour un appel.
    
      - **PERTE DE PAQUETS**   Pourcentage moyen de la perte de paquets de données pour l'appel sélectionné. La perte de paquets est une indication de la fiabilité de la connexion.
    
      - **ALLER-RETOUR**   Durée moyenne d'aller-retour, en millisecondes, de l'audio pour l'appel sélectionné. Le score d'aller-retour mesure la latence de la connexion.
    
      - **DURÉE DE PERTE DE TRANSMISSION EN RAFALE**   Durée moyenne de perte de paquets pendant les rafales de pertes pour l'appel sélectionné.

