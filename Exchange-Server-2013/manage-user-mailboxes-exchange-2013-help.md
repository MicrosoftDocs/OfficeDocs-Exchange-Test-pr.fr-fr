---
title: 'Gestion des boîtes aux lettres utilisateur: Exchange 2013 Help'
TOCTitle: Gestion des boîtes aux lettres utilisateur
ms:assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123809(v=EXCHG.150)
ms:contentKeyID: 50478733
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.translationtype: HT
---

# Gestion des boîtes aux lettres utilisateur

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-05-27_

Après avoir créé une boîte aux lettres d'utilisateur, vous pouvez y apporter des modifications et définir des propriétés supplémentaires via le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell.

Vous pouvez également modifier les propriétés de plusieurs boîtes aux lettres utilisateur en même temps. Pour plus d'informations, consultez la rubrique Modifier des boîtes aux lettres utilisateur en bloc.

## Ce qu'il faut savoir avant de commencer

  - Durée estimée pour effectuer chaque tâche de boîte aux lettres utilisateur : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Modifier les propriétés de boîte aux lettres utilisateur

## Utiliser le CAE pour modifier les propriétés des boîtes aux lettres utilisateur

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez changer les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page Propriétés de la boîte aux lettres, cliquez sur l'une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Espace de stockage utilisé
    
      - Informations sur le contact
    
      - Organisation
    
      - Adresse de messagerie
    
      - Fonctionnalités de boîte aux lettres
    
      - Membre de
    
      - Infos-courrier
    
      - Délégation de boîtes aux lettres

## Général

Dans la section **Général**, vous pouvez afficher ou modifier des informations de base sur l'utilisateur.

  - **Prénom**, **Initiales**, **Nom de famille**

  - **\* Nom**   Il s'agit du nom qui s'affiche dans Active Directory. Si vous modifiez ce nom, il ne peut pas comporter plus de 64 caractères.

  - **\* Nom complet** Ce nom s’affiche dans le carnet d’adresses de l’organisation, sur les lignes À : et De : des messages électroniques, ainsi que dans la liste Boîte aux lettres. Ce nom ne peut pas contenir d’espaces vides avant ou après le nom complet.

  - **\* Alias** Ce paramètre spécifie l'alias de messagerie électronique pour l'utilisateur. L’alias de l’utilisateur est la partie de l’adresse de messagerie qui apparaît à gauche du symbole (@). Ce dernier doit être unique dans la forêt.

  - **\* Nom de connexion utilisateur**    C'est le nom dont l'utilisateur se servira pour accéder à sa boîte aux lettres et se connecter au domaine. Généralement, le nom de connexion utilisateur se compose de l’alias de l’utilisateur sur la partie gauche, du symbole @ et, à droite du symbole @, du nom de domaine dans lequel réside le compte utilisateur.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette zone est appelée <strong>ID de l’utilisateur</strong> dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>


  - **Exiger la modification du mot de passe à la prochaine ouverture de session**   Activez cette case à cocher si vous souhaitez que l'utilisateur réinitialise le mot de passe lors de la connexion suivante à sa boîte aux lettres.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette case n’est pas disponible dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>


  - **Masquer des listes d'adresses**   Activez cette case à cocher pour empêcher que le destinataire n'apparaisse dans le carnet d'adresses et les autres listes d'adresses définies dans votre organisation Exchange. Après activation de cette case à cocher, les utilisateurs peuvent encore envoyer des messages au destinataire en utilisant l'adresse de messagerie.

Cliquez sur **Plus d'options** pour afficher ou modifier les propriétés supplémentaires suivantes :

  - **Unité d'organisation**   Ce champ en lecture seule affiche l'unité d'organisation (UO) qui contient le compte d'utilisateur. Vous devez utiliser le composant Utilisateurs et ordinateurs Active Directory pour déplacer le compte d'utilisateur vers une autre unité d'organisation.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette case n’est pas disponible dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>


  - **Base de données de boîtes aux lettres**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres. Pour déplacer la boîte aux lettres vers une base de données différente, sélectionnez-la dans la liste de boîte aux lettres, puis cliquez sur **Déplacer la boîte aux lettres vers une autre base de données** dans le volet d'informations.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette option n’est pas disponible dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>


  - **Attributs personnalisés**   Cette section affiche les attributs personnalisés définis pour la boîte aux lettres utilisateur. Pour spécifier des valeurs d'attribut personnalisées, cliquez sur **Modifier**. Vous pouvez spécifier jusqu'à 15 attributs personnalisés pour le destinataire.

## Espace de stockage utilisé

