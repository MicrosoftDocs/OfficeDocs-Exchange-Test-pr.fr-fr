---
title: 'Marquages de courrier indésirable: Exchange 2013 Help'
TOCTitle: Marquages de courrier indésirable
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50477704
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Marquages de courrier indésirable

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Les marquages de courrier indésirable vous aident à diagnostiquer les problèmes de courrier indésirable en appliquant des métadonnées de diagnostic, ou « marquages », telles que des informations spécifiques à un expéditeur, des résultats de validation du puzzle et des résultats de filtrage du contenu, aux messages à mesure qu’ils sont soumis aux fonctionnalités de blocage du courrier indésirable qui filtrent les messages entrants en provenance d’Internet. Il existe trois marquages de courrier indésirable : le seuil de probabilité de courrier d’hameçonnage, le seuil de probabilité de courrier indésirable et l’ID de l’expéditeur.

Vous pouvez utiliser les marquages de courrier indésirable comme outils de diagnostic pour déterminer les actions à appliquer aux faux positifs et aux messages suspects que les individus reçoivent dans leurs boîtes aux lettres.

## Affichage des marquages de courrier indésirable

Vous pouvez afficher des marquages de courrier indésirable dans Microsoft Outlook. Pour plus d’informations, consultez la rubrique [Afficher des marquages de courrier indésirable dans Outlook](view-anti-spam-stamps-in-outlook-exchange-2013-help.md).

## Présentation du rapport de blocage du courrier indésirable

Le rapport de blocage du courrier indésirable est un rapport de synthèse des résultats du filtrage du courrier indésirable qui a été appliqué à un message électronique. L’Agent de filtrage du contenu applique ce marquage à l’enveloppe de message sous la forme d’un en-tête X comme suit.

    X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 

Le tableau suivant décrit les informations de filtre qui peuvent figurer dans un rapport de blocage du courrier indésirable.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le rapport de blocage du courrier indésirable n’affiche que les informations des filtres appliqués au message spécifique. Un rapport de blocage du courrier indésirable ne contient pas, en général, toutes les informations contenues dans le tableau suivant. Par exemple, vous pouvez voir s’afficher le rapport de blocage du courrier indésirable suivant : <code>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</code>.</td>
</tr>
</tbody>
</table>


