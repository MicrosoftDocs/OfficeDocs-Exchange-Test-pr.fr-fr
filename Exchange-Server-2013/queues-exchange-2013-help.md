---
title: "Files d'attente: Exchange 2013 Help"
TOCTitle: Files d'attente
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51407251
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Files d'attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Une *file d'attente* est un emplacement d'hébergement temporaire pour les messages attendant de passer à l'étape suivante de traitement ou de remise à destination. Chaque file d'attente représente un ensemble logique de messages traités par un serveur Exchange dans un ordre spécifique. Dans Microsoft Exchange Server 2013, les files d'attente conservent les messages avant, pendant et après leur remise. Il existe des files d'attente sur les serveurs de boîtes aux lettres et les serveurs de transport Edge. Dans cette rubrique, nous appelons les serveurs de boîtes aux lettres et serveurs de transport Edge *serveurs de transport*.

Comme dans les versions précédentes d'Exchange, Exchange 2013 utilise une seule base de données ESE (Extensible Storage Engine) pour le stockage des files d'attente.

Vous pouvez gérer les files d'attente et les messages qu'elles contiennent à l'aide de l'environnement de ligne de commande Exchange Management Shell et de l'Afficheur des files d'attente dans la boîte à outils Exchange. Vous pouvez utiliser ces interfaces pour afficher le statut et le contenu des files d'attente et les propriétés détaillées des messages. Vous pouvez également utiliser ces interfaces pour exécuter des actions modifiant les files d'attente ou les messages dans les files d'attente.

**Contenu de cette rubrique**

  - Types de files d'attente

  - Fichiers de base de données de files d'attente

  - Propriétés de file d'attente
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate et Velocity
    
      - État de file d'attente
    
      - Autres propriétés de file d'attente

  - Propriétés de message
    
      - État de message
    
      - Autres propriétés de message

  - Gestion des files d'attente et des messages qu'elles contiennent

## Types de files d'attente

Les types de file d'attente suivants sont utilisés dans Exchange 2013 :

  - **Files d'attente persistantes**   Des *files d'attente persistantes* sont présentes sur chaque serveur de transport au sein de chaque organisation Exchange. Comme les versions précédentes d'Exchange, Exchange 2013 comprend trois files d'attente persistantes :
    
      - **File d'attente de soumission**   La file d'attente de soumission est utilisée par le catégoriseur pour rassembler tous les messages qui doivent être résolus, routés et traités par les agents de transport sur le serveur de transport. La file d'attente de soumission est la première étape du traitement des messages reçus par un serveur de transport. Sur les serveurs de messagerie, les messages sont soumis via un connecteur de réception, les répertoires de collecte ou de relecture, ou le service de dépôt de transport de boîte aux lettres. Sur les serveurs de transport Edge, les messages sont généralement soumis via un connecteur de réception, mais les répertoires de collecte et de relecture sont également des solutions.
        
        Le catégoriseur récupère les messages depuis cette file d'attente et détermine notamment l'emplacement du destinataire et la route vers cet emplacement. Après la catégorisation, le message est déplacé vers une file d'attente de remise ou dans la file d'attente inaccessible. Chaque serveur de transport dispose d'une seule file d'attente de soumission. Les messages figurant dans la file d'attente de soumission ne peuvent pas se trouver en même temps dans d'autres files d'attente. Pour plus d'informations sur le catégoriseur et le pipeline de transport, consultez la rubrique [Flux de messagerie](mail-flow-exchange-2013-help.md).
    
      - **File d'attente inaccessible**   La file d'attente inaccessible contient des messages qui ne peuvent pas être routés vers leur destination. En général, des changements de configuration qui ont modifié le chemin de routage pour la remise rendent une destination inaccessible. Quelle que soit la destination, tous les messages dont les destinataires sont inaccessibles se trouvent dans cette file d'attente. Chaque serveur de transport dispose d'une seule file d'attente inaccessible.
        
        En cas de détection d'une modification du routage, les messages figurant dans la file d'attente inaccessible sont automatiquement soumis à nouveau. Ainsi, après avoir réparé une condition ou une erreur de configuration à l'origine de l'acheminement des messages vers la file d'attente inaccessible, vous ne devez exécuter aucune action supplémentaire pour extraire les messages de la file d'attente inaccessible en vue de leur remise.
        
        La file d'attente inaccessible est généralement vide. Si la file d'attente inaccessible ne contient pas de message, elle n'apparaît pas dans l'Afficheur des files d'attente ou dans les résultats de la cmdlet **Get-Queue**.
    
      - **File d'attente de messages incohérents**   La file d'attente de messages incohérents est une file d'attente particulière permettant d'isoler les messages considérés comme nuisibles pour le système Exchange 2013 suite à une défaillance du serveur ou du service de transport. Les messages peuvent être véritablement nuisible par leur contenu et leur format. Ils peuvent également résulter d'un agent mal écrit ayant causé une défaillance du serveur Exchange lors du traitement de messages supposés incorrects.
        
        La file d'attente de messages incohérents est généralement vide. Si la file d'attente de messages incohérents ne contient pas de message, elle n'apparaît pas dans l'Afficheur des files d'attente ou dans les résultats de la cmdlet **Get-Queue**. L'expiration ou la reprise automatiques des messages de la file d'attente de messages incohérents sont impossibles. Les messages restent dans la file d'attente de messages incohérents jusqu'à leur reprise ou leur suppression manuelles par un administrateur.

  - **Files d'attente de remise**   Les files d'attente de remise contiennent des messages qui sont remis à des destinations locales ou distantes à l'aide du protocole SMTP. Tous les messages sont échangés entre les serveurs Exchange à l'aide du protocole SMTP. Les destinations non-SMTP utilisent également des files d'attente de remise si elles sont servies par un connecteur d'agent de remise. . Chaque file d'attente de remise contient des messages qui sont routés vers la même destination. Il est pratiquement inévitable que plusieurs files d'attente de remise existent sur un serveur de transport. Les files d'attente de remise sont créées de façon dynamique en fonction des besoins, puis supprimées automatiquement dès qu'elles sont vides ou que le délai d'expiration a expiré. Le délai d'expiration est contrôlé par le paramètre *QueueMaxIdleTime* de la cmdlet **Set-TransportService**. La valeur par défaut est trois minutes.

  - **Files d'attente de clichés instantanés**   Les files d'attente de clichés instantanés contiennent des copies redondantes d'un message en transit. Pour plus d'informations, consultez la rubrique [Redondance des clichés instantanés](shadow-redundancy-exchange-2013-help.md).

  - **Filet de sécurité**   Le filet de sécurité conserve des copies des messages remis avec succès par le serveur de transport. Bien qu'il soit inaccessible aux outils de gestion des files d'attente, le filet de sécurité est tout simplement une file d'attente supplémentaire dans la base de données de files d'attente. Pour plus d'informations, consultez la rubrique [Safety Net](safety-net-exchange-2013-help.md).