Utilisez la section **Utilisation des boîtes aux lettres** pour afficher ou modifier les paramètres de quota de stockage de boîte aux lettres et de rétention des éléments supprimés pour la boîte aux lettres. Ces paramètres sont configurés par défaut lorsque la boîte aux lettres est créée. Ils utilisent les valeurs qui sont configurées pour la base de données de boîtes aux lettres et s'appliquent à toutes les boîtes aux lettres de cette base de données. Vous pouvez personnaliser ces paramètres pour chaque boîte aux lettres au lieu d'utiliser les paramètres par défaut de la base de données de boîtes aux lettres.

  - **Dernière connexion**   Cette boîte de dialogue en lecture seule s'affiche lors de la dernière connexion de l'utilisateur dans sa boîte aux lettres.

  - **Utilisation de la boîte aux lettres**   Cette zone affiche la taille totale de la boîte aux lettres et le pourcentage du quota total de boîte aux lettres qui a été utilisé.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour obtenir les informations qui sont affichées dans les deux champs précédents, le CAE interroge la base de données de boîtes aux lettres qui héberge la boîte aux lettres. Si le Centre d'administration Exchange ne peut pas communiquer avec la banque d'informations qui contient la base de données de boîte aux lettres, ce champ restera vide. Un message d'avertissement s'affiche si l'utilisateur ne s'est pas connecté à la boîte aux lettres pour la première fois.</td>
</tr>
</tbody>
</table>


Cliquez sur **Plus d'options** pour afficher ou modifier les paramètres de quota de stockage de boîte aux lettres et de rétention des éléments supprimés pour la boîte aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ces paramètres ne sont pas disponibles dans le CAE dans Exchange Online.</td>
</tr>
</tbody>
</table>


  - **Paramètres de quota de stockage**   Pour personnaliser ces paramètres pour la boîte aux lettres et ne pas utiliser les paramètres par défaut de la base de données de boîte aux lettres, cliquez sur **Personnaliser les paramètres de cette boîte aux lettres**, saisissez la nouvelle valeur puis cliquez sur **Enregistrer**.
    
    La plage de valeurs de tous les paramètres de quota de stockage s'étend de 0 à 2047 gigaoctets (Go).
    
      - **Émettre un avertissement à (Go)**   Ce champ affiche la limite de stockage maximale avant qu'un avertissement ne soit présenté à l'utilisateur. Si la taille de la boîte aux lettres atteint ou dépasse la valeur spécifiée, Exchange envoie un message d'avertissement à l'utilisateur.
    
      - **Interdire l'envoi à (Go)**   Ce champ affiche la limite d'*interdiction d'envoi* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l'utilisateur d'envoyer de nouveaux messages et affiche un message d'erreur descriptif.
    
      - **Interdire l'envoi et la réception à (Go)**   Ce champ affiche la limite d'*interdiction d'envoi et de réception* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l'utilisateur de la boîte aux lettres d'envoyer de nouveaux messages et ne remettra plus de nouveaux messages dans la boîte aux lettres. Tous les messages envoyés à cette boîte aux lettres seront renvoyés à l'expéditeur avec un message d'erreur descriptif.

  - **Paramètres de rétention des éléments supprimés**   Pour personnaliser ces paramètres pour la boîte aux lettres et ne pas utiliser les paramètres par défaut de la base de données de boîte aux lettres, cliquez sur **Personnaliser les paramètres de cette boîte aux lettres**, saisissez la nouvelle valeur puis cliquez sur **Enregistrer**.
    
      - **Conserver les éléments supprimés pendant (jours)**   Ce champ affiche la durée pendant laquelle les éléments supprimés sont conservés avant leur suppression définitive sans récupération possible par l’utilisateur. Lors de la création de la boîte aux lettres, cette valeur est basée sur les paramètres de rétention des articles supprimés configurés pour la base de données de la boîte aux lettres. Par défaut, une base de données de boîtes aux lettres est configurée pour conserver les éléments supprimés pendant 14 jours. La plage de valeurs de cette propriété s'étend de 0 à 24 855 jours.
    
      - **Ne pas supprimer définitivement les éléments tant que la base de données n?fa pas été sauvegardée**   Cochez cette case pour empêcher la suppression des éléments jusqu?fà la sauvegarde de la base de données de boîtes aux lettres sur laquelle la boîte aux lettres est située.

## Informations sur le contact

Utilisez la section **Coordonnées** pour afficher ou modifier les coordonnées de l'utilisateur. L'information sur cette page s'affiche dans le carnet d'adresses. Cliquez sur **Plus d'options** pour afficher des boîtes de dialogue supplémentaires.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le champ <strong>État/Province</strong> permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie électronique ou des listes d'adresses.</td>
</tr>
</tbody>
</table>


