---
title: 'Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013
ms:assetid: 8e91de84-76fa-49b2-898c-c5eface76560
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232118(v=EXCHG.150)
ms:contentKeyID: 50478677
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous avez besoin d’aide concernant les notifications d’échec de remise dans Office 365 ou Exchange Online, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=524931">Envoyer les notifications d’échec de remise par courrier électronique dans Office 365</a>.</td>
</tr>
</tbody>
</table>


Quand un problème de remise de message survient, Exchange Server 2013 envoie une notification d’état de remise à l’expéditeur du message. Ces messages générés par le système sont également appelés notifications de non-remise. Ils contiennent un code d’erreur, les détails techniques sur le problème et parfois les étapes de dépannage pour l’expéditeur du message. Les messages de notification d’échec de remise sont un type courant de notification d’état. Cette rubrique destinée aux administrateurs de messagerie décrit les causes possibles et les solutions pour de nombreux codes d’état de notification d’échec de remise. Elle explique également comment lire et interpréter les messages de notification d’échec de remise.

**Contenu de cette rubrique**

Codes d’état étendus courants

Sections d'un rapport de non-remise

Exemples de messages de rapport de non-remise

## Codes d’état étendus courants

Le tableau suivant contient la liste des codes d'état étendus renvoyés dans des rapports de non-remise pour les échecs de remise de message les plus courants.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Code d'état étendu</th>
<th>Description</th>
<th>Cause possible</th>
<th>Informations supplémentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4.3.1</p></td>
<td><p><code>Insufficient system resources</code></p></td>
<td><p>Une erreur de mémoire insuffisante s'est produite. Un problème de ressource, tel qu'un disque plein, peut être à l'origine du problème.</p>
<p>Plutôt qu’une erreur de disque plein, vous pouvez recevoir une erreur de mémoire insuffisante.</p></td>
<td><p>Vérifiez que votre serveur Exchange dispose d’un espace disque suffisant.</p></td>
</tr>
<tr class="even">
<td><p>4.3.2</p></td>
<td><p><code>System not accepting network messages</code></p></td>
<td><p>Cette notification d'échec de remise est générée lorsqu'une file d'attente est gelée.</p></td>
<td><p>Vous pouvez résoudre le problème en libérant la file d'attente.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.1</p></td>
<td><p><code>Connection timed out</code></p></td>
<td><p>Le serveur de destination ne répond pas. Des problèmes réseau temporaires peuvent être à l’origine de cette erreur. Le serveur Exchange tente automatiquement de rétablir la connexion et de remettre le message. En cas d’échec de la remise après plusieurs tentatives, une notification d’échec de remise avec un code de défaillance permanente est générée.</p></td>
<td><p>Surveillez la situation. Il s’agit peut-être d’un problème passager qui peut se corriger de lui-même.</p></td>
</tr>
<tr class="even">
<td><p>4.4.2</p></td>
<td><p><code>Connection dropped</code></p></td>
<td><p>Une connexion a été abandonnée entre les serveurs. Des problèmes réseau temporaires ou un serveur rencontrant des problèmes peuvent être à l’origine de cette erreur. Le serveur d’envoi tente à nouveau de remettre le message pendant un délai spécifique, puis génère d’autres rapports d’état.</p></td>
<td><p>Surveillez la situation lors des nouvelles tentatives de remise par le serveur. Il s’agit peut-être d’un problème passager qui peut se corriger de lui-même.</p>
<p>Cette situation peut également survenir lorsque la limite de taille de message est atteinte pour la connexion ou si le taux de dépôt de message pour l'adresse IP client a dépassé la limite configurée.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.7</p></td>
<td><p><code>Message expired</code></p></td>
<td><p>Le message dans la file d'attente a expiré. Le serveur d'envoi a tenté de relayer ou de remettre le message mais l'action n'a pas été exécutée avant l'expiration du message. Ce message peut également indiquer qu'une limite d'en-tête de message a été atteinte sur un serveur distant ou qu'un protocole a expiré lors de la communication avec le serveur distant.</p></td>
<td><p>Ce message indique généralement un problème sur le serveur de réception. Vérifiez la validité de l'adresse de destinataire et déterminez si le serveur de réception est correctement configuré pour recevoir des messages.</p>
<p>Il se peut que vous deviez réduire le nombre de destinataires dans l’en-tête de message pour l’hôte concerné par l’erreur. Si vous renvoyez le message, il est placé à nouveau dans la file d’attente. Si le serveur de réception est disponible, le message est remis.</p></td>
</tr>
<tr class="even">
<td><p>5.0.0</p></td>
<td><p><code>HELO / EHLO requires domain address</code></p></td>
<td><p>Cette situation correspond à une défaillance permanente. Les causes possibles sont les suivantes :</p>
<ul>
<li><p>Il n'y a pas d'itinéraire pour l'espace d'adressage donné. Par exemple, un connecteur SMTP est configuré mais l'adresse ne correspond pas.</p></li>
<li><p>Le serveur DNS a renvoyé un hôte faisant autorité introuvable pour le domaine.</p></li>
<li><p>Une erreur SMTP s'est produite.</p></li>
</ul></td>
<td><p>Voici des solutions potentielles :</p>
<ul>
<li><p>Sur un ou plusieurs connecteurs SMTP, ajoutez un astérisque (<strong>*</strong>) en tant qu’espace d’adressage SMTP.</p></li>
<li><p>Vérifiez que le serveur DNS fonctionne.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>5.1.0</p></td>
<td><p><code>Sender denied</code></p></td>
<td><p>Cette notification d’échec de remise est liée à une défaillance générale (échec lié à une adresse erronée). Une adresse de messagerie ou un autre attribut est introuvable dans les services de domaine Active Directory. Les entrées de contact sans attribut <strong>targetAddress</strong> défini peuvent provoquer ce problème. Une autre cause possible peut être que l’attribut <strong>homeMDB</strong> d’un utilisateur n’a pas pu être déterminé. L’attribut <strong>homeMDB</strong> correspond au serveur Exchange sur lequel réside la boîte aux lettres de l’utilisateur.</p>
<p>Autre cause courante de cette notification d’échec de remise : vous utilisez Microsoft Outlook pour enregistrer un message électronique en tant que fichier, puis un utilisateur ouvre le message hors ligne et y répond. La propriété de message conserve uniquement l’attribut <strong>legacyExchangeDN</strong> lorsqu’Outlook remet le message. Il est donc possible que la recherche ait échoué.</p></td>
<td><p>L'adresse du destinataire n'est pas correctement mise en forme ou le destinataire n'a pas pu être correctement résolu. La première étape de la résolution de cette erreur consiste à vérifier l'adresse du destinataire et à renvoyer le message.</p></td>
</tr>
<tr class="even">
<td><p>5.1.1</p></td>
<td><p><code>Bad destination mailbox address</code></p></td>
<td><p>Cet échec peut résulter des situations suivantes :</p>
<ul>
<li><p>L’adresse de messagerie du destinataire entrée par l’expéditeur est incorrecte.</p></li>
<li><p>Il n’y a pas de destinataire dans le système de messagerie de destination.</p></li>
<li><p>La boîte aux lettres du destinataire a été déplacée et le cache de destinataires Outlook sur l’ordinateur de l’expéditeur n’a pas été mis à jour.</p></li>
<li><p>Un nom de domaine hérité non valide existe pour les services de domaine de la boîte aux lettres Active Directory du destinataire.</p></li>
</ul></td>
<td><p>Cette erreur se produit généralement lorsque l’adresse de messagerie du destinataire entrée par l’expéditeur du message est incorrecte. L'expéditeur doit vérifier l’adresse de messagerie du destinataire et renvoyer le message. Cette erreur peut également se produire si l’adresse de messagerie du destinataire était correcte dans le passé, mais a été modifiée ou supprimée du système de messagerie de destination.</p>
<p>Si l’expéditeur du message se trouve dans la même organisation Exchange que le destinataire et que la boîte aux lettres du destinataire existe encore, déterminez si la boîte aux lettres du destinataire a été déplacée vers un nouveau serveur de messagerie. Si c’est le cas, il se peut qu’Outlook n’ait pas correctement mis à jour le cache de destinataires. Demandez à l’expéditeur de supprimer l’adresse du destinataire du cache de destinataires Outlook de l’expéditeur, puis de créer un nouveau message. Le renvoi du message original entraîne le même échec.</p>
<p>D’autres problèmes peuvent générer cette erreur, par exemple la présence d’un nom unique hérité non valide dans les services de domaine Active Directory. Examinez et corrigez l’ancien nom unique de la boîte aux lettres du destinataire. Demandez à l’expéditeur de supprimer l’adresse du destinataire du cache de destinataires Outlook de l’expéditeur, puis de créer un nouveau message. Le renvoi du message original entraîne le même échec.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.2</p></td>
<td><p><code>Invalid X.400 address</code></p></td>
<td><p>Le destinataire a une adresse autre que SMTP pour laquelle aucune destination correspondante n'a été trouvée. L'adresse ne semble pas être locale et aucun connecteur n'est configuré avec des espaces d'adressage contenant l'adresse du destinataire.</p></td>
<td><p>Vérifiez que l’adresse du destinataire a été entrée correctement. Si l’adresse du destinataire figure dans un système de messagerie autre que SMTP auquel vous souhaitez remettre des messages spécifiquement, vous devez ajouter le type de connecteur approprié à votre topologie et le configurer pour assurer le service auprès du système de messagerie du destinataire.</p></td>
</tr>
<tr class="even">
<td><p>5.1.3</p></td>
<td><p><code>Invalid recipient address</code></p></td>
<td><p>Ce message indique que l’adresse du destinataire n’apparaît pas correctement dans le message.</p></td>
<td><p>L’adresse du destinataire n’est pas correctement mise en forme ou l’adresse du destinataire n’a pas pu être correctement résolue. La première étape de la résolution de cette erreur consiste à vérifier l’adresse du destinataire et à renvoyer le message.</p>
<p>Examinez la stratégie de destinataire SMTP et vérifiez que chaque domaine de messagerie pour lequel vous voulez accepter des messages apparaît correctement.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.4</p></td>
<td><p><code>Destination mailbox address ambiguous</code></p></td>
<td><p>Au moins deux destinataires au sein de l’organisation Exchange ont la même adresse.</p></td>
<td><p>Cette erreur se produit généralement suite à une mauvaise configuration dans les services de domaine Active Directory. Il se peut que, suite à des problèmes de réplication, deux objets destinataires dans les services de domaine Active Directory aient la même adresse SMTP ou adresse Exchange Server (EX).</p></td>
</tr>
<tr class="even">
<td><p>5.1.7</p></td>
<td><p><code>Invalid address</code></p></td>
<td><p>L’adresse SMTP de l’expéditeur est absente ou son format est incorrect, ou l’attribut <strong>mail</strong> n’est pas valide dans le service d’annuaire. L’élément de messagerie ne peut pas être remis sans attribut <strong>mail</strong> valide.</p></td>
<td><p>Vérifiez la structure d’annuaire de l’expéditeur et déterminez si l’attribut <strong>mail</strong> existe.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.1</p></td>
<td><p><code>Mailbox cannot be accessed</code></p></td>
<td><p>La boîte aux lettres est inaccessible. Il se peut que la boîte aux lettres soit hors ligne ou désactivée, ou que le message ait été mis en quarantaine par une règle.</p></td>
<td><p>Vérifiez que la base de données du destinataire est en ligne, que la boîte aux lettres du destinataire est désactivée ou que le message a été mis en quarantaine.</p></td>
</tr>
<tr class="even">
<td><p>5.2.2</p></td>
<td><p><code>Mailbox full</code></p></td>
<td><p>Le quota de stockage de la boîte aux lettres du destinataire étant dépassé, celle-ci ne peut plus accepter de nouveaux messages.</p></td>
<td><p>Cette erreur se produit en cas de dépassement du quota de stockage de la boîte aux lettres du destinataire. Pour que la remise réussisse, le destinataire doit réduire la taille de la boîte aux lettres ou l'administrateur doit augmenter le quota de stockage.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.3</p></td>
<td><p><code>Message too large</code></p></td>
<td><p>Le message est trop volumineux et le quota local est dépassé. Par exemple, un utilisateur Exchange distant peut avoir une restriction quant à la taille maximale d’un message entrant.</p></td>
<td><p>Renvoyez le message sans pièce jointe ou définissez la limite du serveur ou côté client pour autoriser une limite de taille de message supérieure.</p></td>
</tr>
<tr class="even">
<td><p>5.2.4</p></td>
<td><p><code>Mailing list expansion problem</code></p></td>
<td><p>Le destinataire correspond à une liste de distribution dynamique mal configurée. La chaîne de filtrage ou le nom unique de base de la liste de distribution dynamique est incorrect(e).</p></td>
<td><p>Définissez le niveau d'enregistrement des événements du catégoriseur sur le niveau minimum, puis envoyez un autre message à la liste de distribution dynamique. Recherchez dans le journal des événements Applications l'événement 6025 ou 6026 qui identifie l'attribut mal configuré dans l'objet liste de distribution dynamique.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.3</p></td>
<td><p><code>Unrecognized command</code></p></td>
<td><p>Ce rapport de non-remise a pu être généré lorsque l’espace disque du serveur Exchange distant a atteint la limite imposée pour le stockage des messages. Cette erreur survient généralement lorsque le serveur d’envoi envoie des messages avec une commande ESMTP BDAT. Cette erreur peut également indiquer une erreur de protocole SMTP.</p></td>
<td><p>Vérifiez que le serveur distant dispose d'une capacité de stockage suffisante pour conserver les messages. Vérifiez le journal SMTP.</p></td>
</tr>
<tr class="even">
<td><p>5.3.4</p></td>
<td><p><code>Message too big for system</code></p></td>
<td><p>La taille du message dépassant la limite de taille configurée sur une base de données de transport ou de boîtes aux lettres, le message ne peut pas être accepté. Cet échec peut être généré par le système de messagerie d’envoi ou par le système de messagerie de réception.</p></td>
<td><p>Cette erreur se produit lorsque la taille du message envoyé par l'expéditeur dépasse la taille de message maximale autorisée lors du transfert via un composant de transport ou une base de données de boîtes aux lettres. Pour que la remise du message réussisse, l'expéditeur doit réduire la taille du message. Pour plus d’informations sur la configuration des limites de taille des messages, consultez la rubrique <a href="message-size-limits-exchange-2013-help.md">Tailles limites des messages</a>.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.5</p></td>
<td><p><code>System incorrectly configured</code></p></td>
<td><p>Une situation de boucle de courrier a été détectée, ce qui indique que le serveur est configuré pour envoyer les messages en boucle à lui-même.</p></td>
<td><p>Vérifiez la configuration des connecteurs du serveur en relation avec les boucles et assurez-vous que chaque connecteur est défini par un port entrant unique. S'il y a plusieurs serveurs virtuels, vérifiez qu'aucun d'entre eux n'est défini sur la valeur « Aucune assignation. »</p></td>
</tr>
<tr class="even">
<td><p>5.4.4</p></td>
<td><p><code>Invalid arguments</code></p></td>
<td><p>Cette notification d'échec de remise survient s'il n'y a aucun itinéraire pour la remise des messages ou si le catégoriseur n'a pas pu déterminer la destination du saut suivant.</p></td>
<td><p>Vérifiez que le nom de domaine spécifié est valide et que l’enregistrement de serveur de messagerie (MX) existe.</p></td>
</tr>
<tr class="odd">
<td><p>5.4.6</p></td>
<td><p><code>Routing loop detected</code></p></td>
<td><p>Une erreur de configuration a généré une boucle de courrier électronique. Par défaut, après 20 itérations d’une boucle de courrier électronique, Exchange interrompt la boucle et envoie un rapport de non-remise à l’expéditeur du message.</p></td>
<td><p>Cette erreur se produit lorsque la remise d’un message génère un autre message en réponse. Ce message génère à son tour un troisième message, et ainsi de suite, créant une boucle. Pour éviter l’épuisement des ressources système, Exchange interrompt la boucle de courrier électronique après 20 itérations. Les boucles de courrier sont généralement créées en raison d’une erreur de configuration sur le serveur de messagerie d’envoi et/ou le serveur de messagerie de réception. Vérifiez la configuration des règles de boîte aux lettres du destinataire et de l’expéditeur pour déterminer si le transfert de message automatique est activé.</p></td>
</tr>
<tr class="even">
<td><p>5.5.2</p></td>
<td><p><code>Send hello first</code></p></td>
<td><p>Une erreur SMTP générique survient lorsque des commandes SMTP sont envoyées hors séquence. Par exemple, un serveur tente d'envoyer une commande AUTH (autorisation) avant de s'identifier avec une commande EHLO.</p>
<p>Cette erreur peut également se produire lorsque le disque système est plein.</p></td>
<td><p>Consultez le journal SMTP ou une trace Netmon et vérifiez que l'espace disque et la mémoire virtuelle disponibles sont appropriés.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.3</p></td>
<td><p><code>Too many recipients</code></p></td>
<td><p>Le total combiné des destinataires dans les lignes À, Cc et Cci du message dépasse le nombre total de destinataires autorisé par message.</p></td>
<td><p>Cette erreur se produit lorsque l'expéditeur a inclus trop de destinataires dans le message. L'expéditeur doit réduire le nombre d'adresses de destinataire dans le message ou augmenter le nombre maximal de destinataires autorisé pour permettre la remise du message.</p></td>
</tr>
<tr class="even">
<td><p>5.5.4</p></td>
<td><p><code>Invalid domain name</code></p></td>
<td><p>Le message contient un format d'adresse d'expéditeur ou de destinataire non valide.</p>
<p>Une cause possible est que le format d'adresse du destinataire contient des caractères non conformes aux normes Internet.</p></td>
<td><p>Vérifiez que l’adresse du destinataire ne contient pas de caractères non standard.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.6</p></td>
<td><p><code>Invalid message content</code></p></td>
<td><p>Ce message indique une erreur de protocole possible.</p></td>
<td><p>Recherchez des défaillances éventuelles dans le journal des événements.</p></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Delivery not authorized</code></p></td>
<td><p>L'expéditeur du message n'est pas autorisé à envoyer des messages au destinataire.</p></td>
<td><p>Cette erreur se produit lorsque l'expéditeur tente d'envoyer un message à un destinataire alors qu'il n'est pas autorisé à le faire. Cela se produit fréquemment quand un expéditeur tente d'envoyer des messages à un groupe de distribution configuré pour accepter uniquement des messages de membres de ce groupe de distribution ou d'autres expéditeurs autorisés. L'expéditeur doit demander l'autorisation d'envoyer des messages au destinataire.</p>
<p>Cette erreur peut également se produire si une règle de transport Exchange rejette un message parce que ce dernier réunit les conditions configurées sur la règle de transport.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.1</p></td>
<td><p><code>Unable to relay</code></p></td>
<td><p>Le système de messagerie d’envoi n'est pas autorisé à envoyer un message à un système de messagerie lorsque celui-ci n’est pas la destination finale du message.</p></td>
<td><p>Cette erreur se produit lorsque le système de messagerie d’envoi tente d’envoyer un message anonyme à un système de messagerie de réception qui n’accepte pas les messages destinés au(x) domaine(s) spécifié(s) dans l’adresse d’un ou plusieurs destinataires. Les causes les plus fréquentes de cette erreur sont les suivantes :</p>
<ul>
<li><p>Un tiers tente d’utiliser un système de messagerie de réception pour envoyer du courrier indésirable et le système de messagerie de réception rejette la tentative. En raison de la nature du courrier indésirable, il se peut que l’adresse de messagerie de l’expéditeur ait été falsifiée et que le rapport de non-remise généré ait été envoyé à l’adresse de messagerie de l’expéditeur sans méfiance. Il est difficile d’éviter cette situation.</p></li>
<li><p>Un enregistrement de serveur de messagerie (MX) pour un domaine pointe sur un système de messagerie de réception où ce domaine n'est pas accepté. L’administrateur responsable du nom de domaine spécifique doit corriger l’enregistrement MX et/ou configurer le système de messagerie de réception pour accepter les messages envoyés à ce domaine.</p></li>
<li><p>Un système de messagerie d'envoi ou un client qui devrait utiliser le système de messagerie de réception pour relayer les messages ne dispose pas des autorisations appropriées pour le faire.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Client was not authenticated</code></p></td>
<td><p>Le système de messagerie d’envoi ne s’est pas authentifié auprès du système de messagerie de réception. Le système de messagerie de réception requiert une authentification avant le dépôt du message.</p></td>
<td><p>Cette erreur se produit lorsque le serveur de réception doit être authentifié avant le dépôt du message et le système de messagerie d’envoi ne s’est pas authentifié auprès du système de messagerie de réception. L’administrateur du système de messagerie d’envoi doit configurer le système pour s’authentifier auprès du système de messagerie de réception pour que la remise réussisse. Cette erreur peut également se produire si vous tentez d’accepter des messages anonymes en provenance d’Internet en utilisant un serveur de messagerie qui n’est pas configuré pour le faire.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.3</p></td>
<td><p><code>Not Authorized</code></p></td>
<td><p>L'expéditeur a interdit la réaffectation à l'autre destinataire.</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


