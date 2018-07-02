---
title: 'Diagnostic des problèmes d’Exchange Search: Exchange 2013 Help'
TOCTitle: Diagnostic des problèmes d’Exchange Search
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52062998
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Diagnostic des problèmes d’Exchange Search

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Exchange Search indexe les boîtes aux lettres et les pièces jointes prises en charge dans les boîtes aux lettres Exchange. Avec l’augmentation des volumes de courriers électroniques, l’augmentation des tailles de boîtes aux lettres et des quotas de stockage, la mise en service des boîtes aux lettres d’archivage pour les utilisateurs, et la découverte électronique inaltérable pour effectuer des recherches de découverte, Exchange Search est un composant essentiel des serveurs de boîtes aux lettres dans votre organisation Microsoft Exchange Server 2013. Les problèmes liés à Exchange Search peuvent avoir une incidence sur la productivité des utilisateurs et la fonctionnalité de découverte électronique inaltérable.

Pour en savoir plus sur Exchange Search, consultez la rubrique [Service de recherche Exchange](exchange-search-exchange-2013-help.md).

Souhaitez-vous rechercher les tâches de gestion liées à Exchange Search ? Voir [Procédures relatives au service de recherche Exchange](exchange-search-procedures-exchange-2013-help.md).

## Utilisation de la cmdlet Test-ExchangeSearch

L’étape 5 de la procédure de cette rubrique décrit l’exécution de la cmdlet **Test-ExchangeSearch** permettant de diagnostiquer les problèmes Exchange Search. Vous pouvez utiliser la cmdlet **Test-ExchangeSearch** pour tester la fonctionnalité Exchange Search pour un serveur de boîtes aux lettres, une base de données de boîtes aux lettres ou une boîte aux lettres spécifique. La cmdlet fournit un message de test à la boîte aux lettres spécifiée (ou à une boîte aux lettres du système de base de données si aucune boîte aux lettres n’est spécifiée), puis effectue une recherche pour déterminer si le message est indexé, en incluant l’heure de l’indexation. En conditions normales d’utilisation, Exchange Search indexe un message 10 secondes après sa création ou son transfert vers une boîte aux lettres. Le message de test est automatiquement supprimé après le test.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Test-ExchangeSearch](https://technet.microsoft.com/fr-fr/library/bb124733\(v=exchg.150\)).

## Récupération des éléments impossibles à rechercher

Vous pouvez utiliser la cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/fr-fr/library/dd351154\(v=exchg.150\)) pour extraire une liste d’éléments de boîte aux lettres impossibles à rechercher qui n’ont pas pu être indexés par Exchange Search. Vous pouvez exécuter la cmdlet sur un serveur de boîtes aux lettres, une base de données de boîtes aux lettres ou une boîte aux lettres spécifique. La cmdlet renvoie des détails relatifs à chaque élément qui n’a pas pu être recherché. Il existe plusieurs raisons pour lesquelles un élément de boîte aux lettres ne peut pas être recherché ; par exemple, un message électronique peut contenir un type de fichier de pièce jointe qui ne peut pas être indexé pour la recherche ou un filtre de recherche n’est pas installé ou est désactivé. Si un filtre de recherche pour ce type de fichier est disponible, vous pouvez l’installer sur vos serveurs exExchangeNoVersionExchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les filtres de recherche fournis par Microsoft sont testés et pris en charge par Microsoft. Nous vous recommandons de tester les filtres de recherche tiers dans un environnement de test avant de les installer sur des serveurs exExchangeNoVersionExchange dans un environnement de production.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les éléments impossibles à rechercher, consultez :

  - [Formats de fichier indexés par le service de recherche Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Diagnostic des problèmes d’Exchange Search

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Exchange Search » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

1.  **Vérifier l’état du service**   Le service Microsoft Exchange Search (MSExchangeFastSearch) a-t-il démarré sur le serveur de boîtes aux lettres ? Si la réponse est Oui, allez à l’étape 2. Sinon, utilisez le composant logiciel enfichable Services MMC pour vérifier que le service MSExchangeFastSearch est en cours d’exécution en procédant comme suit :
    
    1.  Cliquez sur **Démarrer**, pointez sur **Outils d’administration**, puis cliquez sur **Services**.
    
    2.  Dans **Services**, vérifiez que l’**état** pour le service **Microsoft Exchange Search** est répertorié comme étant **démarré**.

2.  **Vérifier la configuration de la base de données de boîtes aux lettres**   Le paramètre *IndexEnabled* est-il défini à true (activé) pour la base de données de boîtes aux lettres de l’utilisateur ? Si oui, allez à l’étape 3. Si non, exécutez la commande suivante dans l’environnement de ligne de commande Shell pour vérifier que l’indicateur *IndexEnabled* est défini à true (activé).
    
        Get-MailboxDatabase | Format-Table Name,IndexEnabled
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)).

