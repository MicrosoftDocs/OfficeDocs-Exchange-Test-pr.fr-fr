---
title: 'Ajouter ou supprimer des balises de rétention à partir d’une stratégie de rétention: Exchange 2013 Help'
TOCTitle: Ajouter ou supprimer des balises de rétention à partir d’une stratégie de rétention
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50477915
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajouter ou supprimer des balises de rétention à partir d’une stratégie de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-02_

Vous pouvez ajouter des balises de rétention à une stratégie de rétention au moment de sa création ou ultérieurement. Pour plus d’informations sur la création d’une stratégie de rétention, comme la procédure à suivre pour ajouter simultanément des balises de rétention, consultez la rubrique [Créer une stratégie de rétention](create-a-retention-policy-exchange-2013-help.md).

Une stratégie de rétention peut contenir les balises de rétention suivantes :

  - Une ou plusieurs stratégies de rétention des balises pour les dossiers par défaut pris en charge

  - Une seule balise de stratégie par défaut (DPT) avec l’action **Déplacer vers l’archive**

  - Une balise de stratégie par défaut présentant l’action **Supprimer et autoriser la récupération** ou l’action **Supprimer définitivement**

  - Une balise de rétention par défaut pour la messagerie vocale

  - N’importe quel nombre de balises personnelles

Pour plus d’informations sur les balises de rétention, consultez la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez - Entrée « Gestion des enregistrements de messagerie » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les balises de rétention ne sont pas appliquées à une boîte aux lettres tant qu’elles ne sont pas liées à une stratégie de rétention et que l’Assistant Dossier géré traite la boîte aux lettres. Pour démarrer l’Assistant Dossier géré afin qu’il traite une boîte aux lettres, consultez la rubrique [Configurer l’Assistant Dossier géré](configure-the-managed-folder-assistant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le CAE pour ajouter ou supprimer des balises de rétention

1.  Accédez à **Gestion de la conformité** \> **Stratégies de rétention**.

2.  Dans la liste affichée, sélectionnez la stratégie de rétention à laquelle vous souhaitez ajouter des balises de rétention, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **Stratégie de rétention**, utilisez les paramètres suivants :
    
      - **Ajouter** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")   Cliquez sur ce bouton pour ajouter une balise de rétention à la stratégie.
    
      - **Supprimer** ![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression")   Sélectionnez une balise dans la liste, puis cliquez sur ce bouton pour la supprimer de la stratégie.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter ou supprimer des balises de rétention

Cet exemple illustre comment ajouter les balises de rétention VPs-Default, VPs-Inbox et VPs-DeletedItems à la stratégie de rétention RetPolicy-VPs qui ne possède pas encore de balises de rétention liées.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si la stratégie possède des balises de rétention liées, cette commande remplace les balises existantes.</td>
</tr>
</tbody>
</table>


    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

Cet exemple ajoute la balise de rétention VPs-DeletedItems à la stratégie de rétention RetPolicy-VPs, à laquelle sont déjà liées d’autres balises de rétention.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Cet exemple supprime la balise de rétention VPs-Inbox de la stratégie de rétention RetPolicy-VPs.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd335196\(v=exchg.150\)) et [Get-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd298086\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement ajouté ou supprimé une balise de rétention d’une stratégie de rétention, utilisez la cmdlet [Get-RetentionPolicy](https://technet.microsoft.com/fr-fr/library/dd298086\(v=exchg.150\)) pour vérifier la propriété *RetentionPolicyTagLinks*.

Cet exemple utilise la cmdlet **Get-RetentionPolicy** pour récupérer les balises de rétention ajoutées à la stratégie MRM par défaut et les transmet à la cmdlet **Format-Table** pour générer seulement la propriété du nom de chaque balise.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

