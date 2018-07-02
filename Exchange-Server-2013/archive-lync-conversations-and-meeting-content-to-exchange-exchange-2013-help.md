---
title: 'Archivage des conversations Lync et du contenu de réunion dans Exchange: Exchange 2013 Help'
TOCTitle: Archivage des conversations Lync et du contenu de réunion dans Exchange
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678842
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Archivage des conversations Lync et du contenu de réunion dans Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez archiver du contenu Lync Online, tel que des conversations de messagerie instantanée, dans la boîte aux lettres d’un utilisateur dans Exchange Online. Dans les déploiements locaux, vous pouvez archiver du contenu Lync 2013 dans les boîtes aux lettres Exchange 2013. Dans les environnements en ligne et locaux, vous devez placer la boîte aux lettres de l’utilisateur en conservation pour litige ou en conservation inaltérable. Lorsque le contenu Lync est définitivement supprimé par un utilisateur dont la boîte aux lettres est soumise à une obligation de conservation pour litige, le contenu Lync archivé est conservé dans le dossier Éléments récupérables dans la boîte aux lettres de l’utilisateur. Le contenu n’est pas visible par les utilisateurs, mais il est inclus dans les recherches eDiscovery.

Lorsque vous placez une boîte aux lettres en conservation pour litige, tous les types de contenu, y compris les éléments Lync, sont conservés. Par défaut, c’est également le cas lorsque vous placez un élément en conservation inaltérable. Toutefois, si vous souhaitez créer une obligation de conservation inaltérable pour conserver uniquement les éléments Lync, utilisez l’option **Sélectionner les types de messages** dans l’assistant **Conservation et eDiscovery inaltérables** et sélectionnez **Éléments Lync**, comme illustré dans la capture d’écran ci-dessous.

![Placer des éléments Lync en conservation](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Placer des éléments Lync en conservation")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez également configurer une obligation de conservation inaltérable pour exclure des éléments Lync. Par exemple, les organisations peuvent préférer conserver des messages instantanés et des éléments de messagerie vocale sur une durée plus courte que pour les autres types de contenu. Pour implémenter ce type de stratégie de conservation, vous devez créer une obligation de conservation inaltérable pour conserver le contenu sur une longue durée (par exemple, 7 ans) et exclure des éléments Lync de cette stratégie. Ensuite, vous devez créer une autre obligation de conservation inaltérable d’une durée plus courte pour conserver uniquement les éléments Lync. Vous pouvez également spécifier la durée pendant laquelle le contenu doit être conservé. Pour plus d’informations sur la création d’une obligation de conservation sur une durée spécifique, consultez la rubrique <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservation inaltérable et conservation pour litige</a>.</td>
</tr>
</tbody>
</table>


Pour savoir comment placer un utilisateur en conservation, consultez les rubriques suivantes :

  - [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [Placement d’une boîte aux lettres en conservation pour litige](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

Pour les tâches de gestion supplémentaires relatives à l’archivage, consultez la rubrique :

  - [Activer ou désactiver une boîte aux lettres d’archivage dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj984357\(v=exchg.150\))

  - [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## Plus d’informations

  - L’archivage de contenu Lync a lieu sur le serveur, indépendamment du fait que l’utilisateur ait configuré le client Lync pour [enregistrer des conversations de messagerie instantanée Lync dans le dossier Historique des conversations](https://go.microsoft.com/fwlink/p/?linkid=400589).

  - L’archivage de contenu Lync commence dès que l’utilisateur est placé en conservation pour litige ou en conservation inaltérable. Pour vérifier que les communications Lync de l’utilisateur sont archivées dès la création de son compte, placez le compte en conservation immédiatement après sa création.

En outre, dans des déploiements Exchange 2013 et Lync 2013 locaux :

  - Vous devez configurer l’authentification OAuth entre Lync 2013 et Exchange 2013. Pour plus d’informations, consultez la rubrique [Intégration à SharePoint et Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

  - Vous pouvez également archiver du contenu Lync 2013 dans Exchange 2013 indépendamment du fait qu’un utilisateur se trouve en conservation. Pour cela, vous devez configurer la stratégie d’archivage Exchange de l’utilisateur. Utilisez la cmdlet `Set-CsUser` sur le serveur Lync 2013 pour définir la propriété *ExchangeArchivingPolicy* de l’utilisateur Lync sur `ArchivingToExchange`.

  - Pour plus d’informations sur l’archivage de contenu Lync dans des déploiements locaux, consultez la rubrique [Planification de l’archivage dans Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=400590) dans la documentation Lync 2013.

