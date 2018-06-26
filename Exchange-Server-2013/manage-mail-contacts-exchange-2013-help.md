---
title: 'Gérer les contacts de messagerie: Exchange 2013 Help'
TOCTitle: Gérer les contacts de messagerie
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50477272
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: HT
---

# Gérer les contacts de messagerie

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-10-04_

Les contacts de messagerie sont des objets de service d'annuaire à extension messagerie qui contiennent des informations sur les personnes ou les organisations qui existent en dehors de votre organisation Exchange ou Exchange Online. Chaque contact de messagerie dispose d'une adresse de messagerie externe. Pour plus d'informations sur les contacts de messagerie, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

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

## Créer un contact de messagerie

## Utiliser le Centre d'administration Exchange (CAE) pour créer un contact de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") \> **Contact de messagerie**.

3.  Renseignez les zones suivantes de la page **Nouveau contact de messagerie** :
    
      - **Prénom   **Cette zone permet de modifier le prénom du contact.
    
      - **Initiales  **Cette zone permet de modifier les initiales du deuxième prénom du contact.
    
      - **Nom de famille  **Cette zone permet de modifier le nom de famille du contact.
    
      - **\* Nom complet**   Cette zone permet de saisir un nom complet pour le contact. Il s'agit du nom qui est répertorié dans la liste de contacts du CAE et dans le carnet d'adresses de votre organisation. Par défaut, ce champ est renseigné avec les noms que vous avez entrés dans les champs **Prénom**, **Initiales** et **Nom de famille**. Si vous n'avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Le nom ne peut pas comporter plus de 64 caractères.
    
      - **\* Nom**   Cette zone permet de saisir un nom pour le contact. Il s'agit du nom répertorié dans le service d'annuaire. Comme le nom complet, cette zone est renseignée par défaut avec les noms que vous entrez dans les zones **Prénom**, **Initiales** et **Nom de famille**. Si vous n'avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Le nom ne peut pas comporter plus de 64 caractères.
    
      - **\* Alias   **Cette zone permet de saisir l’alias (64 caractères maximum) du contact. Ce champ est obligatoire.
    
      - **\* adresse de messagerie externe**   Cette zone permet de saisir le compte de messagerie externe du contact. Ce champ est obligatoire. Les messages électroniques envoyés à ce contact sont transférés vers cette adresse de messagerie.
    
      - **Unité d'organisation**   Vous pouvez sélectionner une unité d'organisation autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine qui contient l'ordinateur sur lequel le Centre d'administration Exchange est en cours d'exécution. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d'organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d'organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez l'UO souhaitée, puis cliquez sur **OK**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>La zone <strong>Unité d'organisation</strong> est disponible uniquement dans Exchange Server 2013. Elle ne l'est pas dans Exchange Online.</td>
        </tr>
        </tbody>
        </table>


4.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser le shell pour créer un contact de messagerie

Cet exemple montre comment créer un contact de messagerie pour Debra Garcia dans Exchange Server 2013.

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

Cet exemple montre comment créer un contact de messagerie pour Alan Shen dans Exchange Online.

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

Cet exemple montre comment activer la messagerie pour un contact existant nommé Karen Toh dans Exchange Server 2013.

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé un contact de messagerie, procédez de l’une des façons suivantes :

  - Dans le CAE, accédez à **Destinataires**  \> **Contacts**. La nouveau contact de messagerie apparaît dans la liste de contacts. Sous **Type de contact**, le type est **Contact de messagerie**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations sur le nouveau contact de messagerie.
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Modifier les propriétés d'un contact de messagerie

## Utiliser le Centre d'administration Exchange (CAE) pour modifier les propriétés d'un contact de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste des contacts de messagerie et des utilisateurs de messagerie, cliquez sur le contact de messagerie dont vous souhaitez modifier les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  dans la page des propriétés des contacts de messagerie, cliquez sur l'une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Informations sur le contact
    
      - Organisation
    
      - Options de messagerie électronique (non disponible dans Exchange Online)
    
      - Infos-courrier

## Général

