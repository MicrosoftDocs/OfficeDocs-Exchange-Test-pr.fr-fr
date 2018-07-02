---
title: 'Créer et gérer des boîtes aux lettres de salle: Exchange 2013 Help'
TOCTitle: Créer et gérer des boîtes aux lettres de salle
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50477355
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer et gérer des boîtes aux lettres de salle

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-02-02_

Durée d'exécution estimée : 5 minutes.

Une boîte aux lettres de salle est une boîte aux lettres de ressources affectée à un emplacement physique, comme une salle de conférence, un auditorium ou une salle de formation. Dès lors qu'un administrateur a créé des boîtes aux lettres de salles, les utilisateurs peuvent réserver facilement des salles en incluant des boîtes aux lettres de salles dans les demandes de réunion. Pour plus d’informations, voir [Recipients](recipients-exchange-2013-help.md).

Pour plus d’informations sur un autre type de boîte aux lettres de ressources, voir [Gérer les boîtes aux lettres d’équipement](manage-equipment-mailboxes-exchange-2013-help.md).

## Que souhaitez-vous faire ?

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous exécutez Exchange 2013 dans un scénario hybride, veillez à créer les boîtes aux lettres de salle à l’emplacement approprié. Créez vos boîtes aux lettres de salle pour votre organisation locale sur site ; les boîtes aux lettres de salle pour le côté Exchange Online doivent quant à elles être créées dans le nuage.</td>
</tr>
</tbody>
</table>



## Créer une boîte aux lettres de salle

## Utiliser le Centre d’administration Exchange pour créer une boîte aux lettres de salle

1.  Dans le Centre d’administration Exchange, accédez à **Destinataires** \> **Ressources**.

2.  Pour créer une boîte aux lettres de salle, cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") \> **Boîte aux lettres de salle**.

3.  Utilisez les options de la page pour spécifier les paramètres de la nouvelle boîte aux lettres de ressources.
    
      - **\* Nom de la salle**   Ce champ permet de saisir un nom pour l’utilisateur. Il s’agit du nom qui est répertorié dans la liste de boîtes aux lettres de ressources dans le CAE et le carnet d’adresses de votre organisation. Ce nom est requis et il ne doit pas dépasser 64 caractères.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Même si d'autres champs décrivent les détails de la salle, par exemple, Emplacement et Capacité, envisagez de résumer les détails les plus importants dans le nom de la salle à l'aide d'une convention d'affectation des noms cohérente. Pourquoi ? Pour que les utilisateurs puissent consulter les détails facilement lorsqu'ils sélectionnent la salle dans le carnet d'adresses dans la demande de réunion.</td>
        </tr>
        </tbody>
        </table>
    
      - **\* Adresse de messagerie**   Une boîte aux lettres de salle comporte une adresse de messagerie afin de recevoir des demandes de réservation. L'adresse courriel se compose d'un alias sur le côté gauche du symbole @, qui doit être unique dans la forêt, et votre nom de domaine sur la droite. L'adresse de courriel est requise.
    
      - **Emplacement**, **Téléphone**, **Capacité**   Vous pouvez utiliser ces champs pour entrer des détails à propos de la salle. Toutefois, comme expliqué précédemment, vous pouvez inclure une partie ou l'ensemble des informations dans le nom de la salle afin que les utilisateurs puissent les voir.

4.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la boîte aux lettres de salle.

Une fois que vous avez créé votre boîte aux lettres de salle, vous pouvez la modifier pour mettre à jour les informations sur les options de réservation, les infos courrier et la délégation de boîte aux lettres. Consultez la section Utiliser le centre d’administration Exchange ci-dessous pour modifier les propriétés de la boîte aux lettres de salle

## Utiliser Exchange PowerShell pour créer une boîte aux lettres de salle

Cet exemple crée une boîte aux lettres de salle avec la configuration suivante :

  - La boîte aux lettres de salle se trouve sur la base de données de boîtes aux lettres 1.

  - Le nom de la boîte aux lettres est Salleconf1. Ce nom servira à créer l'adresse de messagerie de la salle.

  - Le nom complet dans le Centre d’administration Exchange et le carnet d’adresses sera Salle de conférence 1.

  - Le paramètre de commutateur *Room* indique que cette boîte aux lettres sera créée en tant que boîte aux lettres de salle.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Vous pouvez vous assurer que vous avez correctement créé la boîte aux lettres de salle de deux façons différentes :

  - Dans le Centre d’administration Exchange, accédez à **Destinataires** \> **Ressources**. La nouvelle boîte aux lettres de salle s’affiche dans la liste des boîtes aux lettres. Sous **Type de boîte aux lettres**, le type est **Salle**.

  - Dans Exchange PowerShell, exécutez la commande suivante pour afficher les informations sur la nouvelle boîte aux lettres de salle.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Créer une liste de salles