Les utilisateurs de boîtes aux lettres peuvent utiliser Outlook ou Outlook Web App pour afficher et modifier leurs propres informations de contact. Mais ils ne peuvent pas modifier les informations dans les zones **Remarques** et **Page web**.

## Organisation

La section **Organisation** permet d'enregistrer des informations détaillées sur le rôle de l'utilisateur dans l'organisation. Ces informations s'affichent dans le carnet d'adresses. Aussi, vous pouvez créer un organigramme virtuel accessible à partir de clients de messagerie, tels qu'Outlook.

  - **Titre   **Cette zone permet d'afficher ou de modifier le titre du destinataire.

  - **Service**   Cette zone permet d'afficher ou de modifier le service dans lequel l'utilisateur travaille. Ce champ permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie ou des listes d'adresses.

  - **Société**   Cette zone permet d'afficher ou de modifier la société pour laquelle l'utilisateur travaille. Ce champ permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie ou des listes d'adresses.

  - **Gestionnaire**   Pour ajouter un gestionnaire, cliquez sur **Parcourir**. Dans **Sélectionner le gestionnaire**, sélectionnez une personne, puis cliquez sur **OK**.

  - **Collaborateurs**   Vous ne pouvez pas modifier ce champ. Un *collaborateur* est un utilisateur qui dépend d'un responsable spécifique. Si vous avez indiqué un responsable pour l’utilisateur, ce dernier apparaît en tant que collaborateur dans les informations détaillées relatives à la boîte aux lettres du responsable. Par exemple, Kari est le supérieur hiérarchique de Chris et de Kate. Ainsi, la boîte aux lettres de Kari figure dans la zone **Responsable** des boîtes aux lettres de Chris et de Kate, et ces derniers apparaissent dans la zone **Rapports directs** des propriétés de la boîte aux lettres de Kari.

## Adresse de messagerie

Utilisez la section **Adresse de messagerie** pour afficher ou modifier les adresses de messagerie électronique associées à la boîte aux lettres utilisateur. Cela inclut l’adresse SMTP principale de l’utilisateur et toutes les adresses proxy associées. L'adresse SMTP principale (également appelée *adresse de réponse par défaut*) est affichée en gras dans la liste d'adresses, la valeur **SMTP** apparaissant en lettres majuscules dans la colonne **Type**.

  - **Ajouter **  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l'un des types d'adresses suivants :
    
      - **SMTP**   Il s'agit du type d'adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone **\* Adresse de messagerie**.
    
      - **EUM**   Une adresse de messagerie unifiée Exchange est utilisée par le service de messagerie unifiée de Microsoft Exchange pour localiser des utilisateurs à extension messagerie unifiée dans une organisation Exchange. Les adresses de messagerie unifiée Exchange sont composées du numéro de poste et du plan de numérotation de messagerie unifiée de l'utilisateur à extension messagerie unifiée. Cliquez sur ce bouton puis tapez le numéro de poste dans le champ **Adresse/Poste**. Cliquez ensuite sur **Parcourir** et sélectionnez un plan de numérotation pour l'utilisateur.
    
      - **Adresse personnalisée**   Cliquez sur ce bouton et saisissez dans la zone **\* Adresse de messagerie** l'un des types d'adresse de messagerie électronique non SMTP pris en charge.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>À l'exception des adresses X.400, Exchange ne valide pas la mise en forme des adresses personnalisées. Vous devez veiller à ce que l'adresse personnalisée que vous spécifiez soit conforme aux exigences de mise en forme pour ce type d'adresse.</td>
        </tr>
        </tbody>
        </table>
    
      - **En faire l’adresse de réponse**   Dans Exchange Online, vous pouvez cocher cette case pour faire de la nouvelle adresse électronique l’adresse SMTP principale de la boîte aux lettres. Cette case n’est pas disponible dans le CAE dans Exchange 2013.

  - **Mettre à jour auto. les adresses selon la stratégie de destinataire   **Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d'adresse de messagerie dans votre organisation. Cette case à cocher est activée par défaut.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Cette case n’est pas disponible dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>


  - **En faire l’adresse de réponse**

## Fonctionnalités de boîte aux lettres

