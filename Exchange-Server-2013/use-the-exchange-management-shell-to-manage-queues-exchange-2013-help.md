---
title: 'Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente: Exchange 2013 Help'
TOCTitle: Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51407191
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Comme dans les versions précédentes d'Exchange, vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell dans Microsoft Exchange Server 2013 pour consulter des informations sur les files d'attente et les messages qu'elles contiennent, ainsi que pour effectuer des actions de gestion sur ces éléments. Dans Exchange 2013, il existe des files d'attente sur les serveurs de boîtes aux lettres et les serveurs de transport Edge. Dans cette rubrique, nous appelons ces serveurs *serveurs de transport*.

Lorsque vous utilisez l'environnement de ligne de commande pour afficher et gérer les files d'attente et les messages qu'elles contiennent sur les serveurs de transport, il est important de savoir comment identifier les éléments à gérer. Généralement, les serveurs de transport contiennent un grand nombre de files d'attente et de messages à remettre. Pour identifier les files d'attentes ou les messages à afficher ou à gérer, vous utilisez les paramètres de filtrage disponibles dans les cmdlets de gestion des files d'attente et des messages.

Notez que, pour gérer les files d'attente et les messages qu'elles contiennent, vous pouvez également utiliser l'Afficheur des files d'attente disponible dans la boîte à outils Exchange. Toutefois, les cmdlets d'affichage des files d'attente et des messages prennent en charge un plus grand nombre de propriétés filtrables et d'options de filtrage que l'Afficheur des files d'attente. Pour plus d'informations sur l'Afficheur des files d'attente, consultez la rubrique [Afficheur des files d’attente](queue-viewer-exchange-2013-help.md).

**Contenu de cette rubrique**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## Paramètres de filtrage de file d'attente

Le tableau suivant décrit les paramètres de filtrage disponibles pour les cmdlets de gestion de file d'attente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Paramètres de filtrage</th>
<th>Commentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>Vous ne pouvez pas utiliser le paramètre <em>Identity</em> avec les paramètres <em>Filter</em> dans la même commande. Vous pouvez utiliser les paramètres <em>Include</em> et <em>Exclude</em> avec le paramètre <em>Filter</em> dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Vous devez utiliser le paramètre <em>Identity</em> ou le paramètre<em>Filter</em>, mais vous ne pouvez pas utiliser les deux dans la même commande.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>Vous devez utiliser l'un des paramètres <em>Server</em>, <em>Dag</em>, <em>Site</em> ou <em>Forest</em>, mais vous ne pouvez l'associer a aucun de ces paramètres dans la même commande. Vous pouvez utiliser le paramètre <em>Filter</em> avec tout autre paramètre de filtrage.</p></td>
</tr>
</tbody>
</table>


Notez qu'un paramètre *Server* est disponible pour toutes les cmdlets de gestion de file d'attente. Pour la cmdlet **Get-QueueDigest**, le paramètre *Server* est un paramètre d'étendue qui spécifie le ou les serveurs pour lesquels vous voulez voir des informations résumées sur les files d'attente. Pour toutes les autres cmdlets de gestion de file d'attente, le paramètre *Server* vous permet de vous connecter à un serveur spécifique, et d'exécuter les commandes de gestion de file d'attente sur ce dernier. Vous pouvez utiliser le paramètre *Server* avec ou sans le paramètre *Filter*, mais vous ne pouvez pas utiliser le paramètre *Server* avec le paramètre *Identity*. Vous utilisez le nom d'hôte ou le nom de domaine complet (FQDN) du serveur de transport avec le paramètre *Server*.

Retour au début

## Identité de file d'attente

Le paramètre *Identity* pour les cmdlets de gestion de file d'attente identifie une file d'attente spécifique. Lorsque vous utilisez le paramètre *Identity*, vous ne pouvez spécifier aucun autre paramètre de filtrage de file d'attente, car vous avez déjà identifié la file d'attente de façon unique. Le paramètre *Identity* utilise la syntaxe de base *\<Serveur\>*\\*\<File d'attente\>*.

L'espace réservé *\<Serveur\>* est le nom d'hôte ou le nom de domaine complet (FQDN) du serveur Exchange, par exemple, `mailbox01` ou `mailbox01.contoso.com`. Si vous omettez le qualificateur *\<Serveur\>*, le serveur local est supposé.

