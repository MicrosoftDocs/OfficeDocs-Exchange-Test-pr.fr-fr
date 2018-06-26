---
title: 'Créer une recherche de découverte électronique inaltérable: Exchange 2013 Help'
TOCTitle: Créer une recherche de découverte électronique inaltérable
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50479652
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une recherche de découverte électronique inaltérable

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-01-17_

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous avons différé la date d’échéance du 1er juillet 2017 pour créer ds recherches de découverte électronique inaltérable dans Exchange Online (dans les plans autonomes Office 365 et Exchange Online). Mais plus tard cette année ou au début de l’année prochaine, vous ne pourrez pas créer des recherches dans Exchange Online. Pour créer des recherches de découverte électronique, veuillez commencer à utiliser la <a href="https://go.microsoft.com/fwlink/?linkid=847843">recherche de contenu</a> dans le Centre de conformité et sécurité Office 365. Lorsque nous aurons désactivé les nouvelles recherches de découverte électronique inaltérable, vous pourrez toujours modifier les recherches de découverte électronique inaltérable existantes, et la création de nouvelles recherches de découverte électronique inaltérable sera toujours prise en charge dans les déploiements hybrides Exchange Server 2013 et Exchange.</td>
</tr>
</tbody>
</table>


La [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) vous permet d'effectuer une recherche dans tout le contenu d'une boîte aux lettres, y compris dans les éléments supprimés et les versions originales d'éléments modifiés pour les utilisateurs placés en [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « In-Place eDiscovery » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour créer des recherches de découverte électronique, vous devez disposer d’une adresse SMTP dans l’organisation dans laquelle vous créez les recherches. Ainsi, dans Exchange Online, pour créer des recherches de découverte électronique, vous devez disposer d’une boîte aux lettres Exchange Online (plan 2) sous licence. Dans une organisation hybride Exchange, votre boîte aux lettres Exchange sur site doit disposer d’un compte d’utilisateur de messagerie correspondant dans votre organisation Office 365 pour que vous puissiez rechercher des boîtes aux lettres Exchange Online. Sinon, si vous vous connectez avec un compte qui n’existe que dans Office 365, tel que le compte d’administrateur client, une licence Exchange Online (plan 2) doit être attribuée à ce compte.

  - Le programme d'installation d'Exchange 2013 crée une boîte aux lettres de découverte appelée **Boîte aux lettres de découverte** pour copier les résultats de la recherche. La boîte aux lettres de découverte est également créée par défaut dans Exchange Online. Vous pouvez créer des boîtes aux lettres de découverte supplémentaires. Pour plus d'informations, consultez la rubrique [Créer une boîte aux lettres de découverte](create-a-discovery-mailbox-exchange-2013-help.md).

  - Lorsque vous créez une recherche de découverte électronique locale, les messages renvoyés dans les résultats de la recherche ne sont pas automatiquement copiés dans une boîte aux lettres de découverte. Après avoir créé la recherche, vous pouvez utiliser le Centre d’administration Exchange (CAE) pour estimer et afficher un aperçu des résultats de la recherche, ou les copier dans une boîte aux lettres de découverte. Pour obtenir des informations détaillées, voir :
    
      - Estimate or preview search results (dans la suite de cette rubrique)
    
      - [Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

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


## Utiliser le Centre d'administration Exchange (CAE) pour créer une recherche de découverte électronique locale

Comme expliqué précédemment, pour créer des recherches de découverte électronique, vous devez vous connecter à un compte d’utilisateur qui dispose d’une adresse SMTP dans votre organisation.

1.  Accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**.

2.  Cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **Découverte électronique locale et archive permanente**, dans la page **Nom et description**, tapez un nom pour la recherche et ajoutez une description facultative, puis cliquez sur **Suivant**.

4.  Dans la page **Boîtes aux lettres**, sélectionnez les boîtes aux lettres dans lesquelles effectuer la recherche. Vous pouvez rechercher dans toutes les boîtes aux lettres ou sélectionner celles qui sont propres à la recherche. Dans Exchange Online, vous pouvez également sélectionner des groupes Office 365 comme source de contenu pour la recherche.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous ne pouvez pas utiliser l’option <strong>Rechercher toutes les boîtes aux lettres</strong> pour bloquer toutes les boîtes aux lettres. Pour créer une archive permanente, vous devez sélectionner <strong>Spécifier les boîtes aux lettres à rechercher</strong>. Pour plus d'informations, consultez la rubrique <a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Créer ou supprimer une conservation inaltérable</a>.</td>
    </tr>
    </tbody>
    </table>


5.  Dans la page **Requête de recherche**, complétez les champs suivants :
    
      - **Inclure tout le contenu des boîtes aux lettres utilisateur**   Activez cette option pour placer tout le contenu dans les boîtes aux lettres sélectionnées mises en attente. Si vous sélectionnez cette option, vous ne pouvez pas spécifier de critères de recherche supplémentaires.
    
      - **Filtrer en fonction des critères**   Activez cette option pour spécifier les critères de recherche, y compris les mots clés, les dates de début et de fin, les adresses des expéditeurs et des destinataires et les types de messages.
        
        ![Configurer une requête de recherche de découverte électronique](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurer une requête de recherche de découverte électronique")  
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les champs <strong>De :</strong> et <strong>À/Cc/Cci :</strong> sont connectés par un opérateur <strong>OR</strong> dans la requête de recherche qui est créée lorsque vous exécutez la recherche. Cela signifie que tous les messages envoyés ou reçus par les utilisateurs spécifiés (et correspondant aux autres critères de recherche) sont inclus dans les résultats de la recherche.<br />
    Les dates sont connectées par un opérateur <strong>AND</strong>.</td>
    </tr>
    </tbody>
    </table>


6.  Dans la page **Paramètres du blocage sur place**, vous pouvez cocher la case **Mettre en attente le contenu correspondant à la requête de recherche des boîtes aux lettres sélectionnées** et sélectionnez une des options suivantes pour placer des éléments en blocage local :
    
      - **Bloquer indéfiniment**   Activez cette option pour placer les articles retournés sur suspension indéfini. Les éléments en attente seront conservés jusqu'à ce que vous supprimiez la boîte aux lettres de la recherche ou que vous supprimiez la recherche.
    
      - **Spécifier le nombre de jours pour mettre en attente les articles en fonction de leur date de réception** Utilisez cette option pour bloquer les articles pendant une période donnée. Par exemple, vous pouvez utiliser cette option si votre organisation exige que tous les messages soient conservés pendant au moins sept ans. Vous pouvez utiliser une archive locale *basée sur le temps* parallèlement à une stratégie de rétention pour garantir que les éléments seront supprimés dans sept ans.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Lorsque des boîtes aux lettres ou des articles sont mis en archive permanente à des fins juridiques, il est généralement recommandé de bloquer les articles indéfiniment et de supprimer la suspension lorsque le jugement ou l'enquête est terminé.</td>
        </tr>
        </tbody>
        </table>


7.  Cliquez sur **Terminer** pour enregistrer la recherche et renvoyer une estimation de la taille totale et du nombre d’éléments qui seront renvoyés par la recherche d’après les critères que vous spécifiez. Les estimations sont affichées dans le volet d'informations. Cliquez sur **Actualiser**![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser") pour mettre à jour les informations affichées dans le volet de détails.

Retour au début

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une recherche de découverte électronique locale

Cet exemple crée la recherche de découverte électronique locale appelée Discovery-CaseId012 qui recherche les éléments contenant les mots clés Contoso et ProjectA et qui remplissant également les critères suivants :

  - Date de début : 01/01/09

  - Date de fin : 31/12/2011

  - Boîte aux lettres source : DG-Finance

  - Boîte aux lettres cible : Boîte aux lettres de découverte

  - Types de messages : Email

  - Inclut des éléments impossibles à rechercher dans les statistiques de la recherche

  - Niveau de journalisation : Complet

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous ne précisez pas d’autres paramètres de recherche lorsque vous effectuez une recherche de découverte électronique locale, tous les éléments dans les boîtes aux lettres sources spécifiées sont renvoyés dans les résultats. Si vous ne précisez pas de boîtes aux lettres à rechercher, la recherche a lieu dans toutes les boîtes aux lettres de votre organisation Exchange ou Exchange Online.</td>
</tr>
</tbody>
</table>


    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous utilisez les paramètres <em>StartDate</em> et <em>EndDate</em>, vous devez utiliser le format de date mm/jj/aaaa, même si les paramètres de votre ordinateur local sont configurés pour utiliser un format de date différent, comme jj/mm/aaaa. Par exemple, pour rechercher des messages envoyés entre le 1er avril 2013 et le 1er juillet 2013, vous devez utiliser <strong>04/01/2013</strong> et <strong>07/01/2013</strong> pour les dates de début et de fin.</td>
</tr>
</tbody>
</table>


Cet exemple crée une recherche de découverte électronique inaltérable appelée HRCase090116 qui recherche les messages électroniques envoyés par Alex Darrow à Sara Davis en 2015.

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

Après avoir utilisé l’environnement de ligne de commande Exchange Management Shell pour créer une recherche de découverte électronique locale, vous devez lancer la recherche à l’aide de la cmdlet **Start-MailboxSearch** pour copier des messages vers la boîte aux lettres de découverte indiquée dans le paramètre *TargetMailbox*. Pour plus d’informations, voir [Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd298064\(v=exchg.150\)).

Retour au début

## Utiliser le CAE pour obtenir une estimation et un aperçu des résultats de la recherche

Après avoir créé une recherche de découverte électronique locale, vous pouvez utiliser le CAE pour obtenir une estimation et un aperçu des résultats de la recherche. Si vous avez créé une recherche à l’aide de la cmdlet **New-MailboxSearch**, vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour lancer la recherche et obtenir une estimation des résultats de cette recherche. Vous ne pouvez pas utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher un aperçu des messages renvoyés dans les résultats de la recherche.

1.  Accédez à **Gestion de la conformité** \>**Découverte électronique et blocage sur place**.

2.  Dans l’affichage Liste, sélectionnez la recherche de découverte électronique sur place, puis exécutez l’une des procédures suivantes :
    
      - Cliquez sur **Recherche**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche") \> **Estimation des résultats de recherche** pour obtenir une estimation de la taille totale et du nombre d’éléments qui seront renvoyés par la recherche d’après les critères que vous spécifiez. Sélectionnez cette option pour relancer la recherche et obtenir une estimation.
        
        Les estimations de la recherche sont affichées dans le volet de détails. Cliquez sur **Actualiser**![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser") pour mettre à jour les informations affichées dans le volet de détails.
    
      - Cliquez sur **Aperçu des résultats de recherche** dans le volet des détails pour prévisualiser les résultats une fois l’estimation de la recherche terminée. La sélection de cette option ouvre la fenêtre **Aperçu de la recherche eDiscovery**. Tous les messages renvoyés par les boîtes aux lettres qui ont fait l’objet d’une recherche sont affichés.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Les boîtes aux lettres qui ont fait l’objet d’une recherche sont répertoriées dans le volet de droite de la fenêtre <strong>Aperçu de la recherche eDiscovery</strong>. Pour chaque boîte aux lettres, le nombre d’éléments renvoyés et la taille totale de ces éléments sont également affichés. Tous les éléments renvoyés par la recherche sont répertoriés dans le volet de droite et peuvent être triés par date la plus récente ou la plus ancienne. Les éléments de chaque boîte aux lettres ne peuvent pas s’afficher dans le volet de droite en cliquant sur une boîte aux lettres dans le volet de gauche. Pour afficher les éléments renvoyés par une boîte aux lettres spécifique, vous pouvez copier les résultats de la recherche et afficher les éléments dans la boîte aux lettres de découverte.</td>
        </tr>
        </tbody>
        </table>
    
    ![Obtenir une estimation et un aperçu des résultats de la recherche](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "Obtenir une estimation et un aperçu des résultats de la recherche")  

Retour au début

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour estimer les résultats de la recherche

Vous pouvez utiliser le commutateur *EstimateOnly* pour renvoyer uniquement une estimation des résultats de la recherche et ne pas copier les résultats dans une boîte aux lettres de découverte. Vous devez lancer une recherche d’estimation uniquement avec la cmdlet **Start-MailboxSearch**. Vous pouvez ensuite récupérer les résultats de la recherche estimés avec la cmdlet **Get-MailboxSearch**.

Par exemple, vous devez exécuter les commandes suivantes pour créer une recherche de découverte électronique, puis afficher une estimation des résultats de la recherche :

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics

    Start-MailboxSearch "FY13 Q2 Financial Results"

    Get-MailboxSearch "FY13 Q2 Financial Results"

Pour afficher des informations spécifiques sur les résultats de la recherche estimés à partir de l’exemple précédent, vous pouvez exécuter la commande suivante :

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

Retour au début

## Plus d’informations sur les recherches de découverte électronique

  - Après avoir créé une recherche de découverte électronique, vous pouvez copier les résultats de cette recherche dans la boîte aux lettres de découverte et les exporter dans un fichier PST. Pour plus d’informations, voir :
    
      - [Copier les résultats de la recherche de découverte automatique dans une boîte aux lettres de découverte](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [Exporter les résultats de la recherche électronique vers un fichier PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - Une fois que vous avez exécuté une estimation de recherche de découverte électronique (cela inclut les mots-clés dans les critères de recherche), vous pouvez consulter les statistiques de mots-clés en cliquant sur **Afficher les statistiques sur les mots clés** dans le volet Détails de la recherche sélectionnée. Ces statistiques présentent des informations sur le nombre d’éléments renvoyés pour chaque mot-clé utilisé dans la requête de recherche. Toutefois, si plus de 100 boîtes aux lettres source sont incluses dans la recherche, une erreur sera renvoyée si vous tentez d’afficher les statistiques sur les mots-clés. Pour afficher les statistiques sur les mots-clés, vous ne pouvez pas inclure plus de 100 boîtes aux lettres source dans la recherche.

  - Si vous utilisez **Get-MailboxSearch** dans Exchange Online pour récupérer des informations sur une recherche de découverte électronique, vous devez spécifier le nom d’une recherche pour renvoyer la liste complète des propriétés de recherche ; par exemple, `Get-MailboxSearch "Contoso Legal Case"`. Si vous exécutez la cmdlet **Get-MailboxSearch** sans utiliser les paramètres, les propriétés suivantes ne sont pas renvoyées :
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    Ceci est dû au fait que de nombreuses ressources sont nécessaires pour renvoyer ces propriétés pour toutes les recherches de découverte électronique dans votre organisation.

Retour au début

