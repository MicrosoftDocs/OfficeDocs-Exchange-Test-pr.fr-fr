---
title: 'Règles de transport ou de flux de messagerie: Exchange 2013 Help'
TOCTitle: Règles de flux de messagerie (règles de transport)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50479117
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Règles de transport ou de flux de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-04-28_

Vous pouvez utiliser des règles de flux de messagerie (également appelées règles de transport) pour identifier les messages qui transitent par votre organisation Exchange 2013 et agir sur ceux-ci. Les règles de flux de messagerie sont semblables aux règles de boîte de réception disponibles dans Outlook et Outlook Web App. La principale différence réside dans le fait que les règles de flux de messagerie agissent sur les messages pendant qu’ils sont en transit, et non une fois qu’ils ont été remis dans la boîte aux lettres. Les règles de flux de messagerie contiennent un plus vaste ensemble de conditions, d’exceptions et d’actions, ce qui vous offre plus de souplesse pour mettre en place plusieurs types de stratégies de messagerie.

Cet article décrit les composants des règles de flux de messagerie et leur fonctionnement.

Pour plus d’informations sur les règles de flux de messagerie dans Exchange Online, consultez la rubrique [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)). Pour plus d’informations sur les règles de flux de messagerie dans Exchange Online Protection, consultez la rubrique [Règles de flux de messagerie (règles de transport) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/dn271424\(v=exchg.150\)).