Si vous prévoyez d’avoir plus d’une centaine de salles, ou si vous en avez déjà créé plus d’une centaine, utilisez une liste de salles pour vous aider à les organiser. Si votre société dispose de plusieurs bâtiments avec des salles qui peuvent être réservées pour des réunions, la création de listes de salles pour chaque bâtiment peut s’avérer utile. Les listes de salles sont des groupes de distribution spécifiquement marqués que vous pouvez utiliser de la même façon que les groupes de distribution. Cependant, vous ne pouvez créer des listes de salles qu’avec l’environnement de ligne de commande Exchange Management Shell.

## Utiliser Exchange PowerShell pour créer une liste de salles

Cet exemple crée une liste de salles pour le bâtiment 32.

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## Utiliser Exchange PowerShell pour ajouter une salle à la liste de salles

Cet exemple ajoute confroom3223 à la liste de salles du bâtiment 32.

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## Utiliser Exchange PowerShell pour convertir un groupe de distribution en liste de salles

Vous avez peut-être déjà créé des groupes de distribution qui contiennent vos salles de conférence. Vous n’avez pas besoin de les recréer. Nous pouvons les convertir rapidement en liste de salles.

Cet exemple convertit le groupe de distribution, les salles de conférence du bâtiment 34, en liste de salles.

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## Modifier les propriétés d'une boîte aux lettres de salle

Après avoir créé une boîte aux lettres de salle, vous pouvez la modifier et définir des propriétés supplémentaires en utilisant le Centre d’administration Exchange (CAE) ou Exchange PowerShell.

## Utiliser le Centre d’administration Exchange pour modifier les propriétés d’une boîte aux lettres de salle

1.  Dans le Centre d’administration Exchange, accédez à **Destinataires** \> **Ressources**.

2.  Dans la liste des boîtes aux lettres de ressources, sélectionnez la boîte aux lettres de salle dont vous souhaitez modifier les propriétés, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page Propriétés de la boîte aux lettres de page, cliquez sur une des sections suivantes pour afficher ou modifier les propriétés.
    
      - Général
    
      - Délégués
    
      - Options de réservation
    
      - Informations sur le contact
    
      - Adresse de messagerie
    
      - Infos-courrier

## Général

Utilisez la section **Général** pour afficher ou modifier les informations de base sur la ressource.

  - **\* Nom de la salle**   Ce nom est affiché dans la liste de boîtes aux lettres de ressources du Centre d’administration Exchange (CAE) et dans le carnet d’adresses de votre organisation. Elle ne peut pas dépasser 64 caractères si vous le changez.

  - **\* Adresse de messagerie**   Ce champ en lecture seule affiche l'adresse de messagerie du la boîte aux lettres de salle. Vous pouvez le modifier dans la section Adresse de messagerie.

  - **Capacité**   Entrez dans cette case le nombre maximal de personnes qui peuvent occuper la salle en sécurité.

Cliquez sur **Plus d’options** pour afficher ou modifier les propriétés supplémentaires suivantes :

  - **Unité d'organisation**   Ce champ en lecture seule affiche l’unité d’organisation (UO) qui contient le compte de la boîte aux lettres de la salle. Vous devez utiliser des Utilisateurs et ordinateurs Active Directory pour déplacer le compte vers un autre UO.

  - **Base de données de boîtes aux lettres**   Ce champ en lecture seule affiche le nom de la base de données de boîtes aux lettres qui héberge la boîte aux lettres de la salle. Utilisez la page **Migration** dans le CAE pour déplacer la boîte aux lettres vers une autre base de données.

  - **\* Alias**   Ce champ permet de modifier l'alias de la boîte aux lettres de la salle.

  - **Masquer dans les listes d’adresses Exchange   **Activez cette case à cocher pour empêcher que la boîte aux lettres de la salle n’apparaisse dans le carnet d'adresses et les autres listes d’adresses définies dans votre organisation Exchange. Après avoir activé cette case à cocher, les utilisateurs peuvent encore envoyer des messages de réservation à la boîte aux lettres de la salle en utilisant son adresse de messagerie.

  - **Service**   Ce champ permet de spécifier le nom d'un service auquel la salle est associée. Vous pouvez utiliser cette propriété pour créer des conditions de destinataire pour les groupes de distribution dynamiques et des listes d'adresses.

  - **Société**   Ce champ permet de spécifier le nom d'une société à laquelle la salle est associée. Comme la propriété de département, vous pouvez utiliser cette propriété pour créer des conditions de destinataire pour les groupes de distribution dynamiques et des listes d'adresses.

  - **Stratégie de carnet d’adresses**   Activez cette case à cocher pour spécifier une stratégie de carnet d’adresses pour la boîte aux lettres. Les stratégies de carnet d’adresses contiennent une liste d’adresses globale, un carnet d’adresses en mode hors connexion, une liste de salles et un ensemble de listes d’adresses. Pour en savoir plus, consultez la rubrique [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).
    
    Dans la liste déroulante, sélectionnez la règle que vous souhaitez associer à cette boîte aux lettres.

  - **Attributs personnalisés**   Ce champ affiche les attributs personnalisés définis pour la boîte aux lettres de la salle. Pour spécifier des valeurs d’attribut personnalisées, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"). Vous pouvez spécifier jusqu’à 15 attributs personnalisés pour le destinataire.

