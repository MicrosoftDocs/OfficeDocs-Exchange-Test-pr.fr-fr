---
title: 'Recipients: Exchange 2013 Help'
TOCTitle: Recipients
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 50478014
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recipients

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les personnes et ressources qui échangent des messages constituent le noyau de tout système de collaboration et de messagerie. Dans une organisation Exchange, ces personnes et ressources sont appelées *destinataires*. Un destinataire est un objet à extension messagerie dans Active Directory auquel Microsoft Exchange peut remettre ou router des messages.

## Types de destinataire Exchange

Exchange inclut plusieurs types de destinataire explicites. Chaque type de destinataire est identifié dans le centre d’administration Exchange (CAE) et a une valeur unique dans la propriété *RecipientTypeDetails* dans l’environnement de ligne de commande Exchange Management Shell. L'utilisation de types de destinataire explicites offre les avantages suivants :

  - D'un coup d'œil, vous pouvez différencier les différents types de destinataire.

  - Vous pouvez rechercher et trier selon chaque type de destinataire.

  - La réalisation d’opérations de gestion globale pour des types de destinataire sélectionnés est facilitée.

  - Il est plus facile d’afficher les propriétés des destinataires, car le CAE utilise les types de destinataire pour afficher différentes pages de propriétés. Par exemple, la capacité des ressources s’affiche pour une boîte aux lettres de salle, mais pas pour une boîte aux lettres d’utilisateur.