Vous pouvez utiliser le Centre d’administration Exchange (CAE) ou Environnement de ligne de commande Exchange Management Shell pour gérer les règles de flux de messagerie. Pour savoir comment gérer les règles de transport, reportez-vous à la rubrique [Gestion de règles de flux de messagerie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

Pour chaque règle, vous avez la possibilité de l’appliquer, de la tester ou bien de la tester et d’avertir l’expéditeur. Pour plus d’informations sur les options de test, voir [Tester une règle de flux de messagerie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules) et [Conseils de stratégie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/policy-tips).

Pour mettre en œuvre des stratégies de messagerie spécifiques à l’aide de règles de flux de messagerie, consultez ces rubriques :

  - [Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Scénarios courants de blocage de pièce jointe](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Utiliser des règles de flux de messagerie afin que les messages puissent contourner le courrier non trié](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [Utiliser des règles de flux de messagerie pour acheminer le courrier électronique en fonction d’une liste de mots, d’expressions ou de modèles](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [Scénarios courants d’approbation des messages](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios)

## Composants de règle de flux de messagerie

Une règle de flux de messagerie est constituée de conditions, d’exceptions, d’actions et de propriétés :

  - **Conditions**   Identifient les messages auxquels que vous souhaitez appliquer les actions. Certaines conditions examinent les champs d’en-tête de message (par exemple, les champs À, De ou Cc). D’autres examinent les propriétés des messages (par exemple l’objet, le corps, les pièces jointes, la taille ou la classification du message). La plupart des conditions font appel à un opérateur de comparaison (par exemple, « égal à », « différent de » ou « contient ») ainsi qu’à une valeur de concordance que vous devez spécifier. S’il n’y a ni conditions ni d’exceptions, la règle s’applique à tous les messages.
    
    Pour en savoir plus sur les conditions des règles de flux de messagerie dans Exchange 2013, consultez la rubrique [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

  - **Exceptions**   Identifient éventuellement les messages auxquels les actions ne doivent pas s’appliquer. Les identificateurs de message disponibles dans les conditions le sont également dans les exceptions. Les exceptions ont la priorité sur les conditions et empêchent l’application d’actions à un message, même s’il remplit toutes les conditions configurées.

  - **Actions**   Spécifient que faire des messages qui remplissent les conditions de la règle et qui ne correspondent à aucune des exceptions. De nombreuses actions sont possibles, notamment le rejet, la suppression ou la redirection de messages, l’ajout de destinataires supplémentaires, l’ajout de préfixes à l’objet des messages ou l’insertion de clauses d’exclusion de responsabilité dans le corps des messages.
    
    Pour plus d’informations sur les actions des règles de flux de messagerie dans Exchange 2013, consultez la rubrique [Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

  - **Propriétés** Spécifient d’autres paramètres de règles qui ne sont pas des conditions, des exceptions ou des actions. Par exemple, lorsque la règle doit être appliquée, les propriétés indiquent s’il faut appliquer ou tester la règle, ainsi que la période de temps sur laquelle la règle reste active.
    
    Pour plus d’informations, consultez la section Propriétés des règles de flux de messagerie dans cette rubrique.

## Plusieurs conditions, exceptions et actions

Le tableau suivant explique comment plusieurs conditions, valeurs de condition, exceptions et actions sont traitées dans une règle.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant</th>
<th>Logique</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plusieurs conditions</p></td>
<td><p>AND</p></td>
<td><p>Un message doit remplir toutes les conditions de la règle. Si vous souhaitez qu’une condition ou une autre s’applique, utilisez des règles distinctes pour chaque condition. Par exemple, si vous souhaitez ajouter la même clause d’exclusion de responsabilité aux messages comportant des pièces jointes et aux messages contenant un texte spécifique, créez une règle pour chaque condition. Vous pouvez facilement copier une règle dans le CAE.</p></td>
</tr>
<tr class="even">
<td><p>Une condition avec plusieurs valeurs</p></td>
<td><p>OR</p></td>
<td><p>Certaines conditions vous permettent de spécifier plusieurs valeurs. Le message doit correspondre à l’une des valeurs spécifiées (pas toutes). Par exemple, si l’objet d’un message électronique est <strong>Informations sur le cours des actions</strong> et que la condition <strong>L’objet inclut l’un de ces mots</strong> est configurée pour établir une correspondance avec le mot <strong>Contoso</strong> ou <strong>actions</strong>, la condition est remplie, car l’objet du message contient au moins l’une des valeurs spécifiées.</p></td>
</tr>
<tr class="odd">
<td><p>Plusieurs exceptions</p></td>
<td><p>OR</p></td>
<td><p>Si un message établit une correspondance avec l’une des exceptions, les actions ne sont pas appliquées. Le message ne doit pas forcément correspondre à toutes les exceptions.</p></td>
</tr>
<tr class="even">
<td><p>Plusieurs actions</p></td>
<td><p>AND</p></td>
<td><p>Les messages qui répondent aux conditions d’une règle permettent d’obtenir toutes les actions qui sont spécifiées dans la règle. Par exemple, si les actions <strong>Ajouter à l’objet du message le préfixe</strong> et <strong>Ajouter des destinataires au champ Cci</strong> sont sélectionnées, les deux actions sont appliquées au message.</p>
<p>Souvenez-vous que certaines actions, telles que <strong>Supprimer le message sans avertir personne</strong>, empêchent l’application des règles suivantes à un message. D’autres actions telles que <strong>Transférer le message</strong> ne permettent pas d’actions supplémentaires.</p>
<p>Vous pouvez également définir une action sur une règle de sorte que lorsque cette règle est appliquée, les règles suivantes ne sont pas appliquées au message.</p></td>
</tr>
</tbody>
</table>


Composants de règle de flux de messagerie

## Propriétés de règle de flux de messagerie

Le tableau suivant décrit les propriétés de règle qui sont disponibles dans les règles de flux de messagerie.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de la propriété dans le CAE</th>
<th>Nom du paramètre dans PowerShell</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Priorité</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>Indique l’ordre dans lequel les règles sont appliquées aux messages. La priorité par défaut est définie en fonction de la date de création de la règle (les règles plus anciennes ont une priorité plus élevée que les règles plus récentes et les règles haute priorité sont traitées avant les règles basse priorité).</p>
<p>Vous modifiez la priorité de la règle dans le CAE en la déplaçant vers le haut ou le bas de la liste des règles. Dans l’PowerShell, vous définissez le numéro de priorité (0 représente la priorité la plus élevée).</p>
<p>Par exemple, si vous disposez d’une règle qui rejette les messages dans lesquels figure un numéro de carte de crédit et d’une autre règle qui exige une approbation, vous voudrez certainement que la règle de rejet soit appliquée en premier et que les autres règles ne s’appliquent pas.</p>
<p>Pour plus d’informations, voir <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules">Définir la priorité des règles de flux de messagerie</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mode</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>Vous pouvez spécifier si vous souhaitez que la règle commence immédiatement le traitement des messages ou si vous souhaitez tester les règles sans affecter la remise du message (avec ou sans prévention contre la perte de données ou conseils de stratégie DLP).</p>
<p>Les conseils de stratégie affichent une courte note dans Outlook ou Outlook sur le web afin d’avertir une personne créant un message de possibles violations de stratégie. Pour plus d’informations, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/policy-tips">Conseils de stratégie</a>.</p>
<p>Pour plus d’informations sur les modes, voir <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules">Tester une règle de flux de messagerie</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Activer cette règle à la date suivante</strong></p>
<p><strong>Désactiver cette règle à la date suivante</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>Spécifie la plage de dates au cours de laquelle la règle est active.</p></td>
</tr>
<tr class="even">
<td><p>Case à cocher <strong>Activé</strong> sélectionnée ou non</p></td>
<td><p>Nouvelles règles : paramètre <em>Enabled</em> avec la cmdlet <strong>New-TransportRule</strong>.</p>
<p>Règles existantes : Utilisez les cmdlets <strong>Enable-TransportRule</strong> ou <strong>Disable-TransportRule</strong>.</p>
<p>La valeur est affichée dans la propriété <strong>State</strong> de la règle.</p></td>
<td><p>Vous pouvez créer une règle désactivée, puis l’activer lorsque vous êtes prêt à la tester. Vous pouvez également désactiver une règle sans la supprimer pour en conserver les paramètres.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Différer le message si le traitement de la règle ne se termine pas</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>Vous pouvez spécifier la manière dont le message doit être pris en charge si le traitement des règles ne se termine pas. Par défaut, la règle est ignorée, mais vous pouvez choisir de renvoyer ce message en vue de son traitement.</p></td>
</tr>
<tr class="even">
<td><p><strong>Faire correspondre l’adresse de l’expéditeur dans le message</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Si la règle utilise des conditions ou des exceptions qui examinent l’adresse de messagerie de l’expéditeur, vous pouvez rechercher la valeur dans l’en-tête du message, dans l’enveloppe du message ou dans les deux.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ne plus traiter de règles</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Il s’agit d’une action de la règle, mais celle-ci ressemble à une propriété dans le CAE. Vous pouvez décider d’arrêter d’appliquer des règles à un message après qu’il a été traité par une règle.</p></td>
</tr>
<tr class="even">
<td><p><strong>Commentaires</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>Vous pouvez entrer des commentaires descriptifs sur la règle.</p></td>
</tr>
</tbody>
</table>


Revenir au début

## Application des règles de flux de messagerie au courrier électronique

Tous les messages qui transitent par votre organisation sont évalués par rapport aux règles de flux de messagerie activées de celle-ci. Les règles sont traitées dans l’ordre indiqué sur la page **Flux de messagerie** \> **Règles** du Centre d’administration Exchange ou selon la valeur du paramètre *Priority* correspondant dans l’PowerShell.

Chaque règle offre également la possibilité d’arrêter le traitement des autres règles lorsqu’elle détecte une correspondance. Ce paramètre est important pour les messages qui répondent aux conditions de plusieurs règles de flux de messagerie (quelle règle souhaitez-vous appliquer au message ? Toutes ? Une seule ?).

## Différences de traitement selon le type de message

Plusieurs types de messages transitent par une organisation. Le tableau suivant montre ceux qui peuvent être traités par les règles de flux de messagerie.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de message</th>
<th>Une règle peut-elle être appliquée ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Messages ordinaires</strong> Il s’agit soit de messages contenant un corps de message au format RTF, HTML ou texte brut, soit de messages en plusieurs parties ou composés d’autres ensembles de corps de message.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiffrement de messages Office 365</strong>    Messages chiffrés par Chiffrement de messages Office 365 dans Office 365. Pour plus d’informations, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=39252">Chiffrement dans Office 365</a>.</p></td>
<td><p>Les règles peuvent toujours accéder aux en-têtes des enveloppes contenus dans des messages protégés et traiter les messages en se basant sur les conditions qui analysent les en-têtes.</p>
<p>Pour qu’une règle examine ou modifie le contenu d’un message chiffré, vous devez vérifier que le déchiffrement du transport est activé (Obligatoire ou Facultatif ; la valeur par défaut est Facultatif). Pour plus d’informations, consultez la rubrique relative à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=84806">activation ou la désactivation du déchiffrement du transport</a>.</p>
<p>Vous pouvez également créer une règle qui déchiffre automatiquement les messages chiffrés. Pour en savoir plus, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=40284">Définir des règles pour chiffrer ou déchiffrer des messages électroniques</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messages chiffrés S/MIME</strong></p></td>
<td><p>Les règles peuvent uniquement accéder aux en-têtes d’enveloppe et traiter les messages en fonction de conditions qui inspectent ces en-têtes.</p>
<p>Les règles avec conditions qui requièrent l’inspection du contenu des messages ou les actions qui modifient le contenu des messages ne peuvent pas être traitées.</p></td>
</tr>
<tr class="even">
<td><p><strong>Messages protégés par RMS</strong>   Messages auxquels était appliquée une stratégie Services AD RMS (Active Directory Rights Management Services) (AD RMS) ou Azure Rights Management (RMS).</p></td>
<td><p>Les règles peuvent toujours accéder aux en-têtes des enveloppes contenus dans des messages protégés et traiter les messages en se basant sur les conditions qui analysent les en-têtes.</p>
<p>Pour qu’une règle examine ou modifie le contenu d’un message protégé par RMS, vous devez vérifier que le déchiffrement du transport est activé (Obligatoire ou Facultatif ; la valeur par défaut est Facultatif). Pour plus d’informations, consultez la rubrique relative à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=84806">activation ou la désactivation du déchiffrement du transport</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messages signés en clair</strong> Messages signés, mais non chiffrés.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Messages de messagerie unifiée</strong> Il s’agit de messages créés ou traités par le service de messagerie unifiée, tels que les messages vocaux, les télécopies, les notifications d’appels manqués et les messages créés ou transférés à l’aide de Microsoft Outlook Voice Access.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messages anonymes</strong>   Messages envoyés par des expéditeurs anonymes.</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapports de lecture</strong>   Il s’agit des rapports générés en réponse aux demandes de confirmation de lecture des expéditeurs. Les rapports de lecture sont associés à une classe de message <code>IPM.Note*.MdnRead</code> ou <code>IPM.Note*.MdnNotRead</code>.</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


## Règles de transport et appartenance aux groupes

Lorsque vous définissez une règle de transport à l’aide d’une condition qui développe l’appartenance à un groupe de distribution, la liste des destinataires obtenue est mise en cache par le service de transport sur le serveur de boîte aux lettres qui applique la règle. Il s'agit du *cache des groupes étendus*. L'agent de journalisation s'en sert également pour évaluer l'appartenance au groupe des règles de journalisation. Par défaut, le cache des groupes étendus stocke l'appartenance au groupe pendant quatre heures. Les destinataires retournés par le filtre de destinataires d'un groupe de distribution dynamique y sont également stockés. Le cache des groupes étendus effectue des parcours circulaires répétés vers Active Directory et le trafic réseau résultant de la résolution des appartenances aux groupes jugées non nécessaires.

Dans Exchange 2013, cet intervalle et d'autres paramètres liés au cache des groupes étendus sont configurables. Vous pouvez réduire l'intervalle d'expiration du cache ou désactiver le cache pour vous assurer que les appartenances au groupe sont actualisées plus fréquemment. Vous devez planifier l'augmentation de charge induite sur les contrôleurs de domaine Active Directory afin que les requêtes d'extension des groupes de distribution puissent être traitées. Vous pouvez également effacer le cache sur un serveur de boîtes aux lettres en redémarrant le service de transport Microsoft Exchange exécuté sur ce serveur. Ce redémarrage doit impérativement être effectué sur tous les serveurs de boîtes aux lettres dont vous souhaitez effacer le cache. Lorsque vous créez, testez et corrigez des règles de transport qui font appel à des conditions basées sur une appartenance au groupe de distribution, vous devez également prendre en compte l’impact du cache Groupes développés.

## Stockage et réplication des règles

Les règles de flux de messagerie que vous créez et configurez sur les serveurs de boîte aux lettres sont stockées dans Active Directory et sont lues et appliquées par le service de transport sur tous les serveurs de boîte aux lettres de l’organisation. Lorsque vous créez, modifiez ou supprimez une règle de flux de messagerie, la modification est répliquée entre les contrôleurs de domaine de votre organisation. Cela permet à Exchange de fournir un ensemble cohérent de règles de flux de messagerie dans l’organisation.

**Remarques** :

  - La réplication entre contrôleurs de domaine dépend de facteurs qui ne sont pas contrôlés par Exchange (par exemple, le nombre de sites Active Directory et la vitesse des segments de réseau). Par conséquent, vous devez tenir compte des délais de réplication lorsque vous implémentez des règles de flux de messagerie au sein de votre organisation. Pour plus d’informations sur la réplication Active Directory, consultez la rubrique [Gestion de la topologie et de la réplication Active Directory avec Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=274904).

  - Chaque serveur de boîte aux lettres met en cache des groupes de distribution développés afin d’éviter de répéter les requêtes Active Directory pour déterminer l’appartenance d’un groupe. Par défaut, les entrées dans le cache de groupes développés expirent toutes les quatre heures. Par conséquent, les modifications apportées aux membres du groupe ne sont pas détectées par les règles de flux de messagerie tant que le cache des groupes développé n’est pas mis à jour. Pour forcer une mise à jour immédiate du cache sur un serveur de boîte aux lettres, redémarrez le service de transport Microsoft Exchange. Vous devez redémarrer le service sur chaque serveur de boîte aux lettres sur lequel vous souhaitez forcer la mise à jour du cache.

Les règles de flux de messagerie que vous créez et configurez sur les serveurs de Transport Edge sont stockées dans l’instance locale d’AD LDS sur le serveur. Aucune réplication automatisée des règles de flux de messagerie ne se produit sur les serveurs de transport Edge. Les règles créées sur le serveur de transport Edge s’appliquent uniquement aux messages qui transitent par le serveur local. Si vous devez appliquer le même ensemble de règles de flux de messagerie sur plusieurs serveurs de transport Edge, vous pouvez cloner la configuration du serveur de transport Edge ou exporter et importer les règles de flux de messagerie. Pour plus d’informations, reportez-vous à [Configuration clonée de serveur de transport Edge](edge-transport-server-cloned-configuration-exchange-2013-help.md) et à [Importer ou exporter un regroupement de règles de flux de messagerie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

Chaque fois que le service de transport d’un serveur de boîte aux lettres ou d’un serveur de transport Edge détecte une règle de flux de messagerie modifiée, un événement est enregistré dans le journal d’application dans l’observateur d’événements (ID d’événement 4002 sur des serveurs de boîte aux lettres et ID d’événement 16028 sur les serveurs de transport Edge).

## Réplication et stockage des règles dans les environnements mixtes

Il existe deux scénarios communs d’environnement mixte dans Exchange 2013 :

  - **Déploiements hybrides où une partie de votre organisation réside dans UNRESOLVED\_TOKEN\_VAL(Office365)**
    
    Dans un environnement hybride, aucune réplication de règles ne se produit entre votre organisation Exchange locale et UNRESOLVED\_TOKEN\_VAL(Office365). Par conséquent, lorsque vous créez une règle dans Exchange, vous devez créer une règle correspondante dans UNRESOLVED\_TOKEN\_VAL(Office365). Les règles que vous créez dans UNRESOLVED\_TOKEN\_VAL(Office365) sont stockées dans le cloud, tandis que les règles que vous créez en local dans votre organisation sont stockées localement dans Active Directory. Lorsque vous gérez des règles dans un environnement hybride, vous devez maintenir la synchronisation des deux ensembles de règles en apportant des modifications aux deux emplacements ou en effectuant la modification dans l’un des environnements, avant d’exporter les règles, puis de les importer dans l’autre environnement.
    
	> [!IMPORTANT]
    > Même s’il existe de nombreuses similitudes entre les conditions et les actions disponibles dans UNRESOLVED_TOKEN_VAL(Office365) et dans Exchange Server, il existe toutefois des différences. Si vous envisagez de créer la même règle dans les deux emplacements, vérifiez que toutes les conditions et les actions que vous prévoyez d’utiliser sont disponibles. Pour afficher la liste des conditions et des actions disponibles dans UNRESOLVED_TOKEN_VAL(Office365), consultez les rubriques suivantes :
    > <a href="https://technet.microsoft.com/fr-fr/library/jj919235(v=exchg.150)">Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online</a>
    > <a href="https://technet.microsoft.com/fr-fr/library/jj919237(v=exchg.150)">Courrier des actions de règle de flux dans Exchange en ligne</a>


  - **Coexistence avec Exchange 2010 ou Exchange 2007**
    
    Quand vous créez une situation de coexistence avec Exchange 2010 ou Exchange 2007, toutes les règles de flux de messagerie sont stockées dans Active Directory et répliquées dans votre organisation, quelle que soit la version d’Exchange Server utilisée pour créer les règles. Cependant, toutes les règles de flux de messagerie sont associées à la version d’Exchange Server Server utilisée pour les créer et sont stockées dans un conteneur spécifique de la version dans Active Directory. Quand vous déployez Exchange 2013 pour la première fois dans votre organisation, les règles existantes sont importées vers Exchange 2013 dans le cadre du processus d’installation. Toutefois, les modifications apportées par la suite doivent être effectuées avec les deux versions. Par exemple, si vous modifiez une règle existante dans Exchange 2013 (Environnement de ligne de commande Exchange Management Shell ou le CAE), vous devez répliquer la modification dans Exchange 2010 (Environnement de ligne de commande Exchange Management Shell ou le UNRESOLVED\_TOKEN\_VAL(exEMC)). Sinon, vous pouvez exporter les règles depuis Exchange 2013 et les importer dans Exchange 2010.
    
    Exchange 2010 ne peut pas traiter les règles dont la valeur **Version** ou **RuleVersion** est 15.*n*.*n*.*n*. Pour vous assurer que toutes vos règles peuvent être traitées, utilisez uniquement des règles qui ont la valeur 14.*n*.*n*.*n*.

## Pour plus d'informations

[Gestion de règles de flux de messagerie](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)

[Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Agents de transport](transport-agents-exchange-2013-help.md)

