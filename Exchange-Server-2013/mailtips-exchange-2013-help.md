---
title: 'MailTips: Exchange 2013 Help'
TOCTitle: MailTips
ms:assetid: 9c989167-cc0c-40a6-82ba-383f573bd2d5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649091(v=EXCHG.150)
ms:contentKeyID: 50478792
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MailTips

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-04-28_

Les infos-courrier sont des messages d'information qui s'affichent lorsque les utilisateurs composent un message. Microsoft Exchange Server 2013 analyse le message, notamment la liste des destinataires auxquels il est destiné. Si un problème potentiel est détecté, les infos-courrier avertissent les utilisateurs avant d'envoyer le message. Grâce aux informations fournies par les infos-courrier, les expéditeurs peuvent adapter le message qu'ils rédigent pour éviter des situations indésirables ou des rapports de non-remise.

## Fonctionnement des infos-courrier

Les infos-courrier sont implémentées comme un service web dans Exchange 2013. Quand un expéditeur compose un message, le logiciel client lance un appel de service web Exchange au serveur d'accès au client pour obtenir la liste des infos-courrier. Le serveur répond par la liste d'infos-courrier qui s'appliquent à ce message, et le logiciel client affiche les infos-courrier à l'expéditeur.

Les cas de messagerie non productifs suivants sont courants dans tout environnement de messagerie :

  - Les rapports de non-remise résultant des messages enfreignant les restrictions configurées dans une organisation comme les restrictions de taille des messages ou le nombre maximal de destinataires par message.

  - Les rapports de non-remise des messages envoyés aux destinataires inexistants ou restreints ou aux utilisateurs dont la boîte aux lettres est saturée.

  - Envoi de messages aux utilisateurs avec des réponses automatiques configurées.

Tous ces cas impliquent l'envoi d'un message par l'utilisateur, qui attend sa livraison, mais recevant à la place une réponse déclarant que le message n'a pas été remis. Même dans le meilleur des cas, par exemple la réponse automatique, la productivité diminue. En cas de rapport de non-remise, ce cas peut engendrer un appel coûteux au service d'assistance technique.

L'absence d'erreur due à l'envoi d'un message peut avoir plusieurs causes, mais les conséquences peuvent être indésirables et gênantes :

  - Messages envoyés à des groupes de distribution extrêmement volumineux.

  - Messages envoyés aux groupes de distribution inappropriés.

  - Messages envoyés par inadvertance aux destinataires étrangers à votre structure.

  - Sélectionner **Répondre à tous** à un message que vous avez reçu en tant que destinataire Cci.

Tous ces cas problématiques peuvent être atténués si l'on informe les utilisateurs du résultat possible de l'envoi de message lorsqu'ils le composent. Par exemple, si les expéditeurs savent que la taille du message qu'ils essaient d'envoyer excède la limite imposée par leur structure, ils ne tenteront pas de l'envoyer. De même, si les expéditeurs sont avertis que le message qu'ils envoient sera livré à des personnes étrangères à la structure, ils seront plus susceptibles de vérifier que le contenu et le ton du message conviennent.

Les clients de messagerie suivants prennent en charge les infos-courrier :

  - Outlook Web App

  - Microsoft Outlook 2010 ou version ultérieure

## Infos-courrier dans Exchange