### Informations de filtrage d’un rapport de blocage du courrier indésirable

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Marquage</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>Le marquage de l’ID de l’expéditeur (SID) est basé sur le SPF (sender policy framework) qui autorise l’utilisation de domaines dans la messagerie. Le SPF figure dans l’enveloppe du message comme <code>Received-SPF</code>. Le processus d’évaluation de l’ID de l’expéditeur génère un état d’ID de l’expéditeur pour le message. Cet état peut avoir l’une des valeurs suivantes :</p>
<ul>
<li><p><strong>Pass   </strong>L’adresse IP et la PRA (Purported Responsible Address, adresse prétendue responsable) ont toutes les deux passé le contrôle de vérification de l’ID de l’expéditeur.</p></li>
<li><p><strong>Neutral   </strong>Les données de l’ID de l’expéditeur publiées sont peu concluantes.</p></li>
<li><p><strong>Soft fail</strong>   L’adresse IP de la PRA figure peut-être parmi les adresses non autorisées.</p></li>
<li><p><strong>Fail   </strong>L’adresse IP n’est pas autorisée ; aucune PRA ne figure dans le courrier entrant ou le domaine d’envoi n’existe pas.</p></li>
<li><p><strong>None</strong>   Il n’existe aucune donnée SPF publiée dans le DNS de l’expéditeur.</p></li>
<li><p><strong>TempError</strong>   Une erreur DNS temporaire s’est produite. Un serveur DNS peut être indisponible, par exemple.</p></li>
<li><p><strong>PermError   </strong>L’enregistrement DNS est non valide, tel qu’une erreur dans le format d’enregistrement.</p></li>
</ul>
<p>Le marquage d’ID de l’expéditeur s’affiche comme en-tête X dans l’enveloppe du message comme suit :</p>
<pre><code>X-MS-Exchange-Organization-SenderIdResult:&lt;status&gt;</code></pre>
<p>Pour plus d’informations sur l’ID de l’expéditeur, consultez la rubrique <a href="sender-id-exchange-2013-help.md">ID de l'expéditeur</a>.</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>Le marquage de version DAT (DV) indique la version du fichier de définition du courrier indésirable utilisé lors de l’analyse du message.</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>Le marquage d’action de signature (SA) indique que le message a été soit récupéré, soit supprimé à cause d’une signature trouvée dans le message.</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>Le marquage de version DAT de signature (SV) indique la version du fichier de signature utilisé lors de l’analyse du message.</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>Le marquage du seuil de probabilité de courrier d’hameçonnage (PCL) affiche la valeur du message basé sur son contenu et est appliqué lorsque le message est traité par l’Agent de filtrage du contenu. Cet état peut avoir l’une des valeurs suivantes :</p>
<ul>
<li><p><strong>Neutre   </strong>Le contenu du message n’est probablement pas du hameçonnage.</p></li>
<li><p><strong>Suspect   </strong>Le contenu du message est probablement du hameçonnage.</p></li>
</ul>
<p>La valeur PCL est comprise entre 1 et 8. Une valeur PCL comprise entre 1 et 3 renvoie un état <code>Neutral</code>. Cela signifie que le contenu du message n’est probablement pas du hameçonnage. Une valeur PCL comprise entre 4 et 8 renvoie à un état <code>Suspicious</code>. Cela signifie que le message n’est probablement pas du hameçonnage.</p>
<p>Les valeurs sont utilisées pour déterminer l’action prise par Outlook sur les messages. Outlook utilise le marquage PCL pour bloquer le contenu des messages suspects.</p>
<p>Le marquage PCL s’affiche comme en-tête X dans l’enveloppe du message comme suit :</p>
<pre><code>X-MS-Exchange-Organization-PCL:&lt;status&gt;</code></pre></td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>Le marquage du seuil de probabilité de courrier indésirable (SCL) du message affiche la valeur du message en fonction de son contenu. L’agent de filtrage du contenu utilise la technologie Microsoft SmartScreen pour évaluer le contenu d’un message et pour attribuer une valeur de contrôle d’accès SCL à chaque message. La valeur SCL est comprise entre 0 et 9, avec 0 pour les messages les moins susceptibles d’être du courrier indésirable et 9 pour les messages les plus susceptibles d’être du courrier indésirable. Les actions qu’Exchange et Outlook exécutent dépendent de vos paramètres de seuil SCL.</p>
<p>Le marquage SCL s’affiche comme en-tête X dans l’enveloppe du message comme suit :</p>
<pre><code>X-MS-Exchange-Organization-SCL:&lt;status&gt;</code></pre>
<p>Pour plus d’informations sur les seuils et les actions SCL, consultez la rubrique <a href="spam-confidence-level-threshold-exchange-2013-help.md">Niveau de confiance du courrier indésirable</a>.</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>Le marquage du poids personnalisé (CW) d’un message indique qu’il contient un mot ou une expression non approuvés et que la valeur SCL, ou « Poids », de ce mot ou cette expression non approuvés a été appliquée au résultat SCL final :</p>
<ul>
<li><p>Les expressions non approuvées, ou expressions de blocage, ont un poids maximal et remplacent le résultat SCL par 9.</p></li>
<li><p>Les mots ou expressions approuvés, ou expressions d’autorisation, ont un poids minimal et remplacent le résultat SCL par 0.</p></li>
</ul>
<p>Pour plus d’informations sur l’ajout de mots ou d’expressions approuvés ou non approuvés à l’Agent de filtrage du contenu, consultez la rubrique <a href="manage-content-filtering-exchange-2013-help.md">Gérer le filtrage du contenu</a>.</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>Le marquage du puzzle pré-résolu (PP) indique que, si le message d’un expéditeur contient un cachet de calcul résolu valide, basé sur la fonctionnalité de validation de cachet de courrier électronique Outlook, il est improbable que l’expéditeur soit malveillant. Dans ce cas, l’Agent de filtrage du contenu réduit la valeur de contrôle d’accès SCL.</p>
<p>L’Agent de filtrage du contenu ne modifie pas la valeur de contrôle d’accès SCL si la fonctionnalité de validation de cachet de courrier électronique est activée et que l’une des conditions suivantes est vraie :</p>
<ul>
<li><p>Un message entrant ne contient pas d’en-tête de cachet de calcul.</p></li>
<li><p>L’en-tête de cachet de calcul n’est pas valide.</p></li>
</ul>
<p>Pour plus d’informations sur la fonctionnalité de validation du cachet, consultez la rubrique <a href="content-filtering-exchange-2013-help.md">Filtrage du contenu</a>.</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>Le cachet TIME indique qu’une période d’une longueur significative s’est écoulée entre l’envoi et la réception du message. Le cachet TIME permet de déterminer la valeur de contrôle d’accès SCL finale du message.</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>Le marquage MIME indique que le message électronique n’est pas compatible MIME.</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>Le marquage P100 indique que le message contient une adresse URL présente dans un fichier de définition du hameçonnage.</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>Le marquage IPOnAllowList indique que l’adresse IP de l’expéditeur figure sur la liste verte d’IP. Pour plus d’informations sur la liste verte IP, consultez la rubrique <a href="http://go.microsoft.com/fwlink/?linkid=268732">Présentation du filtrage des connexions</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>Le marquage MessageSecurityAntispamBypass indique que le contenu du message n’a pas été filtré et que l’expéditeur a reçu l’autorisation d’ignorer les filtres de courrier indésirable.</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>Le marquage SenderBypassed indique que l’Agent de filtrage du contenu ne traite aucun filtrage de contenu pour les messages reçus de cet expéditeur. Pour plus d’informations, consultez la rubrique <a href="manage-content-filtering-exchange-2013-help.md">Gérer le filtrage du contenu</a>.</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>Le marquage AllRecipientsBypassed indique que l’une des conditions suivantes a été rencontrée pour tous les destinataires répertoriés dans le message :</p>
<ul>
<li><p>Le paramètre <em>AntispamBypassedEnabled</em> appliqué à la boîte aux lettres du destinataire est défini sur <code>$true</code>. Il s’agit d’un paramètre par destinataire qui ne peut être défini que par un administrateur à l’aide de la cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p>L’expéditeur du message se trouve dans la liste des expéditeurs approuvés Outlook du destinataire. Pour plus d’informations sur la liste des expéditeurs approuvés, consultez la rubrique <a href="manage-safelist-aggregation-exchange-2013-help.md">Gérer l'agrégation de listes fiables</a>.</p></li>
<li><p>L’Agent de filtrage du contenu ne traite aucun filtrage de contenu pour les messages envoyés à ce destinataire. Pour plus d’informations sur les exceptions de destinataires, consultez la rubrique <a href="manage-content-filtering-exchange-2013-help.md">Gérer le filtrage du contenu</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>

