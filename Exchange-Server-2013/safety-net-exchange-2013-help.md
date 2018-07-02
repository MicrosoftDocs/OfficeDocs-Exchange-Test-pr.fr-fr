---
title: 'Safety Net: Exchange 2013 Help'
TOCTitle: Safety Net
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 50479281
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Safety Net

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Microsoft Exchange Server 2013, le principal mécanisme de haute disponibilité des boîtes aux lettres est le groupe de disponibilité de base de données (DAG). Pour plus d'informations sur les groupes de disponibilité de base de données, consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md). La *benne de transport* a été introduite pour la première fois dans Exchange 2007 et a été ultérieurement améliorée dans Exchange 2010 pour fournir des copies redondantes des messages qui ont été remis aux boîtes aux lettres des groupes de disponibilité de base de données. Dans Exchange 2010, la benne de transport permettait de se protéger contre une perte de données en tenant à jour une file d'attente de messages remis qui n'avaient pas été répliqués vers les copies de base de données de boîtes aux lettres passives du groupe de disponibilité de base de données. Lorsqu'une défaillance de la base de données de boîtes aux lettres ou du serveur exigeait la promotion d'une copie obsolète de la base de données de boîtes aux lettres, les messages contenus dans la benne de transport étaient automatiquement renvoyés à la nouvelle copie active de la base de données de boîtes aux lettres.

La benne de transport a été améliorée dans Exchange 2013 et s'appelle désormais *Safety Net*.

Safety Net ressemble à la benne de transport d'Exchange 2010 sur certains points :

  - Safety Net est une file d'attente qui est associée au service de transport sur un serveur de boîtes aux lettres. Cette file d'attente stocke des copies des messages qui ont été correctement traités par le serveur.

  - Vous pouvez spécifier la durée pendant laquelle Safety Net stocke les copies des messages correctement traités avant qu'ils n'expirent et ne soient automatiquement supprimés. La valeur par défaut est 2 jours.

Safety Net diffère dans Exchange 2013 sur les points suivants :

  - Safety Net ne nécessite pas de groupes de disponibilité de base de données. Pour les serveurs de boîtes aux lettres qui n'appartiennent pas à un groupe de disponibilité de base de données, Safety Net stocke les copies des messages remis sur d'autres serveurs de boîtes aux lettres dans le site Active Directory local.

  - Safety Net lui-même est désormais redondant et ne constitue plus un point de défaillance unique, ce qui nous amène au concept de *dispositif de sécurité principal* et de *dispositif de sécurité de secours*. Si le dispositif de sécurité principal n'est pas disponible pendant plus de 12 heures, les demandes de retransmission deviennent des demandes de retransmission de secours et les messages sont retransmis à partir du dispositif de sécurité de secours.

  - Safety Net assume une part de responsabilité en ce qui concerne la redondance de secours dans les environnements DAG. La redondance de secours n'a pas besoin de conserver une autre copie du message remis dans une file d'attente de secours lorsqu'elle attend que le message remis soit répliqué sur les copies passives de la base de données de boîtes aux lettres sur les autres serveurs de boîtes aux lettres du DAG. La copie du message remis est déjà stockée dans Safety Net et le message peut donc être retransmis à partir de Safety Net, si nécessaire.

  - Dans Exchange 2013, la haute disponibilité du transport est bien plus qu'un effort optimal de redondance des messages. Exchange 2013 tente de garantir la redondance des messages. Pour cette raison, vous ne pouvez pas spécifier une taille limite maximale pour Safety Net. Vous pouvez uniquement déterminer la durée pendant laquelle Safety Net stocke les messages avant qu'ils ne soient automatiquement supprimés.

**Contenu de cette rubrique**

Principes de fonctionnement de Safety Net

Retransmission de messages à partir de Safety Net

Retransmission de messages à partir du dispositif de sécurité de secours

## Principes de fonctionnement de Safety Net

La redondance de secours conserve une copie redondante du message lorsque le message est en transit. Safety Net conserve une copie redondante d'un message une fois ce dernier correctement traité. Aussi, Safety Net intervient là où finit la redondance de secours. Les mêmes concepts relatifs à la redondance de secours, notamment les limites de la haute disponibilité du transport, les messages principaux, les serveurs principaux, les messages instantanés et les serveurs de clichés instantanés s'appliquent également à Safety Net. Pour plus d'informations, consultez la rubrique [Redondance des clichés instantanés](shadow-redundancy-exchange-2013-help.md).

