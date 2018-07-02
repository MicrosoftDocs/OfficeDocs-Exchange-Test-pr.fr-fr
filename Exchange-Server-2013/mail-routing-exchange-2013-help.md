---
title: 'Routage du courrier: Exchange 2013 Help'
TOCTitle: Routage du courrier
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 50478411
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Routage du courrier

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

La principale tâche du service de transport qui est présent sur tous les serveurs de boîtes aux lettres de votre organisation Microsoft Exchange Server 2013 de router les messages provenant d'utilisateurs et de sources externes vers leurs destinations finales. Les décisions de routage sont prises lors de la catégorisation des messages. Le catégoriseur est un composant du service de transport sur un serveur de boîtes aux lettres, qui traite tous les messages entrants et détermine l'action à leur appliquer en fonction des informations relatives à leurs destinations.

Le routage dans Exchange 2013 est désormais totalement compatible avec les groupes de disponibilité de base de données (DAG) et utilise l'appartenance au DAG comme limite de routage. Pourquoi ? Dans Exchange 2013, tous les serveurs de boîtes aux lettres hébergent le service de transport. Par conséquent, quand un serveur de boîtes aux lettres appartient à un DAG, le mécanisme principal de routage des messages est étroitement aligné avec le DAG. Et quand un DAG s'étend sur plusieurs sites Active Directory, l'utilisation du site Active Directory comme limite de routage principale se révèle inefficace. Exchange 2013 utilise également l'appartenance au site Active Directory comme limite de routage pour les serveurs de boîtes aux lettres qui n'appartiennent pas aux DAG, ainsi que pour l'interopérabilité de routage avec les versions antérieures d'Exchange. Les autres modifications notables apportées au routage Exchange 2013 sont les suivantes :

  - Le service de transport sur un serveur de boîtes aux lettres ne communique jamais directement avec une base de données de boîtes aux lettres. Au lieu de cela, le service de transport communique avec le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres. Seul le service de transport de boîtes aux lettres communique avec la base de données de boîtes aux lettres sur le serveur de boîtes aux lettres local. Lorsque le serveur de boîtes aux lettres est membre d'un DAG, seul le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres qui contient la copie active de la base de données de boîtes aux lettres accepte le message pour le destinataire.

  - Les appels de procédure distante (RPC) sont utilisés par le service de transport de boîtes aux lettres uniquement lors de l'échange de messages avec la base de données de boîtes aux lettres locale. Lorsque le serveur de boîtes aux lettres est membre d'un DAG, le service de transport de boîtes aux lettres utilise les RPC uniquement pour communiquer localement avec les copies actives des bases de données de boîtes aux lettres. En d'autres termes, RPC n'est jamais utilisé pour les communications entre serveurs. Au lieu de cela, le service de transport de boîtes aux lettres et le service de transport présents sur différents serveurs de boîtes aux lettres communiquent toujours à l'aide du protocole SMTP.

  - Exchange 2013 utilise une mise en file d'attente plus précise pour les destinations distantes. Au lieu d'utiliser une seule file d'attente pour toutes les destinations dans un site Active Directory distant, Exchange 2013 met les messages en file d'attente pour des destinations spécifiques à l'intérieur du site Active Directory, par exemple, en utilisant des connecteurs d'envoi individuels.

  - Les connecteurs liés sont désormais obsolètes. Un connecteur lié était un connecteur de réception lié à un connecteur d'envoi. Tous les messages reçus par le connecteur de réception étaient automatiquement transférés vers le connecteur d'envoi.

**Contenu de cette rubrique**

Composants du routage

  - Destinations de routage

  - Groupes de remise

  - Files d'attente

Routage de messages

  - Routage des messages entre des sites Active Directory

  - Routage dans le service de transport frontal sur des serveurs d’accès au client

  - Routage dans le service de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres

  - Routage dans le service de transport sur les serveurs de transport Edge

## Composants du routage

Quant un message est reçu par le service de transport sur un serveur de boîtes aux lettres Exchange 2013, le message doit être catégorisé. La première phase de la catégorisation des messages consiste en la résolution du destinataire. Une fois le destinataire résolu, la destination finale peut être identifiée. La phase suivante, le routage, détermine la meilleure façon d'atteindre cette destination. Le routage dans Exchange 2013 a été généralisé pour plus de flexibilité et moins de complexité en introduisant les concepts de destinations de routage et de groupes de remise.

