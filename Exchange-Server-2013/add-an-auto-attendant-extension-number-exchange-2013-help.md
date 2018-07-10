---
title: 'Ajouter un numéro de poste standard automatique: Exchange 2013 Help'
TOCTitle: Ajouter un numéro de poste standard automatique
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50479551
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter un numéro de poste standard automatique

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Vous pouvez configurer un numéro de poste ou plusieurs numéros de poste sur un standard automatique de messagerie unifiée (MU). Lorsque vous ajoutez un numéro de poste à un standard automatique de messagerie unifiée, ce numéro utilisable par les appelants à appeler dans le standard automatique. Également, vous devrez peut-être ajouter des numéros de poste, car il existe plus d'un numéro de poste que les appelants peuvent utiliser pour accéder à un standard automatique. Par défaut, aucun des numéros de poste ne sont configurées lorsque vous créez un standard automatique.

Vous pouvez créer un nouveau standard automatique sans configuration d'un numéro de poste pour le standard automatique. Vous pouvez également associer plusieurs numéros de téléphone ou poste avec un standard automatique unique. Vous pouvez ajouter les numéros de poste lorsque vous créez le standard automatique de messagerie unifiée ou ajoutez après avoir configuré le standard automatique. Le nombre de chiffres dans le numéro de poste que vous avez configuré sur le standard automatique de messagerie unifiée doit correspondre au nombre de chiffres pour un numéro de poste qui est configurée sur le plan de numérotation de messagerie unifiée associé du standard automatique de messagerie unifiée.

> [!NOTE]
> Vous pouvez également ajouter une adresse de protocole SIP (Session Initiation) au lieu d'ajouter un numéro de poste. Une adresse SIP est utilisée par certains autocommutateur privé IP (PBX) et Office Communications Server 2007 R2 ou Microsoft Lync Server.


Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour ajouter une extension ou téléphone numéros pour un standard automatique de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **plans de numérotation de messagerie unifiée**. Dans la liste affichée, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de MU que vous souhaitez ajouter des numéros de poste ou le téléphone à.

3.  Dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans la page de **Standard automatique de messagerie unifiée** \> **Général**, sous **numéros d'accès**, dans la zone de texte, entrez le poste ou numéro de téléphone que vous souhaitez utiliser et cliquez sur **Add**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

5.  Cliquez sur **Enregistrer** pour ajouter le numéro.

## Utiliser le Shell pour configurer un numéro de poste sur un standard automatique de messagerie unifiée

Cet exemple configure un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` avec plusieurs numéros de poste.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