Retour au début

## Fichiers de base de données de files d'attente

Les différentes files d'attente sont stockées dans une même base de données ESE. Par défaut, cette base de données de files d'attente se trouve sur le serveur de transport dans l'emplacement `%ExchangeInstallPath%TransportRoles\data\Queue`.

Comme toute base de données ESE, la base de données de files d'attente utilise des fichiers journaux pour accepter, suivre et gérer les données. Pour améliorer les performances, toutes les transactions de message sont écrites en premier lieu dans des fichiers journaux et la mémoire, puis dans le fichier de base de données. Le fichier de point de contrôle suit les entrées de journaux des transactions qui ont été validées dans la base de données. Durant un arrêt ordinaire du service de transport Microsoft Exchange, les modifications de base de données non validées trouvées dans les journaux des transactions sont toujours validées dans la base de données.

Un enregistrement circulaire est utilisé pour la base de données de files d'attente. Cela signifie que l'historique des transactions validées figurant dans les journaux des transactions n'est pas conservé. Tous les journaux des transactions antérieurs au point de contrôle actuel sont supprimés immédiatement et automatiquement. Par conséquent, la relecture des journaux des transactions pour récupérer une base de données de files d'attente à partir d'une sauvegarde est impossible.

Exchange 2013 utilise des *tables de génération* pour le stockage et le nettoyage des messages figurant dans la base de données de files d'attente. Au lieu de traiter et de supprimer des enregistrements de message individuels d'une grande table, la base de données de files d'attente stocke les messages dans des tables basées sur le temps, et supprime la table entière uniquement après que tous les messages figurant dans la table ont été traités avec succès. Par exemple, tous les messages mis en file d'attente entre 13h00 et 14h00, quelle que soit la file d'attente ou la destination, sont stockés dans la table `1p-2p_msgs`. À 14h00, les nouveaux messages sont stockés dans la table `2p-3p_msgs`. À 16h00, une nouvelle table nommée `4p-5p_msgs` est créée, et la table entière `1p-2p_msgs` supprimée, mais uniquement si tous les messages qu'elle contient ont été traités avec succès. Cette approche consistant à supprimer des tables entières de messages plutôt que des messages individuels contribue à améliorer les performances d'E/S du lecteur contenant la base de données de files d'attente.

Le tableau suivant répertorie les fichiers qui composent la base de données de files d'attente.

### Fichiers qui composent la base de données de files d'attente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fichier</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>Ce fichier de base de données de files d'attente stocke tous les messages mis en file d'attente.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>Ce fichier de base de données temporaire permet de vérifier le schéma de la base de données de files d'attente au démarrage.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>Ce journal des transactions enregistre toutes les modifications apportées à la base de données de files d'attente. Les modifications sont d'abord écrites dans le journal des transactions, puis validées dans la base de données. Trn.log est le fichier journal des transactions actives actuel. Trntmp.log est le fichier journal des transactions configuré suivant, créé à l'avance. Si le fichier journal des transactions Trn.log existant atteint sa taille maximale, il est renommé Trn<em>nnnn</em>.log, où <em>nnnn</em> est un numéro séquentiel. Trntmp.log est ensuite renommé Trn.log, et devient le fichier journal des transactions actives actuel.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>Ce fichier de point de contrôle suit les entrées de journau des transactions validées dans la base de données. Ce fichier est toujours situé au même emplacement que le fichier mail.que.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>Ces fichiers journaux des transactions de réserve font office d'espaces réservés. Ils sont utilisés uniquement lorsque l'espace sur le disque dur contenant le journal des transactions n'est pas suffisant pour permettre un arrêt correct de la base de données de files d'attente.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Options de configuration de la base de données de files d'attente

