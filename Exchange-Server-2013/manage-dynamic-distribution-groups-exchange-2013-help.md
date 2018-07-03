---
title: 'Gérer des groupes de distribution dynamiques: Exchange 2013 Help'
TOCTitle: Gérer des groupes de distribution dynamiques
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 50477284
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: HT
---

# Gérer des groupes de distribution dynamiques

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les groupes de distribution dynamiques sont des objets du groupe Active Directory à extension messagerie créés pour accélérer l’envoi massif de messages électroniques et d’autres informations au sein d’une organisation Exchange Microsoft.

Contrairement aux groupes de distribution habituels qui contiennent un ensemble défini de membres, la liste des membres de ces groupes de distribution dynamiques est calculée chaque fois qu’un message leur est envoyé, en fonction des filtres et conditions que vous avez définis. Lorsqu’un courrier électronique est envoyé à un groupe de distribution dynamique, il est remis à tous les destinataires de l’organisation qui respectent les critères définis pour ce groupe.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un groupe de distribution dynamique inclut tout destinataire dans Active Directory ayant des valeurs d'attribut correspondant à son filtre. Si les propriétés d’un destinataire sont modifiées pour correspondre au filtre, le destinataire peut involontairement devenir membre du groupe et commencer à recevoir des messages envoyés au groupe. Des processus de déploiement de compte cohérents et bien définis réduisent la probabilité que cela se produise.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution dynamique » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Permet de créer un groupe de distribution dynamique

## Utiliser l’EAC pour créer un groupe de distribution dynamique

1.  Dans l’EAC, accédez à **Destinataires**  \> **Groupes** \> **Nouveau** \> **Groupe de distribution dynamique**.

2.  Sur la page **Nouveau groupe de distribution dynamique**, complétez les cases suivantes :
    
      - \* **Nom complet**   Saisissez le nom complet. Ce nom apparaît dans le carnet d’adresses partagé, dans la ligne À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes du Centre d’administration Exchange. Le nom d'affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s'agit. Ce nom doit aussi être unique dans la forêt.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>La stratégie de noms de groupes n’est pas appliquée aux groupes de distribution dynamique.</td>
        </tr>
        </tbody>
        </table>
    
      - **\* Alias**   Saisissez le nom de l’alias du groupe. L’alias ne peut pas comporter plus de 64 caractères et doit être unique dans la forêt. Lorsqu’un utilisateur saisit l’alias dans la ligne À : d’un message électronique, sa résolution génère le nom complet du groupe.
    
      - **Description**   Décrivez le groupe afin que l’objet du groupe soit facilement identifiable. Cette description apparaît dans le carnet d’adresses partagé.
    
      - **Unité d’organisation**   Vous pouvez sélectionner une unité d’organisation (UO) autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine Active Directory qui contient l’ordinateur sur lequel le Centre d’administration Exchange est en cours d’exécution. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d’organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d’organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez l'UO souhaitée, puis cliquez sur **OK**.
    
      - **Propriétaire**   Un propriétaire pour un groupe de distribution dynamique est facultatif. Pour ajouter des propriétaires, cliquez sur **Parcourir**, puis sélectionnez des utilisateurs dans la liste.