L'espace réservé \<*File d'attente*\> accepte l'une des valeurs suivantes :

  - **Nom de file d'attente permanente**   Les files d'attente permanentes ont des noms cohérents uniques sur tous les serveurs de boîtes aux lettres ou de transport Edge. Les noms de files d'attente permanentes sont les suivants :
    
      - **Soumission**   Cette file d'attente contient des messages en attente de traitement par le catégoriseur.
    
      - **Inaccessible**   Cette file d'attente contient des messages impossibles à router. Cette file d'attente existe uniquement à partir du moment où des messages y sont placés.
    
      - **Incohérents**   Cette file d'attente contient des messages identifiés comme nuisibles pour le serveur Exchange. Cette file d'attente existe uniquement à partir du moment où des messages y sont placés.

  - **Nom de file d'attente de remise**   Le nom d'une file d'attente de remise est la valeur de la propriété **NextHopDomain** de la file d'attente. Par exemple, le nom de file d'attente peut être l'espace d'adressage d'un connecteur d'envoi, le nom d'un site Active Directory ou le nom d'un DAG. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique [Files d'attente](queues-exchange-2013-help.md).

  - **Entier de file d'attente**   Les files d'attente de remise et de clichés instantanés sont associées à une valeur entière unique dans la base de données de files d'attente. Toutefois, vous devez exécuter la cmdlet **Get-Queue** pour trouver la valeur entière de la file d'attente dans la propriété **Identity** ou **QueueIdentity**.

  - **Nom de file d'attente de clichés instantanés**   Une file d'attente de clichés instantanés utilise la syntaxe `Shadow\`*\<QueueInteger\>*

Le tableau suivant résume la syntaxe que vous pouvez utiliser avec le paramètre *Identity* pour les cmdlets de gestion de file d'attente. Dans toutes les valeurs, *\<Serveur\>* est le nom d'hôte ou le nom de domaine complet (FQDN) du serveur.

### Formats d'identité de file d'attente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur de paramètre d'identité</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> ou <code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>File d'attente permanente sur le serveur spécifié ou sur le serveur local.</p>
<p><em>&lt;PersistentQueueName&gt;</em> est <code>Submission</code>, <code>Unreachable</code> ou <code>Poison</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> ou <code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>File d'attente de remise sur le serveur spécifié ou sur le serveur local.</p>
<p><em>&lt;NextHopDomain&gt;</em> est une destination de routage ou un groupe de remise pour les messages figurant dans la file d'attente. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> ou <code>&lt;QueueInteger&gt;</code></p></td>
<td><p>File d'attente de remise sur le serveur spécifié ou sur le serveur local.</p>
<p><em>&lt;QueueInteger&gt;</em> est la valeur entière unique de la file d'attente indiquée dans la propriété <strong>Identity</strong> de la cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> ou <code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>File d'attente de clichés instantanés sur le serveur spécifié ou sur le serveur local.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> ou <code>*</code></p></td>
<td><p>Toutes les files d'attente sur le serveur spécifié ou sur le serveur local. Notez que ces valeurs peuvent être utilisées uniquement avec la cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Paramètre de filtrage de file d'attente

Vous pouvez utiliser le paramètre *Filter* pour toutes les cmdlets de gestion de file d'attente afin de spécifier les files d'attente à afficher ou à gérer sur la base de leurs propriétés. Le paramètre *Filter* crée une expression comprenant des opérateurs de comparaison, qui limite l'opération de file d'attente aux files d'attente répondant aux critères de filtrage. Pour spécifier plusieurs conditions auxquelles les résultats doivent répondre, vous pouvez utiliser l'opérateur logique `-and`.

Pour obtenir la liste complète des propriétés de file d'attente que vous pouvez utiliser avec le paramètre *Filter*, consultez la rubrique [Files d'attente](queues-exchange-2013-help.md).

Pour obtenir les liste des opérateurs de comparaison que vous pouvez utiliser avec le paramètre *Filter*, consultez la section Comparison operators to use when filtering queues or messages de cette rubrique.

Pour obtenir des exemples de procédures utilisant le paramètre *Filter* pour afficher et gérer des files d'attente, consultez la rubrique [Gestion des files d’attente](manage-queues-exchange-2013-help.md).

Retour au début

## Paramètres Include et Exclude

Dans Exchange 2013, les paramètres *Include* et *Exclude* sont disponibles pour la cmdlet `Get-Queue`. Vous pouvez les utiliser séparément ou ensemble, ainsi qu'avec le paramètre *Filter* pour affiner les résultats de file d'attente sur le serveur de transport local ou spécifié. Par exemple, vous pouvez :

  - Exclure des résultats les files d'attente vides.

  - Exclure des résultats les files d'attente vers des destinations externes.

  - Inclure dans les résultats les files d'attente dont le paramètre **DeliveryType** a une valeur spécifique.

Pour filtrer les files d'attente, les paramètres *Include* et *Exclude* utilisent les propriétés de file d'attente suivantes :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur</th>
<th>Description</th>
<th>Exemple de code dans l'environnement de ligne de commande</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>Cette valeur inclut ou exclut des files d'attente en fonction de la valeur de la propriété <strong>DeliveryType</strong>. Vous pouvez spécifier plusieurs valeurs séparées par des virgules. Les valeurs correctes pour le paramètre <strong>DeliveryType</strong> sont énoncées dans la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
<td><p>Cet exemple renvoie toutes les files d'attente de remise sur le serveur local où le saut suivant est un connecteur d'envoi sur le serveur local, configuré pour le routage d'hôte actif :</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>Cette valeur inclut ou exclut les files d'attente vides. Les files d'attente vides ont la valeur <code>0</code> dans la propriété <strong>MessageCount</strong>.</p></td>
<td><p>Cet exemple renvoie toutes les files d'attente sur le serveur local, qui contiennent des messages</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>Cette valeur inclut ou exclut les files d'attente dont la propriété <strong>NextHopCategory</strong> a la valeur <code>External</code>.</p>
<p>Dans les files d'attente externes, le paramètre <strong>DeliveryType</strong> a toujours l'une des valeurs suivantes :</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
<td><p>Cet exemple renvoie toutes les files d'attente internes sur le serveur local.</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>Cette valeur inclut ou exclut les files d'attente dont la propriété <strong>NextHopCategory</strong> a la valeur <code>Internal</code>. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></td>
<td><p>Cet exemple renvoie toutes les files d'attente internes sur le serveur local.</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


Notez que vous pouvez dupliquer la fonctionnalité des paramètres *Include* et *Exclude* à l'aide du paramètre *Filter*. Par exemple, la commande `Get-Queue -Exclude Empty` produit les mêmes résultats que `Get-Queue -Filter {MessageCount -gt 0}`. Toutefois, la syntaxe des paramètres *Include* et *Exclude* est plus simple et plus facile à mémoriser.

Retour au début

## Get-QueueDigest

Exchange 2013 ajoute une cmdlet de file d'attente nommée **Get-QueueDigest**. Cette cmdlet vous permet d'afficher des informations concernant une partie ou la totalité des files d'attente au sein de votre organisation Exchange à l'aide d'une seule commande. Plus particulièrement, la cmdlet **Get-QueueDigest** vous permet d’afficher des informations sur les files d’attente, en fonction de leur emplacement sur des serveurs, dans des DAG, dans des sites Active Directory ou dans la forêt Active Directory toute entière. Les files d’attente sur un serveur de transport Edge abonné dans le réseau de périmètre ne sont pas incluses dans les résultats. De plus, la cmdlet **Get-QueueDigest** est disponible sur un serveur de transport Edge, mais les résultats sont limités aux files d’attente sur le serveur de transport Edge.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, la cmdlet <strong>Get-QueueDigest</strong> affiche les files d’attente de remise contenant au moins dix messages, et les résultats peuvent dater d’une à deux minutes. Pour obtenir des instructions sur la modification de ces valeurs par défaut, consultez la rubrique Configurer Get-QueueDigest <a href="configure-get-queuedigest-exchange-2013-help.md">Configurer Get-QueueDigest</a>.</td>
</tr>
</tbody>
</table>


Les paramètres de filtrage et de tri disponibles pour la cmdlet **Get-QueueDigest** sont décrits dans le tableau suivant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Dag</em>, <em>Server</em> ou <em>Site</em></p></td>
<td><p>Ces paramètres s'excluent mutuellement et définissent l'étendue d'application de la cmdlet. Vous devez spécifier l'un de ces paramètres ou le commutateur <em>Forest</em>. Généralement, vous utiliserez le nom du serveur, du DAG ou du site Active Directory, mais vous pouvez également utiliser toute valeur identifiant de façon unique le serveur, le DAG ou le site. Vous pouvez spécifier plusieurs serveurs, DAG ou sites séparés par des virgules.</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>Ce commutateur est requis si vous n'utilisez pas les paramètres <em>Dag</em>, <em>Server</em> ou <em>Site</em>. Avec ce commutateur, vous ne spécifiez aucune valeur. En utilisant ce commutateur, vous obtenez les files d'attente de tous les serveurs de boîtes aux lettres Exchange 2013 figurant dans la forêt Active Directory. Vous ne pouvez pas utiliser le commutateur <em>Forest</em> pour afficher des files d'attente figurant dans des forêts Active Directory distantes.</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>Ce paramètre accepte les valeurs <code>None</code>, <code>Normal</code> et <code>Verbose</code>. La valeur par défaut est <code>Normal</code>. Lorsque vous utilisez la valeur <code>None</code>, le nom de file d'attente est omis de la colonne <strong>Détails</strong> dans les résultats.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Ce paramètre vous permet de filtrer des files d'attente sur la base de leurs propriétés. Vous pouvez utiliser toutes les propriétés de file d'attente filtrables décrites dans la rubrique <a href="queue-filters-exchange-2013-help.md">Filtres de file d’attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>Ce paramètre groupe les résultats de file d'attente. Vous pouvez grouper les résultats pour l'une des propriétés suivantes :</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>Par défaut, les résultats sont groupés par <code>NextHopDomain</code>. Pour plus d'informations sur ces propriétés de file d'attente, consultez la rubrique <a href="queue-filters-exchange-2013-help.md">Filtres de file d’attente</a>.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Ce paramètre limite les résultats de file d'attente à la valeur que vous spécifiez. Les files d'attente sont triées dans l'ordre décroissant du nombre de messages qu'elles contiennent, et groupées en fonction de la valeur spécifiée par le paramètre <em>GroupBy</em>. La valeur par défaut est 1 000. Cela signifie que, par défaut, la commande affiche les 1 000 premières files d'attente groupées par <strong>NextHopDomain</strong>, et triées dans l'ordre décroissant du nombre de messages qu'elles contiennent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>Le paramètre spécifie le nombre de secondes s'écoulant avant l'expiration de l'opération. La valeur par défaut est <code>00:00:10</code>, soit 10 secondes.</p></td>
</tr>
</tbody>
</table>


Cet exemple renvoie toutes les files d'attente externes non vides présentes sur les serveurs de boîtes aux lettres Exchange 2013 nommés Mailbox01, Mailbox02 et Mailbox03.

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

Retour au début

## Paramètres de filtrage de message

Le tableau suivant décrit les paramètres de filtrage disponibles pour les cmdlets de gestion de message.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Paramètres de filtrage</th>
<th>Commentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>Tous les paramètres de filtrage s'excluent mutuellement, et vous pouvez les utiliser ensemble dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Vous devez utiliser le paramètre <em>Identity</em> ou le paramètre<em>Filter</em>, mais vous ne pouvez pas utiliser les deux dans la même commande.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p>Le paramètre <em>Identity</em> est obligatoire.</p></td>
</tr>
</tbody>
</table>


Notez qu'un paramètre *Server* est disponible pour toutes les cmdlets de gestion de message, à l'exception de la cmdlet **Export-Message**. Vous utilisez le paramètre *Server* pour vous connecter à un serveur spécifique et exécuter les commandes de gestion de message sur ce dernier. Vous pouvez utiliser le paramètre *Server* avec ou sans le paramètre *Filter*, mais vous ne pouvez pas utiliser le paramètre *Server* avec le paramètre *Identity*. Vous utilisez le nom d'hôte ou le nom de domaine complet (FQDN) du serveur de transport avec le paramètre *Server*.

Retour au début

## Identité de message

Le paramètre *Identity* pour les cmdlets de gestion de message permet d'identifier un message spécifique dans une ou plusieurs files d'attente. Lorsque vous utilisez le paramètre *Identity*, vous ne pouvez spécifier aucun autre paramètre de filtrage de message, car vous avez déjà identifié le message de façon unique. Le paramètre *Identity* utilise la syntaxe de base *\<Serveur\>*\\*\<File d'attente\>*\\*\<MessageInteger\>*.

L'espace réservé *\<Serveur\>* est le nom d'hôte ou le nom de domaine complet (FQDN) du serveur Exchange, par exemple, `mailbox01` ou `mailbox01.contoso.com`. Si vous omettez le qualificateur *\<Serveur\>*, le serveur local est supposé.

L'espace réservé \<*File d'attente*\> accepte l'identité de la file d'attente, telle que décrite dans la section « Identité de file d'attente » de cette rubrique. Par exemple, vous pouvez utiliser le nom de file d'attente permanente, la valeur **NextHopDomain** ou la valeur entière unique de la file d'attente dans la base de données de files d'attente.

L'espace réservé *\<MessageInteger\>* représente la valeur entière unique attribuée au message lorsqu'il entre pour la première fois dans la base de données de files d'attente sur le serveur. Si le message est envoyé à plusieurs destinataires nécessitant plusieurs files d'attente, toutes ses copies dans toutes les files d'attente reprises dans la base de données de files d'attente ont la même valeur entière. Toutefois, vous devez exécuter la cmdlet **Get-Message** pour trouver la valeur entière du message dans la propriété **Identity** ou **MessageIdentity**.

Le tableau suivant résume la syntaxe que vous pouvez utiliser avec le paramètre *Identity* pour les cmdlets de gestion de message. Dans toutes les valeurs, *\<Serveur\>* est le nom d'hôte ou le nom de domaine complet (FQDN) du serveur.

### Formats d'identité de message

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur de paramètre d’identité</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> ou <code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>Message dans une file d'attente spécifique sur le serveur spécifié ou sur le serveur local.</p>
<p><em>&lt;MessageInteger&gt;</em> est la valeur entière unique du message indiquée dans la propriété <strong>Identity</strong> de la cmdlet <strong>Get-Message</strong>.</p>
<p><em>&lt;File d'attente&gt;</em> représente l'une des valeurs suivantes :</p>
<ul>
<li><p><strong>Nom de file d'attente permanente</strong>   Valeur <code>Submission</code>, <code>Unreachable</code> ou <code>Poison</code>.</p></li>
<li><p><strong>Nom de file d'attente de remise</strong>   Valeur de la propriété <strong>NextHopDomain</strong> de la file d'attente, qui est en fait le nom de cette dernière. Cette valeur peut être une destination de routage ou un groupe de remise. Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique <a href="queues-exchange-2013-help.md">Files d'attente</a>.</p></li>
<li><p><strong>Entier de file d'attente</strong>   Valeur entière unique de la file d'attente de remise ou de la file d'attente de clichés instantanés qui apparaît dans la propriété <strong>Identity</strong> des cmdlets <strong>Get-Message</strong> ou <strong>Get-Queue</strong>.</p></li>
<li><p><strong>Identité de file d'attente de clichés instantanés</strong>   La file d'attente de clichés instantanés utilise la syntaxe <code>Shadow\&lt;QueueInteger&gt;</code>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> or <code>*\&lt;MessageInteger&gt;</code> ou <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>Toutes les copies du message dans tous les files d'attente reprises dans la base de données de files d'attente sur le serveur spécifié ou sur le serveur local.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Paramètre de filtrage de message

Vous pouvez utiliser le paramètre *Filter* avec les cmdlets **Get-Message**, **Remove-Message**, **Resume-Message** et **Suspend-Message** pour spécifier les messages que vous voulez afficher ou gérer en fonction de leurs propriétés. Le paramètre *Filter* crée une expression comprenant des opérateurs de comparaison, qui limite l'opération de message aux messages répondant aux critères de filtrage. Pour spécifier plusieurs conditions auxquelles les résultats doivent répondre, vous pouvez utiliser l'opérateur logique `-and`.

Pour obtenir la liste complète des propriétés de message que vous pouvez utiliser avec le paramètre *Filter*, consultez la rubrique [Files d'attente](queues-exchange-2013-help.md).

Pour obtenir les liste des opérateurs de comparaison que vous pouvez utiliser avec le paramètre *Filter*, consultez la section Comparison operators to use when filtering queues or messages de cette rubrique.

Pour obtenir des exemples de procédures utilisant le paramètre *Filter* pour afficher et gérer des messages, consultez la rubrique [Gestion des files d’attente](manage-queues-exchange-2013-help.md).

Retour au début

## Paramètre de file d'attente

Le paramètre *Queue* est utilisé uniquement avec la cmdlet **Get-Message**. Vous pouvez utiliser ce paramètre pour obtenir tous les messages d'une file d'attente spécifique, ou tous les messages de plusieurs files d'attente en utilisant le caractère générique (\*). Lorsque vous utilisez le paramètre *Queue*, utilisez le format d'identité de file d'attente *\<Serveur\>*\\*\<File d'attente\>*, tel que décrit dans la section « identité de file d'attente » de cette rubrique.

Retour au début

## Opérations de comparaison à utiliser lors du filtrage de files d'attente ou de messages

Lorsque vous créez une expression de filtre de file d'attente ou de message à l'aide du paramètre *Filter*, vous devez inclure un opérateur de comparaison pour la valeur de propriété à mettre en correspondance. Le tableau suivant présente les opérateurs de comparaison que vous pouvez utiliser dans une expression de filtre, ainsi que le mode de fonctionnement de chacun d'eux. Quel que soit l'opérateur, les valeur comparées ne sont pas sensibles à la casse.

### Opérateurs de comparaison

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Opérateur</th>
<th>Fonction</th>
<th>Exemple de code dans l’environnement de ligne de commande</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>Cet opérateur permet de spécifier que les résultats doivent correspondre précisément à la valeur de propriété indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste de toutes les files d'attente dont l'état est Nouvelle tentative :</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>Pour afficher la liste de tous les messages dont l'état est Nouvelle tentative :</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>Cet opérateur permet de spécifier que les résultats ne doivent pas correspondre à la valeur de propriété indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste de toutes les files d'attente dont l'état n'est pas Actif :</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>Pour afficher la liste de tous les messages dont l'état n'est pas Actif :</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>Cet opérateur est utilisé avec des propriétés dont la valeur est exprimée sous forme de nombre entier ou de date/heure. Les résultats du filtre incluent uniquement les files d'attente ou messages pour lesquels la valeur de la propriété spécifiée est supérieure à celle indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste des files d'attente contenant actuellement plus de 1 000 messages :</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>Pour afficher la liste des messages pour lesquels le nombre de tentatives est supérieur à 3 :</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>Cet opérateur est utilisé avec des propriétés dont la valeur est exprimée sous forme de nombre entier ou de date/heure. Les résultats du filtre incluent uniquement les files d'attente ou les messages pour lesquels la valeur de la propriété spécifiée est supérieure ou égale à celle indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste des files d'attente contenant actuellement 1 000 messages ou davantage :</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>Pour afficher la liste des messages pour lesquels le nombre de tentatives est supérieur ou égal à 3 :</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>Cet opérateur est utilisé avec des propriétés dont la valeur est exprimée sous forme de nombre entier ou de date/heure. Les résultats du filtre incluent uniquement les files d'attente ou messages pour lesquels la valeur de la propriété spécifiée est inférieure à celle indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste des files d'attente contenant actuellement moins de 1 000 messages :</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>Pour afficher la liste des messages pour lesquels le seuil de probabilité de courrier indésirable est inférieur à 6 :</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>Cet opérateur est utilisé avec des propriétés dont la valeur est exprimée sous forme de nombre entier ou de date/heure. Les résultats du filtre incluent uniquement les files d'attente ou les messages pour lesquels la valeur de la propriété spécifiée est inférieure ou égale à celle indiquée dans l'expression.</p></td>
<td><p>Pour afficher la liste des files d'attente contenant actuellement 1 000 messages ou moins :</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>Pour afficher la liste des messages pour lesquels le seuil de probabilité de courrier indésirable est inférieur ou égal à 6 :</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>Cet opérateur est utilisé avec les propriétés dont la valeur est exprimée sous forme de chaîne de texte. Les résultats du filtre incluent uniquement les files d'attente ou les messages pour lesquels la valeur de la propriété spécifiée contient la chaîne de texte indiquée dans l'expression. Vous pouvez inclure le caractère générique (*) dans une expression <strong>-like</strong> appliquée à un champ de chaîne de texte, mais pas à un champ de type énumération.</p></td>
<td><p>Pour afficher la liste des files d'attente de remise dont la destination est un domaine SMTP dont le nom se termine par Contoso.com :</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>Pour afficher la liste des messages dont l'objet contient le texte « payday loan » :</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


Vous pouvez spécifier un filtre qui évalue plusieurs expressions à l'aide de l'opérateur de comparaison **-and**. Pour figurer dans les résultats, les files d'attente ou les messages doivent répondre à toutes les conditions du filtre.

Cet exemple affiche la liste des files d'attente dont la destination est un domaine SMTP dont le nom de termine par Contoso.com et contenant actuellement plus de 500 messages.

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

Cet exemple affiche la liste des messages envoyés à partir d'une adresse de messagerie du domaine contoso.com, dont le seuil de probabilité de courrier indésirable est supérieur 5.

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

Retour au début

## Paramètres de pagination avancée

En fonction du flux des messages, les requêtes sur les files d'attente et les messages peuvent renvoyer un ensemble d'objets conséquent. Les paramètres de pagination avancée permettent de surveiller le mode de récupération et d'affichage des résultats des requêtes.

Lorsque vous utilisez l'environnement de ligne de commande pour afficher des files d'attente et les messages qu'elles contiennent, votre requête récupère une page d'informations à la fois. Les paramètres de pagination avancée surveillent la taille du jeu de résultats et peuvent également être utilisés pour trier les résultats. Tous les paramètres de pagination avancée sont facultatifs et peuvent être associés à l'un des jeux de paramètres pouvant être utilisés avec les cmdlets **Get-Queue** et **Get-Message**. Si vous ne spécifiez aucun paramètre de pagination avancée, la requête renvoie les résultats dans l'ordre d'identité croissant.

Par défaut, quand un ordre de tri est spécifié, la propriété d'identité de message est toujours incluse et triée dans l'ordre croissant. Il s'agit de la relation de tri par défaut. La propriété d'identité de message est incluse, car les autres propriétés pouvant être incluses dans un ordre de tri ne sont pas uniques. En incluant explicitement la propriété d'identité de message dans l'ordre de tri, vous pouvez spécifier que les résultats affichent l'identité du message triée en ordre décroissant.

Les paramètres *BookmarkIndex* et *BookmarkObject* vous permettent de marquer une position dans le jeu de résultats triés. Si l'objet signet n'existe plus lors de la récupération de la page suivante de résultats, la relation de tri par défaut vérifie que le jeu de résultats commence avec l'objet le plus proche du signet. L'objet le plus proche dépend de l'ordre de tri spécifié.

Le tableau suivant décrit les paramètres de pagination avancée.

### Paramètres de pagination avancée

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BookmarkIndex</em></p></td>
<td><p>Ce paramètre spécifie la position, dans le jeu de résultats, à partir de laquelle les résultats s'affichent. La valeur de ce paramètre est un index basé sur 1 dans le jeu total de résultats. Si la valeur est inférieure ou égale à zéro, la première page de résultats complète est retournée. Si la valeur est définie sur <code>Int.MaxValue</code>, la dernière page complète de résultats est renvoyée.</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>Ce paramètre spécifie l'objet, dans le jeu de résultats, à partir duquel les résultats s'affichent. Si vous spécifiez un objet signet, il est utilisé comme point de départ de la recherche. Les lignes récupérées sont celles se trouvant avant ou après cet objet, en fonction de la valeur du paramètre <em>SearchForward</em>. Vous ne pouvez pas associer les paramètres <em>BookmarkObject</em> et <em>BookmarkIndex</em> dans une seule requête.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>Ce paramètre spécifie si l'objet signet est inclus dans le jeu de résultats. Par défaut, la valeur est définie sur <code>$true</code> et l'objet signet est inclus. Vous pouvez exécuter une requête pour une taille de résultat limitée, puis spécifier le dernier élément de ce jeu de résultats comme le signet pour la prochaine requête. Dans ce cas, vous pouvez définir <em>IncludeBookmark</em> sur <code>$false</code> afin que l'objet ne soit inclus dans aucun jeu de résultats.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Ce paramètre spécifie le nombre de résultats à afficher par page. Si aucune valeur n'est indiquée, la taille du résultat par défaut est de 1 000 objets. Exchange limite la taille du jeu de résultats à 250 000.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>Ce paramètre est un paramètre masqué. Il renvoie des informations sur le nombre total de résultats et l'index du premier objet de la page actuelle. La valeur par défaut est <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>Ce paramètre spécifie le sens de la recherche (avant ou arrière) dans le jeu de résultats. Ce paramètre n'affecte pas l'ordre dans lequel le jeu de résultats est renvoyé. Il détermine le sens de la recherche par rapport à l'index ou à l'objet signet. Si aucun objet ou index signet n'est spécifié, le paramètre <em>SearchForward</em> détermine si la recherche commence à partir du premier ou du dernier objet du jeu de résultats.</p>
<p>La valeur par défaut de ce paramètre est <code>$true</code>. Si Ce paramètre est défini sur <code>$true</code> et si un signet est spécifié, la requête recherche vers l'avant à partir de ce signet. Si vous utilisez cette configuration et s'il n'y a aucun résultat au-delà du signet, la requête renvoie la dernière page complète de résultats.</p>
<p>Si le paramètre <em>SearchForward</em> est défini sur <code>$false</code> et si un signet est spécifié, la requête effectue une recherche vers l'arrière à partir de ce signet. Si vous utilisez cette configuration et s'il y a moins d'une page complète de résultats au-delà du signet, la requête renvoie la première page complète de résultats.</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>Ce paramètre spécifie une série de propriétés de message utilisées pour contrôler l'ordre de tri du jeu de résultats. Les propriétés d'ordre de tri sont spécifiées dans l'ordre décroissant de priorité. Chaque propriété est séparée par une virgule et associée au signe + pour trier dans l'ordre croissant, ou au signe - pour trier dans l'ordre décroissant.</p>
<p>Si aucun ordre de tri explicite n'est pas spécifié à l'aide de ce paramètre, les enregistrements correspondant à la requête sont affichés et triés par le champ d'identité pour le type d'objet concerné. Si aucun ordre de tri n'est spécifié explicitement, les résultats sont toujours triés dans l'ordre croissant des identités.</p></td>
</tr>
</tbody>
</table>


L'exemple de code suivant montre l'utilisation des paramètres de pagination avancée dans une requête. Dans cet exemple, la commande se connecte au serveur spécifié et récupère un jeu de résultats contenant 500 objets. Les résultats affichés sont triés d'abord dans l'ordre croissant des adresses des expéditeurs, puis dans l'ordre décroissant des tailles de message.

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

Si vous voulez afficher les pages successives, vous pouvez définir un signet pour le dernier objet récupéré dans un jeu de résultats et exécuter une requête supplémentaire. Pour exécuter cette procédure, vous devez utiliser les fonctionnalités de script de l'environnement de ligne de commande.

L'exemple suivant utilise des scripts pour récupérer la première page de résultats, définit l'objet signet, exclut l'objet signet du jeu de résultats, puis récupère les 500 objets suivants sur le serveur spécifié.

1.  Ouvrez l'environnement de ligne de commande, puis entrez la commande suivante pour récupérer la première page de résultats.
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  Pour définir l'objet signet, entrez la commande suivante pour enregistrer le dernier élément de la première page dans une variable.
    
        $temp=$results[$results.length-1]

3.  Pour récupérer les 500 objets suivants sur le serveur spécifié en excluant l'objet signet, entrez la commande suivante.
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

Retour au début

