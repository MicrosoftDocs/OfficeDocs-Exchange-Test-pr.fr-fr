---
title: 'Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte: Exchange 2013 Help'
TOCTitle: Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183336
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-24_

Une fois la recherche de découverte électronique inaltérable créée, vous pouvez copier les résultats obtenus dans une boîte aux lettres de découverte via le CAE. Vous pouvez également utiliser l’interpréteur de commandes pour démarrer une recherche de découverte électronique créée à l’aide de la cmdlet **New-MailboxSearch**, qui va copier les résultats vers la boîte aux lettres de découverte spécifiée lors de la création de la recherche.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes ou plus, selon le nombre d’éléments de boîtes aux lettres renvoyés dans les résultats de la recherche.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez section « Découverte électronique inaltérable » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour pouvoir copier les résultats de la recherche, vous devez créer une recherche de découverte électronique à l’aide du CAE ou de l’interpréteur de commandes. Pour plus d’informations, voir [Créer une recherche de découverte électronique inaltérable](create-an-in-place-ediscovery-search-exchange-2013-help.md).

  - Le programme d’installation d’Exchange 2013 crée une boîte aux lettres de découverte appelée **Boîte aux lettres de découverte** pour copier les résultats de la recherche. La boîte aux lettres de découverte est également créée par défaut dans Exchange Online. Vous pouvez créer des boîtes aux lettres de découverte supplémentaires. Pour plus d’informations, voir [Créer une boîte aux lettres de découverte](create-a-discovery-mailbox-exchange-2013-help.md).

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

## Utiliser le CAE pour copier les résultats de la recherche

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**.

2.  Dans la vue de liste, sélectionnez une recherche de découverte électronique.

3.  Cliquez sur **Rechercher** ![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche"), puis sur **Copier les résultats de recherche** dans la liste déroulante.

4.  Dans **Copier les résultats de recherche**, sélectionnez l’une des options suivantes :
    
      - **Inclure les éléments impossibles à rechercher** : cochez cette case pour inclure les éléments de boîte aux lettres qui ne peuvent pas faire l’objet d’une recherche (par exemple, les messages comportant des pièces jointes dont le format empêche de les indexer avec la recherche Exchange). Pour plus d’informations, voir [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).
    
      - **Activer la déduplication** : cochez cette case pour exclure les messages dupliqués. Une seule instance d’un message est copiée dans la boîte aux lettres de découverte.
    
      - **Activer la journalisation complète** : cochez cette case pour inclure un journal complet dans les résultats de la recherche.
    
      - **M’envoyer un message électronique lorsque la copie est terminée** : cochez cette case pour recevoir une notification par courrier électronique lorsque la recherche est terminée.
    
      - **Copier les résultats vers cette boîte aux lettres de découverte** : cliquez sur **Parcourir** pour sélectionner la boîte aux lettres de découverte dans laquelle copier les résultats de la recherche.
        
        ![Copier les résultats de la recherche](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "Copier les résultats de la recherche")  

5.  Cliquez sur **Copier** pour lancer le processus permettant de copier les résultats de la recherche vers la boîte aux lettres de découverte spécifiée.

6.  Cliquez sur **Actualiser** ![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser") pour mettre à jour les informations sur l’état de copie affiché dans le volet Détails.

7.  Une fois la copie terminée, cliquez sur **Ouvrir** pour ouvrir la boîte aux lettres de découverte et afficher les résultats de la recherche.

## Utiliser l’interpréteur de commandes pour copier les résultats de la recherche

Après avoir utilisé la cmdlet **New-MailboxSearch** pour créer une recherche de découverte électronique inaltérable, vous devez lancer la recherche pour copier les messages dans la boîte aux lettres de découverte que vous avez indiquée dans le paramètre *TargetMailbox*. Pour plus d’informations sur la création de recherches de découverte électronique à l’aide de l’interpréteur de commandes, voir :

  - [Use the Shell to create an In-Place eDiscovery search](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd298064\(v=exchg.150\))

Par exemple, vous devez exécuter la commande suivante pour lancer une recherche de découverte automatique nommée *Fabrikam Investigation* et copier les résultats de la recherche vers la boîte aux lettres de découverte spécifiée.

    Start-MailboxSearch "Fabrikam Investigation"

Si vous avez utilisé le commutateur *EstimateOnly* pour obtenir une estimation des résultats de la recherche, vous devez le supprimer pour pouvoir copier ces derniers. Vous devez également indiquer une boîte aux lettres de découverte vers laquelle copier les résultats de la recherche. Par exemple, supposons que vous ayez créé une recherche à des fins d’estimation uniquement à l’aide de la commande suivante :

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

Pour copier les résultats de cette recherche vers une boîte aux lettres de découverte, vous devez exécuter les commandes suivantes :

    Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"

    Start-MailboxSearch "FY13 Q2 Financial Results"

## Plus d’informations sur la copie des résultats de la recherche

  - Une fois les résultats de la recherche copiés dans une boîte aux lettres de découverte, vous pouvez les exporter vers un fichier PST. Pour plus d’informations, voir [Exporter les résultats de la recherche électronique vers un fichier PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

  - Pour plus d’informations sur les éléments ne pouvant pas faire l’objet d’une recherche, voir [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - Si vous copiez tout le contenu de la boîte aux lettres correspondant à une plage de dates précise (mais sans spécifier aucun mot-clé dans les critères de recherche), tous les éléments ne pouvant pas faire l’objet d’une recherche dans cette plage de dates seront automatiquement inclus dans les résultats de la recherche. Par conséquent, n’activez pas la case à cocher **Inclure les éléments qui ne peuvent pas être recherchés** lors de la copie des résultats. Sinon, une copie de tous ces éléments sera placée dans la boîte aux lettres de découverte.

  - Outre la copie des résultats de la recherche vers une boîte aux lettres de découverte, vous pouvez également estimer ou prévisualiser les résultats d’une recherche sélectionnée.
    
      - **Estimation des résultats de recherche** : cette option permet d’obtenir une estimation de la taille totale et du nombre d’éléments renvoyés par la recherche en fonction des critères spécifiés. Les estimations sont affichées dans le volet Détails du CAE.
    
      - **Prévisualiser les résultats de recherche** : cette option vous permet de prévisualiser les résultats renvoyés par la recherche au lieu d’avoir à les copier vers une boîte aux lettres de découverte pour les afficher. C’est un moyen rapide de déterminer si les résultats de la recherche sont pertinents. Après avoir prévisualisé les résultats, vous pouvez réviser votre requête pour les affiner, puis relancer la recherche. Les éléments de la page d’aperçu correspondent à des versions en lecture seule des résultats réels de la recherche. Par conséquent, vous ne pouvez pas les déplacer, les modifier, les supprimer ni les transférer sur la page d’aperçu.
    
    Pour plus d’informations, voir [Estimate or preview search results](create-an-in-place-ediscovery-search-exchange-2013-help.md).

