---
title: 'Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts: Exchange 2013 Help'
TOCTitle: Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50479645
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-11-22_

**Résumé:**  en savoir plus sur la préparation des boîtes aux lettres pour les déplacements entre forêts dans Exchange 2013.

Microsoft Exchange 2013 prend en charge les déplacements de boîtes aux lettres et de migrations à l’aide d’Exchange Management Shell, en particulier, des applets de commande **New-MoveRequest** et **New-MigrationBatch** . Vous pouvez également déplacer la boîte aux lettres via Exchange Administration Center (EAC). Notez que vous pouvez déplacer des boîtes aux lettres Exchange 2010 et Exchange 2013 vers une forêt Exchange 2013.

Pour déplacer une boîte aux lettres d’une forêt Exchange à une forêt de Exchange 2013, la forêt cible Exchange 2013 doit contenir un utilisateur valide de messagerie avec un ensemble spécifié d’attributs de Active Directory. S’il existe au moins un serveur d’accès Client Exchange 2013 déployé dans la forêt, la forêt est considérée comme une forêt Exchange 2013.

En préparation au déplacement de boîte aux lettres, vous devez créer des utilisateurs à extension messagerie dotés des attributs requis dans la forêt cible. Nous vous recommandons d’utiliser ces deux approches pour créer des utilisateurs à extension messagerie dotés des attributs nécessaires :

  - Si vous avez déployé Microsoft Identity Lifecycle Manager (ILM) pour la synchronisation de listes d’adresses globales (LAG) inter-forêts, l’approche recommandée pour créer un utilisateur à extension messagerie est d’utiliser Service Pack 1 (SP1) pour ILM 2007 Feature Pack 1 (FP1). Nous avons créé un échantillon de code que vous pouvez utiliser pour apprendre à personnaliser ILM afin qu’il synchronise l’utilisateur de messagerie source et l’utilisateur de messagerie cible.
    
    Pour plus d’informations, y compris sur la façon de télécharger l’échantillon de code, consultez la rubrique [Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md).

  - Si vous avez créé l'utilisateur de messagerie cible au moyen d'un autre outil que Active Directory ILM/MIIS, utilisez la cmdlet **Update-Recipient** avec le paramètre *Identity* pour exécuter le service de liste d'adresses afin de créer **LegacyExchangeDN** pour l'utilisateur de messagerie de destination. Nous avons créé à titre d'exemple un script Windows PowerShell qui lit et écrit dans Active Directory et appelle la cmdlet **Update-Recipient**.
    
    Pour plus d’informations sur ce script, consultez la rubrique [Préparer des boîtes aux lettres pour des déplacements inter-forêts à l’aide du script Prepare-MoveRequest.ps1 dans l’environnement de ligne de commande Exchange Management Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md).

Après avoir créé l’utilisateur de messagerie cible, vous pouvez exécuter la cmdlet **New-MoveRequest** ou les cmdlets **New-MigrationBatch** pour déplacer la boîte aux lettres vers la forêt cible Exchange 2013.