Pour configurer la base de données de files d'attente, vous devez ajouter ou modifier des clés dans le fichier de configuration d'application XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Ce fichier est associé au service de transport Microsoft Exchange. Les modifications que vous apportez au fichier EdgeTransport.exe.config prennent effet après le redémarrage du service de transport Exchange.

La section `<appSettings>` du fichier EdgeTransport.exe.config vous permet d'ajouter des clés ou de modifier des clés existantes. Si une clé spécifique n'existe pas, vous pouvez l'ajouter manuellement pour en modifier la valeur.

Les clés pour la base de données de files d'attente disponibles dans le fichier EdgeTransport.exe.config sont décrites dans le tableau suivant.

### Clés de base de données de files d'attente de messages disponibles dans le fichier EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Clé</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>Cette clé spécifie le nombre d'opérations d'E/S de base de données qu'il est possible de regrouper avant leur exécution. Par défaut, cette clé n'existe pas dans le fichier EdgeTransport.exe.config.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>Cette clé spécifie le temps maximal, en millisecondes, pendant lequel la base de données attend le regroupement de plusieurs opérations d'E/S de base de données avant leur exécution. Les opérations d'E/S de base de données sont exécutées sans plus attendre si les conditions suivantes sont vraies :</p>
<ul>
<li><p>Le nombre d'opérations d'E/S de base de données spécifié par la clé <em>QueueDatabaseBatchSize</em> n'a pas été atteint.</p></li>
<li><p>Le délai spécifié par la clé <em>QueueDatabaseBatchTimeout</em> a expiré.</p></li>
</ul>
<p>Par défaut, cette clé n'existe pas dans le fichier EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>Cette clé spécifie le nombre de connexions de base de données ESE qui peuvent être ouvertes.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 Mo</p></td>
<td><p>Cette clé spécifie la mémoire utilisée pour mettre en cache les enregistrements des transactions avant leur écriture dans le fichier journal des transactions.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 Mo</p></td>
<td><p>Cette clé spécifie la taille maximale d'un fichier journal des transactions. Une fois la taille maximale du fichier journal atteinte, un nouveau fichier journal est ouvert.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Cette clé spécifie le répertoire par défaut des fichiers journaux de base de données de files d'attente. Pour obtenir des instructions sur la modification de l'emplacement de la base de données de files d'attente, consultez la rubrique <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Modifier l'emplacement de la base de données de file d'attente</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>Cette clé spécifie le nombre maximal d'éléments de travail de nettoyage en arrière-plan pouvant être mis en file d'attente simultanément dans le pool de threads du moteur de base de données.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>La clé active ou désactive la défragmentation en ligne planifiée de la base de données de files d'attente de messagerie. Par défaut, cette clé n'existe pas dans le fichier EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> ou 1h00.</p></td>
<td><p>Cette clé spécifie l'heure (au format 24 heures) à laquelle la défragmentation en ligne de la base de données de files d'attente de messagerie doit commencer. Pour spécifier une valeur, entrez-la sous forme d'heure : <em>hh:mm:ss</em>, où <em>h</em> = heures, <em>m</em> = minutes et <em>s</em> = secondes.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> ou 3 heures</p></td>
<td><p>Cette clé spécifie la durée autorisée pour l'exécution de la tâche de défragmentation en ligne. Même si la tâche de défragmentation ne se termine pas dans le délai imparti, la base de données de files d'attente est conservée dans un état cohérent. Pour spécifier une valeur, entrez-la sous forme de période : <em>hh:mm:ss</em>, où <em>h</em> = heures, <em>m</em> = minutes et <em>s</em> = secondes.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Cette clé spécifie le répertoire par défaut des fichiers de la base de données de files d'attente. Pour obtenir des instructions sur la modification de l'emplacement de la base de données de files d'attente, consultez la rubrique <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Modifier l'emplacement de la base de données de file d'attente</a>.</p></td>
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
<td>Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.</td>
</tr>
</tbody>
</table>


Retour au début

## Propriétés de file d'attente

Une file d'attente a un grand nombre de propriétés qui décrivent son but et son état. Certaines propriétés sont appliquées à la file d'attente lors de sa création, après quoi elles ne changent plus. D'autres contiennent des indicateurs d'état, de taille, de temps et autres qui sont fréquemment mis à jour.

Retour au début

## NextHopSolutionKey

Le composant de routage du catégoriseur dans le service de transport Microsoft Exchange sélectionne la destination d'un message, qui est utilisée pour la création de la file d'attente de remise. La destination est marquée sur chaque destinataire à l'aide de l'attribut **NextHopSolutionKey**. Chaque valeur unique de l'attribut **NextHopSolutionKey** correspond à une file d'attente de remise distincte.

