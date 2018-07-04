---
title: 'Gérer les utilisateurs de messagerie: Exchange 2013 Help'
TOCTitle: Gérer les utilisateurs de messagerie
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 50477377
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: HT
---

# Gérer les utilisateurs de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les utilisateurs de messagerie sont semblables aux contacts de messagerie. Tous deux disposent d'adresses de messagerie externes, contiennent des informations sur des personnes extérieures à votre organisation Exchange ou Exchange Online et peuvent être affichés dans le carnet d'adresses partagé et d'autres listes d'adresses. Toutefois, contrairement à un contact de messagerie, un utilisateur de messagerie dispose d'informations d'identification d'ouverture de session dans votre organisation Exchange ou Office 365 et peut accéder à des ressources. Pour plus d'informations, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Créer un utilisateur de messagerie

## Utiliser le CAE pour créer un utilisateur de messagerie

1.  Dans le Centre d'administration Exchange (CAE), cliquez sur **Destinataires** \> **Contacts** \> **Nouveau** \> **Utilisateur de messagerie**.

2.  Dans la page **Nouvel utilisateur de messagerie**, dans le champ \* **Alias**, saisissez l'alias de l'utilisateur de messagerie. L'alias ne peut pas comporter plus de 64 caractères et doit être unique dans la forêt. Ce champ est obligatoire.

3.  Choisissez l'une des procédures suivantes pour indiquer le type d'adresse de messagerie de l'utilisateur de messagerie :
    
      - Pour indiquer une adresse de messagerie SMTP comme adresse de messagerie externe de l’utilisateur de messagerie, cliquez sur **SMTP**.
        
        > [!NOTE]
        > Exchange vérifie que le format des adresses SMTP est correct. Si votre entrée n'est pas cohérente avec le format SMTP, un message d'erreur s'affiche lorsque vous cliquez sur <strong>Enregistrer</strong> pour créer l'utilisateur de messagerie.
    
      - Pour indiquer un type d'adresse personnalisé, cliquez sur la case d'option et saisissez le type d'adresse personnalisé. Par exemple, vous pouvez indiquer une adresse X.500, GroupWise ou Lotus Notes.

4.  Dans le champ \* **Adresse de messagerie externe**, saisissez l’adresse de messagerie externe de l’utilisateur de messagerie. Les messages électroniques envoyés à ce contact sont transférés à cette adresse de messagerie. Ce champ est obligatoire.

5.      
    Activez l'une des options suivantes :
    
      - **Utilisateur existant**   Activez cette option pour activer la messagerie d'un utilisateur existant.
        
        Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un utilisateur – Forêt entière**. Cette boîte de dialogue affiche la liste des comptes d'utilisateur de l'organisation qui ne sont pas à extension messagerie ou qui n'ont pas de boîte aux lettres. Sélectionnez le compte d'utilisateur pour lequel vous souhaitez activer la messagerie, puis cliquez sur **OK**. Si vous sélectionnez cette option, il n’est pas nécessaire de saisir les informations du compte d’utilisateur puisque ces dernières existent déjà dans Active Directory.
    
      - **Nouvel utilisateur**   Activez cette option pour créer un compte d'utilisateur dans Active Directory et pour activer la messagerie de l'utilisateur. Si vous activez cette option, vous devrez saisir les informations de compte d'utilisateur requises.