Dans la section **Fonctionnalités de boîte aux lettres**, vous pouvez afficher ou modifier les fonctionnalités et paramètres de boîte aux lettres suivants :

  - **Stratégie de partage**   Ce champ affiche la stratégie de partage appliquée à la boîte aux lettres. Une stratégie de partage contrôle la façon dont les utilisateurs de votre organisation peuvent partager les informations de calendrier et de contact avec des utilisateurs extérieurs à votre organisation Exchange. La stratégie de partage par défaut est attribuée aux boîtes aux lettres au moment de leur création. Pour modifier la stratégie de partage attribuée à l’utilisateur, sélectionnez-en une autre dans la liste déroulante.

  - **Stratégie d'attribution de rôle**   Ce champ affiche la stratégie d'attribution de rôle affectée à la boîte aux lettres. La stratégie d'attribution de rôle indique les rôles RBAC (contrôle d'accès basé sur un rôle) qui sont assignés à l'utilisateur et elle contrôle les paramètres de configuration de groupe de distribution et de boîte aux lettres spécifiques que l'utilisateur peut modifier. Pour modifier la stratégie d’attribution de rôle affectée à l’utilisateur, sélectionnez-en une autre dans la liste déroulante.

  - **Stratégie de rétention**   Ce champ affiche la stratégie de rétention attribuée à la boîte aux lettres. Une stratégie de rétention est un groupe de balises de rétention qui sont appliquées à la boîte aux lettres de l’utilisateur. Elles vous permettent de contrôler la durée de conservation des éléments des boîtes aux lettres des utilisateurs et de définir l'action à effectuer sur les éléments qui ont atteint une certaine ancienneté. Aucune stratégie de rétention n’est attribuée aux boîtes aux lettres lorsque ces dernières sont créées. Pour attribuer une stratégie de rétention à l'utilisateur, sélectionnez-en une dans la liste déroulante.

  - **Stratégie de carnet d'adresses**   Cette case à cocher indique la stratégie de carnet d'adresses appliquée à la boîte aux lettres. Une stratégie de carnet d'adresses vous permet de segmenter les utilisateurs dans des groupes spécifiques pour fournir des vues personnalisées du carnet d'adresses. Pour appliquer ou modifier la stratégie de carnet d'adresses appliquée à la boîte aux lettres, sélectionnez-en une dans la liste déroulante.

  - **Messagerie unifiée**   Cette fonctionnalité est désactivée par défaut. Lorsque vous activez la messagerie unifiée, l’utilisateur est en mesure d’utiliser les fonctions de messagerie unifiée de votre organisation et un ensemble par défaut de propriétés de messagerie unifiée est appliqué à l’utilisateur. Cliquez sur **Activer** pour activer la messagerie unifiée pour la boîte aux lettres. Pour plus d'informations sur la procédure d'activation de la messagerie unifiée, reportez-vous à la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Un plan de numérotation de messagerie unifiée et une stratégie de boîte aux lettres de messagerie unifiée doivent exister avant de pouvoir activer la messagerie unifiée.</td>
    </tr>
    </tbody>
    </table>


  - **Appareils mobiles**   Utilisez cette section pour afficher et modifier les paramètres d'Exchange ActiveSync, qui est activé par défaut. Exchange ActiveSync permet d'accéder à une boîte aux lettres Exchange à partir d'un appareil mobile. Cliquez sur **Désactiver Exchange ActiveSync** pour désactiver cette fonctionnalité pour la boîte aux lettres.

  - **Outlook Web App**   Cette fonctionnalité est activée par défaut. Outlook Web App permet d'accéder à une boîte aux lettres Exchange à partir d'un navigateur Web. Cliquez sur **Désactiver** pour désactiver Outlook Web App pour la boîte aux lettres. Cliquez sur **Modifier les détails** pour ajouter ou modifier une stratégie de boîte aux lettres Outlook Web App pour la boîte aux lettres.

  - **IMAP**   Cette fonctionnalité est activée par défaut. Cliquez sur **Désactiver** afin de désactiver la fonctionnalité IMAP pour la boîte aux lettres.

  - **POP3**   Cette fonctionnalité est activée par défaut. Cliquez sur **Désactiver** afin de désactiver la fonctionnalité POP3 pour la boîte aux lettres.

  - **MAPI**   Cette fonctionnalité est activée par défaut. Le protocole MAPI permet d'accéder à une boîte aux lettres Exchange à partir d'un client MAPI tel qu'Outlook. Cliquez sur **Désactiver** pour désactiver MAPI pour la boîte aux lettres.

  - **Mise en attente pour litige**   Cette fonctionnalité est désactivée par défaut. Une mise en attente pour litige permet de conserver les éléments supprimés d'une boîte aux lettres et enregistre les modifications apportées à ces éléments. Les éléments supprimés et tous les éléments modifiés sont renvoyés lors d'une détection. Cliquez sur **Activer** pour placer la boîte aux lettres en mise en attente pour litige. Si la boîte aux lettres est mise en attente pour litige, cliquez sur **Désactiver** pour supprimer la mise en attente pour litige. Les boîtes aux lettres en attente pour litige sont inactives et ne peuvent pas être supprimées. Pour supprimer la boîte aux lettres, supprimez la mise en attente pour litige. Si la boîte aux lettres est mise en attente pour litige, cliquez sur **Modifier les détails** pour afficher et modifier les paramètres de mise en attente pour litige suivants :
    
      - **Date de suspension**   Cette boîte de dialogue en lecture seule indique la date et l'heure auxquelles la boîte aux lettres a été mise en attente pour litige.
    
      - **Suspendu par**   Ce champ en lecture seule indique le nom de l'utilisateur qui a mis la boîte aux lettres en attente pour litige.
    
      - **Remarque**   Ce champ permet d'informer l'utilisateur de la mise en attente pour litige, d'expliquer pourquoi la boîte aux lettres est mise en attente pour litige, ou de fournir de l'aide supplémentaire à l'utilisateur, comme par exemple pour l'informer que la mise en attente pour litige n'affectera pas son utilisation quotidienne de la messagerie.
    
      - **URL**   Ce champ permet de saisir une URL de site Web qui fournit des informations ou de l'aide à propos de la mise en attente pour litige de la boîte aux lettres.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Le texte issu de ces zones apparaît dans la boîte aux lettres de l'utilisateur uniquement s'il utilise Outlook 2010 ou des versions ultérieures. Il n'apparaît pas dans Outlook Web App ou d'autres clients de messagerie. Pour consulter le texte des zones Note et URL dans Outlook, cliquez sur l'onglet <strong>Fichier</strong>. Le commentaire de mis en attente pour litige apparaît dans la page <strong>Informations</strong>, sous <strong>Paramètres du compte</strong>.</td>
        </tr>
        </tbody>
        </table>


  - **Archivage**   S'il n'existe pas de boîte aux lettres d'archive pour l'utilisateur, cette fonctionnalité est désactivée. Pour activer une boîte aux lettres d'archive, cliquez sur **Activer**. Si l'utilisateur possède une boîte aux lettres d'archive, la taille de cette dernière ainsi que les statistiques d'utilisation s'affichent. Cliquez sur **Modifier les détails** pour afficher ou modifier les paramètres de boîte aux lettres d'archivage suivants :
    
      - **État**   Ce champ en lecture seule indique s'il existe ou non une boîte aux lettres d'archivage.
    
      - **Base de données**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres d'archivage. Cette case n’est pas disponible dans Exchange Online.
    
      - **Nom**   Saisissez le nom de la boîte aux lettres d'archivage dans ce champ. Ce nom apparaît sous la liste de dossiers dans Outlook ou Outlook Web App.
    
      - **Quota d’archivage (Go)**   Ce champ indique la taille totale de la boîte aux lettres d’archivage. Pour modifier la taille, saisissez une nouvelle valeur dans le champ ou sélectionnez une valeur dans la liste déroulante.
    
      - **Émettre un avertissement à (Go)**   Ce champ affiche la limite de stockage maximale pour la boîte aux lettres d'archivage avant qu'un avertissement ne soit présenté à l'utilisateur. Si la taille de la boîte aux lettres d'archivage atteint ou dépasse la valeur spécifiée, Exchange envoie un message d'avertissement à l'utilisateur. Pour modifier cette limite, saisissez une nouvelle valeur dans le champ ou sélectionnez une valeur dans la liste déroulante.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Le quota d’archivage et le quota d’émission d’avertissement pour la boîte aux lettres d’archivage ne peuvent pas être modifiés dans Exchange Online.</td>
        </tr>
        </tbody>
        </table>


  - **Options de remise**   Utilisez ce paramètre pour transférer les messages électroniques envoyés à un utilisateur vers un autre destinataire et pour définir le nombre maximum de destinataires auxquels un utilisateur peut envoyer un message. Cliquez sur **Afficher les détails** pour afficher et modifier ces paramètres.
    
      - **Adresse de transfert**   Activez la case à cocher **Activer le transfert**, puis cliquez sur **Parcourir** pour accéder à la page **Sélectionner un utilisateur de messagerie et une boîte aux lettres**. Cette page permet de sélectionner un destinataire auquel vous voulez transférer tous les messages électroniques envoyés à cette boîte aux lettres.
    
      - **Remettre le message à l’adresse de transfert et à la boîte aux lettres**   Cochez cette case pour que les messages soient remis à la fois à l’adresse de transfert et à la boîte aux lettres de l’utilisateur.
    
      - **Limite de destinataire**   Ce paramètre contrôle le nombre maximal de destinataires auxquels l'utilisateur peut envoyer un message. Sélectionnez le **Nombre maximal de destinataires** pour limiter le nombre de destinataires autorisés dans les champs À, Cc et Cci: d'un message électronique, puis spécifiez le nombre maximal de destinataires.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Pour les organisations Exchange locales, la limite de destinataire est illimitée. Pour les organisations Exchange Online, la limite est de 500 destinataires.</td>
        </tr>
        </tbody>
        </table>


  - **Restrictions de taille des messages**   Ces paramètres contrôlent la taille des messages échangés par l'utilisateur. Cliquez sur **Afficher les détails** pour afficher et modifier la taille maximale des messages échangés.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ces paramètres ne peuvent pas être modifiés dans Exchange Online.</td>
    </tr>
    </tbody>
    </table>
    
      - **Messages envoyés**   Pour spécifier une taille maximale de messages envoyés par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l'utilisateur envoie un message dont la taille est supérieure à la taille spécifiée, il est renvoyé à l'utilisateur avec un message d'erreur descriptif.
    
      - **Messages reçus**   Pour spécifier une taille maximale de messages reçus par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l'utilisateur reçoit un message dont la taille est supérieure à la taille spécifiée, le message sera renvoyé à l'expéditeur accompagné d'un message de description de l'erreur.

  - **Restrictions de remise des messages**   Ces paramètres contrôlent les expéditeurs possibles des messages électroniques envoyés à un utilisateur. Cliquez sur **Afficher les détails** pour afficher et modifier ces restrictions.
    
      - **Accepter les messages provenant de**   Cette section permet de spécifier qui peut envoyer des messages à cet utilisateur.
        
          - **Tous les expéditeurs**   Cette option permet d'indiquer que l'utilisateur peut accepter des messages de tous les expéditeurs. Sont inclus à la fois les expéditeurs de votre organisation Exchange et les expéditeurs externes. Cette option est sélectionnée par défaut. Cette option inclut les utilisateurs externes uniquement si vous désactivez la case à cocher **Exiger l'authentification de tous les expéditeurs**. Si cette case à cocher est activée, les messages des utilisateurs externes seront rejetés.
        
          - **Uniquement les expéditeurs de la liste suivante** Cette option permet d'indiquer que l'utilisateur ne peut accepter que les messages provenant d'un ensemble spécifique d'expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour afficher la page **Sélectionner les destinataires**, dans laquelle s'affiche une liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
        
          - **Exiger l'authentification de tous les expéditeurs**   Cette option permet d'empêcher les utilisateurs anonymes d'envoyer des messages à l'utilisateur.
    
      - **Rejeter les messages de**   Cette section permet d'empêcher des personnes d'envoyer des messages à cet utilisateur.
        
          - **Aucun expéditeur**   Cette option permet d’indiquer que la boîte aux lettres ne rejettera les messages d’aucun expéditeur de l’organisation Exchange. Cette option est sélectionnée par défaut.
        
          - **Expéditeurs de la liste suivante** Cette option permet d'indiquer que la boîte aux lettres rejettera les messages provenant d'un ensemble spécifique d'expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour accéder à la page **Sélectionner les destinataires**, qui contient une liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").