## Délégués

Utilisez ce champ pour afficher ou modifier la façon dont la boîte aux lettres de la salle gère les demandes de réservation et pour définir qui peut accepter ou refuser ces demandes si cela n'est pas fait automatiquement.

  - **Demandes de réservation**    Sélectionnez l'une des options suivantes pour gérer les demandes de réservation.
    
      - **Accepter ou refuser les demandes de réservation automatiquement**   Une demande de réunion valide réserve automatiquement la ressource. S'il y a un conflit de planification avec une réservation existante, ou si la demande de réservation viole les limites de planification de la salle, par exemple, si la durée de réunion est trop longue, la demande de réunion est refusée automatiquement.
    
      - **Sélectionner des délégués capables d'accepter ou de refuser des demandes de réservation**   Les délégués sont chargés d'accepter ou de refuser les demandes de réunion envoyées à la boîte aux lettres de la salle. Si vous attribuez plusieurs délégués de ressources, un seul d'entre eux doit agir sur une demande de réunion spécifique.

  - **Délégués**   Si vous avez sélectionné l'option exigeant que les demandes de réservation soient envoyées aux délégués, utilisez cette section pour sélectionner les délégués. Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") ou **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour ajouter ou supprimer des délégués de cette liste.

## Options de réservation

Utilisez le champ **Options de réservation** pour afficher ou modifier les paramètres de la stratégie de réservation qui définissent le moment où la salle peut être occupée, la durée de réservation où le préavis nécessaire pour une réservation.

  - **Autoriser les réunions périodiques**   Ce paramètre autorise ou interdit les réunions périodiques dans la salle. Par défaut, ce paramètre est activé, de sorte que les réunions périodiques sont autorisées.

  - **Autoriser la planification uniquement pendant les heures de travail**   Ce paramètre accepte ou refuse les demandes de réunion en dehors des heures ouvrables définies pour la salle. Par défaut, ce paramètre est désactivé, les demandes de réunion sont autorisées en dehors des heures de travail. Par défaut, les heures de travail sont 8 h à 17 h, du lundi au vendredi. Vous pouvez configurer les heures ouvrables de la boîte aux lettres de la salle dans la section Apparence de la page Calendrier.

  - **Toujours refuser si la date de fin est au-delà de cette limite**   Ce paramètre contrôle le comportement de réunions répétitives qui s'étendent au-delà de la date spécifiée par le réglage de l'heure de réservation maximale.
    
      - Si vous activez ce paramètre, une demande de réservation régulière est automatiquement refusée si les réservations commencent le ou avant la date spécifiée par la valeur de **Durée maximale de réservation**, et s'étendent au-delà de la date spécifiée. Il s’agit du paramètre par défaut.
    
      - Si vous désactivez ce paramètre, une demande de réservation régulière est automatiquement acceptée si les demandes de réservation commencent avant ou à la date spécifiée par la valeur de **Délai maximal de réservation** et se prolongent au-delà de la date spécifiée. Cependant, le nombre de réunions est réduit de sorte que celles-ci n'auront pas lieu après la date spécifiée.

  - **Délai maximal de réservation (jours)**   Ce paramètre spécifie le nombre maximal de jours de préavis pour effectuer une réservation. Une entrée valide est un entier compris entre 0 et 1080. La valeur par défaut est 180 jours.

  - **Durée maximale (heures)**   Ce paramètre spécifie la durée maximale de la réservation lors d'une demande. La valeur par défaut est 24 heures.
    
    Pour les demandes de réservation périodiques, la durée maximale de la réservation s’applique à la durée de chaque instance de la demande.

