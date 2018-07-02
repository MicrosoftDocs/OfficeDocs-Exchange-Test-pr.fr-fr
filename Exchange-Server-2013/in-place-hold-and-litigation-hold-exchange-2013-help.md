---
title: 'Conservation inaltérable et conservation pour litige: Exchange 2013 Help'
TOCTitle: Conservation inaltérable et conservation pour litige
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 50478427
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conservation inaltérable et conservation pour litige

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-11-15_

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous avons différé la date d’échéance du 1er juillet 2017 pour créer des conservations inaltérables dans Exchange Online (dans les plans autonomes Office 365 et Exchange Online). Mais plus tard cette année ou au début de l’année prochaine, vous ne pourrez pas créer des conservations inaltérables dans Exchange Online. Au lieu d’utiliser des conservations inaltérables, vous pouvez avoir recours à des <a href="https://go.microsoft.com/fwlink/?linkid=780738">cas de découverte électronique</a> ou des <a href="https://go.microsoft.com/fwlink/?linkid=827811">stratégies de rétention</a> dans le centre de sécurité et conformité Office 365. Lorsque nous aurons désactivé les nouvelles conservations inaltérables, vous pourrez toujours modifier les conservations inaltérables existantes. La création de conservations inaltérables sera toujours prise en charge dans les déploiements hybrides Exchange Server 2013 et Exchange . Vous serez également toujours en mesure de mettre des boîtes aux lettres en conservation pour litige.</td>
</tr>
</tbody>
</table>


Lorsqu’une situation de litige est vraisemblablement à craindre, les organisations ont pour obligation de conserver les informations pertinentes qui sont stockées électroniquement (ESI), y compris la messagerie. Cette exigence de stockage de la correspondance électronique existe souvent avant que les détails précis du litige soient connus, et la conservation s’applique généralement à un grand nombre d’éléments. Les organisations devront éventuellement conserver tous les messages électroniques concernant un sujet spécifique, ou tous les messages de certaines personnes. En fonction des pratiques de découverte électronique (eDiscovery) de l’organisation, les mesures suivantes peuvent être adoptées pour conserver la messagerie électronique :

  - Les utilisateurs finaux peuvent être contraints de conserver tout leur courrier électronique en ne supprimant aucun message. Toutefois, les utilisateurs peuvent toujours supprimer quand même des messages électroniques, que ce soit sciemment ou par inadvertance.

  - Les mécanismes de suppression automatique tels que la gestion des enregistrements de messagerie peuvent être suspendus. Ceci peut provoquer une saturation de la boîte aux lettres de l’utilisateur qui contient un grand nombre de messages électroniques, et affecter la productivité de l’utilisateur. Qui plus est, le fait d’interrompre la procédure de suppression automatique n’empêche pas les utilisateurs de supprimer manuellement des messages électroniques.

  - Certaines organisations copient ou déplacent leurs messages électroniques vers une archive pour s’assurer que les messages ne sont pas supprimés, modifiés ou falsifiés. Ces organisations font alors face à une augmentation des coûts, en raison des efforts manuels consentis pour la copie ou le déplacement des messages dans une archive, ou des produits tiers utilisés pour collecter et stocker le courrier électronique en dehors d’Exchange.

En cas de non-conservation du courrier électronique, une organisation peut s’exposer à des risques juridiques et financiers, notamment à un examen de ses processus de découverte et de rétention des enregistrements, à des amendes, des sanctions ou des condamnations.

Vous pouvez utiliser la conservation inaltérable et la conservation pour litige pour accomplir les tâches suivantes :

  - Blocage de boîtes aux lettres utilisateur sur place et conservation immuable des éléments de la boîte aux lettres

  - Conserver les éléments de boîte aux lettres supprimés par les utilisateurs ou les processus de suppression automatique, tels que la gestion des enregistrements de messagerie (MRM)

  - Utiliser l’archive permanente basée sur une requête pour rechercher et conserver des éléments répondant aux critères spécifiés.

  - Conserver les éléments indéfiniment ou pendant une durée spécifique.

  - Soumettre un utilisateur à plusieurs suspensions pour différentes procédures ou enquêtes.

  - Garantir la transparence de la conservation des messages pour l’utilisateur sans devoir suspendre la gestion des enregistrements de messagerie

  - Autoriser les recherches de découverte électronique inaltérable dans les éléments mis en attente

**Contenu de cette rubrique**

Scénarios de blocage sur place

Conservation inaltérable et conservation pour litige

Placement d’une boîte aux lettres en blocage sur place (In-Place Hold)

Placer des dossiers publics en conservation

Conservations et dossier Éléments récupérables

