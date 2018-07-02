---
title: 'Création d’un carnet d’adresses en mode hors connexion: Exchange 2013 Help'
TOCTitle: Création d’un carnet d’adresses en mode hors connexion
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50479035
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: HT
---

# Création d’un carnet d’adresses en mode hors connexion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-24_

Dans Exchange Server 2013, un carnet d'adresses en mode hors connexion est une copie téléchargée d'un carnet d'adresses qui permet à un utilisateur Outlook d'accéder aux informations en étant déconnecté du serveur. Les administrateurs Exchange peuvent décider quels carnets d'adresses sont mis à la disposition des utilisateurs qui travaillent en mode hors connexion. Ils peuvent également configurer la manière dont les carnets d'adresses sont distribués (distribution web ou distribution de dossiers publics).

Pour les autres tâches de gestion relatives aux carnets d'adresses en mode hors connexion, consultez la rubrique [Procédures des carnets d’adresses en mode hors connexion](offline-address-book-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Carnets d'adresses en mode hors connexion » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Par défaut dans Exchange Online, le rôle de liste d’adresses n’est affecté à aucun groupe de rôles. Pour utiliser les cmdlets nécessitant le rôle Liste d’adresses, vous devez ajouter ce dernier à un groupe de rôles. Pour plus d’informations, consultez la section « Ajouter un rôle à un groupe de rôles » de la rubrique [Gérer des groupes de rôles](manage-role-groups-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un carnet d'adresses en mode hors connexion qui utilise la distribution web

Cet exemple crée le carnet d'adresses en mode hors connexion OAB\_Contoso qui utilise la distribution web pour les clients Outlook 2007 ou d'une version ultérieure en utilisant le répertoire virtuel par défaut.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-OfflineAddressBook](https://technet.microsoft.com/fr-fr/library/bb123692\(v=exchg.150\)).