Retour au début

## Sections d'un rapport de non-remise

Dans Exchange 2013, les rapports de non-remise sont conçus pour être faciles à lire et à comprendre par les utilisateurs finaux et les administrateurs. Les informations qui s’affichent dans un rapport de non-remise sont réparties dans les deux zones suivantes :

  - Une section des informations utilisateur

  - Une banque d’informations Administrateur

Les informations figurant dans chaque section sont ciblées pour les lecteurs de cette section. La section des informations utilisateur apparaît en premier et contient des commentaires permettant à l’utilisateur de comprendre, en termes non techniques, pourquoi la remise du message a échoué. La section **Informations de diagnostic pour les administrateurs** fournit des informations techniques plus approfondies comme les en-têtes du message d’origine, pour permettre aux administrateurs de messagerie de diagnostiquer et de dépanner un problème de remise. La figure suivante présente la section des informations utilisateur et la section **Informations de diagnostic pour les administrateurs** d’un rapport de non-remise.

**Sections d'un rapport de non-remise**

![Notification d’échec de remise affichant des informations de diagnostic utilisateur et administrateur](images/Bb232118.96245455-5fb9-4669-a931-5563ddd3ab35(EXCHG.150).png "Notification d’échec de remise affichant des informations de diagnostic utilisateur et administrateur")