## Membre de

La section **Membre de** permet d'afficher une liste des groupes de distribution ou de groupes de sécurité auxquels cet utilisateur appartient. Vous ne pouvez pas modifier les informations d'appartenance sur cette page. Notez que l'utilisateur peut répondre aux critères d'un ou de plusieurs groupes de distribution dynamiques de votre organisation. Toutefois, les groupes de distribution dynamiques ne s'affichent pas sur cette page, car leur appartenance est calculée à chaque utilisation.

## Infos-courrier

Utilisez la section **Info courrier** pour ajouter une Info courrier afin d'alerter les utilisateurs de problèmes potentiels s'ils envoient un message à ce destinataire. Une info-courrier est un texte qui s'affiche dans la barre d'informations lorsque ce destinataire est ajouté aux champs À, Cc ou Cci d'un nouveau message électronique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les infos courrier peuvent comporter des balises HTML, mais les scripts ne sont pas autorisés. Une info courrier personnalisée ne doit pas comporter plus de 175 caractères affichés. Les balises HTML ne sont pas prises en compte dans cette limite.</td>
</tr>
</tbody>
</table>


## Délégation de boîtes aux lettres

Utilisez la section **Délégation de boîtes aux lettres** pour attribuer des autorisations aux autres utilisateurs (également nommés *délégués*) pour leur permettre de se connecter à la boîte aux lettres de l’utilisateur ou d’envoyer des messages au nom de l’utilisateur. Vous pouvez attribuer les autorisations suivantes :

  - **Envoyer sous**   Cette autorisation permet aux utilisateurs autres que le propriétaire de la boîte aux lettres d'utiliser la boîte aux lettres pour envoyer des messages. Une fois cette autorisation attribuée à un délégué, tout message envoyé par un délégué depuis cette boîte aux lettres s'affiche comme s'il était envoyé par le propriétaire de la boîte aux lettres. Toutefois, cette autorisation ne permet pas à un délégué de se connecter à la boîte aux lettres de l’utilisateur.

  - **Envoyer de la part de**   Cette autorisation permet également à un délégué d'utiliser cette boîte aux lettres pour envoyer des messages. Cependant, une fois cette autorisation attribuée à un délégué, l'adresse **De :** de tous les messages envoyés par le délégué indique que le message a été envoyé par le délégué, au nom du propriétaire de la boîte aux lettres.

  - **Accès total**   Cette autorisation permet à un délégué de se connecter à la boîte aux lettres de l’utilisateur et d’afficher le contenu de la boîte aux lettres. Cependant, une fois cette autorisation attribuée à un délégué, celui-ci ne peut pas envoyer de messages depuis cette boîte aux lettres. Pour permettre à un délégué d’envoyer des courriers électroniques depuis la boîte aux lettres de l’utilisateur, vous devez attribuer au délégué l’autorisation Envoyer sous ou Envoyer au nom de.

Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") sous l'autorisation voulue afin d'afficher une page qui présente une liste de tous les destinataires de votre organisation Exchange auxquels peut être attribuée l'autorisation. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les propriétés des boîtes aux lettres d'utilisateurs

