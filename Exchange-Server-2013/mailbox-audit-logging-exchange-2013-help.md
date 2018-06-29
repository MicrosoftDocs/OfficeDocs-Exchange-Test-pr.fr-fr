---
title: 'Enregistrement d’audit dans les boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Enregistrement d’audit dans les boîtes aux lettres
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50477707
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enregistrement d’audit dans les boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Les boîtes aux lettres étant susceptibles de renfermer des informations confidentielles, des informations ayant un impact significatif sur l’activité et des informations d’identification personnelle, il est important de connaître le nom des personnes qui se connectent aux boîtes aux lettres de votre organisation et les actions qui sont effectuées. Ceci est particulièrement important si les utilisateurs qui se connectent ne sont pas les propriétaires des boîtes aux lettres. Ces utilisateurs sont appelés *utilisateurs délégués*.

Grâce à l’*enregistrement d’audit des boîtes aux lettres*, vous pouvez enregistrer l’accès aux boîtes aux lettres par les propriétaires des boîtes aux lettres, les délégués (notamment les administrateurs disposant d’autorisations Accès total pour les boîtes aux lettres) et les administrateurs.

Lorsque vous activez l’enregistrement d’audit pour une boîte aux lettres, vous pouvez indiquer quelles actions de l’utilisateur (par exemple l’accès, le déplacement ou la suppression d’un message) doivent être enregistrées pour un type de connexion (administrateur, utilisateur délégué ou propriétaire). Les entrées du journal d’audit comprennent également des informations importantes, telles que l’adresse IP du client, le nom d’hôte et le processus ou client utilisé pour accéder à la boîte aux lettres. En ce qui concerne les éléments déplacés, l’entrée inclut le nom du dossier de destination.

## Journaux d’audit des boîtes aux lettres

Les journaux d’audit des boîtes aux lettres sont générés pour chaque boîte aux lettres pour laquelle l’enregistrement d’audit est activé. Les entrées de journal sont stockées dans le dossier Éléments récupérables dans la boîte aux lettres concernée, dans le sous-dossier Audits. Cela permet de s’assurer que toutes les entrées de journal d’audit sont disponibles dans un emplacement unique, quelle que soit la méthode d’accès au client utilisée pour accéder à la boîte aux lettres et quel que soit le serveur ou la station de travail utilisé par un administrateur pour accéder au journal d’audit de la boîte aux lettres. Si vous déplacez une boîte aux lettres vers un autre serveur, les journaux d’audit de cette boîte aux lettres sont également déplacés, car ils se trouvent dans la boîte aux lettres.

