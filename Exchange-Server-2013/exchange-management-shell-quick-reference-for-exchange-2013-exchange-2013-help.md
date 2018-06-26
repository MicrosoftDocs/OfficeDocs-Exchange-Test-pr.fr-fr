---
title: 'Référence rapide concernant l’environnement de ligne de commande Exchange Management Shell pour Exchange 2013: Exchange 2013 Help'
TOCTitle: Référence rapide concernant l’environnement de ligne de commande Exchange Management Shell pour Exchange 2013
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 50477954
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Référence rapide concernant l’environnement de ligne de commande Exchange Management Shell pour Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Cette rubrique décrit les cmdlets les plus fréquemment utilisées disponibles dans la version de publication (RTM) et les versions ultérieures de Microsoft Exchange Server 2013. Elle fournit également des exemples de leur utilisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Des informations supplémentaires seront bientôt ajoutées sur d’autres domaines de Exchange 2013.</td>
</tr>
</tbody>
</table>


Pour plus d'informations sur l'environnement de ligne de commande Exchange Management Shell d'Exchange 2013 et toutes les cmdlets disponibles décrites dans cette rubrique, voir les rubriques suivantes :

  - [Utilisation de PowerShell avec Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/fr-fr/library/bb123778\(v=exchg.150\))

  - [Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\))

## Sur quels élements souhaitez-vous en savoir plus ?

## Actions de cmdlet communes

Les verbes suivants sont pris en charge par la plupart des cmdlets et associés à une action spécifique.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>Le verbe New crée une instance d'un élément, comme un nouveau paramètre de configuration, une nouvelle base de données ou un nouveau connecteur SMTP.</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>Le verbe Remove supprime une instance d'un élément, comme une boîte aux lettres ou une règle de transport.</p>
<p>Toutes les cmdlets Remove prennent en charge les paramètres <em>WhatIf</em> et <em>Confirm</em>. Pour plus d'informations sur ces paramètres, voir Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>Le verbe Enable active un paramètre ou active la messagerie pour un destinataire.</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>Le verbe Disable désactive un paramètre activé ou désactive la messagerie pour un destinataire.</p>
<p>Toutes les tâches Disable prennent également en charge les paramètres <em>WhatIf</em> et <em>Confirm</em>. Pour plus d'informations sur ces paramètres, voir Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>Le verbe Set modifie des paramètres spécifiques d'un objet, tels que les alias d'un contact ou la rétention d'un élément supprimé d'une base de données de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>Le verbe Get interroge un objet spécifique ou un sous-ensemble d'un type d'objet, tel qu'une boîte aux lettres spécifique, tous les utilisateurs de boîte aux lettres ou les utilisateurs de boîte aux lettres dans un domaine.</p></td>
</tr>
</tbody>
</table>


## Paramètres importants

Les paramètres suivants vous aident à contrôler le mode d'exécution des commandes et indiquent précisément le résultat produit par une commande avant d'affecter les données.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p>Le paramètre <em>Identity</em> identifie l'objet unique pour la tâche. Il est généralement utilisé avec les cmdlets Enable, Disable, Remove, Set et Get. <em>Identity</em> est également un paramètre de position, ce qui signifie qu'il n'est pas nécessaire de spécifier <em>Identity</em> lorsque vous spécifiez la valeur du paramètre dans la ligne de commande.</p>
<p>Par exemple, <em>Get-Mailbox -Identity user1</em> requiert des informations pour la boîte aux lettres de <em>user1</em>. <em>Get-Mailbox user1</em> est équivalent à <em>Get-Mailbox -Identity user1</em>.</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p>Le paramètre <em>WhatIf</em> donne pour instruction à la cmdlet de simuler les actions qu'elle va appliquer à l'objet. Le paramètre <em>WhatIf</em> permet d'afficher les changements potentiels sans devoir les appliquer. La valeur par défaut est <em>$true</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p>Le paramètre <em>Confirm</em> suspend le traitement par la cmdlet et demande à l'administrateur de confirmer les actions que la cmdlet va effectuer avant de continuer le traitement. La valeur par défaut est <em>$true</em>.</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p>Le paramètre <em>Validate</em> amène la cmdlet à vérifier que toutes les conditions préalables à l'exécution de l'opération sont réunies et que l'opération sera exécutée avec succès.</p></td>
</tr>
</tbody>
</table>