Dans la section **Général**, vous pouvez afficher ou modifier des informations de base sur le contact de messagerie.

  - **Prénom**, **Initiales**, **Nom de famille**

  - **\* Nom**   Il s'agit du nom qui s'affiche dans Active Directory. Si vous modifiez ce nom, il ne peut pas comporter plus de 64 caractères.

  - **\* Nom complet**   Ce nom s'affiche dans le carnet d'adresses de votre organisation, sur les lignes À et De du message électronique, ainsi que dans la liste des boîtes aux lettres. Ce nom ne peut pas contenir d'espaces vides avant ou après le nom complet.

  - **\* Alias**   Alias du contact de messagerie. Si vous le modifiez, il doit être unique dans l'organisation et ne doit pas contenir plus de 64 caractères.

  - **\* adresse de messagerie externe**   Adresse SMTP principale et compte de messagerie externe du contact de messagerie. Les messages électroniques envoyés à ce contact sont transférés vers cette adresse de messagerie.

  - Cliquez sur **Plus d'options** pour afficher l'unité d'organisation qui contient le compte de contact de messagerie. Vous devez utiliser les Utilisateurs et ordinateurs Active Directory pour déplacer le contact vers une autre unité d'organisation.

## Informations sur le contact

Utilisez la section **Informations sur le contact** pour afficher ou modifier les informations de contact du destinataire, telles que l'adresse postale et les numéros de téléphone. Ces informations s'affichent dans le carnet d'adresses.

## Organisation

La section **Organisation** permet d'enregistrer des informations détaillées sur le rôle du contact de messagerie dans l'organisation. Ces informations s'affichent dans le carnet d'adresses. Aussi, vous pouvez créer un organigramme virtuel accessible à partir de clients de messagerie, tels qu'Outlook.

  - **Titre**   Cette zone permet d’afficher ou de modifier le titre du contact.

  - **Service**   Cette zone permet d'afficher ou de modifier le service dans lequel le contact travaille. Vous pouvez utiliser cette zone afin de créer des conditions de destinataire pour des groupes de distribution dynamique et des listes d'adresses.

  - **Société**   Cette zone permet d'afficher ou de modifier la société pour laquelle le contact travaille. Vous pouvez aussi utiliser cette zone afin de créer des conditions de destinataire pour des groupes de distribution dynamique.

  - **Gestionnaire**   Pour ajouter un gestionnaire, cliquez sur **Parcourir**. Dans **Sélectionner le gestionnaire**, sélectionnez une personne, puis cliquez sur **OK**.

  - **Collaborateurs**   Vous ne pouvez pas modifier ce champ. Un *collaborateur direct* est un destinataire qui dépend d'un responsable spécifique. Si vous avez indiqué un responsable pour le destinataire, ce dernier apparaît en tant que collaborateur direct dans les informations relatives à la boîte aux lettres du responsable. Par exemple, Toby gère Ann et Spencer, qui sont des contacts de messagerie. Toby est donc spécifié dans la zone **Responsable** des propriétés de l'organisation pour Ann et Spencer, et Ann et Spencer apparaissent dans la zone **Collaborateurs directs** des propriétés de boîte aux lettres de Toby.

## Options de messagerie électronique

Utilisez la section **Options de messagerie électronique** pour ajouter ou supprimer des adresses de proxy pour le contact de messagerie ou pour modifier des adresses de proxy existantes. L'adresse SMTP principale du contact de messagerie s'affiche également dans cette section, mais vous ne pouvez pas la modifier. Pour la modifier, vous devez changer l'adresse de messagerie externe du contact dans la section **Général**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La section <strong>Options de messagerie électronique</strong> est disponible uniquement dans Exchange Server 2013. Elle ne l'est pas dans Exchange Online.</td>
</tr>
</tbody>
</table>


## Infos-courrier

Dans la section **Info-courrier**, vous pouvez ajouter une info-courrier pour alerter les utilisateurs d'éventuels problèmes avant qu'ils n'envoient un message à ce destinataire. Une info-courrier est un texte qui s’affiche dans la barre d’informations lorsque ce destinataire est ajouté aux champs À, Cc ou Cci d’un nouveau message électronique.

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les propriétés d'un contact de messagerie

Les propriétés d'un contact de messagerie sont stockées dans Active Directory et Exchange. En général, vous pouvez utiliser les cmdlets **Get-Contact** et **Set-Contact** pour afficher et modifier les propriétés de l'organisation et des informations de contact. Utilisez les cmdlets **Get-MailContact** et **Set-MailContact** pour afficher ou modifier les propriétés de messagerie, comme les adresses électroniques, les infos-courrier et les attributs personnalisés, mais aussi pour spécifier si le contact doit être masqué dans les listes d'adresses.

