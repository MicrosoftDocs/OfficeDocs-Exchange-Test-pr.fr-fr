---
title: 'Gérer les groupes de sécurité à extension de messagerie: Exchange 2013 Help'
TOCTitle: Gérer les groupes de sécurité à extension de messagerie
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 50477342
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les groupes de sécurité à extension de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-10-04_

Un groupe de sécurité à extension messagerie peut être utilisé pour distribuer des messages et accorder des autorisations d’accès aux ressources dans Active Directory. Pour plus d’informations, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Création d’un groupe de sécurité à extension messagerie

## Utiliser l’EAC pour créer un groupe de sécurité

1.  Dans la CCE, accédez à **Destinataires** \> **Groupes**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") \> **Groupe de sécurité**.

3.  Sur la page **Nouveau groupe de sécurité**, renseignez les champs suivants :
    
      - **\* Nom complet**   Saisissez le nom complet. Ce nom apparaît dans le carnet d’adresses partagé, dans la ligne À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes du Centre d’administration Exchange. Le nom d'affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s'agit. Ce nom doit aussi être unique dans la forêt.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Si une stratégie d’attribution de noms de groupe est appliquée, vous devez respecter les contraintes d’attribution de noms en vigueur dans votre organisation. Pour plus d’informations, consultez la rubrique <a href="create-a-distribution-group-naming-policy-exchange-2013-help.md">Créer une stratégie de noms de groupe de distribution</a>. Si vous souhaitez remplacer la stratégie d’attribution de noms de groupe de votre organisation, consultez la rubrique <a href="override-the-distribution-group-naming-policy-exchange-2013-help.md">Ignorer la stratégie de noms des groupes de distribution</a>.</td>
        </tr>
        </tbody>
        </table>
    
      - **\* Alias**   Dans cette boîte, entrez l’alias du groupe de sécurité. L’alias ne peut pas comporter plus de 64 caractères et doit être unique dans la forêt. Lorsqu’un utilisateur entre l’alias sur la ligne À : d’un message électronique, sa résolution génère le nom complet du groupe.
    
      - **Description**   Dans cette boîte, décrivez le groupe de sécurité afin que l’objet du groupe soit facilement identifiable.
    
      - **Unité d’organisation**   Vous pouvez sélectionner une unité d’organisation (UO) autre que celle définie par défaut (qui est la portée du destinataire). Si la portée du destinataire est définie dans la forêt, la valeur par défaut est définie sur le conteneur Utilisateurs du domaine Active Directory qui contient l’ordinateur sur lequel le CAE est exécuté. Si la portée du destinataire est définie sur un domaine spécifique, le conteneur Users de ce domaine est sélectionné par défaut. Si la portée du destinataire est définie sur une unité d’organisation (UO) spécifique, cette UO est sélectionnée par défaut.
        
        Pour sélectionner une autre UO, cliquez sur **Parcourir**. La boîte de dialogue affiche toutes les unités d’organisation de la forêt qui se trouvent dans la portée indiquée. Sélectionnez le nœud passif, puis cliquez sur **OK**.
    
      - **\* Propriétaires**   Par défaut, la personne qui crée un groupe en est le propriétaire. Tous les groupes doivent avoir au moins un propriétaire. Pour ajouter des propriétaires, cliquez sur **Ajouter**.
    
      - **Membres**   Utilisez cette section pour ajouter des membres et pour spécifier si une approbation est nécessaire pour que des personnes rejoignent ou quittent le groupe.
        
        Les propriétaires des groupes ne doivent pas nécessairement en être membres. L'option **Ajouter les propriétaires du groupe en tant que membres** permet d'ajouter ou de supprimer les propriétaires en tant que membres.
        
        Pour ajouter des membres au groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Lorsque vous avez fini d’ajouter des membres, cliquez sur **OK** pour retourner à la page **Nouveau groupe de sécurité**.
        
        Activez la case à cocher **L’approbation du propriétaire est obligatoire** pour que les propriétaires du groupe reçoivent les demandes des utilisateurs pour rejoindre le groupe. Si vous sélectionnez cette option, les membres ne peuvent être supprimés que par les propriétaires du groupe.

