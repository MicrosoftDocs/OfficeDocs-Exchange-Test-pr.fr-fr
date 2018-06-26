---
title: 'Créer ou supprimer une conservation inaltérable: Exchange 2013 Help'
TOCTitle: Créer ou supprimer une conservation inaltérable
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 50478883
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer ou supprimer une conservation inaltérable

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-01-18_

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous avons différé la date d’échéance du 1er juillet 2017 pour créer des conservations inaltérables dans Exchange Online (dans les plans autonomes Office 365 et Exchange Online). Mais plus tard cette année ou au début de l’année prochaine, vous ne pourrez pas créer des conservations inaltérables dans Exchange Online. Au lieu d’utiliser des conservations inaltérables, vous pouvez avoir recours à des <a href="https://go.microsoft.com/fwlink/?linkid=780738">cas de découverte électronique</a> ou des <a href="https://go.microsoft.com/fwlink/?linkid=827811">stratégies de rétention</a> dans le centre de sécurité et conformité Office 365. Lorsque nous aurons désactivé les nouvelles conservations inaltérables, vous pourrez toujours modifier les conservations inaltérables existantes. La création de conservations inaltérables sera toujours prise en charge dans les déploiements hybrides Exchange Server 2013 et Exchange . Vous serez également toujours en mesure de mettre des boîtes aux lettres en conservation pour litige.</td>
</tr>
</tbody>
</table>