## Conseils et astuces

Les commandes suivantes sont associées à diverses tâches que vous pouvez utiliser dans le cadre de l'administration d'Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>Cette cmdlet extrait toutes les tâches qui peuvent être exécutées dans Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>keyword</em>*</p></td>
<td><p>Cette cmdlet extrait les tâches dont la cmdlet contient <em>keyword</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>task</em> | Get-Member</p></td>
<td><p>Cette cmdlet extrait toutes les propriétés et méthodes de <em>task</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List</p></td>
<td><p>Cette cmdlet affiche la sortie de la requête dans une liste mise en forme. Vous pouvez transmettre la sortie de la cmdlet Get vers Format-List pour afficher l'ensemble des propriétés qui existent sur l'objet renvoyé par cette commande ou spécifier les propriétés individuelles que vous voulez afficher, séparées par des virgules, comme dans l'exemple suivant : <em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>task</em></p></td>
<td><p>Cette cmdlet extrait des informations de l'aide d'Exchange Management Shell pour toute tâche d'Exchange 2013, comme dans l'exemple suivant : <em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List &gt; <em>file.txt</em></p></td>
<td><p>Cette cmdlet exporte la sortie de <em>task</em> dans un fichier texte : <em>file.txt</em></p></td>
</tr>
</tbody>
</table>


