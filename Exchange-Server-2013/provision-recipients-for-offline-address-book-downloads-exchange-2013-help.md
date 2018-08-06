---
title: 'Configuration des desti. pour le téléchgmt du carnet d’adresses hors connexion | Microsoft Docs'
TOCTitle: Configuration des destinataires pour le téléchargement du carnet d’adresses en mode hors connexion
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50477652
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des destinataires pour le téléchargement du carnet d’adresses en mode hors connexion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-15_

Si vous utilisez plusieurs carnets d'adresses en mode hors connexion dans votre organisation, il existe plusieurs méthodes pour déterminer quels destinataires téléchargent quels carnets d'adresses en mode hors connexion :

  - **Par base de données de boîtes aux lettres**   Vous pouvez utiliser le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell pour permettre aux destinataires de télécharger des carnets d'adresses en mode hors connexion en liant une base de données de boîtes aux lettres à un carnet d'adresses en mode hors connexion pour des clients Office Outlook 2007, Outlook 2010 et Outlook 2013.

  - **Par destinataire**   Vous pouvez utiliser la cmdlet **Set-Mailbox** dans l'environnement de ligne de commande Exchange Management Shell pour spécifier quel carnet d'adresses en mode hors connexion est téléchargé en associant le carnet d'adresses en mode hors connexion directement à la boîte aux lettres du destinataire.

  - **Par plusieurs destinataires**  Vous pouvez utiliser une commande en pipeline dans l'environnement de ligne de commande Exchange Management Shell pour indiquer au carnet d'adresses en mode hors connexion que plusieurs destinataires effectuent le téléchargement selon des attributs communs.

  - **Stratégie de carnet d'adresses**   Vous pouvez attribuer une stratégie de carnet d'adresse (ABP) à un compte d'utilisateur de boîte aux lettres pour définir le carnet d'adresses hors connexion à télécharger vers la boîte aux lettres d'un destinataire. Si vous attribuez une ABP à un compte d'utilisateur auquel un carnet d'adresses en mode hors connexion a déjà été attribué, le carnet d'adresses en mode hors connexion explicitement attribué à la boîte aux lettres est prioritaire. Pour plus d'informations, consultez la rubrique [Attribuer une stratégie de carnet d’adresses à des utilisateurs de messagerie](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux carnets d'adresses en mode hors connexion, consultez la rubrique [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer ces procédures. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les destinataires pour les téléchargements de carnets d'adresses en mode hors connexion en associant leur base de données de boîtes aux lettres à une base de données de dossiers publics ou à un carnet d'adresses en mode hors connexion par défaut

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Bases de données de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

Cet exemple définit la distribution web de mon carnet d'adresses en mode hors connexion pour la base de données de boîtes aux lettres par défaut.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier quel carnet d'adresses en mode hors connexion sera téléchargé en associant le carnet d'adresses en mode hors connexion directement à la boîte aux lettres du destinataire

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

Pour spécifier quel carnet d'adresses en mode hors connexion est téléchargé en l'associant directement à la boîte aux lettres du destinataire, utilisez la syntaxe suivante.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>

> [!NOTE]
> Le paramètre <em>Identity</em> identifie la boîte aux lettres et peut prendre l'une des valeurs suivantes : GUID, ADObjectID, nom unique (DN), <em>domain\account</em>, nom d'utilisateur, LegacyExchangeDN, SmtpAddress et alias.


Cet exemple indique que l'utilisateur Rosalie téléchargera le carnet d'adresses en mode hors connexion nommé « mon carnet d'adresses en mode hors connexion ».

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier le carnet d'adresses en mode hors connexion qui sera téléchargé par plusieurs destinataires

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

Cet exemple indique que toutes les boîtes aux lettres d'utilisateurs aux États-Unis pour la société Contoso téléchargent le carnet d'adresses en mode hors connexion Contoso États-Unis.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-User](https://technet.microsoft.com/fr-fr/library/aa996896\(v=exchg.150\)) et [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