## Destinations de routage

Dans Exchange 2013, la destination finale d'un message est appelée une *destination de routage*. Les destinations de routage présentes dans Exchange 2013 sont les suivantes :

  - **Base de données de boîtes aux lettres**   Destination de routage pour tout destinataire disposant d'une boîte aux lettres sur un serveur de boîtes aux lettres au sein de l'organisation Exchange. Dans Exchange 2013, les dossiers publics sont un type de boîte aux lettres. Par conséquent, le routage des messages vers des destinataires de dossiers publics est identique au routage de messages vers de destinataires de boîtes aux lettres.

  - **Connecteur**   Connecteur d'envoi pour les messages SMTP quand il est utilisé comme destination de routage. Un connecteur d'agent de remise ou un connecteur étranger est utilisé comme destination de routage pour les messages non-SMTP.

  - **Serveur d'expansion de groupe de distribution**   Destination de routage quand un groupe de distribution comporte un serveur d'expansion désigné qui est responsable de l'expansion de la liste des membres du groupe. Un serveur d'expansion de groupe de distribution est toujours un serveur de transport Hub ou un serveur de boîtes aux lettres Exchange 2013.

Notez que ces mêmes destinations de routage existaient également dans les versions antérieures d'Exchange.

Retour au début

## Groupes de remise

Chaque destination de routage dans Exchange 2013 a un ou plusieurs serveurs de transport qui sont responsables de la remise des messages à cette destination de routage. Cet ensemble de serveurs de transport se nomme *groupe de remise*. Un serveur de transport peut être un serveur de boîtes aux lettres Exchange 2013, un serveur Exchange 2010 ou un serveur Exchange 2007 sur lequel le rôle serveur de transport Hub est installé. Lorsque la destination de routage est une base de données de boîtes aux lettres, les serveurs de transport du groupe de remise ont la même version d'Exchange que la base de données de boîtes aux lettres. Lorsque la destination de routage est un connecteur ou un serveur d'expansion de groupe de distribution, le groupe de remise peut contenir une combinaison de serveurs de boîtes aux lettres Exchange 2013 et de serveurs de transport Hub Exchange 2010 ou Exchange 2007. La manière dont le message est routé dépend de la relation entre le serveur de transport source et le groupe de remise de destination :

  - Si le serveur de transport source se trouve dans le groupe de remise de destination, la destination de routage elle-même constitue le prochain saut du message. Le message est remis par le serveur de transport source à la base de données de boîtes aux lettres ou au connecteur sur un serveur de transport dans le groupe de remise. Notez que, quand un serveur d'expansion de groupe de distribution est la destination de routage, le groupe de distribution est déjà développé au moment où les messages atteignent l'étape de routage de catégorisation sur le serveur d'expansion du groupe de distribution. Ainsi, la destination de routage à partir du serveur d'expansion du groupe de distribution est toujours une base de données de boîtes aux lettres ou un connecteur.

  - Si le serveur de transport source se trouve en dehors du groupe de remise de destination, le message est relayé sur l'itinéraire de routage le moins coûteux vers le groupe de remise de destination. Selon la taille et la complexité de la topologie Exchange, le message est relayé vers d'autres serveurs de transport sur l'itinéraire de routage le moins coûteux, ou relayé directement vers un serveur de transport dans le groupe de remise de destination.