## Autorisations


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Gestion de l’organisation</em>&quot;</p></td>
<td><p>Cette commande récupère les membres du groupe de rôles de gestion <em>Gestion de l’organisation</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment - rôle &quot;<em>Création de destinataire de message</em>&quot; -GetEffectiveUsers</p></td>
<td><p>Cette commande extrait une liste de tous les utilisateurs qui bénéficient des autorisations émanant du rôle de gestion <em>Création de destinataire de message</em>. notamment les utilisateurs membres de groupes de rôles ou de groupes de sécurité universels auxquels ce rôle a été attribué. Les utilisateurs membres de groupes de rôles liés dans une autre forêt ne sont pas concernés.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrateur</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>Cette commande extrait une liste des cmdlets que l’utilisateur doté du rôle <em>Administrateur</em> peut exécuter.</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>Cette commande extrait une liste de tous les utilisateurs autorisés à exécuter la cmdlet <em>Remove-Mailbox</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>Cette commande extrait une liste de tous les utilisateurs autorisés à modifier la boîte aux lettres de l’utilisateur <em>kima</em>.</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Utilisateurs de Seattle</em>&quot; -RecipientRestrictionFilter { <em>Ville</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Administrateurs de Seattle</em>&quot; -Roles &quot;<em>Destinataires de message</em>&quot;, &quot;<em>Création de destinataire de message</em>&quot;, &quot;<em>Importation/Exportation de boîtes aux lettres</em>&quot;, -CustomRecipientWriteScope &quot;<em>Utilisateurs de Seattle</em>&quot;</p></td>
<td><p>Cette commande crée une nouvelle étendue de gestion et un groupe de rôles de gestion pour permettre aux membres du groupe de rôles de gérer les destinataires à Seattle.</p>
<p>L’étendue de gestion <em>Utilisateurs de Seattle</em> est d’abord créée et correspond uniquement aux destinataires dont l’attribut <em>Ville</em> de leur objet utilisateur contient la valeur <em>Seattle</em>.</p>
<p>Un nouveau groupe de rôles appelé <em>Administrateurs de Seattle</em> est ensuite créé et les rôles <em>Destinataires de message</em>, <em>Création de destinataire de message</em> et <em>Importation/Exportation de boîtes aux lettres</em> sont attribués. L’étendue du groupe de rôles est définie afin que ses membres puissent uniquement gérer les utilisateurs qui correspondent à l’étendue de filtre de destinataire <em>Utilisateurs de Seattle</em>.</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Serveurs de Vancouver</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Gestion des serveurs</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Gestion des serveurs de Vancouver</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Serveurs de Vancouver</em>&quot;</p></td>
<td><p>Cette commande crée une nouvelle étendue de gestion et copie un groupe de rôles existant pour permettre aux membres du nouveau groupe de rôles de gérer uniquement les serveurs du site Active Directory de Vancouver.</p>
<p>L’étendue de gestion <em>Serveurs de Vancouver</em> est d’abord créée et correspond uniquement aux serveurs situés sur le site Active Directory de <em>Vancouver</em>. Le site Active Directory est stocké dans l’attribut <em>ServerSite</em> dans les objets serveur.</p>
<p>Puis, un nouveau groupe de rôles appelé <em>Gestion des serveurs de Vancouver</em> est créé. Il correspond à une copie du groupe de rôles <em>Gestion des serveurs</em>. L’étendue de ce nouveau groupe de rôles est cependant définie pour permettre à ses membres de gérer uniquement les serveurs correspondant à l’étendue de filtre de configuration <em>Serveurs de Vancouver</em>.</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Gestion de l’organisation</em>&quot; -Member <em>davids</em></p></td>
<td><p>Cette commande ajoute l’utilisateur <em>davids</em> au groupe de rôles <em>Gestion de l’organisation</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Création de destinataire de message</em>&quot; -RoleAssignee &quot;<em>Administrateurs de Seattle</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>Cette commande supprime le rôle <em>Création de destinataire de message</em> du groupe de rôles <em>Administrateurs de Seattle</em>. Cette commande est très utile puisque nous n’avez pas besoin de connaître le nom de l’attribution de rôle de gestion qui attribue le rôle au groupe de rôles.</p></td>
</tr>
</tbody>
</table>


## Environnement de ligne de commande Exchange Management Shell distant


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>Ces commandes ouvrent une nouvelle session de l'environnement de ligne de commande Exchange Management Shell distant entre un ordinateur d'un domaine local et un serveur Exchange 2013 distant avec le nom de domaine complet <em>ExServer.contoso.com</em>. Utilisez cette commande pour administrer un serveur Exchange 2013 distant et disposer uniquement de Windows Management Framework (comprenant l'interface de ligne de commande Windows PowerShell) sur l'ordinateur local. Cette commande utilise vos informations d'identification d'ouverture de session actuelles pour l'authentification sur le serveur Exchange 2013 distant.</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>Ces commandes ouvrent une nouvelle session de l'environnement de ligne de commande Exchange Management Shell distant entre un ordinateur d'un domaine local et un serveur Exchange 2013 distant avec le nom de domaine complet <em>ExServer.contoso.com</em>. Utilisez cette commande pour administrer un serveur Exchange 2013 distant et disposer uniquement de Windows Management Framework (comprenant Windows PowerShell) sur l'ordinateur local. Cette commande utilise les informations d'identification d'ouverture de session que vous indiquez de manière explicite pour l'authentification sur le serveur Exchange 2013 distant.</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>Cette commande ferme la session de l'environnement de ligne de commande Exchange Management Shell distant entre un ordinateur local et le serveur Exchange 2013 distant.</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>Cette commande illustre la syntaxe, en italique, requise pour importer un fichier sur un serveur Exchange 2013 distant à l'aide du paramètre FileData d'une cmdlet. La syntaxe encapsule les données contenues dans le fichier <em>M:\AudioFiles\TonySmith.wma</em> et transfère les données à la propriété FileData de la cmdlet Import-RecipientDataProperty.</p>
<p>Le paramètre FileData accepte les données provenant d'un fichier sur votre ordinateur local à l'aide de cette syntaxe sur la plupart des cmdlets.</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>Cette commande illustre un exemple de la syntaxe, en italique, requise pour exporter un fichier à partir d'un serveur Exchange 2013 distant. La syntaxe encapsule les données stockées dans la propriété FileData de l'objet retourné par la cmdlet, puis transfère les données sur votre ordinateur local. Les données sont ensuite stockées dans le fichier <em>C:\tonysmith.wma</em>.</p>
<p>La plupart des cmdlets qui génèrent des objets à l'aide d'une propriété FileData utilisent cette syntaxe pour exporter les données dans un fichier sur votre ordinateur local.</p></td>
</tr>
</tbody>
</table>

