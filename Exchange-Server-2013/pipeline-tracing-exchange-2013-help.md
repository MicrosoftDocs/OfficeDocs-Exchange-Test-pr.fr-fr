---
title: 'Suivi du pipeline: Exchange 2013 Help'
TOCTitle: Suivi du pipeline
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52063028
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suivi du pipeline

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Le suivi du pipeline capture des copies des messages électroniques en provenance d'un expéditeur spécifique pendant qu'ils transitent dans le service de transport sur des serveurs de boîtes aux lettres, dans le service de remise de transport de boîtes aux lettres sur des serveurs de boîtes aux lettres ou dans des serveurs de transport Edge. Le suivi du pipeline capture des informations détaillées sur les modifications que chaque agent de transport applique aux messages figurant dans le pipeline de transport dans des fichiers d'instantané de message. En examinant le contenu des fichiers instantanés de message, vous pouvez déterminer si les agents de transport ont appliqués les modifications que vous avez prévues aux messages figurant dans le pipeline de transport. Si vous dépannez un problème, vous devez déterminer quel agent de transport en est la cause. Vous pouvez ensuite concentrer vos efforts de dépannage sur cet agent pour résoudre le problème. Puis, vous pouvez afficher de nouveau les fichiers instantanés de message pour vérifier que votre solution fonctionne.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Le suivi du pipeline copie le contenu complet des messages électroniques envoyés à partir de l'adresse de messagerie de l'expéditeur. Pour éviter toute exposition involontaire d'informations confidentielles, vous devez définir les autorisations de sécurité appropriées sur le dossier de suivi du pipeline.</p></li>
<li><p>N'activez pas le suivi du pipeline pour de longues périodes. Le suivi du pipeline génère des fichiers qui s'accumulent rapidement. Surveillez toujours l'espace disque disponible lorsque le suivi du pipeline est activé.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Configuration du suivi du pipeline

Avant d'activer le suivi du pipeline, vous devez spécifier l'adresse de messagerie de l'expéditeur que vous voulez surveiller. Le suivi du pipeline est conçu pour journaliser les messages envoyés à partir d'une adresse de messagerie spécifique. L'adresse de messagerie de l'expéditeur peut être interne ou externe à votre organisation Exchange. Vous pouvez également activer le suivi du pipeline pour les messages système générés par le service de transport sur le serveur de boîtes aux lettres ou de transport Edge spécifié, tels que les réponses automatiques, les messages de notification d'état de remise (DSN), les états de journal et d'autres messages générés par le système. Vous pouvez aussi modifier l'emplacement du dossier des fichiers de suivi du pipeline.

Les paramètres que vous pouvez utiliser pour configurer le suivi du pipeline sont récapitulés dans le tableau suivant


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>Vide (<code>$null</code>)</p></td>
<td><p>Spécifiez l'adresse de messagerie de l'expéditeur que vous voulez surveiller.</p>
<p>Spécifiez la valeur &quot;&lt;&gt;&quot; pour surveiller les messages système envoyé par le service de transport spécifié sur le serveur.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>Service de transport</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code></p>
<p><strong>Service de transport de boîtes aux lettres</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code></p></td>
<td><p>Le chemin d'accès doit être sur le serveur local. Les chemins d'accès UNC ne sont pas pris en charge.</p>
<p>Le chemin d'accès spécifié contient le dossier <code>MessageSnapshots</code> dans lequel les fichiers de suivi du pipeline sont enregistrés.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>Vous pouvez activer le suivi du pipeline pour le service de transport spécifié sur le serveur uniquement après avoir configuré l'adresse de l'expéditeur que vous voulez surveiller.</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la procédure d'activation du suivi de pipeline et de configuration de l'adresse de l'expéditeur pour le suivi de pipeline, consultez la rubrique [Configuration du suivi du pipeline](configure-pipeline-tracing-exchange-2013-help.md).

## Fichiers instantanés de message

Les fichiers instantanés de message sont des fichiers qui capturent toutes les modifications apportées à un message par des agents de transport dans le service de transport ou le service de remise de transport de boîtes aux lettres. Ces fichiers sont enregistrés dans le dossier `MessageSnapshots`, dans le chemin d'accès du suivi du pipeline correspondant pour le service de transport.