Une conservation inaltérable conserve tout le contenu d’une boîte aux lettres, y compris les éléments supprimés et les versions originales des éléments modifiés. Tous ces éléments de boîte aux lettres sont retournés dans une recherche de [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md). Lorsque vous placez une conservation inaltérable sur la boîte aux lettres d’un utilisateur, le contenu de la boîte aux lettres d’archivage correspondante (si elle est activée) est également placé en conservation et renvoyé lors d’une recherche de découverte électronique.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Archive permanente » de la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour placer une boîte aux lettres Exchange Online en conservation inaltérable, elle doit disposer d’une licence Exchange Online (Plan 2). Si une boîte aux lettres dispose d’une licence Exchange Online (Plan 1), vous devez lui attribuer une licence Archivage Exchange Online distincte pour la placer en conservation inaltérable.

  - Selon votre latence de réplication et votre topologie Active Directory, la prise d'effet d'une archive permanente peut prendre jusqu'à une heure.

  - Comme expliqué précédemment, lorsque vous placez une conservation inaltérable sur la boîte aux lettres d’un utilisateur, le contenu de la boîte aux lettres d’archivage de l’utilisateur est également placé en conservation inaltérable. Si vous placez une conservation inaltérable sur une boîte aux lettres principale locale dans un déploiement hybride Exchange, la boîte aux lettres d’archivage en nuage (si activée) est également placée en conservation inaltérable.

  - Si un utilisateur est placé dans plusieurs conservations inaltérables, les requêtes de recherche provenant de toute conservation fondée sur une requête sont combinées (avec des opérateurs **OR**). Dans ce cas, le nombre maximal de mots clés dans toutes les conservations fondées sur une requête placés dans une boîte aux lettres s’élève à 500. S’il existe plus de 500 mots-clés, tout le contenu de la boîte aux lettres est placé en conservation (et pas seulement le contenu correspondant aux critères de recherche). Tout le contenu est placé en conservation jusqu’à ce que le nombre total de mots-clés soit réduit à 500 ou moins.

  - Dans Exchange Online, le quota du dossier Éléments récupérables est automatiquement augmenté jusqu’à 100 Go lorsque vous placez une conservation inaltérable sur une boîte aux lettres. La taille par défaut du dossier Éléments récupérables est de 30 Go.

  - Dans Exchange Online, vous pouvez placer une conservation inaltérable sur des groupes Office 365. Lorsque vous placez un groupe Office 365 en conservation, la boîte aux lettres de groupe est placée en conservation, mais pas les boîtes aux lettres des membres du groupe. Pour plus d’informations sur les groupes Office 365, voir [En savoir plus sur les groupes Office 365](https://go.microsoft.com/fwlink/p/?linkid=724066).

## Créer une archive permanente

**Utiliser le Centre d'administration Exchange (CAE) pour créer une archive permanente**

1.  Accédez à **Gestion de la conformité**\>**Découverte électronique et archives locales**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **Découverte électronique et archive permanente**, dans la page **Nom et description**, tapez un nom pour la recherche et une description facultative, puis cliquez sur **Suivant**.

4.  Sur la page **Boîtes aux lettres et Dossiers publics**, choisissez les emplacements de contenu que vous souhaitez placer en conservation, puis cliquez sur **Suivant**.
    
    ![Choisissez les emplacements de contenu à mettre sous conservation](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "Choisissez les emplacements de contenu à mettre sous conservation")  
    
    1.  **Rechercher dans toutes les boîtes aux lettres** Vous ne pouvez pas sélectionner cette option pour créer une conservation inaltérable. Vous pouvez sélectionner cette option pour les recherches de découverte électronique inaltérable, mais pour créer une conservation inaltérable, vous devez sélectionner les boîtes aux lettres spécifiques que vous souhaitez placer en conservation.
    
    2.  **Ne rechercher dans aucune boîte aux lettres** Sélectionnez cette option lorsque vous créez une conservation inaltérable exclusivement pour des dossiers publics.
    
    3.  **Spécifier les boîtes aux lettres à rechercher** Sélectionnez cette option, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") afin de sélectionner les boîtes aux lettres ou les groupes de distribution que vous souhaitez placer en conservation. Dans Exchange Online, vous pouvez également sélectionner des groupes Office 365 à placer en conservation.
    
    4.  **Rechercher dans tous les dossiers publics**   Dans Exchange Online, vous pouvez cocher cette case pour placer tous les dossiers publics de votre organisation en conservation. Comme expliqué précédemment, pour créer une conservation inaltérable uniquement pour les dossiers publics, sélectionnez bien l’option **Ne rechercher dans aucune boîte aux lettres**.

5.  dans la page **Requête de recherche**, complétez les champs suivants, puis cliquez sur **Suivant** :
    
      - **Inclure tout le contenu des boîtes aux lettres utilisateur**   Cliquez sur ce bouton pour archiver tout le contenu des boîtes aux lettres sélectionnées.
    
      - **Filtrer en fonction des critères**   Cliquez sur ce bouton pour spécifier les critères de recherche, y compris les mots clés, les dates de début et de fin, les adresses des expéditeurs et des destinataires et les types de messages. Lorsque vous créez une conservation sur la base d’une requête, seuls les éléments correspondant aux critères de recherche sont conservés.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Lorsque vous placez des dossiers publics en conservation inaltérable, les messages électroniques liés au processus de synchronisation de hiérarchie de dossiers publics sont également conservés. Cela peut entraîner la conservation de milliers de messages électroniques associés à la synchronisation de la hiérarchie. Ces messages peuvent remplir le quota de stockage du dossier Éléments récupérables sur les boîtes aux lettres de dossiers publics. Pour éviter cela, vous pouvez créer une conservation inaltérable fondée sur une requête et ajouter la paire <code>property:value</code> suivante à la requête de recherche :<br />
        <code>NOT(subject:HierarchySync*)</code><br />
        Ainsi, les messages (liés à la synchronisation de la hiérarchie de dossier public) dont la ligne d’objet contient le terme « HierarchySync » ne seront pas placés en conservation.</td>
        </tr>
        </tbody>
        </table>


6.  Dans la page **Paramètres de l'archive permanente**, cochez la case **Mettre en archive permanente le contenu correspondant à la requête de recherche des boîtes aux lettres sélectionnées**, puis activez l'une des options suivantes :
    
      - **Conserver indéfiniment**   Cliquez sur ce bouton pour archiver indéfiniment les éléments renvoyés par la recherche. Les éléments en attente seront conservés jusqu'à ce que vous supprimiez la boîte aux lettres de la recherche ou que vous supprimiez la recherche.
    
      - **Spécifier le nombre de jours pendant lequel conserver les éléments en fonction de leur date de réception**   Cliquez sur ce bouton pour archiver les éléments pendant une période donnée. Par exemple, vous pouvez utiliser cette option si votre organisation exige que tous les messages soient conservés pendant au moins sept ans. Vous pouvez utiliser une archive locale *basée sur le temps* parallèlement à une stratégie de rétention pour garantir que les éléments seront supprimés dans sept ans. Pour en savoir plus sur les stratégies de rétention, consultez la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

**Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une archive permanente**

Cet exemple crée l'archive permanente Hold-CaseId012 et ajoute la boîte aux lettres joe@contoso.com à l'archive.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous ne précisez pas de paramètres de recherche supplémentaires pour une conservation inaltérable, tous les éléments des boîtes aux lettres source spécifiées sont placés en conservation. Si vous ne spécifiez pas le paramètre <em>ItemHoldPeriod</em>, les éléments sont placés en conservation indéfiniment ou jusqu’à ce que la boîte aux lettres ne soit plus conservée ou que la conservation soit supprimée.</td>
</tr>
</tbody>
</table>


    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd298064\(v=exchg.150\)).