6.      
    Si vous avez sélectionné **Nouvel utilisateur** à l'étape 5, complétez les champs suivants dans la page **Nouvel utilisateur de messagerie**. Sinon, passez à l'étape 7.
    
      - **Prénom**   Ce champ permet d'entrer le prénom de l'utilisateur de messagerie.
    
      - **Initiales**   Ce champ permet d'entrer les initiales de l'utilisateur de messagerie.
    
      - **Nom**   Ce champ permet d'entrer le nom de famille de l'utilisateur de messagerie.
    
      - **\*Nom complet**   Ce champ permet de saisir un nom complet pour l'utilisateur. Il s’agit du nom qui est répertorié dans la liste des contacts dans le CAE et le carnet d’adresses de votre organisation. Par défaut, ce champ est renseigné avec les noms que vous avez entrés dans les champs **Prénom**, **Initiales** et **Nom de famille**. Si vous n’avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Le nom ne peut pas comporter plus de 64 caractères.
    
      - \* **Nom**   Ce champ permet de saisir un nom pour l'utilisateur de messagerie. Il s'agit du nom répertorié dans le service d'annuaire. Ce champ est également renseigné avec les noms que vous avez entrés dans les champs **Prénom**, **Initiales** et **Nom de famille**. Si vous n'avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Ce nom ne peut pas comporter plus de 64 caractères.
        
        > [!NOTE]
        > La zone <strong>Nom</strong> est disponible uniquement dans Exchange Server 2013. Elle ne l'est pas dans Exchange Online.
    
      - **Unité d'organisation**   Vous pouvez sélectionner une unité d'organisation (UO) autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine qui contient l'ordinateur sur lequel le CAE est en cours d'exécution. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d'organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d'organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez l'UO souhaitée, puis cliquez sur **OK**.
        
        > [!NOTE]
        > La zone <strong>Unité d'organisation</strong> est disponible uniquement dans Exchange Server 2013. Elle ne l'est pas dans Exchange Online.
    
      - \* **Nom d'ouverture de session de l'utilisateur**   Ce champ permet d'entrer le nom que l'utilisateur de messagerie utilisera pour ouvrir une session sur le domaine. Le nom d'ouverture de session de l'utilisateur est constitué du nom d'utilisateur à gauche du symbole (@) et d'un suffixe à droite. Généralement, le suffixe est le nom du domaine dans lequel le compte d'utilisateur réside.
        
        > [!NOTE]
        > Dans Exchange Online, cette zone est appelée <strong>Identifiant utilisateur</strong>.
    
      - \* **Nouveau mot de passe**   Ce champ permet de saisir le mot de passe que l'utilisateur de messagerie doit utiliser pour ouvrir une session sur le domaine.
        
        > [!NOTE]
        > Assurez-vous que le mot de passe entré est conforme aux exigences de longueur, de complexité et d’historique du domaine dans lequel vous créez le compte d’utilisateur.
    
      - \* **Confirmer le mot de passe**   Ce champ permet de confirmer le mot de passe que vous avez saisi dans le champ **Mot de passe**.
    
      - **Exiger la modification du mot de passe à la prochaine ouverture de session**   Cochez cette case si vous souhaitez que les utilisateurs de messagerie réinitialisent le mot de passe avec lequel ils se sont initialement connectés au domaine.
        
        Si vous cochez cette case, une boîte de dialogue invitera le nouvel utilisateur de messagerie à modifier son mot de passe lors de sa première ouverture de session. L'utilisateur de messagerie ne sera autorisé à effectuer aucune tâche tant que le mot de passe n'aura pas été modifié.

7. Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer l'utilisateur de messagerie.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un utilisateur de messagerie

Dans cet exemple, un compte d'utilisateur à extension messagerie est créé dans Exchange Server 2013 pour l'utilisateur Jeffrey Zeng, avec les informations suivantes :

  - Le nom et le nom complet sont Jeffrey Zeng.

  - L'alias est jeffreyz.

  - L'adresse de messagerie externe est jzeng@tailspintoys.com.

  - Le prénom est Jeffrey et le nom est Zeng.

  - Le nom d'ouverture de session de l'utilisateur est jeffreyz@contoso.com.

  - Le mot de passe est Pa$$word1.

  - L'utilisateur de messagerie sera créé dans l'unité d'organisation par défaut. Pour spécifier un autre UO, utilisez le paramètre *OrganizationalUnit*.

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

Cet exemple crée un compte d'utilisateur à extension messagerie pour Rene Valdes dans Exchange Online.

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## Comment savoir si cela a fonctionné ?

Pour vérifier la création d’un utilisateur de messagerie, procédez comme suit :

  - Dans le CAE, accédez à **Destinataires**  \> **Contacts**. Le nouvel utilisateur de messagerie s'affiche dans la liste de contacts. Sous **Type de contact**, le type est **Utilisateur de messagerie**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations relatives au nouvel utilisateur de messagerie.
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Modifier les propriétés d'un utilisateur de messagerie