Les types de groupes de remise présents dans Exchange 2013 sont les suivants :

  - **DAG routable**   Ensemble de serveurs de boîtes aux lettres Exchange 2013 qui appartiennent à un seul DAG. Les bases de données de boîtes aux lettres dans le DAG sont les destinations de routage desservies par ce groupe de remise. Lorsque le message arrive au service de transport sur un serveur de boîtes aux lettres appartenant au DAG, le service de transport route le message vers le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres du DAG qui contient actuellement la copie active de la base de données de boîtes aux lettres de destination. Le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres de destination remet alors le message à la base de données de boîtes aux lettres locale. Même si un DAG peut contenir des serveurs de boîtes aux lettres situés dans différents sites Active Directory, le DAG constitue la limite du groupe de remise.

  - **Groupe de remise de boîtes aux lettres**   Ensemble de serveurs Exchange de version identique situés dans un seul site Active Directory. Le site Active Directory constitue la limite du groupe de remise. Les destinations de routage et les groupes de remise qui les traitent sont séparés par les principales versions de publication d'Exchange dans le site Active Directory. Les bases de données de boîtes aux lettres situées sur des serveurs de boîtes aux lettres Exchange 2010 sont desservies par les serveurs de transport Hub Exchange 2010 qui se trouvent dans le site Active Directory. Les bases de données de boîtes aux lettres situées sur des serveurs de boîtes aux lettres Exchange 2007 sont desservies par les serveurs de transport Hub Exchange 2007 qui se trouvent dans le site Active Directory. Les bases de données de boîtes aux lettres situées sur des serveurs de boîtes aux lettres Exchange 2013 dans le site Active Directory et qui n'appartiennent pas un DAG sont desservies par le service de transport sur les serveurs de boîtes aux lettres Exchange 2013 dans le site Active Directory. La manière dont le message est remis à la base de données de boîtes aux lettres dépend de la version d'Exchange :
    
      - **Exchange 2013**   Lorsque le message est arrivé sur le serveur de boîtes aux lettres de destination dans le site Active Directory de destination, le service de transport utilise le protocole SMTP pour transférer le message vers le service de transport de boîtes aux lettres. Le service de transport de boîtes aux lettres remet alors le message à la base de données de boîtes aux lettres locale en utilisant RPC.
    
      - **Exchange 2010 ou Exchange 2007**   Lorsque le message est arrivé sur un serveur de transport Hub de la même version choisi de manière aléatoire dans le site Active Directory de destination, le pilote de banque d’informations sur le serveur de transport Hub utilise RPC pour écrire le message dans la base de données de boîtes aux lettres.

  - **Serveurs sources des connecteurs**   Ensemble combiné de serveurs de transport Hub Exchange 2010 ou Exchange 2007, ou de serveurs de boîtes aux lettres Exchange 2013 qui ont l'étendue du serveur source pour un connecteur d'envoi, un connecteur d'agent de remise ou un connecteur étranger. Le connecteur est la destination de routage desservie par ce groupe de routage. Quand un connecteur a l'étendue d'un serveur spécifique, seul ce dernier est autorisé à router des messages vers la destination définie par le connecteur. Ce groupe de remise peut contenir des serveurs de transport Hub Exchange 2010 ou Exchange 2007, ou des serveurs de boîtes aux lettres Exchange 2013 situés dans différents sites Active Directory.

  - **Site AD**   Dans certaines circonstances, un site Active Directory ne constitue pas la destination finale d'un message, mais le message doit transiter par un serveur de transport Hub Exchange 2010 ou Exchange 2007, ou un serveur de boîtes aux lettres Exchange 2013 dans ce site Active Directory. Ces circonstances sont les suivantes :
    
      - Lorsque le site Active Directory est configuré en tant que site hub. Lorsque le site hub est présent sur l'itinéraire de routage le moins coûteux pour la remise des messages, les messages sont placés en file d'attente et traités par un serveur de transport dans le site hub avant d'être relayés vers leur destination finale.
    
      - Lorsqu’un serveur de transport Edge est abonné au site Active Directory. Ces serveurs de transport Edge abonnés ne sont pas directement accessibles à partir d'autres sites Active Directory. Notez que le serveur de transport Edge peut être un serveur Exchange 2013, Exchange 2010 ou Exchange 2007.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La distribution ramifiée retardée est utilisée uniquement lorsque le groupe de remise est un site Active Directory. La distribution ramifiée retardée tente de réduire le nombre de transmissions de messages lorsque plusieurs destinataires partagent une partie de l'itinéraire de routage le moins coûteux.</td>
    </tr>
    </tbody>
    </table>


  - **Liste de serveurs**   Ensemble constitué d'un ou plusieurs serveurs de transport Hub Exchange 2010 ou Exchange 2007, ou serveurs de boîtes aux lettres Exchange 2013 configurés en tant que serveurs d'expansion de groupe de distribution. Le serveur d'expansion de groupe de distribution est la destination de routage traitée par ce groupe de remise.