Le dispositif de sécurité principal existe sur le serveur de boîtes aux lettres qui contenait le message principal avant que le message ne soit correctement traité par le service de transport. Cela peut signifier que le message a été remis au service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres de destination. Ou bien que le message a été relayé via le serveur de boîtes aux lettres dans un site Active Directory conçu comme un site hub pendant son transit vers le groupe de disponibilité de base de données de destination ou le site Active Directory. Une fois traité par le serveur principal, le message principal est déplacé de la file d'attente active vers le dispositif de sécurité principal sur le même serveur.

Le dispositif de sécurité de secours existe sur le serveur de boîtes aux lettres qui contenait le message instantané. Une fois que le serveur de clichés instantanés a déterminé que le serveur principal a traité correctement le message principal, il déplace le message instantané de la file d'attente de secours vers le dispositif de sécurité de secours sur le même serveur. Même si cela peut sembler évident, l'existence du dispositif de sécurité de secours requiert l'activation de la redondance de secours. Cette dernière est activée par défaut dans Exchange 2013.

Les paramètres utilisés par Safety Net sont décrits dans le tableau suivant.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>SafetyNetHoldTime</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>2 jours</p></td>
<td><p>Durée de stockage des messages principaux correctement traités dans le dispositif de sécurité principal et des messages instantanés avec accusé de réception dans le dispositif de sécurité de secours.</p>
<p>Vous pouvez également spécifier cette valeur dans le Centre d'administration Exchange (CAE), sous <strong>Flux de messagerie</strong> &gt; <strong>Connecteurs de réception</strong> &gt; <strong>Autres options</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icône Options supplémentaires" alt="Icône Options supplémentaires" /> &gt; <strong>Paramètres de transport de l'organisation</strong> &gt; <strong>Safety Net</strong> &gt; <strong>Temps de retenue du dispositif de sécurité</strong>.</p>
<p>Les messages instantanés sans accusé de réception finissent par expirer à partir du dispositif de sécurité de secours après la somme de <em>SafetyNetHoldTime</em> et de <em>MessageExpirationTimeout</em> sur <strong>Set-TransportService</strong>.</p>
<p>Pour éviter la perte de données durant les retransmissions Safety Net, la valeur de <em>SafetyNetHoldTime</em> doit être supérieure ou égale à la valeur de <em>ReplayLagTime</em> sur <strong>Set-MailboxDatabaseCopy</strong> pour la copie retardée de la base de données de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplayLagTime</em> sur <strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Non configurée</p></td>
<td><p>Temps d'attente nécessaire au service de réplication Microsoft Exchange pour relire les fichiers journaux qui ont été copiés vers la copie de la base de données passive. La définition de ce paramètre sur une valeur supérieure à 0 engendre la création d'une copie retardée de la base de données de boîtes aux lettres. La valeur maximale est de 14 jours.</p>
<p>Pour éviter la perte de données durant les retransmissions Safety Net, la valeur de <em>ReplayLagTime</em> doit être inférieure ou égale à la valeur de <em>SafetyNetHoldTime</em> sur <strong>Set-TransportConfig</strong> pour la copie retardée de la base de données de boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> sur <strong>Set-TransportService</strong></p></td>
<td><p>2 jours</p></td>
<td><p>La durée de temps pendant laquelle un message peut rester dans une file d'attente avant d'expirer.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> permet la redondance des clichés instantanés sur tous les serveurs de transport dans l'organisation.</p></li>
<li><p><code>$false</code>désactive la redondance des clichés instantanés sur tous les serveurs de transport dans l'organisation.</p></li>
</ul>
<p>Un dispositif de sécurité redondant requiert l'activation de la redondance de secours.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Retransmission de messages à partir de Safety Net

Les retransmissions de messages à partir de Safety Net sont initiées par le composant Active Manager du service de réplication Microsoft Exchange qui gère les groupes de disponibilité de base de données et les copies de base de données de boîtes aux lettres. Aucune intervention manuelle n'est requise pour retransmettre des messages à partir de Safety Net. Pour plus d'informations sur Active Manager, consultez la rubrique [Active Manager](active-manager-exchange-2013-help.md).

Il existe deux scénarios de base de retransmission de messages Safety Net :

  - Après le basculement automatique ou manuel d'une base de données de boîtes aux lettres dans un groupe de disponibilité de base de données.

  - Après l'activation d'une copie retardée d'une base de données de boîtes aux lettres.

Une *copie de base de données de boîtes aux lettres retardée* ou *copie retardée* est une copie passive de base de données de boîtes aux lettres dans laquelle des mises à jour de la base de données sont volontairement retardées pour se protéger contre un endommagement logique de la base de données de boîtes aux lettres. Pour plus d'informations, consultez la rubrique [Gestion des copies de base de données de boîtes aux lettres](managing-mailbox-database-copies-exchange-2013-help.md).