Pour plus d’informations sur les demandes de déplacement, consultez les rubriques suivantes :

  - [New-MigrationBatch](https://technet.microsoft.com/fr-fr/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/fr-fr/library/dd351123\(v=exchg.150\))

Pour plus d’informations sur les déplacements de boîtes aux lettres à distance et les déplacements de boîtes aux lettres héritées à distance, voir [Déplacements de boîtes aux lettres dans Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

La suite de cette rubrique décrit les attributs de l'utilisateur de messagerie Active Directory indispensables pour un déplacement de boîte aux lettres. Ces attributs sont configurés pour vous lorsque vous utilisez le code ou le script de préparation du déplacement de la boîte aux lettres. Toutefois, vous pouvez copier manuellement ces attributs à l’aide d’un éditeur Active Directory.

## Attributs utilisateur Active Directory requis pour un déplacement de boîtes aux lettres

Afin de prendre en charge un déplacement de boîte aux lettres à distance, l’objet utilisateur de messagerie dans la forêt Exchange 2013 cible doit être doté des attributs Active Directory décrits dans cette section:

  - Attributs obligatoires

  - Attributs facultatifs

  - Attributs liés

  - Attributs des utilisateurs liés

  - Attributs de la boîte aux lettres de ressources

  - Attributs supplémentaires

## Attributs obligatoires

Le tableau suivant répertorie l'ensemble minimum d’attributs devant être configurés dans ILM au niveau de l’utilisateur de messagerie cible pour que la cmdlet **New-MoveRequest** fonctionne correctement.

### Attributs de l’utilisateur de messagerie

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>Copiez l’attribut correspondant depuis la boîte aux lettres source ou générez une nouvelle valeur.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>Copiez l’attribut correspondant depuis la boîte aux lettres source ou générez une nouvelle valeur.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source. Les attributs sont uniquement disponibles si la boîte aux lettres source est Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 (décimal) //équivalent à 0x80000006 (hexadécimal).</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (décimal) / 0 x 80 (hexa.).</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (décimal).</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>Copiez l’attribut correspondant depuis la boîte aux lettres source ou générez une nouvelle valeur.</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>Copiez l’attribut <strong>proxyAddresses</strong> de la boîte aux lettres source. En outre, copiez <strong>LegacyExchangeDN</strong> de la boîte aux lettres source en tant qu’adresse X500 dans l’attribut <strong>proxyAddresses</strong> de l’utilisateur de messagerie cible.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’attribut <strong>proxyAddresses</strong> de la boîte aux lettres source doit contenir une adresse SMTP correspondant au contrôleur de domaine de la forêt cible. Cela permet à la cmdlet <strong>New-MoveRequest</strong> de sélectionner correctement l’attribut <strong>targetAddress</strong> de l’utilisateur à extension messagerie source (converti à partir de l’utilisateur de messagerie source après la réalisation de la demande de déplacement de la boîte aux lettres) afin de s’assurer que le routage du courrier fonctionne toujours.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>Copiez l’attribut correspondant depuis la boîte aux lettres source ou générez une nouvelle valeur.</p>
<p>Assurez-vous que la valeur est unique au sein du domaine de la forêt cible à laquelle l’utilisateur de messagerie cible appartient.</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>Paramétrer sur une adresse SMTP dans l’attribut <strong>proxyAddresses</strong> de la boîte aux lettres source.</p>
<p>L’adresse SMTP doit appartenir au contrôleur de domaine de la forêt source.</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>Constante : 514 //équivalent à 0x202, ACCOUNTDISABLE | NORMAL_ACCOUNT.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>Copiez l’attribut correspondant depuis la boîte aux lettres source ou générez une nouvelle valeur. Étant donné que la connexion de l’utilisateur de messagerie est désactivée, <strong>userPrincipalName</strong> n’est pas utilisé.</p></td>
</tr>
</tbody>
</table>


## Attributs facultatifs

Il n’est pas obligatoire que les attributs suivants soient configurés pour que la cmdlet **New-MoveRequest** fonctionne correctement. Cependant, leur synchronisation améliore l’expérience de l’utilisateur final après déplacement de la boîte aux lettres. Du fait que la liste d’adresses globale de la forêt cible affiche cet utilisateur de messagerie cible, il est conseillé de paramétrer les attributs suivants liés à la liste d’adresses globale.

### Attributs liés à la liste d’adresses globale

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
</tbody>
</table>


## Attributs liés

Un attribut lié est un attribut Active Directory qui référence à d’autres objets Active Directory dans la forêt locale. Vous ne pouvez pas copier directement les valeurs de l’attribut lié à partir d’une boîte aux lettres dans la forêt source vers un utilisateur de messagerie dans la forêt cible. Tout d’abord, vous devez trouver les objets Active Directory dans la forêt source auxquels l’attribut de la boîte aux lettres cible se réfère. Ensuite, vous devez trouver les objets Active Directory correspondants dans la forêt cible pour l’objet Active Directory mentionné ci-dessus dans la forêt source. Enfin, paramétrez l’attribut de l’utilisateur de messagerie cible afin qu’il se réfère aux objets Active Directory dans la forêt cible.

### Attributs liés

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>Correspond à l’attribut <strong>altRecipient</strong> de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source. Cet attribut est une valeur boléenne devant être paramétrée avec <strong>altRecipient</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (et ses liens secondaires)</p></td>
<td><p>Correspond à l’attribut de gestionnaire de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (liens secondaires)</p></td>
<td><p>Il s’agit du lien secondaire de l’attribut de membre de groupe.</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (et ses liens secondaires)</p></td>
<td><p>Correspond à l’attribut <strong>publicDelegates</strong> de la boîte aux lettres source.</p></td>
</tr>
</tbody>
</table>


## Attributs des utilisateurs liés

Si vous souhaitez déplacer une boîte aux lettres vers une forêt de ressources Exchange 2013, la boîte aux lettres au sein de la forêt de ressources est considérée comme une *boîte aux lettres liée*. Dans ce scénario, vous devez créer un utilisateur de messagerie lié dans la forêt de ressources (cible). Pour créer un utilisateur de messagerie lié, vous devez paramétrer les attributs indiqués dans le tableau suivant.

### Attributs des utilisateurs de messagerie liés

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>Si la boîte aux lettres source dispose de <strong>msExchMasterAccountSid</strong>, copiez-le. Dans le cas contraire, copiez <strong>objectSid</strong> de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Constante : -1073741818 (décimal) //équivalent à 0xC0000006 *non signé*.</p></td>
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
<td>Une boîte aux lettres liée ne peut être créée que s’il existe une approbation de forêt entre la forêt source et la forêt cible.</td>
</tr>
</tbody>
</table>


Si l’objet source est désactivé et l’attribut **msExchMasterAccountSid** paramétré sur auto (boîte aux lettres de ressources, boîte aux lettres partagée), ne marquez rien dans l’objet utilisateur cible.

Si l’objet source est désactivé et l’attribut **msExchMasterAccountSid** n’est pas configuré, la boîte aux lettres n’est pas valide.

Si l’objet source est activé et l’attribut **msExchMasterAccountSid** est configuré, la boîte aux lettres n’est pas valide.

## Attributs de la boîte aux lettres de ressources

Si vous souhaitez déplacer une boîte aux lettres vers une forêt Exchange 2013, vous devez définir les attributs indiqués dans le tableau suivant sur l’utilisateur de messagerie cible.

### Attributs de la boîte aux lettres de ressources

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Si la boîte aux lettres source est une salle de conférence :</p>
<ul>
<li><p><strong>Constante</strong> -2147481850 (décimal) //équivalent à 0x80000706 *non signé*.</p></li>
</ul>
<p>Si la boîte aux lettres source est une boîte aux lettres d’équipement :</p>
<ul>
<li><p><strong>Constante</strong> -2147481594 (décimal) //équivalent à 0x80000806 *non signé*.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
</tbody>
</table>


## Attributs supplémentaires

Dans Exchange 2007, la cmdlet **Move-Mailbox** copie également les attributs indiqués dans le tableau suivant lors du déplacement d’une boîte aux lettres. Vous pouvez éventuellement copier les attributs en fonction des besoins de votre organisation.

### Attributs de la boîte aux lettres de ressources

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributs Active Directory de l’utilisateur de messagerie</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>Copiez directement l’attribut correspondant de la boîte aux lettres source.</p></td>
</tr>
</tbody>
</table>

