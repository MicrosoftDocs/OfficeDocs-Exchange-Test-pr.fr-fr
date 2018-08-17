---
title: 'Réamorcer le catalogue de recherche: Exchange 2013 Help'
TOCTitle: Réamorcer le catalogue de recherche
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52062986
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réamorcer le catalogue de recherche

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Si le catalogue d'indexation de contenu d'une copie de base de données de boîte aux lettres est corrompu, vous devrez peut-être réamorcer le catalogue. Les index de contenu corrompus sont indiqués dans le journal des événements d'application par l'événement suivant.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID d'événement</th>
<th>Niveau</th>
<th>Source</th>
<th>Détails</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>Erreur</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>À l'&lt;<em>horodatage</em>&gt;, la copie de l'&lt;<em>identité</em>&gt; de base de données des banques d'informations de Microsoft Exchange sur ce serveur a rencontré un problème de catalogue de recherche corrompu. Pour obtenir des informations détaillées sur cette erreur, recherchez les autres événements « ExchangeStoreDb » et « MSExchange Search Indexer » dans le journal des événements sur le serveur. Nous vous recommandons d'effectuer un réamorçage du catalogue via la tâche « Update-MailboxDatabaseCopy ».</p></td>
</tr>
</tbody>
</table>


Si la copie de base de données de boîtes aux lettres se trouve sur un serveur qui fait partie d’un groupe de disponibilité de base de données (DAG), vous pouvez réamorcer le catalogue d’indexation de contenu à partir d’un autre membre du DAG.

Si la copie de base de données de boîte aux lettres est la seule copie, vous devez créer manuellement un catalogue d’indexation de contenu.

Pour les autres tâches de gestion concernant le service de recherche Exchange, consultez la rubrique [Procédures relatives au service de recherche Exchange](exchange-search-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 minutes. La durée actuelle du réamorçage peut varier en fonction de la taille du catalogue d'indexation de contenu.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Exchange Search » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Réamorcer le catalogue d’indexation de contenu si la base de données de boîtes aux lettres fait partie d’un DAG

Utilisez l’une des procédures suivantes si la base de données de boîtes aux lettres se trouve sur un serveur qui fait partie d’un DAG.

## Réamorcer le catalogue d'indexation de contenu à partir de n'importe quelle source

Cet exemple réamorce le catalogue d’indexation de contenu pour la copie de base de données DB1 sur le serveur de boîtes aux lettres MBX1 à partir de n’importe quel serveur source du DAG qui dispose d’une copie de base de données.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

## Réamorcer le catalogue d'indexation de contenu à partir d'une source spécifique

Cet exemple réamorce le catalogue d'indexation de contenu pour la copie de base de données DB1 sur le serveur de boîte aux lettres MBX1 à partir du serveur de boîte aux lettres MBX2 qui dispose également d'une copie de la base de données.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

## Réamorcer le catalogue d’indexation de contenu s’il existe une seule copie de la base de données de boîtes aux lettres

S’il existe une seule copie de la base de données de boîtes aux lettres, vous devez réamorcer manuellement le catalogue de recherche en recréant le catalogue d’indexation de contenu.

1.  Exécutez les commandes suivantes pour arrêter la recherche Microsoft Exchange et les services du contrôleur de l’hôte de la recherche Microsoft Exchange.
    
    ```
        Stop-Service MSExchangeFastSearch
    ```
    
    ```
        Stop-Service HostControllerService
    ```

2.  Supprimez, déplacez ou renommez le dossier qui contient le catalogue d’indexation de contenu Exchange. Le nom de ce dossier est `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`. Par exemple, vous pouvez renommer le dossier `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`.
    
    > [!NOTE]
    > La suppression de ce dossier libère de l’espace disque supplémentaire. Vous pouvez également renommer ou déplacer le dossier pour le conserver à des fins de dépannage.


3.  Exécutez les commandes suivantes pour redémarrer la recherche Microsoft Exchange et les services du contrôleur de l’hôte de la recherche Microsoft Exchange.
    
    ```
        Start-Service MSExchangeFastSearch
    ```    
    ```
        Start-Service HostControllerService
    ```
    Après le redémarrage de ces services, la recherche Exchange recrée le catalogue d’indexation de contenu.

## Comment savoir si cela a fonctionné ?

Le réamorçage du catalogue d’indexation de contenu par la recherche Exchange peut prendre un certain temps. Exécutez la commande suivante pour afficher l’état du processus de réamorçage :

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

Lorsque le réamorçage du catalogue de recherche est en cours, la valeur de la propriété *ContentIndexState* est **Crawling**. Une fois le réamorçage terminé, la valeur affichée est **Healthy**.

