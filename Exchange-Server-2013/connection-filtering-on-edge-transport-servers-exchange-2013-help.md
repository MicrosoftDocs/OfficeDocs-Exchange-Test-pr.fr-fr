---
title: 'Filtrage des connexions sur des serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Filtrage des connexions sur des serveurs de transport Edge
ms:assetid: b513755c-5d3e-44fa-a6cb-771d48b544ac
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124320(v=EXCHG.150)
ms:contentKeyID: 60829197
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrage des connexions sur des serveurs de transport Edge

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Le filtrage des connexions est une fonctionnalité de blocage du courrier indésirable de Microsoft Exchange Server 2013 qui autorise ou bloque les messages électronique selon la source du message. Le filtrage des connexions est effectué par l’agent de filtrage des connexions, qui est uniquement disponible sur les serveurs de transport Edge. L’agent de filtrage des connexions s’appuie sur l’adresse IP du serveur de messagerie expéditeur pour déterminer les mesures à prendre, s’il y en a, concernant un message entrant.

Par défaut, l’agent de filtrage des connexions est le premier agent de blocage du courrier indésirable qui évalue un message entrant sur un serveur de transport Edge. L’adresse IP source de la connexion SMTP est comparée aux adresses IP autorisées ou bloquées. Si l’adresse IP source est spécifiquement autorisée, le message est envoyé aux destinataires de votre organisation sans traitement supplémentaire par d’autres agents de blocage du courrier indésirable. Si l’adresse IP source est spécifiquement bloquée, la connexion SMTP est abandonnée. Si l’adresse IP source n’est pas spécifiquement autorisée ou bloquée, le message transite par d’autres agents de blocage du courrier indésirable sur le serveur de transport Edge.