Le tableau suivant répertorie les types de destinataire disponibles. Tous ces types de destinataires sont décrits en détail ci-après dans cette rubrique.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de destinataire</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Groupe de distribution dynamique</p></td>
<td><p>Groupe de distribution qui utilise des filtres des destinataires et des conditions pour déterminer son appartenance lors de l'envoi des messages.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de ressource</p></td>
<td><p>Boîte aux lettres de ressources affectée à une ressource qui n’est pas propre à un emplacement, telle qu’un projecteur, un ordinateur portable, un microphone ou un véhicule de société. Les boîtes aux lettres d’équipement peuvent être incluses comme ressources dans les demandes de réunion et constituent pour vos utilisateurs une manière simple et efficace d’utiliser des ressources.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres liée</p></td>
<td><p>Boîte aux lettres affectée à un utilisateur individuel dans une forêt approuvée distincte.</p></td>
</tr>
<tr class="even">
<td><p>Contact de messagerie</p></td>
<td><p>Contact Active Directory à extension messagerie contenant des informations sur les personnes ou les entités extérieures à l'organisation Exchange. Chaque contact de messagerie dispose d’une adresse de messagerie externe. Tous les messages envoyés au contact de messagerie sont routés à cette adresse de messagerie externe.</p></td>
</tr>
<tr class="odd">
<td><p>Contact de forêt de messagerie</p></td>
<td><p>Contact de messagerie qui représente un objet destinataire d'une autre forêt. Les contacts de forêt de messagerie sont généralement créés par la fonctionnalité de synchronisation Microsoft Identity Integration Server (MIIS).</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les contacts de forêt de messagerie sont des objets destinataires mis à jour uniquement à l'aide de MIIS ou d'une synchronisation personnalisée similaire. Vous ne pouvez pas supprimer ni modifier un contact de forêt de messagerie à l’aide du CAE ou de l’environnement de ligne de commande Exchange Management Shell.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Utilisateur de messagerie</p></td>
<td><p>Utilisateur Active Directory à extension messagerie qui représente un utilisateur extérieur à l'organisation Exchange. Chaque utilisateur de messagerie dispose d’une adresse de messagerie externe. Tous les messages envoyés à l’utilisateur de messagerie sont routés à cette adresse de messagerie externe.</p>
<p>Un utilisateur de messagerie est semblable à un contact de messagerie, sauf qu'un utilisateur de messagerie dispose d'informations d'identification d'ouverture de session Active Directory et peut accéder aux ressources.</p></td>
</tr>
<tr class="odd">
<td><p>Groupe non universel à extension messagerie</p></td>
<td><p>Objet de groupe global ou local à extension messagerie Active Directory. Les groupes non universels à extension messagerie ont été abandonnés dans Exchange Server 2007 et peuvent uniquement exister s'ils ont été migrés d'Exchange 2003 ou de versions antérieures d'Exchange. Vous ne pouvez pas utiliser Exchange Server 2013 pour créer des groupes de distribution non universels.</p></td>
</tr>
<tr class="even">
<td><p>Dossier public à extension messagerie</p></td>
<td><p>Dossier public Exchange configuré pour recevoir des messages.</p></td>
</tr>
<tr class="odd">
<td><p>Groupes de distribution</p></td>
<td><p>Un groupe de distribution est un groupe de distribution Active Directory à extension messagerie qui peut être uniquement utilisé pour distribuer des messages à un groupe de destinataires.</p></td>
</tr>
<tr class="even">
<td><p>Groupe de sécurité à extension messagerie</p></td>
<td><p>Un groupe de sécurité à extension messagerie est un objet de groupe universel de sécurité Active Directory qui peut être utilisé pour affecter des autorisations d’accès à des ressources dans Active Directory et qui peut également être utilisé pour distribuer des messages.</p></td>
</tr>
<tr class="odd">
<td><p>Destinataire Microsoft Exchange</p></td>
<td><p>Objet de destinataire spécifique qui fournit un expéditeur unifié et connu distinguant les messages générés par le système des autres messages. Il remplace l'expéditeur « Administrateur système » utilisé pour les messages générés par le système dans les versions antérieures d'Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de salle</p></td>
<td><p>Boîte aux lettres de ressources affectée à un lieu de réunion tel qu'une salle de conférence, un auditorium ou une salle de formation. Les boîtes aux lettres de salle peuvent être incluses comme ressources dans les demandes de réunion et offrent un moyen simple et efficace d'organiser des réunions pour vos utilisateurs.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres partagée</p></td>
<td><p>Boîte aux lettres non associée principalement à un utilisateur unique et généralement configurée pour permettre l’accès à plusieurs utilisateurs.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de site</p></td>
<td><p>Boîte aux lettres constituée d’une boîte aux lettres Exchange pour stocker les messages électroniques et d’un site SharePoint pour stocker des documents. Les utilisateurs peuvent accéder aux messages électroniques et aux documents à l’aide d’une même interface client. Pour plus d’informations, voir <a href="site-mailboxes-exchange-2013-help.md">Boîtes aux lettres de site</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres d'utilisateur</p></td>
<td><p>Boîte aux lettres affectée à un utilisateur individuel dans votre organisation Exchange. Elle contient généralement des messages, des éléments de calendrier, des contacts, des tâches, des documents et d'autres données professionnelles importantes.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres Office 365</p></td>
<td><p>Dans les déploiements hybrides, une boîte aux lettres Office 365 est composée d’un utilisateur de messagerie existant dans Active Directory version locale et une boîte aux lettres en nuage associée existant dans Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Utilisateur lié</p></td>
<td><p>Un utilisateur lié est un utilisateur dont la boîte aux lettres réside dans une autre forêt que la sienne.</p></td>
</tr>
</tbody>
</table>


## Boîtes aux lettres

Les boîtes aux lettres constituent le type de destinataire le plus couramment utilisé par les professionnels de l'information dans une organisation Exchange. Chaque boîte aux lettres est associée à un compte d'utilisateur Active Directory. L'utilisateur peut se servir de la boîte aux lettres pour envoyer et recevoir des messages, ainsi que pour stocker des messages, des rendez-vous, des tâches, des notes et des documents. Les boîtes aux lettres sont les principaux outils de collaboration et de messagerie des utilisateurs de votre organisation Exchange.

## Composants de boîte aux lettres

Chaque boîte aux lettres est constituée d'un utilisateur Active Directory et des données de boîte aux lettres stockées dans la base de données de boîtes aux lettres Exchange (comme indiqué dans la figure suivante). Toutes les données de configuration de la boîte aux lettres sont stockées dans les attributs Exchange de l'objet utilisateur Active Directory. La base de données de boîtes aux lettres contient les données de la boîte aux lettres associée au compte d'utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous créez une boîte aux lettres pour un nouvel utilisateur ou un utilisateur existant, les attributs Exchange requis pour une boîte aux lettres sont ajoutés à l'objet utilisateur dans Active Directory. Les données de boîte aux lettres associées ne sont créées que lorsque la boîte aux lettres reçoit un message ou que l’utilisateur s’y connecte.</td>
</tr>
</tbody>
</table>