## Section des informations utilisateur

La section des informations utilisateur d’un rapport de non-remise généré par Exchange contient les informations que vous voulez communiquer à un utilisateur final qui a envoyé un message renvoyé par la suite avec un rapport de non-remise. Le texte qui s’affiche dans cette section est inséré par le serveur Exchange ayant généré le rapport de non-remise.

Le texte de la section des informations utilisateur est conçu pour permettre à l’utilisateur final de déterminer pourquoi le message a été rejeté et comment renvoyer le message correctement, s’il faut le renvoyer. Le cas échéant, le nom de domaine complet (FQDN) du serveur qui a rejeté le message est inclus dans la section des informations utilisateur. En cas d’échec de la remise à plusieurs destinataires, l’adresse de messagerie de chacun d’eux est indiquée et le motif de l’échec est mentionné dans l’espace situé sous l’adresse de messagerie du destinataire.

Vous pouvez modifier le texte de la section des informations utilisateur à l’aide de la cmdlet **New-SystemMessage**. En créant un message personnalisé, vous pouvez fournir à des utilisateurs finals des informations spécifiques, comme un numéro de téléphone à utiliser pour contacter le service d’assistance ou un lien hypertexte à utiliser pour accéder à un support en libre-service.

Retour au début

## Informations de diagnostic pour les administrateurs