Par défaut, les entrées du journal d’audit des boîtes aux lettres sont conservées pendant 90 jours dans la boîte aux lettres, puis supprimées. Vous pouvez modifier cette période de rétention en utilisant le paramètre *AuditLogAgeLimit* avec la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)). Si une boîte aux lettres est en conservation inaltérable ou en conservation pour litige, les entrées du journal d’audit sont seulement conservées jusqu’à la fin de la période de rétention de journal d’audit de la boîte aux lettres. Pour conserver les entrées du journal d’audit plus longtemps, vous devez augmenter la période de rétention en modifiant la valeur du paramètre *AuditLogAgeLimit*. Vous pouvez également exporter les entrées du journal d’audit avant la fin de la période de rétention. Pour plus d'informations, consultez les rubriques suivantes :

  - [Exporter les journaux d’audit de boîte aux lettres](export-mailbox-audit-logs-exchange-2013-help.md)

  - [Créer une recherche dans le journal d’audit de la boîte aux lettres](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## Activation de l’enregistrement d’audit des boîtes aux lettres

L’enregistrement d’audit des boîtes aux lettres est activé pour chaque boîte aux lettres. Utilisez la cmdlet **Set-Mailbox** pour activer ou désactiver l’enregistrement d’audit des boîtes aux lettres. Pour plus d’informations, voir [Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

Lorsque vous activez l’enregistrement d’audit pour une boîte aux lettres, l’accès à la boîte aux lettres, ainsi que certaines actions réalisées par les administrateurs et les délégués, sont enregistrées par défaut. Pour enregistrer les actions effectuées par le propriétaire de la boîte aux lettres, vous devez indiquer quelles actions doivent être enregistrées.

## Actions consignées par l’enregistrement d’audit des boîtes aux lettres

Le tableau suivant répertorie les actions consignées par l’enregistrement d’audit des boîtes aux lettres et précise les types de connexion pour lesquels l’action est enregistrée.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Description</th>
<th>Administrateur</th>
<th>Délégué</th>
<th>Propriétaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Copier</p></td>
<td><p>Un élément est copié dans un autre dossier.</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Create</p></td>
<td><p>Un élément est créé dans le dossier Calendrier, Contacts, Notes ou Tâches de la boîte aux lettres. Par exemple, une demande de réunion est créée. Notez que la création de message ou de dossier n’est pas auditée.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>Un utilisateur accède à un dossier de boîte aux lettres.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui**</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>Un élément est définitivement supprimé du dossier Éléments récupérables.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>Un utilisateur accède à un élément dans le volet de lecture ou l’ouvre.</p></td>
<td><p>Oui</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>Déplacer</p></td>
<td><p>Un élément est déplacé vers un autre dossier.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>Un élément est déplacé vers le dossier Éléments supprimés.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>Un message est envoyé à l’aide des autorisations Envoyer en tant que.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>Un message est envoyé à l’aide des autorisations Envoyer de la part de.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>Un élément est supprimé du dossier Éléments supprimés.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Mettre à jour</p></td>
<td><p>Les propriétés d’un élément sont mises à jour.</p></td>
<td><p>Oui*</p></td>
<td><p>Oui*</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


\* Enregistré par défaut si l’enregistrement d’audit est activé pour une boîte aux lettres.

\*\* Les entrées correspondant aux actions de liaison des dossiers effectuées par des délégués sont consolidées. Une entrée de journal est générée pour chaque accès aux dossiers sur une période de 24 heures.

Si vous ne souhaitez plus que certains types d’actions liées aux boîtes aux lettres soient enregistrés, vous devez modifier la configuration d’enregistrement d’audit de la boîte aux lettres pour désactiver ces actions. Les entrées de journal existantes ne sont pas effacées tant que l’âge limite des entrées du journal d’audit n’est pas atteint.

## Recherche dans les entrées du journal d’audit des boîtes aux lettres

Vous pouvez faire appel aux méthodes suivantes pour effectuer une recherche dans les entrées du journal d’audit des boîtes aux lettres :

  - **Effectuer une recherche synchrone dans une seule boîte aux lettres**   Vous pouvez utiliser la cmdlet [Search-MailboxAuditLog](https://technet.microsoft.com/fr-fr/library/ff522360\(v=exchg.150\)) pour effectuer une recherche synchrone dans les entrées du journal d’audit d’une seule boîte aux lettres. La cmdlet affiche les résultats de la recherche dans la fenêtre Exchange Management Shell. Pour plus d'informations, consultez la rubrique [Rechercher une boîte aux lettres dans le journal d’audit de boîte aux lettres](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

  - **Effectuer une recherche asynchrone dans une ou plusieurs boîtes aux lettres**   Vous pouvez créer une recherche de journaux d’audit pour effectuer une recherche asynchrone dans les journaux d’audit d’une ou plusieurs boîtes aux lettres, puis faire en sorte que les résultats de la recherche soient envoyés à une adresse de messagerie spécifique. Les résultats de la recherche sont envoyés sous forme de pièce jointe au format XML. Pour créer la recherche, utilisez la cmdlet [New-MailboxAuditLogSearch](https://technet.microsoft.com/fr-fr/library/ff522362\(v=exchg.150\)). Pour plus d’informations, voir [Créer une recherche dans le journal d’audit de la boîte aux lettres](create-a-mailbox-audit-log-search-exchange-2013-help.md).

  - **Utiliser des rapports d’audit dans le Centre d’administration Exchange (CAE)**   Vous pouvez utiliser l’onglet **Audit** du CAE pour exécuter un rapport d’accès non propriétaire à la boîte aux lettres ou pour exporter les entrées du journal d’audit de la boîte aux lettres. Pour obtenir des informations détaillées, voir :
    
      - [Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [Exporter les journaux d’audit de boîte aux lettres](export-mailbox-audit-logs-exchange-2013-help.md)

## Entrées de journal d’audit de boîte aux lettres

Le tableau suivant décrit les champs enregistrés dans une entrée de journal d’audit de boîte aux lettres.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Champ</th>
<th>Renseigné avec</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>Une des actions suivantes :</p>
<ul>
<li><p>Copy</p></li>
<li><p>Create</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Move</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Update</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>Un des résultats suivants :</p>
<ul>
<li><p>Échec</p></li>
<li><p>Réussite partielle</p></li>
<li><p>Réussite</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>Type de connexion de l’utilisateur qui a réalisé l’opération. Les types de connexion sont les suivants :</p>
<ul>
<li><p>Propriétaire</p></li>
<li><p>Délégué</p></li>
<li><p>Administrateur</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>GUID du dossier de destination pour les opérations de déplacement.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>Chemin d’accès au dossier de destination pour les opérations de déplacement.</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>GUID du dossier.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>Chemin d’accès au dossier.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>Détails permettant d’identifier le client ou le composant Exchange qui a effectué l’opération.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>Adresse IP de l’ordinateur client.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>Nom de l’ordinateur client.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>Nom du processus de l’application cliente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>Version de l’application cliente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>Type de connexion de l’utilisateur qui a réalisé l’opération. Les types de connexion sont les suivants :</p>
<ul>
<li><p>Propriétaire</p></li>
<li><p>Délégué</p></li>
<li><p>Administrateur</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>Nom d’utilisateur principal (UPN) du propriétaire de la boîte aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>Identificateur de sécurité (SID) du propriétaire de la boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>UPN du propriétaire de la boîte aux lettres de destination, connecté pour des opérations sur plusieurs boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>SID du propriétaire de la boîte aux lettres de destination, connecté pour des opérations sur plusieurs boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>GUID du propriétaire de la boîte aux lettres de destination.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>Informations permettant de savoir si l’opération enregistrée porte sur plusieurs boîtes aux lettres (par exemple, la copie ou le déplacement de messages entre plusieurs boîtes aux lettres).</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>Nom complet de l’utilisateur qui est connecté.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>Nom complet de l’utilisateur délégué.</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>SID de l’utilisateur qui est connecté.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>Identificateur des éléments de boîtes aux lettres sur lesquels l’action enregistrée est réalisée (par exemple, un déplacement ou une suppression). Pour les opérations effectuées sur plusieurs éléments, ce champ est retourné sous forme d’une série d’éléments.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>GUID du dossier source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>Identificateur de l’élément.</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>Objet de l’élément.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>GUID de la boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>Nom résolu de l’utilisateur de la boîte aux lettres, au format <em>DOMAINE</em>\<em>SamAccountName</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>Heure à laquelle l’opération a été effectuée.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>ID d’entrée du journal d’audit.</p></td>
</tr>
</tbody>
</table>


## Plus d’informations

  - **Accès administrateur aux boîtes aux lettres**   On considère qu’un administrateur peut accéder à une boîte aux lettres uniquement dans les situations suivantes :
    
      - La [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) est utilisée pour effectuer une recherche dans une boîte aux lettres.
    
      - La cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/fr-fr/library/ff607299\(v=exchg.150\)) est utilisée pour exporter une boîte aux lettres.
    
      - [Éditeur MAPI Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=204086) sert à accéder à la boîte aux lettres.

  - **Contournement de l’enregistrement d’audit des boîtes aux lettres**   L’accès aux boîtes aux lettres par des processus automatisés autorisés, tels que les comptes utilisés par des outils tiers ou à des fins de surveillance licite, peut entraîner la création d’un grand nombre d’entrées de journal d’audit de boîte aux lettres et s’avérer sans intérêt pour votre organisation. Vous pouvez faire en sorte que l’enregistrement d’audit ne s’effectue pas dans les boîtes aux lettres de ces comptes. Pour plus d’informations, voir [Contournement d'un compte d'utilisateur lors de la journalisation d'audit des boîtes aux lettres](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md).

  - **Enregistrement des actions des propriétaires de boîte aux lettres**   Pour les boîtes aux lettres, telles que la boîte aux lettres de détection, qui peuvent contenir des informations dont le niveau de confidentialité est plus élevé, il est conseillé d’activer l’enregistrement d’audit pour les actions réalisées par les propriétaires des boîtes aux lettres, telles que la suppression des messages.

Journaux d’audit des boîtes aux lettres