Après avoir créé un utilisateur de messagerie, vous pouvez y apporter des modifications et définir des propriétés supplémentaires via le CAE ou l'environnement de ligne de commande Exchange Management Shell.

Vous pouvez également modifier les propriétés de plusieurs boîtes aux lettres utilisateur en même temps. Pour plus d'informations, consultez la rubrique Utiliser le CAE pour modifier en bloc des utilisateurs de messagerie.

La durée d'exécution estimée pour cette tâche varie selon le nombre de propriétés que vous souhaitez afficher ou modifier.

## Utiliser le CAE pour modifier les propriétés des boîtes aux lettres utilisateur

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste de contacts, cliquez sur l'utilisateur de messagerie dont vous voulez modifier les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés de l'utilisateur de messagerie, cliquez sur l'une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Informations sur le contact
    
      - Organisation
    
      - Adresses électroniques
    
      - Paramètres du flux de messagerie
    
      - Membre de
    
      - Infos-courrier

## Général

Dans la section **Général**, vous pouvez afficher ou modifier des informations de base sur l'utilisateur de messagerie.

  - **Prénom**, **Initiales**, **Nom de famille**

  - \* **Nom**   Il s'agit du nom qui s'affiche dans Active Directory. Si vous modifiez ce nom, il ne peut pas comporter plus de 64 caractères.

  - \* **Nom complet**    Ce nom s’affiche dans le carnet d’adresses de l’organisation, sur les lignes À : et De : dans le message électronique et dans la liste des contacts au sein du CAE. Ce nom ne peut pas contenir d’espaces vides avant ou après le nom complet.

  - \* **Nom d'ouverture de session de l'utilisateur**   Nom que l'utilisateur utilise pour ouvrir une session dans le domaine. Dans Exchange Online, il s'agit de l'identifiant utilisateur utilisé pour se connecter à Office 365.

  - **Masquer dans les listes d'adresses**   Cochez cette case pour empêcher que l'utilisateur de messagerie n'apparaisse dans le carnet d'adresses et dans d'autres listes d'adresses définies dans votre organisation Exchange. Après activation de cette case à cocher, les utilisateurs peuvent encore envoyer des messages au destinataire en utilisant l'adresse de messagerie.

  - **Exiger la modification du mot de passe à la prochaine ouverture de session**   Cochez cette case si vous souhaitez que l'utilisateur réinitialise son mot de passe lors de sa prochaine ouverture de session dans le domaine.
    
    > [!NOTE]
    > Ce champ n'est pas disponible dans Exchange Online.


Cliquez sur **Plus d'options** pour afficher ou modifier les propriétés supplémentaires suivantes :

  - **Unité d'organisation**   Ce champ en lecture seule affiche l'unité d'organisation (UO) qui contient le compte d'utilisateur de messagerie. Vous devez utiliser des Utilisateurs et ordinateurs Active Directory pour déplacer le compte vers un autre UO.
    
    > [!NOTE]
    > Ce champ n'est pas disponible dans Exchange Online.


  - **Attributs personnalisés**   Cette section affiche les attributs personnalisés définis pour l'utilisateur de messagerie. Pour spécifier des valeurs d'attribut personnalisées, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Vous pouvez spécifier jusqu'à 15 attributs personnalisés pour le destinataire.

## Informations sur le contact

Utilisez la section **Coordonnées** pour afficher ou modifier les coordonnées de l'utilisateur. L'information sur cette page s'affiche dans le carnet d'adresses. Cliquez sur **Plus d'options** pour afficher des boîtes de dialogue supplémentaires.

> [!TIP]
> Le champ <strong>État/Province</strong> permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie ou des listes d'adresses.


## Organisation

