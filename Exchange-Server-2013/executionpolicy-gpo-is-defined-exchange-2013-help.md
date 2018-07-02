---
title: 'L’objet de stratégie de groupe ExecutionPolicy est défini: Exchange 2013 Help'
TOCTitle: L’objet de stratégie de groupe ExecutionPolicy est défini
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61204570
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# L’objet de stratégie de groupe ExecutionPolicy est défini

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-15_

Le programme d’installation de Microsoft Exchange Server 2013 ne peut pas continuer car l’objet de stratégie de groupe **ExecutionPolicy** définissant l’une ou les deux stratégies suivantes a été détecté :

  - **MachinePolicy**

  - **UserPolicy**

La façon dont les stratégies ont été définies n’est pas importante. Seul le fait qu’elles aient été définies importe.

Lors de l’exécution du programme d’installation Exchange 2013, Exchange arrête et désactive le service Windows Management Instrumentation (WMI). Lorsque l’une de ces stratégies est définie, le service WMI doit être activé pour exécuter un script Windows PowerShell. Si les stratégies sont définies et que le service WMI est arrêté, le programme d’installation échouera et l’état du serveur restera incohérent.

Pour permettre la poursuite de l’installation, vous devez supprimer temporairement toute définition des paramètres **MachinePolicy** ou **UserPolicy** dans l’objet de stratégie de groupe **ExecutionPolicy**.

Pour plus d’informations sur la suppression des définitions de **MachinePolicy** ou **UserPolicy** dans l’objet de stratégie de groupe **ExecutionPolicy**, voir l’[article KB 981474 de la base de connaissances](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Même si cet article de la base de connaissance a été rédigé pour Exchange 2010, il s’applique également aux mises à jour cumulatives et aux Service Packs Exchange 2013.</td>
</tr>
</tbody>
</table>


Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

