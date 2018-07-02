---
title: 'Configuration des dossiers publics dans une nouvelle organisation: Exchange 2013 Help'
TOCTitle: Configuration des dossiers publics dans une nouvelle organisation
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50478528
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des dossiers publics dans une nouvelle organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-11-09_

**Résumé** : Comment configurer des dossiers publics, y compris en leur attribuant des autorisations dans le Centre d’administration Exchange.

Cette rubrique explique comment configurer des dossiers publics et les exécuter dans une nouvelle organisation ou dans une organisation n'ayant jamais eu de dossiers publics auparavant.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour plus d’informations sur les limites et les quotas de stockage pour les dossiers publics, consultez les rubriques suivantes :
<ul>
<li><p>Pour les dossiers publics dans Office 365, voir <a href="https://go.microsoft.com/fwlink/?linkid=391188">Limites d’Exchange Online</a>.</p></li>
<li><p>Pour les dossiers publics dans Exchange Server 2013 sur site, voir <a href="limits-for-public-folders-exchange-2013-help.md">Limites pour les dossiers publics</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange Server 2013, consultez la rubrique [Procédures relatives aux dossiers publics](public-folder-procedures-exchange-2013-help.md).

Pour découvrir d'autres tâches de gestion associées aux dossiers publics dans Exchange Online, consultez la rubrique [Procédures de dossiers publics dans Office 365 et Exchange Online](https://technet.microsoft.com/fr-fr/library/jj966272\(v=exchg.150\)).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Dossiers publics » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

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


## Comment procéder ?

## Étape 1 : Créer la boîte aux lettres de dossiers publics principale

La boîte aux lettres de dossiers publics principale constitue la première boîte aux lettres de dossiers publics que vous créez pour votre organisation. Elle contient une copie accessible en écriture de la hiérarchie de dossiers publics. Les boîtes aux lettres de dossiers publics suivantes seront les boîtes secondaires, qui contiendront une copie en lecture seule de la hiérarchie et du contenu.

Pour obtenir la procédure détaillée, consultez la rubrique [Création d’une boîte aux lettres de dossiers publics](create-a-public-folder-mailbox-exchange-2013-help.md).

## Étape 2 : Créer votre premier dossier public

Pour obtenir la procédure détaillée, consultez la rubrique [Créer un dossier public](create-a-public-folder-exchange-2013-help.md).

## Étape 3 : Attribuer des autorisations au dossier public

Après avoir créé le dossier public, vous devez attribuer le niveau d’autorisation **Propriétaire** pour qu’au moins un utilisateur puisse accéder au dossier public à partir du client et créer des sous-dossiers. Tous les dossiers publics créés après celui-ci hériteront des autorisations du dossier public parent.

1.  Dans le Centre d'administration Exchange (CAE), accédez à **Dossiers publics** \> **Dossiers publics**.

2.  Dans l'affichage Liste, sélectionnez le dossier public.

3.  Dans le volet d'informations, sous **Autorisations du dossier**, cliquez sur **Gérer**.

4.  Dans **Autorisations des dossiers publics**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Cliquez sur **Parcourir** pour sélectionner un utilisateur.

6.  Dans la liste **Niveau d'autorisation**, sélectionnez un niveau. Au moins un utilisateur doit être **Propriétaire**.

7.  Cliquez sur **Enregistrer**.

8.  Vous pouvez ajouter plusieurs utilisateurs en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") et en attribuant les autorisations appropriées via la procédure ci-dessous. Vous pouvez aussi personnaliser le niveau d'autorisation en activant ou désactivant les cases à cocher. Lorsque vous modifiez un niveau d'autorisation prédéfini tel que **Propriétaire**, il devient **Personnalisé**.

Pour plus d'informations sur l'utilisation de l'environnement de ligne de commande Exchange Management Shell pour affecter des autorisations à un dossier public, consultez la rubrique [Add-PublicFolderClientPermission](https://technet.microsoft.com/fr-fr/library/bb124743\(v=exchg.150\)).

## Étape 4 (facultatif) : Attribuer une extension messagerie au dossier public

Si vous souhaitez que les utilisateurs envoient des messages électroniques vers le dossier public, vous pouvez lui attribuer une extension messagerie. Cette étape est facultative. Si vous n'activez pas la messagerie pour le dossier public, les utilisateurs peuvent publier des messages vers le dossier public en les faisant glisser vers celui-ci depuis Outlook.

1.  Dans le CAE, accédez à **Dossiers publics** \> **Dossiers publics**.

2.  Dans l'affichage Liste, sélectionnez le dossier public auquel vous souhaitez attribuer l'extension messagerie.

3.  Dans le volet d'informations, sous **Paramètres de la messagerie – Désactivé**, cliquez sur **Activer**.
    
    Un message d'avertissement s'affiche. Celui-ci vous invite à confirmer que vous souhaitez attribuer l'extension messagerie au dossier public. Cliquez sur **Oui**.

Le dossier public se voit attribuer l'extension messagerie et son nom devient l'alias du dossier public. Si plusieurs destinataires portent ce nom, un numéro est ajouté à l’alias du dossier public. Par exemple, si vous avez un groupe de distribution appelé SalesTeam et que vous créez un dossier public nommé SalesTeam, puis que vous l'activez, l'alias de ce dossier public sera SalesTeam1.

Pour plus d'informations sur l'utilisation de l'environnement de ligne de commande Exchange Management Shell pour activer la messagerie pour un dossier public,consultez la rubrique [Enable-MailPublicFolder](https://technet.microsoft.com/fr-fr/library/aa998824\(v=exchg.150\)).