Utilisez les cmdlets **Get-Mailbox** et **Set-Mailbox** pour afficher et modifier les propriétés des boîtes de réception des utilisateurs. En utilisant l'environnement de ligne de commande Exchange Management Shell, vous avez la possibilité de modifier les propriétés de plusieurs boîtes aux lettres. Pour plus d'informations sur les paramètres qui correspondent aux propriétés des boîtes aux lettres, consultez les rubriques suivantes :

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

Voici quelques exemples d'utilisation de l'environnement de ligne de commande pour modifier des propriétés de boîtes aux lettres utilisateurs.

Dans cet exemple, nous montrons comment transférer les messages électroniques de Pat Coleman vers la boîte aux lettres de Sunil Koduri (sunilk@contoso.com).

    Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com

Cet exemple utilise la commande **Get-Mailbox** pour trouver toutes les boîtes aux lettres utilisateurs dans l'organisation, puis la commande **Set-Mailbox** est utilisée pour définir la limite à 500 destinataires autorisés dans les champs À, Cc et Cci: d'un message électronique.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -RecipientLimits 500

Cet exemple utilise la commande **Get-Mailbox** pour trouver toutes les boîtes aux lettres dans l'unité d'organisation Marketing, puis il utilise la commande **Set-Mailbox** pour configurer ces boîtes aux lettres. Les limites personnalisées d'avertissement, d'interdiction d'envoi et d'interdiction d'envoi et de réception sont définies à 200 mégaoctets (Mo), 250 Mo et 280 Mo, respectivement, et les limites par défaut de la base de données de boîtes aux lettres sont ignorées. Vous pouvez utiliser cette commande pour configurer un ensemble spécifique de boîtes aux lettres de sorte que leurs limites soient plus élevées ou moins élevées que celles des autres boîtes aux lettres de l'organisation.

    Get-Mailbox -OrganizationalUnit "Marketing" | Set-Mailbox -IssueWarningQuota 209715200 -ProhibitSendQuota 262144000 -ProhibitSendReceiveQuota 293601280 -UseDatabaseQuotaDefaults $false 

