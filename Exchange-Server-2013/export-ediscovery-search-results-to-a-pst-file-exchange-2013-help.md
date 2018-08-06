---
title: 'Export des résult. de la rech. électr. vers un fichier PST: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Exporter les résultats de la recherche électronique vers un fichier PST
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59634306
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exporter les résultats de la recherche électronique vers un fichier PST

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-09-07_

Vous pouvez utiliser l’outil d’exportation d’eDiscovery dans le Centre d’administration Exchange (EAC) pour exporter les résultats d’une recherche d’e-Discovery en Place dans un fichier de données Outlook, également appelé un fichier PST. Les administrateurs peuvent distribuer les résultats de la recherche à d’autres personnes au sein de votre organisation, comme un gestionnaire de ressources humaines ou enregistrements, ou de s’opposer à conseiller dans un cas juridique. Une fois les résultats de la recherche sont exportés vers un fichier PST, vous ou autres utilisateurs peuvent les ouvrir dans Outlook pour visualiser ou imprimer les messages renvoyés dans les résultats de recherche. Fichiers PST peuvent également être ouvert dans l’e-Discovery de tiers et des applications. Cette rubrique vous indique comment effectuer cette opération, ainsi que résoudre les problèmes que vous pouvez avoir.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : La durée varie en fonction de la quantité et de la taille des résultats de recherche exportés.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « eDiscovery inaltérable » dans la rubrique relative à la [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - L’ordinateur que vous utilisez pour exporter les résultats vers un fichier PST doit répondre aux conditions suivantes :
    
      - versions 32 ou 64 bits de Windows 7 et versions ultérieures
    
      - Microsoft.NET Framework 4.7
    
      - un navigateur pris en charge :
        
          - Internet Explorer 10 et versions ultérieures
            
            OU
        
          - Mozilla Firefox ou Google Chrome. Si vous utilisez l’un de ces navigateurs, veillez à installer l’extension *ClickOnce*. Pour installer le complément ClickOnce, reportez-vous à la page de recherche de [module ClickOnce de Mozilla](https://addons.mozilla.org/fr-fr/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) ou la page de recherche d’extensions [ClickOnce pour Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions).

  - Vous devez disposer d’une boîte aux lettres active liée au compte que vous souhaitez exporter.

  - Assurez-vous que les paramètres intranet locaux sont correctement configurés dans Internet Explorer. Vérifiez que l’URL **https://\*.outlook.com** est ajoutée à la zone Intranet local.

  - Assurez-vous que les URL suivantes ne figurent pas dans la zone Sites de confiance.
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Centre d’administration Exchange pour exporter les résultats de recherche eDiscovery inaltérable vers un fichier PST

1.  Accédez à **Gestion de la conformité** \> **Découverte électronique et conservation inaltérables**.

2.  Dans l’affichage Liste, sélectionnez la recherche de découverte électronique locale dont vous souhaitez exporter les résultats, puis cliquez sur **Exporter vers un fichier PST**.
    
    ![Exporter vers un fichier PST](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "Exporter vers un fichier PST")  

3.  Dans la fenêtre **Outil d’exportation au format PST de la découverte électronique**, effectuez les opérations suivantes :
    
      - Cliquez sur **Parcourir** pour spécifier l’emplacement où vous souhaitez télécharger le fichier PST.
    
      - Cochez la case **Activer la déduplication** pour exclure les messages en double. Une seule instance d’un message sera incluse dans le fichier PST.
    
      - Cochez la case **Inclure les éléments impossibles à rechercher** pour inclure les éléments de boîte aux lettres qu’il n’est pas possible de rechercher (par exemple, les messages avec des pièces jointes dans des types de fichiers qu’Exchange Search ne peut pas indexer). Les éléments impossibles à rechercher sont exportés dans un fichier PST distinct.
        
        > [!IMPORTANT]
		> Inclure les éléments impossibles à rechercher lorsque vous exportez les résultats de la recherche de découverte électronique prend plus de temps lorsque les boîtes aux lettres contiennent un grand nombre d’éléments impossibles à rechercher. Pour réduire le temps nécessaire pour exporter les résultats de la recherche et pour éviter les fichiers d’exportation PST volumineux, tenez compte des recommandations suivantes :
        > <ul>
        > <li><p>Créez plusieurs recherches de découverte électronique qui recherchent chacune un petit nombre de boîtes aux lettres sources.</p></li>
        > <li><p>Si vous exportez tout le contenu de la boîte aux lettres correspondant à une plage de dates précise (mais sans spécifier aucun mot clé dans les critères de recherche), tous les éléments impossibles à rechercher dans cette plage de dates seront automatiquement inclus dans les résultats de la recherche. Par conséquent, n’activez pas la case à cocher <strong>Inclure les éléments qui ne peuvent pas être recherchés</strong>.</p></li></ul>

4.  Cliquez sur **Démarrer** pour exporter les résultats de recherche vers un fichier PST.
    
    Une fenêtre contenant des informations sur l’état du processus d’exportation s’affiche.

## Plus d’informations

  - Pour réduire la taille du fichier d’exportation PST, vous pouvez exporter uniquement les éléments impossibles à rechercher. Pour ce faire, créez ou modifiez une recherche, indiquez une date de début à venir, puis supprimez tous les mots-clés de la zone **Mots-clés**. Aucun résultat de recherche ne sera renvoyé. Lorsque vous copiez ou exportez les résultats de la recherche et que la case à cocher **Inclure les éléments qui ne peuvent pas être recherchés** est sélectionnée, seuls les éléments impossibles à rechercher seront copiés dans la boîte aux lettres de découverte ou exportés vers un fichier PST.

  - Si vous activez la déduplication, tous les résultats de la recherche sont exportés dans un seul fichier PST. Si vous n’activez pas la déduplication, un fichier PST distinct est exporté pour chaque boîte aux lettres incluse dans la recherche. Et, comme indiqué précédemment, les éléments impossibles à rechercher sont exportés dans un fichier PST distinct.

  - Outre les fichiers PST contenant les résultats de la recherche, deux autres fichiers sont également exportés :
    
      - Un fichier de configuration (format de fichier .txt) qui contient des informations sur la demande d’exportation PST, telles que le nom de la recherche de découverte électronique qui a été exportée, la date et l’heure de l’exportation, si la déduplication et les éléments impossibles à rechercher ont été activés, la requête de recherche et les boîtes aux lettres sources qui ont fait l’objet de la recherche.
    
      - Un journal de résultats de recherche (format de fichier .csv) qui contient une entrée pour chaque message renvoyé dans les résultats de la recherche. Chaque entrée identifie la boîte aux lettres source où se trouve le message. Si vous avez activé la déduplication, cela permet d’identifier toutes les boîtes aux lettres contenant un message en double.

  - Le nom de la recherche constitue la première partie du nom de fichier pour chaque fichier exporté. En outre, la date et l’heure de la demande d’exportation sont ajoutées au nom de chaque fichier PST et du journal de résultats.

  - Pour plus d’informations sur la déduplication et les éléments impossibles à rechercher, voir :
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Éléments impossibles à rechercher dans la découverte électronique Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - Pour exporter les résultats de recherche de découverte électronique à partir du centre de découverte électronique vers SharePoint ou SharePoint Online, consultez la rubrique [Exporter du contenu eDiscovery et créer des rapports](https://go.microsoft.com/fwlink/p/?linkid=324757).

## Résolution des problèmes


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Symptôme</th>
<th>Cause possible</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impossible d’exporter vers un fichier PST.</p></td>
<td><ul>
<li><p>Aucune boîte aux lettres active n’est liée au compte. Pour exporter le fichier PST, vous devez disposer d’un compte actif.</p></li>
<li><p>Votre version d’Internet Explorer est obsolète. Essayez de mettre à jour Internet Explorer vers la version 10 ou ultérieure. Sinon, essayez un autre navigateur.</p></li>
<li><p>Les critères de recherche saisis dans la requête <strong>Filtre basé sur des critères</strong> sont incorrects. Par exemple, un nom d’utilisateur est saisi au lieu d’une adresse de messagerie. Pour plus d’informations sur le filtrage en fonction des critères, voir <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modifier une recherche de découverte électronique inaltérable</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Impossible d’exporter les résultats de recherche sur un ordinateur spécifique. L’exportation fonctionne comme prévu sur un autre ordinateur.</p></td>
<td><p>Des informations d’identification Windows incorrectes ont été enregistrées dans le <strong>Gestionnaire d’informations d’identification</strong>. Supprimez vos informations d’identification et reconnectez-vous.</p></td>
</tr>
<tr class="odd">
<td><p>L’outil d’exportation de fichier PST de découverte électronique ne se lance pas.</p></td>
<td><p>Les paramètres de la zone Intranet local ne sont pas correctement configurés dans Internet Explorer. Vérifiez que les domaines *.outlook.com, *.office365.com, *.sharepoint.com et *.onmicrosoft.com sont ajoutés à la zone Intranet local des sites de confiance.</p>
<p>Pour ajouter ces sites à la zone de confiance dans Internet Explorer, voir <a href="https://windows.microsoft.com/fr-fr/windows/security-zones-adding-removing-websites#1tc=windows-7">Zones de sécurité : ajout ou suppression de sites web</a>.</p></td>
</tr>
</tbody>
</table>

