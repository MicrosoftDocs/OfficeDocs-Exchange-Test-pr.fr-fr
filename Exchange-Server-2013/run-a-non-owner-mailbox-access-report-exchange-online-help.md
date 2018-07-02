---
title: 'Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires: Exchange 2013 Help'
TOCTitle: Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50477389
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires

 

_**Sapplique à :** Exchange Online_

_**Dernière rubrique modifiée :** 2016-12-09_

Le rapport d’accès aux boîtes aux lettres par des non-propriétaires dans le Centre d’administration Exchange répertorie les boîtes aux lettres auxquelles un individu autre que la personne qui possède la boîte aux lettres a accédé. Lorsqu’un non-propriétaire accède à une boîte aux lettres, Microsoft Exchange enregistre les informations à propos de cette action dans un journal d’audit de la boîte aux lettres stocké comme un message électronique dans un dossier caché dans la boîte aux lettres qui est auditée. Les entrées de ce journal sont affichées comme résultats de la recherche et incluent une liste de boîtes aux lettres auxquelles un non-propriétaire a accédé, qui a accédé à la boîte aux lettres et quand, les actions exécutées par le non-propriétaire et si l’action a réussi. Par défaut, les entrées du journal d’audit de boîtes aux lettres sont conservées pendant 90 jours.

Lorsque vous activez l’enregistrement d’audit de boîte aux lettres pour une boîte aux lettres, Microsoft Exchange enregistre des actions spécifiques effectuées par les non-propriétaires, notamment les administrateurs et les utilisateurs, les *utilisateurs délégués* appelés, qui se sont vus attribuer des autorisations pour une boîte aux lettres. Vous pouvez également limiter la recherche aux utilisateurs à l’intérieur ou à l’extérieur de votre organisation.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Journaux d’audit des boîtes aux lettres » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Activer l’enregistrement d’audit de boîte aux lettres

Vous devez activer l’enregistrement d’audit de boîte aux lettres pour chaque boîte aux lettres pour laquelle vous souhaitez exécuter un rapport d’accès aux boîtes aux lettres par un non-propriétaire. Si l’enregistrement d’audit de boîte aux lettres n’est pas activé, vous n’obtiendrez pas de résultats lorsque vous exécuterez un rapport.

Pour activer l’enregistrement d’audit de boîte aux lettres pour une boîte aux lettres unique, exécutez la commande suivante de l’environnement de ligne de commande Exchange Management Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Par exemple, pour activer l’audit de la boîte aux lettres pour un utilisateur nommé Florence Flipo, exécutez la commande suivante.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

Pour activer l’audit de boîte aux lettres pour toutes les boîtes aux lettres des utilisateurs de votre organisation, exécutez les commandes suivantes.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Comment savoir si cela a fonctionné ?

Exécutez la commande suivante pour vérifier que vous avez correctement configuré l’enregistrement d’audit des boîtes aux lettres.

    Get-Mailbox | FL Name,AuditEnabled

Une valeur de `True` pour la propriété *AuditEnabled* vérifie que la journalisation d'audit est activée.

Revenir au début

## Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Gestion de la conformité** \> **Audit**.

2.  Cliquez sur **Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires**.
    
    Par défaut, Microsoft Exchange exécute le rapport pour l’accès par des non-propriétaires à toutes les boîtes aux lettres de l’organisation au cours des deux dernières semaines. Les boîtes aux lettres répertoriées dans les résultats de la recherche ont été activées pour l’enregistrement d’audit de boîte aux lettres.

3.  Pour afficher l’accès par des non-propriétaires à une boîte aux lettres spécifique, sélectionnez la boîte aux lettres dans la liste de boîtes aux lettres. Consultez les résultats de la recherche dans le volet d’informations.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Souhaitez-vous affiner les résultats de la recherche ? Sélectionnez la date de début, la date de fin, ou les deux, et sélectionnez des boîtes aux lettres spécifiques dans lesquelles effectuer la recherche. Cliquez sur <strong>Rechercher</strong> pour réexécuter le rapport.</td>
</tr>
</tbody>
</table>


## Rechercher des types spécifiques d’accès non-propriétaire