La section **Informations de diagnostic pour les administrateurs** contient des informations plus détaillées sur l'erreur spécifique qui s'est produite durant la remise du message, le serveur ayant généré le rapport de non-remise et le serveur ayant rejeté le message. La plupart des rapports de non-remise contiennent les champs suivants, qui sont visibles dans la figure « Sections d'un rapport de non-remise » ci-avant dans cette rubrique :

  - **Serveur de génération**   Le serveur de génération est le serveur SMTP ayant créé le rapport de non-remise. Le serveur de génération prend le code d’état étendu décrit ci-après dans cette rubrique. Ce code crée un rapport de non-remise facile à lire. Si aucun serveur distant ne figure sous l’adresse de messagerie de l’expéditeur plus loin dans la section **Informations de diagnostic pour les administrateurs**, le serveur de génération est également le serveur ayant rejeté le message électronique d’origine. En cas d’échec de la remise d’un message lors de l’envoi de ce dernier à un autre destinataire au sein de l’organisation Exchange, généralement, le même serveur rejette le message d’origine et génère le rapport de non-remise.

  - **Destinataire rejeté**   Le destinataire rejeté est indiqué par l’adresse de messagerie du destinataire auprès duquel la remise du message d’origine a échoué. En cas d’échec de la remise à plusieurs destinataires, l’adresse de messagerie de chacun d’eux est indiquée. Le champ du destinataire rejeté contient également les sous-champs suivants pour chaque adresse de messagerie répertoriée :
    
      - **Serveur distant**   Le champ du serveur distant indique le nom de domaine complet (FQDN) du serveur ayant rejeté la remise du message durant la conversation SMTP. Le champ du serveur distant n'est renseigné que lorsqu'une remise à un serveur distant a été tentée et que la tentative de remise a été rejetée avant que le serveur de réception n'accuse réception du message après l'envoi du corps de celui-ci. Si le serveur de réception accuse réception du message original et si le message est ensuite rejeté, par exemple, en raison de restrictions de contenu, le champ du serveur distant n'est pas renseigné.
    
      - **Code d’état étendu**   Le code d’état étendu est le code renvoyé par le serveur ayant rejeté le message original. Le code d’état étendu indique le motif du rejet du message original. Le code d’état étendu n’est pas réécrit par Exchange, mais utilisé pour déterminer la nature du texte à afficher dans la section des informations utilisateur. Les codes d’état étendus les plus fréquents sont répertoriés dans la section « Codes d’état étendus courants », ci-après dans cette rubrique. Pour obtenir la liste détaillée des codes d’état étendus, consultez le standard RFC 3463.
    
      - **Réponse SMTP**   La réponse SMTP est le texte codé renvoyé par le serveur ayant rejeté le message original. La réponse SMTP contient généralement une chaîne courte fournissant une explication sur le code d’état étendu également renvoyé. La réponse SMTP n’est pas réécrite par Exchange. En outre, cette réponse est toujours présentée en code US-ASCII.

  - **En-têtes de message originaux**   La section des en-têtes de message originaux contient les en-têtes du message rejeté. Ces en-têtes peuvent fournir des informations de diagnostic utiles, comme des informations permettant de déterminer le chemin parcouru par le message avant son rejet ou si le contenu du champ **À** correspond à l’adresse de messagerie spécifiée dans le champ du destinataire rejeté.

