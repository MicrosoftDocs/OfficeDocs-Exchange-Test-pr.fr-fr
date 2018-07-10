---
title: 'Création et gestion de groupes de distribution: Exchange 2013 Help'
TOCTitle: Création et gestion de groupes de distribution
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 50479183
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# Création et gestion de groupes de distribution

 

_**Sapplique à :** Exchange Online, Exchange Server 2016, Office 365_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell pour créer un groupe de distribution dans votre organisation Exchange ou pour activer la messagerie sur un groupe existant dans Active Directory.

Deux types de groupes peuvent servir à distribuer des messages :

  - Les *groupes de distribution universels à extension messagerie* (aussi appelés *groupes de distribution*) ne peuvent être utilisés que pour distribuer des messages.

  - Les *groupes de sécurité universels à extension messagerie* (aussi appelés *groupes de sécurité*) peuvent être utilisés pour distribuer des messages et accorder des autorisations d’accès aux ressources dans Active Directory. Pour plus d’informations, voir [Gérer les groupes de sécurité à extension de messagerie](manage-mail-enabled-security-groups-exchange-2013-help.md).

Il est important de noter les différences de terminologie entre Active Directory et Exchange. Dans Active Directory, un groupe de distribution correspond à tout groupe sans contexte de sécurité, qu’il soit doté d’une extension messagerie ou non. En revanche, dans Exchange, tous les groupes à extension messagerie sont appelés groupes de distribution, qu’ils aient un contexte de sécurité ou non.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Si votre organisation a configuré une stratégie de noms de groupes, elle est appliquée uniquement aux groupes créés par les utilisateurs. Lorsque vous ou un autre administrateur utilisez le CAE pour créer des groupes de distribution, la stratégie de noms de groupes est ignorée et n’est pas appliquée au nom de groupe. Toutefois, si vous utilisez l’environnement de ligne de commande Exchange Management Shell ou que vous renommez un groupe de distribution, la stratégie est appliquée sauf si vous utilisez le paramètre *IgnoreNamingPolicy* pour écraser la stratégie de noms de groupes. Pour plus d’informations, voir :
    
      - [Créer une stratégie de noms de groupe de distribution](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [Ignorer la stratégie de noms des groupes de distribution](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## Que souhaitez-vous faire ?

## Créer un groupe de distribution

## Utiliser le CAE pour créer un groupe de distribution

1.  Dans la CCE, accédez à **Destinataires** \> **Groupes**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") \> **Groupe de distribution**.

3.  > [!TIP]  
	> <img src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png" title="Nouveaux groupes d’essai Office 365" alt="Nouveaux groupes d’essai Office 365" /><br />
    > Vous pouvez désormais créer un groupe Office 365 au lieu d’un groupe de distribution si vous avez un plan Office 365 pour entreprise ou un plan Exchange Online. Les groupes Office 365 ont les fonctionnalités d’un groupe de distribution et bien plus encore. Avec les groupes Office 365, vous pouvez envoyer des messages électroniques à un groupe, partager un calendrier commun, disposer d’une bibliothèque afin de stocker des fichiers et des dossiers de groupe, et de travailler sur ces derniers. Cliquez sur <strong>Nouveau</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /> &gt; <strong>Groupe Office 365</strong> pour commencer et consultez l’article <a href="https://go.microsoft.com/fwlink/p/?linkid=800653">Groupes Office 365 - Aide pour l’administrateur</a>.<br />
    > Si vous souhaitez migrer des groupes de distribution existants vers des groupes Office 365, consultez l’article <a href="https://go.microsoft.com/fwlink/p/?linkid=824756">Migrer les listes de distribution vers des groupes Office 365 - Aide pour l’administrateur</a>.<br />
    > Si vous souhaitez quand même créer un groupe de distribution, vous pouvez cliquer ou appuyer sur l’Assistant <strong>Nouveau groupe de distribution</strong>.
    
4.  Dans la page **Nouveau groupe de distribution**, complétez les champs suivants :
    
      - \* **Nom complet**   Saisissez le nom complet. Ce nom apparaîtra dans le carnet d’adresses de votre organisation, ainsi que dans les lignes À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes du Centre d’administration Exchange. Le nom d’affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s’agit. Ce nom doit aussi être unique dans la forêt.
    
      - \* **Alias**   Saisissez le nom de l’alias du groupe. L’alias ne peut pas comporter plus de 64 caractères et doit être unique dans la forêt. Lorsqu’un utilisateur saisit l’alias dans la ligne À : d’un message électronique, sa résolution génère le nom complet du groupe.
    
      - **Unité d’organisation**   (Cette option s’affiche uniquement dans Exchange 2013 local) Vous pouvez sélectionner une unité d’organisation (UO) autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine Active Directory qui contient l’ordinateur sur lequel le CAE est exécuté. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d’organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d’organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez l’UO souhaitée, puis cliquez sur **OK**.
    
      - \* **Propriétaires**   Par défaut, la personne qui crée un groupe en est le propriétaire. Tous les groupes doivent avoir au moins un propriétaire. Vous pouvez ajouter des propriétaires en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").
    
      - **Membres**   Utilisez cette section pour ajouter des membres et pour spécifier si une approbation est nécessaire pour que des personnes rejoignent ou quittent le groupe.
        
        Les propriétaires des groupes ne doivent pas nécessairement en être membres. L’option **Ajouter les propriétaires du groupe en tant que membres** permet d’ajouter ou de supprimer les propriétaires en tant que membres.
        
        Pour ajouter des membres au groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Lorsque vous avez terminé d’ajouter des membres, cliquez sur **OK** pour retourner à la page **Nouveau groupe de distribution**.
        
        Sous **Choisissez si l’approbation du propriétaire du groupe est requise pour rejoindre ce dernier**, spécifiez si une approbation est requise pour les personnes rejoignant le groupe. Sélectionnez-en un :
        
          - **Ouverte : tout le monde peut rejoindre le groupe sans approbation des propriétaires du groupe**   Il s’agit du paramètre par défaut.
        
          - **Fermée : seuls les propriétaires du groupe peuvent ajouter des membres. Toutes les demandes visant à rejoindre le groupe sont rejetées automatiquement**
        
          - **Approbation manuelle : Toutes les demandes sont approuvées ou rejetées manuellement par les propriétaires du groupe**   Si vous sélectionnez cette option, le ou les propriétaires du groupe reçoivent un message électronique demandant l’approbation de la demande de participation au groupe.
        
        Sous **Choisir s’il est possible de quitter le groupe**, spécifiez si une approbation est requise pour les personnes quittant le groupe. Sélectionnez-en un :
        
          - **Ouverte : tout le monde peut quitter le groupe sans approbation des propriétaires du groupe**   Il s’agit du paramètre par défaut.
        
          - **Fermée : seuls les propriétaires du groupe peuvent supprimer des membres. Toutes les demandes visant à quitter le groupe sont rejetées automatiquement**   

5.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer le groupe de distribution.

> [!NOTE]  
> Par défaut, les nouveaux groupes de distribution exigent l’authentification de tous les expéditeurs. Cela empêche des expéditeurs externes d’envoyer des messages aux groupes de distribution. Pour configurer un groupe de distribution afin d’accepter des messages de tous les expéditeurs, vous devez modifier les paramètres de restriction de remise de messages pour ce groupe de distribution.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer un groupe de distribution

Cet exemple crée un groupe de distribution avec un alias **itadmin** et le nom **IT Administrators**. Le groupe de distribution est créé dans l’unité d’organisation par défaut et n’importe qui peut rejoindre ce groupe sans l’approbation des propriétaires du groupe.

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

Pour plus d’informations sur l’utilisation de l’environnement de ligne de commande Exchange Management Shell, voir [New-DistributionGroup](https://technet.microsoft.com/fr-fr/library/aa998856\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier si vous avez créé avec succès un groupe de distribution, procédez comme suit :

  - Dans la CCE, accédez à **Destinataires** \> **Groupes**. Le nouveau groupe de distribution s’affiche dans la liste de groupes. Sous **Type de groupe**, le type est **Groupe de distribution**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations sur le nouveau groupe de distribution.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

> [!NOTE]  
> Vous pouvez créer ou activer la messagerie de groupes de distribution universels uniquement. Pour convertir un groupe de domaine local ou global en groupe universel, vous pouvez utiliser la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123770(v=exchg.150)">Set-Group</a> à l’aide de l’environnement de ligne de commande. Vous disposez peut-être de groupes à extension messagerie ayant migré à partir de versions antérieures d’Exchange qui ne sont pas des groupes universels. Vous pouvez utiliser le CAE ou l’environnement de ligne de commande Exchange Management Shell pour gérer ces groupes


## Modifier les propriétés de groupe de distribution

## Utiliser le CAE pour modifier les propriétés de groupe de distribution

1.  Dans la CCE, accédez à **Destinataires** \> **Groupes**.

2.  Dans la liste des groupes, cliquez sur le groupe de distribution à afficher ou à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du groupe, cliquez sur les sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Propriété
    
      - Appartenance
    
      - Approbation d’appartenance
    
      - Gestion de la remise des messages
    
      - Approbation de messages
    
      - Options de messagerie électronique
    
      - MailTip
    
      - Délégation de groupe

## Général

Utilisez cette section pour afficher ou modifier les informations de base relatives au groupe.

  - \* **Nom complet**   Ce nom s’affiche dans le carnet d’adresses, sur les lignes À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes. Le nom d’affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s’agit. Il doit également être unique dans votre domaine.
    
    Si vous avez implémenté une stratégie de noms de groupes, le nom d’affichage doit se conformer au format de nom défini par la stratégie.

  - \* **Alias**   L’alias est la partie de l’adresse de messagerie qui apparaît à gauche du signe @. Si vous modifiez l’alias, l’adresse SMTP principale du groupe est également modifiée et contient le nouvel alias. De plus, l’adresse de messagerie électronique qui comprend l’alias précédent est gardée en tant qu’adresse de proxy du groupe.

  - **Description**   Décrivez le groupe afin que l’objet du groupe soit facilement identifiable. Cette description apparaît dans le carnet d’adresses et dans le volet d’informations du Centre d’administration Exchange.

  - **Masquer le groupe dans les listes d’adresses Exchange**   Cochez cette case si vous ne souhaitez pas que les utilisateurs voient ce groupe dans le carnet d’adresses. Pour envoyer un message électronique à ce groupe, l’expéditeur doit saisir l’alias ou l’adresse de messagerie électronique du groupe dans les lignes ou Cc :, À :.
    
    > [!TIP]
    > Envisagez de masquer des groupes de sécurité parce qu’ils sont utilisés en général pour attribuer des autorisations aux membres du groupe et ne pas envoyer de courriers électroniques.


  - **Unité d’organisation**   Ce champ en lecture seule affiche l’unité d’organisation (UO) qui contient le groupe de distribution. Vous devez utiliser des utilisateurs et ordinateurs Active Directory pour déplacer le groupe dans une autre UO.

## Propriété

Utilisez cette section pour attribuer des propriétaires du groupe. Le propriétaire du groupe peut ajouter des membres au groupe, approuver ou rejeter les demandes visant à rejoindre ou quitter le groupe, ainsi qu’approuver ou rejeter des messages envoyés au groupe. Par défaut, la personne qui crée un groupe en est le propriétaire. Tous les groupes doivent avoir au moins un propriétaire.

Vous pouvez ajouter des propriétaires en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Vous pouvez supprimer un propriétaire en le sélectionnant, puis en cliquant sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Appartenance

Utilisez cette section pour ajouter ou supprimer des membres. Les propriétaires des groupes ne doivent pas nécessairement en être membres. Sous **Membres**, vous pouvez ajouter des membres en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Vous pouvez supprimer un membre en sélectionnant un utilisateur dans la liste des membres et en cliquant sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Approbation d’appartenance

Cette section permet de spécifier si une approbation est nécessaire pour que des utilisateurs rejoignent ou quittent le groupe.

  - **Choisissez si l’approbation du propriétaire du groupe est requise pour rejoindre ce dernier**   Sélectionnez l’un des paramètres suivants :
    
      - **Ouverte : Tout utilisateur peut faire partie de ce groupe sans l’approbation des propriétaires du groupe**
    
      - **Fermée : seuls les propriétaires du groupe peuvent ajouter des membres. Toutes les demandes visant à rejoindre le groupe sont rejetées automatiquement**
    
      - **Approbation manuelle : Toutes les demandes sont approuvées ou rejetées par les propriétaires du groupe**   Si vous sélectionnez cette option, le ou les propriétaires du groupe reçoivent un message électronique demandant l’approbation de la demande de participation au groupe.

  - **Choisissez s’il est possible de quitter le groupe**   Sélectionnez l’un des paramètres suivants :
    
      - **Ouverte : Tout utilisateur peut quitter ce groupe sans l’approbation des propriétaires du groupe**  
    
      - **Fermée : seuls les propriétaires du groupe peuvent supprimer des membres. Toutes les demandes visant à quitter le groupe sont rejetées automatiquement**  

## Gestion de la remise des messages

Cette section permet de gérer les utilisateurs autorisés à envoyer des messages électroniques à ce groupe.

  - **Uniquement les expéditeurs de mon organisation**   Sélectionnez cette option pour autoriser uniquement les expéditeurs de votre organisation à envoyer des messages au groupe. Cela signifie que si quelqu'un en dehors de votre organisation envoie un courrier électronique à ce groupe, celui-ci sera rejeté. Il s’agit du paramètre par défaut.

  - **Expéditeurs internes et à l'extérieur de mon organisation**Sélectionnez cette option pour permettre à tout le monde d'envoyer des messages au groupe.
    
    Vous pouvez limiter davantage l’envoi de messages au groupe en permettant uniquement à des expéditeurs spécifiques d’envoyer des messages à ce groupe. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez au moins un destinataire. Si vous ajoutez des émetteurs à cette liste, ils seront les seuls à pouvoir envoyer des messages au groupe. Tout message envoyé par un expéditeur qui n’est pas répertorié dans la liste sera rejeté.
    
    Pour supprimer un individu ou un groupe de la liste, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").
    
    > [!NOTE]  
    > Si vous avez configuré le groupe pour qu’il accepte uniquement les messages provenant des membres de votre organisation, tous les messages électroniques provenant d’un contact de messagerie sont rejetés, que vous ayez ajouté ces contacts à cette liste ou non.


## Approbation de messages

Cette section permet de définir les options de modération du groupe. Les modérateurs approuvent ou rejettent les messages envoyés au groupe avant qu'ils atteignent les membres du groupe.

  - **Les messages envoyés à ce groupe doivent être approuvés par un modérateur**   Cette case n’est pas cochée par défaut. Si vous activez cette case à cocher, les messages entrants sont examinés par les modérateurs de groupe avant leur remise. Les modérateurs de groupe peuvent approuver ou rejeter les messages entrants.

  - **Modérateurs de communauté**   Pour ajouter des modérateurs de groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un modérateur, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"). Si vous avez coché la case « Les messages envoyés à ce groupe doivent être approuvés par un modérateur » sans sélectionner de modérateur, les messages destinés au groupe sont envoyés aux propriétaires du groupe pour approbation.

  - **Les expéditeurs qui ne demandent pas l’approbation de messages**    Pour ajouter des individus ou des groupes non soumis à la modération pour ce groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un individu ou un groupe, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Sélectionner les notifications de modération**  Cette section permet de définir la manière dont les utilisateurs sont informés de l'approbation de messages.
    
      - **Avertir tous les expéditeurs lorsque leurs messages ne sont pas approuvés**   Il s’agit du paramètre par défaut. Permet de notifier tous les expéditeurs, à l’intérieur et à l’extérieur de votre organisation, lorsque leur message n’est pas approuvé.
    
      - **Avertir les expéditeurs de votre organisation lorsque leurs messages ne sont pas approuvés**   Lorsque vous activez cette option, seules les personnes ou les groupes de votre organisation sont informés lorsqu’un message qu’ils ont envoyé au groupe n’est pas approuvé par un modérateur.
    
      - **N’avertir personne lorsqu’un message n’est pas approuvé**   Lorsque vous activez cette option, aucune notification n’est envoyée aux expéditeurs dont les messages sont rejetés par les modérateurs de groupe.

## Options de messagerie électronique

Cette section permet d’afficher ou de modifier les adresses de messagerie électronique associées au groupe. Adresses incluses : adresses SMTP principales du groupe et toute adresse de proxy associée. L’adresse SMTP principale (aussi appelée *adresse de réponse*) apparaît en gras dans la liste d’adresses, avec la valeur **SMTP** inscrite en majuscules dans la colonne **Type**.

  - **Ajouter**  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l’un des types d’adresses suivants :
    
      - **SMTP**   Il s’agit du type d’adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone \* **Adresse de messagerie**.
        
        > [!NOTE]  
        > Pour que la nouvelle adresse devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>.
    
      - **Adresse personnalisée**   Cliquez sur ce bouton et saisissez dans la zone \* **Adresse de messagerie** l’un des types d’adresse de messagerie électronique non SMTP pris en charge.
        
        > [!NOTE]  
        > À l’exception des adresses X.400, Exchange ne valide pas la mise en forme des adresses personnalisées. Vous devez veiller à ce que l’adresse personnalisée que vous spécifiez soit conforme aux exigences de mise en forme pour ce type d’adresse.


  - **Modifier**   Pour modifier une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    > [!NOTE]  
    > Pour que l’adresse existante devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>.


  - **Supprimer**   Pour supprimer une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Mettre à jour auto. les adresses selon la stratégie de destinataire**   Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d’adresses de messagerie dans votre organisation. Cette case à cocher est activée par défaut.

## MailTip

Utilisez cette section pour ajouter une info-courrier afin d’alerter les utilisateurs de problèmes potentiels s’ils envoient un message à ce groupe. Une info courrier est un texte affiché dans la barre d’informations lorsque ce groupe est ajouté aux lignes À, Cc ou Cci d’un nouveau message électronique. Par exemple, vous pourriez ajouter une info courrier aux grands groupes pour prévenir des expéditeurs potentiels que leur message sera envoyé à beaucoup de personnes.

> [!NOTE]  
> Les infos courrier peuvent comporter des balises HTML, mais les scripts ne sont pas autorisés. Une info courrier personnalisée ne doit pas comporter plus de 175 caractères affichés. Les balises HTML ne sont pas prises en compte dans cette limite.


## Délégation de groupe

Cette section permet d’attribuer des autorisations à un utilisateur (appelé *délégué*) pour lui permettre d’envoyer des messages en tant que groupe ou de la part du groupe. Vous pouvez attribuer les autorisations suivantes :

  - **Envoyer en tant que**   Cette autorisation permet au délégué d’envoyer des messages en tant que groupe. Une fois cette autorisation attribuée, le délégué a la possibilité d’ajouter le groupe dans la ligne **De** pour indiquer que le message a été envoyé par le groupe.

  - **Envoyer de la part de**   Cette autorisation permet également au délégué d’envoyer des messages au nom du groupe. Une fois l’autorisation attribuée, le délégué peut ajouter le groupe dans la ligne **De**. Le message apparaîtra comme ayant été envoyé par le groupe et indiquera qu’il a été envoyé par le délégué au nom du groupe.

Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter** sous l’autorisation voulue afin d’afficher la page **Sélectionner un destinataire** qui présente une liste de tous les destinataires de votre organisation Exchange auxquels peut être attribuée l’autorisation. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Il est également possible de rechercher un destinataire spécifique en saisissant son nom dans le champ de recherche, puis en cliquant sur **Rechercher**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier des propriétés de groupe de distribution

Utilisez les cmdlets **Get-DistributionGroup** et **Set-DistributionGroup** pour afficher et modifier les propriétés des groupes de distribution. L’utilisation de l’environnement de ligne de commande Exchange Management Shell a pour avantage de pouvoir modifier les propriétés qui ne sont pas disponibles dans le CAE et de modifier les propriétés pour plusieurs groupes. Pour plus d’informations sur les paramètres qui correspondent aux propriétés des groupes de distribution, consultez les rubriques suivantes :

  - [Get-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\))

Exemples d’utilisation de l’environnement de ligne de commande pour modifier les propriétés des groupes de distribution.

Cet exemple remplace l’adresse SMTP primaire (également appelée l’adresse de réponse) pour le groupe de distribution Seattle Employees employees@contoso.com par sea.employees@contoso.com. De plus, l’adresse de réponse précédente sera conservée en tant qu’adresse proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

Cet exemple limite à 10 mégaoctets (Mo) la taille maximale des messages pouvant être envoyés à tous les groupes de distribution de l’organisation.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

Dans cet exemple, la modération est activée pour le groupe de distribution Support technique et Joëlle est désignée comme modératrice. En outre, ce groupe de distribution modéré avertira les expéditeurs qui envoient des messages depuis l’organisation si leurs messages ne sont pas approuvés.

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

Dans cet exemple, le groupe de distribution créé par un utilisateur, Nos amis les chiens, nécessite que le gestionnaire du groupe approuve les demandes des utilisateurs pour rejoindre ce groupe. En outre, à l’aide du paramètre *BypassSecurityGroupManagerCheck*, le gestionnaire de groupe ne sera pas averti de la modification apportée aux paramètres du groupe de distribution.

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## Comment savoir si cela a fonctionné ?

Pour vérifier que les modifications des propriétés d’un groupe de distribution sont réussies, procédez comme suit :

  - Dans le Centre d’administration Exchange, sélectionnez le groupe et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonction que vous avez modifiée. En fonction de la propriété modifiée, cette dernière peut s’afficher dans le volet d’informations du groupe sélectionné.

  - Dans l’environnement Shell, utilisez la cmdlet **Get-DistributionGroup** pour vérifier les modifications. En utilisant l’environnement de ligne de commande Exchange Management Shell, vous avez l’avantage de pouvoir afficher plusieurs propriétés de plusieurs groupes. Dans l’exemple ci-dessus, où la limite de destinataires a été modifiée, exécutez la commande suivante pour vérifier la nouvelle valeur.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Dans l’exemple ci-dessus où les limites de message ont été modifiées, exécutez cette commande.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