**Comment savoir si cela a fonctionné ?**

Pour vérifier que vous avez bien créé l'archive permanente; procédez de l'une des façons suivantes :

  - Utilisez le CAE pour vérifier que l'archive permanente est répertoriée dans l'affichage Liste de l'onglet **Découverte électronique et archive permanente**.

  - Utilisez la cmdlet **Get-MailboxSearch** pour récupérer la recherche de boîte aux lettres et vérifier les paramètres de recherche. Pour voir un exemple de récupération d'une recherche de boîte aux lettres, consultez les exemples de la rubrique [Get-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd351021\(v=exchg.150\)).

Retour au début

## Supprimer une archive permanente

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange 2013, les recherches de boîtes aux lettres peuvent être utilisées pour une archive permanente et pour la découverte électronique locale. Vous ne pouvez pas supprimer une recherche de boîte aux lettres utilisée pour une conservation inaltérable. Vous devez d'abord désactiver l'archive permanente en décochant la case <strong>Mettre en archive le contenu correspondant à la requête de recherche des boîtes aux lettres sélectionnées</strong> dans la page <strong>Paramètres de l'archive permanente</strong> ou en définissant le paramètre <em>InPlaceHoldEnabled</em> sur <code>$false</code> dans l'environnement de ligne de commande Exchange Management Shell. Vous pouvez également supprimer une boîte aux lettres en utilisant le paramètre <em>SourceMailboxes</em> spécifié dans la recherche.</td>
</tr>
</tbody>
</table>


**Utiliser le CAE pour supprimer une archive permanente**

1.  Accédez à **Gestion de la conformité**\>**Découverte électronique et archivage permanent**.

2.  Dans l'affichage Liste, sélectionnez l'archive permanente à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans les propriétés de **Découverte électronique et archive permanente**, dans la page **Archive permanente**, décochez la case **Mettre en archive le contenu correspondant à la requête de recherche des boîtes aux lettres sélectionnées**, puis cliquez sur **Enregistrer**.

4.  Sélectionnez à nouveau l'archive permanente dans la liste, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

5.  Dans l'avertissement, cliquez sur **Oui** pour supprimer la recherche.

**Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une archive permanente**

Cet exemple désactive d'abord l'archive permanente Hold-CaseId012, puis supprime la recherche de boîte aux lettres.

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd335145\(v=exchg.150\)).

**Comment savoir si cela a fonctionné ?**

Pour vérifier que vous avez bien supprimé une archive permanente, procédez de l'une des façons suivantes :

  - Utilisez le CAE pour vérifier que la conservation inaltérable n’est plus répertoriée dans l’affichage Liste de l’onglet **Découverte électronique et blocage sur place**.

  - Utilisez la cmdlet **Get-MailboxSearch** pour récupérer toutes les recherches de boîtes aux lettres et vérifier que la recherche que vous avez supprimée n'est plus répertoriée. Pour voir un exemple de récupération d'une recherche de boîte aux lettres, consultez les exemples de la rubrique [Get-MailboxSearch](https://technet.microsoft.com/fr-fr/library/dd351021\(v=exchg.150\)).

Retour au début

