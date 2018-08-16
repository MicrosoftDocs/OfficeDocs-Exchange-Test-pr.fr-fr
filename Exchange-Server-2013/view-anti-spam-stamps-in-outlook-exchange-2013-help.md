---
title: 'Afficher des marquages anti-spam dans Outlook: Exchange 2013 Help'
TOCTitle: Afficher des marquages de courrier indésirable dans Outlook
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50479254
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Afficher des marquages de courrier indésirable dans Outlook

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Vous pouvez utiliser Microsoft Outlook pour afficher les cachets de blocage du courrier indésirable que Microsoft Exchange a appliqués à un message électronique. Les cachets de blocage de courrier indésirable vous aident à diagnostiquer les problèmes de courrier indésirable en appliquant des métadonnées de diagnostic, ou « cachets de blocage », telles que des informations spécifiques à un expéditeur, des résultats de validation du puzzle et des résultats de filtrage du contenu, aux messages à mesure qu’ils sont soumis aux fonctionnalités de blocage du courrier indésirable qui filtrent les messages entrants en provenance d’Internet.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Accès à la boîte aux lettres » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser Outlook 2010 ou Outlook 2013 pour afficher les cachets de blocage du courrier indésirable

1.  Dans Outlook 2010 ou sur Outlook 2013, sur un ordinateur client, dans l’affichage **Courrier électronique**, double-cliquez sur un message pour l’ouvrir.

2.  Dans la section **Balises** de la barre d’outils du ruban, cliquez sur l’icône **Options** pour afficher la boîte de dialogue **Propriétés** du message.

3.  Dans la boite de dialogue **Propriétés**, dans la section **En-têtes Internet**, utilisez la barre de défilement pour afficher les cachets de blocage du courrier indésirable comme le montre l’exemple suivant.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Utiliser Outlook 2007 pour afficher les cachets de blocage du courrier indésirable

1.  Dans Outlook 2007, sur un ordinateur client, dans l’affichage **Courrier électronique**, double-cliquez sur un message pour l’ouvrir.

2.  Dans l’onglet **Message**, dans le groupe **Options**, cliquez sur **Options de message**.

3.  Dans la boite de dialogue **Options de message**, dans la section **En-têtes Internet**, utilisez la barre de défilement pour afficher les cachets de blocage du courrier indésirable comme le montre l’exemple suivant.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

