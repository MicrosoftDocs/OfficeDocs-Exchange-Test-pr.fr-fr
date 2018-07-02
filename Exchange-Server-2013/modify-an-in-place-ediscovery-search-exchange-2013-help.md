---
title: 'Modifier une recherche de découverte électronique inaltérable: Exchange 2013 Help'
TOCTitle: Modifier une recherche de découverte électronique inaltérable
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50477840
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier une recherche de découverte électronique inaltérable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-08-27_

Après avoir créé une recherche de découverte électronique locale, vous pouvez la modifier pour choisir d'autres paramètres de recherche. Par exemple, vous pouvez modifier les boîtes aux lettres à rechercher, les plages de dates, les mot clés, les options de journalisation, ou encore spécifier une boîte aux lettres de découverte différente pour stocker les résultats de la recherche. Les modifications que vous apportez aux propriétés de la recherche seront utilisées lors du redémarrage de la recherche.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si une recherche de découverte électronique locale est en cours d'exécution, vous devez l'arrêter avant de la modifier. Quand vous redémarrez la recherche, les résultats de la dernière exécution de la recherche sont supprimés de la boîte aux lettres de découverte. Toutefois, les journaux correspondant aux recherches précédentes sont conservés.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 2 à 5 minutes.

  - Une recherche de découverte électronique locale a été créée et n'est pas en cours d'exécution.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « In-Place eDiscovery » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le CAE pour modifier une recherche de découverte électronique locale

1.  Accédez à **Gestion de la conformité** \> **Découverte électronique et blocage sur place**.

2.  Dans l’affichage Liste, sélectionnez la recherche de découverte électronique sur place à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **Découverte électronique locale et Archive permanente**, vous pouvez modifier les paramètres suivants :
    
      - Dans la page **Nom**, modifiez le nom pour la recherche et la description facultative.
    
      - Dans la page **Boîtes aux lettres**, modifiez les boîtes aux lettres à rechercher. Vous pouvez rechercher dans toutes les boîtes aux lettres ou sélectionner celles qui sont spécifiques à la recherche.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous ne pouvez pas utiliser l’option <strong>Rechercher toutes les boîtes aux lettres</strong> pour mettre en attente toutes les boîtes aux lettres des serveurs de messagerie Exchange 2013. Pour créer une archive permanente, vous devez sélectionner <strong>Spécifier les boîtes aux lettres à rechercher</strong>. Pour plus d'informations, consultez la rubrique <a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Créer ou supprimer une conservation inaltérable</a>.</td>
        </tr>
        </tbody>
        </table>
    
      - Dans la page **Requête de recherche**, modifiez les champs suivants :
        
          - **Inclure tout le contenu des boîtes aux lettres utilisateur**   Activez cette option pour placer tout le contenu dans les boîtes aux lettres sélectionnées mises en attente.
        
          - **Filtrer en fonction des critères**   Activez cette option pour spécifier les critères de recherche, y compris les mots clés, les dates de début et de fin, les adresses des expéditeurs et des destinataires et les types de messages.
    
      - Dans la page **Archive permanente**, activez la case à cocher **Mettre en attente le contenu correspondant à la requête de recherche des boîtes aux lettres sélectionnées**, puis activez l'une des options suivantes pour mettre des éléments en archive permanente :
        
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
            <td>Quand des boîtes aux lettres ou des articles sont mis en archive permanente à des fins juridiques, il est généralement recommandé de bloquer les articles indéfiniment et de supprimer la suspension quand le jugement ou l'enquête est terminé.</td>
            </tr>
            </tbody>
            </table>


4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier une recherche de découverte électronique locale

Cet exemple modifie la recherche de découverte électronique locale Search-Project Contoso pour rechercher des boîtes aux lettres appartenant à des membres du groupe de distribution DG-ProjectManagers.

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement modifié une recherche de découverte électronique locale, effectuez l'une des opérations suivantes :

  - Utilisez le CAE pour vérifier les propriétés de la recherche.

  - Exemples

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez <strong>Get-MailboxSearch</strong> dans Exchange Online pour récupérer des informations sur une recherche de découverte électronique, vous devez spécifier le nom d’une recherche pour renvoyer la liste complète des propriétés de recherche ; par exemple, <code>Get-MailboxSearch &quot;Contoso Legal Case&quot;</code>. Si vous exécutez la cmdlet <strong>Get-MailboxSearch</strong> sans utiliser les paramètres, les propriétés suivantes ne sont pas renvoyées :
<ul>
<li><p>SourceMailboxes</p></li>
<li><p>Sources</p></li>
<li><p>SearchQuery</p></li>
<li><p>ResultsLink</p></li>
<li><p>PreviewResultsLink</p></li>
<li><p>Erreurs</p></li>
</ul>
Ceci dû au fait que de nombreuses ressources sont nécessaires pour renvoyer ces propriétés pour toutes les recherches de découverte électronique dans votre organisation.</td>
</tr>
</tbody>
</table>

