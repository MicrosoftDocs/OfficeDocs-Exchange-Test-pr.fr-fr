---
title: "Suppression d'une relation d'organisation: Exchange 2013 Help"
TOCTitle: Suppression d'une relation d'organisation
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50479639
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suppression d'une relation d'organisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-04_

Une relation d’organisation permet aux utilisateurs de votre organisation Exchange de partager des informations de disponibilité de calendrier avec une organisation Office 365 ou une autre organisation Exchange sur site. Vous pouvez supprimer une relation d’organisation pour désactiver le partage de calendrier avec l’autre organisation.

Pour pouvoir partager des calendriers avec une autre organisation, vous devez configurer une relation d’authentification avec le système d'authentification Azure Active Directory (également appelé « fédération ») et satisfaire la configuration logicielle requise minimale. Pour en savoir plus sur le partage fédéré, consultez la rubrique [Partage](sharing-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Calendrier et autorisations de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer une relation d'organisation

1.  Sur un serveur Exchange 2013 de votre organisation sur site, accédez à **organisation** \> **partage**.

2.  Sous **Partage de l'organisation**, sélectionnez une relation d'organisation et cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer") pour la supprimer.

3.  Dans l’avertissement qui s’affiche, cliquez sur **oui**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une relation d'organisation

Cet exemple supprime la relation d'organisation Contoso de l'organisation Exchange

    Remove-OrganizationRelationship -Identity "Contoso"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332362\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la suppression a été effectuée correctement, procédez comme suit :

  - Dans le CAE, accédez à **Organisation**\>**Partage** et vérifiez que la relation d’organisation n’est pas affichée dans la vue Liste sous **Partage de l’organisation**.

  - Exécutez la commande de l'environnement de ligne de commande suivante pour vérifier que les informations sur la relation d'organisation ont été supprimées.
    
        Get-OrganizationRelationship | Format-List

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>