3.  Utilisez la section **Membres** pour indiquer les types de destinataires pour le groupe et configurer des règles qui doivent déterminer un appartenance. Sélectionnez l’une des cases suivantes :
    
      - **Tous les types de destinataires**   Sélectionnez cette option pour envoyer des messages qui satisfont les critères définis pour ce groupe à tous les types de destinataires.
    
      - **Uniquement les types de destinataires suivants**   Les messages qui satisfont les critères définis pour ce groupe seront envoyés à un ou plusieurs types de destinataires suivants :
        
          - **Utilisateurs avec boîtes aux lettres Exchange**   Activez cette case à cocher si vous souhaitez inclure les utilisateurs ayant des boîtes aux lettres Exchange. Les utilisateurs ayant des boîtes aux lettres Exchange sont ceux qui ont un compte de domaine d’utilisateur et une boîte aux lettres dans l’organisation Exchange.
        
          - **Utilisateurs avec adresses de messagerie externes**   Activez cette case à cocher si vous souhaitez inclure les utilisateurs ayant des adresses de messagerie externes. Les utilisateurs disposant de comptes de messagerie externes ont des comptes de domaine utilisateur dans Active Directory, mais utilisent des comptes de messagerie externes à l’organisation. Cela leur permet d’être inclus dans la liste d’adresses globale (LAG) et ajoutés aux listes de distribution.
        
          - **Boîtes aux lettres de ressources**   Activez cette case à cocher si vous souhaitez inclure les boîtes aux lettres de ressources Exchange. Les boîtes aux lettres de ressources permettent d’administrer, via une boîte aux lettres, des ressources d’entreprise comme une salle de conférence ou un véhicule de société.
        
          - **Contacts avec adresses de messagerie externes**   Activez cette case à cocher si vous souhaitez inclure les contacts ayant des adresses de messagerie externes. Les contacts ayant des adresses de messagerie externes n’ont pas de comptes de domaine utilisateur dans Active Directory, mais l’adresse de messagerie externe est disponible dans la LAG.
        
          - **Groupes à extension messagerie**   Activez cette case à cocher si vous souhaitez inclure les groupes de sécurité ou de distribution à extension messagerie. Les groupes à extension messagerie sont similaires aux groupes de distribution. Les messages électroniques envoyés à un compte de groupe à extension messagerie sont transmis à plusieurs destinataires.

4.  Cliquez sur **Ajouter une règle** pour définir les critères d'appartenance à ce groupe.

5.  Sélectionnez l'un des attributs de destinataire suivant dans la liste déroulante et donnez une valeur. Si la valeur pour l’attribut sélectionné correspond à cette valeur que vous avez définie, le destinataire reçoit un message envoyé à ce groupe.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Attribut</th>
    <th>Envoi du message à un destinataire si...</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Conteneur de destinataires</strong></p></td>
    <td><p>L’objet destinataire réside dans le domaine spécifié ou dans l’unité d’organisation.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Département ou région</strong></p></td>
    <td><p>La valeur spécifiée correspond à la propriété de département ou de région du destinataire.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Company</strong></p></td>
    <td><p>La valeur spécifiée correspond à la propriété Société du destinataire.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Service</strong></p></td>
    <td><p>La valeur spécifiée correspond à la propriété Service du destinataire.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Attribut personnalisé N</strong> (où N est un nombre compris entre 1 et 15)</p></td>
    <td><p>La valeur spécifiée correspond à la propriété CustomAttributeN du destinataire.</p></td>
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
    <td>Les valeurs que vous entrez pour l’attribut sélectionné doivent exactement correspondre à celles qui s’affichent dans les propriétés du destinataire. Par exemple, si vous entrez <strong>Washington</strong> comme <strong>Département ou région</strong>, sauf que la valeur pour la propriété du destinataire est <strong>WA</strong>, la condition n’est pas satisfaite. Notez que les valeurs basées sur un texte que vous avez spécifié ne respectent pas la casse. Par exemple, si vous indiquez <strong>Contoso</strong> pour l’attribut <strong>Société</strong>, les messages sont envoyés à un destinataire si la valeur est <strong>contoso</strong>.</td>
    </tr>
    </tbody>
    </table>


6.  Dans la fenêtre **Spécifier des mots ou des expressions**, entrez la valeur dans la zone de texte. Cliquez sur **Ajouter**, puis sur **OK**.

7.  Pour ajouter une autre règle visant à définir des critères d’appartenance, cliquez sur **Ajouter une règle** sous la règle que vous avez créée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous ajoutez plusieurs règles pour définir une appartenance, un destinataire doit satisfaire les critères de chacune des règles pour recevoir un message envoyé au groupe. En d'autres termes, les règles sont connectées entre elles par l’opérateur booléen <strong>AND</strong>.</td>
    </tr>
    </tbody>
    </table>


8.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer le groupe de distribution dynamique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour spécifier des règles pour des attributs autres que ceux disponibles dans l’EAC, vous devez l’environnement de ligne de commande Exchange Management Shell pour créer un groupe de distribution dynamique. N’oubliez pas que les paramètres de filtre et de condition pour les groupes de distribution dynamiques dotés de filtres des destinataires personnalisés ne peuvent être gérés qu’à l’aide de l’environnement. Pour voir un exemple de création d’un groupe de distribution dynamique avec une requête personnalisée, reportez-vous à la section suivante traitant de l'utilisation de l’environnement de ligne de commande Exchange Management Shell pour créer un groupe de distribution dynamique.</td>
</tr>
</tbody>
</table>