L'appartenance au groupe de remise n'est pas mutuellement exclusive. Par exemple, un serveur de boîtes aux lettres Exchange 2013 qui est membre d'un DAG peut aussi être le serveur source d'un connecteur d'envoi dont l'étendue est délimitée. Le serveur de boîtes aux lettres peut ainsi appartenir au groupe de remise DAG routable pour les bases de données de boîtes aux lettres du DAG, ainsi qu'à un groupe de remise de serveur source de connecteur pour le connecteur d'envoi délimité dont l'étendue est délimitée.

Le tableau suivant mappe les destinations de routage sur le groupe de remise en fonction de la version d'Exchange impliquée :


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Serveur de boîtes aux lettres Exchange 2013</th>
<th>Serveur de transport hub Exchange 2010 ou Exchange 2007</th>
<th>Serveur de transport Edge dans le réseau de périmètre</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Base de données de boîtes aux lettres figurant dans un DAG</p></td>
<td><p>DAG routable</p></td>
<td><p>Groupe de remise de boîtes aux lettres</p></td>
<td><p>s/o</p></td>
</tr>
<tr class="even">
<td><p>Base de données de boîtes aux lettres ne figurant pas dans un DAG</p></td>
<td><p>Groupe de remise de boîtes aux lettres</p></td>
<td><p>Groupe de remise de boîtes aux lettres</p></td>
<td><p>s/o</p></td>
</tr>
<tr class="odd">
<td><p>Connecteur</p></td>
<td><p>Serveurs sources des connecteurs</p></td>
<td><p>Serveurs sources des connecteurs</p></td>
<td><p>Site AD</p></td>
</tr>
<tr class="even">
<td><p>Serveur d'expansion du groupe de distribution</p></td>
<td><p>Liste de serveurs</p></td>
<td><p>Liste de serveurs</p></td>
<td><p>s/o</p></td>
</tr>
</tbody>
</table>


Retour au début

## Files d'attente

Du point de vue du serveur d'envoi, chaque file d'attente de remise correspond à la destination d'un message spécifique. Lorsque le service de transport sur le serveur de boîtes aux lettres Exchange 2013 sélectionne la destination d'un message, cette dernière est marquée sur le destinataire en tant qu'attribut **NextHopSolutionKey**. Si un message est en cours d'envoi à plusieurs destinataires, chaque destinataire dispose de l'attribut **NextHopSolutionKey**. Le serveur de réception procède également à la catégorisation du message et place le message en file d'attente pour remise. Une fois un message placé en file d'attente, vous pouvez examiner le type de remise pour une file d'attente donnée afin de déterminer si un message sera de nouveau relayé lorsqu'il atteint la destination du saut suivant. Chaque valeur unique de l'attribut **NextHopSolutionKey** correspond à une file d'attente de remise distincte.

Pour plus d'informations, consultez la section « NextHopSolutionKey » de la rubrique [Files d'attente](queues-exchange-2013-help.md).

Retour au début

## Routage de messages

Quand un message doit être remis à un groupe de remise distant, un itinéraire de routage doit être déterminé pour le message. Exchange 2013 applique la logique suivante pour sélectionner l’itinéraire de routage d’un message. Cette logique reste fondamentalement la même depuis Exchange 2010 :

1.  Calculer l'itinéraire de routage le moins coûteux en additionnant le coût des liens de sites IP à utiliser pour parvenir à la destination. Si la destination est un connecteur, le coût affecté à l'espace d'adressage est ajouté au coût pour atteindre le connecteur sélectionné. Si plusieurs itinéraires de routage sont possibles, celui dont le coût d'agrégation est le plus faible est utilisé.

2.  Si plusieurs itinéraires de routage ont le même coût d'agrégation, le nombre de sauts dans chaque itinéraire est évalué et l'itinéraire de routage présentant le nombre de sauts le moins élevé est utilisé.

3.  Si plusieurs itinéraires de routage sont encore disponibles, le nom attribué aux sites Active Directory situés avant la destination est pris en compte. L'itinéraire de routage dont le site Active Directory le plus proche de la destination est le plus bas dans l'ordre alphanumérique est utilisé. Si le site le plus proche de la destination est le même pour tous les chemins de routage évalués, un nom de site précédent est sélectionné.

