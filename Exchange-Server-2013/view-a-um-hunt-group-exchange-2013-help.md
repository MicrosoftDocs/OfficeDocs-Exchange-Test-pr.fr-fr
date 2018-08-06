---
title: "Afficher un groupement de postes de messagerie unifiée: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Permet d'afficher un groupement de postes de messagerie unifiée
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50555516
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permet d'afficher un groupement de postes de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Lorsque vous affichez les propriétés d'un groupement de postes de messagerie unifiée (MU), vous pouvez afficher les propriétés associée liées un groupe de recherche de MU unique ou à tous les groupements de postes de messagerie unifiée associées à une seule passerelle IP de messagerie unifiée. Si aucun paramètre n'est spécifié, tous les groupes de postes de messagerie unifiée seront retournées. Vous ne pouvez pas utiliser le CAE pour afficher les propriétés du groupe de recherche ; la messagerie unifiée Vous devez utiliser l'interpréteur de commandes.

Une fois un groupement de postes de messagerie unifiée a été créé, les paramètres configurés ne peut pas être modifiés. Si vous souhaitez modifier un paramètre de configuration telles que le groupement de postes de l'identificateur pilote sur une messagerie unifiée, vous devez supprimer le groupement de postes de messagerie unifiée existant et créer un nouveau groupement de postes de messagerie unifiée qui possède les paramètres corrects.

Pour d’autres tâches relatives aux groupements de postes de messagerie unifiée, consultez la rubrique [Procédures de groupe postes de messagerie unifiée](um-hunt-group-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins de 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Groupements de postes de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une passerelle de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, voir [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un groupement de postes de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, voir [Créer un groupement de postes de messagerie unifiée](create-a-um-hunt-group-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Shell pour afficher les propriétés d'un groupement de postes de messagerie unifiée

Cet exemple affiche tous les groupements de postes de MU dans la forêt Active Directory.

    Get-UMHuntGroup

Cet exemple montre comment afficher les détails d'un groupement de postes de messagerie unifiée nommé `MyUMHuntGroup` dans une liste mise en forme.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List

> [!NOTE]
> Lorsque vous utilisez l'applet de commande <strong>Get-UMHuntGroup</strong> , vous ne pouvez pas entrer uniquement le nom du groupement de postes de messagerie unifiée. Vous devez également inclure le nom de la passerelle IP de messagerie unifiée associée au groupement de postes de messagerie unifiée.