Retour au début

## Exemples de messages de rapport de non-remise

Les sections suivantes fournissent des exemples des deux méthodes de génération de messages de rapport de non-remise :

  - par le même serveur

  - par des serveurs différents

## Rapport de non-remise généré et message d’origine rejeté par le même serveur

L'exemple suivant montre ce qui se passe lorsqu’une organisation de messagerie distante accepte la remise d’un message électronique via un serveur de transport Edge, puis rejette ce message en raison d’une restriction de stratégie sur la boîte aux lettres du destinataire. Dans ce cas, l'expéditeur n'est pas autorisé à envoyer des messages au destinataire. Les serveurs de transport Edge n'effectuant pas de validation de la taille des messages, le serveur de transport Edge dans cet exemple accepte le message parce que l'adresse du destinataire est valide et que le message ne viole pas les restrictions de contenu. Parce que l’organisation de messagerie distante accepte le message entier, y compris son contenu, cette organisation est responsable du rejet du message et de la génération du message de rapport de non-remise à envoyer à l’expéditeur.

**Rapport de non-remise généré et message rejeté par le même serveur**

![Notification d’échec de remise indiquant des serveurs de génération/de rejet identiques](images/Bb232118.c9a7cd2d-f35f-4d77-8225-c29585fa3ccd(EXCHG.150).gif "Notification d’échec de remise indiquant des serveurs de génération/de rejet identiques")