4.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer le groupe de sécurité.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, tous les nouveaux groupes de sécurité à extension messagerie nécessitent l’authentification de tous les utilisateurs. En procédant de la sorte, des expéditeurs externes ne peuvent pas envoyer de messages aux groupes de sécurité à extension messagerie. Pour configurer un groupe de sécurité à extension messagerie afin qu’il accepte des messages de tous les expéditeurs, vous devez modifier les paramètres de restriction de remise de messages pour ce groupe.</td>
</tr>
</tbody>
</table>


## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour créer un groupe de distribution

Dans cet exemple, nous créons un groupe de sécurité avec un alias fsadmin et le nom File Server Managers (Gestionnaires du serveur de fichiers). Le groupe de sécurité est créé sur l’unité d'organisation et tout utilisateur peut rejoindre ce groupe avec l’approbation des propriétaires du groupe.

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

Pour plus d’informations sur l’utilisation de l’environnement de ligne de commande Exchange Management Shell pour créer des groupes de sécurité à extension messagerie, consultez la rubrique [New-DistributionGroup](https://technet.microsoft.com/fr-fr/library/aa998856\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la création d’un groupe de sécurité à extension messagerie s’est correctement effectuée, procédez comme suit :

  - Dans la CCE, accédez à **Destinataires** \> **Groupes**. Le nouveau groupe de sécurité à extension messagerie est affiché dans la liste des groupes. Sous **Type de groupe**, le type est **Groupe de sécurité**.

  - Dans l’environnement Shell, exécutez la commande suivante pour afficher des informations sur le nouveau groupe de sécurité à extension messagerie.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Modifier les propriétés du groupe de sécurité à extension messagerie

## Utilisez l'EAC pour modifier les propriétés du groupe de sécurité à extension messagerie

1.  Dans la CCE, accédez à **Destinataires** \> **Groupes**.

2.  Dans la liste des groupes, cliquez sur le groupe de sécurité que vous souhaitez afficher et modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du groupe, cliquez sur les sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Propriété
    
      - Appartenance
    
      - Approbation d'appartenance
    
      - Gestion de la remise des messages
    
      - Approbation de messages
    
      - Options de messagerie électronique
    
      - MailTip
    
      - Délégation de groupe

## Général

Utilisez cette section pour afficher ou modifier les informations de base relatives au groupe.

  - **\* Nom complet**   Ce nom s'affiche dans le carnet d'adresses, sur les lignes À : quand un message électronique est envoyé à ce groupe, et dans la liste Groupes. Le nom d'affichage est obligatoire et doit être convivial afin que les personnes identifient facilement de quoi il s'agit. Il doit également être unique dans votre domaine.

  - **\* Alias**   L’alias est la partie de l’adresse de messagerie qui apparaît à gauche du signe @. Si vous modifiez l’alias, l’adresse SMTP principale du groupe est également modifiée et contient le nouvel alias. De plus, l’adresse de messagerie électronique qui comprend l’alias précédent est gardée en tant qu’adresse de proxy du groupe.

  - **Description**   Décrivez le groupe afin que l’objet du groupe soit facilement identifiable. Cette description apparaît dans le carnet d’adresses et dans le volet d’informations du Centre d’administration Exchange.

  - **Masquer le groupe dans les listes d’adresses Exchange**   Cochez cette case si vous ne souhaitez pas que les utilisateurs voient ce groupe dans le carnet d’adresses. Si cette case à cocher est activée, l’expéditeur doit entrer l’alias ou l’adresse de messagerie électronique du groupe dans les lignes À : ou Cc: pour envoyer des messages au groupe.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Envisagez de masquer des groupes de sécurité parce qu'ils sont utilisés en général pour attribuer des autorisations aux membres du groupe et ne pas envoyer de courriers électroniques.</td>
    </tr>
    </tbody>
    </table>


  - **Unité d’organisation**   Cette boîte en lecture seule affiche l’unité d’organisation contenant le groupe de sécurité. Vous devez utiliser des utilisateurs et ordinateurs Active Directory pour déplacer le groupe dans une autre UO.

## Propriété

Utilisez cette section pour attribuer des propriétaires du groupe. Le propriétaire du groupe peut ajouter des membres au groupe et approuver ou rejeter des demandes de rejoindre le groupe. Par défaut, la personne qui crée un groupe en est le propriétaire. Tous les groupes doivent avoir au moins un propriétaire.

Vous pouvez ajouter des propriétaires en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Vous pouvez supprimer un propriétaire en le sélectionnant, puis en cliquant sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Appartenance

Utilisez cette section pour ajouter ou supprimer des membres. Les propriétaires des groupes ne doivent pas nécessairement en être membres. Sous **Membres**, vous pouvez ajouter des membres en cliquant sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Vous pouvez supprimer un membre en sélectionnant un utilisateur dans la liste des membres et en cliquant sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

## Approbation d'appartenance

Cette section permet de spécifier si une approbation du propriétaire est nécessaire pour permettre à des utilisateurs de rejoindre le groupe. Si vous activez la case à cocher **L’approbation du propriétaire est obligatoire**, le ou les propriétaires du groupe reçoivent un message électronique demandant d’approuver la demande de rejoindre le groupe. Comme mentionné précédemment, seuls les propriétaires peuvent supprimer des membres du groupe.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette option ne fonctionne pas avec les groupes de sécurité avec messagerie en raison des limitations relatives à la sécurité.</td>
</tr>
</tbody>
</table>


## Gestion de la remise des messages

Cette section permet de gérer les utilisateurs autorisés à envoyer des messages électroniques à ce groupe.

  - **Uniquement les expéditeurs de mon organisation**   Sélectionnez cette option pour autoriser uniquement les expéditeurs de votre organisation à envoyer des messages au groupe. Cela signifie que si quelqu'un en dehors de votre organisation envoie un courrier électronique à ce groupe, celui-ci sera rejeté. Il s’agit du paramètre par défaut.

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

  - **Modérateurs de communauté**   Pour ajouter des modérateurs de groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un modérateur, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression"). Si vous avez activé la case à cocher « Les messages envoyés à ce groupe doivent être approuvés par un modérateur » sans sélectionner de modérateur, les messages destinés au groupe sont envoyés aux propriétaires du groupe pour approbation.

  - **Les expéditeurs qui ne demandent pas l’approbation de messages**   Pour ajouter des individus ou des groupes non soumis à la modération pour ce groupe, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un individu ou un groupe, sélectionnez-le, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Sélectionner les notifications de modération   **Cette section permet de définir la manière dont les utilisateurs sont informés de l'approbation de messages.
    
      - **Avertir tous les expéditeurs lorsque leurs messages ne sont pas approuvés**   Il s’agit du paramètre par défaut. Les expéditeurs intérieur et extérieur à votre organisation sont avertis que leurs messages ne sont pas approuvés.
    
      - **Avertir les expéditeurs de votre organisation lorsque leurs messages ne sont pas approuvés**   Lorsque vous activez cette option, seules les personnes ou les groupes de votre organisation sont informés lorsqu'un message qu'ils ont envoyé au groupe n'est pas approuvé par un modérateur.
    
      - **N’avertir personne lorsqu’un message n’est pas approuvé**   Lorsque vous activez cette option, aucune notification n’est envoyée aux expéditeurs dont les messages sont rejetés par les modérateurs de groupe.

## Options de messagerie électronique

Cette section permet d’afficher ou de modifier les adresses de messagerie électronique associées au groupe. Adresses incluses : adresses SMTP principales du groupe et toute adresse de proxy associée. L’adresse SMTP principale (aussi appelée *adresse de réponse*) apparaît en gras dans la liste d’adresses, avec la valeur **SMTP** inscrite en majuscules dans la colonne **Type**.

  - **Ajouter **  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l’un des types d’adresses suivants :
    
      - **SMTP**   Il s’agit du type d’adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone **\* Adresse de messagerie**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Pour que la nouvelle adresse devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>. Cette case à cochée n’apparaît que lorsque la case à cocher <strong>Mettre à jour automatiquement les adresses de messagerie en fonction de la stratégie des adresses de messagerie applicable à ce destinataire</strong> n’est pas sélectionnée.</td>
        </tr>
        </tbody>
        </table>
    
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


  - **Modifier**   Pour modifier une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour que l’adresse existante devienne l’adresse SMTP principale de ce groupe, cochez la case <strong>Définir comme adresse de réponse</strong>. Comme nous l’avons précédemment mentionné, cette case à cochée n’apparaît que lorsque la case à cocher <strong>Mettre à jour automatiquement les adresses de messagerie en fonction de la stratégie des adresses de messagerie applicable à ce destinataire</strong> n’est pas sélectionnée.</td>
    </tr>
    </tbody>
    </table>


  - **Supprimer**   Pour supprimer une adresse de messagerie électronique associée au groupe, sélectionnez-la dans la liste, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

  - **Mettre à jour auto. les adresses selon la stratégie de destinataire   **Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d’adresses de messagerie dans votre organisation. Cette case à cocher est activée par défaut.

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

  - **Envoyer de la part de**   Cette autorisation permet également au délégué d’envoyer des messages au nom du groupe. Une fois l'autorisation attribuée, le délégué peut ajouter le groupe dans la ligne **De**. Le message apparaîtra comme ayant été envoyé par le groupe et indiquera qu’il a été envoyé par le délégué au nom du groupe.

Pour attribuer des autorisations à des délégués, cliquez sur **Ajouter** sous l’autorisation voulue afin d’afficher la page **Sélectionner un destinataire** qui présente une liste de tous les destinataires de votre organisation Exchange auxquels peut être attribuée l’autorisation. Sélectionnez les destinataires voulus, ajoutez-les à la liste, puis cliquez sur **OK**. Vous pouvez également rechercher un destinataire spécifique en tapant son nom dans la zone de recherche et en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche").

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier les propriétés du groupe de sécurité

Utilisez les cmdlets **Get-DistributionGroup** et **Set-DistributionGroup** pour afficher et modifier les propriétés pour les groupes de sécurité. L’utilisation de l’environnement Shell offre les avantages de pouvoir modifier les propriétés qui ne sont pas accessibles dans l’EAC et de modifier des propriétés pour plusieurs groupes de sécurité. Pour plus d’informations sur les paramètres qui correspondent aux propriétés du groupe de distribution, consultez les rubriques suivantes :

  - [Get-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/fr-fr/library/bb124955\(v=exchg.150\))

Voici quelques exemples d’utilisation de l’environnement Shell pour modifier des propriétés du groupe de sécurité.

Dans cet exemple, nous affichons la liste de tous les groupes de sécurité de l’organisation.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

Dans cet exemple, nous modifions l’adresse SMTP principale (également appelée adresse de réponse) du groupe de sécurité Seattle Administrators de admins@contoso.com pour seattle.admins@contoso.com. L’adresse de réponse précédente est conservée comme une adresse proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

Dans cet exemple, nous masquons tous les groupes de sécurité de l’organisation du carnet d’adresses.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que la modification des propriétés pour un groupe de sécurité s’est correctement effectuée, procédez comme suit :

  - Dans le Centre d’administration Exchange, sélectionnez le groupe et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonction que vous avez modifiée. En fonction de la propriété modifiée, cette dernière peut s’afficher dans le volet d’informations du groupe sélectionné.

  - Dans l'environnement Shell, utilisez la cmdlet **Get-DistributionGroup** pour vérifier les modifications. En utilisant l’environnement de ligne de commande Exchange Management Shell, vous avez l’avantage de pouvoir afficher plusieurs propriétés de plusieurs groupes. Dans l’exemple ci-dessus, où tous les groupes de sécurité ont été masqués dans le carnet d’adresses, exécutez la commande suivante pour vérifier la nouvelle valeur.
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


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

