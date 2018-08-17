---
title: 'Archivage inaltérable dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Archivage inaltérable dans Exchange 2013
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50478910
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Archivage inaltérable dans Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

*L'archivage local* permet de reprendre le contrôle des données de messagerie de l’organisation en supprimant le besoin de recourir aux fichiers .pst et d'autoriser les utilisateurs à stocker les messages dans une *boîte aux lettres d’archivage* accessible dans MicrosoftOutlook 2010 et les versions ultérieures et dans Microsoft OfficeOutlook Web App.

Dans Microsoft Exchange Server 2013, vous pouvez utiliser l'archivage local pour fournir aux utilisateurs un autre emplacement de stockage pour stocker l’historique des données de messagerie. Une archive personnelle correspond à une boîte aux lettres supplémentaire (appelée boîte aux lettres d’archivage) activée pour un utilisateur de boîtes aux lettres. Les utilisateurs d’Outlook 2007 et des versions ultérieures ainsi que les utilisateurs d’Outlook Web App bénéficient d’un accès transparent à leur boîte aux lettres d’archivage. À l’aide de l’une de ces applications clientes, les utilisateurs peuvent afficher une boîte aux lettres d’archivage et déplacer ou copier des messages entre leur boîte aux lettres principale et l’archive. L'archivage local présente aux utilisateurs une vue cohérente des données de messagerie et élimine les tâches supplémentaires nécessaires à l’utilisateur pour gérer les fichiers .pst.

Vous pouvez configurer l’archive d’un utilisateur sur la même base de données de boîtes aux lettres que la boîte aux lettres principale de l’utilisateur, une autre base de données de boîtes aux lettres sur le même serveur de boîtes aux lettres ou encore une base de données de boîtes aux lettres sur un autre serveur de boîtes aux lettres dans le même site Active Directory. Dans les déploiements hybrides d’Exchange 2010 et des versions ultérieures, vous pouvez également configurer une archive en nuage des boîtes aux lettres situées dans vos serveurs de boîtes aux lettres locaux.

**Contenu de cette rubrique**

Données de messagerie et fichiers .pst

Accès client aux boîtes aux lettres d’archivage

Accès délégué

Déplacer des messages vers la boîte aux lettres d’archivage

Stratégies d’archivage et de rétention

Stratégie de gestion des enregistrements de messagerie par défaut

Quotas d’archivage

Archives locales et autres fonctionnalités Exchange

Gestion des boîtes aux lettres d’archivage

## Données de messagerie et fichiers .pst

Outlook utilise les fichiers .pst pour stocker les données en local sur les ordinateurs ou les partages réseau des utilisateurs. Contrairement aux fichiers .ost (utilisés par Outlook pour stocker une copie de la boîte aux lettres en mode Exchange mis en cache à des fins d’accès hors connexion), les fichiers .pst ne sont pas synchronisés avec la boîte aux lettres Exchange de l’utilisateur. Si un utilisateur déplace des messages vers un fichier .pst, ces messages sont alors supprimés de la boîte aux lettres.

L’utilisation des fichiers .pst pour gérer les données de messagerie peut générer les problèmes suivants :

  - **Fichiers non gérés**   En général, les fichiers .pst sont créés par les utilisateurs et résident sur leurs ordinateurs ou leurs partages réseau. Ils ne sont pas gérés par votre organisation. Les utilisateurs peuvent alors créer un certain nombre de fichiers .pst contenant des messages identiques ou différents et les enregistrer à différents emplacements, sans aucun contrôle de l’organisation.

  - **Augmentation des coûts de découverte**  Certaines actions en justice ou exigences de réglementation ou commerciales peuvent parfois aboutir à des demandes de découverte. La localisation de données de messagerie qui résident dans les fichiers .pst sur les ordinateurs des utilisateurs peut être une opération coûteuse. Étant donné que le suivi des fichiers .pst non gérés peut être difficile, il peut être impossible de trouver les données .pst dans de nombreux cas. Cette situation peut exposer votre organisation à des risques juridiques et financiers.

  - **Impossibilité d’appliquer des stratégies de rétention de messagerie**   Les stratégies de rétention de messagerie ne peuvent pas être appliquées aux messages localisés dans des fichiers .pst. Par conséquent, selon le cas, votre organisation risque de ne pas être conforme aux réglementations commerciales ou applicables.

  - **Risque de vol de données**   Les données de messagerie enregistrées dans les fichiers .pst sont vulnérables au vol. Par exemple, les fichiers .pst sont souvent enregistrés sur des périphériques portables tels que les ordinateurs portables, les disques durs amovibles et des supports mobiles tels que les lecteurs USB, les CD et DVD.

  - **Vue fragmentée des données de messagerie**   Les utilisateurs qui enregistrent des informations dans des fichiers .pst n’ont pas une vue uniforme de leurs données. Les messages enregistrés dans des fichiers .pst sont généralement et uniquement disponibles sur l’ordinateur où réside le fichier .pst. Par conséquent, si les utilisateurs accèdent à leurs boîtes aux lettres en utilisant Outlook Web App ou Outlook sur un autre ordinateur, les messages enregistrés dans les fichiers .pst ne sont pas accessibles.

