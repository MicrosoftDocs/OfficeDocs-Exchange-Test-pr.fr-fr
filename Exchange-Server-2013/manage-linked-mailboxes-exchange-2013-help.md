---
title: 'Gérer les boîtes aux lettres liées: Exchange 2013 Help'
TOCTitle: Gérer les boîtes aux lettres liées
ms:assetid: 76e12d4a-1c3a-42e2-b64c-c09d36e81bd3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673532(v=EXCHG.150)
ms:contentKeyID: 50478491
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les boîtes aux lettres liées

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-27_

Les boîtes aux lettres liées sont les boîtes aux lettres des utilisateurs qui y accèdent par une forêt séparée et approuvée. Les boîtes aux lettres liées peuvent être utiles pour les organisations qui déploient Exchange dans une forêt ressource. Le scénario de forêt de ressources permet à une organisation de centraliser Exchange dans une forêt unique, tout en permettant d’accéder à l’organisation Exchange avec des comptes d’utilisateur situés dans une ou plusieurs forêts approuvées (appelées *forêts de comptes*). Le compte d’utilisateur qui accède à la boîte aux lettres liée n’existe pas dans la forêt où Exchange est déployé. Par conséquent, un compte d’utilisateur désactivé existant dans la même forêt qu’Exchange est créé et associé à la boîte aux lettres liée correspondante.

La figure suivante décrit la relation entre le compte d’utilisateur lié servant à accéder à la boîte aux lettres liée (située dans la forêt de comptes) et le compte d’utilisateur désactivé dans la forêt de ressources Exchange qui est associée à la boîte aux lettres liée.

**Boîtes aux lettres liées**

