---
title: "Nbre d’échecs de connexion avant verrouillage d’un utilisateur de messag. voc. | Microsoft Docs"
TOCTitle: Définir le nombre d'échecs de connexion avant qu'un utilisateur de messagerie vocale est verrouillé
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50555435
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir le nombre d'échecs de connexion avant qu'un utilisateur de messagerie vocale est verrouillé

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez configurer le nombre d'échecs de connexion autorisé avant le verrouillage de la boîte aux lettres d'un utilisateur d'Outlook Voice Access. Le nombre d'échecs de connexion autorisé avant le verrouillage d'un utilisateur de messagerie vocale est configuré dans une stratégie de boîte aux lettres de messagerie unifiée et s'applique à tous les utilisateurs à extension messagerie unifiée qui y sont associés. Par défaut, cette valeur est définie sur 15.

Pour augmenter la sécurité, diminuez le nombre maximal de tentatives infructueuses. Toutefois, gardez à l'esprit que le fait de sélectionner un nombre largement inférieur à la valeur par défaut peut entraîner des verrouillages intempestifs pour les utilisateurs. La messagerie unifiée génère des événements d'avertissement qui peuvent être affichés à l'aide de l'observateur d'événements si l'authentification du code confidentiel échoue pour un utilisateur à extension messagerie unifiée ou si l'utilisateur ne parvient pas à se connecter au système. Ce paramètre doit être supérieur au nombre d'échecs de connexion avant la réinitialisation du code confidentiel.

Pour les autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer le nombre d'échecs de connexion précédant le verrouillage d'un utilisateur de messagerie vocale

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Stratégies de code confidentiel**, puis en regard de **Nombre d'échecs de connexion avant verrouillage**, entrez une valeur comprise entre 1 et 999.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le nombre d'échecs de connexion précédant le verrouillage d'un utilisateur de messagerie vocale

Dans cet exemple, le nombre maximal de tentatives de connexion est limité à 10 pour les utilisateurs à extension messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

Dans cet exemple, nous définissons le nombre d'échecs de connexion précédant la réinitialisation à 3 du code confidentiel d'un utilisateur d'Outlook Voice Access, le nombre maximal de tentatives de connexion à 5 et la longueur minimale du code confidentiel à 9 caractères pour les utilisateurs à extension messagerie unifiée qui sont associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