Pour plus d'informations, consultez les rubriques suivantes :

  - [Get-Contact](https://technet.microsoft.com/fr-fr/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/fr-fr/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/fr-fr/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/fr-fr/library/aa995950\(v=exchg.150\))

Voici quelques exemples d'utilisation de l'environnement de ligne de commande Exchange Management Shell pour la modification des propriétés d'un contact de messagerie.

Cet exemple montre comment configurer les propriétés Titre, Service, Société et Responsable du contact de messagerie Kai Axford.

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

Cet exemple montre comment définir la propriété CustomAttribute1 sur la valeur PartTime pour tous les contacts de messagerie, et les masque dans le carnet d’adresses de l’organisation.

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

Cet exemple montre comment définir la propriété CustomAttribute15 sur la valeur TemporaryEmployee pour tous les contacts de messagerie dans le service Relations publiques.

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement modifié les propriétés du contact de messagerie, procédez comme suit :

  - Dans le CAE, sélectionnez le contact de messagerie puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété modifiée.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez les cmdlets **Get-Contact** et **Get-MailContact** pour vérifier les modifications. L'environnement de ligne de commande Exchange Management Shell a pour avantage de permettre l'affichage de plusieurs propriétés pour divers contacts de messagerie. Dans l'exemple ci-dessus, où la propriété CustomAttribute1 a été définie sur PartTime pour tous les contacts de messagerie et où ces derniers ont été masqués dans le carnet d'adresses, exécutez la commande suivante pour vérifier les modifications.
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    Dans l'exemple ci-dessus, où la propriété CustomAttribute15 a été définie pour tous les contacts de messagerie du service Relations publiques, exécutez la commande suivante pour vérifier les modifications.
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## Modifier en bloc les contacts de messagerie

Vous pouvez utiliser le CAE pour modifier les propriétés sélectionnées de plusieurs contacts de messagerie. Lorsque vous sélectionnez au moins deux contacts de messagerie dans la liste de contacts du CAE, les propriétés pouvant être modifiées en bloc apparaissent dans le volet d'informations. Lorsque vous modifiez l'une de ces propriétés, la modification est appliquée à tous les destinataires sélectionnés.

Lorsque vous modifiez en bloc des contacts de messagerie, vous pouvez modifier les zones de propriétés suivantes :

  - **Informations de contact**   Permet de modifier des propriétés communes, telles que la rue, le code postal et le nom de la ville.

  - **Organisation**   Permet de modifier des propriétés communes, telles que le nom du service, le nom de la société et le nom du responsable auquel les contacts de messagerie ou les utilisateurs de messagerie sélectionnés rendent compte.

## Utiliser le CAE pour modifier en bloc des contacts de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste de contacts, sélectionnez au moins deux contacts de messagerie. Vous ne pouvez pas modifier en bloc une combinaison de contacts de messagerie et d’utilisateurs de messagerie.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous pouvez sélectionner plusieurs contacts de messagerie adjacents en maintenant la touche Maj enfoncée et en cliquant sur le premier puis le dernier contact à modifier. Vous pouvez aussi sélectionner plusieurs contacts de messagerie en maintenant la touche Ctrl enfoncée, puis en cliquant sur chacun des contacts à modifier.</td>
    </tr>
    </tbody>
    </table>


3.  Dans le volet Détails, sous **Modification en bloc**, cliquez sur **Mettre à jour** sous **Informations de contact** ou **Organisation**.

4.  Apportez les modifications souhaitées dans la page Propriétés, puis enregistrez-les.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement modifié en bloc des contacts de messagerie, procédez de l’une des manières suivantes :

  - Dans le CAE, sélectionnez chacun des contacts de messagerie modifiés en bloc, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher les propriétés modifiées.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Get-Contact** pour vérifier les modifications. Par exemple, supposons que vous ayez utilisé la fonction de modification en bloc dans le CAE pour modifier le responsable et le bureau de tous les contacts de messagerie d'un fournisseur appelé A. Datum Corporation. Pour vérifier ces modifications, vous pouvez exécuter la commande suivante dans l'environnement de ligne de commande Exchange Management Shell.
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icône rapide pour LinkedIn Learning" alt="Icône rapide pour LinkedIn Learning" /> <strong>Vous débutez avec Office 365 ?</strong><br />
Découvrez les cours vidéo gratuits pour <a href="https://support.office.com/fr-fr/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> proposés par LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

