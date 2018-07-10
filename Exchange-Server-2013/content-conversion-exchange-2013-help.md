---
title: 'conversion de contenu.: Exchange 2013 Help'
TOCTitle: conversion de contenu.
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 50479077
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# conversion de contenu.

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

La *conversion de contenu* est le processus consistant à mettre en forme un message correctement pour chaque destinataire. La décision d'exécuter une conversion de contenu sur un message dépend de la destination et du format du message en cours de traitement. Dans Microsoft Exchange Server 2013, il existe deux types de conversion de contenu :

  - **Conversion de message pour des destinataires externes**   Ce type de conversion de contenu comprend les options de conversion du format (TNEF) et les options d’encodage de message pour les destinataires externes. Les messages envoyés à des destinataires à l’intérieur de l’organisation Exchange ne nécessitent pas ce type de conversion de contenu. Ce type de conversion de contenu est géré par le catégoriseur dans le service de transport du serveur de boîtes aux lettres. Une catégorisation de chaque message intervient après qu’un nouveau message a été placé dans la file d’attente de soumission. En plus de la résolution des destinataires et de la résolution du routage, une conversion de contenu est appliquée au message avant son placement dans la file d'attente de remise. Si un seul message contient plusieurs destinataires, le catégoriseur détermine l’encodage approprié pour chaque destinataire. Le suivi de conversion de contenu ne capture aucune erreur de conversion de contenu que le catégoriseur rencontre lors de la conversion des messages envoyés à des destinataires externes.

  - **Conversion MAPI pour les destinataires internes**   Ce type de conversion de contenu est géré par le service de transport de boîtes aux lettres. Le service de transport de boîtes aux lettres, qui existe sur les serveurs de boîtes aux lettres, permet de transmettre des messages entre des bases de données de boîtes aux lettres du serveur local et le service de transport de serveurs de boîtes aux lettres. Plus précisément, le service de dépôt de transport de boîtes aux lettres transmet des messages depuis la boîte d’envoi de l’expéditeur vers le service de transport d’un serveur de boîtes aux lettres. Le service de remise de transport de boîtes aux lettres transmet les messages du service de transport d’un serveur de boîtes aux lettres à la boîte de réception du destinataire. Le service de dépôt de transport de boîtes aux lettres convertit tous les messages sortants à partir du format MAPI et le service de remise de transport de boîtes aux lettres convertit tous les messages entrants au format MAPI. Le suivi de conversion de contenu capture ces erreurs de conversion MAPI. Pour plus d'informations, consultez la rubrique [Suivi de la conversion de contenu](content-conversion-tracing-exchange-2013-help.md).

Cette rubrique décrit les options de conversion de message pour des destinataires externes.

**Contenu de cette rubrique**

Formats de message Exchange et Outlook

Options de conversion de contenu pour des destinataires externes

Compréhension de la structure des messages électroniques

## Formats de message Exchange et Outlook

