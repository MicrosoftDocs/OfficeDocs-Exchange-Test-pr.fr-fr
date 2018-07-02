---
title: 'Déplacements de boîtes aux lettres dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Déplacements de boîtes aux lettres dans Exchange 2013
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50478810
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Déplacements de boîtes aux lettres dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Lorsque vous déplacez une boîte aux lettres, vous la déplacez depuis une *base de données de boîtes aux lettres source* vers une *base de données de boîtes aux lettres cible*. La base de données de boîtes aux lettres cible peut se trouver sur le même serveur, sur un serveur différent, dans un domaine ou un site Active Directory différents, ou encore dans une autre forêt.

## Motifs de déplacement de boîtes aux lettres

Le déplacement de boîtes aux lettres peut s'avérer nécessaire dans les scénarios suivants :

  - **Mise à niveau**   Lorsque vous effectuez une mise à niveau à partir d'une organisation Microsoft Exchange Server 2007 ou Exchange Server 2010 existante vers Exchange Server 2013, vous déplacez les boîtes aux lettres des serveurs Exchange existants vers un serveur de boîtes aux lettres Exchange 2013.

  - **Réalignement**   Vous pouvez déplacer les boîtes aux lettres à des fins de réalignement. Par exemple, il se peut que vous vouliez déplacer une boîte aux lettres d'une base de données à une autre dont la limite de taille de boîte aux lettres est supérieure.

  - **Enquête sur un problème**   Si vous avez besoin d'enquêter sur un problème concernant une boîte aux lettres, vous pouvez la déplacer vers un autre serveur. Par exemple, vous pouvez déplacer toutes les boîtes aux lettres dont l'activité est importante vers un autre serveur.

  - **Boîtes aux lettres endommagées**   Si vous trouvez des boîtes aux lettres endommagées, vous pouvez déplacer ces boîtes aux lettres vers un autre serveur ou une autre base de données. Les messages endommagés ne sont pas déplacés.

  - **Modifications de l'emplacement physique**   Vous pouvez déplacer des boîtes aux lettres vers un serveur situé sur un site Active Directory différent. Par exemple, si un utilisateur se déplace vers un emplacement physique différent, vous pouvez déplacer sa boîte aux lettres vers un serveur situé sur un site plus proche du nouvel emplacement.

  - **Séparation des rôles administratifs**   Vous souhaiterez peut-être séparer l'administration d'Exchange de l'administration des comptes du système d'exploitation Windows. Pour ce faire, vous pouvez déplacer les boîtes aux lettres d'une forêt vers un scénario de forêt de ressources. Dans ce scénario, les boîtes aux lettres Exchange résident dans une forêt et les comptes d'utilisateurs Windows associés dans une autre.

  - **Externalisation de l'administration de la messagerie électronique**   Vous souhaitez peut-être externaliser l'administration de la messagerie électronique tout en conservant l'administration des comptes d'utilisateurs Windows. Pour ce faire, vous pouvez déplacer les boîtes aux lettres d'une forêt vers un scénario de forêt de ressources.

  - **Intégration de l'administration de la messagerie électronique et des comptes d'utilisateurs**   Vous souhaitez peut-être passer d'une administration de messagerie électronique externalisée ou indépendante à un modèle dans lequel la messagerie électronique et les comptes d'utilisateurs peuvent être gérés depuis la même forêt. Pour ce faire, vous pouvez déplacer des boîtes aux lettres d'un scénario de forêt de ressources vers une forêt unique. Dans ce scénario, les boîtes aux lettres Exchange et les comptes d'utilisateurs Windows résident dans la même forêt.

## Exchange 2013 évolue

Microsoft Exchange Server 2013 introduit le concept de *déplacements par lot* et de *points de terminaison de migration*. Les points de terminaison de migration sont des objets de gestion qui décrivent le serveur distant et les connexions qui peuvent être associés à un ou plusieurs lots. La nouvelle architecture de déplacement par lots, quant à elle, améliore les déplacements du service de réplication de boîte aux lettres à l'aide de meilleures capacités de gestion. L'architecture de déplacement par lots d'Exchange 2013 présente les fonctionnalités suivantes :

  - Possibilité de déplacer plusieurs boîtes aux lettres par grandes quantités.

  - Notification par courrier électronique lors du déplacement avec rapports.

  - Nouvelle tentative automatique et priorisation automatique des déplacements.

  - Les boîtes aux lettres d'archivage principale et personnelle peuvent être déplacées ensemble ou séparément.

  - Option de finalisation de demande de déplacement manuel, ce qui vous permet de revoir votre déplacement avant de l'exécuter.

  - Synchronisations incrémentielles périodiques pour mettre à jour les modifications de migration.

Dans Exchange 2013, vous devez déplacer les boîtes aux lettres entre Exchange 2007 et Exchange 2010 et Exchange 2013 à partir du Centre d'administration Exchange 2013 (CAE) et de l'environnement de ligne de commande Exchange Management Shell.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange 2013, vous pouvez toujours effectuer des déplacements de boîtes aux lettres uniques tout comme dans Exchange Server 2010, en utilisant soit le Centre d'administration Exchange, soit les cmdlets de demande de déplacement ou de lot de migration.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas déplacer de boîtes aux lettres locales d’Exchange Server 2003 vers Exchange 2013.</td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la gestion des déplacements nouveaux et existants, consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).

## Points de terminaison de migration

Les points de terminaison de migration capturent les informations de serveur distant et conservent les informations d'identification requises pour la migration des données et des paramètres de limitation de source. Vous pouvez utiliser les points de terminaison de migration pour configurer des paramètres relatifs aux déplacements à distance et inter-forêts. Les déplacements locaux ne nécessitent pas l'utilisation d'un point de terminaison. (Les déplacements locaux sont des déplacements de boîtes aux lettres entre deux bases de données Exchange locales différentes.)

La liste suivante affiche les types de déplacements prenant en charge les points de terminaison de migration :

  - **Déplacement inter-forêts**   Déplacer des boîtes aux lettres entre deux forêts sur site Exchange différentes. Les déplacements inter-forêts nécessitent l'utilisation d'un point de terminaison Exchange RemoteMove.

  - **Remote move**   Dans un déploiement hybride, un déplacement distant implique des migrations *d'embarquement* ou *de débarquement*. Les déplacements distants nécessitent l'utilisation d'un point de terminaison RemoteMove. L'embarquement déplace des boîtes aux lettres d'une organisation Exchange locale vers Exchange Online dans Microsoft Office 365 et utilise un point de terminaison RemoteMove comme point de terminaison source du lot de migration. Le débarquement déplace des boîtes aux lettres Exchange Online dans Office 365 vers une organisation Exchange locale et utilise un point de terminaison Exchange RemoteMove comme point de terminaison cible du lot de migration.

Le tableau suivant présente les types et les valeurs de point de terminaison de migration que vous pouvez gérer dans Exchange 2013.

### Valeurs des types de point de terminaison de migration

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Databases</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur les points de terminaison de migration, consultez l'interface utilisateur **Migration** du CAE et [New-MigrationEndpoint](https://technet.microsoft.com/fr-fr/library/jj218611\(v=exchg.150\)).

Pour plus d'informations sur la gestion des déplacements nouveaux et existants, consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).