Conservations et quotas de boîte aux lettres

Conservations et transfert du courrier électronique

Conservation du contenu Lync archivé

Suppression d'une boîte aux lettres en attente

Migration de boîtes aux lettres en attente à partir d'Exchange 2013 vers Office 365

## Scénarios de blocage sur place

Dans Exchange Server 2010, la notion de blocage légal implique le blocage de toutes les données de boîte aux lettres d’un utilisateur, indéfiniment ou jusqu’à la suppression du blocage. Dans Exchange 2013, le blocage sur place constitue un nouveau modèle qui vous permet de spécifier les paramètres suivants :

  - **Que mettre en attente ?**   Vous pouvez définir les éléments à mettre en attente à l’aide de paramètres de requête comme des mots-clés, des expéditeurs et des destinataires, des dates de début et de fin, mais aussi spécifier les types de messages (messages électroniques ou éléments de calendrier) que vous souhaitez mettre en attente.

  - **Bloquer pendant combien de temps**   Vous pouvez spécifier une durée pour les éléments bloqués.

Avec ce nouveau modèle, le blocage sur place (In-Place Hold) vous permet de créer des stratégies de blocage précises afin de conserver des éléments de boîte aux lettres dans les scénarios suivants :

  - **Conservation indéfinie**   Le scénario de conservation indéfinie est semblable à la conservation pour litige. Il vise à conserver les éléments de boîte aux lettres de façon à respecter les exigences de découverte électronique. Pendant la période de litige ou d’enquête, les éléments ne sont jamais supprimés. La durée n’est pas connue à l’avance ; aucune date de fin n’est donc configurée. Pour mettre en attente indéfiniment tous les éléments de messagerie électronique, vous ne spécifiez ni paramètres de requête ni durée lors de la création d’une conservation inaltérable.

  - **Blocage basé sur une requête**   Si votre organisation conserve des éléments selon les paramètres de requête spécifiés, vous pouvez utiliser un blocage sur place basé sur une requête. Vous pouvez spécifier des paramètres de requête comme des mots-clés, des dates de début et de fin, des adresses d’expéditeur et de destinataire ou encore des types de messages. Une fois que vous avez créé un blocage sur place basé sur une requête, tous les éléments de boîte aux lettres existants et futurs (notamment les messages reçus à une date ultérieure) qui correspondent aux paramètres de requête sont conservés.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les éléments marqués comme ne pouvant pas faire l’objet d’une recherche, généralement en raison de l’échec d’indexation d’une pièce jointe, sont également conservés, car il est impossible de déterminer s’ils correspondent aux paramètres de la requête. Pour plus d’informations sur l’élément ne pouvant pas faire l’objet d’une recherche, voir <a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Éléments impossibles à rechercher dans la découverte électronique Exchange</a>.</td>
    </tr>
    </tbody>
    </table>


  - **Conservation à durée définie**   La conservation inaltérable et la conservation pour litige vous permettent de spécifier une durée pendant laquelle mettre en attente les éléments. La durée est calculée à compter de la date de réception ou de création de l’élément de boîte aux lettres.
    
    Si votre organisation requiert que tous les éléments de boîte aux lettres soient conservés pendant une période donnée (7 ans, par exemple), vous pouvez créer un blocage basé sur la durée. Dans Exchange 2013, vous pouvez spécifier une période de rétention des éléments. La durée de blocage des éléments bloqués est calculée à partir de leur date de réception. Par exemple, envisagez de placer une boîte aux lettres en blocage sur place basé sur la durée et définissez une période de rétention sur 365 jours. Si un élément d’une boîte aux lettres est supprimé au bout de 300 jours à compter de la date à laquelle il a été reçu, il est conservé pendant une période supplémentaire de 65 jours avant d’être définitivement supprimé. Vous pouvez appliquer un blocage sur place basé sur la durée conjointement avec une stratégie de rétention pour vous assurer que les éléments seront conservés pendant la durée spécifiée et qu’ils seront définitivement supprimés une fois cette période terminée.

Vous pouvez utiliser la conservation inaltérable pour placer un utilisateur dans plusieurs conservations. Lorsqu’un utilisateur est placé dans plusieurs conservations, les requêtes de recherche provenant de toute conservation fondée sur une requête sont combinées (avec des opérateurs **OR**). Dans ce cas, le nombre maximal de mots-clés dans toutes les conservations fondées sur une requête placées dans une boîte aux lettres s’élève à 500. S’il existe plus de 500 mots-clés, tout le contenu de la boîte aux lettres est placé en conservation (et pas seulement le contenu correspondant aux critères de recherche). Tout le contenu est placé en conservation jusqu’à ce que le nombre total de mots-clés soit réduit à 500 ou moins.

