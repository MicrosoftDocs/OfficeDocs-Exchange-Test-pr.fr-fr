---
title: 'Création de boîtes aux lettres utilisateur: Exchange 2013 Help'
TOCTitle: Création de boîtes aux lettres utilisateur
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52062961
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Création de boîtes aux lettres utilisateur

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-04-12_

Les boîtes aux lettres sont le type de destinataire le plus courant utilisé par les professionnels de l'information dans une organisation Exchange. Chaque boîte aux lettres est associée à un compte d'utilisateur Active Directory. L'utilisateur peut se servir de la boîte aux lettres pour envoyer et recevoir des messages, ainsi que pour stocker des messages, des rendez-vous, des tâches, des notes et des documents. Utilisez le Centre d'administration Exchange ou l'environnement de ligne de commande Exchange Management Shell pour créer des boîtes aux lettres utilisateur

Vous pouvez également créer des boîtes aux lettres utilisateur pour les utilisateurs existants ayant un compte d'utilisateur Active Directory mais sans boîte aux lettres correspondante. Il s'agit de l'*activation des boîtes aux lettres* pour les utilisateurs existants.

## Ce qu'il faut savoir avant de commencer

  - Durée estimée pour effectuer chaque tâche de boîte aux lettres utilisateur : 2 à 5 minutes.

  - Quand vous créez une boîte aux lettres utilisateur, vous ne pouvez pas utiliser d'apostrophe (') ni de guillemets (") dans l'alias ou le nom de connexion d'utilisateur, car ces caractères ne sont pas pris en charge. Bien qu'il soit possible que vous ne receviez pas d'erreur si vous créez une boîte aux lettres comportant des caractères non pris en charge, ceux-ci peuvent se révéler problématiques par la suite. Par exemple, les utilisateurs autorisés à accéder à une boîte aux lettres créée avec un caractère non pris en charge peuvent rencontrer des problèmes ou un comportement inattendu.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Créer une boîte aux lettres utilisateur

## Utiliser le Centre d'administration Exchange (CAE) pour créer une boîte aux lettres utilisateur

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Cliquez sur **Nouveau** \> **Boîte aux lettres utilisateur**.

3.  Dans le champ **Alias** de la page **Nouvelle boîte aux lettres utilisateur**, saisissez l'alias de l'utilisateur, qui indique son alias de messagerie. L'alias de l'utilisateur est la partie de l'adresse de messagerie qui apparaît à gauche du symbole (@). Il doit être unique dans la forêt.
    
    > [!NOTE]  
    > Si vous ne renseignez pas cette zone, la valeur de la partie nom d'utilisateur du <strong>Nom de connexion utilisateur</strong> est utilisée pour l'alias de messagerie.


4.  Activez l'une des options suivantes :
    
      - **Utilisateur existant**   Activez cette option pour activer la messagerie et créer une boîte aux lettres pour un utilisateur existant.
        
        Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un utilisateur – Forêt entière**. Cette boîte de dialogue contient une liste des comptes d'utilisateur Active Directory de la forêt qui ne sont pas à extension messagerie ou qui n'ont pas de boîte aux lettres Exchange. Sélectionnez le compte d'utilisateur pour lequel vous souhaitez activer la messagerie, puis cliquez sur **OK**. Si vous activez cette option, il n'est pas nécessaire de saisir les informations du compte d'utilisateur, car elles existent déjà dans Active Directory.
    
      - **Nouvel utilisateur**   Activez cette option pour créer un compte d'utilisateur dans Active Directory et créer une boîte aux lettres pour cet utilisateur. Si vous activez cette option, vous devrez saisir les informations de compte d'utilisateur requises.
    
    > [!NOTE]  
    > Le compte Active Directory associé aux boîtes aux lettres utilisateur doit résider dans la même forêt que le serveur Exchange. Pour créer une boîte aux lettres pour un compte d'utilisateur résidant dans une forêt approuvée, vous devez créer une boîte aux lettres liée. Consultez la rubrique <a href="manage-linked-mailboxes-exchange-2013-help.md">Gérer les boîtes aux lettres liées</a>.


5.  Si vous avez sélectionné **Nouvel utilisateur** à l'étape 4, renseignez les zones suivantes de la page **Nouvelle boîte aux lettres utilisateur**. Sinon, passez à l'étape 7.
    
      - **Prénom**   Cette zone de texte permet d'entrer le prénom de l'utilisateur.
    
      - **Initiales**   Cette zone de texte permet d'entrer les initiales de l'utilisateur.
    
      - **Nom de famille**   Cette zone de texte permet d'entrer le nom de famille de l'utilisateur.
    
      - \* **Nom complet**   Ce champ permet d'entrer un nom complet pour l'utilisateur. Il s'agit du nom répertorié dans la liste de boîtes aux lettres du CAE et dans le carnet d'adresses partagé. Par défaut, ce champ est renseigné avec les noms entrés dans les champs **Prénom**, **Initiales** et **Nom de famille**. Si vous n'avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Le nom ne peut pas comporter plus de 64 caractères.
    
      - \* **Nom**   Ce champ permet d'entrer un nom pour l'utilisateur. Il s'agit du nom qui s'affiche dans Active Directory. Ce champ est également renseigné avec les noms entrés dans les champs **Prénom**, **Initiales** et **Nom de famille**. Si vous n'avez pas utilisé ces champs, vous devez tout de même saisir un nom car ce champ est obligatoire. Ce nom ne peut pas comporter plus de 64 caractères.
    
      - **Unité d'organisation**   Vous pouvez sélectionner une unité d'organisation autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine Active Directory qui contient l'ordinateur sur lequel le CAE est exécuté. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Utilisateurs de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d'organisation spécifique, cette unité est sélectionnée par défaut.
        
        Pour sélectionner une autre unité d'organisation, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d'organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez l'unité d'organisation souhaitée, puis cliquez sur **OK**.
    
      - \* **Nom de connexion utilisateur**    Utilisez cette zone pour saisir le nom dont l'utilisateur se servira pour accéder à la boîte aux lettres et se connecter au domaine. Le nom de connexion de l'utilisateur est constitué du nom d'utilisateur à gauche du symbole (@) et d'un suffixe à droite. Généralement, le suffixe est le nom du domaine dans lequel le compte d'utilisateur réside. Notez que vous ne pouvez pas utiliser d'apostrophe (') ni de guillemets (") dans le nom de connexion de l'utilisateur, car ces caractères ne sont pas pris en charge.
        
        > [!NOTE]  
        > Si la valeur du nom d'utilisateur diffère de celle utilisée dans le champ <strong>Alias</strong>, l'adresse de messagerie de l'utilisateur et le nom de connexion de l'utilisateur seront différents.
    
      - \* **Nouveau mot de passe**   Ce champ permet d'entrer le mot de passe que l'utilisateur doit utiliser pour se connecter à sa boîte aux lettres.
        
        > [!NOTE]  
        > Assurez-vous que le mot de passe que vous tapez est conforme aux exigences de longueur, de complexité et d'historique de mot de passe du domaine dans lequel vous créez le compte d'utilisateur.
    
      - \* **Confirmer le mot de passe**   Ce champ permet de confirmer le mot de passe entré dans le champ **Mot de passe**.
    
      - **Exiger le changement du mot de passe à la prochaine connexion**   Cochez cette case si vous voulez que l'utilisateur réinitialise le mot de passe lors de sa première connexion à la boîte aux lettres.
        
        Si vous cochez cette case, une boîte de dialogue s'ouvre lors de la première connexion et invite le nouvel utilisateur à changer son mot de passe. L'utilisateur ne peut effectuer aucune tâche tant que le mot de passe n'a pas été modifié.

6.  Cliquez sur **Plus d'options** pour configurer les zones suivantes. Sinon, passez à l'étape 7 pour enregistrer la nouvelle boîte aux lettres utilisateur.
    
      - **Spécifier la base de données de boîtes aux lettres**   Cette option permet de spécifier une base de données de boîtes aux lettres au lieu d'autoriser Exchange à en sélectionner une à votre place. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner une base de données de boîtes aux lettres**. Cette boîte de dialogue répertorie toutes les bases de données de boîtes aux lettres au sein de votre organisation Exchange. Par défaut, les bases de données de boîtes aux lettres sont triées par nom. Vous pouvez également cliquer sur le titre de la colonne correspondante pour trier les bases de données par nom ou version de serveur. Sélectionnez la base de données de boîtes aux lettres à utiliser, puis cliquez sur **OK**.
    
      - **Créer un stockage d'archive locale pour cet utilisateur**   Cochez cette case pour créer une boîte aux lettres d'archivage pour la boîte aux lettres. Si vous créez une boîte aux lettres d'archivage, les éléments de la boîte aux lettres seront automatiquement déplacés de la boîte aux lettres principale vers l'archive, selon les paramètres de stratégie de rétention par défaut ou ceux que vous définissez.
        
        Cliquez sur **Parcourir** pour sélectionner une base de données résidant dans la forêt locale pour stocker la boîte aux lettres d'archivage.
        
        Pour plus d'informations, consultez la rubrique [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Stratégie de carnet d'adresses**   Cette option permet de spécifier une stratégie de carnet d'adresses pour la boîte aux lettres. Les stratégies de carnet d'adresses contiennent une liste d'adresses globale (LAG), un carnet d'adresses en mode hors connexion, une liste de salles et un ensemble de listes d'adresses. Quand elle est appliquée à des utilisateurs de boîtes aux lettres, une stratégie de carnet d'adresses leur fournit l'accès à une liste d'adresses globale personnalisée dans Outlook et Outlook Web App. Pour plus d'informations, consultez la rubrique [Stratégies de carnet d’adresses](https://docs.microsoft.com/fr-fr/exchange/address-books/address-book-policies/address-book-policies).
        
        Dans la liste déroulante, sélectionnez la stratégie à associer à cette boîte aux lettres.

7.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la boîte aux lettres.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres utilisateur

Cet exemple crée un compte d'utilisateur et sa boîte aux lettres pour Pilar Pinilla avec les détails suivants :

  - L'alias est pilarp

  - Le prénom est Pilar et le nom de famille est Pinilla

  - Le nom et le nom complet sont Pilar Pinilla

  - Le nom de connexion de l'utilisateur est pilarp@contoso.com

  - Le mot de passe est Pa$$word1

  - La boîte aux lettres sera créée dans l'unité d'organisation par défaut. Pour spécifier un autre unité d'organisation, utilisez le paramètre *OrganizationalUnit*.

<!-- end list -->

```powershell
New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)
```

Pour obtenir des informations sur la syntaxe et les paramètres, consultez la rubrique [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Voici comment vérifier qu'une boîte aux lettres utilisateur a bien été créée :

  - Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**. La nouvelle boîte aux lettres d'utilisateur s'affiche dans la liste des boîtes aux lettres. Sous **Type de boîte aux lettres**, le type est **Utilisateur**.

  - Dans l'environnement de ligne de commande, exécutez la commande suivante pour afficher les informations sur la nouvelle boîte aux lettres utilisateur.
    
    ```powershell
    Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```

## Créer une boîte pour un utilisateur existant

Vous pouvez également créer des boîtes aux lettres utilisateur pour les utilisateurs existants ayant un compte d'utilisateur Active Directory mais sans boîte aux lettres correspondante. Il s'agit de l'*activation des boîtes aux lettres* pour les utilisateurs existants. Après avoir activé une boîte aux lettres pour un utilisateur existant, celui-ci peut envoyer et recevoir des messages électroniques.

## Utiliser le Centre d'administration Exchange (CAE) pour créer une boîte aux lettres pour un utilisateur existant

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Cliquez sur **Nouveau** \> **Boîte aux lettres utilisateur**.

3.  Dans le champ **Alias** de la page **Nouvelle boîte aux lettres utilisateur**, saisissez l'alias de l'utilisateur, qui indique son alias de messagerie. L'alias de l'utilisateur est la partie de l'adresse de messagerie qui apparaît à gauche du symbole (@). Il doit être unique dans la forêt.
    
    > [!NOTE]  
    > Si vous ne renseignez pas cette zone, la valeur de la partie nom d'utilisateur du <strong>Nom de connexion utilisateur</strong> est utilisée pour l'alias de messagerie.


4.  Cliquez sur **Utilisateur existant**.

5.  Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un utilisateur – Forêt entière**. Cette boîte de dialogue contient une liste des comptes d'utilisateur Active Directory de la forêt qui ne sont pas à extension messagerie ou qui n'ont pas de boîte aux lettres Exchange. Sélectionnez le compte d'utilisateur pour lequel vous souhaitez activer la messagerie, puis cliquez sur **OK**.
    
    Quand vous créez une boîte aux lettres pour un utilisateur existant, vous n'avez pas besoin de fournir les informations sur le compte car elles existent déjà dans Active Directory.
    
    > [!NOTE]  
    > Le compte Active Directory associé aux boîtes aux lettres utilisateur doit résider dans la même forêt que le serveur Exchange. Pour créer une boîte aux lettres pour un compte d'utilisateur résidant dans une forêt approuvée, vous devez créer une boîte aux lettres liée. Consultez la rubrique <a href="manage-linked-mailboxes-exchange-2013-help.md">Gérer les boîtes aux lettres liées</a>.


6.  Cliquez sur **Plus d'options** pour configurer les zones suivantes. Sinon, passez à l'étape 7 pour enregistrer la nouvelle boîte aux lettres utilisateur.
    
      - **Spécifier la base de données de boîtes aux lettres**   Cette option permet de spécifier une base de données de boîtes aux lettres au lieu d'autoriser Exchange à en sélectionner une à votre place. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner une base de données de boîtes aux lettres**. Cette boîte de dialogue répertorie toutes les bases de données de boîtes aux lettres au sein de votre organisation Exchange. Par défaut, les bases de données de boîtes aux lettres sont triées par nom. Vous pouvez également cliquer sur le titre de la colonne correspondante pour trier les bases de données par nom ou version de serveur. Sélectionnez la base de données de boîtes aux lettres à utiliser, puis cliquez sur **OK**.
    
      - **Créer un stockage d'archive locale pour cet utilisateur**   Cochez cette case pour créer une boîte aux lettres d'archivage pour la boîte aux lettres. Si vous créez une boîte aux lettres d'archivage, les éléments de boîte aux lettres seront automatiquement déplacés de la boîte aux lettres principale vers l'archive, selon les paramètres de stratégie de rétention par défaut ou ceux que vous définissez.
        
        Cliquez sur **Parcourir** pour sélectionner une base de données résidant dans la forêt locale pour stocker la boîte aux lettres d'archivage.
        
        Pour plus d'informations, consultez la rubrique [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Stratégie de carnet d'adresses**   Cette option permet de spécifier une stratégie de carnet d'adresses pour la boîte aux lettres. Les stratégies de carnet d'adresses contiennent une liste d'adresses globale (LAG), un carnet d'adresses en mode hors connexion, une liste de salles et un ensemble de listes d'adresses. Quand elle est appliquée à des utilisateurs de boîtes aux lettres, une stratégie de carnet d'adresses leur fournit l'accès à une liste d'adresses globale personnalisée dans Outlook et Outlook Web App. Pour plus d'informations, consultez la rubrique [Stratégies de carnet d’adresses](https://docs.microsoft.com/fr-fr/exchange/address-books/address-book-policies/address-book-policies).
        
        Dans la liste déroulante, sélectionnez la stratégie à associer à cette boîte aux lettres.

7.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la boîte aux lettres.

## Utiliser l'environnement de ligne de commande pour créer une boîte aux lettres pour un utilisateur existant

Cet exemple permet de créer une boîte aux lettres pour l'utilisateur existant estherv@contoso.com dans la base de données Exchange appelée UsersMailboxDatabase.

```powershell
Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase
```

La cmdlet **Enable-Mailbox** permet d'activer la messagerie de plusieurs utilisateurs. Pour ce faire, il faut envoyer les résultats de la cmdlet **Get-User** vers la cmdlet **Enable-Mailbox**. Lorsque vous exécutez la cmdlet **Get-User**, vous devez renvoyer uniquement les utilisateurs pour lesquels la messagerie n'est pas activée. Pour ce faire, vous devez spécifier la valeur User avec le paramètre *RecipientTypeDetails*. Vous pouvez également limiter les résultats renvoyés à l'aide du paramètre *Filter* pour demander uniquement les utilisateurs répondant aux critères spécifiés. Vous canalisez ensuite les résultats vers la cmdlet **Enable-Mailbox**.

Par exemple, la commande suivante active une boîte aux lettres pour des utilisateurs qui n'en possèdent pas et dont la propriété **UserPrincipalName** possède une valeur. Cela permet de s'assurer qu'un compte système n'est pas converti par inadvertance en boîte aux lettres.

```powershell
Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox
```

Pour obtenir des informations sur la syntaxe et les paramètres, consultez les rubriques [Enable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa998251\(v=exchg.150\)) et [Get-User](https://technet.microsoft.com/fr-fr/library/aa996896\(v=exchg.150\)).

Pour plus d'informations sur le traitement « pipeline », consultez la rubrique [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez bien créé une boîte aux lettres pour un utilisateur existant :

  - Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**. Le nouvel utilisateur dont la boîte à lettres vient d'être activée s'affiche dans la liste des boîtes aux lettres. Sous **Type de boîte aux lettres**, le type est **Utilisateur**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher des informations sur le nouvel utilisateur dont la boîte à lettres vient d'être activée.
    
    ```powershell
    Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```
    
    Notez que la valeur pour la propriété *RecipientTypeDetails* est `UserMailbox`.

