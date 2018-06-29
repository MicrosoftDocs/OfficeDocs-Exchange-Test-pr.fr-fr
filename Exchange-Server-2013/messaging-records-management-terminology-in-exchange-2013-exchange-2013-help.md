---
title: 'Des enregistrements de messagerie terminologie de gestion dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Des enregistrements de messagerie terminologie de gestion dans Exchange 2013
ms:assetid: de3e3503-6de3-4666-aeb9-cd877efb93bb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb408414(v=EXCHG.150)
ms:contentKeyID: 50479349
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Des enregistrements de messagerie terminologie de gestion dans Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-30_

Cette rubrique définit les composants principaux associés à la gestion des enregistrements (MRM) dans Microsoft Exchange Server 2013 de messagerie. MRM est une technologie de gestion des enregistrements dans Exchange 2013 qui aide les organisations à réduire les risques associés à la messagerie et autres communications. MRM rend plus faciles à conserver les messages nécessaires pour se conformer à la stratégie d'entreprise, aux réglementations gouvernementales ou besoins juridiques et supprimer le contenu qui a ne juridique ou économique.

  - **balise de stratégie par défaut (DPT)**  
    Une balise de stratégie par défaut est une balise de rétention qui s’applique à tous les éléments d’une boîte aux lettres à laquelle aucune balise de rétention n’est encore appliquée. Vous ne pouvez avoir qu'une seule balise de stratégie par défaut dans une stratégie de rétention.

<!-- end list -->

  - **utilisateur organisé**  
    Utilisateur qui classe régulièrement les éléments de la boîte aux lettres dans des dossiers.
    
    Voir utilisateur désorganisé.

<!-- end list -->

  - **journalisation**  
    Capacité d'enregistrer toutes les communications, y compris les communications électroniques, au sein d'une organisation afin de les utiliser en relation avec la stratégie de rétention ou d'archivage du courrier électronique de l'organisation. Dans la gestion des enregistrements de messagerie, la journalisation fait généralement référence au processus d'envoi d'un rapport de journal sur les messages situés dans un dossier géré à l'adresse SMTP spécifiée. Ce processus est exécuté par l'Assistant Dossier géré.

<!-- end list -->

  - **paramètres de contenu géré**  
    Les informations de rétention créées pour les dossiers gérés, la fonctionnalité MRM disponible dans Exchange Server 2007 et Exchange Server 2010. Un dossier géré peut posséder plusieurs paramètres de contenu pour les différents types de messages : messages électroniques, messages vocaux et éléments de calendriers. Les paramètres de rétention des messages définis dans les paramètres de contenu pour un dossier géré s'appliquent aux messages qui se trouvent dans ce dossier géré.

<!-- end list -->

  - **dossier géré**  
    Utilisé pour la fonctionnalité MRM d’Exchange Server 2007 et d’Exchange Server 2010, un dossier géré est un objet Active Directory qui représente un dossier de boîtes aux lettres afin d’y appliquer des paramètres de contenu géré. Dans une boîte aux lettres, un dossier géré correspond au dossier auquel des paramètres de contenu géré ont été appliqués.

<!-- end list -->

  - **Assistant Dossier géré**  
    L’un des assistants de boîte aux lettres Microsoft Exchange d’Exchange 2013. L’assistant Dossier géré est responsable de l’archivage, de l’expiration des messages et de la conformité. Il traite des boîtes aux lettres et applique des stratégies de rétention.

<!-- end list -->

  - **stratégie de boîte aux lettres de dossier géré**  
    Regroupement logique de dossiers gérés. Dans Exchange 2010 et Exchange 2007, lors de l’application d’une stratégie de boîte aux lettres de dossier géré à une boîte aux lettres utilisateur, tous les dossiers gérés liés à la stratégie sont déployés en une seule opération.

<!-- end list -->

  - **balise personnelle**  
    Une balise personnelle est une balise de rétention mise à la disposition des utilisateurs d’Outlook Web App et d’Outlook 2010 et version ultérieure pour l’application des paramètres de rétention à des dossiers personnalisés et des éléments individuels, tels que des messages électroniques.

<!-- end list -->

  - **utilisateur désorganisé**  
    Utilisateur qui ne classe pas régulièrement les éléments de la boîte aux lettres. Ce type d'utilisateur a tendance à avoir une boîte de réception volumineuse et à s'appuyer sur la fonction de recherche pour retrouver ses messages.
    
    Voir utilisateur organisé.

<!-- end list -->

  - **stratégie**  
    Voir *stratégie de rétention* ou *stratégie de boîte aux lettres de dossier géré*.

<!-- end list -->

  - **balise de stratégie de rétention (RPT)**  
    Une balise de stratégie de rétention est une balise de rétention qui est appliquée à des dossiers par défaut, tels que Boîte de réception et Éléments supprimés.

<!-- end list -->

  - **stratégie de rétention**  
    Une stratégie de rétention est un groupement logique de balises de rétention. Lors de l'application d'une stratégie de rétention à la boîte aux lettres d'un utilisateur, toutes les balises de rétention liées à la stratégie sont déployées en une seule opération.

<!-- end list -->

  - **balise de rétention**  
    Les balises de rétention sont utilisées pour appliquer des paramètres de rétention à des messages et des dossiers dans les boîtes aux lettres utilisateur. Il existe trois types de balise de rétention :
    
      - Les balises de stratégie par défaut (DPT)
    
      - Les balises de stratégie de rétention (RPT)
    
      - Les balises personnelles