La liste suivante répertorie les formats de message de base disponibles dans Exchange et Microsoft Outlook :

  - **Texte brut**   Un message en texte brut contient uniquement du texte US-ASCII, comme décrit dans la norme RFC 2822. Le message ne peut pas contenir des polices différentes ni de mise en forme du texte. Les deux formats suivants peuvent être utilisés pour un message en texte brut :
    
      - Les en-têtes et le corps du message sont composés de texte US-ASCII. Les pièces jointes doivent être codées à l'aide de l'algorithme *Uuencode*. Uuencode est une abréviation de « Unix-to-Unix encoding » qui définit un algorithme d’encodage pour le stockage de pièces jointes binaires dans le corps d’un message électronique à l’aide de caractères de texte US-ASCII.
    
      - Le message est codé MIME avec une valeur Content-Type de text/plain et une valeur Content-Transfer-Encoding de 7bit pour les parties texte d'un message multipart. Toute pièce jointe d'un message est codée à l'aide d'un codage Quoted-printable ou Base64. Par défaut, lorsque vous composez et envoyez un message en texte brut dans Outlook, le message est codé MIME à l’aide d’une valeur Content-Type de text/plain.

  - **HTML**   Un message HTML prend en charge la mise en forme de texte, les images d'arrière-plan, les tableaux, les listes à puces et d'autres éléments graphiques. Par définition, un message au format HTML doit être codé MIME pour conserver ces éléments de mise en forme.

  - **Rich text format (RTF)**   RTF prend en charge la mise en forme de texte et d'autres éléments graphiques. RTF est synonyme de TNEF. Les formats TNEF et RTF peuvent être utilisés de façon interchangeable. Ce format RTF est totalement différent du format RTF disponible dans Microsoft Word.
    
    Seul Outlook et quelques autres clients de messagerie MAPI comprennent les messages RTF.

  - **TNEF**   Le format TNEF (Transport Neutral Encapsulation Format) est un format spécifique de Microsoft qui permet d’encapsuler des propriétés de messages MAPI. Un message TNEF contient une version du message en texte brut et une pièce jointe qui contient la version mise en forme d’origine du message. Généralement, cette pièce jointe est nommée Winmail.dat. La pièce jointe Winmail.dat inclut les informations suivantes :
    
      - version mise en forme d'origine du message incluant, par exemple, les polices, les tailles et les couleurs de texte
    
      - objets OLE incluant, par exemple, des images ou des documents Microsoft Office imbriqués
    
      - fonctionnalités Outlook spéciales incluant, par exemple, des écrans personnalisés, des boutons de vote ou des demandes de réunion
    
      - pièces jointes au message d'origine
    
    Le message en texte brut obtenu peut être représenté dans les formats suivants :
    
      - message conforme à la norme RFC 2822 composé uniquement de texte US-ASCII avec une pièce jointe Winmail.dat codée en Uuencode
    
      - message multipart codé MIME contenant une pièce jointe Winmail.dat
    
    Un client de messagerie compatible MAPI qui comprend parfaitement le format TNEF, comme c'est le cas de Outlook, traite la pièce jointe Winmail.dat et affiche le contenu du message d’origine sans jamais afficher la pièce jointe Winmail.dat. Un client de messagerie ne comprenant pas le format TNEF peut présenter un message TNEF de l’une des manières suivantes :
    
      - La version en texte brut du message s'affiche et le message contient une pièce jointe nommée Winmail.dat, Win.dat ou à l'aide d'un autre nom générique tel que Att*nnnnn*.dat ou Att*nnnnn*.eml où l'espace réservé *nnnnn* représente un numéro aléatoire.
    
      - La version en texte brut du message s'affiche. La pièce jointe TNEF est ignorée ou supprimée. Le résultat est un message en texte brut.
    
      - Les serveurs de messagerie qui comprennent le format TNEF peuvent être configurés pour supprimer les pièces jointes TNEF des messages entrants. Le résultat est un message en texte brut. En outre, certains clients de messagerie tels que Microsoft Outlook Express peuvent ne pas comprendre le format TNEF, mais reconnaître et ignorer les pièces jointes TNEF. Le résultat est un message en texte brut.
    
    Certains utilitaires tiers peuvent aider à convertir des pièces jointes Winmail.dat.
    
    TNEF est compris par toutes les versions d’Exchange depuis Exchange Server version 5.5.

  - **STNEF (Summary Transport Neutral Encapsulation Format)**   STNEF équivaut à TNEF. Toutefois, les messages STNEF sont codés différemment des messages TNEF. Plus précisément, les messages STNEF sont toujours codés MIME et ont toujours une valeur Content-Transfer-Encoding de Binary. C'est pourquoi il n'y a pas de représentation en texte brut du message ni de pièce jointe Winmail.dat distincte contenue dans le corps du message. Le message entier est représenté uniquement à l'aide de données binaires. Les messages qui ont une valeur Content-Transfer-Encoding de Binary ne peuvent être transférés qu'entre des serveurs de messagerie SMTP qui prennent en charge et annoncent les extensions BINARYMIME et CHUNKING SMTP définies dans la norme RFC 3030. Les messages sont toujours transférés entre messageries SMTP à l'aide de la commande BDAT au lieu de la commande DATA standard.
    
    Le format STNEF est compris par toutes les versions d’Exchange depuis Exchange 2000. Le format STNEF est automatiquement utilisé pour tous les messages transférés entre des serveurs Exchange au sein de l’organisation, et ce depuis le mode natif de Exchange Server 2003.
    
    Exchange n’envoie jamais de message au format STNEF à des destinataires externes. Seuls des messages TNEF peuvent être envoyés à des destinataires en dehors de l’organisation Exchange.

Retour au début

## Options de conversion de contenu pour des destinataires externes