Dans Exchange 2010, chaque destinataire de message est toujours associé à un seul site Active Directory et il n'y a qu'un seul routage « le moins coûteux » entre le site Active Directory source et le site Active Directory de destination. Dans Exchange 2013, un groupe de remise peut s’étendre sur plusieurs sites Active Directory et il peut y avoir plusieurs itinéraires de routage « les moins coûteux » vers ces différents sites Active Directory. Exchange 2013 désigne en tant que *site principal* un seul site Active Directory dans le groupe de remise de destination. Le site principal est le site Active Directory le plus proche sur la base de la logique de routage décrite précédemment. Pour réussir le routage de messages entre des groupes de remise, Exchange 2013 prend en compte les éléments suivants :

  - **Présence d'un ou plusieurs sites hub sur l'itinéraire de routage le moins coûteux**   Si l'itinéraire de routage le moins coûteux vers le site principal contient des sites hub, le message doit être routé via les sites hub. Le site hub le plus proche sur l'itinéraire de routage le moins coûteux est sélectionné en tant que nouveau groupe de remise de type **Site AD**, ce qui inclut tous les serveurs de transport dans le site hub. Une fois que le message a transité par le site hub, son routage sur l'itinéraire de routage le moins coûteux se poursuit. Si le site principal est un site hub, il est toujours considéré comme un site hub pour les raisons suivantes :
    
      - Si le groupe de remise de destination s'étend sur plusieurs sites Active Directory, le serveur source doit seulement essayer de se connecter aux serveurs du site hub.
    
      - Les serveurs du site hub qui appartiennent réellement au groupe de remise cible sont préférés.
    
    Comme dans la version précédente d'Exchange, tous les sites hub qui ne se trouvent pas sur l'itinéraire de routage le moins coûteux vers le site principal sont ignorés.

  - **Serveur Exchange cible à sélectionner dans le groupe de routage de destination**   Lorsque le groupe de remise de destination s'étend sur plusieurs sites Active Directory, l'itinéraire de routage vers des serveurs spécifiques au sein du groupe de remise peut avoir différents coûts. Les serveurs situés dans le site Active Directory le plus proche sont sélectionnés en tant que serveurs cibles du groupe de remise sur la base de l'itinéraire de routage le moins coûteux, et le site Active Directory où se trouvent ces serveurs est sélectionné en tant que site principal.

  - **Options de secours en cas d'échec des tentatives de connexion à tous les serveurs du groupe de routage de destination**   Si le groupe de routage de destination s'étend sur plusieurs sites Active Directory, la première option de secours correspond à tous les autres serveurs du groupe de remise de destination dans les autres sites Active Directory qui ne sont pas sélectionnés en tant que serveurs cibles. La sélection des serveurs s'effectue en fonction du coût de l'itinéraire de routage vers ces autres sites Active Directory. Si le groupe de remise de destination comporte des serveurs figurant dans le site Active Directory local, il n'y a pas d'autre option de secours, car le message est déjà aussi proche que possible de la destination de routage cible. Si le groupe de remise de destination comporte des serveurs figurant dans des sites Active Directory distants, l'option consiste à essayer de se connecter à tous les autres serveurs du site principal. Si cette opération échoue, un chemin d’interruption sur l’itinéraire de routage le moins coûteux vers le site principal est utilisé. Exchange 2013 tente de remettre le message aussi près que possible de la destination en s’interrompant à chaque saut sur le chemin de routage le moins coûteux jusqu’à ce qu’une connexion soit établie.

Retour au début

## Routage des messages entre des sites Active Directory

Exchange 2013 route les messages entre les Active Directory pratiquement de la même façon que Exchange 2010. Pour plus d’informations, consultez la rubrique [Routage des messages entre les sites Active Directory](route-mail-between-active-directory-sites-exchange-2013-help.md).

Retour au début

## Routage dans le service de transport frontal sur des serveurs d’accès au client

Il agit comme un proxy sans état pour tout le trafic SMTP externe entrant ou (éventuellement) sortant pour l’organisation Exchange 2013. Pour les messages sortants, le service de transport utilise des connecteurs d'envoi pour communiquer avec le service de transport frontal sur un serveur d'accès au client. Plus précisément, les messages sortants sont envoyés par proxy via le service de transport frontal lorsque le paramètre *FrontEndProxyEnabled* d'un connecteur d'envoi applicable est défini sur `$true`, ou lorsque l'option **Proxy via serveur d'accès au client** est sélectionnée dans les propriétés du connecteur d'envoi dans le Centre d'administration Exchange (CAE). Tout serveur d'accès au client dans le site Active Directory local est sélectionné. Le service de transport frontal ne dispose pas de connecteurs d’envoi.

