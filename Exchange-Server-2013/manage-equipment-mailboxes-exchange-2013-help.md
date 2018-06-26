---
title: 'Gérer les boîtes aux lettres d’équipement: Exchange 2013 Help'
TOCTitle: Gérer les boîtes aux lettres d’équipement
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 50477392
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les boîtes aux lettres d’équipement

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-10-09_

Une *boîte aux lettres d’équipement* est une boîte aux lettres de ressources affectée à une ressource spécifique autre qu’un emplacement, telle qu’un ordinateur portable, un projecteur, un microphone ou un véhicule de société. Après qu'un administrateur a créé une boîte aux lettres d'équipement, les utilisateurs peuvent facilement réserver un équipement donné en incluant la boîte aux lettres d'équipement correspondante dans la demande de réunion. Vous pouvez utiliser le CAE et l’environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres d'équipement ou en modifier les propriétés. Pour plus d’informations, consultez la rubrique [Recipients](recipients-exchange-2013-help.md).

Pour plus d’informations sur un autre type de boîte aux lettres de ressources, une boîte aux lettres de salle, consultez la page [Créer et gérer des boîtes aux lettres de salle](create-and-manage-room-mailboxes-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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

## Créer une boîte aux lettres d'équipement

## Utiliser le CAE pour créer une boîte aux lettres d’équipement

1.  Dans le CAE, accédez à **Destinataires**  \> **Ressources**.

2.  Pour créer une boîte aux lettres d’équipement, cliquez sur **Nouveau** \> **Boîte aux lettres d’équipement**. Pour créer une boîte aux lettres de salle, cliquez sur **Nouveau** \> **Boîte aux lettres de salle**.

3.  Utilisez les options de la page pour spécifier les paramètres de la nouvelle boîte aux lettres de ressources.
    
      - **\* Nom de l'équipement**   Ce champ permet de saisir le nom de l'équipement. Il s'agit du nom qui est répertorié dans la liste de boîte aux lettres de ressources dans le CAE et le carnet d'adresses de votre organisation. Ce nom est requis et il ne doit pas dépasser 64 caractères.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Même si d'autres champs décrivent les détails de la salle, par exemple, Capacité, envisagez de résumer les détails les plus importants dans le nom de l'équipement à l'aide d'une convention d'affectation des noms cohérente. Pourquoi ? Pour que les utilisateurs puissent consulter les détails facilement lorsqu'ils sélectionnent l'équipement dans le carnet d'adresses dans la demande de réunion.</td>
        </tr>
        </tbody>
        </table>
    
      - **\* Adresse de messagerie**   Une boîte aux lettres d'équipement est dotée d'une adresse de messagerie pour lui permettre de recevoir des demandes de réservation. L'adresse courriel se compose d'un alias sur le côté gauche du symbole @, qui doit être unique dans la forêt, et votre nom de domaine sur la droite. L'adresse de courriel est requise.

4.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la boîte aux lettres d'équipement.

Une fois que vous avez créé votre boîte aux lettres d’équipement, vous pouvez la modifier pour mettre à jour les informations sur les options de réservation, les infos courrier et les délégués. Consultez la section Modifier les propriétés de la boîte aux lettres d’équipement ci-dessous pour modifier les propriétés de la boîte aux lettres de salle.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une boîte aux lettres d’équipement

Cet exemple crée une boîte aux lettres d’équipement avec la configuration suivante :

  - La boîte aux lettres d’équipement réside sur la base de données de boîtes aux lettres 1.

  - Le nom de l'équipement est véhiculemotorisé2 et le nom figurera dans la LAG sous Véhicule motorisé 2.

  - L'adresse de messagerie est véhiculemotorisé2@contoso.com.

  - La boîte aux lettres se trouve dans l’unité d’organisation d’équipement.

  - Le paramètre *Equipment* indique que cette boîte aux lettres sera créée en tant que boîte aux lettres d’équipement.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier la création avec succès d'une boîte aux lettres utilisateur, procédez comme suit :

  - Dans le CAE, accédez à **Destinataires**  \> **Ressources**. La nouvelle boîte aux lettres de l’utilisateur s’affiche dans la liste de boîtes aux lettres. Sous **Type de boîte aux lettres**, le type est **Équipement**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher des informations au sujet de la nouvelle boîte aux lettres d'équipement.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Modifier les propriétés de la boîte aux lettres d'équipement

Après avoir créé une boîte aux lettres d'équipement, vous pouvez la modifier et lui définir des paramètres supplémentaires à l'aide du CAE ou de l'environnement de ligne de commande Exchange Management Shell.

## Utiliser le CAE pour modifier les propriétés des boîtes aux lettres d'équipement

1.  Dans le CAE, accédez à **Destinataires**  \> **Ressources**.

2.  Dans la liste des boîtes aux lettres de ressources, cliquez sur la boîte aux lettres d'équipement dont vous souhaitez modifier les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page de propriétés de la boîte aux lettres d'équipement, cliquez sur l’une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Délégués
    
      - Options de réservation
    
      - Informations sur le contact
    
      - Adresse de messagerie
    
      - Infos-courrier

## Général

Utilisez la section **Général** pour afficher ou modifier les informations de base sur la ressource.

  - **\* Nom de l'équipement**   Ce nom figure dans la liste de boîte aux lettres de ressources dans le CAE et le carnet d'adresses de votre organisation. Elle ne peut pas dépasser 64 caractères si vous le changez.

  - **\* Adresse de messagerie**   Ce champ en lecture seule affiche l'adresse de messagerie de la boîte aux lettres d'équipement. Vous pouvez le modifier dans la section Adresse de messagerie.

  - **Capacité**   Utilisez ce champ pour saisir le nombre maximum de personnes pouvant utiliser cette ressource, si applicable. Par exemple, si la boîte aux lettres d'équipement correspond à une voiture compacte, vous pouvez saisir **4**.

Cliquez sur **Plus d’options** pour afficher ou modifier les propriétés supplémentaires suivantes :

  - **Unité d'organisation**   Ce champ en lecture seule affiche l’unité d’organisation (UO) qui contient le compte de la boîte aux lettres d'équipement. Vous devez utiliser des Utilisateurs et ordinateurs Active Directory pour déplacer le compte vers un autre UO.

  - **Base de données de boîtes aux lettres**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres d'équipement. Utilisez la page **Migration** dans le CAE pour déplacer de la boîte aux lettres à une autre base de données.

  - **\* Alias** Ce champ permet de modifier l'alias de la boîte aux lettres d'équipement.

  - **Masquer dans les listes d’adresses Exchange**   Activez cette case à cocher pour empêcher que la boîte aux lettres d'équipement n’apparaisse dans le carnet d'adresses et les autres listes d’adresses définies dans votre organisation Exchange. Après activation de cette case à cocher, les utilisateurs peuvent encore envoyer des messages de réservation à la boîte aux lettres d'équipement en utilisant l’adresse de messagerie.

  - **Département**   Utilisez ce champ pour indiquer le nom du département auquel la ressource est associée. Vous pouvez utiliser cette propriété pour créer des conditions de destinataire pour les groupes de distribution dynamiques et des listes d'adresses.

  - **Société**   Utilisez ce champ pour indiquer la société à laquelle la ressource est associée. Comme la propriété de département, vous pouvez utiliser cette propriété pour créer des conditions de destinataire pour les groupes de distribution dynamiques et des listes d'adresses.

  - **Stratégie de carnet d’adresses**   Cette option permet de spécifier une stratégie de carnet d’adresses pour la ressource. Les stratégies de carnet d’adresses contiennent une liste d’adresses globale, un carnet d’adresses en mode hors connexion, une liste de salles et un ensemble de listes d’adresses. Pour en savoir plus, consultez la rubrique [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).
    
    Dans la liste déroulante, sélectionnez la règle que vous souhaitez associer à cette boîte aux lettres.

  - **Attributs personnalisés**   Cette section affiche les attributs personnalisés définis pour la boîte aux lettres d'équipement. Pour spécifier des valeurs d’attribut personnalisées, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Vous pouvez spécifier jusqu’à 15 attributs personnalisés pour le destinataire.

## Délégués

Utilisez cette section pour afficher ou modifier la façon dont la boîte aux lettres d'équipement traite les demandes de réservation, et pour définir qui peut accepter ou refuser les demandes de réservation (si cela ne se fait pas automatiquement).

  - **Demandes de réservation**    Sélectionnez l'une des options suivantes pour gérer les demandes de réservation.
    
      - **Accepter ou refuser les demandes de réservation automatiquement**   Une demande de réunion valide réserve automatiquement la salle. S'il y a un conflit de planification avec une réservation existante, ou si la demande de réservation viole les limites de planification de la salle, par exemple, si la durée de réunion est trop longue, la demande de réunion est refusée automatiquement.
    
      - **Sélectionner des délégués qui peuvent accepter ou refuser des demandes de réservation**   Les délégués des ressources sont chargés d'accepter ou de refuser les demandes de réunion qui sont envoyées à la boîte aux lettres d'équipement. Si vous attribuez plusieurs délégués de ressources, un seul d'entre eux doit agir sur une demande de réunion spécifique.

  - **Délégués**   Si vous avez sélectionné l'option exigeant que les demandes de réservation soient envoyées aux délégués, utilisez cette section pour sélectionner les délégués. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") ou **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour ajouter ou supprimer des délégués de cette liste.

## Options de réservation

La section **Options de réservation** permet d'afficher ou de modifier les paramètres de la stratégie de réservation qui définit à quel moment les ressources peuvent être planifiées, la durée de leur réservation et le nombre de jours à l'avance selon lequel la réservation peut s'effectuer.

  - **Autoriser les réunions périodiques**   Ce paramètre autorise ou interdit les réunions périodiques pour la ressource. Par défaut, ce paramètre est activé, de sorte que les réunions périodiques sont autorisées.

  - **Autoriser la planification uniquement pendant les heures de travail**   Ce paramètre accepte ou refuse les demandes de réunion en dehors des heures de travail définies pour la ressource. Par défaut, ce paramètre est désactivé, les demandes de réunion sont autorisées en dehors des heures de travail. Par défaut, les heures de travail sont 8 h à 17 h, du lundi au vendredi. Vous pouvez configurer les heures de travail de la boîte aux lettres d'équipement dans la section Apparence de la page Calendrier.

  - **Toujours refuser si la date de fin est au-delà de cette limite**   Ce paramètre contrôle le comportement de réunions répétitives qui s'étendent au-delà de la date spécifiée par le réglage de l'heure de réservation maximale.
    
      - Si vous activez ce paramètre, une demande de réservation régulière est automatiquement refusée si les réservations commencent le ou avant la date spécifiée par la valeur de **Durée maximale de réservation**, et s'étendent au-delà de la date spécifiée. Il s’agit du paramètre par défaut.
    
      - Si vous désactivez ce paramètre, une demande de réservation régulière est automatiquement acceptée si les demandes de réservation commencent le ou avant la date spécifiée par la valeur de **Durée maximale de réservation**, et s'étendent au-delà de la date spécifiée. Cependant, le nombre de réunions est réduit de sorte que celles-ci n'auront pas lieu après la date spécifiée.

  - **Durée maximale de réservation (jours)**   Ce paramètre indique le nombre de jours maximum en fonction duquel la ressource peut être réservée à l'avance. Une entrée valide est un entier compris entre 0 et 1080. La valeur par défaut est 180 jours.

  - **Durée maximale (heures)**   Ce paramètre indique la durée maximale de réservation de la ressource dans une demande de réservation. La valeur par défaut est 24 heures.
    
    Pour les réunions périodiques, la durée maximale de la réunion s'applique à la durée de chaque instance de la réunion.

Cette page contient également un champ que vous pouvez utiliser pour rédiger un message à l'intention des utilisateurs qui envoient des demandes de réunion pour réserver la ressource.

## Informations sur le contact

La section **Informations sur le contact** permet d’afficher ou de modifier les informations de contact de la ressource. L'information sur cette page s'affiche dans le carnet d'adresses.

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


## Adresse de messagerie

La section **Adresse de messagerie** permet d’afficher ou de modifier les adresses de messagerie électronique associées à la boîte aux lettres d'équipement. Cela inclut l'adresse SMTP principale de la boîte aux lettres et toutes les adresses proxy associées. L’adresse SMTP principale (aussi appelée *adresse de réponse*) apparaît en gras dans la liste d’adresses, avec la valeur **SMTP** inscrite en majuscules dans la colonne **Type**.

  - **Ajouter **  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une nouvelle adresse de messagerie électronique pour cette boîte aux lettres. Sélectionnez l’un des types d’adresses suivants :
    
      - **SMTP**   Il s’agit du type d’adresse par défaut. Cliquez sur ce bouton, puis saisissez la nouvelle adresse SMTP dans la zone **\* Adresse de messagerie**.
    
      - **EUM**   Une adresse de messagerie unifiée Exchange est utilisée par le service de messagerie unifiée de Microsoft Exchange pour localiser des utilisateurs à extension messagerie unifiée dans une organisation Exchange. Les adresses de messagerie unifiée Exchange sont composées du numéro de poste et du plan de numérotation de messagerie unifiée de l’utilisateur à extension messagerie unifiée. Cliquez sur ce bouton puis tapez le numéro de poste dans le champ **Adresse/Poste**. Puis cliquez sur **Parcourir**, puis sélectionnez un plan de numérotation pour la boîte aux lettres.
    
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
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lorsque vous ajoutez une adresse électronique, vous avez la possibilité d'en faire l'adresse SMTP principale.</td>
    </tr>
    </tbody>
    </table>


  - **Mettre à jour auto. les adresses selon la stratégie de destinataire   **Cochez cette case pour que les adresses de messagerie du destinataire soient automatiquement mises à jour en fonction des modifications apportées aux stratégies d’adresses de messagerie dans votre organisation.

## Infos-courrier

Dans la section **Info-courrier**, vous pouvez ajouter une info-courrier pour alerter les utilisateurs d’éventuels problèmes avant qu’ils n’envoient une demande de réservation à la boîte aux lettres d'équipement. Une info-courrier est un texte qui s’affiche dans la barre d’informations lorsque ce destinataire est ajouté aux champs À, Cc ou Cci d’un nouveau message électronique.

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


## Utiliser le l’environnement de ligne de commande Exchange Management Shell pour modifier les propriétés des boîtes aux lettres d'équipement

Utilisez les ensembles suivants de cmdlets pour afficher et modifier les propriétés de la boîte aux lettres d'équipement : les cmdlets **Get-Mailbox** et**Set-Mailbox** pour afficher et modifier les propriétés générales et les adresses de messagerie de la boîte aux lettres d'équipement. Utilisez les cmdlets **Get-CalendarProcessing** et **Set-CalendarProcessing** pour afficher et modifier les délégués et les options de réservation.

  - **Get-User** et **Set-User**   Utilisez ces cmdlets pour afficher et définir les propriétés générales, telles que les noms de la société et du département.

  - **Get-Mailbox** et **Set-Mailbox**   Utilisez ces cmdlets pour afficher et définir les propriétés de boîtes aux lettres, telles que les adresses courriels et la base de données de boîtes aux lettres.

  - Utilisez les cmdlets **Get-CalendarProcessing** et **Set-CalendarProcessing** pour afficher et définir les délégués et les options de réservation.

Pour plus d'informations à propos de ces cmdlets, consultez les rubriques suivantes :

  - [Get-User](https://technet.microsoft.com/fr-fr/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/fr-fr/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/fr-fr/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/fr-fr/library/dd335046\(v=exchg.150\))

Voici quelques exemples d'utilisation de l’environnement de ligne de commande Exchange Management Shell pour modifier des propriétés de la boîte aux lettres d'équipement.

Cet exemple indique comment modifier le nom d'affichage et l'adresse SMTP principale (appelées adresse de réponse par défaut) de la boîte aux lettres d'équipement ParcAuto 1. L'adresse de réponse précédente est conservée comme adresse proxy.

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

Cet exemple explique comment configurer les boîtes aux lettres d'équipement pour autoriser la planification des demandes de réservation uniquement pendant les heures de travail.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

Dans cet exemple, la cmdlet **Get-User** est utilisée pour trouver toutes les boîtes aux lettres d'équipement du département Audiovisuel, puis la cmdlet **Set-CalendarProcessing** permet d'envoyer des demandes de réservation à une déléguée, appelée Ann Beebe, pour qu'elle les accepte ou les refuse.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié les propriétés d'une boîte aux lettres d'équipement, procédez comme suit :

  - Dans le CAE, sélectionnez la boîte aux lettres puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonction modifiée. Selon la propriété modifiée, elle peut être affichée dans le volet Détails de la boîte aux lettres sélectionnée.

  - Dans l'environnement Shell, utilisez la cmdlet **Get-Mailbox** pour vérifier les modifications. L'utilisation du Shell permet d'afficher plusieurs propriétés pour plusieurs boîtes aux lettres. Dans l'exemple ci-dessus, où les demandes de réunion ne pouvaient être planifiées que pendant les heures de travail, exécutez la commande suivante pour vérifier la nouvelle valeur.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

