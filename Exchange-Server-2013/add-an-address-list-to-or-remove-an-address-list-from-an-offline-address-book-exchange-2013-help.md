---
title: 'Ajout ou suppression d’une liste d’adresses de carnet en mode hors connexion'
TOCTitle: Ajout ou suppression d'une liste d'adresses à partir d'un carnet d'adresses en mode hors connexion
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50478609
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajout ou suppression d'une liste d'adresses à partir d'un carnet d'adresses en mode hors connexion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour ajouter ou supprimer une liste d'adresses dans un carnet d'adresses en mode hors connexion. Par défaut, il existe un carnet d'adresses en mode hors connexion appelé Carnet d'adresses en mode hors connexion par défaut, qui contient la liste d'adresses globale. Les carnets d'adresses en mode hors connexion sont générés sur la base des listes d'adresses qu'ils contiennent. Pour créer des carnets d'adresses en mode hors connexion personnalisés que les utilisateurs peuvent télécharger, vous pouvez ajouter ou supprimer des listes d'adresses dans les carnets d'adresses en mode hors connexion.

Pour les autres tâches de gestion relatives aux carnets d'adresses en mode hors connexion, consultez la rubrique [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Carnets d'adresses en mode hors connexion » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Les modifications apportées à la liste d'adresses ne sont pas accessibles pour un téléchargement client tant que le carnet d'adresses en mode hors connexion dans lequel réside la liste d'adresses n'a pas été généré. Pour plus d'informations, consultez la rubrique [Mettre à jour un carnet d’adresses en mode hors connexion](update-an-offline-address-book-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour ajouter une liste d'adresses à un carnet d'adresses en mode hors connexion

Lorsque le paramètre *AddressLists* est utilisé, les listes d'adresses existantes sont remplacées. Vous devez inclure les listes d'adresses existantes lorsque vous utilisez le paramètre *AddressLists* si vous voulez continuer à générer ces listes d'adresses dans votre carnet d'adresses en mode hors connexion. Dans cet exemple, AddressList3 est ajoutée à AddressList1 et AddressList2.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/aa996330\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une liste d'adresses d'un carnet d'adresses en mode hors connexion

Pour supprimer une liste d'adresses d'un carnet d'adresses en mode hors connexion, il suffit d'omettre cette liste d'adresses des listes d'adresses. Dans cet exemple, AddressList3 est soustraite à AddressList1 et AddressList2.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/aa996330\(v=exchg.150\)).