Cet exemple utilise la cmdlet **Get-Mailbox** pour trouver tous les utilisateurs du département « Customer Service », puis il utilise la cmdlet **Set-Mailbox** pour définir 2 Mo comme taille maximale de message pour l'envoi des messages.

    Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2097152

Cet exemple définit la traduction MailTip (Info courrier) en français et en chinois.

    Set-Mailbox john@contoso.com -MailTipTranslations ("FR: C'est la langue française", "CHT: 這是漢語語言")

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié les propriétés pour une boîte aux lettres, procédez comme suit :

  - Dans le CAE, sélectionnez la boîte aux lettres puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonction modifiée. Selon la propriété modifiée, elle peut être affichée dans le volet Détails de la boîte aux lettres sélectionnée.

  - Dans l'environnement Shell, utilisez la cmdlet **Get-Mailbox** pour vérifier les modifications. L'utilisation du Shell permet d'afficher plusieurs propriétés pour plusieurs boîtes aux lettres. Dans l'exemple ci-dessus, où la limite de destinataires a été modifiée, exécutez la commande suivante pour vérifier la nouvelle valeur.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Dans l'exemple ci-dessus où les limites de message ont été modifiées, exécutez cette commande.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

## Modifier des boîtes aux lettres utilisateur en bloc