**Composants de boîte aux lettres**

![Composants d’une boîte aux lettres](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Composants d’une boîte aux lettres")

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous supprimez une boîte aux lettres, les données de boîte aux lettres stockées dans la base de données de boîtes aux lettres Exchange sont marquées pour suppression et le compte d'utilisateur associé est également supprimé d'Active Directory. Pour conserver le compte d'utilisateur et supprimer uniquement les données de boîte aux lettres, vous devez désactiver la boîte aux lettres.</td>
</tr>
</tbody>
</table>


## Types de boîte aux lettres

Exchange prend en charge les types de boîte aux lettres suivants :

  - **Boîte aux lettres d'utilisateur   **Les boîtes aux lettres d'utilisateur sont assignées à des utilisateurs individuels dans votre organisation Exchange. Les boîtes aux lettres d'utilisateur fournissent à vos utilisateurs une plate-forme de collaboration riche. Les utilisateurs peuvent échanger des messages, gérer leurs contacts, programmer des réunions et gérer une liste de tâches. Ils peuvent également recevoir des messages vocaux dans leurs boîtes aux lettres. Les boîtes aux lettres d'utilisateur constituent le type de boîte aux lettres le plus répandu et le plus couramment affecté aux utilisateurs de votre organisation.

  - **Boîtes aux lettres liées**   Les boîtes aux lettres liées sont des boîtes aux lettres d'utilisateur auxquelles accèdent les utilisateurs dans une forêt approuvée distincte. Les boîtes aux lettres liées peuvent être utiles pour les organisations qui déploient Exchange dans une forêt ressource. Le scénario de forêt ressource permet à une organisation de centraliser Exchange dans une forêt unique, tout en permettant d'accéder à l'organisation Exchange avec des comptes d'utilisateur dans une ou plusieurs forêts approuvées.
    
    Comme indiqué précédemment, un compte d'utilisateur doit être associé à chaque boîte aux lettres. Toutefois, le compte d'utilisateur qui accède à la boîte aux lettres liée n'existe pas dans la forêt où Exchange est déployé. Par conséquent, un compte d'utilisateur désactivé existant dans la même forêt qu'Exchange est associé à chaque boîte aux lettres liée. La figure suivante décrit la relation entre le compte d'utilisateur lié servant à accéder à la boîte aux lettres liée et le compte d'utilisateur désactivé dans la forêt ressource Exchange associé à la boîte aux lettres liée.
    
    **Boîte aux lettres liée**
    
    ![Organisation Exchange complexe avec forêt de ressources](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organisation Exchange complexe avec forêt de ressources")  

  - **Boîtes aux lettres Office 365   **Lorsque vous créez une boîte aux lettres Office 365 dans Exchange Online dans un déploiement hybride, l’utilisateur de messagerie est créé dans Active Directory version locale. Si elle est configurée, la synchronisation d’annuaires synchronise automatiquement ce nouvel objet utilisateur avec Office 365, où il est converti en boîte aux lettres en nuage dans Exchange Online. Vous pouvez créer des boîtes aux lettres Office 365 comme boîtes aux lettres d’utilisateur ordinaire, comme boîtes aux lettres de ressources pour des salles de réunion et de l’équipement, et comme boîtes aux lettres partagées.

  - **Boîtes aux lettres partagées**   Les boîtes aux lettres partagées ne sont pas principalement associées à des utilisateurs individuels et sont généralement configurées pour permettre l’accès à plusieurs utilisateurs.
    
    Bien qu’il soit possible d’affecter des autorisations d’accès par ouverture de session à des utilisateurs supplémentaires sur tout type de boîte aux lettres, les boîtes aux lettres partagées sont conçues pour cette fonctionnalité. L’utilisateur Active Directory associé à une boîte aux lettres partagée doit être un compte désactivé. Après la création d’une boîte aux lettres partagée, vous devez affecter des autorisations à tous les utilisateurs nécessitant l’accès à la boîte aux lettres partagée.

  - **Boîtes aux lettres de ressources**   Les boîtes aux lettres de ressources sont des boîtes aux lettres spécialement conçues pour planifier des ressources. Comme tous les types de boîte aux lettres, une boîte aux lettres de ressources est associée à un compte d'utilisateur Active Directory qui doit être désactivé. Les types de boîtes aux lettres de ressources sont les suivants :
    
      - **Boîtes aux lettres de salle**   Ces boîtes aux lettres sont associées à des lieux de réunion, tels que des salles de conférence, des auditoriums et des salles de formation.
    
      - **Boîtes aux lettres de ressource**   Ces boîtes aux lettres sont affectées à des ressources qui ne sont pas propres à un emplacement, telles que des ordinateurs portables, des projecteurs, des microphones ou encore des véhicules de société.
    
    Les deux types de boîte aux lettres de ressources peuvent être inclus comme ressources dans les demandes de réunion et offrent à vos utilisateurs un moyen simple et efficace d’utiliser des ressources. Vous pouvez configurer des boîtes aux lettres de ressources pour qu'elles traitent automatiquement les demandes de réunion entrantes selon les stratégies de réservation de ressources définies par les propriétaires des ressources. Par exemple, vous pouvez configurer une salle de conférence pour qu'elle accepte automatiquement les demandes de réunion entrantes à l'exception des réunions récurrentes, qui peuvent faire l'objet d'une approbation par le propriétaire de la ressource.

## Boîtes aux lettres système

Les boîtes aux lettres système sont créées par Exchange dans le domaine racine de la forêt Active Directory lors de l'installation. Les utilisateurs ou les administrateurs ne peuvent pas se connecter à ces boîtes aux lettres. Les boîtes aux lettres système sont créées pour des fonctionnalités Exchange telles que la messagerie unifiée, la migration, l’approbation de messages et la découverte électronique locale. Ce tableau répertorie les informations sur les boîtes aux lettres système telles qu'elles apparaissent dans Active Directory.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Boîte aux lettres</th>
<th>Nom</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organisation</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>Approbation de messages</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p>où <em>x</em> est un nombre aléatoire et unique affecté à chaque forêt Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Stockage de données de messagerie unifiée</p></td>
<td><p>SystemMailbox {e0dc1c29 89 c 3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>Découverte</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>Messagerie fédérée</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>Migration</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


Pour désactiver le dernier serveur de boîtes aux lettres Exchange dans votre organisation, vous devez d’abord désactiver ces boîtes aux lettres système à l’aide de la cmdlet [Disable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997210\(v=exchg.150\)). Lorsque vous désactivez un serveur de boîtes aux lettres contenant ces boîtes aux lettres système, vous devez les déplacer vers un autre serveur de boîtes aux lettres pour être sûr de ne perdre aucune fonctionnalité.

## Planification des boîtes aux lettres

Les boîtes aux lettres sont créées dans les bases de données de boîtes aux lettres sur les serveurs Exchange sur lesquels le rôle serveur de boîtes aux lettres est installé. Pour fournir une plate-forme fiable et efficace à vos utilisateurs de boîte aux lettres, une planification détaillée du déploiement des serveurs et bases de données de boîtes aux lettres est essentielle. Pour plus d’informations sur la planification des serveurs de boîtes aux lettres et des bases de données, consultez la rubrique [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Groupes de distribution

Les groupes de distribution sont des objets groupe Active Directory à extension messagerie principalement utilisés pour distribuer des messages à plusieurs destinataires. Tout type de destinataire peut être membre d'un groupe de distribution.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Notez les différences terminologiques entre Active Directory et Exchange. Dans Active Directory, un groupe de distribution correspond à tout groupe sans contexte de sécurité, qu'il soit doté d'une extension messagerie ou non. Dans Exchange, tous les groupes à extension messagerie sont appelés groupes de distribution, qu’ils aient ou non un contexte de sécurité.</td>
</tr>
</tbody>
</table>


Exchange prend en charge les types de groupe de distribution suivants :

  - **Groupes de distribution**   Il s’agit d’objets de groupe de distribution universel Active Directory à extension messagerie. Ils peuvent uniquement être utilisés pour distribuer des messages à un groupe de destinataires.

  - **Groupes de sécurité à extension messagerie**   Il s’agit d’objets de groupe universel de sécurité Active Directory à extension messagerie. Ils peuvent être utilisés pour affecter l’accès à des ressources dans Active Directory et distribuer des messages.

  - **Groupes non universels à extension messagerie**   Il s'agit d'objets de groupe local ou global Active Directory à extension messagerie. Vous pouvez créer ou activer la messagerie de groupes de distribution universels uniquement. Vous disposez peut-être de groupes à extension messagerie ayant été migré à partir de versions antérieures d'Exchange qui ne sont pas des groupes universels. Ces groupes peuvent toujours êtres gérés via le CAE ou l’environnement de ligne de commande Exchange Management Shell.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour convertir un groupe de domaine local ou global en groupe universel, vous pouvez utiliser la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123770(v=exchg.150)">Set-Group</a> de l'environnement de ligne de commande.</td>
    </tr>
    </tbody>
    </table>


## Groupes de distribution dynamique

Les groupes de distribution dynamique sont des groupes de distribution dont l'appartenance se base sur des filtres des destinataires spécifiques plutôt que sur un ensemble de destinataires défini.

Contrairement aux groupes de distribution habituels, la liste des membres de ces groupes de distribution dynamiques est calculée chaque fois qu'un message leur est envoyé, en fonction des filtres et conditions spécifiés. Lorsqu’un message électronique est envoyé à un groupe de distribution dynamique, il est remis à tous les destinataires de l’organisation qui correspondent aux critères définis pour ce groupe de distribution dynamique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un groupe de distribution dynamique inclut tout destinataire dans Active Directory dont les attributs correspondent au filtre du groupe au moment de l'envoi du message. Si les propriétés d'un destinataire sont modifiées pour correspondre au filtre du groupe, ce destinataire peut involontairement devenir membre du groupe et commencer à recevoir des messages envoyés au groupe de distribution dynamique. Des processus de déploiement de compte cohérents et clairement définis peuvent limiter ce risque.</td>
</tr>
</tbody>
</table>


Pour faciliter la création de filtres des destinataires pour les groupes de distribution dynamique, vous pouvez utiliser des filtres prédéfinis. Un *filtre prédéfini* est un filtre couramment utilisé qui permet de répondre à de nombreux critères de filtrage des destinataires. Vous pouvez utiliser ces filtres pour spécifier les types de destinataire que vous voulez inclure dans un groupe de distribution dynamique. En outre, vous pouvez également spécifier la liste des conditions que les destinataires doivent satisfaire. Vous pouvez créer des conditions prédéfinies sur la base des propriétés suivantes :

  - Attributs personnalisés 1–15

  - Département ou région

  - Société

  - Département

  - Conteneur de destinataires

Vous pouvez également spécifier des conditions en fonction de propriétés de destinataire autres que celles répertoriées précédemment. L'environnement de ligne de commande permet de créer une requête personnalisée pour le groupe de distribution dynamique. N’oubliez pas que les paramètres de filtre et de condition pour les groupes de distribution dynamiques dotés de filtres de destinataires personnalisés ne peuvent être gérés qu’à l’aide de l’environnement de ligne de commande Exchange Management Shell. Pour obtenir un exemple de création d'un groupe de distribution dynamique à l'aide d'une requête personnalisée, consultez la rubrique [Gérer des groupes de distribution dynamiques](manage-dynamic-distribution-groups-exchange-2013-help.md).

## Contacts de messagerie

Les contacts de messagerie contiennent généralement des informations sur les personnes ou les entités extérieures à votre organisation Exchange. Les contacts de messagerie peuvent apparaître dans le carnet d’adresses partagé de votre organisation (également appelé liste d’adresses globale, ou GAL) et dans d’autres listes d’adresses. Ils peuvent également être ajoutés en tant que membres à des groupes de distribution. Chaque contact dispose d’une adresse de messagerie externe et tous les messages électroniques envoyés à un contact sont automatiquement transférés à cette adresse. Les contacts sont parfaits pour représenter des personnes extérieures à votre organisation Exchange (dans le carnet d’adresses partagé) qui n’ont pas besoin d’accéder à des ressources internes. Les types de contact de messagerie suivants sont disponibles :

  - **Contacts de messagerie**   Les contacts de messagerie sont des contacts de Active Directory à extension messagerie qui contiennent des informations sur les personnes ou les entités extérieures à votre organisation Exchange.

  - **Contacts de forêt de messagerie**   Ces contacts représentent des objets destinataire d'une autre forêt. Ces contacts sont généralement créés par la synchronisation d’annuaires. Les contacts de forêt de messagerie sont des objets destinataires en lecture seule qui peuvent être mis à jour ou supprimés uniquement à l'aide de la synchronisation. Vous ne pouvez pas utiliser les interfaces de gestion Exchange pour modifier ou supprimer un contact de forêt de messagerie.

## Utilisateurs de messagerie

Les utilisateurs de messagerie sont semblables aux contacts de messagerie. Tous deux disposent d’adresses de messagerie externes, contiennent des informations sur des personnes extérieures à votre organisation Exchange et peuvent être affichés dans le carnet d’adresses partagé et d’autres listes d’adresses. Toutefois, contrairement à un contact de messagerie, un utilisateur de messagerie est doté d’informations d’identification d’ouverture de session Active Directory et peut accéder aux ressources pour lesquelles il dispose d’autorisations.

Si une personne externe à votre organisation a besoin d'accéder aux ressources de votre réseau, vous devez créer un utilisateur de messagerie plutôt qu'un contact de messagerie. Par exemple, vous pouvez créer des utilisateurs de messagerie pour des consultants temporaires qui ont besoin d’accéder à l’infrastructure du serveur mais utiliseront leur propre adresse de messagerie externe.

Un autre scénario consiste à créer des utilisateurs de messagerie dans votre organisation pour les utilisateurs qui ne souhaitent pas conserver de boîte aux lettres Exchange. Par exemple, après une acquisition, la société acquise peut conserver son infrastructure de messagerie distincte, mais peut également avoir besoin d'accéder aux ressources de votre réseau. Pour ces utilisateurs, vous pouvez créer des utilisateurs de messagerie plutôt que des utilisateurs de boîte aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans le CAE, la page <strong>Destinataires</strong> &gt; <strong>Contacts</strong> permet de créer et gérer les utilisateurs de messagerie. Il n’existe pas de page distincte pour les utilisateurs de messagerie.</td>
</tr>
</tbody>
</table>


## Dossiers publics à extension messagerie

Les dossiers publics sont conçus comme un référentiel des informations partagées entre plusieurs utilisateurs. Le fait de doter un dossier public d'une extension messagerie apporte aux utilisateurs un niveau de fonctionnalité supplémentaire. Outre la possibilité de publier des messages dans le dossier, les utilisateurs peuvent échanger des messages électroniques avec le dossier public. Chaque dossier à extension messagerie a un objet dans Active Directory qui mémorise ses adresses de messagerie, le nom de son carnet d’adresses et d’autres attributs de messagerie.

Vous pouvez gérer les dossiers publics via le CAE ou l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations sur la gestion des dossiers publics, consultez la rubrique [Dossiers publics](public-folders-exchange-2013-help.md).

## Destinataire Microsoft Exchange

Le destinataire Microsoft Exchange est un objet de destinataire spécifique qui fournit un expéditeur de message unifié et connu distinguant les messages générés par le système des autres messages. Il remplace l'expéditeur « Administrateur système » utilisé pour les messages générés par le système dans les versions antérieures d'Exchange.

Le destinataire Microsoft Exchange n'est pas un objet de destinataire classique, comme une boîte aux lettres, un utilisateur de messagerie ou un contact de messagerie, et n'est pas géré à l'aide d'outils de destinataire standard. Cependant, vous pouvez utiliser la cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/fr-fr/library/aa997443\(v=exchg.150\)) de l'environnement de ligne de commande pour configurer le destinataire Microsoft Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque des messages générés par le système sont envoyés à un expéditeur externe, le destinataire Microsoft Exchange n'est pas utilisé comme expéditeur du message. L’adresse de messagerie spécifiée par le paramètre <em>ExternalPostmasterAddress</em> pour la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb124151(v=exchg.150)">Set-TransportConfig</a> est utilisée à la place.</td>
</tr>
</tbody>
</table>


## Documentation de destinataires

Le tableau suivant contient des liens vers des rubriques qui vous aideront à découvrir et à gérer les destinataires Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rubrique</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Création de boîtes aux lettres utilisateur</a></p></td>
<td><p>Apprendre à créer des boîtes aux lettres d’utilisateur à l’aide du centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Gestion des boîtes aux lettres utilisateur</a></p></td>
<td><p>Apprendre à créer des boîtes aux lettres utilisateur, modifier les propriétés de boîte aux lettres et modifier en bloc des propriétés sélectionnées pour plusieurs boîtes aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">Gérer les boîtes aux lettres liées</a></p></td>
<td><p>Découvrir les exigences des boîtes aux lettres liées, comment créer et lier ces dernières à un compte principal et changer les propriétés des boîtes aux lettres liées.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-and-manage-distribution-groups-exchange-2013-help.md">Création et gestion de groupes de distribution</a></p></td>
<td><p>Apprendre à créer et gérer des groupes de distribution et créer une stratégie de noms de groupes pour votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-enabled-security-groups-exchange-2013-help.md">Gérer les groupes de sécurité à extension de messagerie</a></p></td>
<td><p>Apprendre à créer et gérer des groupes de sécurité à extension messagerie.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-dynamic-distribution-groups-exchange-2013-help.md">Gérer des groupes de distribution dynamiques</a></p></td>
<td><p>Apprendre à créer des groupes de distribution dynamique et gérer des propriétés de groupe de distribution dynamique, par exemple, à l’aide d’attributs personnalisés et autres propriétés pour déterminer l’appartenance au groupe.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-contacts-exchange-2013-help.md">Gérer les contacts de messagerie</a></p></td>
<td><p>Apprendre à créer et gérer des contacts de messagerie.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-mail-users-exchange-2013-help.md">Gérer les utilisateurs de messagerie</a></p></td>
<td><p>Apprendre à créer et gérer des utilisateurs de messagerie.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-and-manage-room-mailboxes-exchange-2013-help.md">Créer et gérer des boîtes aux lettres de salle</a></p></td>
<td><p>Apprendre à créer des boîtes aux lettres de salle et gérer des propriétés de boîte aux lettres de salle, comme l’activation des réunions périodiques et la configuration des options de planification et de réservation.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-equipment-mailboxes-exchange-2013-help.md">Gérer les boîtes aux lettres d’équipement</a></p></td>
<td><p>Apprendre à créer des boîtes aux lettres d’équipement, configurer les options de planification et de réservation, et gérer d’autres propriétés de boîte aux lettres.</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">Boîtes aux lettres déconnectées</a></p></td>
<td><p>Découvrir les deux types de boîtes aux lettres déconnectées et apprendre à les utiliser.</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">Attributs personnalisés</a></p></td>
<td><p>Apprendre à ajouter des informations sur un destinataire à l’aide d’attributs personnalisés.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/bb124268(v=exchg.150)">Filtres dans les commandes de l’environnement de ligne de commande Exchange Management Shell du destinataire</a></p></td>
<td><p>Apprendre à utiliser des filtres prédéfinis ou personnalisés avec des commandes pour filtrer un ensemble de destinataires.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-permissions-for-recipients-exchange-online-help.md">Gestion des autorisations des destinataires</a></p></td>
<td><p>Apprendre à utiliser le CAE ou l’environnement de ligne de commande pour attribuer des autorisations aux utilisateurs et aux groupes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">Distribution automatique de boîtes aux lettres</a></p></td>
<td><p>Découvrez comment fonctionne la distribution automatique de boîtes aux lettres et comment contrôler la sélection des bases de données pour les boîtes aux lettres nouvelles ou déplacées.</p></td>
</tr>
</tbody>
</table>

