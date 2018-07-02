---
title: 'Gestion de règles de flux de messagerie: Exchange 2013 Help'
TOCTitle: Gestion de règles de flux de messagerie
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50479472
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de règles de flux de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les règles de flux de messagerie, également appelées règles de transport vous permettent de rechercher des conditions spécifiques sur les messages qui circulent dans votre organisation, et de prendre des mesures les concernant. Cette rubrique vous montre comment créer, copier, classer, activer ou désactiver, supprimer ou importer ou exporter des règles, et comment surveiller l’utilisation de ces règles.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour vous assurer que vos règles fonctionnent comme vous l’entendez, assurez-vous de bien tester chaque règle et les interactions entre les différentes règles.</td>
</tr>
</tbody>
</table>


Vous êtes intéressé par des scénarios où ces procédures sont utilisées ? Consultez les rubriques suivantes :

  - [Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Scénarios courants de blocage de pièce jointe](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Utiliser des règles de flux de messagerie pour acheminer le courrier électronique en fonction d’une liste de mots, d’expressions ou de modèles](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Scénarios courants d’approbation des messages](common-message-approval-scenarios-exchange-2013-help.md)

  - [Utiliser des règles de flux de messagerie afin que les messages puissent contourner le courrier non trié](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Meilleures pratiques pour la configuration de règles de flux de messagerie](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\))

  - [Utilisez les règles de transport pour configurer le filtrage des e-mails en masse](https://technet.microsoft.com/fr-fr/library/dn720438\(v=exchg.150\))

  - [Définir des règles pour chiffrer ou déchiffrer des messages électroniques](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [Création de listes d’expéditeurs bloqués et autorisés à l’échelle de l’organisation dans Office 365](https://technet.microsoft.com/fr-fr/library/dn198251\(v=exchg.150\))

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - l’entrée Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez « Règles de transport » dans [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md) (Exchange Server) ou dans [Autorisations des fonctionnalités dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200673\(v=exchg.150\)).

  - Lorsqu’une règle est répertoriée en tant que **version 14**, cela signifie que la règle a été créée à partir d’un format de règle de flux de messagerie Exchange Server 2010. Toutes les options sont disponibles pour ces règles.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Créer une règle de flux de messagerie

Vous pouvez créer une règle de flux de messagerie en configurant une stratégie de protection contre la perte de données (DLP), en créant une règle, ou en copiant une règle. Vous pouvez utiliser le Centre d’administration Exchange (CAE) ou l’Environnement de ligne de commande Exchange Management Shell.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une fois que vous avez créé ou modifié une règle de flux de messagerie, la règle nouvelle ou mise à jour peut prendre jusqu’à 30 minutes pour être appliquée au courrier électronique.</td>
</tr>
</tbody>
</table>


## Utiliser une stratégie DLP pour créer des règles de flux de messagerie

Chaque stratégie DLP est un ensemble de règles de flux de messagerie. Après avoir créé une stratégie DLP, vous pouvez ajuster les règles à l’aide des procédures suivantes.

1.  Créez une stratégie DLP. Pour plus d’informations, voir :
    
      - [Procédures de DLP pour Exchange Server 2013](dlp-procedures-exchange-2013-help.md)
    
      - [Procédures de DLP pour Exchange Online](dlp-procedures-exchange-2013-help.md)

2.  Modifiez les règles de flux de messagerie créées par la stratégie DLP. Consultez la rubrique Afficher ou modifier une règle de transport.

## Utiliser le CAE pour créer une règle de flux de messagerie

Le CAE vous permet de créer des règles de flux de messagerie à partir d’un modèle, en copiant une règle existante ou à partir de zéro.

1.  Accédez à **Flux de messagerie**\>**Règles**.

2.  Créez la règle à l’aide de l’une des options suivantes :
    
      - Pour créer une règle à partir d’un modèle, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") et sélectionnez un modèle.
    
      - Pour copier une règle, sélectionnez-la, puis sélectionnez **Copier**![Icône Copier](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Icône Copier").
    
      - Pour créer une règle de A à Z, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") puis sélectionnez **Créer une règle**.

3.  Dans la boîte de dialogue **Nouvelle règle**, nommez la règle, puis sélectionnez les conditions et les actions pour cette règle :
    
    1.  Dans **Appliquer cette règle si...**, sélectionnez la condition souhaitée dans la liste des conditions disponibles.
        
          - Pour certaines conditions, vous devez spécifier des valeurs. Par exemple, si vous sélectionnez la condition **L’expéditeur est...**, vous devez indiquer l’adresse d’un expéditeur. Si vous ajoutez un mot ou une expression, notez que les espaces de fin ne sont pas autorisés.
        
          - Si la condition souhaitée ne figure pas dans la liste, ou si vous avez besoin d’ajouter des exceptions, sélectionnez **Plus d’options**. Les exceptions et les autres conditions apparaissent dans la liste.
        
          - Si vous ne souhaitez pas spécifier de condition mais voulez appliquer cette règle à tous les messages de votre organisation, sélectionnez la condition **\[Appliquer à tous les messages\]**.
    
    2.  Dans **Effectuer les opérations suivantes**, sélectionnez l’action que la règle doit appliquer aux messages répondant aux critères parmi les actions disponibles dans la liste.
        
          - La sélection de certaines actions vous invitera à spécifier des valeurs. Par exemple, si vous sélectionnez la condition **Transférer le message pour approbation à...**, vous devez sélectionner un destinataire dans votre organisation.
        
          - Si la condition souhaitée n’est pas répertoriée, sélectionnez **Plus d’options**. D’autres conditions supplémentaires seront répertoriées.
    
    3.  Indiquez comment les données de correspondance de cette règle s’affichent dans les [rapports sur la détection de stratégies DLP](https://go.microsoft.com/fwlink/p/?linkid=402768) et les [rapports de règle de transport](https://go.microsoft.com/fwlink/p/?linkid=402769).
        
          - Sous **Auditer cette règle avec le niveau de gravité**, spécifiez le niveau de gravité de cette règle. Les rapports d’activité Office 365 pour les correspondances de règle de groupe de règles de flux de messagerie par niveau de gravité. Le niveau de gravité est simplement un filtre qui facilite l’utilisation des rapports. Le niveau de gravité n’a aucun impact sur la priorité avec laquelle la règle est traitée.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Si vous désactivez la case à cocher <strong>Auditer cette règle avec un niveau de gravité :</strong>, les correspondances de règle ne s’affichent pas dans les rapports de règle.</td>
            </tr>
            </tbody>
            </table>
    
    4.  Définissez le mode de la règle. Vous pouvez utiliser l’un des deux modes de test disponibles pour tester la règle sans impacter le flux de messagerie. Dans les deux modes de test, lorsque les conditions sont remplies, une entrée est ajoutée au suivi des messages.
        
          - **Appliquer**   La règle est activée et commence à traiter les messages immédiatement. Toutes les actions de la règle seront exécutées.
        
          - **Test avec Conseils de stratégie**   Cette option active la règle, et les actions de conseils de stratégie (**Avertir l’expéditeur par un conseil de stratégie**) seront envoyées, mais aucune action relative à la remise des messages ne sera exécutée. La protection contre la perte de données (DLP) est requise pour pouvoir utiliser ce mode. Pour en savoir plus, consultez la rubrique [Conseils de stratégie](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
        
          - **Test sans Conseils de stratégie**   Seule l’action Générer un rapport d’incident sera appliquée. Aucune action liée à la remise des messages n’est exécutée.

4.  Si la règle vous convient, passez à l’étape 5. Si vous souhaitez ajouter des conditions ou des actions, ou encore spécifier des exceptions ou définir des propriétés supplémentaires, cliquez sur **Plus d’options**. Après avoir cliqué sur **Autres options**, complétez les champs suivants pour créer votre règle :
    
    1.  Pour ajouter des conditions supplémentaires, cliquez sur **Ajouter une condition**. Si vous disposez de plusieurs conditions, vous pouvez supprimer celles de votre choix en cliquant sur **Supprimer X** en regard de celles-ci. Notez qu'un plus grand nombre de conditions est disponible lorsque vous cliquez sur **Autres options**.
    
    2.  Pour ajouter d’autres actions, cliquez sur **Ajoutez une action**. Si vous disposez de plusieurs actions, vous pouvez supprimer celles de votre choix en cliquant sur **Supprimer X** en regard de celles-ci. Notez qu'un plus grand nombre d'actions est disponible lorsque vous cliquez sur **Autres options**.
    
    3.  Pour spécifier des exceptions, cliquez sur **Ajouter une exception**, puis sélectionnez les exceptions dans la liste déroulante **Sauf si...** Vous pouvez retirer des exceptions de la liste en cliquant sur **Supprimer X** en regard de celles-ci.
    
    4.  Pour que cette règle prenne effet après une date donnée, cliquez sur **Activer cette règle à la date suivante :**  et spécifie une date. Notez que la règle restera active avant cette date, mais qu'elle ne sera pas traitée.
        
        De même, vous pouvez choisir de ne plus traiter la règle à une date donnée. Pour ce faire, cliquez sur **Cette règle expire à la date suivante :**  et spécifie une date. Notez que la règle restera active, mais qu'elle ne sera pas traitée.
    
    5.  Vous pouvez choisir de ne plus ajouter d'autres règles lorsque cette règle traite un message. Pour ce faire, cliquez sur **Ne plus traiter de règles**. Si vous activez cette option et qu'un message est traité par cette règle, aucune autre règle n'est traitée pour ce message.
    
    6.  Vous pouvez spécifier la manière dont le message doit être traité si le traitement de la règle ne peut pas être terminé. Par défaut, la règle est ignorée et le message est traité régulièrement, mais vous pouvez décider de renvoyer le message pour traitement. Pour ce faire, cochez la case **Différer le message si le traitement de la règle ne termine pas**.
    
    7.  Par défaut, si votre règle analyse l'adresse de l'expéditeur, elle n'examine que les en-têtes de messages. Cependant, vous pouvez configurer votre règle de manière à examiner également l'enveloppe de message SMTP. Pour spécifier les éléments à examiner, cliquez sur l'une des valeurs suivantes pour l'option **Correspondance avec l'adresse de l'expéditeur dans le message** :
        
          - **En-tête**   Seuls les en-têtes des messages sont examinés.
        
          - **Enveloppe**   Seule l'enveloppe de message SMTP est examinée.
        
          - **En-tête ou enveloppe**   Les en-têtes de messages et les enveloppes de message SMTP sont examinées.
    
    8.  Vous pouvez ajouter des commentaires à cette règle dans la zone **Commentaires**.

5.  Cliquez sur **Enregistrer** pour terminer la création de la règle.

## Utiliser le Environnement de ligne de commande Exchange Management Shell pour créer une règle de flux de messagerie

Cet exemple présente l’utilisation de la cmdlet [New-TransportRule](https://technet.microsoft.com/fr-fr/library/bb125138\(v=exchg.150\)) pour créer une règle de flux de messagerie qui ajoute le texte « `External message to Sales DG:` » aux messages envoyés depuis l’extérieur de l’organisation au groupe de distribution Sales Department.

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

Les paramètres et l’action de règle utilisés dans la procédure ci-dessus servent d’illustration uniquement. Examinez toutes les conditions et actions de règle de flux de messagerie disponibles pour déterminer celles qui répondent à vos besoins.

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une règle de flux de messagerie a bien été créée, procédez comme suit :

  - Dans le CAE, vérifiez que la nouvelle règle de flux de messagerie que vous avez créée figure dans la liste **Règles**.

  - Dans le Environnement de ligne de commande Exchange Management Shell, vérifiez que vous avez bien créé la règle de flux de messagerie en exécutant la commande suivante (l’exemple ci-dessous vérifie la règle créée dans l’exemple de Environnement de ligne de commande Exchange Management Shell ci-dessus) :
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## Afficher ou modifier une règle de flux de messagerie

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une fois que vous avez créé ou modifié une règle de flux de messagerie, la règle nouvelle ou mise à jour peut prendre jusqu’à 30 minutes pour être appliquée au courrier électronique.</td>
</tr>
</tbody>
</table>


## Utiliser le CAE pour afficher ou modifier une règle de flux de messagerie

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Règles**.

2.  Lorsque vous sélectionnez une règle dans la liste, les conditions, actions, exceptions et propriétés de sélection de cette règle sont affichées dans le volet d'informations. Double-cliquez sur une règle pour en afficher toutes les propriétés. La fenêtre de l’éditeur des règles s’ouvre et vous permet de modifier la règle. Pour plus d’informations sur les propriétés des règles, consultez la section Utiliser le CAE pour créer une règle de flux de messagerie plus haut dans cette rubrique.

## Utiliser le Environnement de ligne de commande Exchange Management Shell pour afficher ou modifier une règle de flux de messagerie

L'exemple suivant présente la liste de toutes les règles configurées dans votre organisation :

    Get-TransportRule

Pour afficher les propriétés d’une règle de flux de messagerie spécifique, indiquez le nom ou le GUID de cette règle. Il est généralement utile d’envoyer le résultat à la cmdlet **Format-List** pour mettre en forme les propriétés. L’exemple suivant renvoie toutes les propriétés de la règle de flux de messagerie nommée **Sender is a member of Marketing** :

    Get-TransportRule "Sender is a member of marketing" | Format-List

Pour modifier les propriétés d’une règle existante, utilisez la cmdlet [Set-TransportRule](https://technet.microsoft.com/fr-fr/library/bb123534\(v=exchg.150\)). Cette cmdlet vous permet de modifier les propriétés, conditions, actions ou exceptions associées à une règle. L'exemple suivant ajoute une exception à la règle « Sender is a member of marketing » pour qu'elle ne soit pas appliquée aux messages envoyés par l'utilisateur Kelly Rollin :

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une règle de flux de messagerie a bien été modifiée, procédez comme suit :

  - Dans la liste des règles du CAE, cliquez sur la règle que vous avez modifiée dans la liste **Règles** et consultez le volet d’informations.

  - Dans l’Environnement de ligne de commande Exchange Management Shell, vérifiez que vous avez bien modifié la règle de flux de messagerie en exécutant la commande suivante, qui répertoriera les propriétés que vous avez modifiées avec le nom de la règle (l’exemple ci-dessous vérifie la règle modifiée dans l’exemple de l’Environnement de ligne de commande Exchange Management Shell ci-dessus) :
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## Propriétés de règle de flux de messagerie

Vous pouvez également utiliser la cmdlet Set-TransportRule pour modifier des règles de transport de votre organisation. Voici une liste de propriétés non disponible dans le CAE, que vous pouvez modifier. Pour plus d’informations sur l’utilisation de la cmdlet Set-TransportRule pour apporter ces modifications, voir [Set-TransportRule](https://technet.microsoft.com/fr-fr/library/bb123534\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de la condition dans le CAE</th>
<th>Nom de la condition dans Environnement de ligne de commande Exchange Management Shell</th>
<th>Propriétés</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Arrêter de traiter les règles</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>Vous permet d’arrêter le traitement des règles supplémentaires.</p></td>
</tr>
<tr class="even">
<td><p><strong>Correspondance en-tête/enveloppe</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>Non applicable</p></td>
<td><p>Vous permet d’examiner l’enveloppe de message SMTP, afin de vous assurer de la correspondance de l’en-tête et de l’enveloppe.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>Gravité d’audit</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Vous permet de sélectionner un niveau de gravité pour l’audit.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modes de règle</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Vous permet de définir le mode de la règle.</p></td>
</tr>
</tbody>
</table>


## Définir la priorité d’une règle de flux de messagerie

La règle en haut de la liste est traitée en premier. Cette règle a une **priorité** de 0.

## Utiliser le CAE pour définir la priorité d’une règle

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Règles**. Les règles sont affichées dans l’ordre dans lequel elles sont traitées.

2.  Sélectionnez une règle et utilisez les flèches pour la déplacer vers le haut ou vers le bas de la liste.

## Utiliser le Environnement de ligne de commande Exchange Management Shell pour définir la priorité d’une règle

L’exemple suivant définit la priorité de la règle « Sender is a member of marketing » (L’expéditeur est membre du service Marketing) sur 2 :

    Set-TransportRule "Sender is a member of marketing" priority "2"

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une règle de flux de messagerie a bien été modifiée, procédez comme suit :

  - Dans la liste de règles du CAE, examinez l’ordre des règles.

  - À partir de l’Environnement de ligne de commande Exchange Management Shell, vérifiez la priorité des règles (l’exemple ci-dessous vérifie la règle modifiée dans l’exemple de l’Environnement de ligne de commande Exchange Management Shell ci-dessus) :
    
        Get-TransportRule * | Format-List Name,Priority

## Activer ou désactiver une règle de flux de messagerie

Les règles sont activées lors de leur création. Vous pouvez désactiver une règle de flux de messagerie.

## Utiliser le CAE pour activer ou désactiver une règle de flux de messagerie

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Règles**.

2.  Pour désactiver une règle, décochez la case en regard de son nom.

3.  Pour activer une règle désactivée, cochez la case en regard de son nom.

## Utiliser le Environnement de ligne de commande Exchange Management Shell pour activer ou désactiver une règle de flux de messagerie

L’exemple suivant désactive la règle de flux de messagerie « Sender is a member of marketing » :

    Disable-TransportRule "Sender is a member of marketing"

L’exemple suivant active la règle de flux de messagerie « Sender is a member of marketing » :

    Enable-TransportRule "Sender is a member of marketing"

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une règle de flux de messagerie a bien été activée ou désactivée, procédez comme suit :

  - Dans le CAE, affichez les règles dans la liste **Règles** et vérifiez l’état de la case dans la colonne **ACTIVÉ**.

  - Dans l’Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour renvoyer la liste de toutes les règles de votre organisation, ainsi que leur état :
    
        Get-TransportRule | Format-Table Name,State

## Supprimer une règle de flux de messagerie

## Utiliser le CAE pour supprimer une règle de flux de messagerie

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Règles**.

2.  Sélectionnez la règle à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

## Utiliser le Environnement de ligne de commande Exchange Management Shell pour supprimer une règle de flux de messagerie

L’exemple suivant supprime la règle de flux de messagerie « Sender is a member of marketing » :

    Remove-TransportRule "Sender is a member of marketing"

## Comment savoir si cela a fonctionné ?

Pour vérifier que la règle de flux de messagerie a bien été supprimée, procédez comme suit :

  - Dans le CAE, affichez les règles dans la liste **Règles** et vérifiez que la règle que vous venez de supprimer n’y figure plus.

  - Dans l’Environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante et vérifiez que la règle supprimée n’y figure plus :
    
        Get-TransportRule

## Surveiller l’utilisation des règles

Si vous utilisez Exchange Online ou Exchange Online Protection, vous pouvez vérifier le nombre de fois que chaque règle trouve une correspondance à l’aide d’un rapport de règles. Pour qu’une règle soit incluse dans les rapports, la case **Auditer cette règle avec le niveau de gravité** de cette règle doit être cochée. Vous pouvez consulter un rapport en ligne ou télécharger une version Excel de tous les rapports de protection du courrier électronique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Alors que la plupart des données apparaissent dans le rapport dans les 24 heures, cela peut prendre 5 jours pour certaines données.</td>
</tr>
</tbody>
</table>


## Utiliser le Centre d’administration Office 365 pour générer un rapport de règles

1.  Dans le Centre d’administration Office 365, sélectionnez **Rapports**.

2.  Dans la section **Règles**, sélectionnez **Principales correspondances de règles pour le courrier électronique** ou **Correspondances de règle pour le courrier électronique**.

Pour en savoir plus, voir [Afficher les rapports de protection de courrier électronique](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Télécharger les rapports au format Excel

1.  Sur la page Rapports du Centre d’administration Office 365, sélectionnez **Rapports de protection du courrier électronique (Excel)**.

2.  Si vous utilisez les rapports de protection du courrier électronique Excel pour la première fois, un onglet s’ouvre sur la page de téléchargement.
    
    1.  Sélectionnez **Télécharger** pour télécharger le plug-in Excel de Microsoft Office 365 pour les rapports Exchange Online.
    
    2.  Ouvrez le téléchargement.
    
    3.  Dans la boîte de dialogue de **configuration des rapports de protection du courrier électronique pour Office 365**, sélectionnez **Suivant**, acceptez les termes du contrat de licence, puis sélectionnez **Suivant**.
    
    4.  Sélectionnez le service que vous utilisez, puis sélectionnez **Suivant**.
    
    5.  Vérifiez les paramètres, puis cliquez sur **Suivant**.
    
    6.  Sélectionnez **Installer**. Un raccourci vers les rapports est placé sur votre bureau.

3.  Sur votre bureau, sélectionnez **Rapports de protection du courrier électronique Office 365**.

4.  Dans le rapport, sélectionnez l’onglet **Règles**.

## Importer ou exporter un regroupement de règles de flux de messagerie

Vous devez utiliser le Environnement de ligne de commande Exchange Management Shell pour importer ou exporter un regroupement de règles de flux de messagerie. Pour plus d’informations sur la procédure d’importation d’un regroupement de règles de flux de messagerie à partir d’un fichier XML, consultez la rubrique [Import-TransportRuleCollection](https://technet.microsoft.com/fr-fr/library/bb123582\(v=exchg.150\)). Pour plus d’informations sur la procédure d’exportation d’un regroupement de règles de flux de messagerie vers un fichier XML, consultez la rubrique [Export-TransportRuleCollection](https://technet.microsoft.com/fr-fr/library/bb124410\(v=exchg.150\)).

## Besoin d’aide supplémentaire ?

Ressources pour Exchange Online :

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))

[Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\))

[Courrier des actions de règle de flux dans Exchange en ligne](https://technet.microsoft.com/fr-fr/library/jj919237\(v=exchg.150\))

[Limites concernant les règles de transport et de boîte de réception](https://go.microsoft.com/fwlink/p/?linkid=324584)

Ressources pour Exchange Online Protection :

[Règles de flux de messagerie (règles de transport) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/dn271424\(v=exchg.150\))

[Mail flux conditions et les exceptions (prédicat) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj919234\(v=exchg.150\))

[Envoyer par courrier électronique les actions de règle de flux dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj920117\(v=exchg.150\))

[Limites concernant les règles de transport et de boîte de réception](https://go.microsoft.com/fwlink/p/?linkid=324584)

Ressources pour Exchange Server 2013 :

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

