---
title: 'Analyse de pièces jointes des msg avec des rgl de transp.: Exchange 2013 Help'
TOCTitle: Utiliser des règles de transport pour analyser les pièces jointes des messages
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50479090
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utiliser des règles de transport pour analyser les pièces jointes des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-27_

Vous pouvez analyser des pièces jointes des messages électroniques au sein de votre organisation en définissant des règles de transport. Exchange fournit des règles de transport qui offrent la possibilité d’examiner les pièces jointes des messages électroniques dans le cadre de vos exigences en matière de sécurité et de conformité de la messagerie. Lorsque vous analysez les pièces jointes, vous pouvez agir sur les messages en fonction du contenu ou des caractéristiques de ces pièces jointes. Voici quelques tâches concernant les pièces jointes que vous pouvez effectuer à l’aide des règles de transport :

  - Effectuez des recherches dans les fichiers de pièces jointes compressés, comme les fichiers .zip et .rar et, si vous trouvez du texte correspondant à un modèle que vous avez spécifié, ajoutez une clause d’exclusion de responsabilité à la fin du message.

  - Analysez le contenu des pièces jointes et, si elles contiennent les mots-clés que vous avez spécifiés, redirigez le message vers un modérateur pour approbation avant qu’il ne soit remis.

  - Vérifiez les messages avec des pièces jointes qui ne peuvent pas être analysés, puis bloquez l’envoi du message dans son intégralité.

  - Vérifiez les pièces jointes qui dépassent une certaine taille, puis informez l’expéditeur du problème si vous choisissez de bloquer la remise du message.

  - Créez des notifications qui alertent les utilisateurs s’ils envoient un message déclenchant une règle de transport.

  - Bloquez tous les messages contenant des pièces jointes. Pour obtenir des exemples, consultez la rubrique [Scénarios courants de blocage de pièce jointe](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

Les administrateurs Exchange peuvent créer des règles de transport en accédant au **Centre d’administration Exchange** \> **Flux de messagerie** \> **Règles**. Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Une fois que vous avez commencé la création d’une règle, vous pouvez voir la liste complète des conditions applicables aux pièces jointes en cliquant sur **Plus d’options** \> **Toute pièce jointe** sous **Appliquer cette règle si**. Les options applicables aux pièces jointes sont présentées dans le schéma suivant.

![Boîte de dialogue pour sélectionner les règles associées aux pièces jointes](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "Boîte de dialogue pour sélectionner les règles associées aux pièces jointes")

Pour plus d’informations sur les règles de transport, y compris l’ensemble des conditions et des actions que vous pouvez choisir, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) . Les clients Exchange Online Protection (EOP) et hybrides peuvent tirer parti des meilleures pratiques en matière de règles de transport fournies dans [Meilleures pratiques de configuration d’EOP](https://technet.microsoft.com/fr-fr/library/jj723164\(v=exchg.150\)). Si vous êtes prêt à créer des règles, consultez [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md).

## Analyser le contenu des pièces jointes

Vous pouvez utiliser les conditions de règles de transport du tableau ci-dessous pour examiner le contenu des pièces jointes aux messages. Pour ces conditions, seuls les 150 premiers Ko d’une pièce jointe sont analysés. Pour commencer à utiliser ces conditions lors de l’analyse des messages, vous devez les ajouter à une règle de transport. Pour en savoir plus sur la création ou la modification des règles, voir [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de la condition dans le CAE</th>
<th>Nom de la condition dans l’environnement de ligne de commande Exchange Management Shell</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Un contenu de pièce jointe, quel qu’il soit, comprend l’un de ces mots</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages contenant des pièces jointes présentées dans un format de fichier pris en charge et comportant une chaîne ou un groupe de caractères spécifique.</p></td>
</tr>
<tr class="even">
<td><p><strong>Un contenu de pièce jointe, quel qu’il soit, correspond à ces modèles de texte</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages contenant des pièces jointes présentées dans un format de fichier pris en charge et comportant un modèle de texte qui correspond à une expression régulière spécifiée.</p></td>
</tr>
</tbody>
</table>


Les noms Environnement de ligne de commande Exchange Management Shell pour les conditions énumérées ici sont des paramètres qui nécessitent la cmdlet `TransportRule`.

  -  Pour plus d’informations concernant la cmdlet, voir [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)).

  -  Pour en savoir plus sur les types de propriétés de ces conditions, voir [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Les règles de transport peuvent analyser uniquement le contenu des types de fichiers pris en charge. Si l’agent des règles de transport détecte une pièce jointe qui ne se trouve pas dans la liste des types de fichiers pris en charge, la condition `AttachmentIsUnsupported` est déclenchée. Les types de fichiers pris en charge sont répertoriés dans la section suivante. Les fichiers non répertoriés déclencheront la condition `AttachmentIsUnsupported`.

## Fichiers d'archives compressés

Si le message contient un fichier d’archive compressé, tel qu’un fichier ZIP ou CAB, l’agent des règles de transport inspecte les fichiers contenus dans cette pièce jointe. Ces messages sont traités de la même façon que les messages comportant plusieurs pièces jointes. Les propriétés des fichiers d’archive compressés ne sont pas analysées. Par exemple, si le type de fichier du conteneur prend en charge des commentaires, ce champ n’est pas analysé.

## Types de fichiers pris en charge pour l’analyse du contenu des règles de transport

Le tableau suivant répertorie les types de fichiers pris en charge par les règles de transport. Le système utilise la détection automatique des types de fichiers en analysant les propriétés de fichiers plutôt que l’extension réelle de nom de fichier, empêchant ainsi les expéditeurs de courrier indésirable de pouvoir contourner le filtrage des règles de transport en renommant l’extension des fichiers. La liste des types de fichiers avec un code exécutable pouvant être vérifiés dans le cadre des règles de transport figure plus loin dans cette rubrique.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Catégorie</th>
<th>Extension de fichier</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013, Office 2010 et Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Les fichiers Microsoft OneNote et Microsoft Publisher ne sont pas pris en charge par défaut. Vous pouvez activer la prise en charge de ces types de fichiers via l’intégration IFilter. Pour plus d’informations, voir <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Inscrire les IFilters Filter Pack avec Exchange 2013</a>.</p>
<p>Le contenu des pièces incorporées contenues dans ces types de fichier est également analysé. Cependant, les objets qui ne sont pas incorporés, comme les documents liés, ne sont pas analysés.</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="odd">
<td><p>Fichiers Office supplémentaires</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="odd">
<td><p>Texte</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, .inf, .ini, .inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>Aucun</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>Aucune partie des fichiers .odf n’est traitée. Par exemple, si le fichier .odf contient un document incorporé, le contenu de ce document incorporé n’est pas analysé.</p></td>
</tr>
<tr class="odd">
<td><p>Dessin AutoCAD</p></td>
<td><p>.dxf</p></td>
<td><p>Les fichiers AutoCAD 2013 ne sont pas pris en charge.</p></td>
</tr>
<tr class="even">
<td><p>Image</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>Seul le texte des métadonnées associé à ces fichiers image est analysé. Il n’y a aucune reconnaissance optique de caractères.</p></td>
</tr>
</tbody>
</table>


## Analyser les propriétés de fichier des pièces jointes

Les conditions de règle de transport suivantes analysent les propriétés d’un fichier joint à un message. Pour commencer à utiliser ces conditions lors de l’analyse des messages, vous devez les ajouter à une règle de transport. La liste des types de fichiers pris en charge avec un code exécutable pouvant être vérifiés dans le cadre des règles de transport figure ici. Pour plus d’informations sur la création ou la modification des règles, consultez la rubrique [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de la condition dans le CAE</th>
<th>Nom de la condition dans l’environnement de ligne de commande Exchange Management Shell</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Le nom de fichier de n’importe quelle pièce jointe correspond à ces modèles de texte</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages qui contiennent des pièces jointes dont le type de fichier est pris en charge si ces pièces jointes ont un nom qui contient les caractères que vous spécifiez.</p></td>
</tr>
<tr class="even">
<td><p><strong>Une extension de fichier de pièce jointe contient ces mots</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages qui contiennent des pièces jointes présentées dans un format de fichier pris en charge si l’extension de nom de fichier correspond à une extension que vous spécifiez.</p></td>
</tr>
<tr class="odd">
<td><p><strong>La taille de n’importe quelle pièce jointe est supérieure ou égale à</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages qui contiennent des pièces jointes présentées dans un format de fichier pris en charge si la taille de ces pièces jointes est supérieure à la taille que vous spécifiez.</p></td>
</tr>
<tr class="even">
<td><p><strong>La pièce jointe n’a pas terminé l’analyse</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages si une pièce jointe n’est pas analysée par l’agent des règles de transport.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Une pièce jointe comporte un contenu exécutable</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages qui contiennent des fichiers exécutables sous forme de pièces jointes. Les types de fichiers pris en charge sont répertoriés ici.</p></td>
</tr>
<tr class="even">
<td><p><strong>Toutes les pièces jointes sont protégées par mot de passe</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>Cette condition établit une correspondance avec les messages qui contiennent des pièces jointes présentées dans un format de fichier pris en charge si ces pièces jointes sont protégées par mot de passe.</p></td>
</tr>
</tbody>
</table>


Les noms Environnement de ligne de commande Exchange Management Shell pour les conditions énumérées ici sont des paramètres qui nécessitent la cmdlet `TransportRule`.

  -  Pour plus d’informations concernant la cmdlet, voir [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)).

  -  Pour en savoir plus sur les types de propriétés de ces conditions, voir [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

## Types de fichiers exécutables pris en charge pour l’analyse des règles de transport

L’agent de transport utilise la détection True Type par l’inspection des propriétés de fichier et non simplement des extensions de fichier. Cela empêche les expéditeurs de courrier indésirable de contourner votre règle en renommant une extension de fichier. Le tableau suivant répertorie les types de fichiers exécutables pris en charge par ces conditions. Si un fichier trouvé n’est pas répertorié ici, la condition `AttachmentIsUnsupported` est déclenchée.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de fichier</th>
<th>Extension native</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Fichier d’archives auto-extractible créé avec le programme d’archivage WinRAR.</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>Fichier exécutable Windows 32 bits avec une extension de bibliothèque de liens dynamiques.</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>Fichier de programme exécutable auto-extractible.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Fichier d’archives Java.</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>Fichier exécutable de désinstallation.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Fichier de raccourci de programme.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Fichier de code source compilé, fichier d’objet 3D ou fichier de séquence.</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>Fichier exécutable Windows 32 bits.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Fichier de dessin XML Microsoft Visio.</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>Fichier de système d’exploitation OS/2.</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>Fichier exécutable Windows 16 bits.</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>Fichier de système d’exploitation du disque.</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>Fichier de test anti-virus standard de l’European Institute for Computer Antivirus Research (EICAR).</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Fichier d’informations de programme Windows.</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Fichier de programme exécutable Windows.</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## Extension du nombre de types de fichiers pris en charge

Les types de fichiers pris en charge répertoriés dans cette rubrique peuvent être révisés à tout moment à l'aide de l'intégration d'IFilter. Pour plus d'informations, consultez la rubrique [Inscrire les IFilters Filter Pack avec Exchange 2013](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md).

Les types de fichiers que vous ajoutez à l’aide de ce processus deviennent des types de fichiers pris en charge et ne déclenchent plus la condition `AttachmentIsUnsupported`.

## Stratégies de protection contre la perte de données et règles de transport de pièces jointes

Pour vous aider à gérer des informations professionnelles importantes dans le courrier électronique, vous pouvez inclure l’une des conditions liées aux pièces jointes, ainsi que les règles d’une stratégie de protection contre la perte de données (DLP). Par exemple, vous pouvez autoriser l’envoi de messages contenant des numéros de passeport mais uniquement si les numéros de passeport se trouvent dans une pièce jointe protégée par mot de passe. Pour le vérifier, procédez comme suit :

  - Créez une stratégie DLP qui vérifie si le courrier indésirable contient des informations sensibles concernant un passeport. Pour plus d’informations, consultez la rubrique [Procédures relatives à la protection contre la perte de données (DLP)](dlp-procedures-exchange-2013-help.md).

  - Ajoutez l’exception **Toutes les pièces jointes sont protégées par mot de passe** dans la zone de règle de transport **Sauf si...**.

  - Définissez une action à effectuer sur le courrier qui contient des numéros de passeport qui ne sont pas dans le fichier protégé.

Les stratégies DLP et les conditions applicables aux pièces jointes peuvent vous aider à respecter les besoins de votre entreprise en formulant ces besoins sous forme de conditions, d’exceptions et d’actions de règle de transport. Lorsque vous incluez l’analyse d’informations sensibles dans une stratégie DLP, les pièces jointes des messages sont analysées pour détecter uniquement ces informations. Cependant, les conditions applicables aux pièces jointes, portant par exemple sur la taille ou le type de fichier ne sont pas incluses tant que vous n’ajoutez pas les conditions répertoriées dans cette rubrique. La stratégie DLP n’est pas disponible pour toutes les versions d’Exchange. Pour en savoir plus, voir [Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\)) dans Exchange Online

