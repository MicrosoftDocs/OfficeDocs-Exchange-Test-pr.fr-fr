---
title: 'Durée de vie du code confidentiel pour la messag. voc.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Définir la durée de vie du code confidentiel pour la messagerie vocale
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50555496
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir la durée de vie du code confidentiel pour la messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Vous pouvez configurer la durée de vie du code confidentiel pour les utilisateurs à messagerie unifiée. La durée de vie du code confidentiel correspond au temps maximum pendant lequel un code confidentiel Outlook Voice Access reste valide pour vos destinataires à extension messagerie unifiée. Le paramètre de durée de vie du code confidentiel est configuré dans une stratégie de boîte aux lettres de messagerie unifiée et appliqué à tous les utilisateurs à messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée.

Plusieurs paramètres relatifs au code confidentiel peuvent être configurés dans une stratégie de boîte aux lettres de messagerie unifiée. Le paramètre de durée de vie du code confidentiel contrôle l'intervalle de temps, en jours, entre la date où les utilisateurs Outlook Voice Access ont modifié leur code confidentiel pour la dernière fois et la date où ils seront obligés de le modifier de nouveau. La plage s'étend de 0 à 999 et la valeur par défaut est de 60 jours. Si vous saisissez la valeur 0, le code confidentiel de l'utilisateur n'a pas de date d'expiration. Nous vous recommandons de ne pas définir ce paramètre à la valeur zéro (0), car vous risquez ainsi de diminuer considérablement la sécurité de votre réseau.

> [!NOTE]
> La messagerie unifiée n'informe pas les utilisateurs lorsque leur code confidentiel est sur le point d'expirer.


Pour découvrir d'autres tâches de gestion concernant la sécurité d'Outlook Voice Access par code confidentiel, consultez la rubrique [Procédures de sécurité de code confidentiel](pin-security-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer la durée de vie du code confidentiel

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie de boîte aux lettres de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Stratégies de code confidentiel**, puis en regard de **Appliquer la durée de vie du code confidentiel (jours)**, entrez une valeur comprise entre 0 et 999.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la durée de vie du code confidentiel

Cet exemple définit sur 30 le nombre de jours d'utilisation d'un code confidentiel pour les utilisateurs d'Outlook Voice Access associés à la stratégie de boîte aux lettres `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

Cet exemple définit les paramètres de code confidentiel suivants pour les utilisateurs d'Outlook Voice Access associés à la stratégie de boîte aux lettres de messagerie unifiée `MyUMMailboxPolicy` :

  - Le nombre d'échecs de connexion avant redéfinition du code confidentiel de l'utilisateur est rétabli à 3.

  - Définit le nombre maximal de tentatives de connexion sur 5.

  - La longueur minimale du code confidentiel est fixée à 9 chiffres.

  - Le code confidentiel est defini pour expirer dans 40 jours.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

