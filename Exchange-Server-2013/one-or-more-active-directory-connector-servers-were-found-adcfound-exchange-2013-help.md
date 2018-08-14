---
title: 'Un ou plusieurs serveurs du Connecteur AD ont été détectés'
TOCTitle: Un ou plusieurs serveurs du Connecteur Active Directory ont été détectés_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50478968
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Un ou plusieurs serveurs du Connecteur Active Directory ont été détectés\_ADCFound

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-15_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

L’installation de Microsoft Exchange Server 2007 et d’Exchange Server 2010 ne peut pas continuer car un ou plusieurs Connecteurs Active Directory ont été détectés dans l’environnement Microsoft Exchange actuel.

L’ADC réplique les objets d’Exchange Server version 5.5 dans le service d’annuaire Active Directory dans un environnement Microsoft Exchange en mode mixte et n’est pas pris en charge par Exchange 2007 ni par Exchange 2010.

L’installation d’Exchange 2007 ou d’Exchange 2010 exige la suppression de tous les composants ADC.

Pour résoudre ce problème, supprimez tous les composants ADC et recommencez l’installation d’Exchange 2007 ou d’Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Pour supprimer les composants Active Directory Connector</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Pour désactiver le service ADC sur le serveur exécutant ADC, cliquez avec le bouton droit sur <strong>Poste de travail</strong> sur le Bureau, puis cliquez sur <strong>Gérer</strong>.</p></li>
<li><p>Développez le nœud <strong>Services et applications</strong>, puis cliquez sur le nœud <strong>Services</strong>.</p></li>
<li><p>Dans le volet droit, cliquez avec le bouton droit sur <strong>Microsoft Active Directory Connector</strong> et cliquez sur <strong>Propriétés</strong>.</p></li>
<li><p>Modifiez <strong>Type de démarrage</strong> en <strong>Désactivé</strong>. Au prochain démarrage de l’ordinateur, le service ADC ne sera pas lancé.</p></li>
<li><p>Cliquez sur <strong>Appliquer</strong>, puis cliquez sur <strong>OK</strong>.</p></li>
<li><p>L’Assistant Installation d’Active Directory fourni sur le CD-ROM Microsoft Exchange 2000 Server ou Microsoft Exchange Server 2003 permet de désinstaller le service ADC. Ouvrez le dossier \ADC\I386 et double-cliquez sur le programme Setup.exe. Suivez les invites pour <strong>Supprimer tous</strong> les composants du service ADC.</p>

> [!NOTE]
> Vous devez effectuez l’étape 6 et <strong>Supprimer tous</strong> les composants ADC pour résoudre ce problème. Il ne suffit pas de désactiver le service ADC.

</li>
</ol></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur le connecteur ADC, voir les articles suivants de la Base de connaissances Microsoft :

  - 325300, « Webdiffusion du support : Introduction au connecteur Active Directory » ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325300)).

  - 325221, « présentation technique en ligne : Microsoft Advanced connecteur Active Directory » ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325221)).

  - 312632, « Comment faire installer et configurer le connecteur Active Directory dans Exchange 2000 Server » ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052&kbid=312632)).