En outre, les messages rejetés lors de leur envoi à des destinataires faisant partie de la même organisation Exchange sont généralement rejetés par le même serveur de messagerie qui génère le message de rapport de non-remise. Les messages envoyés à des destinataires locaux peuvent être rejetés pour diverses raisons, comme un dépassement du quota de boîte aux lettres, une absence d’autorisation d’envoi de messages au destinataire titulaire de l’adresse ou des défaillances matérielles entraînant une perte importante de connectivité avec d’autres serveurs au sein de l’organisation.

Dans les deux cas, aucun serveur distant n’est indiqué sous l’adresse de messagerie des destinataires répertoriés dans le message de rapport de non-remise.

Retour au début

## Rapport de non-remise généré et message d'origine rejeté par des serveurs différents

L’exemple suivant montre ce qui se passe lorsqu’une organisation de messagerie distante rejette la remise d’un message électronique avant même d’avoir accepté le message. Dans cet exemple, le serveur distant rejette le message et renvoie un code d'état étendu au serveur d'envoi local parce que le destinataire spécifié n'existe pas. Le rejet intervient avant que le serveur de réception accuse réception du message. Comme le serveur de réception n'accuse pas réception du message, il n'est pas responsable du message. C'est pourquoi le serveur d'envoi local génère le message de rapport de non-remise et l'envoie à l'expéditeur du message original.

**Rapport de non-remise généré et message rejeté par des serveurs différents**

![Notification d’échec de remise indiquant différents serveurs de génération/d’envoi](images/Bb232118.adfb8d5a-9c1d-4cd9-8a71-ce14224434f8(EXCHG.150).gif "Notification d’échec de remise indiquant différents serveurs de génération/d’envoi")

Retour au début

## Voir aussi


[Notifications d’échec de remise dans Exchange Online et Office 365](https://go.microsoft.com/fwlink/p/?linkid=524931)