La seule différence majeure entre ces deux scénarios est la durée de la période de rétroactivité nécessaire pour retransmettre des messages à partir de Safety Net. En règle générale, pour un basculement dans un groupe de disponibilité de base de données, la nouvelle copie active de la base de données de boîtes aux lettres a généralement entre quelques minutes et plusieurs heures de retard par rapport à l'ancienne copie active. Une copie retardée d'une base de données de boîtes aux lettres a généralement plusieurs jours de retard par rapport à l'ancienne copie active.

La principale condition d'une retransmission réussie d'une copie retardée à partir de Safety Net est la durée de stockage des messages dans Safety Net, qui doit être supérieure ou égale au délai d'attente de la copie retardée de la base de données de boîtes aux lettres. En d'autres termes, la valeur de *SafetyNetHoldTime* sur **Set-TransportConfig** doit être supérieure ou égale à la valeur de *ReplayLagTime* sur **Set-MailboxDatabaseCopy** pour la copie retardée.

Retour au début

## Retransmission de messages à partir du dispositif de sécurité de secours

Tout comme la retransmission des messages à partir du dispositif de sécurité principal, les retransmissions de messages à partir du dispositif de sécurité de secours sont entièrement automatisées et ne requièrent aucune intervention manuelle.

Quand Active Manager demande la retransmission d'un message à partir de Safety Net sur une période donnée, la demande est envoyée au service de transport sur les serveurs de boîtes aux lettres sur lesquels le dispositif de sécurité principal conserve les copies du message pour la période requise. Dans les organisations Exchange de grande taille, il est probable que les messages souhaités existent dans Safety Net sur plusieurs serveurs de boîtes aux lettres, notamment si la période requise est longue.

Sans optimisation, la retransmission des messages à partir de Safety Net génèrerait des volumes potentiellement importants de remises dupliquées. Les remises dupliquées au sein de l'organisation Exchange ne constituent pas en soi un problème, car la détection de messages dupliqués empêche les utilisateurs de la boîte aux lettres de voir les copies en double d'un message. Toutefois, la remise de messages dupliqués à des destinataires extérieurs à l'organisation Exchange entraîne la création de copies en double des messages. Heureusement, la retransmission de messages à partir de Safety Net a été optimisée dans Exchange 2013 pour réduire la remise de messages dupliqués.

Si le dispositif de sécurité principal ne répond pas initialement, ou s'il ne répond pas pendant la retransmission du message, Active Manager poursuit ses tentatives de contact pendant 12 heures avant d'abandonner. Passé ce délai, une diffusion est envoyée au service de transport sur tous les serveurs de boîtes aux lettres dans les limites de haute disponibilité du transport, et une demande de retransmission du message à partir de Safety Net est présentée pour l'intervalle de temps et la base de données de boîtes aux lettres requis. Quand un dispositif de sécurité de secours répond, il retransmet les messages pour la base de données de boîtes aux lettres demandée uniquement pendant l'intervalle de temps requis.

Certains aspects importants doivent être pris en compte pour les messages instantanés stockés dans le dispositif de sécurité de secours :

  - Le dispositif de sécurité de secours ignore à quel emplacement le serveur principal a transmis le message principal.

  - Les messages instantanés du dispositif de sécurité de secours ne contiennent que les destinataires de l'enveloppe de message d'origine, et non les destinataires réels auxquels le message principal a été remis. Par exemple, le destinataire de l'enveloppe de message peut être un groupe de distribution qui requiert une expansion.

  - Les messages contenus dans le dispositif de sécurité de secours ne reflètent aucune des mises à jour survenues après le traitement du message par le serveur principal. Par exemple, le codage de messages ou la conversion de contenu.

Les messages instantanés retransmis à partir du dispositif de sécurité de secours requièrent une catégorisation et un traitement complets via le service de transport sur le serveur de boîtes aux lettres. La retransmission de quantités importantes de messages instantanés à partir du dispositif de sécurité de secours peut être coûteuse en ressources de serveur de boîtes aux lettres. Heureusement, la retransmission de messages instantanés à partir du dispositif de sécurité de secours est également optimisée de sorte que seuls les messages du dispositif de sécurité de secours pour l'intervalle de temps et la base de données de boîtes aux lettres requis sont retransmis.

L'interaction entre le dispositif de sécurité principal et le dispositif de sécurité de secours pendant la retransmission des messages est décrite dans le scénario suivant.