## Accès client aux boîtes aux lettres d’archivage

Le tableau suivant présente la liste des applications clientes que l’on peut utiliser pour accéder aux boîtes aux lettres d’archivage.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Accès aux boîtes aux lettres d’archivage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013, Outlook 2010, Outlook 2007 et Outlook Web App</p></td>
<td><p>Oui. Les utilisateurs de Outlook 2013, Outlook 2010, Outlook 2007 et Outlook Web App peuvent copier et déplacer des éléments de leur boîte aux lettres principale vers leur boîte aux lettres d’archivage. Ils peuvent également utiliser des stratégies de rétention pour déplacer des éléments vers l’archive.</p>

> [!NOTE]    
> Les utilisateurs de Outlook 2007, de Outlook 2010 et des versions ultérieures peuvent également copier ou déplacer des éléments depuis des fichiers .pst vers leur boîte aux lettres d’archivage. Les utilisateurs de Outlook 2007 doivent installer la mise à jour cumulative de Microsoft Office 2007 de février 2011. Certaines différences de support d'archive existent entre la version 2007 de Outlook et les versions 2010 et ultérieures de Outlook. Pour plus d'informations, consultez l'article du Blog de l’équipe Exchange, <a href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">Oui Virginie, les archives Exchange 2010 sont prises en charge dans Outlook 2007</a>.

</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> L’archivage local constituent une fonctionnalité étendue et requiert une licence d’accès client (CAL) Exchange Enterprise. Pour plus d’informations sur les licences Exchange, voir la rubrique <a href="https://go.microsoft.com/fwlink/?linkid=237292">Exchange Server Licensing</a>. Pour plus d’informations sur les versions d’Outlook requises pour accéder à une boîte aux lettres d’archivage, consultez la rubrique <a href="https://go.microsoft.com/fwlink/?linkid=237276">Conditions requises pour les licences relatives aux stratégies d’archivage et de rétention personnelles</a>.


Outlook ne crée pas de copie locale de la boîte aux lettres d’archivage sur l’ordinateur d’un utilisateur, même si la configuration permet l’utilisation du Mode Exchange mis en cache. Les utilisateurs peuvent accéder à une boîte aux lettres d’archivage en mode en ligne uniquement.

## Accès délégué

La fonction *Accès délégué* permet d’accorder un accès à la boîte aux lettres d’un autre utilisateur à un ensemble d’utilisateurs. Cette section décrit les différentes approches que vous pouvez utiliser pour accorder ce type d’accès, notamment :

  - Accorder à un ou plusieurs utilisateurs un accès à la boite aux lettres d’un utilisateur qui ne fait plus partie de l’organisation. Dans ce cas, les utilisateurs à qui l’on peut accorder un accès délégué incluent le responsable ou le superviseur de l’utilisateur qui a quitté l’organisation ou bien un autre utilisateur qui prendra en charge les responsabilités de cet employé.

  - Accorder un accès à une boîte aux lettres partagée à un ou plusieurs utilisateurs.

  - Accorder aux assistant(e)s de direction un accès aux boîtes aux lettres des directeurs qu’ils(elles) assistent.

Lorsque vous octroyez à un délégué une autorisation d’accès total à une boîte aux lettres dans Exchange 2013, ce délégué peut également accéder à l’archive de l’utilisateur. Les délégués doivent utiliser Outlook pour accéder à la boîte aux lettres et doivent se connecter à un serveur d’accès au client Exchange 2010 ou ultérieur à des fins de découverte automatique. Exchange comprend un service de découverte automatique qui permet de configurer automatiquement les paramètres des clients Outlook. Lorsque les délégués utilisent Outlook pour accéder à une boîte aux lettres Exchange 2013, la boîte aux lettres principale et l’archive auxquelles ils ont accès sont affichées dans Outlook.