Le filtrage des connexions compare l’adresse IP du serveur de messagerie source aux valeurs de la liste d’adresses IP autorisées et de la liste d’adresses IP bloquées, ainsi qu’aux fournisseurs de listes d’adresses IP autorisées et de listes d’adresses IP bloquées. Vous devez configurer au moins une de ces quatre banques de données d’adresses IP pour que le filtrage des connexions fonctionne. Si vous ne spécifiez pas de données d’adresses IP, désactivez l’agent de filtrage des connexions. Pour plus d’informations, voir [Gérer le filtrage des connexions sur les serveurs de transport Edge](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

**Contenu de cette rubrique**

IP Block list

IP Allow list

IP Block List providers

IP Allow List providers

Test IP Block List providers and IP Allow List providers

Configure connection filtering on Edge Transport servers that aren't directly connected to the Internet

## Liste d’adresses IP bloquées

La liste d’adresses IP bloquées contient les adresses IP des serveurs de messagerie que vous souhaitez bloquer. Vous devez gérer manuellement les adresses IP de la liste d’adresses IP bloquées. Vous pouvez ajouter des adresses IP individuelles ou des plages d’adresses IP. Vous pouvez spécifier un délai d’expiration indiquant combien de temps l’entrée d’adresse IP sera bloquée. Lorsque le délai d’expiration est atteint, l’entrée correspondant à l’adresse IP est désactivée dans la liste.

Si l’agent de filtrage des connexions trouve l’adresse IP source dans la liste d’adresses IP bloquées, la connexion SMTP est abandonnée après que tous les en-têtes **RCPT TO** (destinataires de l’enveloppe) du message ont été traités.

En outre, les adresses IP peuvent être automatiquement ajoutées à la liste d’adresses IP bloquées grâce à la fonctionnalité Réputation de l’expéditeur de l’agent d’analyse de protocole. Pour plus d’informations, voir [Réputation de l’expéditeur et agent d’analyse de protocole](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

## Liste d’adresses IP autorisées

La liste d’adresses IP autorisées contient les adresses IP des serveurs de messagerie que vous souhaitez désigner comme sources de messagerie fiables. Un message électronique provenant de serveurs de messagerie que vous spécifiez dans la liste d’adresses IP autorisées n’est traité par aucun autre agent de blocage Exchange.

Vous devez gérer manuellement les adresses IP de la liste d’adresses IP autorisées. Vous pouvez ajouter des adresses IP individuelles ou des plages d’adresses IP. Vous pouvez spécifier un délai d’expiration indiquant combien de temps l’entrée d’adresse IP sera autorisée. Lorsque le délai d’expiration est atteint, l’entrée est désactivée dans la liste d’adresses IP autorisées.

Retour au début

## Fournisseurs de listes d'adresses IP bloquées

Les fournisseurs de listes d’adresses IP bloquées sont fréquemment appelés *listes rouges en temps réel*. Les fournisseurs de listes d’adresses IP bloquées compilent des listes d’adresses IP de serveurs de messagerie qui envoient du courrier indésirable. De nombreux fournisseurs d’adresses IP bloquées compilent également des listes d’adresses IP de serveurs de messagerie susceptibles d’être utilisés pour envoyer du courrier indésirable. Il s’agit par exemple des serveurs de messagerie configurés comme relais ouvert, des fournisseurs de services Internet qui attribuent des adresses IP dynamiques et des fournisseurs de services Internet qui autorisent le trafic sur les serveurs de messagerie SMTP à partir de comptes d’accès à distance.

Lorsque vous configurez le filtrage des connexions pour utiliser un fournisseur de listes d’adresses IP bloquées, l’agent de filtrage des connexions compare l’adresse IP du serveur de messagerie expéditeur à la liste d’adresses IP du fournisseur de listes d’adresses IP bloquées. Si l’adresse est trouvée dans la liste, le message n’est pas autorisé à entrer dans votre organisation. Vous pouvez configurer le filtrage des connexions pour utiliser plusieurs fournisseurs de listes d’adresses IP bloquées. Vous pouvez alors attribuer des valeurs de priorité différentes à chaque fournisseur.

L’agent de filtrage des connexions cherche si l’adresse IP source se trouve dans la liste d’adresses IP bloquées ou dans la liste d’adresses IP autorisées. Si l’adresse IP n’existe sur aucune des listes, l’agent de filtrage des connexions interroge le fournisseur de listes d’adresses IP bloquées selon la valeur de priorité que vous lui avez attribué. Si l’adresse IP est répertoriée par un fournisseur de listes d’adresses IP bloquées, le serveur de transport Edge attend et traite l’en-tête **RCPT TO**, répond au serveur de messagerie expéditeur par une erreur `SMTP 550` et ferme la connexion. La connexion n’est pas immédiatement abandonnée, d’une part pour que la tentative de connexion puisse être journalisée, et d’autre part parce que vous pouvez spécifier des destinataires pour lesquels les messages ne sont jamais bloqués par un fournisseur de listes d’adresses IP bloquées.

Si l’adresse IP n’est répertoriée sur aucun des fournisseurs de listes d’adresses IP bloquées, l’agent de filtrage du contenu remet le message à l’agent de transport suivant sur le serveur de transport Edge.

Pour chaque fournisseur de listes d’adresses IP bloquées, vous pouvez personnaliser l’erreur `SMTP 550` envoyée à l’expéditeur d’un message lorsque ce dernier est bloqué. Vous devez repérer le fournisseur de listes d’adresses IP bloquées ayant identifié la source du message comme émettrice de courrier indésirable. Si un serveur de messagerie légitime est identifié par erreur comme source de courrier indésirable, l’administrateur peut alors contacter le fournisseur de listes d’adresses IP bloquées et prendre les mesures nécessaires pour supprimer le serveur de messagerie du service fournisseur de listes d’adresses IP bloquées.

Les fournisseurs de listes d’adresses IP bloquées peuvent renvoyer différents types de codes pour déterminer la raison pour laquelle une adresse IP est définie dans leurs listes. La plupart des fournisseurs de listes d’adresses IP bloquées renvoient des données de type masque de bits ou valeur absolue. Pour chacun de ces types de données, le fournisseur de listes d’adresses IP bloquées peut utiliser plusieurs valeurs pour classer l’adresse IP par type de menace.

Lorsque vous utilisez des fournisseurs de listes d’adresses IP bloquées, certains problèmes sont à prendre en considération :

  - Tout retard ou panne du service fournisseur de listes d’adresses IP bloquées peut entraîner un retard dans le traitement des messages sur le serveur de transport Edge. Choisissez toujours des fournisseurs de listes d’adresses IP bloquées fiables.

  - Les serveurs source que vous considérez comme légitimes peuvent être identifiés à tort comme sources de courrier indésirable. Par exemple, un serveur de messagerie peut être involontairement configuré pour servir de relais ouvert. Choisissez toujours des fournisseurs de listes d’adresses IP bloquées dont les procédures d’évaluation et de suppression de serveurs sont simples et claires.

Retour au début

## Exemples de code en masques de bits et en valeur absolue

Cette section présente un exemple de codes d'état retournés par la plupart des fournisseurs de listes bloquées. Pour plus d'informations sur les codes d'état qu'un fournisseur renvoie, consultez la documentation de ce fournisseur.

Pour les données de type masque de bits, le service fournisseur de listes d'adresses IP bloquées retourne le code d'état 127.0.0.*x*, où le nombre entier *x* est l'une des valeurs indiquées dans le tableau suivant.

### Valeurs et codes d'état pour les données de type masque de bits

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur</th>
<th>Code d'état</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>L'adresse IP figure dans une liste d'adresses IP bloquées.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Le serveur SMTP est configuré pour agir comme un relais ouvert.</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>L'adresse IP prend en charge une adresse IP d'appel.</p></td>
</tr>
</tbody>
</table>


Avec le type valeur absolue, le fournisseur de listes d’adresses IP bloquées renvoie des réponses explicites qui définissent la raison pour laquelle l’adresse IP est répertoriée dans leurs listes d’adresses IP bloquées. Le tableau suivant présente des exemples de valeurs absolues et les réponses explicites.

### Valeurs et codes d'état pour les données de type valeur absolue

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur</th>
<th>Réponse explicite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>127.0.0.2</p></td>
<td><p>L'adresse IP est une source de courrier indésirable direct.</p></td>
</tr>
<tr class="even">
<td><p>127.0.0.4</p></td>
<td><p>L'adresse IP est un expéditeur de courrier non sollicité.</p></td>
</tr>
<tr class="odd">
<td><p>127.0.0.5</p></td>
<td><p>Le serveur distant qui expédie le message est connu pour prendre en charge des relais ouverts multiniveau.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Fournisseurs de listes d'adresses IP autorisées

Les fournisseurs de listes d’adresses IP autorisées sont également appelés *listes vertes* ou *listes d’expéditeurs certifiés*. Les fournisseurs de listes d’adresses IP autorisées se configurent de la même manière que les fournisseurs de listes d’adresses IP bloquées, mais avec des résultats inverses : ils répertorient les adresses IP de serveurs de messagerie n’ayant aucun lien avec des activités d’envoi de courrier indésirable. Si l’adresse IP du serveur de messagerie expéditeur se trouve dans un fournisseur de listes d’adresses IP autorisées, le message n’est pas traité par d’autres agents de blocage du courrier indésirable Exchange. Pour cette raison, les fournisseurs de listes d’adresses IP bloquées sont utilisés beaucoup plus fréquemment que les fournisseurs de listes d’adresses IP autorisées. Choisissez soigneusement votre fournisseur de listes d’adresses IP autorisées.

Retour au début

## Test des fournisseurs de listes d’adresses IP autorisées et des fournisseurs de listes d’adresses IP bloquées

Une fois que vous avez configuré le filtrage des connexions pour utiliser un fournisseur de listes d’adresses IP bloquées ou de listes d’adresses IP autorisées, vous pouvez effectuer des tests pour vérifier que les fournisseurs fonctionnent correctement. La plupart des fournisseurs fournissent des adresses IP de test que vous pouvez utiliser pour évaluer leurs services. Lorsque vous testez un fournisseur, l’agent de filtrage des connexions émet une requête DNS censée déclencher une réponse spécifique de la part du fournisseur. Pour plus d’informations sur la manière de tester des adresses IP avec un service fournisseur de listes d’adresses IP bloquées ou de listes d’adresses IP autorisées, voir [Gérer le filtrage des connexions sur les serveurs de transport Edge](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

Retour au début

## Configurer le filtrage des connexions sur des serveurs de transport Edge qui ne sont pas directement connectés à Internet.

Vous pouvez utiliser le filtrage des connexions sur des serveurs de transport Edge qui ne reçoivent pas de courrier électronique directement d’Internet. Dans ce scénario, le serveur de transport Edge se trouve derrière un autre serveur de messagerie qui reçoit et traite les messages directement à partir d’Internet. Par exemple, votre organisation peut faire transiter le trafic de messagerie par un serveur, un service ou un dispositif de blocage du courrier indésirable avant que les messages n’atteignent le serveur de transport Edge. Dans ce scénario, l’agent de filtrage des connexions doit extraire la véritable adresse IP d’origine du message. Pour ce faire, il doit analyser les valeurs du champ d’en-tête **Reçu** de l’en-tête de message et comparer ces valeurs aux adresses IP connues du serveur de messagerie se trouvant entre le serveur de transport Edge et Internet.

Chaque serveur de messagerie qui accepte et relaie un message SMTP sur le chemin de remise du message ajoute son propre champ d’en-tête **Reçu** dans l’en-tête du message. L’en-tête **Reçu** contient généralement le nom de domaine et l’adresse IP du serveur de messagerie ayant traité le message.

Si le serveur de transport Edge n’accepte pas les messages directement à partir d’Internet, vous devez utiliser le paramètre *InternalSMTPServers* de la cmdlet **Set-TransportConfig** sur un serveur de messagerie Exchange 2013 pour identifier l’adresse IP du serveur de messagerie qui se trouve entre le serveur de transport Edge et Internet. Les données d'adresse IP sont répliquées sur les serveurs de transport Edge par EdgeSync. Lorsque les messages sont reçus par le serveur de transport Edge, l’agent de filtrage des connexions suppose que les adresses IP du champ d’en-tête **Reçu** qui ne correspondent à aucune valeur spécifiée par le paramètre *InternalSMTPServers* est l’adresse IP source à vérifier. Par conséquent, vous devez spécifier tous les serveurs SMTP internes pour que le filtrage des connexions fonctionne correctement.

Retour au début