## Utiliser le shell pour créer un groupe de distribution dynamique

Cet exemple crée le groupe de distribution dynamique « Utilisateurs de boîtes aux lettres DDG » qui contient uniquement des utilisateurs de boîtes aux lettres.

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

Cet exemple crée un groupe de distribution dynamique avec un filtre de destinataires personnalisé. Le groupe de distribution dynamique contient tous les utilisateurs de boîte aux lettres sur un serveur nommé Server1.

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

Cet exemple crée un groupe de distribution dynamique avec un filtre de destinataires personnalisé. Le groupe de distribution dynamique contient tous les utilisateurs de boîtes aux lettres dont la valeur de la propriété **CustomAttribute10** est « FullTimeEmployee ».

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb125127\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier la création avec succès d’un groupe de distribution dynamique, procédez comme suit :

  - Dans la CCE, accédez à **Destinataires** \> **Groupes**. Le nouveau groupe de distribution dynamique est affiché dans la liste des groupes. Sous **Type de groupe**, le type est **Groupe de distribution dynamique**.

  - Dans l’environnement Shell, exécutez la commande suivante pour afficher des informations sur le nouveau groupe de distribution dynamique.
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## Modification des propriétés du groupe de distribution dynamique

## Utiliser l’EAC pour modifier les propriétés du groupe de distribution dynamique

1.  Dans la CCE, accédez à **Destinataires** \> **Groupes**.

2.  Dans la liste des groupes, cliquez sur le groupe de distribution dynamique que vous souhaitez afficher et modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du groupe, cliquez sur les sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Propriété
    
      - Appartenance
    
      - Gestion de la remise des messages
    
      - Approbation de messages
    
      - Options de messagerie électronique
    
      - MailTip
    
      - Délégation de groupe

## Général

Utilisez cette section pour afficher ou modifier les informations de base relatives au groupe.

  - \* **Nom complet**   Ce nom s'affiche dans le carnet d'adresses, sur les lignes À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes. Le nom d'affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s'agit. Il doit également être unique dans votre domaine.

  - \* **Alias**   L’alias est la partie de l’adresse de messagerie qui apparaît à gauche du signe @. Si vous modifiez l’alias, l’adresse SMTP principale du groupe est également modifiée et contient le nouvel alias. De plus, l’adresse de messagerie électronique qui comprend l’alias précédent est gardée en tant qu’adresse de proxy du groupe.

  - **Description**   Décrivez le groupe afin que l’objet du groupe soit facilement identifiable. Cette description apparaît dans le carnet d’adresses et dans le volet d’informations du Centre d’administration Exchange.

  - **Masquer le groupe dans les listes d’adresses Exchange**   Cochez cette case si vous ne souhaitez pas que les utilisateurs voient ce groupe dans le carnet d’adresses. Pour envoyer un message électronique à ce groupe, l’expéditeur doit saisir l’alias ou l’adresse de messagerie électronique du groupe dans les lignes: ou Cc: À.

  - **Unité d’organisation**   Cette zone en lecture seule affiche l’unité d’organisation (UO) qui contient le groupe de distribution. Vous devez utiliser des utilisateurs et ordinateurs Active Directory pour déplacer le groupe dans une autre UO.

## Propriété

Utilisez cette section pour attribuer un propriétaire de groupe. Un groupe de distribution dynamique ne peut avoir qu’un seul propriétaire. Le propriétaire de groupe apparaît sous l’onglet **Géré par** de l’objet dans Utilisateurs et ordinateurs Active Directory.