Retour au début

## Conservation inaltérable et conservation pour litige

Conservation pour litige, la fonction de conservation introduite dans Exchange 2010 afin de conserver les données pour la découverte électronique (eDiscovery), est toujours disponible dans Exchange 2013. La conservation pour litige utilise la propriété **LitigationHoldEnabled** d’une boîte aux lettres. Tandis que la conservation inaltérable offre une fonctionnalité de conservation précise basée sur les paramètres de requête et la possibilité de placer plusieurs blocages. La conservation pour litige vous permet uniquement de placer tous les éléments en conservation. Vous pouvez également spécifier une durée pour conserver les éléments lorsqu’une boîte aux lettres est conservée pour litige. La durée est calculée à compter de la date de réception ou de création de l’élément de boîte aux lettres. Si une durée n’est pas définie, les éléments sont conservés indéfiniment ou jusqu’à ce que la conservation soit supprimée.

Lorsqu’une boîte aux lettres est placée simultanément sur une ou plusieurs conservations inaltérables et une conservation pour litige (sans indication de durée), tous les éléments sont conservés indéfiniment ou jusqu’à la suppression des conservations. Si vous supprimez la conservation pour litige et que l’utilisateur est toujours placé sur une ou plusieurs conservations inaltérables, les éléments correspondant aux critères Conservation inaltérable sont conservés pendant la période spécifiée dans les paramètres de conservation. Lorsque vous déplacez une boîte aux lettres conservée pour litige dans Exchange 2010 vers un serveur de boîtes aux lettres Exchange 2013, le paramètre de conservation pour litige continue de s’appliquer, ce qui garantit que les exigences de conformité sont respectées pendant et après le déplacement.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous placez une boîte aux lettres en conservation inaltérable ou en conservation pour litige, la conservation porte à la fois sur la boîte aux lettres d’archivage et la boîte aux lettres principale. Si vous placez une boîte aux lettres principale locale en conservation inaltérable dans un déploiement hybride Exchange, la boîte aux lettres d’archivage en nuage (si activée) est également placée en conservation inaltérable.</td>
</tr>
</tbody>
</table>