L'attribut **NextHopSolutionKey** contient les champs suivants :

  - **DeliveryType**   La valeur de ce champ représente les résultats de la catégorisation du message, et la manière dont le service de transport va transmettre le message au saut suivant, qui peut être la destination finale du message ou un saut intermédiaire sur l'itinéraire. Le service de transport utilise une liste prédéfinie de valeurs pour le champ **DeliveryType**, qui est basée sur la destination de routage cible ou le groupe de remise.

  - **NextHopDomain**   Ce champ utilise des valeurs spécifiques basées sur la valeur du champ **DeliveryType**. Pour les files d'attente de remise, la valeur de ce champ est effectivement le nom de la file d'attente. La valeur du champ **NextHopDomain** n'est pas toujours un nom de domaine. Par exemple, cette valeur peut être le nom du site Active Directory cible ou du groupe de disponibilité de base de données (DAG). Considérez ce champ comme représentant le nom du saut suivant, dont la valeur est le nom de la destination de routage ou du groupe de remise cible.

  - **NextHopConnector**   Ce champ utilise des valeurs spécifiques basées sur la valeur du champ **DeliveryType**. La valeur est toujours exprimée sous forme d'indicateur global unique (GUID). Si ce champ n'est pas utilisé, la valeur est un GUID contenant uniquement des zéros. La valeur du champ **NextHopConnector** n'est pas toujours le GUID d'un connecteur. Par exemple, cette valeur peut être le GUID du site Active Directory cible ou du DAG. Considérez ce champ comme représentant le GUID du saut suivant, dont la valeur est le GUID de la destination de routage ou du groupe de remise cible.

Exchange 2013 ajoute également la propriété **NextHopCategory** à la file d'attente basée sur la valeur **DeliveryType**. La valeur de la propriété **NextHopCategory** est `External` ou `Internal`. La valeur `External` indique que la saut suivant de la file d'attente se trouve hors de l'organisation Exchange. La valeur `Internal` indique que la saut suivant de la file d'attente se trouve dans l'organisation Exchange. Notez que la remise d'un message à un destinataire externe peut nécessiter un ou plusieurs sauts internes.

