---
title: 'Attribuer strat. de crnt d’adresses aux utlsr de messag.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Attribuer une stratégie de carnet d’adresses à des utilisateurs de messagerie
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50479085
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Attribuer une stratégie de carnet d’adresses à des utilisateurs de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-11_

Après avoir créé une stratégie de carnet d'adresses (ABP) vous devez l'affecter à des utilisateurs de boîtes aux lettres. Aucune stratégie de carnet d'adresses par défaut n'est affectée aux utilisateurs à la création de leur compte utilisateur. Si vous n'affectez pas de stratégie de carnet d'adresses à un utilisateur, ce dernier pourra accéder à la liste d'adresses globale (LAG) de toute votre organisation via Outlook et Outlook Web App. Pour en savoir plus, voir [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives aux stratégies de carnet d'adresses, consultez la rubrique [Procédures des stratégies de carnet d’adresses](address-book-policy-procedures-exchange-2013-help.md).

Les situations dans lesquelles cette procédure est utilisée vous intéressent ? Voir [Scénario : Déploiement de stratégies de carnet d’adresses](scenario-deploying-address-book-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies de carnet d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour affecter une stratégie de carnet d’adresses à un utilisateur de boîtes aux lettres

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans l’affichage liste, sélectionnez l’utilisateur auquel vous voulez attribuer la stratégie, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Dans la liste **Stratégie de carnet d’adresses**, sélectionnez la stratégie de carnet d’adresses à appliquer à cet utilisateur.

5.  Cliquez sur **Enregistrer**.

## Utiliser le CAE pour affecter une stratégie de carnet d’adresses à plusieurs utilisateurs de boîtes aux lettres

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans l’affichage liste, utilisez la touche Ctrl pour sélectionner plusieurs utilisateurs.

3.  Dans le volet d’informations, cliquez sur **Plus d’options**.

4.  Sous **Stratégie de carnet d’adresses**, cliquez sur **Mettre à jour**.

5.  Dans la liste **Sélectionner une stratégie de carnet d’adresses**, sélectionnez la stratégie de carnet d’adresses à appliquer à ces utilisateurs.

6.  Cliquez sur **Enregistrer**.

## Utilisation du Shell pour affecter une stratégie de carnet d'adresses à des utilisateurs de boîtes aux lettres

Dans cet exemple, stratégie de carnet d’adresses All Fabrikam est attribuée à l’utilisateur de boîte aux lettres existant joe@fabrikam.com.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

Dans cet exemple, la stratégie de carnet d’adresses ABP\_EngineeringDepartment est affectée à tous les utilisateurs de boîtes aux lettres dont la valeur `CustomAttribute11` contient « Département d’ingénierie ».

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) et [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