Pour plus d’informations, consultez les rubriques suivantes :

  - [Placement d’une boîte aux lettres en conservation pour litige](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [Placement de toutes les boîtes aux lettres en conservation](place-all-mailboxes-on-hold-exchange-2013-help.md)

## Placement d’une boîte aux lettres en blocage sur place (In-Place Hold)

Les utilisateurs autorisés qui ont été ajoutés au groupe de rôles de contrôle d’accès basé sur les rôles (RBAC) [Gestion de la détection](discovery-management-exchange-2013-help.md), ou auxquels les rôles de gestion de blocage légal et de recherche dans les boîtes aux lettres ont été attribués, peuvent placer des utilisateurs de boîte aux lettres en blocage sur place (In-Place Hold). Vous pouvez déléguer la tâche aux responsables des enregistrements, aux responsables de la mise en conformité ou aux avocats du service juridique de votre organisation en affectant le moins de privilèges possible. Pour en savoir plus sur l’affectation du groupe de rôles Gestion de la découverte, voir [Attribution d’autorisations eDiscovery dans Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange 2010, le rôle de conservation légale fournit les autorisations nécessaires aux utilisateurs pour placer des boîtes aux lettres en conservation pour litige. Dans Exchange 2013, vous pouvez utiliser la même autorisation pour placer des boîtes aux lettres en blocage sur place indéfini ou basé sur la durée. Cependant, pour créer un blocage sur place basé sur une requête, l’utilisateur doit se voir attribuer le rôle de recherche dans les boîtes aux lettres. Ces deux rôles sont attribués au groupe de rôles Gestion de la découverte.</td>
</tr>
</tbody>
</table>


Dans Exchange 2013, la fonctionnalité de blocage sur place (In-Place Hold) est intégrée aux recherches de découverte électronique sur place (In-Place eDiscovery). Vous pouvez utiliser l’Assistant **Découverte électronique et blocage sur place** du Centre d’Administration Exchange (EAC) ou la cmdlet **New-MailboxSearch** et autres commandes associées dans l’environnement de ligne de commande Exchange Management Shell pour placer une boîte aux lettres en blocage sur place. Pour en savoir plus sur le placement d’une boîte aux lettres en blocage sur place, consultez la rubrique [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez l’archivage Exchange Online pour configurer une archive basée sur le cloud pour vos boîtes aux lettres locales, vous devez gérer la conservation inaltérable à partir de votre organisation Exchange 2013 locale. Les paramètres de blocage sont automatiquement propagés à l’archive basée sur le cloud via DirSync. Comme indiqué précédemment, lorsque vous placez une boîte aux lettres locale en attente, l’archive basée sur le cloud correspondante est également placée en attente.</td>
</tr>
</tbody>
</table>


De nombreuses organisations sont tenues d’informer les utilisateurs lorsque les boîtes aux lettres de ces derniers sont soumises à un blocage. Qui plus est, lorsqu’une boîte aux lettres fait l’objet d’un blocage, il n’est pas nécessaire que les stratégies de rétention qui s’appliquent à l’utilisateur de boîte aux lettres soient suspendues. Étant donné que la suppression des messages se poursuit normalement, les utilisateurs ne remarquent pas forcément qu’ils font l’objet d’un blocage. Si votre organisation nécessite que les utilisateurs bloqués en soient informés, vous pouvez ajouter un message de notification à la propriété **Retention Comment** de l’utilisateur de boîte aux lettres et utiliser la propriété **RetentionUrl** pour établir un lien vers une page Web pour plus d’informations. Outlook 2010 et versions ultérieures affiche la notification et l’URL dans la zone en arrière-plan. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell afin d’ajouter et de gérer ces propriétés pour une boîte aux lettres.

Retour au début

## Placer des dossiers publics en conservation

Dans Exchange Online, vous pouvez placer des dossiers publics en conservation en utilisant une conservation inaltérable. La conservation pour litige des dossiers publics n’est pas prise en charge. Lorsque vous créez une conservation inaltérable, vous devez placer tous les dossiers publics de votre organisation en conservation. Au final, toutes les boîtes aux lettres de dossiers publics sont placées en conservation inaltérable.

De plus, lorsque vous placez des dossiers publics en conservation inaltérable, les messages électroniques liés à la synchronisation de la hiérarchie des dossiers publics sont également conservés. Cela peut entraîner la conservation de milliers de messages électroniques associés à ce processus. Ces messages peuvent remplir le quota de stockage du dossier Éléments récupérables situé dans les boîtes aux lettres de dossiers publics. Pour éviter cela, vous pouvez créer une conservation inaltérable basée sur une requête et ajouter la paire `property:value` suivante à la requête de recherche :

    NOT(subject:HierarchySync*)

Ainsi, les messages (liés à la synchronisation de la hiérarchie de dossier public) dont la ligne d’objet contient le terme « HierarchySync » ne seront pas placés en conservation.

## Conservations et dossier Éléments récupérables

La conservation inaltérable et la conservation pour litige utilisent le dossier Éléments récupérables pour conserver les éléments. Le dossier Éléments récupérables remplace la fonction communément appelée *conteneur de dépôt* dans les versions précédentes d’Exchange. En mode d’affichage par défaut de Outlook, Outlook Web App et d’autres clients de messagerie, le dossier Éléments récupérables n’est pas visible. Pour plus d’informations sur le dossier Éléments récupérables, voir [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

Par défaut, lorsqu’un utilisateur supprime un message d’un dossier autre que le dossier Éléments supprimés, le message est déplacé vers le dossier Éléments supprimés. C'est ce qu’on appelle un *transfert*. Lorsqu’un utilisateur procède à la *suppression réversible* d’un élément (en appuyant sur les touches MAJ et SUPPR) ou supprime un élément du dossier Éléments supprimés, le message est placé dans le dossier Éléments récupérables et n’est donc plus visible.

Les éléments du dossier Éléments récupérables sont conservés pendant une durée correspondant à la période de rétention des éléments supprimés qui est configurée dans la base de données de boîtes aux lettres de l’utilisateur. Par défaut, la période de rétention des éléments supprimés est de 14 jours pour les bases de données de boîtes aux lettres. Vous pouvez également configurer un quota de stockage pour le dossier Éléments récupérables. Ce quota permet à l’organisation de se prémunir contre une éventuelle attaque par déni de service due à l’augmentation rapide de la taille du dossier Éléments récupérables, et par conséquent de la base de données de boîtes aux lettres. Si une boîte aux lettres n’est pas placée en conservation inaltérable ou en conservation pour litige, les éléments sont supprimés définitivement du dossier Éléments récupérables selon la méthode « premier entré, premier sorti » lorsque le quota d’avertissement de stockage du dossier Éléments récupérables est dépassé ou lorsque les éléments ont été stockés dans ce dossier pendant une durée supérieure à la période de rétention des éléments supprimés.

Le dossier Éléments récupérables contient les sous-dossiers suivants qui permettent de stocker les éléments supprimés dans différents sites et de faciliter la procédure de conservation inaltérable et de conservation pour litige :

  - **Suppressions**   Les éléments supprimés du dossier Éléments supprimés ou supprimés provisoirement d’autres dossiers sont déplacés vers le sous-dossier Suppressions et sont visibles lorsque l’utilisateur recourt à la fonction de récupération des éléments supprimés dans Outlook et Outlook Web App. Par défaut, les éléments résident dans ce dossier jusqu’à l’expiration de la période de rétention des éléments supprimés qui est configurée pour la base de données de boîtes aux lettres.

  - **Purges**   Lorsqu’un utilisateur supprime un élément du dossier Éléments récupérables (à l’aide de l’outil de récupération des éléments supprimés dans Outlook et Outlook Web App), l’élément est déplacé vers le dossier Purges. Les éléments ayant été conservés pour une durée supérieure à la période de rétention des éléments supprimés configurée sur la base de données de boîtes aux lettres ou la boîte aux lettres sont également déplacés vers le dossier Purges. L’utilisateur ne peut pas voir les éléments de ce dossier s’il recourt à l’outil de récupération des éléments supprimés. Lorsque l’Assistant de boîte aux lettres traite la boîte aux lettres, les éléments du dossier Purges sont purgés de la base de données de boîtes aux lettres. Lorsque vous placez la boîte aux lettres de l’utilisateur en conservation pour litige, l’Assistant de boîte aux lettres ne purge pas les éléments de ce dossier.

  - **DiscoveryHold**   Si un utilisateur est placé sur un blocage sur place, les éléments supprimés sont déplacés vers ce dossier. Lorsque l’Assistant de boîte aux lettres traite la boîte aux lettres, il évalue les messages dans ce dossier. Les éléments qui correspondent à la requête de blocage sur place (In-Place Hold) sont conservés jusqu’à la fin de la période de blocage spécifiée dans la requête. Si aucune période de blocage n’est définie, les éléments sont bloqués indéfiniment ou jusqu’à ce que l’utilisateur soit supprimé du blocage.

  - **Versions**   Lorsqu’un utilisateur est placé en conservation inaltérable ou en conservation pour litige, les éléments de boîte aux lettres doivent être protégés de toute falsification ou modification pouvant être réalisée par l’utilisateur ou un processus. Un processus de *copie sur écriture* permet de bénéficier de cette protection. Lorsqu’un utilisateur ou un processus change des propriétés spécifiques d’un élément de boîte aux lettres, une copie de l’élément d’origine est enregistrée dans le dossier Versions avant l’application de la modification. Le processus est répété pour les modifications ultérieures. Les éléments capturés dans le dossier Versions sont également indexés et renvoyés dans les recherches de découverte électronique sur place (In-Place eDiscovery). Une fois le blocage supprimé, les copies présentes dans le dossier Versions sont supprimées par l’Assistant Dossier géré.

### Propriétés qui déclenchent une opération de copie sur écriture

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d’élément</th>
<th>Propriétés qui déclenchent une opération de copie sur écriture</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messages (IPM.Note*)</p>
<p>Publications (IPM.Post*)</p></td>
<td><ul>
<li><p>Objet</p></li>
<li><p>Body</p></li>
<li><p>Pièces jointes</p></li>
<li><p>Expéditeurs/destinataires</p></li>
<li><p>Dates d’envoi et de réception</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Éléments autres que les messages et les publications</p></td>
<td><p>Toute modification apportée à une propriété visible, à l’exception des éléments suivants :</p>
<ul>
<li><p>Emplacement d’un élément (lorsqu’un élément fait l’objet de déplacements entre des dossiers)</p></li>
<li><p>Modification de l’état d’un élément (lu ou non lu)</p></li>
<li><p>Modifications apportées à la balise de rétention appliquée à un élément</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Éléments du dossier par défaut Brouillons</p></td>
<td><p>Aucune (les éléments du dossier Brouillons sont exemptés de copie sur écriture)</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La copie sur écriture est désactivée pour les éléments du calendrier dans la boîte aux lettres de l’organisateur lors de la réception des réponses des participants à la réunion et de la mise à jour des informations de suivi. Pour les éléments de calendrier et les éléments pour lesquels un rappel est défini, la copie sur écriture est désactivée pour les propriétés ReminderTime et ReminderSignalTime. Les changements apportés à ces propriétés ne sont pas capturés par la copie sur écriture. Les changements apportés aux flux RSS ne sont pas pris en compte par la copie sur écriture.</td>
</tr>
</tbody>
</table>


Bien que les dossiers DiscoveryHold, Purges et Versions ne soient pas visibles par l’utilisateur, tous les éléments du dossier Éléments récupérables sont indexés par Exchange Search et peuvent être découverts à l’aide de la découverte électronique sur place (In-Place eDiscovery). Lorsqu’un utilisateur de boîte aux lettres est supprimé d’une conservation inaltérable ou d’une conservation pour litige, les éléments des dossiers DiscoveryHold, Purges et Versions sont purgés par l’Assistant Dossier géré.

Retour au début

## Conservations et quotas de boîte aux lettres

Les éléments du dossier Éléments récupérables ne sont pas calculés en fonction du quota de boîte aux lettres de l’utilisateur. Dans Exchange, le dossier Éléments récupérables possède son propre quota. Pour Exchange, les valeurs par défaut pour les propriétés de boîte aux lettres *RecoverableItemsWarningQuota* et *RecoverableItemsQuota* sont définies sur 20 Go et 30 Go, respectivement. Pour modifier ces valeurs pour une base de données de boîtes aux lettres pour Exchange Server 2013, utilisez la cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)). Pour modifier ces valeurs pour des boîtes aux lettres spécifiques, utilisez la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

Lorsque le quota d’avertissement des éléments récupérables (spécifié par le paramètre *RecoverableItemsWarningQuota*) a été dépassé dans le dossier Éléments récupérables d’un utilisateur, un événement est consigné dans le journal des événements d’application du serveur de boîtes aux lettres. Lorsque le quota des éléments récupérables (spécifié par le paramètre *RecoverableItemsQuota*) du dossier a été dépassé, les utilisateurs ne sont plus en mesure de vider le dossier Éléments supprimés ou de supprimer définitivement des éléments de boîte aux lettres. Qui plus est, la copie sur écriture ne peut plus créer de copie des éléments modifiés. Par conséquent, vous devez impérativement surveiller les quotas du dossier Éléments récupérables des utilisateurs de boîte aux lettres qui sont placés en blocage sur place (In-Place Hold).

Dans Exchange Online, le quota du dossier Éléments récupérables (dans la boîte aux lettres principale de l’utilisateur) est automatiquement augmenté jusqu’à 100 Go quand vous placez une boîte aux lettres en conservation pour litige ou inaltérable. Lorsque le quota de stockage pour le dossier Éléments récupérables dans la boîte aux lettres principale d’une boîte aux lettres placée en conservation est proche de sa limite, vous pouvez effectuer les opérations suivantes :

  - **Activer la boîte aux lettres d’archivage et activer l’archivage à développement automatique**   Vous pouvez autoriser une capacité de stockage illimitée pour le dossier Éléments récupérables simplement en activant la boîte aux lettres d’archivage puis en activant la fonctionnalité d’archivage à développement automatique dans Exchange Online. Ainsi, le dossier Éléments récupérables dispose de 100 Go dans la boîte aux lettres principale et d’une quantité illimitée de capacité de stockage dans l’archive de l’utilisateur. Pour en savoir plus, consultez les rubriques relatives à l’[activation des boîtes aux lettres d’archivage dans le Centre de sécurité et conformité Office 365](https://go.microsoft.com/fwlink/p/?linkid=863320) et à l’[activation de l’archivage illimité dans Office 365](https://go.microsoft.com/fwlink/p/?linkid=844569).
    
    **Remarques** :
    
      - Après avoir activé l’archivage pour une boîte aux lettres qui va bientôt dépasser le quota de stockage du dossier Éléments récupérables, vous pouvez exécuter l’Assistant Dossier géré pour qu’il analyse la boîte aux lettres et déplace les éléments arrivés à expiration vers le dossier Éléments récupérables dans la boîte aux lettres d’archivage. Pour connaître la marche à suivre, consultez l’Étape 4 dans [Augmenter le quota des éléments récupérables pour les boîtes aux lettres placées en conservation](https://go.microsoft.com/fwlink/p/?linkid=786479).
    
      - Notez que d’autres éléments dans la boîte aux lettres de l’utilisateur peuvent être déplacés vers la nouvelle boîte aux lettres d’archivage. Envisagez d’indiquer à l’utilisateur que ceci peut se produire après l’activation de la boîte aux lettres d’archivage.

  - **Créer une stratégie de rétention personnalisée pour les boîtes aux lettres placées en conservation**   En plus d’activer la boîte aux lettres d’archivage et l’archivage à développement automatique pour les boîtes aux lettres placées en conservation pour litige ou inaltérable, vous pouvez créer une stratégie de rétention personnalisée pour les boîtes aux lettres placées en conservation. Cette stratégie peut être différente de la stratégie MRM par défaut appliquée aux boîtes aux lettres qui ne sont pas placées en conservation. Ainsi, vous pouvez appliquer des balises de rétention conçues spécifiquement pour les boîtes aux lettres placées en conservation, et créer une balise de rétention pour le dossier Éléments récupérables.

Pour plus d’informations, consultez l’article [Augmenter le quota des éléments récupérables pour les boîtes aux lettres en placées en conservation](https://go.microsoft.com/fwlink/p/?linkid=786479).

## Conservations et transfert du courrier électronique

Les utilisateurs peuvent utiliser Outlook et Outlook Web App pour configurer le transfert du courrier électronique pour leur boîte aux lettres. Le transfert du courrier électronique permet aux utilisateurs de configurer leur boîte aux lettres de manière à transférer le courrier électronique envoyé à celle-ci vers une autre boîte aux lettres se trouvant à l’intérieur ou à l’extérieur de leur organisation. Le transfert du courrier électronique peut être configuré de sorte que les messages envoyés vers la boîte aux lettres d’origine ne soient pas copiés dans cette boîte aux lettres, mais envoyés uniquement à l’adresse de transfert.

Si le transfert des e-mails a été configuré pour une boîte aux lettres et que les messages ne sont pas copiés vers la boîte aux lettres d’origine, que se passe-t-il si la boîte aux lettres est placée en conservation ? Tout dépend si la boîte aux lettres est hébergée dans une organisation Exchange 2013 ou Exchange Online.

  - **Exchange Online**   Les paramètres de mise en attente de la boîte aux lettres sont vérifiés au cours du processus de remise. Si le message répond aux critères de conservation pour la boîte aux lettres, une copie du message est enregistrée dans le dossier Éléments récupérables. Cela signifie que vous pouvez utiliser la découverte électronique inaltérable pour rechercher la boîte aux lettres d’origine, afin de trouver les messages qui ont été transmis à une autre boîte aux lettres.

  - **Exchange 2013**   Si les messages sont transférés à une autre boîte aux lettres et qu’ils ne sont pas copiés dans la boîte aux lettres d’origine, ils ne sont pas capturés et copiés dans le dossier Éléments récupérables. Cela signifie que les messages transférés ne figureront pas dans les résultats d’une recherche de découverte électronique inaltérable. Pour résoudre ce problème, les organisations Exchange 2013 peuvent envisager de supprimer la possibilité de configurer le transfert du courrier électronique pour les utilisateurs.

Retour au début

## Conservation du contenu Lync archivé

Exchange 2013, Microsoft Lync 2013 et Microsoft SharePoint 2013 offrent une fonctionnalité de découverte électronique (eDiscovery) et de conservation intégrée qui vous permet de conserver et de rechercher des éléments dans différents magasins de données. Exchange 2013 vous permet d’archiver du contenu Lync Server 2013 dans Exchange, ce qui ne nécessite pas de disposer d’une base de données SQL Server distincte pour stocker le contenu Lync archivé. La fonctionnalité de découverte électronique et de blocage intégrée dans SharePoint 2013 vous permet de conserver et de rechercher des données dans tous les magasins à partir d’une seule console.

Lorsque vous placez une boîte aux lettres Exchange 2013 en conservation inaltérable (In-Place Hold) ou conservation pour litige, le contenu Microsoft Lync 2013 (tel que les conversations de messagerie instantanée et les fichiers partagés lors d’une réunion en ligne) est archivé dans la boîte aux lettres. Si vous effectuez une recherche dans la boîte aux lettres via le eDiscovery Center dans Microsoft SharePoint 2013 ou la découverte électronique sur place (In-Place eDiscovery) dans Exchange 2013, tout le contenu Lync archivé qui correspond à la requête de recherche est aussi renvoyé dans les résultats de recherche. Vous pouvez également limiter la recherche au contenu Lync archivé dans la boîte aux lettres.

Pour activer l’archivage du contenu Lync dans la boîte aux lettres Exchange 2013, vous devez configurer l’intégration Lync 2013 avec Exchange 2013. Pour plus de détails, consultez les rubriques suivantes :

  - [Planification de l’archivage dans Lync Server 2013](https://technet.microsoft.com/fr-fr/library/jj205069\(v=ocs.15\))

  - [Déploiement de l’archivage dans Lync Server 2013](https://technet.microsoft.com/fr-fr/library/jj205147\(v=ocs.15\))

Retour au début

## Suppression d’une boîte aux lettres en attente

Lorsque vous supprimez une boîte aux lettres sur laquelle la conservation pour litige ou la conservation inaltérable a été activée, le résultat est différent selon que la boîte aux lettres est hébergée dans une organisation Exchange 2013 ou Exchange Online.

  - **Exchange 2013**   Si un administrateur supprime un compte d’utilisateur qui comporte une boîte aux lettres, la banque d’informations Exchange détectera que la boîte aux lettres n’est plus connectée à un compte d’utilisateur et la marquera pour suppression, même si elle est en attente. Pour conserver la boîte aux lettres, procédez comme suit :
    
    1.  Au lieu de supprimer le compte d’utilisateur, désactivez-le.
    
    2.  Modifiez les propriétés de la boîte aux lettres pour en restreindre l’utilisation et l’accès. Par exemple, la définition de quotas d’envoi/de réception sur 1 permet de bloquer les personnes pouvant envoyer des messages à la boîte aux lettres et de restreindre l’accès à cette dernière.
    
    3.  Conservez la boîte aux lettres jusqu’à ce que toutes les données aient pu être vidées ou jusqu’à ce que la conservation des données ne soit plus nécessaire.

  - **Exchange Online**   Si la conservation inaltérable ou la conservation pour litige est activée pour la boîte aux lettres d’un utilisateur et que le compte Office 365 correspondant est supprimé, la boîte aux lettres est convertie en *boîte aux lettres inactive*, qui est un type de boîte aux lettres supprimée (récupérable). Les boîtes aux lettres inactives sont utilisées pour conserver le contenu de la boîte aux lettres d’un utilisateur après son départ de votre organisation. Les éléments contenus dans une boîte aux lettres inactive sont conservés pendant la durée de la conservation placée sur la boîte aux lettres avant qu’elle ne soit définie comme inactive. Cela permet aux administrateurs, aux responsables de la mise en conformité ou aux gestionnaires des enregistrements d’utiliser la découverte électronique inaltérable pour accéder au contenu d’une boîte aux lettres inactive et y effectuer des recherches. Les boîtes aux lettres inactives ne peuvent pas recevoir de courrier électronique et n’apparaissent pas dans le carnet d’adresses partagé de votre organisation ou dans d’autres listes. Pour plus d’informations, consultez la rubrique [Boîtes aux lettres inactives dans Exchange Online](https://technet.microsoft.com/fr-fr/library/dn798632\(v=exchg.150\)).

Retour au début

## Migration de boîtes aux lettres en attente à partir d’Exchange 2013 vers Office 365

Si vous disposez d’un déploiement hybride Exchange, les conditions suivantes sont remplies lorsque vous déplacez (embarquement) une boîte aux lettres Exchange 2013 locale vers Exchange Online dans Office 365 :

  - Si la boîte aux lettres locale est en conservation pour litige ou en conservation inaltérable, les paramètres de mise en attente sont conservés après le déplacement de la boîte aux lettres vers Exchange Online.

  - Si la boîte aux lettres locale est en conservation pour litige ou en conservation inaltérable, le contenu du dossier Éléments récupérables est déplacé vers la boîte aux lettres Exchange Online.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les paramètres de mise en attente et le contenu du dossier Éléments récupérables sont également conservés lorsque vous déplacez (débarquement) une boîte aux lettres Exchange Online vers votre organisation Exchange 2013 locale.</td>
</tr>
</tbody>
</table>


Il existe d’autres façons de migrer des données de messagerie locale vers Office 365, par exemple en utilisant une migration intermédiaire Exchange migration ou une migration à basculement Exchange.

  - La migration intermédiaire peut être utilisée pour migrer des boîtes aux lettres depuis Exchange 2003 ou Exchange 2007 vers Office 365. Dans ces versions d’Exchange, le dossier Éléments récupérables (ainsi que ses fonctionnalités) n’existe pas. Par conséquent, lorsque vous migrez des boîtes aux lettres Exchange 2003 ou Exchange 2007 vers Office 365, il n’existe aucun contenu du dossier Éléments récupérables à déplacer.

  - Une migration à basculement peut être utilisée pour migrer des boîtes aux lettres depuis Exchange 2003, Exchange 2007 et Exchange 2010 vers Office 365. Comme indiqué plus haut, les boîtes aux lettres Exchange 2003 et Exchange 2007 n’ont pas de dossier Éléments récupérables à migrer. Comme le dossier Éléments récupérables a été introduit dans Exchange 2010, le contenu de ce dossier est migré vers Office 365 lorsque vous utilisez une migration à basculement pour migrer les boîtes aux lettres Exchange 2010.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour Exchange 2013 et Exchange 2010, un déploiement hybride Exchange est recommandé pour migrer les boîtes aux lettres locales vers Office 365.</td>
</tr>
</tbody>
</table>


Retour au début