Le tableau suivant répertorie les infos-courrier disponibles dans Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Infos-courrier</th>
<th>Disponibilité</th>
<th>Scénario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinataire interne non valide</p></td>
<td><p>Outlook</p></td>
<td><p>L'info-courrier de destinataire interne non valide est affichée si l'expéditeur ajoute un destinataire qui semble interne à l'organisation mais qui n'existe pas.</p>
<p>Cela peut se produire si l'expéditeur envoie un message à un utilisateur ayant quitté l'entreprise mais dont l'adresse est résolue à cause du cache de résolution de noms ou d'une entrée dans le dossier Contacts de l'expéditeur. Cela peut également être dû au fait que l'expéditeur ait saisi une adresse SMTP avec un domaine pour lequel Exchange fait autorité et que l'adresse ne correspond pas à un destinataire existant.</p>
<p>L'info-courrier indique le destinataire non valide et lui accorde la possibilité de retirer le destinataire du message.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres saturée</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier Boîte aux lettres saturée est affichée si l'expéditeur ajoute un destinataire dont la boîte aux lettres est saturée et si votre structure a mis en œuvre une restriction d'interdiction de réception pour boîte aux lettres au-delà d'une taille spécifiée.</p>
<p>L'info-courrier indique le nom du destinataire dont la boîte aux lettres est saturée et lui accorde la possibilité de retirer le destinataire du message.</p>
<p>L'info-courrier est précise au moment de l'affichage. Si le message n'est pas immédiatement envoyé, l'info-courrier est mise à jour toutes les deux heures. C'est également le cas si les messages ont été enregistrés en tant que Brouillons et rouverts 2 heures plus tard ou plus.</p></td>
</tr>
<tr class="odd">
<td><p>Réponses automatiques</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier des réponses automatiques est affichée si l'expéditeur ajoute un destinataire qui a activé les réponses automatiques.</p>
<p>L’Info-courrier indique que le destinataire a activé les réponses automatiques et affiche les 175 premiers caractères de la réponse automatique configurée par le destinataire.</p>
<p>L'info-courrier est précise au moment de l'affichage. Si le message n'est pas immédiatement envoyé, l'info-courrier est mise à jour toutes les deux heures. C'est également le cas si les messages ont été enregistrés en tant que Brouillons et rouverts 2 heures plus tard ou plus.</p>
<p>Si une partie de vos boîtes aux lettres utilisateur est hébergée sur Exchange Online et que vous vous trouvez dans une coexistence avec un scénario Exchange Online, le paramètre sur l'objet de domaine distant qui représente la partie distante de votre organisation a un impact direct sur le traitement de l'info-courrier.</p>
<p>Dans Exchange 2013, les utilisateurs peuvent configurer différentes réponses automatiques pour les expéditeurs internes et externes. Si le domaine distant est configuré comme domaine interne (en définissant le paramètre <em>IsInternal</em> sur l'objet du domaine distant sur <code>$true</code>), la réponse automatique interne est renvoyée à tous les utilisateurs du domaine indépendamment de l'endroit où réside leur boîte aux lettres. Cependant, si le domaine distant n'est pas configuré comme domaine interne, la réponse automatique interne est renvoyée à tous les utilisateurs dont les boîtes aux lettres se trouvent dans le domaine local et la réponse automatique externe est renvoyée aux utilisateurs dont les boîtes aux lettres se trouvent dans le domaine distant.</p></td>
</tr>
<tr class="even">
<td><p>Personnalisé</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Une info-courrier personnalisée est affichée si l'expéditeur ajoute un destinataire pour lequel une info-courrier personnalisée est configurée.</p>
<p>Une info-courrier personnalisée peut s'avérer utile pour transmettre des informations spécifiques sur un destinataire. Par exemple, vous pouvez créer une info-courrier personnalisée pour un groupe de distribution expliquant son objectif afin de réduire les abus. Pour plus d'informations, consultez la rubrique <a href="configure-custom-mailtips-for-recipients-exchange-2013-help.md">Configurer les infos-courrier personnalisées pour les destinataires</a>.</p>
<p>Par défaut, des infos-courrier personnalisées ne s'affichent pas si l'expéditeur n'est pas autorisé à envoyer un message à ce destinataire. Dans ce cas, l'info-courrier destinataire restreint s'affiche. Cependant, vous pouvez changer cette configuration et faire afficher l'info-courrier personnalisée.</p></td>
</tr>
<tr class="odd">
<td><p>Destinataire restreint</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier du destinataire restreint s'affiche si l'expéditeur ajoute un destinataire pour lequel les restrictions de livraison sont configurées, interdisant l'envoi de messages de cet expéditeur.</p>
<p>L'info-courrier indique le destinataire auquel l'expéditeur ne peut envoyer de message et lui accorde la possibilité de retirer le destinataire du message. Elle informe clairement l'expéditeur que le message, si envoyé, ne sera pas livré.</p>
<p>Si le destinataire restreint est externe, ou s'il s'agit d'un groupe de distribution contenant des destinataires externes, cette information est également révélée à l'expéditeur. Cependant, les infos-courrier suivantes, le cas échéant, sont supprimées :</p>
<ul>
<li><p>Réponses automatiques</p></li>
<li><p>Boîte aux lettres saturée</p></li>
<li><p>Info-courrier personnalisée</p></li>
<li><p>Destinataire modéré</p></li>
<li><p>Message dépassant la taille limite</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Destinataires externes</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier des destinataires externes est affichée si l'expéditeur ajoute un destinataire externe ou un groupe de distribution comprenant des destinataires externes.</p>
<p>L'info-courrier informe les expéditeurs si un message en cours de saisie quittera la structure, et les aide à prendre les bonnes décisions en termes de langage, de ton et de contenu.</p>
<p>Par défaut, l'info-courrier est désactivée. Vous pouvez l'activer à l'aide de la cmdlet <strong>Set-OrganizationConfig</strong>. Pour plus d'informations, consultez la rubrique <a href="mailtips-over-organization-relationships-exchange-2013-help.md">Infos-courrier sur les relations de l’organisation</a>.</p>
<p>Si une partie de vos boîtes aux lettres utilisateur est hébergée sur Exchange Online et que vous vous trouvez dans une coexistence avec un scénario Exchange Online, le paramètre sur l'objet de domaine distant qui représente la partie distante de votre organisation a un impact direct sur le traitement de l'info-courrier.</p>
<p>Si le domaine distant est configuré comme domaine interne (en définissant le paramètre <em>IsInternal</em> sur l'objet du domaine distant sur <code>$true</code>), n'importe quel destinataire de ce domaine distant sera traité comme interne ; par conséquent, l'info-courrier des destinataires externes ne s'affichera pas. Cependant, si le domaine distant n'est pas configuré comme domaine interne, les destinataires dans ce domaine seront considérés comme externes et l'info-courrier s'affichera lorsqu'un message sera rédigé à ces destinataires.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette info-courrier n'est pas évaluée à la rédaction d'un message destiné à un groupe de distribution dans le domaine distant.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>Large public</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier Large public s'affiche si l'expéditeur ajoute un groupe de distribution dépassant la taille de large public configurée dans votre structure. Par défaut, Exchange affiche cette info-courrier pour les messages destinés aux groupes de distribution de plus de 25 membres. Pour plus d'informations, consultez la rubrique <a href="configure-the-large-audience-size-for-your-organization-exchange-2013-help.md">Configurer la taille du large public pour votre organisation</a>.</p>
<p>La taille des groupes de distribution n'est pas calculée à chaque fois. Au lieu de cela, les informations du groupe de distribution sont lues dans les données de mesures de groupe.</p></td>
</tr>
<tr class="even">
<td><p>Destinataire modéré</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'info-courrier de destinataire modéré s'affiche si l'expéditeur ajoute un destinataire modéré.</p>
<p>L'info-courrier indique quel destinataire est modéré et informe l'expéditeur du retard possible de la remise.</p>
<p>Si l'expéditeur est également le modérateur, cette info-courrier ne s'affiche pas. Elle ne s'affichera pas non plus si l'expéditeur a été explicitement autorisé à envoyer des messages au destinataire (en ajoutant le nom de l'expéditeur à la liste Accepter uniquement les messages de pour le destinataire).</p>
<p>Pour obtenir des instructions sur la configuration de destinataires modérés dans Exchange 2013, consultez la rubrique <a href="common-message-approval-scenarios-exchange-2013-help.md">Scénarios courants d’approbation des messages</a>.</p>
<p>Pour obtenir des instructions sur la configuration de destinataires modérés dans Exchange Online, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/jj983442(v=exchg.150)">Configuration d’un destinataire modéré dans Exchange Online</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Répondre à tous en Cci</p></td>
<td><p>Outlook Web App</p></td>
<td><p>L'info-courrier Répondre à tous en Cci s'affiche si l'expéditeur reçoit une copie Cci d'un message et sélectionne <strong>Répondre à tous</strong>.</p>
<p>Quand un utilisateur sélectionne <strong>Répondre à tous</strong> pour ce type de message, le fait que l'utilisateur a reçu ce message en Cci est révélé au reste du public auquel a été envoyé le message. Dans presque tous les cas, c'est une situation indésirable et cette info-courrier informe l'utilisateur de ces circonstances.</p></td>
</tr>
<tr class="even">
<td><p>Message dépassant la taille limite</p></td>
<td><p>Outlook</p></td>
<td><p>L'info-courrier de message trop volumineux s'affiche si le message que rédige l'expéditeur est plus volumineux que la limite configurée par votre structure.</p>
<p>L'info-courrier s'affiche si la taille du message enfreint l'une des restrictions de taille suivantes :</p>
<ul>
<li><p>Paramètre de taille maximale d'envoi sur la boîte aux lettres de l'expéditeur</p></li>
<li><p>Paramètre de taille maximale de réception sur la boîte aux lettres du destinataire</p></li>
<li><p>Restriction de taille maximale des messages pour l'organisation</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>En raison de la complexité de la mise en œuvre, les limites de taille sur les connecteurs de votre organisation ne sont pas prises en compte.</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## Restrictions des infos-courrier

Les Infos-courrier sont soumises aux restrictions suivantes :

  - Les infos-courrier ne sont pas prises en charge lorsque vous travaillez en mode hors connexion dans Outlook.

  - Quand un message est adressé à un groupe de distribution, les infos-courrier des destinataires individuels membres d'un groupe de distribution ne sont pas évaluées. En revanche, si un membre quelconque est un destinataire externe, l'info-courrier des destinataires externes s'affiche, et montre à l'expéditeur le nombre de destinataires externes dans le groupe de distribution.

  - Si le message est adressé à plus de 200 destinataires, les infos-courrier des boîtes aux lettres individuelles ne sont pas évaluées pour des raisons de performances.

  - Les Infos-courrier personnalisées sont limitées à 175 caractères.

  - Exchange 2010 renseigne les Infos-courrier dans leur intégralité mais Exchange 2013 affiche seulement 1 000 caractères maximum.

  - Si l'expéditeur démarre la saisie d'un message et le laisse ouvert à durée prolongée, les infos-courrier de boîte aux lettres saturée et réponses automatiques sont évaluées toutes les deux heures.