Les options de conversion de contenu configurables dans une organisation Exchange pour des destinataires externes sont décrites dans les catégories suivantes :

  - **Options de conversion TNEF**   Ces options de conversion indiquent si le format TNEF (Transport Neutral Encapsulation Format) doit être préservé ou supprimé des messages sortants de l’organisation Exchange.

  - **Options de codage des messages**   Ces options spécifient les options de codage des messages, telles que les jeux de caractères MIME et non-MIME, le codage des messages et les formats des pièces jointes.

Ces options de conversion et de codage sont indépendantes l'une de l'autre. Par exemple, le fait que des messages TNEF puissent quitter l’organisation Exchange n’est pas lié aux paramètres d’encodage MIME ou de texte brut de ces messages.

Vous pouvez indiquer la conversion de contenu à divers niveaux de l’organisation Exchange, tels que décrits dans la liste suivante :

  - **Paramètres de domaine distant**   Les domaines distants permettent de définir des paramètres de transfert des messages sortants entre l’organisation Exchange et des domaines externes. Même si vous ne créez pas d'entrée de domaine distant pour des domaines spécifiques, il existe un domaine distant prédéfini, nommé Default, qui s'applique à tous les espaces d'adressage distants ( \* ).

  - **Paramètres d’utilisateur de messagerie et de contact de messagerie**   Les utilisateurs de messagerie et les contacts de messagerie sont similaires : ils ont des adresses de messagerie externes et contiennent des informations sur des personnes externes à l’organisation Exchange. La différence principale est la suivante : les utilisateurs de messagerie disposent de comptes qui peuvent être utilisés pour ouvrir une session dans le domaine Active Directory et accéder à des ressources de l’organisation.

  - **Paramètres Outlook**   Outlook vous permet de définir les options de mise en forme et d’encodage des messages décrites dans la liste suivante :
    
      - **Format des messages**   Permet de définir le format de message par défaut pour tous les messages. Vous pouvez également remplacer le format de message par défaut à mesure que vous composez un message spécifique.
    
      - **Format des messages Internet**   Permet de contrôler si des messages de format TNEF sont envoyés à des destinataires distants ou s'ils sont d'abord convertis en un format plus compatible. Vous pouvez également spécifier diverses options de codage pour les messages envoyés à des destinataires distants. Ces paramètres ne s’appliquent pas aux messages envoyés à des destinataires au sein de l’organisation Exchange.
    
      - **Format de message de destinataire Internet**   Permet de contrôler si des messages de format TNEF sont envoyés à des destinataires spécifiques ou s'ils sont d'abord convertis en un format plus compatible. Vous pouvez définir les options de conversion pour des contacts spécifiques dans le dossier Contacts ainsi que remplacer des options de conversion pour un destinataire spécifique dans les champs À :, Cc et Cci : Ces options de conversion ne sont pas disponibles pour des destinataires de l'organisation Exchange.
    
      - **Options de codage de message de destinataire Internet**   Permet de contrôler les options de codage MIME ou de texte brut pour des contacts spécifiques dans votre dossier Contacts ; vous pouvez également remplacer les options de conversion pour un destinataire spécifique dans les champs À :, Cc et Cci lorsque vous composez un message. Ces options de conversion ne sont pas disponibles pour des destinataires de l'organisation Exchange.
    
      - **Options internationales**   Vous pouvez contrôler les jeux de caractères utilisés dans les messages.

## Options de conversion TNEF

Vous pouvez spécifier les options de conversion TNEF aux niveaux suivants :

  - paramètres de domaine distant

  - paramètres d’utilisateur et de contact de messagerie

  - Paramètres d’Outlook, y compris :
    
      - format des messages
    
      - format de message Internet
    
      - format de message de destinataire Internet

## Options d’encodage des messages

Vous pouvez indiquer les options d’encodage des messages aux niveaux suivants :

  - Paramètres de domaine distant

  - paramètres d’utilisateur et de contact de messagerie

  - Paramètres d’Outlook, y compris :
    
      - format des messages
    
      - message Internet
    
      - format de message de destinataire Internet
    
      - options de codage de jeu de caractères de message

Pour plus d'informations, consultez [Options d’encodage des messages](message-encoding-options-exchange-2013-help.md).

Retour au début

## Compréhension de la structure des messages électroniques