3.  **Vérifier l’état de recherche de la base de données de boîtes aux lettres**   La base de données Exchange a-t-elle été recherchée ? Si oui, passez à l'étape 4. Sinon, utilisez l’Analyseur de performances et de fiabilité pour vérifier le compteur **Robot : boîtes aux lettres restantes** de l’objet de performances **Index de recherche MSExchange**. Effectuez les opérations suivantes :
    
    1.  Ouvrez l’**Analyseur de performances** (perfmon.exe).
    
    2.  Dans l’arborescence de la console, sous **Outils de contrôle**, cliquez sur **Analyseur de performances**.
    
    3.  Dans le volet de l’Analyseur de performances, cliquez sur **Ajouter** (signe plus vert).
    
    4.  Dans **Ajouter des compteurs**, sous la liste **Choisir les compteurs sur**, sélectionnez le serveur sur lequel se trouve la base de données de boîtes aux lettres que vous souhaitez contrôler.
    
    5.  Dans la zone sans titre située sous la liste **Choisir les compteurs sur**, sélectionnez l’objet de performances **Index de recherche MSExchange**.
    
    6.  Dans la zone **Instances de l’objet sélectionné**, sélectionnez l’instance pour la base de données de boîtes aux lettres de l’utilisateur.
    
    7.  Cliquez sur **Ajouter**, puis sur **OK**.
        
        Dans le volet de l’Analyseur de performances, l’objet de performances **Index de recherche MSExchange** est répertorié dans la colonne **Objet** et ses différents compteurs sont répertoriés dans la colonne **Compteur**.
    
    8.  Consultez le compteur **Robot : boîtes aux lettres restantes**. Toute valeur supérieure ou égale à 1 indique que les boîtes aux lettres dans la base de données sont encore en cours d'analyse. Une fois l’analyse terminée, la valeur est **0**.
    
    Pour plus d’informations sur l’utilisation de l’Analyseur de performances, consultez le [Guide pas à pas de l’analyse des performances et de la fiabilité dans Windows Server 2008](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **Vérifier l’intégrité de l’indexation de la copie de base de données**   L’index du contenu est-il correct ? Utilisez la cmdlet **Get-MailboxDatabaseCopyStatus** pour vérifier l’intégrité d’indexation du contenu pour une copie de base de données.
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/fr-fr/library/dd298044\(v=exchg.150\)).

5.  **Exécuter la cmdlet Test-ExchangeSearch**   Si la base de données de boîte aux lettres a déjà été recherchée, vous pouvez exécuter la cmdlet **Test-ExchangeSearch** pour la base de données de boîtes aux lettres ou pour une boîte aux lettres spécifique.
    
        Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Test-ExchangeSearch](https://technet.microsoft.com/fr-fr/library/bb124733\(v=exchg.150\)).

6.  **Vérifier le journal des événements d’application**   À l’aide de l’Observateur d’événements ou de l’environnement de ligne de commande Exchange Management Shell, vérifiez le journal des événements d’application pour les messages d’erreur relatifs à la recherche. Recherchez les sources d’événements suivantes.
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    Pour plus d’informations, suivez le lien dans l’entrée du journal des événements.

7.  **Redémarrer le service Microsoft Exchange Search**   Utilisez le composant logiciel enfichable Services MMC ou l’environnement de ligne de commande Exchange Management Shell pour arrêter puis redémarrer le service Microsoft Exchange Search (MSExchangeFastSearch) :
    
    1.  Cliquez sur **Démarrer**, pointez sur **Outils d'administration**, puis cliquez sur **Services**.
    
    2.  Dans **Services**, cliquez avec le bouton droit de la souris sur **Microsoft Exchange Search**, puis cliquez sur **Arrêter**. Après l’arrêt du service, cliquez de nouveau avec le bouton droit sur le service, puis cliquez sur **Démarrer**.

8.  **Réamorcer le catalogue de recherche**   Dans certains cas, lorsque le catalogue de recherche est corrompu, vous devrez peut-être le réamorcer. Lorsqu’un catalogue de recherche doit être réamorcé, Exchange Search vous le signale en enregistrant les entrées dans le journal des événements d’application. Pour plus d’informations sur le réamorçage du catalogue de recherche, voir [Réamorcer le catalogue de recherche](reseed-the-search-catalog-exchange-2013-help.md).