Les valeurs des propriétés **DeliveryType**, **NextHopCategory**, **NextHopDomain** et **NextHopConnector** sont décrites dans le tableau suivant.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de remise dans l'Afficheur des files d'attente</th>
<th>DeliveryType dans l'environnement de ligne de commande</th>
<th>Description</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Agent de remise</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires situés dans un espace d'adressage non-SMTP. Les messages sont remis à l'aide d'un connecteur d'agent de remise configuré sur le serveur local.</p></td>
<td><p>External</p></td>
<td><p>Cette valeur est l'espace d'adressage de destination configuré sur le connecteur d'agent de remise.</p></td>
<td><p>Cette valeur est le GUID du connecteur d'agent de remise. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires situés dans un espace d'adressage SMTP. Les messages sont remis à l'aide d'un connecteur d'envoi configuré sur le serveur local. Le connecteur d'envoi est configuré pour utiliser un routage DNS.</p></td>
<td><p>External</p></td>
<td><p>Cette valeur est l'espace d'adressage de destination configuré sur le connecteur d'envoi. Par exemple, <code>contoso.com</code>.</p></td>
<td><p>Cette valeur est le GUID du connecteur d'envoi. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires situés dans un espace d'adressage non-SMTP. Les messages sont remis à l'aide d'un connecteur étranger configuré sur le serveur local.</p></td>
<td><p>External</p></td>
<td><p>Cette valeur est l'espace d'adressage de destination configuré sur le connecteur étranger.</p></td>
<td><p>Cette valeur est le GUID du connecteur étranger. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires situés dans un espace d'adressage SMTP. Les messages sont remis à l'aide d'un connecteur d'envoi configuré sur le serveur local. Le connecteur d'envoi est configuré pour utiliser un routage d'hôte.</p></td>
<td><p>External</p></td>
<td><p>Cette valeur est la liste des hôtes actifs configurés sur le connecteur d'envoi. Les hôtes actifs peuvent être configurés comme noms de domaine complets (FQDN), adresses IP ou les deux. Les valeurs possibles sont les suivantes :</p>
<ul>
<li><p><strong>FQDN</strong>   La syntaxe est <code>&lt;FQDN1,FQDN2,...&gt;</code>. Par exemple, <code>smarthost01.contoso.com</code> ou <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>.</p></li>
<li><p><strong>Adresse IP</strong>   La syntaxe est <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>. Par exemple, <code>[10.10.10.100]</code> ou <code>[10.10.10.100],[10.10.10.101]</code>.</p></li>
<li><p><strong>FQDN et adresse IP</strong>   La syntaxe est <code>&lt;[IPAddress1],FQDN1,...&gt;</code>, et dépend de la manière dont les hôtes actifs sont répertoriés sur le connecteur d'envoi. Par exemple, <code>[172.17.17.7],relay.tailspintoys.com</code> ou <code>mail.contoso.com,[192.168.1.50]</code>.</p></li>
</ul></td>
<td><p>Cette valeur est le GUID du connecteur d’envoi. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remise SMTP à la boîte aux lettres</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires de boîte aux lettres Exchange 2013. La base de données de boîtes aux lettres de destination est l'un des emplacements suivants :</p>
<ul>
<li><p>Le serveur de boîtes aux lettres Exchange 2013 local.</p></li>
<li><p>Un serveur de boîtes aux lettres Exchange 2013 situé dans le même DAG.</p></li>
<li><p>Un serveur de boîtes aux lettres Exchange 2013 du même site Active Directory dans un environnement non-DAG.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le nom de la base de données de boîtes aux lettres de destination. Par exemple, <code>Mailbox Database 0471695037</code>.</p></td>
<td><p>Cette valeur est le GUID de la base de données de boîtes aux lettres cible. Par exemple, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Relais SMTP vers les serveurs sources du connecteur d'envoi</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires SMTP ou non-SMTP. Les messages sont remis à l'aide d'un connecteur d'envoi, d'un connecteur d'agent de remise ou d'un connecteur étranger configuré sur un serveur de transport distant. Le serveur de transport distant peut être un serveur de boîtes aux lettres Exchange 2013 ou un serveur de transport Hub Exchange 2007 ou Exchange 2010 d'une version précédente d'Exchange. Le serveur distant peut se trouver dans le site Active Directory local ou dans un site Active Directory distant.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le nom du connecteur d'envoi, du connecteur d'agent de remise ou du connecteur étranger de destination. Par exemple, <code>Contoso.com Send Connector</code>.</p></td>
<td><p>Cette valeur est le GUID du connecteur d'envoi, du connecteur d'agent de remise ou du connecteur étranger de destination. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Relais SMTP vers le groupe de disponibilité de base de données</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires de boîte aux lettres Exchange 2013, où la base de données de boîtes aux lettres de destination se trouve dans un DAG distant. Le DAG distant peut se trouver dans le site Active Directory local ou dans un site Active Directory distant.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le nom du DAG de destination. Par exemple, <code>DAG1</code>.</p></td>
<td><p>Cette valeur est le GUID du DAG de destination. Par exemple, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Relais SMTP vers le groupe de remise de boîte aux lettres</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à des destinataires de boîte aux lettres héritée, où la boîte aux lettres de destination se trouve sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010. Le message a trait à un serveur de transport Hub exécutant la même version d'Exchange que la boîte aux lettres de destination. Le serveur de transport Hub de destination peut se trouver dans le site Active Directory local ou dans un site Active Directory distant.</p></td>
<td><p>Internal</p></td>
<td><p>Le nom de file d'attente utilise la syntaxe suivante : <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>, où <em>&lt;ADSiteName&gt;</em> est le nom du site Active Directory de destination, et <em>&lt;ExchangeVersion&gt;</em> la version d'Exchange sur le serveur de boîtes aux lettres.</p></td>
<td><p>Cette valeur est vide.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Relais SMTP vers le site Active Directory distant</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à une destination distante, et la topologie de routage requiert que le message soit routé via un site Active Directory spécifique. Le site est un saut intermédiaire sur l'itinéraire de la destination finale. Cette situation se présente dans les circonstances suivantes :</p>
<ul>
<li><p>Le message doit être routé via un site hub.</p></li>
<li><p>Le message requiert une remise via un connecteur d'envoi configuré sur un serveur de transport Edge abonné à un site Active Directory distant.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le nom du site Active Directory cible. Par exemple, <code>NorthAmericanSite</code>.</p></td>
<td><p>Cette valeur est le GUID du site Active Directory cible. Par exemple, <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Relais SMTP vers les serveurs Exchange spécifiés</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à un groupe de distribution configuré pour un serveur d'expansion spécifique. L'expansion peut être un serveur de boîtes aux lettres Exchange 2013 ou un serveur de transport hub Exchange 2007 ou Exchange 2010. Le serveur peut se trouver dans le site Active Directory local ou dans un site Active Directory distant.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le FQDN du serveur d'expansion cible. Par exemple, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Cette valeur est <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Relais SMTP dans un site Active Directory vers serveur de transport Edge</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>La file d'attente contient des messages à remettre à un espace d'adressage SMTP. Les messages sont remis à l'aide d'un connecteur d'envoi configuré sur un serveur de transport Edge abonné au site Active Directory local.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le nom du connecteur d'envoi qui achemine les messages Internet sortants de l'organisation vers Internet. Ce connecteur d'envoi créé automatiquement par l'abonnement Edge est nommé <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>. <em>&lt;ADSiteName&gt;</em> est le nom du site Active Directory local auquel le serveur de transport Edge est abonné.</p></td>
<td><p>Cette valeur est le GUID du connecteur d’envoi. Par exemple, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>Cette valeur est réservée à un usage interne chez Microsoft. Pour plus d'informations sur la pulsation, consultez la rubrique <a href="shadow-redundancy-exchange-2013-help.md">Redondance des clichés instantanés</a>.</p></td>
<td><p>s/o</p></td>
<td><p>s/o</p></td>
<td><p>s/o</p></td>
</tr>
<tr class="odd">
<td><p><strong>Redondance des clichés instantanés</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>La file d'attente contient des messages figurant dans une file d'attente de fichiers instantanés. Une file d'attente de clichés instantanés contient des copies redondantes de messages en transit, au cas où la remise des messages principaux échouerait. Pour plus d'informations, consultez la rubrique <a href="shadow-redundancy-exchange-2013-help.md">Redondance des clichés instantanés</a>.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est le FQDN du serveur principal pour lequel la file d'attente de clichés instantanés contient des copies redondantes des messages principaux. Par exemple, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Cette valeur est <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>Cette valeur est utilisée uniquement pour les files d'attente de soumission et de messages incohérents.</p></td>
<td><p>Internal</p></td>
<td><p>Pour la file d'attente de soumission, cette valeur est <code>Submisssion</code>. Pour la file d'attente de messages incohérents, cette valeur est <code>Poison Message</code>.</p></td>
<td><p>Cette valeur est <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inaccessible</strong></p></td>
<td><p><strong>Unreachable</strong></p></td>
<td><p>Cette valeur est utilisée uniquement pour la file d'attente inaccessible.</p></td>
<td><p>Internal</p></td>
<td><p>Cette valeur est <code>Unreachable Domain</code>.</p></td>
<td><p>Cette valeur est <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
</tbody>
</table>


