---
title: 'Afficher les rapports de détection de stratégies DLP: Exchange 2013 Help'
TOCTitle: Afficher les rapports de détection de stratégies DLP
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50477309
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher les rapports de détection de stratégies DLP

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-16_

La gestion de la détection de la stratégie de protection contre la perte de données (DLP) définit les activités exécutées par une organisation afin d'identifier, d'enquêter et de résoudre les violations des stratégies DLP. Afin de gérer les incidents, vous devez disposer de l'accès aux informations qui identifient les éléments détectés par vos stratégies DLP. Ces informations de détection sont intégrées dans les formats de données et de journaux Microsoft Exchange Server 2013 existants afin d'exploiter un système de données riche pour la gestion des incidents de flux de messagerie.

Pour plus d'informations sur la création d'un rapport de compte rendu d'incident avec un événement de détection des stratégies, consultez la rubrique [Créer des rapports de compte-rendu d’incident pour la détection de stratégies DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Pour plus d'informations sur les journaux de messages, consultez la rubrique [Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md).

> [!NOTE]
> Exchange 2013 : la protection contre la perte de données est une fonctionnalité étendue qui nécessite une licence d’accès client (CAL) Exchange Enterprise. Pour plus d’informations sur les licences d’accès client et les licences par serveur, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licences Exchange Server</a>.


## Informations d'audit

Les données relatives à la gestion de la détection de DLP dans Exchange sont intégrées dans le message des journaux de suivi également connu sous le nom de rapports de remise. Les fonctionnalités réutiliser une grande partie de l’infrastructure de journalisation existants disponible dans le système. Pour des informations générales, y compris la compréhension de la structure de fichiers journaux de suivi des messages, veuillez consulter un contenu existant dans la [Compréhension du suivi des messages](message-tracking-exchange-2013-help.md) ou [Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md).

Le rapport de remise est un journal détaillé de toute l'activité des messages lorsque les messages sont transmis vers et depuis un ordinateur qui exécute le service de transport sur un serveur de boîtes aux lettres. Il est possible d'avoir accès au journal de suivi des messages via l'environnement de ligne de commande Exchange Management Shell au moyen de la cmdlet **Get-MessageTrackingLog**. Les données DLP sont intégrées dans le rapport de remise suivant les formats et les conventions de données existants.

## Format de journalisation des données

Les journaux de suivi des messages contiennent des données en provenance des agents impliqués dans le traitement du contenu du flux de messagerie. Pour DLP, l'agent des règles de transport est utilisé pour appeler l'analyse approfondie du contenu des messages et pour appliquer les stratégies définies dans le cadre des ETR. L'évènement AgentInfo existant est utilisé pour ajouter des entrées relatives au DLP dans le journal de suivi des messages.

Le nom de l'agent sera **TRA** ou **Agent des règles de transport** dans l'évènement AgentInfo. Un unique évènement AgentInfo sera consigné par message décrivant le traitement DLP appliqué au message. Le champ **CustomData** du champ d'entrée du journal de suivi des messages constitue l'emplacement où les données DLP consignées par l'agent des règles de transport s'affichent. Ce champ peut contenir plusieurs entrées : une ligne de classification des données et d'informations aux clients pour chaque classification de données trouvée dans le message, une ligne de règles pour chaque règle qui s'applique au message et une ligne d'analyse du fonctionnement dépassant la charge ou le seuil de la durée d'exécution.

Un exemple de l'entrée du journal DLP est affiché ici. Le résultat a été formaté pour afficher des chaînes dans des lignes séparées avec de nouvelles lignes au milieu.

Source : AGENT

EventId : AGENTINFO

CustomData : S:TRA=DC|dcid=41BFDBC6C9D811E0816A3CD34824019B|count=10|conf=77;

S:TRA=DC|dcid=C7ECCBA0CA0011E0B6C00B124924019B|count=3|conf=81;

S:TRA=CI|sndOverride=or|just=Business Reason;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

L'agent des règles de transport exige le regroupement de l'ID de la règles, l'ID de la stratégie DLP (facultatif), la date de la dernière modification, l'action, la gravité, le mode, la classification des données détectées (facultatif) et le remplacement de l'expéditeur (facultatif) basé sur l'ID de la règle (indiqué par « TRA=ETR » dans la ligne du journal). L'ID de la classification des données est également requis, le décompte et le niveau de confiance des classifications à regrouper par nom de classification (indiqué par « TRA=DC » dans la ligne du journal).

Des regroupements supplémentaires inclus l'ID de classification des données, le remplacement de l'expéditeur (facultatif), la justification du remplacement (facultatif) basé sur l'ID de classification des données pour toutes les classifications détectées sur le client (indiqué par « TRA=CI » dans la ligne du journal). L'agent des règles de transport exige également que l'ID de la règle, le temps horloge de la charge (facultatif), l'horloge de l'UC de la charge (facultatif), le temps horloge de l'exécution (facultatif) et l'horloge de l'UC de l'exécution (facultatif) soient regroupés par ID de règle pour toutes les règles qui dépassent les seuils de l'horloge de l'UC ou du temps d'horloge de la charge ou de l'exécution (indiqués par « TRA=ETRP » dans la ligne du journal).

