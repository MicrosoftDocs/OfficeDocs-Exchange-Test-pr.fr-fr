---
title: 'Activation d’un message d’accueil personnalisé pour les utilisateurs d’OVA'
TOCTitle: Activation d’un message d’accueil personnalisé pour les utilisateurs d’Outlook Voice Access
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50555456
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation d’un message d’accueil personnalisé pour les utilisateurs d’Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Par défaut, chaque plan de numérotation de messagerie unifiée utilise un fichier .wav standard dédié au message d'accueil qui est lu aux appelants, y compris les utilisateurs d'Outlook Voice Access qui composent un numéro Outlook Voice Access qui a été configuré. Cependant, vous pouvez créer un fichier .wav ou .wma pour le message d'accueil, puis l'activer dans le plan de numérotation de messagerie unifiée.

Par exemple, vous souhaitez peut-être modifier le message d'accueil par défaut et fournir à la place un message d'accueil spécifique de votre entreprise, comme « Bienvenue dans Outlook Voice Access pour Woodgrove Bank ». Pour ce faire, enregistrez le message d'accueil personnalisé dans un fichier .wav. ou .wma. Configurez ensuite le plan de numérotation pour utiliser le message d'accueil personnalisé.

Pour plus d'informations sur les options de menu disponibles pour les utilisateurs d'Outlook Voice Access, consultez le guide de référence rapide pour Outlook Voice Access disponible dans le [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour activer un message d'accueil personnalisé

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l’affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Outlook Voice Access**, sous **Message d'accueil**, cliquez sur **Modifier**, puis cliquez sur **Parcourir** pour rechercher le fichier du message d'accueil.
    
    > [!Important]  
    > Le fichier que vous utilisez pour le message d'accueil doit être un fichier au format .wav ou .wma.


5.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer un message d'accueil personnalisé

Cet exemple active un message d'accueil qui utilise le fichier C:\\UMPrompts\\welcome.wav sur un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