Vous pouvez utiliser le CAE pour modifier les propriétés pour plusieurs boîtes aux lettres d'utilisateurs. Lorsque vous sélectionnez deux boîtes aux lettres utilisateurs ou plus dans la liste des boîtes aux lettres du Centre d'administration Exchange, les propriétés pouvant être modifiées en bloc s'affichent dans le volet d'informations. Lorsque vous modifiez l'une de ces propriétés, la modification est appliquée à toutes les boîtes aux lettres sélectionnées.

Voici une liste des propriétés et fonctions de boîtes aux lettres des utilisateurs qui peuvent être modifiées en bloc. Remarquez qu'il n'est pas possible de modifier l'intégralité des propriétés de chaque zone.

  - **Informations de contact**   Permet de modifier des propriétés communes, telles que la rue, le code postal et le nom de la ville.

  - **Organisation**   Permet de modifier des propriétés communes, telles que le nom du service, le nom de la société et le nom du responsable duquel les utilisateurs sélectionnés dépendent.

  - **Attributs personnalisés**   Permet de changer ou d'ajouter des valeurs pour les attributs personnalisés 1-15.

  - **Quota de boîte aux lettres**   Permet de modifier les valeurs de quota des boîtes aux lettres et la période de rétention des éléments supprimés. Non disponible dans Exchange Online.

  - **Connectivité de messagerie**   Permet d'activer ou de désactiver Outlook Web App, POP3, IMAP, MAPI et Exchange ActiveSync.

  - **Archiver**   Permet d'activer ou de désactiver la boîte aux lettres d'archivage.

  - **Stratégie de rétention, stratégie d'attribution de rôle et stratégie de partage**   Permet de mettre à jour les paramètres pour chacune de ces fonctionnalités de boîte aux lettres.

  - **Déplacer les boîtes aux lettres vers une autre base de données**   Permet de déplacer les boîtes aux lettres sélectionnées vers une base de données différente.

  - **Déléguer des autorisations**   Permet d’attribuer des autorisations à des utilisateurs ou des groupes pour qu’ils puissent ouvrir ou envoyer des messages provenant d’autres boîtes aux lettres. Vous pouvez attribuer les autorisations Complet, Envoyer en tant que et Envoyer pour le compte de aux utilisateurs ou groupes. Pour plus de détails, consultez la rubrique [Gestion des autorisations des destinataires](manage-permissions-for-recipients-exchange-online-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le temps estimé pour la réalisation de cette tâche est de 2 minutes, mais ce temps peut être allongé si vous changez plusieurs propriétés ou fonctionnalités à la fois.</td>
</tr>
</tbody>
</table>


## Utiliser le Centre d'administration Exchange pour modifier en bloc des boîtes aux lettres utilisateurs

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres, sélectionnez deux boîtes aux lettres ou plus.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour sélectionner plusieurs boîtes aux lettres adjacentes, maintenez la touche Maj enfoncée, cliquez sur la première, puis sur la dernière boîte aux lettres à modifier. Vous pouvez également sélectionner plusieurs boîtes aux lettres non adjacentes en maintenant enfoncée la touche Ctrl, puis en cliquant sur chacune des boîtes aux lettres à modifier.</td>
    </tr>
    </tbody>
    </table>


3.  Dans le volet d'informations, sous **Modifier en bloc**, sélectionnez les propriétés ou fonctionnalités de boîtes aux lettres à modifier.

4.  Apportez les modifications souhaitées dans la page Propriétés, puis enregistrez-les.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié en bloc des boîtes aux lettres d’utilisateurs, procédez comme suit :

  - Dans le Centre d'administration Exchange, sélectionnez les boîtes aux lettres auxquelles vous avez apporté des changements, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonctionnalité modifiée.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Get-Mailbox** pour vérifier les modifications. L'utilisation du Shell permet d'afficher plusieurs propriétés pour plusieurs boîtes aux lettres. Par exemple, imaginons que vous avez utilisé la fonctionnalité de modification en bloc dans le Centre d'administration Exchange pour activer la boîte aux lettres d'archivage et assigner une stratégie de rétention à tous les utilisateurs de votre organisation. Pour vérifier ces modifications, vous pouvez exécuter la commande suivante :
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,ArchiveDatabase,RetentionPolicy
    
    Pour plus d'informations sur les paramètres disponibles pour la cmdlet **Get-Mailbox**, consultez la rubrique [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

