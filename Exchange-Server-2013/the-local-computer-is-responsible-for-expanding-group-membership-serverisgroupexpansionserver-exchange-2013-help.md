---
title: 'L’ordinateur local est responsable de l’expansion de l’appartenance à un groupe_ServerIsGroupExpansionServer: Exchange 2013 Help'
TOCTitle: L’ordinateur local est responsable de l’expansion de l’appartenance à un groupe_ServerIsGroupExpansionServer
ms:assetid: 52872561-60e6-4f3d-bbc6-6de0edf74b09
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.serverisgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50478191
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# L’ordinateur local est responsable de l’expansion de l’appartenance à un groupe\_ServerIsGroupExpansionServer

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car sa tentative de désinstallation d’un rôle Hub Transport responsable du développement de l’appartenance au groupe a échoué.

L’installation d’Exchange 2007 nécessite la suppression de l’extension de la liste de distribution du serveur Bridgehead actuel avant de pouvoir désinstaller le rôle Hub Transport.

L’extension des listes de distribution active l’identification des différents destinataires qui font partie de la liste de distribution à identifier ou l’identification des listes de distributions supplémentaires pour l’extension. Une liste de distribution étendue peut renvoyer le chemin d’accès de toute notification d’état de remise (DSN) demandée. Les notifications d’état de remise (DSN) avertissent l’administrateur Microsoft Exchange ou l’expéditeur d’un message électronique particulier. En outre, l’extension de la liste de distribution indique si les messages Absent du bureau ou les réponses générées automatiquement doivent être envoyées à l’expéditeur du message original.

Pour résoudre ce problème, déplacez l’extension du groupe de distribution sur un autre serveur et recommencez l’installation de Microsoft Exchange.

Pour modifier le serveur d’extension pour un groupe de distribution ou un groupe de distribution dynamique.

1.  Ouvrez Exchange Management Console.

2.  Dans l’arborescence de la console, développez **Configuration du destinataire**.

3.  Dans l’arborescence de la console, cliquez sur **Groupe de distribution**.

4.  Créez un filtre pour afficher tous les groupes de distribution et les groupes de distribution dynamique qui utilisent le serveur Bridgehead actuel comme serveur d’extension.
    
    1.  Dans le volet Action, cliquez sur **Créer un filtre**.
    
    2.  Dans la liste déroulante des propriétés, cliquez sur **Serveur d’expansion**.
    
    3.  Dans la liste déroulante des opérateurs, cliquez sur **Equals**.
    
    4.  Dans la zone de valeur, cliquez sur le bouton **Parcourir** pour sélectionner le serveur Bridgehead servant actuellement de serveur d’expansion.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L’étape suivante est facultative.</td>
</tr>
</tbody>
</table>


1.  Cliquez sur **Ajouter une expression** pour spécifier des critères de filtrage supplémentaires. Seuls les messages répondant aux critères de filtrage s’affichent.

2.  Cliquez sur **Appliquer le filtre**. Les résultats correspondant aux critères de filtrage s’affichent.

<!-- end list -->

1.  Dans le volet des résultats, cliquez sur le groupe de distribution pour lequel vous souhaitez modifier le serveur d’expansion, puis cliquez sur **Propriétés** dans le volet Actions.

2.  Sous **Propriétés**, cliquez sur l’onglet **Paramètres avancés**.

3.  Dans la liste déroulante du serveur d’expansion, sélectionnez un serveur spécifique dans la liste ou sélectionnez **Tout serveur de l’organisation**.

4.  Répétez les étapes 5 à 7 pour tous les groupes de distribution ou les groupes de distribution dynamique qui utilisent le serveur Bridgehead comme serveur d’expansion.

