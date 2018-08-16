---
title: 'Appliquer une strat. de rétention aux boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Appliquer une stratégie de rétention aux boîtes aux lettres
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50478388
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Appliquer une stratégie de rétention aux boîtes aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-10-01_

À l’aide des stratégies de rétention, vous pouvez regrouper une ou plusieurs balises de rétention et les appliquer aux boîtes aux lettres pour que les paramètres de rétention des messages soient utilisés. Une boîte aux lettres ne peut pas avoir plusieurs stratégies de rétention.

> [!CAUTION]
> Les messages arrivent à expiration en fonction des paramètres définis dans les balises de rétention liées à la stratégie. Ces paramètres incluent des actions, telles que le déplacement des messages dans les archives ou leur suppression définitive. Avant d’appliquer une stratégie de rétention à une ou plusieurs boîtes aux lettres, nous vous recommandons de tester la stratégie et d’inspecter chaque balise de rétention qui lui est associée.


Pour les autres tâches de gestion relatives à la gestion des enregistrements de messagerie (MRM), voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Stratégies de rétention – Appliquer » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (CAE) pour appliquer une stratégie de rétention à une seule boîte aux lettres

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres à laquelle vous souhaitez appliquer la stratégie de rétention, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **Boîte aux lettres de l’utilisateur**, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Dans la liste **Stratégie de rétention**, sélectionnez la stratégie que vous souhaitez appliquer à la boîte aux lettres, puis cliquez sur **Enregistrer**.

## Utiliser le Centre d’administration Exchange (CAE) pour appliquer une stratégie de rétention à plusieurs boîtes aux lettres

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Dans la liste affichée, utilisez les touches Maj ou Ctrl pour sélectionner plusieurs boîtes aux lettres.

3.  Dans le volet d’informations, cliquez sur **Plus d’options**.

4.  Sous **Stratégie de rétention**, cliquez sur **Mettre à jour**.

5.  Dans **Attribuer la stratégie de rétention en bloc**, sélectionnez la stratégie de rétention que vous souhaitez appliquer aux boîtes aux lettres, puis cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour appliquer une stratégie de rétention à une seule boîte aux lettres

Cet exemple applique la stratégie de rétention RP-Finance à la boîte aux lettres de Morris.

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour appliquer une stratégie de rétention à plusieurs boîtes aux lettres

Cet exemple applique la nouvelle stratégie de rétention « New-Retention-Policy » à toutes les boîtes aux lettres qui disposent de l’ancienne stratégie de rétention « Old-Retention-Policy ».

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

Cet exemple applique la stratégie de rétention RetentionPolicy-Corp à toutes les boîtes aux lettres de l’organisation Exchange.

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

Cet exemple applique la stratégie de rétention RetentionPolicy-Finance à toutes les boîtes aux lettres de l’unité d’organisation Finance.

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) et [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si l’opération a fonctionné ?

Pour vérifier que vous avez appliqué la stratégie de rétention, exécutez la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) afin de récupérer la stratégie de rétention pour la ou les boîtes aux lettres.

Cet exemple récupère la stratégie de rétention pour la boîte aux lettres de Morris.

    Get-Mailbox Morris | Select RetentionPolicy

Cette commande récupère toutes les boîtes aux lettres auxquelles la stratégie de rétention RP-Finance est appliquée.

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