Notez qu'Exchange 2013 prend en charge les valeurs héritées de **DeliveryType** pour assurer la compatibilité ascendante avec les versions précédentes d'Exchange. Ces valeurs sont disponibles dans l'Afficheur des files d'attente et l'environnement de ligne de commande, mais ne sont pas utilisées par Exchange 2013. Ces valeurs **DeliveryType** héritées sont les suivantes :

  - **MapiDelivery**   La file d'attente contient des messages qu'un serveur de transport hub Exchange 2007 ou Exchange 2010 doit remettre à une boîte aux lettres sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010 dans le site Active Directory local.

  - **SmtpRelayWithinAdSite**   La file d'attente contient des messages qu'un serveur de transport hub Exchange 2007 ou Exchange 2010 doit remettre à un autre serveur de transport hub dans le même site Active Directory. Le serveur de transport hub de destination peut être le serveur source pour un connecteur ou un serveur d'expansion de groupe de distribution.

  - **SmtpRelaytoTiRg**   La file d'attente contient des messages qu'un serveur de transport hub Exchange 2007 ou Exchange 2010 doit remettre à un groupe de routage Exchange Server 2003. Le serveur de destination peut être le serveur source pour un connecteur, un serveur d'expansion de groupe de distribution ou un serveur tête de pont Exchange 2003.

Retour au début

## IncomingRate, OutgoingRate et Velocity

Exchange 2013 mesure le débit des messages entrants et sortants d'une file d'attente, et stocke ces valeurs dans les propriétés de cette dernière. Vous pouvez utiliser ces débits comme indicateurs de l'intégrité de la file d'attente et du serveur de transport. Les propriétés sont les suivantes :

  - **IncomingRate**   Cette propriété est le débit d'entrée des messages dans la file d'attente.
    
    Cette valeur est calculée à partir du nombre de messages entrant dans la file d'attente toutes les 5 secondes, selon une moyenne basée sur les 60 dernières secondes. La formule se présente sous la forme `(i1+i2+i3+i4+i5+i6)/6`, où i*n* = nombre de messages entrants en 5 secondes.

  - **OutgoingRate**   Cette propriété est le débit de sortie des messages de la file d'attente.
    
    Cette valeur est calculée à partir du nombre de messages sortant de la file d'attente toutes les 5 secondes, selon une moyenne basée sur les 60 dernières secondes. La formule se présente sous la forme `(o1+o2+o3+o4+o5+o6)/6`, où i*n* = nombre de messages sortants en 5 secondes.

  - **Velocity**   Cette propriété est le débit de drainage de la file d'attente, calculé en soustrayant la valeur **IncomingRate** de la valeur **OutgoingRate**.
    
    Si la valeur de **Velocity** est supérieure à 0, les messages sortent de la file d'attente plus rapidement qu'ils n'y entrent.
    
    Si la valeur de **Velocity** est égale à 0, les messages sortent de la file d'attente au même rythme qu'ils y entrent. C'est également la valeur qui s'affiche quand la file d'attente est inactive.
    
    Si la valeur de **Velocity** est inférieure à 0, les messages entrent dans la file d'attente plus rapidement qu'ils n'en sortent.

À un niveau de base, une valeur positive de **Velocity** indique une file d'attente intègre dont le drainage est efficace, tandis qu'une valeur négative de **Velocity** indique une file d'attente dont le drainage est inefficace. Toutefois, vous devez également considérer les valeurs des propriétés **IncomingRate**, **OutgoingRate** et **MessageCount**, ainsi que la magnitude de la valeur **Velocity** pour la file d'attente. Par exemple, une valeur **Velocity** élevée négative, une valeur **MessageCount** faible, une valeur **OutgoingRate** faible et une valeur **IncominRate** élevée indiquent clairement que le drainage de la file d'attente est inefficace. En revanche, une valeur **Velocity** négative proche de zéro associée à des valeurs **IncomingRate**, **OutgoingRate** et **MessageCount** très faibles n'indiquent pas de problème avec la file d'attente.

Retour au début

## État de file d'attente

