---
title: 'Modifier une relation organisationnelle: Exchange 2013 Help'
TOCTitle: Modifier une relation organisationnelle
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50477880
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier une relation organisationnelle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-01_

Une relation organisationnelle permet aux utilisateurs de votre organisation Exchange de partager des informations de disponibilité de calendrier avec une organisation Office 365 ou une autre organisation Exchange sur site. Vous souhaiterez peut-être modifier les paramètres d’une relation organisationnelle, tels que la modification du nom, la désactivation temporaire du partage du calendrier, la modification du niveau d’accès ou des groupes de sécurité qui partageront des calendriers.

Pour pouvoir partager des calendriers avec une autre organisation, vous devez configurer une relation d’authentification avec le nuage (également appelée « fédération ») et satisfaire à la configuration logicielle requise minimale. Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à la fédération, voir [Procédures de fédération](federation-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez *Calendar and Sharing Permissions* Entrée dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Une approbation de fédération active pour l’organisation Exchange sur site doit être configurée.

  - Une approbation de fédération doit être établie avec le système d’authentification Azure ADdans l’organisation externe que vous souhaitez configurer dans la relation organisationnelle.

  - Les procédures décrites dans cette rubrique apportent des modifications à une relation organisationnelle nommée Contoso. Les exemples expliquent comment effectuer les actions suivantes :
    
      - Ajouter un domaine nommé service.contoso.com à l’organisation externe.
    
      - Désactiver le partage de la disponibilité pour la relation organisationnelle.
    
      - Modifier le niveau d’accès à la disponibilité de *Calendar free/busy information with time, subject, and location* et le remplacer par *Calendar free/busy information with time only*.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le CAE pour ajouter un domaine à une relation organisationnelle

1.  Sur un serveur Exchange 2013 de votre organisation sur site, accédez à **organisation** \> **partage**.

2.  Dans la liste affichée, sous **Partage de l'organisation**, sélectionnez la relation d'organisation Contoso, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **relation organisationnelle**, **général**, ne modifiez pas le **Nom** de la relation organisationnelle.

4.  Dans la zone **Domaines à partager avec**, saisissez le domaine **service.contoso.com**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Cliquez sur **enregistrer** pour mettre à jour la relation organisationnelle.

## Utiliser le CAE pour désactiver le partage de disponibilité pour la relation d’organisation

1.  Accédez à **organisation** \> **partage**.

2.  Dans la liste affichée, sous **Partage de l’organisation**, sélectionnez la relation organisationnelle Contoso, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **relation organisationnelle**, cliquez sur **partage**.

4.  Sélectionnez **Informations de disponibilité du calendrier avec heure uniquement**.

5.  Cliquez sur **enregistrer** pour mettre à jour la relation organisationnelle.

## Utiliser le CAE pour modifier le niveau d’accès à la disponibilité pour la relation d’organisation

1.  Accédez à **organisation** \> **partage**.

2.  Dans la liste affichée, sous **Partage de l’organisation**, sélectionnez la relation organisationnelle Contoso, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **relation organisationnelle**, cliquez sur **partage**.

4.  Sélectionnez **Informations de disponibilité du calendrier avec heure uniquement**.

5.  Cliquez sur **enregistrer** pour mettre à jour la relation organisationnelle.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier la relation organisationnelle

  - Cet exemple ajoute le nom de domaine service.contoso.com à la relation d’organisation Contoso.
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - Cet exemple désactive la relation d’organisation Contoso.
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - Cet exemple montre comment activer l’accès aux informations de disponibilité du calendrier pour la relation d’organisation WoodgroveBank et définir le niveau d’accès sur `AvailabilityOnly` (informations de disponibilité du calendrier avec les heures de disponibilité uniquement).
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332343\(v=exchg.150\)) et [Set-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332326\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement mis à jour la relation d’organisation, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell et vérifiez les informations de la relation d’organisation :

    Get-OrganizationRelationship | format-list

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