Pour les messages entrants, le service de transport frontal doit trouver rapidement un service de transport unique et intègre sur un serveur de boîtes aux lettres pour recevoir la transmission du message, quel que soit le nombre ou le type de destinataires. Si cette recherche n'aboutit pas, le service de messagerie électronique apparaît comme indisponible pour les expéditeurs externes. Comme le service de transport, le service de transport frontal charge les tables de routage en fonction des informations issues d'Active Directory, et utilise des groupes de remise pour déterminer comment router les messages. Cependant, les tables de routage utilisées par le service de transport frontal ont les caractéristiques uniques suivantes :

  - Le service de transport frontal n'est jamais considéré comme un membre d'un groupe de remise, même lorsque le serveur de boîtes aux lettres et le serveur d'accès au client sont installés sur le même serveur physique. Cela oblige le service de transport frontal à communiquer avec le service de transport uniquement.

  - Les tables de routage ne contiennent de routes de connecteur d'envoi.

  - Les tables de routage contiennent une liste spéciale de serveurs de boîtes aux lettres figurant dans le site Active Directory local à des fins de basculement rapide.

Le routage dans le service de transport frontal résout les destinataires du message en bases de données de boîtes aux lettres. La liste des serveurs de boîtes aux lettres utilisés par le service de transport frontal est basée sur les bases de données de boîtes aux lettres des destinataires du message. Remarque : il se peut qu'aucun des destinataires n'aient de boîte aux lettres, par exemple, si le destinataire est un groupe de distribution ou un utilisateur de messagerie. Pour chaque base de données de boîtes aux lettres, le service de transport frontal recherche le groupe de remise et les informations de routage associées. Les groupes de remise utilisés par le service de transport frontal sont les suivants :

  - DAG routable

  - Groupe de remise de boîtes aux lettres

  - Site AD

Selon le nombre et le type de destinataires, le service de transport frontal effectue l'une des actions suivantes :

  - Pour les messages n'ayant qu'un destinataire de boîte aux lettres unique, sélectionnez un serveur de boîtes aux lettres dans le groupe de remise cible et préférez le serveur de boîtes aux lettres qui se situe à proximité du site Active Directory. Le routage du message vers le destinataire peut impliquer le passage par un site hub.

  - Pour les messages ayant plusieurs destinataires de boîte aux lettres, utilisez les 20 premiers destinataires pour sélectionner un serveur de boîtes aux lettres dans le groupe de remise le plus proche, en fonction de la proximité du site Active Directory. Notez que la bifurcation des messages ne s'effectue pas dans le transport frontal. Par conséquent, un seul serveur de boîtes aux lettres est finalement sélectionné, quel que soit le nombre de destinataires d'un message.

  - Si le message n'a pas de destinataire de boîtes aux lettres, sélectionnez de manière aléatoire un serveur de boîtes aux lettres dans le site Active Directory local.

Retour au début

## Routage dans le service de transport de boîtes aux lettres sur les serveurs de boîtes aux lettres

Il est composé de deux services distincts : le service de dépôt de transport de boîte aux lettres et de remise de transport de boîte aux lettres. Pour les messages entrants, le service de remise de transport de boîtes aux lettres reçoit les messages SMTP du service de transport et se connecte à la base de données de boîtes aux lettres locale via RPC pour remettre le message. Pour les messages sortants, le service de dépôt de transport de boîtes aux lettres se connecte à la base de données de boîtes aux lettres locale via RPC pour récupérer les messages, puis envoie ces derniers via SMTP au service de transport. Le service de Transport de boîtes aux lettres n'a pas d'état et ne met aucun message en file d'attente localement.