Pour mieux comprendre les options de conversion de contenu pour les destinataires externes, vous devez comprendre la structure des messages électroniques. Un message SMTP est basé sur du texte brut US-ASCII 7 bits pour la composition et l’envoi de messages électroniques. Un message SMTP standard comprend les éléments suivants :

  - **Enveloppe du message**   L'enveloppe du message est définie en RFC 2821. Elle contient les informations requises pour transmettre et remettre le message. Les destinataires ne voient jamais l'enveloppe du message, car elle est générée par le processus de transmission du message et ne fait pas partie du contenu du message.

  - **Contenu du message**   Le contenu du message est défini en RFC 2822. Il comprend les éléments suivants :
    
      - **En-tête du message**   L'en-tête du message est un ensemble de champs d'en-tête. Les champs d'en-tête se composent d'un champ name, suivi du caractère deux-points ( : ), suivi d'un champ body, puis d'une combinaison de caractères de retour chariot/retour à la ligne (CR/LF).
        
        Un champ name doit être composé de caractères de texte US-ASCII imprimables, à l'exception du caractère deux-points ( : ). Plus précisément, les caractères ASCII autorisés doivent avoir des valeurs comprises entre 33 et 57 et entre 59 et 126.
        
        Un champ body peut contenir tout caractère US-ASCII, à l'exception du caractère de retour chariot (CR) et du caractère de retour à la ligne (LF). Toutefois, un champ body peut contenir la combinaison de caractères CR/LF en cas d’utilisation dans le *pliage d’en-tête*. Le pliage d'en-tête est la séparation d'un champ body d'en-tête en plusieurs lignes conformément à la description de la section 2.2.3 de la norme RFC 2822. D'autres exigences de syntaxe concernant le champ body sont décrites dans les sections 3 et 4 de la norme RFC 2822.
    
      - **Corps du message**   Le corps du message est un ensemble de lignes de caractères de texte US-ASCII qui s'affichent après l'en-tête du message. L'en-tête du message et le corps du message sont séparés par une ligne vide qui se termine par la combinaison de caractères CR/LF. Le corps du message est facultatif. Une ligne de texte dans le corps du message doit compter moins de 998 caractères. Les caractères CR et LF ne peuvent apparaître ensemble que pour indiquer la fin d'une ligne.

Si des messages SMTP contiennent des éléments qui ne sont pas du texte brut US-ASCII, il faut coder le message pour préserver ces éléments. La norme MIME définit une méthode de codage du contenu non-texte des messages. MIME autorise du texte dans d'autres jeux de caractères, des pièces jointes sans texte, des corps de message en plusieurs parties et des champs d'en-tête dans d'autres jeux de caractères. MIME est défini dans les normes RFC 2045, RFC 2046, RFC 2047, RFC 2048 et RFC 2077. MIME définit un ensemble de champs d'en-tête qui spécifient des attributs de message supplémentaires. Le tableau suivant décrit certains champs d'en-tête MIME importants.