Dans le dossier `MessageSnapshots`, Exchange crée un dossier pour chaque message envoyé par l'expéditeur surveillé qui transite par le service de transport spécifié. Chaque dossier est nommé d'après un GUID attribué au message. Si vous activez le suivi du pipeline pour le service de transport et le service de transport de boîtes aux lettres sur le même serveur de boîtes aux lettres, un GUID distinct est attribué au même message par chaque service de transport, de sorte que le nom de dossier pour un message figurant dans le dossier `MessageSnapshots` destiné au service de transport diffère du nom de dossier pour le même message dans le dossier `MessageSnapshots` destiné au service de transport de boîtes aux lettres. Si vous activez le suivi du pipeline sur plusieurs serveurs Exchange, un GUID distinct est attribué au même message lorsqu'il transite dans le service de transport sur chaque serveur Exchange.

Dans chaque dossier de messages, Exchange crée plusieurs fichiers instantanés de message portant l'extension .eml. Ces fichiers instantanés de message incluent le contenu du message reflétant chaque événement SMTP et agent de transport rencontré.

Si un agent de transport est enregistré pour un événement SMTP, Exchange crée un instantané du message avant que ce dernier rencontre un agent de transport. Vous disposez ainsi d'une copie du message avant qu'il rencontre les agents de transport enregistrés sur cet événement Ensuite, un instantané de message est créé pour chaque agent de transport rencontré, même si ce dernier ne modifie pas le message. Toutefois, si aucun agent n'est enregistré sur un événement, Exchange ne crée pas d'instantané de message pour cet événement.

Par exemple, si trois agents de transport sont enregistrés sur l'événement **OnEndofData** mais que seuls deux d'entre eux modifient un message, quatre instantanés de message sont créés. Le premier instantané de message capture le message lorsqu'il rencontre l'événement **OnEndofData** avant toute modification effectuée par les agents de transport enregistrés sur cet événement. Ensuite, un instantané de message est créé pour chaque agent de transport, même si ce dernier ne modifie pas le message.

La fichiers instantanés de message créés sont décrits dans la liste suivante :

  - **Original.eml**   Ce fichier inclut le contenu d'origine non modifié du message électronique avant que celui-ci rencontre un événement SMTP ou un agent de transport.

  - **Routingnnnn.eml**   Ces fichiers incluent le contenu du message électronique lorsqu'il rencontre les événements SMTP et les agents de transport enregistrés sur ces derniers dans la phase de catégorisation du service de transport. L'espace réservé *nnnn* représente une valeur entière commençant par `0001`. Cette valeur est incrémentée pour chaque événement SMTP et agent de transport enregistré sur cet événement dans l'ordre dans lequel les événements et agents agissent sur le message. Le service de remise de transport de boîtes aux lettres ne génère pas ces fichiers instantanés de **Routage**.

  - **SmtpReceivennnn.eml**   Ces fichiers incluent le contenu du message électronique quand il rencontre les événements SMTP **OnEndofData** et **OnEndOfHeaders** ainsi que les agents de transport enregistrés sur ces derniers durant la phase de réception du service de transport ou du service de remise de transport de boîtes aux lettres. L'espace réservé *nnnn* représente une valeur entière commençant par `0001`. Cette valeur est incrémentée pour chaque événement SMTP et agent de transport enregistré sur cet événement dans l'ordre dans lequel les événements et agents agissent sur le message.

Vous pouvez ouvrir les fichiers instantanés de message à l'aide de Bloc-notes ou de tout éditeur de texte.

Chaque fichier instantané de message commence par des en-têtes qui sont ajoutés au contenu du message et répertorient l'événement SMTP et l'agent de transport auquel le fichier instantané de message est lié. Ces en-têtes commencent par `X-CreatedBy: MessageSnapshot-Begin injected headers` et se terminent par `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`. Ils sont remplacés dans chaque fichier instantané de message par l'agent de transport et l'événement SMTP suivants. Voici un exemple des en-têtes qui sont ajoutés à un fichier de message électronique :

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

Sous les en-têtes de l'instantané de message, le fichier inclut le contenu du message comprenant tous les en-têtes du message d'origine. Si un agent de transport modifie le contenu du message, les modifications sont intégrées au message. Le message étant traité par chaque agent de transport, les modifications apportées par chaque agent sont appliquées au contenu du message. Si un agent de transport ne modifie pas le contenu du message, l'instantané de message créé par cet agent est identique à l'instantané de message créé par l'agent de transport précédent.