La section **Organisation** permet d'enregistrer des informations détaillées sur le rôle de l'utilisateur dans l'organisation. Ces informations s'affichent dans le carnet d'adresses. Aussi, vous pouvez créer un organigramme virtuel accessible à partir de clients de messagerie, tels qu’Outlook.

  - **Titre** Cette zone permet d'afficher ou de modifier le titre du destinataire.

  - **Service**   Cette zone permet d'afficher ou de modifier le service dans lequel l'utilisateur travaille. Ce champ permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie ou des listes d'adresses.

  - **Société**   Cette zone permet d'afficher ou de modifier la société pour laquelle l'utilisateur travaille. Ce champ permet de créer des conditions de destinataire pour des groupes de distribution dynamiques, des stratégies d'adresse de messagerie électronique ou des listes d'adresses.

  - **Gestionnaire**   Pour ajouter un gestionnaire, cliquez sur **Parcourir**. Dans **Sélectionner le gestionnaire**, sélectionnez une personne, puis cliquez sur **OK**.

  - **Collaborateurs**   Vous ne pouvez pas modifier ce champ. Un *collaborateur* est un utilisateur qui dépend d'un responsable spécifique. Si vous avez indiqué un responsable pour l’utilisateur, ce dernier apparaît en tant que collaborateur dans les informations détaillées relatives à la boîte aux lettres du responsable. Par exemple, Kari gère Chris et Kate, donc Kari est indiquée dans le champ **Responsable** pour Chris et Kate, et Chris et Kate apparaissent dans le champ **Collaborateurs** dans les propriétés du compte de Kari.

## Adresses électroniques

La section **Adresses de messagerie** permet d'afficher ou de modifier les adresses de messagerie associées à l'utilisateur de messagerie. Cela inclut l’adresse SMTP principale de l’utilisateur de messagerie, son adresse de messagerie externe et toutes les adresses proxy associées. L'adresse SMTP principale (également appelée *adresse de réponse par défaut*) est affichée en gras dans la liste d'adresses, la valeur **SMTP** apparaissant en lettres majuscules dans la colonne **Type**. Par défaut, une fois l'utilisateur de messagerie créé, l'adresse SMTP principale et l'adresse de messagerie externe sont les mêmes.

  - **Ajouter**  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l'un des types d'adresses suivants :
    
      - **SMTP**   Il s'agit du type d'adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone \* **Adresse de messagerie**.
    
      - **Adresse personnalisée**   Cliquez sur ce bouton et saisissez dans la zone \* **Adresse de messagerie** l'un des types d'adresse de messagerie électronique non SMTP pris en charge.
        
        > [!NOTE]
        > À l'exception des adresses X.400, Exchange ne valide pas la mise en forme des adresses personnalisées. Vous devez veiller à ce que l'adresse personnalisée que vous spécifiez soit conforme aux exigences de mise en forme pour ce type d'adresse.


  - **Définir comme adresse de messagerie externe**   Ce champ permet de modifier l’adresse externe de l’utilisateur de messagerie. Les messages électroniques envoyés à ce contact sont transférés à cette adresse de messagerie.

  - **Mettre à jour auto. les adresses selon la stratégie de destinataire**   Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d'adresse de messagerie dans votre organisation. Cette case à cocher est activée par défaut.
    
    > [!NOTE]
    > Cette option n'est pas disponible dans Exchange Online.


## Paramètres du flux de messagerie