## Déplacer des messages vers la boîte aux lettres d’archivage

Différentes méthodes permettent de déplacer des messages vers des boîtes aux lettres d’archivage :

  - **Déplacer ou copier des messages manuellement**   Les utilisateurs de boîtes aux lettres peuvent déplacer ou copier manuellement des messages de leur boîte aux lettres principale ou fichier .pst vers leur boîte aux lettres d’archivage. La boîte aux lettres d’archivage apparaît en tant que boîte aux lettres différente ou fichier .pst dans Outlook et Outlook Web App.

  - **Déplacer ou copier des messages à l’aide des règles de la boîte de réception**   Les utilisateurs de boîtes aux lettres peuvent créer des règles de boîte de réception dans Outlook ou Outlook Web App afin de déplacer automatiquement des messages vers un dossier de leur boîte aux lettres d’archivage. Pour plus d’informations, consultez l’article [En savoir plus sur les règles de la boîte de réception](http://help.outlook.com/fr-fr/140/bb899620.aspx).

  - **Déplacer des messages à l’aide des stratégies de rétention**   Vous pouvez utiliser les stratégies de rétention pour déplacer automatiquement des messages vers l’archive. Les utilisateurs peuvent également appliquer une balise personnelle pour déplacer des messages vers l’archive. Pour en savoir plus sur les stratégies d’archivage et de rétention, voir la section Stratégies d’archivage et de rétention plus bas dans cette rubrique.
    
    > [!NOTE]  
    > Les balises personnelles ne sont accessibles que sous Outlook Web App et sous Outlook 2010 et les versions ultérieures.


  - **Importer des messages à partir de fichiers .pst**   Dans Exchange 2013, vous pouvez effectuer une demande d’importation de boîte aux lettres pour importer des messages d’un fichier .pst vers la boîte aux lettres d’archivage ou la boîte aux lettres principale d’un utilisateur. Pour plus d’informations, consultez la rubrique [Demandes d’exportation et d’importation de boîtes aux lettres](mailbox-import-and-export-requests-exchange-2013-help.md). Vous pouvez aussi utiliser l'outil PST Capture pour rechercher des fichiers .pst sur des ordinateurs de votre organisation et importer des données de fichiers .pst dans des archives d'utilisateurs.

## Stratégies d’archivage et de rétention

Dans Exchange 2013, vous pouvez appliquer des stratégies d’archivage à une boîte aux lettres qui déplaceront automatiquement des messages de la boîte aux lettres principale d’un utilisateur vers la boîte aux lettres d’archivage après une période déterminée. Les stratégies d’archivage sont des stratégies de rétention mises en œuvre par la création de balises de rétention qui spécifient l’action **Déplacer vers l’archive**.

Les messages sont déplacés dans un dossier de la boîte aux lettres d’archivage qui porte le même nom que le dossier source dans la boîte aux lettres principale. Si un dossier portant un nom identique n’existe pas dans la boîte aux lettres d’archivage, il est créé lorsque l’Assistant Dossier géré déplace un message. La création d’une hiérarchie de dossiers similaire dans la boîte aux lettres d’archivage permet à l’utilisateur de trouver les messages plus facilement.

Pour en savoir plus sur les stratégies de rétention, les balises de rétention et l’action de rétention **Déplacer vers l’archive**, voir la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

## Stratégie de gestion des enregistrements de messagerie par défaut

Le programme d’installation d’Exchange 2013 crée une stratégie d’archivage et de rétention par défaut intitulée **Stratégie MRM par défaut**. Cette stratégie comprend des balises de rétention qui spécifient l’action **Déplacer vers l’archive**, comme indiqué dans le tableau suivant.

> [!NOTE]
> Dans Exchange 2010, la stratégie d’archivage et de rétention par défaut créée par le programme d'installation d'Exchange s'appelle la <strong>Stratégie d’archivage et de rétention par défaut</strong> (Default Archive and Retention Policy).



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de balise de rétention</th>
<th>Type de balise</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Déplacement vers l’archive après 2 ans - Par défaut</strong></p></td>
<td><p>Par défaut (balise de stratégie par défaut)</p></td>
<td><p>Les messages sont automatiquement déplacés dans la boîte aux lettres d’archivage après 2 ans. S’applique aux éléments de toute la boîte aux lettres ne disposant pas de balise de rétention appliquée explicitement ou héritée du dossier.</p></td>
</tr>
<tr class="even">
<td><p><strong>Déplacement vers l’archive après 1 ans - Personnel</strong></p></td>
<td><p>Personnelle</p></td>
<td><p>Les messages sont automatiquement déplacés dans la boîte aux lettres d’archivage après 1 an.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Déplacement vers l’archive après 5 ans - Personnel</strong></p></td>
<td><p>Personnelle</p></td>
<td><p>Les messages sont automatiquement placés dans la boîte aux lettres d’archivage après cinq ans.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ne jamais déplacer vers l’archive - Personnel</strong></p></td>
<td><p>Personnelle</p></td>
<td><p>Les messages ne sont jamais placés dans la boîte aux lettres d’archivage.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Les éléments récupérables de 14 jours sont déplacés vers l'archive</strong></p></td>
<td><p>Dossier Éléments récupérables</p></td>
<td><p>Les messages sont déplacés du dossier Éléments récupérables de la boîte aux lettres principale de l’utilisateur vers le dossier Éléments récupérables de la boîte aux lettres d’archivage. Les utilisateurs qui tentent de récupérer des éléments supprimés dans l’archive doivent utiliser l’option Récupérer les éléments supprimés dans la boîte aux lettres d’archivage.</p></td>
</tr>
</tbody>
</table>


Si vous activez une archive locale pour un utilisateur de boîte aux lettres et que cette dernière n’est pas associée à une stratégie de rétention, la stratégie d’archivage et de rétention par défaut est automatiquement attribuée. Une fois que l’Assistant Dossier géré traite la boîte aux lettres, l’utilisateur peut accéder aux balises et baliser les dossiers ou les messages à déplacer dans la boîte aux lettres d’archivage. Par défaut, les messages électroniques de toute la boîte aux lettres sont déplacés après deux ans.

Avant de configurer les boîtes aux lettres d’archivage pour vos utilisateurs, nous vous recommandons de les informer des stratégies d’archivage qui seront appliquées à leur boîte aux lettres et de les former ou de les documenter selon leurs besoins. Ces informations devront porter sur les éléments suivants :

  - Fonctionnalités disponibles dans l’archive, l’archivage par défaut et les stratégies de rétention.

  - Informations relatives à la durée au terme de laquelle les messages peuvent être automatiquement déplacés dans l’archive.

  - Informations concernant la hiérarchie du dossier créée dans la boîte aux lettres d’archivage.

  - La méthode permettant d’appliquer des balises personnelles (affichées dans le menu Stratégie d'archivage de Outlook et de Outlook Web App).

> [!NOTE]
> Si vous appliquez une stratégie de rétention aux utilisateurs disposant d’une boîte aux lettres d’archivage, elle remplace la stratégie de gestion des enregistrements de messagerie par défaut. Vous pouvez créer une ou plusieurs balises de rétention avec l’action <strong>Déplacer vers l’archive</strong>, puis lier les balises à la stratégie de rétention. Vous pouvez également ajouter les balises par défaut <strong>Déplacer vers l’archive</strong> (Move to Archive), créées par le programme d’installation et liées à la stratégie de gestion des enregistrements de messagerie par défaut, à n’importe quelle stratégie de rétention créée.


Pour obtenir des informations sur la conformité et l’archivage dans Outlook 2010 et dans les versions ultérieures, voir la rubrique [Planifier la conformité et l’archivage dans Outlook 2010](https://go.microsoft.com/fwlink/?linkid=210902).

## Quotas d’archivage

Les boîtes aux lettres d’archivage sont conçues pour permettre aux utilisateurs d’enregistrer l’historique des données de messagerie en dehors de leur boîte aux lettres principale. Les utilisateurs se servent souvent des fichiers .pst en raison de quotas de stockage de boîte aux lettres faibles et des restrictions imposées lorsque ces quotas sont dépassés. Par exemple, les utilisateurs peuvent ne pas être autorisés à envoyer des messages lorsque la taille de leur boîte aux lettres dépasse le *Quota d’interdiction d’envoi*. De même, les utilisateurs peuvent ne pas être autorisés à envoyer ni à recevoir des messages lorsque la taille de leur boîte aux lettres dépasse le *quota Interdire l’envoi et la réception*.

Pour ne pas avoir à recourir aux fichiers .pst, vous pouvez fournir une boîte aux lettres d’archivage avec des limites de stockage qui répondent aux exigences de l’utilisateur. Toutefois, en même temps, vous souhaiterez probablement continuer à contrôler les quotas de stockage et la croissance des boîtes aux lettres d’archivage pour surveiller les coûts et l’expansion.

Pour ce faire, vous pouvez configurer les boîtes aux lettres d’archivage avec un *quota d’avertissement d’archivage* et un *quota d’archivage*. Lorsqu’une boîte aux lettres d’archivage dépasse le quota d’avertissement d’archivage spécifié, un événement d’avertissement est consigné dans le Journal des événements d’application. Lorsqu’une boîte aux lettres d’archivage dépasse le quota d’archivage spécifié, les messages ne sont plus placés dans l’archive, un événement d’avertissement est consigné dans le Journal des événements d’application et un message de quota est envoyé à l’utilisateur de la boîte aux lettres. Par défaut, dans Exchange 2013, le quota d’avertissement d’archivage est défini sur 45 gigaoctets (Go) et le quota d’archivage sur 50 Go.

Le tableau suivant affiche la liste des évènements consignés et des messages d’avertissement envoyés lorsque le quota d’avertissement d’archivage et le quota d’archivage sont atteints.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>ID d’évènement</th>
<th>Type</th>
<th>Source</th>
<th>Catégorie</th>
<th>Message</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Quota d’avertissement d’archivage</p></td>
<td><p>10022</p></td>
<td><p>Avertissement</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>La boîte aux lettres d’archivage « &lt;Nom complet&gt; : &lt;GUID&gt; : &lt;Base de données de boîte aux lettres&gt; : &lt;Nom de domaine complet du serveur&gt; » a dépassé le quota d’avertissement d’archivage « &lt;Quota d’avertissement d’archivage&gt; ». La taille de la boîte aux lettres d’archivage est de « &lt;Taille&gt; » octets.</p></td>
</tr>
<tr class="even">
<td><p>Quota d’archivage</p></td>
<td><p>8537</p></td>
<td><p>Avertissement</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Général</p></td>
<td><p>La boîte aux lettres d’archivage pour le &lt;DN hérité&gt; a dépassé la taille maximale de la boîte aux lettres d’archivage. Vous ne pouvez pas copier ou ni déplacer des éléments vers la boîte aux lettres d’archivage. Toutes les actions de rétention des messages qui entraînent le déplacement d’éléments vers la boîte aux lettres d’archivage vont échouer et la boîte aux lettres principale risque de contenir des éléments dont les balises de rétention ont expiré jusqu’à ce que la boîte aux lettres d’archivage repasse en-dessous de la taille maximale. Le propriétaire de la boîte aux lettres devrait être informé de la situation de la boîte aux lettres d’archivage.</p></td>
</tr>
</tbody>
</table>


## Archives locales et autres fonctionnalités Exchange

Cette section décrit la relation entre les archives locales et d’autres fonctionnalités Exchange :

  - **Recherche Exchange   **Avec les boîtes aux lettres d’archivage, il est important de pouvoir rapidement rechercher les messages. Pour la recherche d'Exchange, il n'existe aucune différence entre la boîte aux lettres d’archivage et la boîte aux lettres principale. Le contenu des deux boîtes aux lettres est indexé. Dans la mesure où la boîte aux lettres d’archivage n’est pas mise en cache sur l’ordinateur d’un utilisateur (même en utilisant Outlook en mode Exchange mis en cache), les résultats de recherche pour l’archive sont toujours fournis par la recherche d'Exchange. Lorsqu’une recherche est lancée sur l’ensemble de la boîte aux lettres dans les versions 2010 et ultérieures de Outlook et dans Outlook Web App, les résultats de recherche incluent la boîte aux lettres principale et la boîte aux lettres d’archivage de l’utilisateur.

  - **Découverte électronique sur place**   Quand un gestionnaire de découverte effectue une recherche de découverte électronique, la recherche inclut les boîtes aux lettres d'archivage des utilisateurs. Aucune option ne permet d’exclure les boîtes aux lettres d’archivage lors de la création d’une recherche de découverte dans le Centre d'administration Exchange (CAE). Lorsque vous utilisez l’environnement de ligne de commande Exchange Management Shell pour créer une recherche de découverte, vous pouvez exclure l’archive en utilisant le commutateur *DoNotIncludeArchive*. Pour plus d’informations, consultez la rubrique [New-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd298064\(v=exchg.150\)). Pour en savoir plus, voir [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md).
    
    > [!IMPORTANT]
    > Vous ne pouvez pas utiliser la découverte électronique sur place pour effectuer une recherche sur une boîte aux lettres déconnectée.


  - **Blocage sur place et suspension pour litige**   Lorsque vous mettez une boîte aux lettres en blocage sur place ou en suspension pour litige, la suspension s’applique à la boîte aux lettres principale et à la boîte aux lettres d’archivage. Pour en savoir plus sur le blocage sur place et la suspension pour litige, voir [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Dossier Éléments récupérables   **La boîte aux lettres d’archivage comprend son propre dossier d’Éléments récupérables et est soumise aux mêmes quotas de dossier d’Éléments récupérables que la boîte aux lettres principale. Pour plus d’informations sur les éléments récupérables, consultez la rubrique [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

  - **Archivage du contenu Lync dans Exchange**   Vous pouvez archiver des conversations de messagerie instantanée et des documents de réunions en ligne partagés dans la boîte aux lettres principale de l’utilisateur. La boîte aux lettres doit résider sur un serveur de boîtes aux lettres Exchange 2013 et Microsoft Lync 2013 doit être déployé dans votre organisation. Pour plus d’informations, consultez la rubrique [Intégration à SharePoint et Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Gestion des boîtes aux lettres d’archivage

Dans Exchange 2013, la création et la gestion des boîtes aux lettres d’archivage sont intégrées aux tâches courantes de gestion des boîtes aux lettres, y compris :

  - **Création d’une boîte aux lettres d’archivage**   Lorsque vous créez une boîte aux lettres, vous pouvez créer une boîte aux lettres d’archivage ou bien l’activer cette dernière pour une boîte aux lettres existante. Pour plus d’informations, consultez la rubrique [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Déplacement d’une boîte aux lettres d’archivage**   Vous pouvez transférer la boîte aux lettres d’archivage d’un utilisateur vers une autre base de données de boîtes aux lettres sur le même serveur de boîtes aux lettres ou bien sur un autre serveur, indépendamment de la boîte aux lettres principale. Pour déplacer la boîte aux lettres d’archivage d’un utilisateur, vous devez créer une demande de déplacement de boîte aux lettres. Pour plus d’informations, consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).
    
    > [!IMPORTANT]
    > La recherche de la boîte aux lettres et des archives d’un utilisateur dans différentes versions d’Exchange Server n’est pas prise en charge.


  - **Désactivation d’une boîte aux lettres d’archivage**   Il peut être utile de désactiver la boîte aux lettres d’archivage d’un utilisateur pour résoudre des problèmes ou si vous transférez la boîte aux lettres principale vers une version d’Exchange qui ne prend pas en charge l’archivage local. La procédure de désactivation d’une archive est similaire celle utilisée pour une boîte aux lettres principale. Pour plus d’informations, consultez la rubrique [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md). Dans le cas de déploiements locaux, un boîte aux lettres d’archivage désactivée est conservée dans la base de données de boîtes aux lettres jusqu’à ce que la période de rétention de la boîte aux lettres supprimée ait expirée. Durant cette période, vous pouvez reconnecter l’archive à la boite aux lettres d’un utilisateur. À l’issue de la période de rétention de la boîte aux lettres supprimée, la boîte aux lettres d’archivage déconnectée est définitivement supprimée de la base de données de boîtes aux lettres.

  - **Récupération de statistiques de boîtes aux lettres et de dossiers**   Vous pouvez récupérer les statistiques de boîtes aux lettres et les statistiques des dossiers de boîtes aux lettres pour la boîte aux lettres d’archivage d’un utilisateur à l’aide du commutateur *Archive* avec les cmdlets [Get-MailboxStatistics](https://technet.microsoft.com/fr-fr/library/bb124612\(v=exchg.150\)) et [Get-MailboxFolderStatistics](https://technet.microsoft.com/fr-fr/library/aa996762\(v=exchg.150\)).

  - **Tester la connectivité des archives**   Dans Exchange 2013, vous pouvez utiliser la cmdlet [Test-ArchiveConnectivity](https://technet.microsoft.com/fr-fr/library/hh529914\(v=exchg.150\)) pour tester la connectivité vers une archive en nuage ou locale d'un utilisateur spécifique.