Vous trouverez ci-après une liste complète des fichiers de données. Toutes les données dans le MTL sont des chaînes de types. La colonne Format décrit comment reconnaître chaque champ dans le journal de suivi des messages. La colonne Champ facultatif spécifie les champs qui ne doivent pas être enregistrés quand une règle correspond. La colonne Spécifique au DLP indique quels champs sont spécifiques à la fonctionnalité DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Nom de champ</strong></p></td>
<td><p><strong>Description</strong></p></td>
<td><p><strong>Format</strong></p></td>
<td><p><strong>Champ facultatif</strong></p></td>
<td><p><strong>Spécifique au DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>Agent des règles de transport ; type AgentName</p></td>
<td><p>TRA=DC, ETR, CI ou ETRP</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>Classification des données ; type groupName</p></td>
<td><p>TRA=DC</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Règle de transport Exchange ; type groupName</p></td>
<td><p>TRA=ETR</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>Renseignements sur les clients, type groupName</p></td>
<td><p>TRA=CI</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>ERTP</p></td>
<td><p>Performances des règles de transport Exchange ; type groupName</p></td>
<td><p>TRA=ETRP</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>ID de la classification des données</p></td>
<td><p>dcid=GUID</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>count</p></td>
<td><p>Décompte de la classification des données</p></td>
<td><p>count=Integer</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>Niveau de confiance de la classification des données</p></td>
<td><p>conf=Integer (pourcentage)</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>Remplacement de l'expéditeur ; le champ est facultatif.</p>
<p>Dans la ligne TRA=CI, lorsque le champ est défini sur « or », la classification des données a été remplacée. Si le champ est défini sur « fp », la classification des données a été reportée comme faux positif.</p>
<p>Dans la ligne TRA=ETR, lorsque le champ est défini sur « or », la règle ou une partie de la règle a été remplacée. Si le champ est défini sur « fp », la règle ou une partie de la règle a été reportée comme faux positif.</p></td>
<td><p>sndOverride=or ou fp</p>
<p>Où « or » représente le remplacement et « fp » le faux positif. Le champ sndOverride est présent quand un utilisateur final a signalé un remplacement ou un faux positif pour une règle.</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>just</p></td>
<td><p>Justification ; le champ est facultatif et uniquement disponible quand le champ Remplacement de l'expéditeur est égal à « or » dans la ligne TRA=CI. Le texte de justification entré par l'utilisateur comme motif pour la classification des données devra être remplacé.</p></td>
<td><p>just=IW (chaîne de justification d'entrée)</p>
<p>Le champ Justification n'est connecté que lorsque l'utilisateur final signale un remplacement.</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>ID d'une règle</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>ID d'une stratégie DLP. Le champ est facultatif ; s’il n’existe aucun dlpId, la règle n’appartient pas à une stratégie DLP.</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>Facultatif</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>Dernière date de modification d'une règle</p></td>
<td><p>st=UTC date-time</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>action</p></td>
<td><p>Mesure prise par une règle ; plusieurs actions par règle sont possibles</p></td>
<td><p>action=single action</p>
<p>Si plusieurs actions sont appliquées à une règle, il y aura plusieurs champs action.</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>Audit de la gravité de la règle</p></td>
<td><p>sev=1, 2 ou 3</p>
<p>Où 1 signifie bas, 2 moyen et 3 haute.</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>mode</p></td>
<td><p>État de la règle quand elle a été atteinte (application, audit ou auditandnotify).</p></td>
<td><p>mode=audit, auditandnotify ou application</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>Temps horloge de la charge ; le champ est facultatif</p></td>
<td><p>loadW=temps en ms</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>Horloge de l'UC de la charge ; le champ est facultatif</p></td>
<td><p>loadC=temps en ms</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>Temps horloge de l'exécution ; le champ est facultatif</p></td>
<td><p>execW=temps en ms</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>Horloge de l'UC de l'exécution ; le champ est facultatif</p></td>
<td><p>execC=temps en ms</p></td>
<td><p>Facultatif</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>message-id</p></td>
<td><p>ID du message</p></td>
<td><p>message-id=ID du message</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>Date et heure de l'envoi du message en temps universel</p></td>
<td><p>date-time=date et heure au format UTC</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>sender-address</p></td>
<td><p>Adresse de messagerie spécifiée dans le champ Expéditeur</p></td>
<td><p>sender-address=Adresse de messagerie</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p>recipient-address</p></td>
<td><p>Adresses de messagerie des destinataires du message</p></td>
<td><p>recipient-address=Adresse de messagerie</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p>message-subject</p></td>
<td><p>Données trouvées dans le champ Objet du message</p></td>
<td><p>message-subject=chaîne d'objet d'entrées de l'utilisateur final</p></td>
<td><p>Obligatoire</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Créer des rapports de compte-rendu d’incident pour la détection de stratégies DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md)