![Organisation Exchange complexe avec forêt de ressources](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organisation Exchange complexe avec forêt de ressources")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une approbation doit être configurée entre la forêt Exchange et au moins une forêt de comptes pour pouvoir créer des boîtes aux lettres liées. Vous devez au minimum configurer une approbation sortante unidirectionnelle, afin que la forêt Exchange approuve la forêt de comptes. Pour plus d’informations, voir <a href="https://technet.microsoft.com/fr-fr/library/jj156983(v=exchg.150)">En savoir plus sur la configuration d’une approbation de forêt prenant en charge les boîtes aux lettres liées</a>.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Un compte d’utilisateur (appelé *compte principal lié*) doit être présent dans la forêt de comptes pour pouvoir créer une boîte aux lettres liée. Ceci est dû au fait que la boîte aux lettres liée est associée à un utilisateur dans la forêt de comptes.

  - Si vous avez configuré une approbation sortante unidirectionnelle dans laquelle la forêt Exchange approuve la forêt de comptes, vous aurez besoin des informations d’identification d’administrateur dans la forêt de comptes pour créer une boîte aux lettres liée.
    
    Pour créer une boîte aux lettres liée sans être invité à saisir les informations d’identification de l’administrateur dans la forêt de compte, vous devez créer une approbation bilatérale, ou créer une autre approbation sortante unilatérale lorsque la forêt de compte approuve également la forêt Exchange. Cette étape nécessite également les informations d’identification d’administrateur dans la forêt de comptes.

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

## Créer une boîte aux lettres liée

## Utiliser le Centre d’administration Exchange (EAC) pour créer une boîte aux lettres liée

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Cliquez sur **Nouveau** \> **Boîte aux lettres liée**.

3.  Sur la page **Nouvelle boîte aux lettres liée**, dans la zone **Forêt ou domaine approuvé**, sélectionnez le nom de la forêt de comptes qui contient le compte d’utilisateur pour lequel vous créez la boîte aux lettres liée. Cliquez sur **Suivant**.

4.  Si votre organisation a configuré une approbation sortante unidirectionnelle dans laquelle la forêt Exchange approuve la forêt de comptes, vous devrez entrer les informations d’identification d’administrateur dans la forêt de comptes pour pouvoir accéder à un contrôleur de domaine dans la forêt approuvée. Saisissez le nom d’utilisateur et le mot de passe d’un compte administrateur dans la forêt de comptes, puis cliquez sur **Suivant**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous n’aurez pas à entrer les informations d’identification d’administrateur si vous avez créé une approbation bidirectionnelle ou une autre approbation sortante unidirectionnelle dans laquelle la forêt de comptes approuve la forêt Exchange.</td>
    </tr>
    </tbody>
    </table>


5.  Renseignez les zones suivantes sur la page **Sélectionner un compte principal lié**.
    
      - **Contrôleur de domaine lié**   Sélectionnez un contrôleur de domaine dans la forêt de comptes. Exchange se connectera à ce contrôleur de domaine pour récupérer la liste des comptes d’utilisateur dans la forêt de comptes, afin que vous puissiez sélectionner le compte principal lié.
    
      - **Compte principal lié**   Cliquez sur **Parcourir**, sélectionnez un compte d’utilisateur dans la forêt de comptes, puis cliquez sur **OK**. La nouvelle boîte aux lettres liée sera associée à ce compte.

6.  Cliquez sur **Suivant** et renseignez les zones suivantes sur la page **Entrer des informations générales**.
    
      - **\*Nom**   Ce champ permet de saisir un nom pour l’utilisateur. Il s’agit du nom utilisé comme nom complet dans le Centre d’administration Exchange (EAC) et le carnet d’adresses de votre organisation, mais aussi du nom répertorié dans Active Directory. Ce nom est obligatoire.
    
      - **Unité d’organisation**   Vous pouvez sélectionner une unité d’organisation (UO) autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine Active Directory qui contient l’ordinateur sur lequel le CAE est exécuté. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d’organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d’organisation de la forêt Exchange qui se trouvent dans la portée indiquée. Sélectionnez l’UO souhaitée, puis cliquez sur **OK**.
    
      - **\* Nom de connexion utilisateur**   Utilisez cette zone pour saisir le nom de connexion utilisateur qui est obligatoire pour créer une boîte aux lettres liée. Saisissez le nom d’utilisateur ici. Ce nom sera utilisé dans la partie gauche de l’adresse électronique pour la boîte aux lettres liée si vous ne spécifiez pas d’alias.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Puisque le compte d’utilisateur créé dans la forêt Exchange est désactivé lorsque vous créez une boîte aux lettres liée, l’utilisateur n’emploie pas le nom de connexion utilisateur pour se connecter à la boîte aux lettres liée. Il se connecte avec ses informations d’identification depuis la forêt de comptes.</td>
        </tr>
        </tbody>
        </table>


7.  Cliquez sur **Plus d’options** pour configurer les cases suivantes. Sinon, passez à l’étape 8 pour enregistrer la nouvelle boîte aux lettres liée.
    
      - **Alias**   Saisissez l’alias qui spécifie l’alias de messagerie électronique pour la boîte aux lettres liée. L’alias de l’utilisateur est la partie de l’adresse de messagerie qui apparaît à gauche du symbole (@). Ce dernier doit être unique dans la forêt.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Si vous ne renseignez pas ce champ, la valeur de la partie nom d’utilisateur du <strong>Nom de connexion utilisateur</strong> est utilisée pour l’alias de messagerie.</td>
        </tr>
        </tbody>
        </table>
    
      - **Prénom**, **Initiales**, **Nom de famille**
    
      - **Base de données de boîtes aux lettres**   Cette option permet de spécifier une base de données de boîtes aux lettres au lieu d’autoriser Exchange à choisir une base de données à votre place. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélection de base de données de boîtes aux lettres**. Cette boîte de dialogue répertorie toutes les bases de données de boîtes aux lettres au sein de votre organisation Exchange. Par défaut, les bases de données de boîtes aux lettres sont triées par nom. Vous pouvez également cliquer sur le titre de la colonne correspondante pour trier les bases de données par nom ou version de serveur. Sélectionnez la base de données de boîtes aux lettres à utiliser, puis cliquez sur **OK**.
    
      - **Stratégie de carnet d’adresses**   Cette option permet de spécifier une stratégie de carnet d’adresses pour la boîte aux lettres liée. Les stratégies de carnet d’adresses contiennent une liste d’adresses globale, un carnet d’adresses en mode hors connexion, une liste de salles et un ensemble de listes d’adresses. Lors de l’affectation aux utilisateurs, une stratégie de carnet d’adresses leur fournit l’accès à une liste d’adresses globale personnalisée dans Outlook et Outlook Web App. Pour en savoir plus, voir [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).
        
        Dans la liste déroulante, sélectionnez la règle que vous souhaitez associer à cette boîte aux lettres.

8.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la nouvelle boîte aux lettres liée.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres liée

Cet exemple crée une boîte aux lettres liée pour Ayla Kol dans la forêt de ressources Exchange CONTOSO. Le domaine FABRIKAM se trouve dans la forêt de comptes. Le compte d’administrateur FABRIKAM \\administrator est utilisé pour accéder au contrôleur de domaine lié.

    New-Mailbox -Name "Ayla Kol" -LinkedDomainController "DC1_FABRIKAM" -LinkedMasterAccount " FABRIKAM\aylak" -OrganizationalUnit Users -UserPrincipalName aylak@contoso.com -LinkedCredential:(Get-Credential FABRIKAM\administrator)

Pour obtenir des informations sur la syntaxe et les paramètres, voir [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une boîte aux lettres liée, procédez de l’une des façons suivantes :

  - Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**. La nouvelle boîte aux lettres liée s’affiche dans la liste de boîtes aux lettres. Sous **Type de boîte aux lettres**, le type est **Lié**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations sur la nouvelle boîte aux lettres liée.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,IsLinked,LinkedMasterAccount

## Modifier les propriétés de la boîte aux lettres liée

Une fois que vous avez créé une boîte aux lettres liée, vous pouvez la modifier et définir des propriétés supplémentaires via le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell.

Vous pouvez également modifier les propriétés de plusieurs boîtes aux lettres liées en même temps. Pour plus d’informations, voir la section « Modifier en bloc des boîtes aux lettres utilisateur » de la rubrique [Gestion des boîtes aux lettres utilisateur](manage-user-mailboxes-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La durée d’exécution estimée pour cette tâche varie selon le nombre de propriétés que vous souhaitez afficher ou modifier.</td>
</tr>
</tbody>
</table>


## Utiliser le Centre d’administration Exchange (CAE) pour modifier les propriétés d’une boîte aux lettres liée

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres, cliquez sur la boîte aux lettres liée dont vous souhaitez modifier les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page Propriétés de la boîte aux lettres, cliquez sur l’une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Espace de stockage utilisé
    
      - Adresse de messagerie
    
      - Fonctionnalités de boîte aux lettres
    
      - Membre de
    
      - Infos-courrier
    
      - Délégation de boîtes aux lettres

## Général

Dans la section **Général**, vous pouvez afficher ou modifier des informations de base sur l’utilisateur.

  - **\* Nom de la boîte aux lettres liée**   Nom qui est indiqué dans Active Directory. Si vous modifiez ce nom, il ne peut pas comporter plus de 64 caractères.

  - **\* Nom complet**   Ce nom s’affiche dans le carnet d’adresses de l’organisation, sur les lignes À : et De : du message électronique, mais aussi dans la liste des boîtes aux lettres du Centre d’administration Exchange (CAE). Ce nom ne peut pas contenir d’espaces vides avant ou après le nom complet.

  - **\* Nom de connexion utilisateur**   Pour les boîtes aux lettres utilisateur, il s’agit du nom employé par l’utilisateur pour se connecter à sa boîte aux lettres et au domaine. Pour les boîtes aux lettres liées, le compte d’utilisateur correspondant qui a été créé dans la forêt Exchange lors de la création de la boîte aux lettres liée est désactivé. L’utilisateur utilise ses informations d’identification depuis la forêt de comptes pour se connecter à la boîte aux lettres liée.
    
    Si vous modifiez ce nom, celui-ci doit être unique dans votre organisation.

  - **Compte principal lié**   Cette zone en lecture seule affiche l’utilisateur (au format domaine\\nom d’utilisateur) à partir de la forêt de comptes qui est associée à la boîte aux lettres liée. Pour changer le compte principal lié associé à la boîte aux lettres liée, vous devez utiliser la cmdlet **Set-Mailbox** dans l’environnement de ligne de commande Exchange Management Shell. Si vous changez le compte principal lié, l’utilisateur devra utiliser les informations d’identification du nouveau compte principal lié pour se connecter à la boîte aux lettres liée. Pour obtenir la syntaxe de commande permettant de changer le compte principal lié, voir Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier les propriétés d’une boîte aux lettres liée.

  - **Masquer des listes d’adresses**   Activez cette case à cocher pour que la boîte aux lettres liée n’apparaisse pas dans le carnet d’adresses et les autres listes d’adresses qui sont définies dans votre organisation Exchange. Une fois que vous avez activé cette case à cocher, les utilisateurs peuvent encore envoyer des messages à cet utilisateur en utilisant l’adresse de messagerie électronique.

Cliquez sur **Plus d’options** pour afficher ou modifier les propriétés supplémentaires suivantes :

  - **Unité d’organisation**   Ce champ en lecture seule affiche l’unité d’organisation (UO) qui contient le compte d’utilisateur. Vous devez utiliser le composant Utilisateurs et ordinateurs Active Directory pour déplacer le compte d’utilisateur vers une autre unité d’organisation.

  - **Base de données de boîtes aux lettres**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres. Pour déplacer la boîte aux lettres vers une autre base de données, sélectionnez-la dans la liste de boîtes aux lettres, puis cliquez sur **Déplacer la boîte aux lettres vers une autre base de données** dans le volet d’informations.

  - **\* Alias** Spécifie l’alias de messagerie électronique pour la boîte aux lettres liée. L’alias est la partie de l’adresse de messagerie qui apparaît à gauche du symbole @. Ce dernier doit être unique dans la forêt.

  - **Prénom**, **Initiales**, **Nom de famille**

  - **Attributs personnalisés**   Cette section affiche les attributs personnalisés définis pour la boîte aux lettres liée. Pour spécifier des valeurs d’attribut personnalisées, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Vous pouvez spécifier jusqu’à 15 attributs personnalisés pour le destinataire.

## Espace de stockage utilisé

Utilisez la section **Utilisation de la boîte aux lettres** pour afficher ou modifier les paramètres de quota de stockage de boîte aux lettres et de rétention des éléments supprimés pour la boîte aux lettres liée. Ces paramètres sont configurés par défaut lors de la création de la boîte aux lettres liée. Ils utilisent les valeurs qui sont configurées pour la base de données de boîtes aux lettres et s’appliquent à toutes les boîtes aux lettres de cette base de données. Vous pouvez personnaliser ces paramètres pour chaque boîte aux lettres au lieu d’utiliser les paramètres par défaut de la base de données de boîtes aux lettres.

  - **Dernière connexion**   Cette boîte de dialogue en lecture seule affiche l’heure à laquelle l’utilisateur s’est connecté pour la dernière fois à la boîte aux lettres.

  - **Utilisation de la boîte aux lettres**   Cette zone affiche la taille totale de la boîte aux lettres et le pourcentage du quota total de boîte aux lettres qui a été utilisé.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour obtenir les informations qui sont affichées dans les deux champs précédents, le CAE interroge la base de données de boîtes aux lettres qui héberge la boîte aux lettres. Si le Centre d’administration Exchange (EAC) ne peut pas communiquer avec la banque d’informations Exchange qui contient la base de données de boîtes aux lettres, ces zones resteront vides. Un message d’avertissement s’affiche si l’utilisateur ne s’est pas connecté à la boîte aux lettres pour la première fois.</td>
</tr>
</tbody>
</table>


Cliquez sur **Plus d’options** pour afficher ou modifier les paramètres de quota de stockage de boîte aux lettres et de rétention des éléments supprimés pour la boîte aux lettres.

  - **Paramètres de quota de stockage**   Afin de personnaliser ces paramètres pour la boîte aux lettres et ne pas utiliser les valeurs par défaut de la base de données de boîtes aux lettres, cliquez sur **Personnaliser les paramètres pour cette boîte aux lettres**, saisissez une nouvelle valeur, puis cliquez sur **Enregistrer**.
    
    La plage de valeurs de tous les paramètres de quota de stockage s’étend de 0 à 2047 gigaoctets (Go).
    
      - **Émettre un avertissement à (Go)**   Ce champ affiche la limite de stockage maximale avant qu’un avertissement ne soit présenté à l’utilisateur. Si la taille de la boîte aux lettres atteint ou dépasse la valeur spécifiée, Exchange envoie un message d’avertissement à l’utilisateur.
    
      - **Interdire l’envoi à (Go)**   Ce champ affiche la limite d’*interdiction d’envoi* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l’utilisateur d’envoyer de nouveaux messages et affiche un message d’erreur descriptif.
    
      - **Interdire l’envoi et la réception à (Go)**   Ce champ affiche la limite d’*interdiction d’envoi et de réception* pour la boîte aux lettres. Si la taille de la boîte aux lettres atteint ou dépasse la limite spécifiée, Exchange empêche l’utilisateur de la boîte aux lettres d’envoyer de nouveaux messages et ne remettra plus de nouveaux messages dans la boîte aux lettres. Tous les messages envoyés à cette boîte aux lettres seront renvoyés à l’expéditeur avec un message d’erreur descriptif.

  - **Paramètres de rétention des éléments supprimés**   Afin de personnaliser ces paramètres pour la boîte aux lettres et ne pas utiliser les valeurs par défaut de la base de données de boîtes aux lettres, cliquez sur **Personnaliser les paramètres pour cette boîte aux lettres**, saisissez une nouvelle valeur, puis cliquez sur **Enregistrer**.
    
      - **Conserver les éléments supprimés pendant (jours)**   Ce champ affiche la durée pendant laquelle les éléments supprimés sont conservés avant leur suppression définitive sans récupération possible par l’utilisateur. Lors de la création de la boîte aux lettres, cette durée est basée sur les paramètres de rétention des éléments supprimés qui sont configurés pour la base de données de boîtes aux lettres. Par défaut, une base de données de boîtes aux lettres est configurée pour conserver les éléments supprimés pendant 14 jours. La plage de valeurs de cette propriété s’étend de 0 à 24 855 jours.
    
      - **Ne pas supprimer définitivement les éléments tant que la base de données n’a pas été sauvegardée**   Activez cette case à cocher pour empêcher la suppression des éléments jusqu’à la sauvegarde de la base de données de boîtes aux lettres sur laquelle la boîte aux lettres est située.

## Adresse de messagerie

Utilisez la section **Adresse de messagerie** pour afficher ou modifier les adresses de messagerie électronique associées à la boîte aux lettres liée. Adresses incluses : adresses SMTP principales de l’utilisateur et toute adresse de proxy associée. L’adresse SMTP principale (également appelée *adresse de réponse par défaut*) est affichée en gras dans la liste d’adresses, la valeur **SMTP** apparaissant en lettres majuscules dans la colonne **Type**.

  - **Ajouter **  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l’un des types d’adresses suivants :
    
      - **SMTP**   Il s’agit du type d’adresse par défaut. Cliquez sur cette case d’option, puis saisissez la nouvelle adresse SMTP dans la zone **\* Adresse de messagerie**.
    
      - **EUM**   Une adresse de messagerie unifiée Exchange est utilisée par le service de messagerie unifiée de Microsoft Exchange pour localiser des utilisateurs à extension messagerie unifiée dans une organisation Exchange. Les adresses de messagerie unifiée Exchange sont composées du numéro de poste et du plan de numérotation de messagerie unifiée de l’utilisateur à extension messagerie unifiée. Cliquez sur cette case d’option, puis saisissez le numéro de poste dans la zone **Adresse/Poste**. Cliquez ensuite sur **Parcourir** et sélectionnez un plan de numérotation pour l’utilisateur.
    
      - **Adresse personnalisée**   Cliquez sur ce bouton et saisissez dans la zone **\* Adresse de messagerie** l’un des types d’adresse de messagerie électronique non SMTP pris en charge.
        
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


  - **Mettre à jour automatiquement les adresses de messagerie en fonction de la stratégie des adresses de messagerie applicable à ce destinataire   **Activez cette case à cocher pour que les adresses de messagerie du destinataire soient automatiquement mises à jour lorsque des modifications sont apportées aux stratégies d’adresses de messagerie dans votre organisation. Cette case à cocher est activée par défaut.

## Fonctionnalités de boîte aux lettres

Dans la section **Fonctionnalités de boîte aux lettres**, vous pouvez afficher ou modifier les fonctionnalités et paramètres de boîte aux lettres suivants :

  - **Stratégie de partage**   Ce champ affiche la stratégie de partage appliquée à la boîte aux lettres. Une stratégie de partage contrôle la façon dont les utilisateurs de votre organisation peuvent partager les informations de calendrier et de contact avec des utilisateurs extérieurs à votre organisation Exchange. La stratégie de partage par défaut est attribuée aux boîtes aux lettres au moment de leur création. Pour modifier la stratégie de partage attribuée à l’utilisateur, sélectionnez-en une autre dans la liste déroulante.

  - **Stratégie d’attribution de rôle**   Ce champ affiche la stratégie d’attribution de rôle affectée à la boîte aux lettres. La stratégie d’attribution de rôle spécifie les rôles de contrôle d’accès basé sur les rôles (RBAC) qui sont attribués à l’utilisateur et contrôle les paramètres de configuration de groupe de distribution et de boîte aux lettres que les utilisateurs peuvent modifier. Pour modifier la stratégie d’attribution de rôle affectée à l’utilisateur, sélectionnez-en une autre dans la liste déroulante.

  - **Stratégie de rétention**   Ce champ affiche la stratégie de rétention attribuée à la boîte aux lettres. Une stratégie de rétention est un groupe de balises de rétention qui sont appliquées à la boîte aux lettres de l’utilisateur. Les balises vous permettent de contrôler la durée de conservation des éléments des boîtes aux lettres des utilisateurs et de définir l’action à effectuer sur les éléments qui ont atteint une certaine ancienneté. Aucune stratégie de rétention n’est attribuée aux boîtes aux lettres lorsque ces dernières sont créées. Pour attribuer une stratégie de rétention à l’utilisateur, sélectionnez-en une dans la liste déroulante.

  - **Stratégie de carnet d’adresses**   Cette zone indique la stratégie de carnet d’adresses appliquée à la boîte aux lettres. Une stratégie de carnet d’adresses vous permet de segmenter les utilisateurs dans des groupes spécifiques pour fournir des vues personnalisées du carnet d’adresses. Pour appliquer ou modifier la stratégie de carnet d’adresses appliquée à la boîte aux lettres, sélectionnez-en une dans la liste déroulante.

  - **Messagerie unifiée**   Cette fonctionnalité est désactivée par défaut. Lorsque vous activez la messagerie unifiée, l’utilisateur peut utiliser les fonctionnalités de messagerie unifiée de votre organisation et un ensemble par défaut de propriétés de messagerie unifiée est appliqué à l’utilisateur. Cliquez sur **Activer** pour activer la messagerie unifiée pour la boîte aux lettres. Pour plus d’informations sur la procédure d’activation de la messagerie unifiée, reportez-vous à la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).
    
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


  - **Périphériques mobiles**   Utilisez cette section pour afficher et modifier les paramètres d’Exchange ActiveSync, qui est activé par défaut. Exchange ActiveSync permet d’accéder à une boîte aux lettres Exchange à partir d’un appareil mobile. Cliquez sur **Désactiver Exchange ActiveSync** pour désactiver cette fonctionnalité pour la boîte aux lettres.

  - **Outlook Web App**   Cette fonctionnalité est activée par défaut. Outlook Web App permet d’accéder à une boîte aux lettres Exchange via un navigateur Web. Cliquez sur **Désactiver** pour désactiver Outlook Web App pour la boîte aux lettres. Cliquez sur **Modifier les détails** pour ajouter ou modifier une stratégie de boîte aux lettres Outlook Web App pour la boîte aux lettres.

  - **IMAP**   Cette fonctionnalité est activée par défaut. Cliquez sur **Désactiver** afin de désactiver la fonctionnalité IMAP pour la boîte aux lettres.

  - **POP3**   Cette fonctionnalité est activée par défaut. Cliquez sur **Désactiver** afin de désactiver la fonctionnalité POP3 pour la boîte aux lettres.

  - **MAPI**   Cette fonctionnalité est activée par défaut. Le protocole MAPI permet d’accéder à une boîte aux lettres Exchange à partir d’un client MAPI tel qu’Outlook. Cliquez sur **Désactiver** pour désactiver MAPI pour la boîte aux lettres.

  - **Suspension pour litige**   Cette fonctionnalité est désactivée par défaut. Une mise en attente pour litige permet de conserver les éléments supprimés d’une boîte aux lettres et enregistre les modifications apportées à ces éléments. Les éléments supprimés et tous les éléments modifiés sont renvoyés lors d’une détection. Cliquez sur **Activer** pour mettre la boîte aux lettres en suspension pour litige. Si la boîte aux lettres est suspendue pour litige, cliquez sur **Désactiver** pour supprimer la suspension pour litige. Si la boîte aux lettres est suspendue pour litige, cliquez sur **Modifier les détails** pour afficher et modifier les paramètres de suspension pour litige suivants :
    
      - **Date de suspension**   Cette zone en lecture seule indique la date et l’heure auxquelles la boîte aux lettres a été placée en suspension pour litige.
    
      - **Suspendu par**   Ce champ en lecture seule indique le nom de l’utilisateur qui a mis la boîte aux lettres en suspension pour litige.
    
      - **Remarque**   Ce champ permet d’informer l’utilisateur de la suspension pour litige, d’expliquer pourquoi la boîte aux lettres est suspendue pour litige, ou de fournir de l’aide supplémentaire à l’utilisateur, comme par exemple pour l’informer que la suspension pour litige n’affectera pas son utilisation quotidienne de la messagerie.
    
      - **URL**   Ce champ permet de saisir une URL de site Web qui fournit des informations ou de l’aide à propos de la suspension pour litige de la boîte aux lettres.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Le texte de ces zones s’affiche dans la boîte aux lettres de l’utilisateur uniquement s’il utilise Outlook 2010 ou des versions ultérieures. Il n’apparaît pas dans Outlook Web App ou d’autres clients de messagerie. Pour consulter le texte des zones Note et URL dans Outlook, cliquez sur l’onglet <strong>Fichier</strong>, et dans la page <strong>Informations</strong>, sous <strong>Paramètres du compte</strong>, vous voyez le commentaire de suspension pour litige.</td>
        </tr>
        </tbody>
        </table>


  - **Archivage**   S’il n’existe pas de boîte aux lettres d’archive pour l’utilisateur, cette fonctionnalité est désactivée. Pour activer une boîte aux lettres d’archive, cliquez sur **Activer**. Si l’utilisateur possède une boîte aux lettres d’archive, la taille de cette dernière ainsi que les statistiques d’utilisation s’affichent. Cliquez sur **Modifier les détails** pour afficher ou modifier les paramètres de boîte aux lettres d’archivage suivants :
    
      - **État**   Ce champ en lecture seule indique s’il existe ou non une boîte aux lettres d’archivage.
    
      - **Base de données**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres d’archivage.
    
      - **Nom**   Saisissez le nom de la boîte aux lettres d’archivage dans ce champ. Ce nom apparaît sous la liste de dossiers dans Outlook ou Outlook Web App.
    
      - **Utilisation du quota**   Ce champ en lecture seule affiche la taille totale de la boîte aux lettres d’archivage et le pourcentage du quota total de boîte aux lettres d’archivage qui a été utilisé.
    
      - **Valeur du quota (Go)**   Ce champ indique la taille totale de la boîte aux lettres d’archivage. Pour modifier la taille, saisissez une nouvelle valeur dans le champ ou sélectionnez une valeur dans la liste déroulante.
    
      - **Émettre un avertissement à (Go)**   Ce champ affiche la limite de stockage maximale pour la boîte aux lettres d’archivage avant qu’un avertissement ne soit présenté à l’utilisateur. Si la taille de la boîte aux lettres d’archivage atteint ou dépasse la valeur spécifiée, Exchange envoie un message d’avertissement à l’utilisateur. Pour modifier cette limite, saisissez une nouvelle valeur dans le champ ou sélectionnez une valeur dans la liste déroulante.

  - **Options de remise**   Utilisez Options de remise pour transférer à un autre destinataire les messages électroniques envoyés à l’utilisateur, mais aussi pour définir le nombre maximal de destinataires auxquels l’utilisateur peut envoyer un message. Cliquez sur **Modifier les détails** pour afficher et modifier ces paramètres.
    
      - **Adresse de transfert**   Activez la case à cocher **Activer le transfert**, puis cliquez sur **Parcourir** pour accéder à la page **Sélectionner un utilisateur de messagerie et une boîte aux lettres**. Cette page permet de sélectionner un destinataire auquel vous voulez transférer tous les messages électroniques envoyés à cette boîte aux lettres. Les messages seront remis à la boîte aux lettres liée et à l’adresse de transfert.
    
      - **Limite de destinataire**   Ce paramètre contrôle le nombre maximal de destinataires auxquels l’utilisateur peut envoyer un message. Activez la case à cocher **Nombre maximal de destinataires** pour limiter le nombre de destinataires autorisé sur les lignes À :, Cc : et Cci : d’un message électronique, puis spécifiez le nombre maximal de destinataires.
        
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


  - **Restrictions de taille des messages**   Ces paramètres contrôlent la taille des messages échangés par l’utilisateur. Cliquez sur **Modifier les détails** pour afficher et modifier la taille maximale des messages envoyés et reçus.
    
      - **Messages envoyés**   Pour spécifier une taille maximale de messages envoyés par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l’utilisateur envoie un message dont la taille est supérieure à la taille spécifiée, il est renvoyé à l’utilisateur avec un message d’erreur descriptif.
    
      - **Messages reçus**   Pour spécifier une taille maximale de messages reçus par cet utilisateur, activez la case à cocher **Taille maximale du message (Ko)** et saisissez une valeur dans le champ. La taille des messages doit être comprise entre 0 et 2 097 151 Ko. Si l’utilisateur reçoit un message dont la taille est supérieure à la taille spécifiée, le message sera renvoyé à l’expéditeur accompagné d’un message de description de l’erreur.

  - **Restrictions de remise des messages**   Ces paramètres contrôlent les expéditeurs possibles des messages électroniques envoyés à un utilisateur. Cliquez sur **Modifier les détails** pour afficher et modifier ces restrictions.
    
      - **Accepter les messages provenant de**   Cette section permet de spécifier qui peut envoyer des messages à cet utilisateur.
        
          - **Tous les expéditeurs**   Cette option permet d’indiquer que l’utilisateur peut accepter des messages de tous les expéditeurs. Sont inclus à la fois les expéditeurs de votre organisation Exchange et les expéditeurs externes. Cette option est sélectionnée par défaut. Cette option inclut les utilisateurs externes uniquement si vous désactivez la case à cocher **Exiger l’authentification de tous les expéditeurs**. Si cette case à cocher est activée, les messages des utilisateurs externes seront rejetés.
        
          - **Uniquement les expéditeurs de la liste suivante** Cette option permet d’indiquer que l’utilisateur ne peut accepter que les messages provenant d’un ensemble spécifique d’expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter** pour accéder à la page **Sélectionner les destinataires**, qui contient une liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Il est également possible de rechercher un destinataire spécifique en saisissant son nom dans le champ de recherche, puis en cliquant sur **Rechercher**.
        
          - **Exiger l’authentification de tous les expéditeurs**   Cette option permet d’empêcher les utilisateurs anonymes d’envoyer des messages à l’utilisateur.
    
      - **Rejeter les messages de**   Cette section permet d’empêcher des personnes d’envoyer des messages à cet utilisateur.
        
          - **Aucun expéditeur** Cette option permet d’indiquer que la boîte aux lettres ne rejettera les messages d’aucun expéditeur de l’organisation Exchange. Cette option est sélectionnée par défaut.
        
          - **Expéditeurs de la liste suivante** Cette option permet d’indiquer que la boîte aux lettres rejettera les messages provenant d’un ensemble spécifique d’expéditeurs de votre organisation Exchange. Cliquez sur **Ajouter** pour afficher la page **Sélectionner un destinataire**, qui contient une liste de tous les destinataires de votre organisation Exchange. Sélectionnez les destinataires dont vous souhaitez rejeter les messages, ajoutez-les à la liste, puis cliquez sur **OK**. Il est également possible de rechercher un destinataire spécifique en saisissant son nom dans le champ de recherche, puis en cliquant sur **Rechercher**.

## Membre de

La section **Membre de** permet d’afficher une liste des groupes de distribution ou de groupes de sécurité auxquels cet utilisateur appartient. Vous ne pouvez pas modifier les informations d’appartenance sur cette page. Notez que l’utilisateur peut répondre aux critères d’un ou de plusieurs groupes de distribution dynamiques de votre organisation. Toutefois, les groupes de distribution dynamiques ne s’affichent pas sur cette page car leur appartenance est calculée à chaque utilisation.

## Infos-courrier

Utilisez la section **Info courrier** pour ajouter une Info courrier afin d’alerter les utilisateurs de problèmes potentiels s’ils envoient un message à ce destinataire. Une info-courrier est un texte qui s’affiche dans la barre d’informations lorsqu’un destinataire est ajouté aux lignes À, Cc ou Cci d’un nouveau message électronique.

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

  - **Envoyer sous**   Cette autorisation permet aux utilisateurs autres que le propriétaire de la boîte aux lettres d’utiliser la boîte aux lettres pour envoyer des messages. Une fois cette autorisation attribuée à un délégué, tout message envoyé par un délégué depuis cette boîte aux lettres s’affiche comme s’il était envoyé par le propriétaire de la boîte aux lettres. Cette autorisation ne permet pas toutefois pas à un délégué de se connecter à la boîte aux lettres de l’utilisateur.

  - **Envoyer au nom de**   Cette autorisation permet également à un délégué d’utiliser cette boîte aux lettres pour envoyer des messages. Cependant, une fois cette autorisation attribuée à un délégué, l’adresse **De :**  de tous les messages envoyés par le délégué indique que le message a été envoyé par le délégué, au nom du propriétaire de la boîte aux lettres.

  - **Accès total**   Cette autorisation permet à un délégué de se connecter à la boîte aux lettres de l’utilisateur et d’afficher le contenu de la boîte aux lettres. Cependant, une fois cette autorisation attribuée à un délégué, celui-ci ne peut pas envoyer de messages depuis cette boîte aux lettres. Pour permettre à un délégué d’envoyer des courriers électroniques depuis la boîte aux lettres de l’utilisateur, vous devez attribuer au délégué l’autorisation Envoyer sous ou Envoyer au nom de.

Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter** sous l’autorisation voulue afin d’afficher la page **Sélectionner un destinataire** qui présente une liste de tous les destinataires de votre organisation Exchange auxquels peut être attribuée l’autorisation. Sélectionnez les destinataires auxquels vous souhaitez attribuer les autorisations de délégué, ajoutez-les à la liste, puis cliquez sur **OK**. Il est également possible de rechercher un destinataire spécifique en saisissant son nom dans le champ de recherche, puis en cliquant sur **Rechercher**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier les propriétés d’une boîte aux lettres liée

Utilisez les cmdlets **Get-Mailbox** et **Set-Mailbox** pour afficher et modifier les propriétés des boîtes aux lettres liées. En utilisant l’environnement de ligne de commande Exchange Management Shell, vous avez la possibilité de modifier les propriétés de plusieurs boîtes aux lettres liées. Pour plus d’informations sur les paramètres qui correspondent aux propriétés des boîtes aux lettres, consultez les rubriques suivantes :

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

Voici quelques exemples d’utilisation de l’environnement de ligne de commande Exchange Management Shell pour la modification des propriétés de boîte aux lettres liée.

Cet exemple utilise la commande **Get-Mailbox** pour rechercher toutes les boîtes aux lettres liées dans l’organisation.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')}

Cet exemple utilise la commande **Set-Mailbox** pour limiter à 500 le nombre de destinataires autorisé sur les lignes À :, Cc : et Cci : d’un message électronique. Cette limite s’applique à toutes les boîtes aux lettres liées dans l’organisation.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | Set-Mailbox -RecipientLimits 500

Cet exemple modifie le compte principal lié dans la forêt de comptes fabrikam.com qui est associée à une boîte aux lettres liée dans une forêt Exchange.

    Set-Mailbox -Identity "Ayla Kol" -LinkedDomainController DC1.fabrikam.com -LinkedMasterAccount "fabrikam\robinw" -LinkedCredential:(Get-Credential fabrikam\administrator)

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement modifié les propriétés d’une boîte aux lettres liée, procédez comme suit :

  - Dans le Centre d’administration Exchange (EAC), sélectionnez la boîte aux lettres liée, puis cliquez sur **Modifier** pour afficher la propriété ou la fonction que vous avez modifiée. Selon la propriété modifiée, elle peut être affichée dans le volet Détails de la boîte aux lettres sélectionnée.

  - Dans l’environnement Shell, utilisez la cmdlet **Get-Mailbox** pour vérifier les modifications. L’utilisation de l’environnement de ligne de commande Exchange Management Shell permet notamment d’afficher plusieurs propriétés pour plusieurs boîtes aux lettres liées. Dans l’exemple ci-dessus, où la limite de destinataires a été modifiée, l’exécution de la commande suivante permet de vérifier la nouvelle valeur.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | fl Name,RecipientLimits
    
    Dans l’exemple ci-dessus, où le compte principal lié a été modifié, exécutez la commande suivante pour vérifier la nouvelle valeur.
    
        Get-Mailbox "Ayla Kol" | fl LinkedMasterAccount

