---
title: "Supprimer une liste d'adresses: Exchange 2013 Help"
TOCTitle: Supprimer une liste d'adresses
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50477930
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Supprimer une liste d'adresses

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-14_

Cette rubrique décrit la suppression d’une liste d’adresses. Vous ne pouvez pas supprimer la liste d’adresses globale (GAL) par défaut.

Pour les autres tâches de gestion relatives aux listes d’adresses, consultez la rubrique [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez - Entrée « Liste d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas supprimer une liste d’adresses parent contenant des listes d’adresses enfant. Toutefois, vous pouvez supprimer les listes d’adresses parent et enfant en appuyant sur la touche CTRL du clavier et en sélectionnant les listes d’adresses concernées. Si vous essayez de supprimer une liste d’adresses parent sans supprimer les listes d’adresses enfant, vous recevez un message d’erreur.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour supprimer une liste d’adresses

1.  Accédez à **Organisation** \> **Listes d’adresses**.

2.  Dans la liste affichée, sélectionnez la liste d’adresses que vous souhaitez supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  À l’affichage de l’avertissement, cliquez sur **Oui** pour supprimer la liste d’adresses.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer une liste d’adresses

Cet exemple supprime la liste d’adresses Sales Department, qui ne contient pas de listes d’adresses enfant.

    Remove-AddressList -Identity "Sales Department"

Tapez **Y** pour confirmer la suppression de cette liste d’adresses, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-AddressList](https://technet.microsoft.com/fr-fr/library/bb124342\(v=exchg.150\)).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer une liste d’adresses contenant des listes d’adresses enfant

Cet exemple supprime la liste d’adresses parent Departments et toutes ses listes d’adresses enfant.

    Remove-AddressList -Identity Departments -Recursive

Tapez **Y** pour confirmer la suppression de la liste d’adresses parent et de ses listes d’adresses enfant, puis appuyez sur ENTRÉE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-AddressList](https://technet.microsoft.com/fr-fr/library/bb124342\(v=exchg.150\)).

