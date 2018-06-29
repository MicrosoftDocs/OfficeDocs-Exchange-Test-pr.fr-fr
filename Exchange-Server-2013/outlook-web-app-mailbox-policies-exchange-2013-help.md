---
title: 'Stratégies de boîte aux lettres de Outlook Web App: Exchange 2013 Help'
TOCTitle: Stratégies de boîte aux lettres de Outlook Web App
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50477635
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégies de boîte aux lettres de Outlook Web App

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-05_

Utilisez les stratégies de boîte aux lettres Microsoft Outlook Web App pour créer des stratégies au niveau de l’organisation et gérer l’accès aux fonctionnalités dans Outlook Web App.

**Table des matières**

Stratégies de boîte aux lettres de Outlook Web App

Création ou suppression de stratégies de boîtes aux lettres Outlook Web App

Configuration des stratégies de boîtes aux lettres Outlook Web App

Application de stratégies de boîtes aux lettres Outlook Web App

## Stratégies de boîte aux lettres de Outlook Web App

Dans Exchange 2013, vous pouvez créer des stratégies de boîtes aux lettres Outlook Web App multiples et les appliquer à des boîtes aux lettres individuelles. Lorsqu’une stratégie de boîte aux lettres d’Outlook Web App est appliquée à une boîte aux lettres, elle écrase les paramètres du répertoire virtuel.

Vous pouvez également gérer les fonctionnalités d’Outlook Web App en configurant les répertoires virtuels d’Outlook Web App. Les paramètres du répertoire virtuel seront utilisés pour toute boîte aux lettres à laquelle aucune stratégie de boîte aux lettres n’a été appliquée.

## Création ou suppression de stratégies de boîtes aux lettres Outlook Web App

Une stratégie de boîte aux lettres Outlook Web App par défaut est automatiquement créée lorsqu’Exchange est installé. Par défaut, toutes les options sont activées sur la stratégie de boîte aux lettres d’Outlook Web App par défaut. Vous pouvez créer autant de stratégies de boîte aux lettres d’Outlook Web App que nécessaire pour satisfaire les besoins de votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La stratégie de boîte aux lettres par défaut d’Outlook Web App n’est pas automatiquement appliquée à toutes les boîtes aux lettres.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la création ou la suppression de stratégies de boîtes aux lettres, consultez les rubriques [Création d'une stratégie de boîte aux lettres Outlook Web App](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) et [Suppression d'une stratégie de boîte aux lettres Outlook Web App dans Exchange](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md).

## Configuration des stratégies de boîtes aux lettres Outlook Web App

Les options de stratégies de boîtes aux lettres Outlook Web App par défaut sont activées par défaut. Pour plus d’informations sur la configuration de stratégies de boîtes aux lettres Outlook Web App, consultez la rubrique [Afficher ou configurer des propriétés de stratégie de boîte aux lettres Outlook Web App](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md).

## Application de stratégies de boîtes aux lettres Outlook Web App

Une seule stratégie de boîte aux lettres d’Outlook Web App peut être appliquée à une boîte aux lettres.

S’il n’existe pas de stratégie de boîte aux lettres d’Outlook Web App appliquée à une boîte aux lettres, les paramètres définis sur le répertoire virtuel s’appliqueront.

Vous pouvez appliquer une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres via le Centre d’administration Exchange (EAC) pour modifier une boîte aux lettres existante ou via le Shell et la cmdlet [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)) pour appliquer une stratégie de boîte aux lettres. Pour plus d’informations, consultez la rubrique [Appliquer (ou supprimer) une stratégie de boîte aux lettres Outlook Web App à une boîte aux lettres](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md).