La section **Paramètres du flux de messagerie** permet d'afficher ou de modifier les paramètres suivants :

  - **Restrictions de taille des messages**   Ces paramètres permettent de contrôler la taille des messages échangés par l'utilisateur de messagerie. Cliquez sur **Afficher les détails** pour afficher et modifier la taille maximale des messages échangés.
    
      - **Messages envoyés**   Pour spécifier une taille maximale de messages envoyés par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l'utilisateur envoie un message dont la taille est supérieure à la taille spécifiée, il est renvoyé à l'utilisateur avec un message d'erreur descriptif.
    
      - **Messages reçus**   Pour spécifier une taille maximale de messages reçus par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l'utilisateur reçoit un message dont la taille est supérieure à la taille spécifiée, le message sera renvoyé à l'expéditeur accompagné d'un message de description de l'erreur.

  - **Restrictions de remise des messages**   Ces paramètres permettent de contrôler les expéditeurs possibles des messages électroniques envoyés à un utilisateur de messagerie. Cliquez sur **Afficher les détails** pour afficher et modifier ces restrictions.
    
      - **Accepter les messages provenant de**   Cette section permet de spécifier qui peut envoyer des messages à cet utilisateur.
        
          - **Tous les expéditeurs**   Cette option permet d'indiquer que l'utilisateur peut accepter des messages de tous les expéditeurs. Sont inclus à la fois les expéditeurs de votre organisation Exchange et les expéditeurs externes. Cette option est sélectionnée par défaut. Cette option inclut les utilisateurs externes uniquement si vous désactivez la case à cocher **Exiger l'authentification de tous les expéditeurs**. Si cette case à cocher est activée, les messages des utilisateurs externes seront rejetés.
        
          - **Uniquement les expéditeurs de la liste suivante** Cette option permet d'indiquer que l'utilisateur ne peut accepter que les messages provenant d'un ensemble spécifique d'expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour afficher la page **Sélectionner des destinataires**, dans laquelle s'affiche la liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher** ![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").
        
          - **Exiger l'authentification de tous les expéditeurs**   Cette option permet d'empêcher les utilisateurs anonymes d'envoyer des messages à l'utilisateur.
    
      - **Rejeter les messages de**   Cette section permet d'empêcher des personnes d'envoyer des messages à cet utilisateur.
        
          - **Aucun expéditeur**   Cette option permet d’indiquer que la boîte aux lettres ne rejettera les messages d’aucun expéditeur de l’organisation Exchange. Cette option est sélectionnée par défaut.
        
          - **Expéditeurs de la liste suivante** Cette option permet d'indiquer que la boîte aux lettres rejettera les messages provenant d'un ensemble spécifique d'expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour afficher la page **Sélectionner des destinataires**, dans laquelle s'affiche la liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher** ![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").

## Membre de

La section **Membre de** permet d'afficher une liste des groupes de distribution ou de groupes de sécurité auxquels cet utilisateur appartient. Vous ne pouvez pas modifier les informations d'appartenance sur cette page. Notez que l'utilisateur peut répondre aux critères d'un ou de plusieurs groupes de distribution dynamiques de votre organisation. Toutefois, les groupes de distribution dynamiques ne s’affichent pas sur cette page, car leur appartenance est calculée à chaque utilisation.

## Infos-courrier

Dans la section **Info-courrier**, vous pouvez ajouter une info-courrier pour alerter les utilisateurs d'éventuels problèmes avant qu'ils n'envoient un message à ce destinataire. Une info-courrier est un texte qui s’affiche dans la barre d’informations lorsque ce destinataire est ajouté aux champs À, Cc ou Cci d’un nouveau message électronique.

> [!NOTE]
> Les infos courrier peuvent comporter des balises HTML, mais les scripts ne sont pas autorisés. Une info courrier personnalisée ne doit pas comporter plus de 175 caractères affichés. Les balises HTML ne sont pas prises en compte dans cette limite.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier les propriétés de l'utilisateur de messagerie

Les propriétés d'un utilisateur de messagerie sont stockées dans Active Directory et Exchange. En général, utilisez les cmdlets **Get-User** et **Set-User** pour afficher et modifier des propriétés d'informations sur des organisations et des contacts. Utilisez les cmdlets **Get-MailUser** et **Set-MailUser** pour afficher ou modifier des propriétés liées à la messagerie, comme les adresses de messagerie, les infos courrier, les attributs personnalisés et l'option de masquage de l'utilisateur de messagerie dans les listes d'adresses.

Utilisez les cmdlets **Get-MailUser** et **Set-MailUser** pour afficher et modifier des propriétés des utilisateurs de messagerie. Pour plus d'informations, consultez les rubriques suivantes :

  - [Get-User](https://technet.microsoft.com/fr-fr/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/fr-fr/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/fr-fr/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/fr-fr/library/aa995971\(v=exchg.150\))

Voici quelques exemples d'utilisation de l'environnement de ligne de commande Exchange Management Shell pour modifier des propriétés d'utilisateur de messagerie.

Cet exemple définit l'adresse de messagerie externe pour Pilar Pinilla.

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

Cet exemple masque tous les utilisateurs de messagerie dans le carnet d’adresses de l’organisation.

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

Cet exemple définit la propriété Société de tous les utilisateurs de messagerie sur Contoso.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

Cet exemple attribue la valeur ContosoEmployee à la propriété CustomAttribute1 pour tous les utilisateurs de messagerie qui ont une valeur Contoso dans la propriété Société.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié les propriétés des utilisateurs de messagerie, procédez comme suit :

  - Dans le CAE, sélectionnez l'utilisateur de messagerie et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété modifiée.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez les cmdlets **Get-User** et **Get-MailUser** pour vérifier les modifications. L'environnement de ligne de commande Exchange Management Shell a pour avantage de permettre l'affichage de plusieurs propriétés pour divers contacts de messagerie.
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    Dans l'exemple ci-dessus où la valeur Contoso a été attribuée à la propriété Société pour tous les contacts de messagerie, exécutez la commande suivante pour vérifier les modifications :
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    Dans l'exemple ci-dessus où la valeur ContosoEmployee a été attribuée à la propriété CustomAttribute1 pour tous les utilisateurs de messagerie, exécutez la commande suivante pour vérifier les modifications.
    
        Get-MailUser | Fl Name,CustomAttribute1 

## Modifier en bloc des utilisateurs de messagerie

Vous pouvez également utiliser le CAE pour modifier des propriétés sélectionnées de plusieurs utilisateurs de messagerie. Quand vous sélectionnez au moins deux utilisateurs de messagerie dans la liste de contacts du CAE, les propriétés pouvant être modifiées en bloc apparaissent dans le volet d'informations. Lorsque vous modifiez l'une de ces propriétés, la modification est appliquée à tous les destinataires sélectionnés.

Quand vous modifiez en bloc des utilisateurs de messagerie, vous pouvez modifier les zones de propriété suivantes :

  - **Informations de contact**   Permet de modifier des propriétés communes, telles que la rue, le code postal et le nom de la ville.

  - **Organisation**   Permet de modifier des propriétés communes, telles que le nom du service, le nom de la société et le nom du responsable auquel les contacts de messagerie ou les utilisateurs de messagerie sélectionnés rendent compte.

## Utiliser le CAE pour modifier en bloc des utilisateurs de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste de contacts, sélectionnez au moins deux utilisateurs de messagerie. Vous ne pouvez pas modifier en bloc une combinaison de contacts de messagerie et d’utilisateurs de messagerie.
    
    > [!TIP]
    > Vous pouvez sélectionner plusieurs utilisateurs de messagerie adjacents en maintenant la touche Maj enfoncée tout en cliquant sur le premier puis le dernier utilisateur de messagerie à modifier. Vous pouvez aussi sélectionner plusieurs utilisateurs de messagerie en maintenant enfoncée la touche Ctrl tout en cliquant sur chaque utilisateur à modifier.


3.  Dans le volet Détails, sous **Modification en bloc**, cliquez sur **Mettre à jour** sous **Informations de contact** ou **Organisation**.

4.  Apportez les modifications souhaitées dans la page Propriétés, puis enregistrez-les.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié en bloc des utilisateurs de messagerie, procédez de l’une des manières suivantes :

  - Dans le CAE, sélectionnez chacun des utilisateurs de messagerie que vous avez modifiés en bloc et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher les propriétés modifiées.

  - Dans l'environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Get-User** pour vérifier les modifications. Par exemple, supposons que vous ayez utilisé la fonctionnalité de modification en bloc dans le CAE pour modifier le responsable et le bureau de tous les utilisateurs de messagerie d'une entreprise de vente nommée A. Datum Corporation. Pour vérifier ces modifications, vous pouvez exécuter la commande suivante dans l'environnement de ligne de commande Exchange Management Shell :
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## Utiliser la synchronisation d’annuaires pour gérer les utilisateurs de messagerie dans Exchange Online

Cette section fournit des informations sur la gestion des utilisateurs de messagerie électronique à l’aide de la synchronisation d’annuaires dans Exchange Online. La synchronisation d’annuaires est disponible pour les clients hybrides disposant de boîtes aux lettres locales et hébergées dans le cloud, ainsi que pour les clients Exchange Online entièrement hébergés avec un annuaire Active Directory local.

> [!NOTE]
> Si vous utilisez la synchronisation d’annuaires pour gérer vos destinataires, vous pouvez toujours ajouter et gérer les utilisateurs dans le Centre d’administration Office 365, mais ils ne seront pas synchronisés avec votre annuaire Active Directory sur site. En effet, la synchronisation d’annuaires ne synchronise que les destinataires de votre annuaire Active Directory sur site vers le nuage.


> [!NOTE]
> Il est recommandé d’utiliser la synchronisation d’annuaires avec les fonctionnalités suivantes :
> <ul>
> <li><p><strong>Listes d’expéditeurs autorisés et bloqués dans Outlook</strong> : une fois synchronisées avec le service, ces listes seront prioritaires sur le filtrage de courrier indésirable dans le service. Cela permet aux utilisateurs de gérer leurs propres listes d’expéditeurs autorisés et bloqués en fonction de l’utilisateur et du domaine.</p></li>
> <li><p><strong>Blocage du périmètre basé sur l’annuaire (DBEB)</strong>: pour plus d’informations sur le DBEB, voir <a href="https://technet.microsoft.com/fr-fr/library/dn600322(v=exchg.150)">Utiliser le blocage du périmètre basé sur l’annuaire pour rejeter les messages envoyés à des destinataires non valides</a>.</p></li>
> <li><p><strong>Mise en quarantaine du courrier indésirable des utilisateurs finals</strong> : pour accéder à leur courrier indésirable mis en quarantaine, les utilisateurs finals doivent disposer d’un identifiant utilisateur et d’un mot de passe Office 365 valides. Les clients qui disposent de boîtes aux lettres locales doivent être des utilisateurs de messagerie électronique valides.</p></li>
> <li><p><strong>Règles de transport -</strong> lorsque vous utilisez la synchronisation d’annuaires, les utilisateurs et les groupes Active Directory existants sont automatiquement téléchargés dans le cloud. Vous pouvez alors créer des règles de transport qui ciblent des utilisateurs et/ou groupes spécifiques sans avoir à les ajouter manuellement via le CAE ou via la session Windows PowerShell distante. Notez que les <a href="https://go.microsoft.com/fwlink/?linkid=507569">groupes de distribution dynamiques</a> ne peuvent pas être synchronisés via la synchronisation d’annuaires.</p></li></ul>

**Avant de commencer**

Obtenez les autorisations nécessaires et préparez la synchronisation d’annuaires, comme décrit dans la rubrique [Préparer la synchronisation d’annuaires](https://go.microsoft.com/fwlink/p/?linkid=308908).

**Pour synchroniser les annuaires d’utilisateurs**

1.  Activez la synchronisation d’annuaires, comme décrit dans la rubrique [Activer la synchronisation d’annuaires](https://go.microsoft.com/fwlink/p/?linkid=308909).

2.  Configurez votre ordinateur de synchronisation d’annuaires, comme décrit dans la rubrique [Configurer votre ordinateur de synchronisation d’annuaires](http://go.microsoft.com/fwlink/p/?linkid=308911).

3.  Synchronisez vos annuaires, comme décrit dans la rubrique [Utiliser l’Assistant Configuration pour synchroniser vos annuaires](http://go.microsoft.com/fwlink/?linkid=308912).
    
    > [!NOTE]
    > Après exécution de l’Assistant Configuration de l’outil de synchronisation Azure Active Directory, le compte <strong>MSOL_AD_SYNC</strong> est créé dans votre forêt Active Directory. Ce compte permet de lire et de synchroniser vos informations Active Directory sur site. Pour que la synchronisation d’annuaires fonctionne correctement, assurez-vous que le port TCP 443 est ouvert sur votre serveur de synchronisation d’annuaires sur site.


4.  Activez les utilisateurs synchronisés, comme décrit dans la rubrique [Activer les utilisateurs synchronisés](http://go.microsoft.com/fwlink/p/?linkid=308913).

5.  Gérez la synchronisation d’annuaires, comme décrit dans la rubrique [Gérer la synchronisation d’annuaires](http://go.microsoft.com/fwlink/p/?linkid=308915).

6.  Vérifiez qu’Exchange Online effectue la synchronisation correctement. Dans le CAE, accédez à **Destinataires** \> **Contacts** et vérifiez que la liste des utilisateurs a été correctement synchronisée à partir de votre environnement local.