Vous pouvez aussi spécifier le type d’accès non-propriétaire, également appelé le type d’ouverture de session, à rechercher. Voici vos options :

  - **Tous les non-propriétaires**   Recherchez les accès par les administrateurs et les utilisateurs délégués au sein de votre organisation. Cette option comprend également l’utilisateur d’accès qui ne fait pas partie de votre organisation.

  - **Utilisateurs externes**   Recherchez les accès par des utilisateurs qui ne font pas partie de votre organisation.

  - **Administrateurs et utilisateurs délégués**   Recherchez les accès par les administrateurs et les utilisateurs délégués au sein de votre organisation.

  - **Administrateurs**   Recherchez les accès par les administrateurs au sein de votre organisation.

Revenir au début

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien exécuté un rapport d’accès aux boîtes aux lettres par des non-propriétaires, vérifiez le volet des résultats de la recherche. Les boîtes aux lettres pour lesquelles vous avez exécuté le rapport s’affichent dans ce volet. Si aucun résultat ne s’affiche pour une boîte aux lettres spécifique, il est possible qu’aucun accès par un non-propriétaire ne se soit produit ou qu’aucun accès par un non-propriétaire n’ait eu lieu dans l’intervalle de dates spécifié. Comme précédemment décrit, assurez-vous de vérifier que l’enregistrement d’audit a été activé pour les boîtes aux lettres dont vous souhaitez vérifier l’accès par des non-propriétaires.

Revenir au début

## Qu’est-ce qui est enregistré dans le journal d’audit de boîte aux lettres ?

Lorsque vous exécutez un rapport d’accès aux boîtes aux lettres par des non-propriétaires, les entrées du journal d’audit de la boîte aux lettres sont affichées dans les résultats de la recherche du Centre d’administration Exchange. Chaque entrée de rapport contient ces informations :

  - Qui a accédé à la boîte aux lettres et quand

  - Actions exécutées par le non-propriétaire

  - Message affecté et l’emplacement de son dossier

  - Si l’action a réussi

Le tableau suivant répertorie les actions effectuées par des utilisateurs non propriétaires pouvant être consignées à l’aide de l’enregistrement d’audit des boîtes aux lettres. Dans le tableau, **Oui** indique que l’action peut être consignée pour ce type de connexion et **Non** indique qu’une action ne peut pas être consignée. Un astérisque (**\***) indique que l’action est consignée par défaut lorsque l’enregistrement d’audit est activé pour la boîte aux lettres. Si vous souhaitez suivre des actions qui ne sont pas consignées par défaut, vous devez utiliser PowerShell pour activer l’enregistrement de ces actions.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un administrateur disposant de l’autorisation Accès complet sur la boîte aux lettres d’un utilisateur est considéré comme un utilisateur délégué.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Description</th>
<th>Administrateur</th>
<th>Utilisateur délégué</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copy</strong></p></td>
<td><p>Un message a été copié dans un autre dossier.</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p><strong>Create</strong></p></td>
<td><p>Un élément est créé dans le dossier Calendrier, Contacts, Notes ou Tâches de la boîte aux lettres. Par exemple, une demande de réunion est créée. Notez que la création de message ou de dossier n’est pas auditée.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>Un dossier de boîte aux lettres a été accédé.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Suppression définitive</strong></p></td>
<td><p>Un message a été purgé du dossier Éléments récupérables.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>Un message a été affiché dans le volet de visualisation ou ouvert.</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p><strong>Déplacer</strong></p></td>
<td><p>Un message a été déplacé vers un autre dossier.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p><strong>Déplacer vers les éléments supprimés</strong></p></td>
<td><p>Un message a été déplacé vers le dossier Éléments supprimés.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Envoyer en tant que</strong></p></td>
<td><p>Un message a été envoyé à l’aide de l’autorisation SendAs. Cela signifie qu’un autre utilisateur a envoyé le message comme s’il provenait du propriétaire de la boîte aux lettres.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Envoyer de la part de</strong></p></td>
<td><p>Un message a été envoyé à l’aide de l’autorisation SendOnBehalf. Cela signifie qu’un autre utilisateur a envoyé le message de la part du propriétaire de la boîte aux lettres. Le message indiquera au destinataire de la part de qui le message a été envoyé et qui a envoyé réellement le message.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Soft-delete</strong></p></td>
<td><p>Un message a été supprimé du dossier Éléments supprimés.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Update</strong></p></td>
<td><p>Un message a été modifié.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>* Enregistré par défaut si l’enregistrement d’audit est activé pour une boîte aux lettres.</td>
</tr>
</tbody>
</table>


Revenir au début