Comme le service de transport, le service de transport de boîtes aux lettres charge les tables de routage en fonction des informations issues d'Active Directory, et utilise les groupes de remise pour déterminer comment router les messages. Cependant, certains aspects du routage sont propres au service de transport de boîtes aux lettres :

  - Puisque le service de transport et le service de transport de boîtes aux lettres sont présents sur le même serveur de boîtes aux lettres Exchange 2013, le service de transport de boîtes aux lettres appartient toujours au même groupe de remise que le serveur de boîtes aux lettres. On appelle ce groupe de remise le *groupe de remise local*.

  - Le service de dépôt de transport de boîtes aux lettres envoie automatiquement les messages au service de transport sur le serveur de boîtes aux lettres local ou sur d'autres serveurs de boîtes aux lettres au sein de son propre groupe de remise local. Le service de dépôt de transport de boîtes aux lettres a accès aux mêmes informations de topologie de routage que le service de transport. Le service de dépôt de transport de boîtes aux lettres peut donc envoyer des messages au service de transport sur les serveurs de boîtes aux lettres situés en dehors du groupe de remise. Les serveurs de boîtes aux lettres au sein du groupe de remise local sont utilisés en tant qu'options de secours, ainsi que pour la remise aux destinataires non associés à une boîte aux lettres.

  - Le service de transport de boîtes aux lettres communique uniquement avec le service de transport sur des serveurs de boîtes aux lettres Exchange 2013.

  - Le service de transport de boîtes aux lettres communique uniquement avec des bases de données de boîtes aux lettres sur le serveur de boîtes aux lettres Exchange 2013 local. Le service de transport de boîtes aux lettres ne communique jamais avec des bases de données de boîtes aux lettres sur d'autres serveurs de boîtes aux lettres.

Lorsqu'un utilisateur envoie un message de sa boîte aux lettres, le service de dépôt de transport de boîtes aux lettres résout les destinataires du message en bases de données de boîtes aux lettres. La liste des serveurs de boîtes aux lettres utilisés par le service de dépôt de transport de boîtes aux lettres est basée sur les bases de données de boîtes aux lettres des destinataires du message. Remarque : il se peut qu'aucun des destinataires n'aient de boîte aux lettres, par exemple, si le destinataire est un groupe de distribution ou un utilisateur de messagerie. Pour chaque base de données de boîtes aux lettres, le service de dépôt de transport de boîtes aux lettres recherche le groupe de remise et les informations de routage associées. Les groupes de remise utilisés par le service de dépôt de transport de boîtes aux lettres sont les suivants :

  - DAG routable

  - Groupe de remise de boîtes aux lettres

  - Site AD

Selon le nombre et le type de destinataires, le service de dépôt de transport de boîtes aux lettres effectue l'une des actions suivantes :

  - Pour les messages n'ayant qu'un destinataire de boîte aux lettres unique, sélectionnez un serveur de boîtes aux lettres dans le groupe de remise cible et préférez le serveur de boîtes aux lettres qui se situe à proximité du site Active Directory. Le routage du message vers le destinataire peut impliquer le passage par un site hub.

  - Pour les messages ayant plusieurs destinataires de boîte aux lettres, utilisez les 20 premiers destinataires pour sélectionner un serveur de boîtes aux lettres dans le groupe de remise le plus proche, en fonction de la proximité du site Active Directory.

  - Si le message n'a pas de destinataire de boîtes aux lettres, sélectionnez un serveur de boîtes aux lettres dans le groupe de remise local.

Lorsque le service de remise de transport de boîtes aux lettres reçoit un message du service de transport, il accepte ou refuse la remise du message à une base de données de boîtes aux lettres locale. Le service de remise de transport de boîtes aux lettres peut remettre le message si le destinataire réside dans une copie active d'une base de données de boîtes aux lettres locale. Toutefois, si le destinataire ne réside pas dans une copie active d'une base de données de boîtes aux lettres locale, le service de remise de transport de boîtes aux lettres ne peut pas remettre le message et doit fournir une réponse de non-remise au service de transport. Par exemple, si la copie active de la base de données de boîtes aux lettres a été récemment déplacée vers un autre serveur, le service de transport peut transmettre erronément un message à un serveur de boîtes aux lettres contenant désormais une copie inactive de la base de données de boîtes aux lettres. Les réponses de non-remise que le service de remise de transport de boîtes aux lettres renvoie au service de transport sont les suivantes :

  - Nouvelle tentative de remise

  - Générer une notification d'échec de remise

  - Re-router le message

Retour au début

## Routage dans le service de transport sur les serveurs de transport Edge