Cette page contient également un champ utilisable pour rédiger un message qui sera envoyé aux utilisateurs qui envoient des demandes de réservation de la salle.

## Informations sur le contact

L’onglet **Coordonnées** permet d’afficher ou de modifier les informations de contact de la salle. L'information sur cette page s'affiche dans le carnet d'adresses.

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

Ce champ permet d’afficher ou de modifier les adresses de messagerie associées à la boîte aux lettres de la salle. Cela inclut l'adresse SMTP principale de la boîte aux lettres et toutes les adresses proxy associées. L’adresse SMTP principale (aussi appelée *adresse de réponse*) apparaît en gras dans la liste d’adresses, avec la valeur **SMTP** inscrite en majuscules dans la colonne **Type**.

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

Dans le champ **Info-courrier**, vous pouvez ajouter une info-courrier pour alerter les utilisateurs d’éventuels problèmes avant qu’ils n’envoient une demande à la boîte aux lettres de la salle. Une info-courrier est un texte qui s’affiche dans la barre d’informations lorsque ce destinataire est ajouté aux champs À, Cc ou Cci d’un nouveau message électronique.

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


## Utiliser Exchange PowerShell pour modifier les propriétés d’une boîte aux lettres de salle

Utilisez les ensembles suivants de cmdlets pour afficher ou modifier les propriétés d'une boîte aux lettres de salle :** Get-Mailbox** et **Set-Mailbox** pour afficher et modifier les propriétés générales et les adresses de messagerie des boîtes aux lettres de salles. Utilisez les cmdlets **Get-CalendarProcessing** et **Set-CalendarProcessing** pour afficher et modifier les délégués et les options de réservation.

  - **Get-User** et **Set-User**   Utilisez ces cmdlets pour afficher et définir les propriétés générales (ex. emplacement, nom d'un service et nom d'une société).

  - **Get-Mailbox** et **Set-Mailbox**   Utilisez ces cmdlets pour afficher et définir les propriétés de boîtes aux lettres, telles que les adresses courriels et la base de données de boîtes aux lettres.

  - Utilisez les cmdlets **Get-CalendarProcessing** et **Set-CalendarProcessing** pour afficher et définir les délégués et les options de réservation.

Pour plus d'informations à propos de ces cmdlets, consultez les rubriques suivantes :

  - [Get-User](https://technet.microsoft.com/fr-fr/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/fr-fr/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/fr-fr/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/fr-fr/library/dd335046\(v=exchg.150\))

Voici des exemples d’utilisation d’Exchange PowerShell pour modifier les propriétés des boîtes aux lettres de salle.

Cet exemple modifie le nom complet, l'adresse SMTP principale (appelée adresse de réponse par défaut) et la capacité de la salle. De plus, l'adresse de réponse précédente est conservée comme adresse proxy.

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

Cet exemple configure des boîtes aux lettres de salle pour pouvoir planifier les demandes de réservation uniquement pendant les heures ouvrables ; il définit également une durée maximale de 9 heures.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

Cet exemple utilise la cmdlet **Get-User** pour rechercher toutes les boîtes aux lettres de salle qui correspondent à des salles de conférence privées ; il utilise ensuite la cmdlet **Set-CalendarProcessing** pour envoyer des demandes de réservation à un délégué (Robin Wood) qui les accepte ou les refuse.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## Comment savoir si cela a fonctionné ?

Pour vérifier que les modifications des propriétés d'une boîte aux lettres de salle sont réussies, procédez comme suit :

  - Dans le Centre d’administration Exchange, sélectionnez la boîte aux lettres puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour afficher la propriété ou la fonctionnalité modifiée. Selon la propriété modifiée, elle peut être affichée dans le volet Détails de la boîte aux lettres sélectionnée.

  - Dans Exchange PowerShell, utilisez la cmdlet **Get-Mailbox** pour vérifier les modifications. L’utilisation d’Exchange PowerShell permet d’afficher plusieurs propriétés pour plusieurs boîtes aux lettres. Dans l'exemple ci-dessus où les demandes de réservation peuvent être planifiées uniquement pendant les heures ouvrables et durer au maximum 9 heures, exécutez la commande suivante pour vérifier les nouvelles valeurs.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

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