Pour ajouter des propriétaires, cliquez sur **Parcourir**, puis sélectionnez le propriétaire dans la liste. Pour retirer le propriétaire, cliquez sur **Effacer**, puis sur **Enregistrer**.![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Appartenance

Utilisez cette section pour modifier les critères permettant de déterminer une appartenance au groupe. Vous pouvez supprimer ou modifier des règles d’appartenance existantes et ajouter de nouvelles règles. Pour voir savoir comment procéder, voir Utiliser l’EAC pour créer un groupe de distribution dynamique des procédures de configuration d’appartenance lorsque vous utilisez l’EAC pour créer un groupe de distribution dynamique.

## Gestion de la remise des messages

Cette section permet de gérer les utilisateurs autorisés à envoyer des messages électroniques à ce groupe.

  - **Uniquement les expéditeurs de mon organisation**   Sélectionnez cette option pour autoriser uniquement les expéditeurs de votre organisation à envoyer des messages au groupe. Cela signifie que si quelqu’un extérieur à votre organisation envoie un message électronique à ce groupe, celui-ci est rejeté. Il s’agit du paramètre par défaut.

  - **Expéditeurs internes et à l'extérieur de mon organisation**Sélectionnez cette option pour permettre à tout le monde d'envoyer des messages au groupe.
    
    Vous pouvez limiter davantage l’envoi de messages au groupe en permettant uniquement à des expéditeurs spécifiques d’envoyer des messages à ce groupe. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez au moins un destinataire. Si vous ajoutez des émetteurs à cette liste, ils seront les seuls à pouvoir envoyer des messages au groupe. Tout message envoyé par un expéditeur qui n’est pas répertorié dans la liste sera rejeté.
    
    Pour supprimer un individu ou un groupe de la liste, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous avez configuré le groupe pour autoriser uniquement des expéditeurs appartenant à votre organisation à envoyer des messages au groupe, un message électronique qui est envoyé par un contact de messagerie est alors rejeté, même si vous aviez ajouté ce contact à cette liste.</td>
    </tr>
    </tbody>
    </table>


## Approbation de messages

Cette section permet de définir les options de modération du groupe. Les modérateurs approuvent ou rejettent les messages envoyés au groupe avant qu'ils atteignent les membres du groupe.

  - **Les messages envoyés à ce groupe doivent être approuvés par un modérateur**   Cette case n’est pas cochée par défaut. Si vous activez cette case à cocher, les messages entrants sont examinés par les modérateurs de groupe avant leur remise. Les modérateurs de groupe peuvent approuver ou rejeter les messages entrants.

  - **Modérateurs de communauté**   Pour ajouter des modérateurs de groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un modérateur, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"). Si vous avez coché la case « Les messages envoyés à ce groupe doivent être approuvés par un modérateur » sans sélectionner de modérateur, les messages destinés au groupe sont envoyés aux propriétaires du groupe pour approbation.

  - **Les expéditeurs qui ne demandent pas l’approbation de messages**    Pour ajouter des individus ou des groupes non soumis à la modération pour ce groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un individu ou un groupe, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Sélectionner les notifications de modération**   Cette section permet de définir la manière dont les utilisateurs sont informés de l'approbation de messages.
    
      - **Avertir tous les expéditeurs lorsque leurs messages ne sont pas approuvés**   Il s’agit du paramètre par défaut. Permet de notifier tous les expéditeurs, à l'intérieur et à l'extérieur de votre organisation, lorsque leur message n'est pas approuvé.
    
      - **Avertir les expéditeurs de votre organisation uniquement lorsque leurs messages ne sont pas approuvés**   Lorsque vous activez cette option, seuls les personnes ou les groupes de votre organisation sont informés lorsqu’un message qu’ils ont envoyé au groupe n’est pas approuvé par un modérateur.
    
      - **N’avertir personne lorsqu’un message n’est pas approuvé**   Lorsque vous activez cette option, aucune notification n’est envoyée aux expéditeurs dont les messages sont rejetés par les modérateurs de groupe.

## Options de messagerie électronique

Cette section permet d’afficher ou de modifier les adresses de messagerie électronique associées au groupe. Adresses incluses : adresses SMTP principales du groupe et toute adresse de proxy associée. L’adresse SMTP principale (aussi appelée *adresse de réponse*) apparaît en gras dans la liste d’adresses, avec la valeur **SMTP** inscrite en majuscules dans la colonne **Type**.

  - **Ajouter**  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l’un des types d’adresses suivants :
    
      - **SMTP**   Il s’agit du type d’adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone \* **Adresse de messagerie**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Pour que la nouvelle adresse devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>.</td>
        </tr>
        </tbody>
        </table>
    
      - **Adresse personnalisée**   Cliquez sur ce bouton et saisissez dans la zone \* **Adresse de messagerie** l’un des types d’adresse de messagerie électronique non SMTP pris en charge.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>À l’exception des adresses X.400, Exchange ne valide pas la mise en forme des adresses personnalisées. Vous devez veiller à ce que l’adresse personnalisée que vous spécifiez soit conforme aux exigences de mise en forme pour ce type d’adresse.</td>
        </tr>
        </tbody>
        </table>


  - **Modifier**   Pour modifier une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour que l’adresse existante devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>.</td>
    </tr>
    </tbody>
    </table>


  - **Supprimer**   Pour supprimer une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Mettre à jour auto. les adresses selon la stratégie de destinataire**   Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d’adresses de messagerie dans votre organisation. Cette case à cocher est activée par défaut.

## MailTip

Utilisez cette section pour ajouter une info courrier afin d’alerter les utilisateurs de problèmes potentiels avant qu’ils envoient un message à ce groupe. Une info courrier est un texte affiché dans la barre d’informations lorsque ce groupe est ajouté aux lignes À, Cc ou Cci d’un nouveau message électronique. Par exemple, vous pourriez ajouter une info courrier aux grands groupes pour prévenir des expéditeurs potentiels que leur message sera envoyé à beaucoup de personnes.

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


## Délégation de groupe

Cette section permet d’attribuer des autorisations à un utilisateur (appelé *délégué*) pour lui permettre d’envoyer des messages en tant que groupe ou de la part du groupe. Vous pouvez attribuer les autorisations suivantes :

  - **Envoyer en tant que**   Cette autorisation permet au délégué d’envoyer des messages en tant que groupe. Une fois cette autorisation attribuée, le délégué a la possibilité d’ajouter le groupe dans la ligne **De** pour indiquer que le message a été envoyé par le groupe.

  - **Envoyer de la part de**   Cette autorisation permet également au délégué d’envoyer des messages au nom du groupe. Une fois l’autorisation attribuée, le délégué peut ajouter le groupe sur la ligne **De**. Le message apparaîtra comme ayant été envoyé par le groupe et indiquera qu’il a été envoyé par le délégué au nom du groupe.

Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter** sous l’autorisation voulue afin d’afficher la page **Sélectionner un destinataire** qui présente une liste de tous les destinataires de votre organisation Exchange auxquels peut être attribuée l’autorisation. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Il est également possible de rechercher un destinataire spécifique en saisissant son nom dans le champ de recherche, puis en cliquant sur **Rechercher**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier les propriétés du groupe de distribution dynamique

Utilisez les cmdlets **Get-DynamicDistributionGroup** et **Set-DynamicDistributionGroup** pour afficher et modifier les propriétés pour les groupes de distribution dynamique. L’utilisation de l’environnement Shell offre les avantages de pouvoir modifier les propriétés qui ne sont pas accessibles dans l’EAC et de modifier des propriétés pour plusieurs groupes. Pour plus d’informations sur les paramètres qui correspondent aux propriétés du groupe de distribution, consultez les rubriques suivantes :

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/fr-fr/library/bb123796\(v=exchg.150\))

