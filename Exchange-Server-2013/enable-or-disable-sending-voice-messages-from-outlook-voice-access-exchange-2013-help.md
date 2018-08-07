---
title: 'Activer ou désactiver l’envoi de messages vocaux dans Outlook Voice Access'
TOCTitle: Activer ou désactiver l'envoi de messages vocaux à partir d'Outlook Voice Access
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52057089
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver l'envoi de messages vocaux à partir d'Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-12-13_

Vous pouvez autoriser les utilisateurs d'Outlook Voice Access à envoyer des messages vocaux à d'autres utilisateurs à extension messagerie unifiée associés au même plan de numérotation, ou au contraire les empêcher de le faire.

Par défaut, ce paramètre est activé. Si vous désactivez ce paramètre, les utilisateurs d'Outlook Voice Access qui composent un numéro Outlook Voice Access ne pourront plus envoyer de messages vocaux à des utilisateurs se trouvant dans le même plan de numérotation.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour permettre ou empêcher les utilisateurs d'Outlook Voice Access d'envoyer des messages vocaux à des utilisateurs se trouvant dans le même plan de numérotation

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Transfert et recherche**, sous **Autoriser les appelants à**, sélectionnez **Laisser des messages vocaux sans faire sonner le téléphone de l'utilisateur** pour autoriser l'envoi de messages vocaux. Désactivez ce paramètre si vous souhaitez empêcher l'envoi de messages vocaux pour des utilisateurs.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour permettre ou empêcher les utilisateurs d'Outlook Voice Access d'envoyer des messages vocaux à des utilisateurs se trouvant dans le même plan de numérotation

Cet exemple montre comment permettre aux utilisateurs d'Outlook Voice Access associés au plan de numérotation de messagerie unifiée `MyUMDialPlan` d'envoyer des messages vocaux à des utilisateurs associés au même plan de numérotation.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

Cet exemple montre comment empêcher les utilisateurs d'Outlook Voice Access associés au plan de numérotation de messagerie `MyUMDialPlan` d'envoyer des messages vocaux à des utilisateurs associés au même plan de numérotation.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