### Champ d'en-tête MIME importants

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de champ d'en-tête</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version MIME</p></td>
<td><p>1.0</p></td>
<td><p>Ce champ d'en-tête et le premier champ d'en-tête MIME apparaissant dans un message au format MIME. Ce champ d'en-tête apparaît après les autres champs d'en-tête RFC 2822 standard mais avant tout autre champ d'en-tête MIME. Les clients de messagerie compatibles MIME utilisent ce champ d’en-tête pour identifier un message encodé MIME. Lorsque ce champ d’en-tête est absent, les clients de messagerie compatibles MIME identifient le message comme étant en texte brut.</p></td>
</tr>
<tr class="even">
<td><p>Content-Type</p></td>
<td><p>text/plain</p></td>
<td><p>Ce champ d'en-tête identifie le type de média du contenu du message, comme décrit dans la norme RFC 2046. Un type de média consiste en un type, un sous-type et un ou plusieurs paramètres facultatifs, tel qu'un paramètre <em>charset=</em> définissant le codage de caractères MIME. Les types commençant par « x- » ne sont pas standard. Les sous-types commençant par « vnd. » sont spécifiques au fournisseur. L'IANA (Internet Assigned Numbers Authority) conserve une liste des types de médias enregistrés. Pour plus d'informations, consultez la page Web présentant les <a href="https://www.iana.org/assignments/media-types/">types de médias MIME</a>.</p>
<p>Le type de média <em>multipart</em> permet de composer un message contenant plusieurs parties en utilisant des sections définies par différents types de médias. text/plain, text/html, multipart/mixed et multipart/alternative sont certaines des valeurs du champ Content-Type.</p></td>
</tr>
<tr class="odd">
<td><p>Content-Transfer-Encoding</p></td>
<td><p>7bit</p></td>
<td><p>Ce champ d'en-tête peut décrire les informations suivantes sur un message :</p>
<ul>
<li><p>l'algorithme de codage utilisé pour transformer toute donnée texte ou binaire non-US-ASCII existant dans le corps du message.</p></li>
<li><p>un indicateur décrivant la condition actuelle du corps du message.</p></li>
</ul>
<p>Le champ d'en-tête Content-Transfer-Encoding d'un message MIME peut prendre plusieurs valeurs. Lorsqu'il apparaît dans l'en-tête du message, il s'applique à l'ensemble du corps du message. Lorsqu'il apparaît dans une des parties d'un message multipart, il ne s'applique qu'à cette partie du message.</p>
<p>Quand un algorithme de codage est appliqué aux données du corps du message, celles-ci sont transformées en texte brut US-ASCII. Cette transformation permet au message de transiter sur des serveurs de messagerie SMTP plus anciens qui ne prennent en charge que les messages en texte US-ASCII. Les valeurs du champ d'en-tête Content-Transfer-Encoding indiquant qu'un algorithme de codage a été utilisé pour le corps du message sont les suivantes :</p>
<ul>
<li><p><strong>Quoted-printable</strong>   Cet algorithme de codage utilise des caractères US-ASCII imprimables pour coder les données du corps du message. Si le texte du message d'origine est essentiellement du texte US-ASCII, le codage Quoted-printable fournit des résultats relativement lisibles et compacts. Tous les caractères de texte US-ASCII imprimables à l'exception du signe égal (=) peuvent être représentés sans codage.</p></li>
<li><p><strong>Base64</strong>   Cet algorithme de codage est principalement basé sur le standard Privacy-Enhanced Mail (PEM) défini dans la norme RFC 1421. Le codage Base64 utilise l'algorithme de codage alphabétique de 64 caractères alphabet et les caractères de remplissage de sortie définis par PEM pour coder les données du corps du message. Un message codé Base64 est généralement 33 pour cent plus volumineux que le message d'origine. Le codage Base64 crée un accroissement prévisible de la taille du message et convient parfaitement pour des données binaires et du texte non-US-ASCII.</p></li>
</ul>
<p>Il est rare que plusieurs algorithmes de codage soient utilisés dans le même message.</p>
<p>Si aucun algorithme de codage n'est utilisé dans le corps du message, le champ d'en-tête Content-Transfer-Encoding identifie simplement la condition actuelle des données du corps du message. Les valeurs du champ d'en-tête Content-Transfer-Encoding indiquant qu'aucun algorithme de codage n\a été utilisé pour le corps du message sont les suivantes :</p>
<ul>
<li><p><strong>7bit</strong>    Cette valeur indique que les données du corps du message sont déjà au format RFC 2822. Plus précisément, cela signifie que les conditions suivantes doivent être remplies :</p>
<ul>
<li><p>Les lignes de texte doivent compter moins de 998 caractères.</p></li>
<li><p>Tous les caractères doivent être des caractères de texte US-ASCII de la plage de valeurs 1 à 127.</p></li>
<li><p>Les caractères CR et LF ne peuvent apparaître ensemble que pour indiquer la fin d'une ligne de texte.</p></li>
</ul>
<p>Le corps du message tout entier peut être 7bit ou, s'il s'agit d'un message de type multipart, seule une partie du message peut être 7bit. Si le message multipart contient d'autres parties comprenant des données binaires ou du texte non-US-ASCII, cette partie du message doit être codée à l'aide des algorithmes de codage Quoted-printable ou Base64.</p>
<p>Des messages ayant un corps 7bit peuvent voyager entre des serveurs de messagerie SMTP grâce à la commande DATA standard.</p></li>
<li><p><strong>8bit</strong>    Cette valeur indique que les données du corps du message contiennent des caractères non-US-ASCII. Plus précisément, cela signifie que les conditions suivantes doivent être remplies :</p>
<ul>
<li><p>Les lignes de texte doivent compter moins de 998 caractères.</p></li>
<li><p>Un ou plusieurs caractères du corps du message ont des valeurs supérieures aux valeurs US-ASCII 127.</p></li>
<li><p>Les caractères CR et LF ne peuvent apparaître ensemble que pour indiquer la fin d'une ligne de texte.</p></li>
</ul>
<p>Le corps du message tout entier peut être 8bit ou, s'il s'agit d'un message de type multipart, seule une partie du message peut être 8bit. Si le message multipart contient d'autres parties comprenant des données binaires, cette partie du message doit être codée à l'aide des algorithmes de codage Quoted-printable ou Base64.</p>
<p>Les messages dont le corps est en 8bit ne peuvent voyager qu’entre des serveurs de messagerie SMTP qui prennent en charge l’extension SMTP 8BITMIME définie dans la norme RFC 1652, tels que des serveurs exécutant Exchange 2000 Server ou des versions plus récentes. Plus précisément, cela signifie que les conditions suivantes doivent être remplies :</p>
<ul>
<li><p>Le mot clé 8BITMIME doit être annoncé dans la réponse EHLO du serveur.</p></li>
<li><p>Les messages sont malgré tout transférés à l'aide de la commande DATA standard du protocole SMTP. Toutefois, le paramètre BODY=8BITMIME doit être ajouté à la fin de la commande MAIL FROM.</p></li>
</ul></li>
<li><p><strong>Binary</strong>    Cette valeur indique que les données du corps du message contiennent du texte non-US-ASCII ou des données binaires. Plus précisément, cela signifie que les conditions suivantes sont remplies :</p>
<ul>
<li><p>Toute séquence de caractères est autorisée.</p></li>
<li><p>Il n'existe aucune limitation à la longueur de ligne.</p></li>
<li><p>Les éléments de message binaires ne nécessitent pas de codage.</p></li>
</ul>
<p>Les messages dont le corps est Binary ne peuvent voyager qu’entre des serveurs de messagerie SMTP qui prennent en charge l’extension SMTP BINARYMIME définie dans la norme RFC 3030, tels que des serveurs exécutant Exchange 2000 Server ou des versions plus récentes. Plus précisément, cela signifie que les conditions suivantes doivent être remplies :</p>
<ul>
<li><p>Le mot clé BINARYMIME doit être annoncé dans la réponse EHLO du serveur.</p></li>
<li><p>L'extension SMTP BINARYMIME ne peut être utilisée qu'avec l'extension SMTP CHUNKING. <em>Chunking</em> permet d'envoyer des corps de message volumineux en plusieurs blocs de plus petite taille. L'extension Chunking est également définie dans la norme RFC 3030. Le mot clé CHUNKING doit également être annoncé dans la réponse EHLO du serveur.</p></li>
<li><p>Les messages sont transférés à l'aide de la commande BDAT au lieu de la commande DATA standard.</p></li>
<li><p>Le paramètre <em>BODY=BINARYMIME</em> doit être ajouté à la fin de la commande MAIL FROM si le message contient un corps de message.</p></li>
</ul></li>
</ul>
<p>Les valeurs 7bit, 8bit et Binary ne coexistent jamais dans un message multipart. Ces valeurs s'excluent mutuellement. Les valeurs Quoted-printable ou Base64 peuvent apparaître dans un corps de message multipart 7bit ou 8bit, mais jamais dans un corps de message Binary. Si un corps de message multipart contient plusieurs parties composées de contenu 7bit et 8bit, le message entier est classifié 8bit. Si un corps de message multipart contient plusieurs parties composées de contenu 7bit, 8bit et Binary, le message entier est classifié Binary.</p></td>
</tr>
<tr class="even">
<td><p>Content-Disposition</p></td>
<td><p>Pièce jointe</p></td>
<td><p>Ce champ d’en-tête indique à un client de messagerie compatible MIME la manière d’afficher un fichier joint ; il est décrit dans la norme RFC 2183. Les valeurs de ce champ peuvent être Inline ou Attachment. Si la valeur de ce champ est Inline, la pièce jointe s'affiche dans le corps du message. Si la valeur de ce champ est Attachment, le fichier joint s'affiche comme pièce jointe ordinaire séparée du corps du message. D'autres paramètres sont disponibles si la valeur est Attachment, tels que Filename, Creation-date et Size.</p></td>
</tr>
</tbody>
</table>


Retour au début