L'état actuel d'une file d'attente est stocké dans sa propriété **Status**. Les valeurs d'état d'une file d'attente peuvent être les suivantes :

  - **Active**   La file d'attente transmet activement les messages.

  - **Connexion**   La file d'attente se connecte au saut suivant.

  - **Prête**   La file d'attente à transmis des messages récemment, mais est actuellement vide.

  - **Nouvelle tentative**   La dernière tentative de connexion automatique ou manuelle a échoué, et la file d'attente attend une nouvelle tentative de connexion.

  - **Suspendue**   Un administrateur a suspendu la file d'attente manuellement pour empêcher toute remise de message. De nouveaux messages peuvent entrer dans la file d'attente, tandis que la remise des messages en cours de transmission vers le saut suivant s'achève, avant qu'ils quittent la file d'attente. Autrement, aucun message ne sort de la file d'attente tant qu'un administrateur ne reprend pas cette dernière manuellement. Notez que la suspension d’une file d’attente n’a pas pour effet de modifier l’état individuel des messages qu’elle contient.
    
    Vous pouvez suspendre une file d'attente présentant l'état Actif ou Nouvelle tentative. Vous pouvez également suspendre la file d'attente inaccessible et la file d'attente de soumission.
    
    Si vous suspendez la file d'attente inaccessible, les messages ne sont pas resoumis automatiquement au catégoriseur en cas de détection de mises à jour de configuration. Pour resoumettre automatiquement ces messages, vous devez reprendre manuellement la file d'attente inaccessible. Si vous suspendez la file d'attente de soumission, les messages ne sont pas collectés par le catégoriseur tant que la file d'attente n'a pas repris.

Retour au début

## Autres propriétés de file d'attente

D'autres propriétés de file d'attente sont explicites. La plupart des propriétés de file d'attente peuvent servir d'options de filtrage. La spécification de critères de filtrage vous permet de localiser rapidement des files d'attente et d'agir sur ces dernières. Pour une description complète des propriétés filtrables de file d'attente, consultez la rubrique [Filtres de file d’attente](queue-filters-exchange-2013-help.md).

Une propriété importante de file d'attente méritant également d'être signalée est la propriété **MessageCount** qui indique le nombre de messages présents dans la file d'attente. Cette propriété est un indicateur important de l'intégrité de la file d'attente. Par exemple, une file d'attente de remise contenant un grand nombre de messages, qui continue à croître sans jamais décroître, peut indiquer un problème de pipeline de routage ou de transport requérant votre attention.

Retour au début

## Propriétés de message

Un message en file d'attente a un grand nombre de propriétés. Bon nombre d'entre elles reflètent des informations utilisées pour la création du message. Certaines propriétés d'état et d'informations des messages sont fortement influencées par des propriétés correspondantes de la file d'attente. Toutefois, un message peut avoir une valeur différente de celle de la propriété correspondante de la file d'attente. D'autres propriétés contiennent des indicateurs d'état, de taille, de temps et autres qui sont fréquemment mis à jour.

Retour au début

## État de message

L'état actuel d'un message est stocké dans sa propriété **Status**. Les valeurs d'état d'un message peuvent être les suivantes :

  - **Actif** Si le message figure dans une file d'attente de remise, il est remis à sa destination. Si le message se trouve dans la file d'attente de soumission, il est traité par le catégoriseur.

  - **Verrouillé**   Cette valeur est réservée à un usage interne chez Microsoft, et n'est pas utilisée dans les organisations Exchange locales.

  - **PendingRemove**   Le message a été supprimé par l'administrateur, mais était déjà en cours de transmission vers le saut suivant. Le message est supprimé si la remise se solde par une erreur qui provoque la réintroduction du message dans la file d'attente. Autrement, la remise continue.

  - **PendingSuspend**   Le message a été suspendu par l'administrateur, mais était déjà en cours de transmission vers le saut suivant. Le message est suspendu si la remise se solde par une erreur qui provoque la réintroduction du message dans la file d'attente. Autrement, la remise continue.

  - **Prêt** Le message se trouve dans la file d'attente, prêt à être traité.

  - **Nouvelle tentative** La dernière tentative de connexion automatique ou manuelle pour la file d'attente dans laquelle se trouve le message a échoué. Le message attend la prochaine tentative de connexion automatique de la file d'attente.

  - **Suspendu**   L'administrateur a suspendu manuellement le message. Tous les messages dans la file d'attente de messages incohérents sont définitivement suspendus.

Retour au début

## Autres propriétés de message

D'autres propriétés de message sont explicites. La plupart des propriétés de message peuvent servir d'options de filtrage. La spécification de critères de filtrage vous permet d'identifier rapidement des messages et d'agir sur ces derniers. Pour une description complète des propriétés filtrables de message, consultez la rubrique [Filtres de messages](message-filters-exchange-2013-help.md).

Retour au début

## Gestion des files d'attente et des messages qu'elles contiennent

L'Afficheur des files d'attente et pratiquement toutes les cmdlets de gestion de file d'attente et de message sont limités à un seul serveur Exchange. Vous pouvez afficher ou manipuler des files d'attente ou des messages individuels ou multiples, mais uniquement sur un serveur spécifié.