Si un serveur de transport Edge est installé dans votre réseau de périmètre, le service de transport sur le serveur de transport Edge fournit des services d’hôte actif et de relais SMTP pour l’ensemble du flux de messagerie via Internet. Les messages qui proviennent d’Internet et qui sont dirigés vers Internet sont mis en file d’attente localement sur le serveur de transport Edge. Les files d’attente correspondent à des domaines externes ou des connecteurs d’envoi. Pour plus d’informations, consultez la section « NextHopSolutionKey » dans la rubrique [Files d'attente](queues-exchange-2013-help.md).

En règle générale, lors de l’installation d’un serveur de transport Edge dans votre réseau de périmètre, vous abonnez le serveur de transport Edge à un site Active Directory. Le site Active Directory contient les serveurs de boîtes aux lettres qui relaient les messages vers le serveur de transport Edge et à partir de celui-ci. Le processus d’abonnement Edge crée une affiliation d’appartenance au site Active Directory pour le serveur de transport Edge. L’affiliation au site permet aux serveurs de boîtes aux lettres dans le site Active Directory de relayer les messages vers le serveur de transport Edge pour remise sur Internet sans qu’il soit nécessaire de configurer des connecteurs d’envoi explicites.

Dans les configurations multisites, le courrier sortant provenant d’utilisateurs internes vers des destinataires externes est d’abord routé vers le site Active Directory abonné. Le site Active Directory cible constitue le groupe de remise. La destination de routage est le connecteur d’envoi intra-organisationnel dans le service de transport sur n’importe quel serveur de boîtes aux lettres dans le site Active Directory abonné. Le *connecteur d’envoi intra-organisationnel* est un connecteur d’envoi spécial qui se trouve dans le service de transport sur chaque serveur de boîtes aux lettres. Ce connecteur d’envoi est créé implicitement. Il est invisible et n’a pas besoin d’être géré. Il est utilisé pour relayer des messages entre serveurs Exchange.

Le courrier sortant destiné à des destinataires externes est routé à partir du serveur de boîtes aux lettres vers le serveur de transport Edge. Le serveur d’accès au client n’est pas impliqué dans le routage du courrier vers un serveur de transport Edge abonné. Le courrier est transmis à partir du connecteur d’envoi intra-organisationnel dans le service de transport sur le serveur de boîtes aux lettres vers un connecteur de réception dans le service de transport sur le serveur de transport Edge. Sur un serveur de transport Edge abonné, le connecteur de réception par défaut est configuré pour écouter les connexions des serveurs de boîtes aux lettres internes dans le site Active Directory abonné et les connexions anonymes à partir d’Internet. Après avoir été classé par le service de transport sur le serveur de transport Edge, le message est en mis en file d’attente localement pour être remis à Internet à l’aide du connecteur d’envoi dédié créé lors du processus d’abonnement Edge.

Le courrier entrant provenant d’utilisateurs externes arrive sur le serveur de transport Edge via le connecteur de réception par défaut et les messages sont classés et mis en file d’attente pour être remis. Les messages sont relayés via le connecteur d’envoi dédié créé par l’abonnement Edge pour l’envoi de courrier dans l’organisation Exchange. L’emplacement où sont ensuite dirigés les messages dépend de la configuration des serveurs Exchange internes.

  - **Serveur de boîtes aux lettres et serveur d’accès au client installés sur le même ordinateur**   Dans cette configuration, le serveur d’accès au client est utilisé pour le flux de messagerie entrant. Le courrier part du connecteur d’envoi dans le service de transport sur le serveur de transport Edge, puis est dirigé vers le connecteur de réception par défaut dans le service de transport frontal sur le serveur d’accès au client, puis vers le connecteur de réception par défaut dans le service de transport sur le serveur de boîtes aux lettres.

  - **Serveur de boîtes aux lettres et serveur d’accès au client installés sur des ordinateurs distincts**   Dans cette configuration, le flux de messagerie entrant contourne le serveur d’accès au client. Le courrier part du connecteur d’envoi dans le service de transport sur le serveur de transport Edge, puis est dirigé vers le connecteur de réception par défaut dans le service de transport sur le serveur de boîtes aux lettres.

Si un serveur de transport Edge Exchange 2007 ou Exchange 2010 est installé dans le réseau de périmètre, le flux de messagerie entrant et sortant est toujours direct entre le serveur de transport Edge et le serveur de boîtes aux lettres. Le serveur d’accès au client n’est pas utilisé.

Retour au début

