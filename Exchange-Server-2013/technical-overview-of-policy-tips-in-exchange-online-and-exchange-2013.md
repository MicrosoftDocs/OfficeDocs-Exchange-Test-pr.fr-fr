---
title: 'Aperçu technique des conseils de strat. Exchange Online et Exchange 2013'
TOCTitle: Conseils de stratégie
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50477243
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conseils de stratégie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-07-22_

Vous pouvez contribuer à empêcher les utilisateurs de messagerie électronique Microsoft Outlook, Outlook Web App (OWA) et OWA pour les appareils de votre organisation d’envoyer de manière inappropriée des informations sensibles en créant des stratégies de protection contre la perte de données comprenant des messages de notification *Conseil de stratégie*. De manière similaire aux infos-courrier introduits dans Microsoft Exchange Server 2010, les messages de notification de conseil de stratégie s'affichent à l'attention des utilisateurs dans Outlook pendant qu'ils composent leur courrier électronique. Les messages de notification Conseil de stratégie apparaissent seulement si un élément du courrier électronique de l’expéditeur semble ne pas respecter une stratégie DLP mise en place et que cette stratégie comprend une règle pour avertir l’expéditeur dès que les conditions que vous établissez sont remplies. Pour plus d'informations générales sur la protection contre la perte de données, consultez la rubrique [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

Pour afficher des conseils de stratégie à vos expéditeurs de courrier électronique, vos règles doivent inclure l'action **Avertir l'expéditeur à l'aide d'un conseil de stratégie**. Vous pouvez ajouter ceci dans l'éditeur de règles à partir du Centre d'administration Exchange. Pour plus d'informations, consultez la rubrique [Gérer les conseils de stratégie](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

L'agent de règle de transport qui applique les stratégies DLP ne différencie pas les pièces jointes des messages électroniques, le corps du texte ou les lignes d'objet lors de l'évaluation des messages et des conditions dans vos stratégies. Par exemple, si un utilisateur crée un message électronique qui inclut un numéro de carte de crédit dans le corps du message et qu’il essaie ensuite d’adresser le message à un destinataire externe à votre organisation, alors un message de notification Conseil de stratégie lui rappelant ainsi les attentes de votre entreprise vis-à-vis de telles informations peut s’afficher pour cet utilisateur dans Outlook ou Outlook Web App. Toutefois, ce type de notification ne s'affichera que si vous avez configuré une stratégie DLP qui restreint les actions décrites dans l'exemple, c'est-à-dire ici l'ajout d'un alias de messagerie externe à l'en-tête d'un message contenant des informations de carte de crédit. Lors de la création des stratégies DLP, vous avez le choix entre diverses conditions, actions et exceptions. Cette variété permet d’adapter vos efforts de prévention des pertes de données d’une manière qui répond aux besoins spécifiques de votre organisation.

Chaque fois que vous utilisez l'action de notification de l'expéditeur ou une action de remplacement au sein d'une règle, nous vous recommandons d'inclure également la condition que le message a été envoyé à partir de votre organisation. Pour cela, ajoutez la condition suivante à l'aide de l'éditeur de règles de stratégie : **L'expéditeur se trouve…**\>**dans l'organisation**. Pour en savoir plus sur la modification des stratégies DLP existantes, consultez [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md). Cette opération est recommandée car l’action de notification de l’expéditeur est appliquée dans le cadre de l’expérience de création de message de votre entreprise. Les expéditeurs auxquels l'action fait référence sont les auteurs de messages au sein de votre entreprise. Vos utilisateurs ne peuvent pas agir sur l'interaction de l'utilisateur présentée par les conseils de stratégie pour les messages entrants. L'interaction est ignorée si l'expéditeur se trouve en dehors de l'organisation. Vous pouvez appliquer des stratégies DLP pour analyser les messages entrants et effectuer certaines actions mais, dans ce cas, n’ajoutez pas l’action de notification de l’expéditeur.

Si les expéditeurs de votre organisation qui sont en train de composer un message sont mis en garde au sujet de vos attentes et de vos normes organisationnelles en temps réel par le biais des notifications de conseil de stratégie, ils sont moins susceptibles d'enfreindre les normes que votre organisation essaie d'appliquer.

> [!NOTE]
> <ul>
> <li><p>Exchange Online : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence Exchange Online Plan 2. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licences Exchange Online</a>.</p></li>
> <li><p>Exchange 2013 : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence d’accès client (CAL) Exchange Enterprise. Pour plus d’informations sur les licences d’accès client et les licences par serveur, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licences Exchange Server</a>.</p></li>
> <li><p>Si votre organisation utilise Exchange 2013 SP1 ou Exchange Online, les conseils de stratégie sont disponibles pour les personnes envoyant du courrier depuis Outlook 2013, Outlook Web App ou OWA pour les périphériques. Cependant, si votre organisation utilise actuellement Exchange 2013, les conseils de stratégie ne sont disponibles que pour les personnes envoyant du courrier électronique depuis Outlook 2013.</p></li></ul>

## Texte par défaut des Conseils de stratégie et des options de règles

De nombreuses possibilités s'offrent à vous lorsque vous ajoutez des règles de notification de l'expéditeur à des stratégies DLP. Lorsque vous ajoutez une règle pour aviser l'expéditeur en utilisant l'action **Avertir l'expéditeur à l'aide d'un conseil de stratégie** dans une stratégie DLP, vous pouvez choisir le degré de restriction. Les options de notification sont répertoriées dans le tableau suivant. Pour des informations générales sur la modification des stratégies, consultez la rubrique [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md). Pour des informations précises sur la création de Conseils de stratégie, consultez la rubrique [Gérer les conseils de stratégie](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Règle de notification</th>
<th>Signification</th>
<th>Message de notification de conseil de stratégie par défaut que les utilisateurs d’Outlook verront</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notifier uniquement</strong></p></td>
<td><p>Comme pour les infos-courrier, ceci affiche un message de notification de conseil de stratégie informatif au sujet d'une infraction de la stratégie. Un expéditeur peut empêcher l’affichage de ce type de conseil par le biais d’une boîte de dialogue d’options Conseil de stratégie accessible dans Outlook.</p></td>
<td><p>Ce message peut contenir des données confidentielles. Tous les destinataires doivent être autorisés à recevoir ces informations.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeter le message</strong></p></td>
<td><p>Le message ne sera pas remis tant que la condition est présente. L'expéditeur a la possibilité d'indiquer que son message électronique ne contient pas d'informations sensibles. Il s'agit également d'un remplacement faux positif. Si l’expéditeur indique ceci, alors Outlook permettra au message de quitter la boîte d’envoi afin que le rapport de l’utilisateur puisse faire l’objet d’un audit, mais Exchange bloquera l’envoi du message.</p></td>
<td><p>Ce message peut contenir des données confidentielles. Votre organisation ne permettra pas l’envoi de ce message tant que le contenu n’est pas supprimé.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeter à moins d'un remplacement faux positif</strong></p></td>
<td><p>Le résultat de cette règle de notification est semblable à celui de la règle <strong>Rejeter le message</strong>. Toutefois, si vous activez cette option, Exchange permettra au message d'être envoyé au destinataire prévu, au lieu de bloquer le message.</p></td>
<td><p><strong>Avant que l'expéditeur ne sélectionne une option permettant de remplacer :</strong>Ce message peut contenir des données confidentielles. Votre organisation ne permettra pas l’envoi de ce message tant que le contenu n’est pas supprimé.</p>
<p><strong>Après que l’expéditeur a sélectionné une option de substitution :</strong> Vos commentaires seront soumis à votre administrateur lors de l’envoi du message.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeter à moins d'un remplacement silencieux</strong></p></td>
<td><p>Le message ne sera pas remis tant que la condition est présente, sauf si l'utilisateur signale un remplacement. L'expéditeur a la possibilité d'indiquer qu'il souhaite remplacer la stratégie.</p></td>
<td><p><strong>Avant que l'expéditeur ne sélectionne une option permettant de remplacer :</strong>Ce message peut contenir des données confidentielles. Votre organisation ne permettra pas l’envoi de ce message tant que le contenu n’est pas supprimé.</p>
<p><strong>Après que l'expéditeur a sélectionné une option de substitution :</strong> Vous avez remplacé la stratégie de votre organisation pour les données confidentielles dans ce message. Votre action sera auditée par votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeter à moins d'un remplacement explicite</strong></p></td>
<td><p>Le résultat de cette règle de notification est semblable à celui de la règle <strong>Rejeter à moins d'un remplacement silencieux</strong>, sauf que dans ce cas, quand l'expéditeur tente de remplacer la stratégie, il doit fournir une justification.</p></td>
<td><p><strong>Avant que l'expéditeur ne sélectionne une option permettant de remplacer :</strong>Ce message peut contenir des données confidentielles. Votre organisation ne permettra pas l’envoi de ce message tant que le contenu n’est pas supprimé.</p>
<p><strong>Après que l'expéditeur a sélectionné une option de substitution :</strong> Vous avez remplacé la stratégie de votre organisation pour les données confidentielles dans ce message. Votre action sera auditée par votre organisation.</p></td>
</tr>
</tbody>
</table>


## Personnaliser vos messages de notification de conseil de stratégie

Pour personnaliser le texte d'une notification de conseil de stratégie que les expéditeurs de messages électroniques voient dans leur programme de messagerie, sélectionnez **Gérer les conseils de stratégie** sur la page de protection contre la perte de données. Ce texte ne s’affiche que si une règle de la stratégie DLP inclut l’action **Notifier l’expéditeur à l’aide d’un Conseil de stratégie**. Ajoutez l'action à une règle à l'aide de l'éditeur de règles DLP.

Pour les procédures expliquant comment créer vos propres Conseils de stratégie, consultez la rubrique [Gérer les conseils de stratégie](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). Le texte personnalisé que vous créez peut remplacer le texte par défaut indiqué dans le tableau précédent.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètres et actions de notification de conseil de stratégie</th>
<th>Signification</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Informer l'expéditeur</strong></p></td>
<td><p>Votre texte ne s'affiche que lorsqu'une action <strong>Informer l'expéditeur mais autoriser l'envoi</strong> est initialisée.</p></td>
</tr>
<tr class="even">
<td><p><strong>Autoriser l'expéditeur à remplacer</strong></p></td>
<td><p>Votre texte n'apparaît que lorsque sont initialisées les actions suivantes : <strong>Bloquer le message à moins qu’il ne soit faux positif</strong>, <strong>Bloquer le message, mais autoriser l’expéditeur à le remplacer et à l’envoyer</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Bloquer le message</strong></p></td>
<td><p>Votre texte ne s'affiche que lorsqu'une action <strong>Bloquer le message</strong> est initialisée.</p></td>
</tr>
<tr class="even">
<td><p><strong>Lien vers l'URL de la conformité</strong></p></td>
<td><p>L'URL de la conformité est un lien vers une page web où vous pouvez expliquer vos stratégies de remplacement et de conformité. Ce lien s'affiche dans le conseil de stratégie lorsqu'un utilisateur clique sur le lien <strong>Détails</strong>.</p></td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md)

[Gérer les conseils de stratégie](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