Exchange 2013 introduit la cmdlet **Get-QueueDigest** qui fournit une vue agrégée de niveau supérieur de l'état des files d'attentes sur tous les serveurs au sein d'une étendue spécifique telle qu'un DAG, un site Active Directory, une liste de serveurs ou la forêt Active Directory entière. Les files d’attente d’un serveur de transport Edge abonné se trouvant dans le réseau de périmètre ne sont pas incluses dans les résultats. De plus, la cmdlet **Get-QueueDigest** est disponible sur un serveur de transport Edge, mais les résultats sont limités aux files d’attente du serveur de transport Edge.

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


Le tableau suivant décrit les tâches de gestion que vous pouvez effectuer sur les files d'attente ou les messages qu'elles contiennent.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tâche</th>
<th>Description</th>
<th>Outil approprié</th>
<th>Instructions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Affichage et filtrage des files d'attente sur un serveur</p></td>
<td><p>Cette action affiche une ou plusieurs files d'attente sur un serveur de transport. Vous pouvez utiliser les résultats pour agir sur les files d'attente.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Get-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="even">
<td><p>Affichage et filtrage de files d'attente sur des serveurs spécifiques dans des DAG spécifiques, des sites Active Directory spécifiques ou la forêt Active Directory entière.</p></td>
<td><p>Cette action affiche une récapitulatif des files d'attente dans une étendue définie (serveurs, DAG, sites Active Directory ou forêt Active Directory entière).</p></td>
<td><p>Cmdlet <strong>Get-QueueDigest</strong> uniquement</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspension des files d'attente</p></td>
<td><p>Cette action empêche temporairement la remise des messages qui se trouvent actuellement dans la file d'attente. La file d'attente accepte toujours de nouveaux messages mais aucun message ne quitte la file d'attente.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Suspend-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="even">
<td><p>Reprise de files d'attente</p></td>
<td><p>Cette action annule la suspension des files d'attente et active la reprise de la remise des messages en file d'attente.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Resume-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="odd">
<td><p>Nouvelles tentatives de files d'attente</p></td>
<td><p>Cette action tente immédiatement une connexion au saut suivant. Sans intervention manuelle, en cas d'échec de la connexion au saut suivant, la connexion est tentée un certain nombre de fois après un intervalle de temps spécifique entre chaque tentative.</p>
<p>Si la tentative de connexion est manuelle ou automatique, toute tentative de connexion réinitialise l'heure de la tentative suivante. Pour plus d'informations, consultez la rubrique <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">Intervalles de nouvelle tentative, de renvoi et d’expiration des messages</a>.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Retry-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="even">
<td><p>Nouvelle soumission des messages en files d'attente</p></td>
<td><p>Cette action entraîne une nouvelle soumission des messages en file d'attente à la file d'attente de soumission et une reprise du processus de catégorisation.</p></td>
<td><p><strong>Retry-Queue</strong> avec le paramètre <em>Resubmit</em></p>
<p>Notez que vous pouvez utiliser l'Afficheur des files d'attente pour resoumettre des messages, mais uniquement à partir de la file d'attente de messages incohérents. Pour resoumettre un message de la file d'attente de messages incohérents, vous devez le reprendre dans l'Afficheur des files d'attente ou utiliser la cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestion des files d’attente</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspension des messages en files d'attente</p></td>
<td><p>Cette action empêche temporairement la remise d'un message. Vous pouvez utiliser cette action pour empêcher la remise d'un message à tous les destinataires dans une file d'attente spécifique ou dans toutes les files d'attente.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Suspend-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestion des messages dans les files d'attente</a></p></td>
</tr>
<tr class="even">
<td><p>Reprise des messages en files d'attente</p></td>
<td><p>Cette action annule la suspension des messages et active la reprise de la remise des messages en file d'attente. Vous pouvez utiliser cette action pour reprendre la remise d'un message à tous les destinataires dans une file d'attente spécifique ou dans toutes les files d'attente.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestion des messages dans les files d'attente</a></p></td>
</tr>
<tr class="odd">
<td><p>Suppression de messages de files d'attente</p></td>
<td><p>Cette action empêche définitivement la remise d'un message. Vous pouvez utiliser cette action pour empêcher la remise d'un message à tous les destinataires dans une file d'attente spécifique ou dans toutes les files d'attente. Vous pouvez également configurer cette action pour envoyer un rapport de non-remise (NDR) à l'expéditeur lors de la suppression du message.</p></td>
<td><p>Afficheur des files d'attente ou cmdlet <strong>Remove-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestion des messages dans les files d'attente</a></p></td>
</tr>
<tr class="even">
<td><p>Exportation de messages de files d'attente</p></td>
<td><p>Cette action copie un message vers le chemin d'accès au fichier que vous spécifiez. Les messages ne sont pas supprimés de la file d'attente, mais une copie est enregistrée dans un emplacement de fichier. Cela permet aux administrateurs ou aux personnes autorisées dans une organisation d'examiner ultérieurement les messages. Avant d'exporter un message, vous devez le suspendre dans la file d'attente afin que la remise classique ne se poursuive pas lors du processus d'exportation.</p></td>
<td><p>Cmdlet <strong>Export-Message</strong> uniquement.</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">Exportation de messages de files d'attente</a></p></td>
</tr>
</tbody>
</table>


Retour au début

