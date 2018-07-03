---
title: 'Créer une stratégie de partage: Exchange 2013 Help'
TOCTitle: Créer une stratégie de partage
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 50479242
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une stratégie de partage

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Les stratégies de partage vous permettent de contrôler la manière dont les utilisateurs de votre organisation Exchange peuvent partager les informations de calendrier avec des utilisateurs extérieurs à votre organisation. Les stratégies de partage offrent un partage établi par utilisateur, et de personne à personne, des informations de calendrier et de contacts avec les différents types d’utilisateurs externes. Elles prennent en charge le partage des informations de calendrier avec des organisations fédérées externes (comme Office 365 ou une autre organisation Exchange sur site), des organisations non fédérées externes et les personnes ayant accès à Internet. Pour appliquer aux utilisateurs une stratégie de partage spécifique, consultez [Appliquer une stratégie de partage aux boîtes aux lettres](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La création d’une stratégie de partage fait partie des étapes permettant de configurer le partage fédéré dans votre organisation Exchange. Vous devez configurer une approbation de fédération avec le système d’authentification Azure Active Directory pour votre organisation Exchange sur site afin de pouvoir partager des informations de calendrier avec d’autres organisations Exchange fédérées. Une approbation de fédération n’est pas requise pour les stratégies de partage Internet.</td>
</tr>
</tbody>
</table>


Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

Pour les autres tâches de gestion relatives à la fédération, voir [Procédures de fédération](federation-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Calendrier et autorisations de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les conditions suivantes doivent être réunies pour le partage de stratégies entre des organisations Exchange fédérées :
    
      - Un serveur d’accès au client Exchange 2013 existe dans chaque organisation Exchange. Les stratégies de partage sont également prises en charge entre les organisations Exchange où une organisation possède des serveurs d’accès au client Exchange 2013 et l’autre possède des serveurs d’accès au client Exchange 2010 SP3 ou de version supérieure.
    
      - Chaque organisation Exchange a créé une approbation de fédération avec le système d'authentification Azure AD. Pour plus d’informations, consultez la rubrique [Configurer une approbation de fédération](configure-a-federation-trust-exchange-2013-help.md).
    
      - Chaque organisation Exchange a configuré un identificateur d’organisation fédérée. Les domaines utilisés pour générer les adresses de messagerie des utilisateurs ont été ajoutés aux identificateurs de l’organisation.
    
      - Les boîtes aux lettres utilisateur sont situées sur les serveurs de boîtes aux lettres Exchange 2013 ou Exchange 2010 de chaque organisation Exchange.
    
      - Seuls les utilisateurs d’Outlook 2010 (ou version ultérieure) et d’Outlook Web App peuvent créer des invitations de partage.

  - Les conditions suivantes doivent être remplies pour appliquer des stratégies de partage à des organisations Exchange non fédérées ou à des utilisateurs individuels :
    
      - Un serveur d’accès au client Exchange 2013 existe dans l’organisation Exchange qui partage les informations de calendrier de l’utilisateur.
    
      - Les boîtes aux lettres utilisateur sont stockées sur des serveurs de boîtes aux lettres Exchange 2013 dans l’organisation Exchange qui partage les informations de calendrier de l’utilisateur.
    
      - Le serveur d’accès au client Exchange 2013 doit être activé pour l’accès à Outlook Web App.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le CAE pour créer une stratégie de partage

1.  Accédez à **organisation**\> **partage**.

2.  Dans l'affichage Liste, sous **Partage individuel**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **nouvelle stratégie de partage**, tapez un nom convivial pour la stratégie de partage dans la zone **Nom de la stratégie**.

4.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour spécifier les règles de partage pour la stratégie de partage.

5.  Dans **règle de partage**, sélectionnez l’une des options suivantes pour spécifier les domaines avec lesquels vous souhaitez partager :
    
      - **Partage avec tous les domaines**
    
      - **Partage avec un domaine spécifique**

6.  Si vous sélectionnez **Partage avec un domaine spécifique**, entrez le nom du domaine avec lequel vous souhaitez partager. Si vous devez entrer plusieurs domaines pour cette stratégie de partage, enregistrez les paramètres du premier domaine, puis modifiez les règles de partage pour ajouter d’autres domaines.

7.  Pour définir les niveaux de partage de calendrier à appliquer à la stratégie, activez la case à cocher **Partager votre dossier de calendrier**, puis sélectionnez l’une des options suivantes :
    
      - **Informations de disponibilité de calendrier avec les heures de disponibilité uniquement**
    
      - **Informations de disponibilité de calendrier avec heure, objet et emplacement**
    
      - **Toutes les informations de calendrier des rendez-vous, y compris l’heure, l’objet, le lieu et le titre**

8.  Cliquez sur **enregistrer** pour définir les règles de la stratégie de partage.

9.  Si vous souhaitez que cette stratégie de partage devienne la stratégie de partage par défaut pour les utilisateurs de votre organisation Exchange, cochez la case **Définir cette stratégie comme ma stratégie de partage par défaut**.

10. Cliquez sur **enregistrer** pour créer la stratégie de partage.

## Utiliser le CAE pour permettre à tous les utilisateurs de partager tous les détails du calendrier

Vous pouvez modifier la stratégie de partage par défaut pour permettre à tous les utilisateurs de partager tous les détails du calendrier avec des personnes externes à votre organisation.

1.  Accédez à **organisation**\> **partage**.

2.  Dans l’affichage de liste, sous **Partage individuel**, sélectionnez **Stratégie de partage par défaut**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la boîte de dialogue **Stratégie de partage**, sélectionnez **Partage avec tous les domaines**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans la boîte de dialogue **Règle de partage**, sous **Spécifier les informations à partager**, sélectionnez **Toutes les informations de rendez-vous de calendrier, notamment l’heure, l’objet, le lieu et le titre**, puis cliquez sur **enregistrer**.

5.  Dans la boîte de dialogue **Stratégie de partage**, cliquez sur **enregistrer** pour définir les règles de la stratégie de partage.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une stratégie de partage

  - Cet exemple crée la stratégie de partage Contoso pour le domaine externe fédéré contoso.com. Cette stratégie permet aux utilisateurs du domaine contoso.com de consulter en détail les informations de disponibilité de calendrier (disponible/occupé) de votre utilisateur. Par défaut, cette stratégie est activée.
    
        New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail

  - Cet exemple crée la stratégie de partage ContosoWoodgrove pour deux domaines fédérés différents (contoso.com et woodgrovebank.com) avec des actions de partage spécifiques configurées pour chaque domaine. La stratégie est désactivée.
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - Cet exemple crée la stratégie de partage Anonyme pour une organisation Exchange avec le serveur d’accès au client CAS01 et le serveur de boîtes aux lettres MAIL01, avec l’action de partage configurée pour des informations de disponibilité de calendrier limitées. Cette stratégie permet aux utilisateurs de votre organisation Exchange d’inviter des utilisateurs disposant d’un accès Internet à consulter leurs informations de disponibilité de calendrier en leur envoyant un lien. La stratégie est activée.
    
    1.  Définissez l’URL du proxy Web pour MAIL01.
        
            Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
    
    2.  Activez le répertoire virtuel de publication sur CAS01.
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  Créez la stratégie de partage Anonyme et configurez le partage d’informations de calendrier limitées.
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [New-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/fr-fr/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\))

## Comment savoir si cela a fonctionné ?

Pour vérifier que la création de la stratégie de partage s’est effectuée correctement, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell suivante et vérifiez les informations relatives à la stratégie de partage.

    Get-SharingPolicy <policy name> | format-list

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

