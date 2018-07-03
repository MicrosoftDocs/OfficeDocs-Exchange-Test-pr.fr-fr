---
title: 'Créer une relation d’organisation: Exchange 2013 Help'
TOCTitle: Créer une relation d’organisation
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50478293
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une relation d’organisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Configurez une relation organisationnelle pour partager des informations de calendrier avec un partenaire commercial externe. Une relation organisationnelle peut être configurée entre deux organisations Exchange 2013 fédérées ou entre une organisation Exchange 2013 fédérée et des organisations Exchange 2010 fédérées. Vous pouvez également configurer une relation organisationnelle entre votre organisation Exchange sur site et une organisation Office 365.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La création d'une relation d'organisation fait partie des différentes étapes de la mise en place du partage fédéré dans votre organisation Exchange et exige la configuration d'une approbation de fédération pour votre organisation Exchange locale.</td>
</tr>
</tbody>
</table>


Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Calendrier et autorisations de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Une approbation de fédération active pour l’organisation Exchange sur site doit être configurée. Pour plus d’informations, consultez la rubrique [Configurer une approbation de fédération](configure-a-federation-trust-exchange-2013-help.md).

  - Une approbation de fédération doit être établie avec le système d’authentification Azure AD dans l’organisation externe que vous souhaitez configurer dans la relation d'organisation. Le domaine fédéré principal sera utilisé pour l'organisation Exchange externe au moment de la configuration de la relation d'organisation.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le centre d'administration Exchange pour créer une relation d'organisation

1.  Sur un serveur Exchange 2013 de votre organisation sur site, accédez à **organisation** \> **partage**.

2.  Sous **Partage organisationnel**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **nouvelle relation organisationnelle**, dans la zone **nom de la relation**, entrez un nom convivial pour la relation organisationnelle.

4.  Dans la zone **Domaines à partager avec**, saisissez le domaine ou sous-domaine fédéré pour l’organisation Office 365 ou Exchange sur site qui pourra voir vos calendriers. Pour saisir plusieurs domaines pour l’organisation externe, séparez les domaines par une virgule. Par exemple, **contoso.com, service.contoso.com**.

5.  Cochez la case **Activer le partage des informations de disponibilité de calendrier** pour activer le partage de calendrier avec les domaines que vous avez répertoriés. Définissez le niveau de partage des informations de disponibilité de calendrier, ainsi que les utilisateurs pouvant partager ces informations.
    
    Pour définir le niveau d'accès de la disponibilité, sélectionnez l'une des opérations suivantes :
    
      - **Informations de disponibilité de calendrier avec les heures de disponibilité uniquement**
    
      - **Disponibilité de calendrier avec l’heure, l'objet et emplacement**
    
    Pour définir les utilisateurs qui partagent des informations de disponibilité de calendrier, sélectionnez l’une des options suivantes :
    
      - **Tout le monde dans votre organisation**
    
      - **Un groupe de sécurité spécifié**
        
        Pour spécifier un groupe de sécurité, cliquez sur **parcourir**.

6.  Cliquez sur **enregistrer** pour créer la relation organisationnelle.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une relation organisationnelle

Cet exemple crée une relation d’organisation avec Contoso, Ltd en utilisant les conditions suivantes :

  - La relation d’organisation est activée pour contoso.com, northamerica.contoso.com et europe.contoso.com.

  - L’accès aux informations de disponibilité est activé.

  - L’organisation qui émet la demande reçoit les informations de disponibilité, d’objet et d’emplacement de la part de l’organisation cible.

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

Cet exemple tente de découvrir automatiquement des informations de configuration de l'organisation Exchange externe Contoso.com en utilisant les noms de domaine fournis dans la cmdlet **Get-FederationInformation**. Si vous utilisez cette méthode pour créer votre relation d'organisation, vous devez tout d'abord vous assurer que vous avez créé un identificateur d'organisation en utilisant la cmdlet **Set-FederatedOrganizationIdentifier**.

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Get-FederationInformation](https://technet.microsoft.com/fr-fr/library/dd351221\(v=exchg.150\)) et [New-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332357\(v=exchg.150\)).

Cet exemple crée une relation d’organisation avec Bon café. Dans cet exemple, les paramètres de connexion avec l'organisation Exchange externe sont fournis. Les conditions suivantes s’appliquent :

  - La relation d'organisation est établie avec le domaine fédéré de Fourth Coffee, fourthcoffee.com.

  - L’URL de l’application des services Web d’Exchange est mail.fourthcoffee.com.

  - L'URL de découverte automatique est https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity.

  - L’accès aux informations de disponibilité est activé.

  - L'organisation qui émet la demande reçoit uniquement les informations de disponibilité avec les heures de disponibilité.

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332357\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

L’exécution réussie de l’Assistant **Nouvelle relation organisationnelle** constitue la première indication que la création des relations d’organisation a fonctionné comme prévu.

Pour vérifier que vous avez créé la relation d'organisation avec succès, exécutez la commande Shell suivante pour vérifier les informations de relation d'organisation :

    Get-OrganizationRelationship | format-list

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

