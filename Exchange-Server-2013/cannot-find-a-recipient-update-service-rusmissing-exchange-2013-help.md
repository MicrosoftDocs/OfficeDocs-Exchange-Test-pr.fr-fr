---
title: 'Impossible de trouver un service de mise à jour de destinataire_RUSMissing: Exchange 2013 Help'
TOCTitle: Impossible de trouver un service de mise à jour de destinataire_RUSMissing
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50478720
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impossible de trouver un service de mise à jour de destinataire\_RUSMissing

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-15_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft ® Exchange Server 2007 ou Exchange Server 2010 ne peut pas poursuivre son exécution car le service de mise à jour de destinataire responsable d’un domaine dans l’organisation Exchange existante est introuvable.

Le programme d’installation de Microsoft Exchange nécessite que chaque domaine de l’organisation Exchange existante dispose d’une instance du service de mise à jour de destinataire.

Si une instance du service de mise à jour de destinataire est manquante pour un domaine, de nouveaux objets utilisateur créés dans le domaine ne reçoivent pas d’adresse de courrier électronique.

Pour résoudre ce problème, vérifiez qu’une instance du service de mise à jour de destinataire existe pour chaque domaine et créez une instance du service de mise à jour de destinataire pour les domaines qui n’en ont pas, puis recommencez l’installation de Microsoft Exchange.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Pour créer une instance du service de mise à jour de destinataire pour un domaine</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Ouvrez le Gestionnaire système Exchange.</p></li>
<li><p>Développez <strong>Destinataires</strong>.</p></li>
<li><p>Cliquez avec le bouton droit sur le nœud <strong>Services de mise à jour de destinataire</strong>, cliquez sur <strong>Nouveau</strong>, puis sur <strong>Service de mise à jour de destinataire</strong>.</p></li>
<li><p>Dans la fenêtre Nouvel objet, cliquez sur <strong>Parcourir</strong> pour rechercher le nom du domaine.</p></li>
<li><p>Sélectionnez le nom du domaine et cliquez sur <strong>OK</strong>.</p></li>
<li><p>Dans la fenêtre Nouvel objet, cliquez sur <strong>Suivant</strong>, puis sur <strong>Terminer</strong>.</p></li>
</ol></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur le service de mise à jour de destinataire, voir les articles suivants de la Base de connaissances Microsoft :

  - Comment le service de mise à jour de destinataire applique les stratégies de destinataire ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=328738)).

  - Comment le service de mise à jour de destinataire renseigne les listes d’adresses ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253828)).

  - Comment vérifier la progression du service de mise à jour de destinataire Exchange ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=246127)).

  - Tâches effectuées par le service de mise à jour de destinataire Exchange ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253770)).