1.  Active Manager demande une retransmission des messages à partir de Safety Net pour une base de données de boîtes aux lettres pendant l'intervalle de temps 5h00-9h00. Cependant, le serveur de boîtes aux lettres qui contient le dispositif de sécurité principal s'est bloqué suite à une panne matérielle. Active Manager essaie à plusieurs reprises de contacter le dispositif de sécurité principal pendant 12 heures.

2.  Au bout de 12 heures, Active Manager envoie un message de diffusion au service de transport sur tous les serveurs de boîtes aux lettres dans les limites de haute de disponibilité du transport, et recherche d'autres dispositifs de sécurité qui contiennent des messages pour la base de données de boîtes aux lettres cible pour l'intervalle de temps 5h00-9h00. Le dispositif de sécurité de secours répond et retransmet les messages pour la base de données de boîtes aux lettres entre 5h00 et 9h00.

Une interaction intéressante se produit si le dispositif de sécurité principal était hors connexion pendant une partie de l'intervalle de retransmission demandé, comme décrit dans le scénario suivant.

1.  La base de données de file d'attente sur le serveur de boîtes aux lettres qui contient le dispositif de sécurité principal est endommagée, et une nouvelle base de données de file d'attente est créée à 7h00. Tous les messages principaux stockés dans le dispositif de sécurité principal entre 1h00 et 7h00 sont perdus, mais le serveur peut néanmoins stocker les copies des messages correctement remis dans Safety Net à partir de 7h00.

2.  Active Manager demande la retransmission des messages à partir de Safety Net pour une base de données de boîtes aux lettres durant l'intervalle de temps 1h00-9h00.

3.  Le dispositif de sécurité principal retransmet les messages entre 7h00 et 9h00.

4.  Le dispositif de sécurité principal envoie un message de diffusion au service de transport sur tous les serveurs de boîtes aux lettres dans les limites de haute disponibilité du transport, et recherche d'autres dispositifs de sécurité qui contiennent des messages pour la base de données de boîtes aux lettres cible durant l'intervalle de temps compris entre 1h00 et 7h00 pour lequel le dispositif de sécurité principal ne possède aucun message. Le dispositif de sécurité de secours génère une deuxième demande de retransmission pour le compte du dispositif de sécurité principal afin de retransmettre les messages instantanés pour la base de données de boîtes aux lettres cible entre 1h00 et 7h00.

D'autres problèmes doivent être pris en compte lors de la retransmission de messages à partir de Safety Net.

1.  Toutes les notifications d'état de remise (DSN) et les notifications d'échec de remise sont supprimées pour les retransmissions Safety Net. Par exemple, si le message principal a entraîné la création d'une notification d'échec de remise, la notification d'échec de remise relative au message retransmis ne sera pas délivrée.

2.  Il est possible que les utilisateurs supprimés d'un groupe de distribution ne reçoivent pas un message retransmis lorsque le dispositif de sécurité de secours retransmet le message. Par exemple, un message est envoyé à un groupe contenant de l'utilisateur A et l'utilisateur B, et les deux destinataires reçoivent le message. L'utilisateur B est ensuite supprimé du groupe. Ultérieurement, une demande de retransmission à partir du dispositif de sécurité principal est effectuée pour la base de données de boîtes aux lettres qui contient la boîte aux lettres de l'utilisateur B. Cependant, le dispositif de sécurité principal n'est pas disponible pendant plus de 12 heures. Par conséquent, le dispositif de sécurité de secours répond et retransmet le message en question. Pendant la retransmission, lorsque le groupe de distribution est étendu, l'utilisateur B n'est pas membre du groupe et ne recevra pas de copie du message retransmis.

3.  Les nouveaux utilisateurs ajoutés à un groupe de distribution peuvent éventuellement recevoir un ancien message retransmis lorsque le dispositif de sécurité de secours retransmet le message. Par exemple, un message est envoyé à un groupe contenant de l'utilisateur A et l'utilisateur B, et les deux destinataires reçoivent le message. L'utilisateur C est ensuite ajouté au groupe. Ultérieurement, une demande de retransmission à partir du dispositif de sécurité principal est effectuée pour la base de données de boîtes aux lettres qui contient la boîte aux lettres de l'utilisateur C. Toutefois, le serveur de sécurité principal n'est pas disponible pendant plus de 12 heures. Par conséquent, le dispositif de sécurité de secours répond et retransmet les messages en question. Pendant la retransmission, lorsque le groupe de distribution est étendu, l'utilisateur C est membre du groupe et recevra une copie du message retransmis.

Retour au début