Voici quelques exemples d’utilisation de l’environnement Shell pour modifier des propriétés du groupe de distribution dynamique.

Dans cet exemple, nous modifions les paramètres suivants pour tous les groupes de distribution dynamique de l’organisation :

  - Masquer tous les groupes de distribution dynamique à partir du carnet d’adresses

  - Définir à 5 Mo la taille de message maximale qui peut être envoyée au groupe

  - Activer la modération

  - Désigner l’administrateur comme le modérateur du groupe

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

Dans cet exemple, nous ajoutons l’adresse de messagerie proxy SMTP, Seattle.Employees@contoso.com, au groupe Tous les employés.

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que la modification des propriétés pour un groupe de distribution dynamique s’est correctement effectuée, procédez comme suit :

  - Dans le Centre d’administration Exchange, sélectionnez le groupe et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonction que vous avez modifiée. En fonction de la propriété modifiée, cette dernière peut s’afficher dans le volet d’informations du groupe sélectionné.

  - Dans l’environnement Shell, utilisez la cmdlet **Get-DynamicDistributionGroup** pour vérifier les modifications. En utilisant l’environnement de ligne de commande Exchange Management Shell, vous avez l’avantage de pouvoir afficher plusieurs propriétés de plusieurs groupes. Dans le premier exemple, vous devez exécuter la commande suivante pour vérifier les nouvelles valeurs.
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    Dans l’exemple ci-dessus où les limites de message ont été modifiées, exécutez cette commande.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

