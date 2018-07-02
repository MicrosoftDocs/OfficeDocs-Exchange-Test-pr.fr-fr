---
title: 'Liste de vérification pour la sécurité du pré-déploiement: Exchange 2013 Help'
TOCTitle: Liste de vérification pour la sécurité du pré-déploiement
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50477548
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de vérification pour la sécurité du pré-déploiement

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les fonctionnalités de Microsoft Exchange Server 2013 vous permettent d’améliorer la sécurité de votre environnement de messagerie. En règle générale, pour Exchange 2013, les conditions suivantes sont vraies :

  - Les comptes utilisés par Exchange 2013 disposent des droits minimaux requis pour exécuter les ensembles de tâches indiqués.

  - Par défaut, les services ne sont démarrés que lorsqu’ils sont requis.

  - Les droits liés à la liste de contrôle d’accès (ACL) pour les objets Exchange sont minimisés.

  - Les autorisations administratives sont définies en fonction de la portée de modification de l’objet qu’une modification donnée requiert.

  - Par défaut, tous les chemins de message interne par défaut sont chiffrés.

Cette rubrique dresse la liste des étapes qu’il est recommandé d’exécuter pour renforcer l’environnement de messagerie avant d’installer Microsoft Exchange. Nous vous recommandons de vous référer à cette liste de vérification chaque fois que vous installez un nouveau rôle serveur Exchange.

Avant l’installation d’Exchange 2013, effectuez les procédures suivantes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Procédure</th>
<th>Terminé ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exécutez <a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exécutez l’Outil de suppression des logiciels malveillants Microsoft Windows. L’Outil de suppression des logiciels malveillants est inclus dans Microsoft Update. Pour plus d’informations sur cet outil, consultez le site <a href="http://go.microsoft.com/fwlink/p/?linkid=73452">Outil de suppression des logiciels malveillants</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exécutez <a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

