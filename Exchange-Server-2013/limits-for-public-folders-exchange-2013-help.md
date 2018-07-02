---
title: 'Limites pour les dossiers publics: Exchange 2013 Help'
TOCTitle: Limites pour les dossiers publics
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170904
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limites pour les dossiers publics

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans Exchange Server 2013, nous avons déplacé les dossiers publics d’une architecture traditionnelle de base de données vers une architecture de boîtes aux lettres. Ainsi, les dossiers publics peuvent bénéficier, entre autres, de la résilience d’un groupe de disponibilité de base de données (DAG) et d’autres améliorations relatives aux boîtes aux lettres apportées au fil des ans. Toutefois, de nouvelles limites et de nouveaux problèmes de performances doivent être pris en compte. Dans ce document, nous fournissons quelques conseils de haut niveau pour les options de configuration dont vous disposez et qui pourraient avoir une incidence sur la connectivité et les performances des dossiers publics.

## Limites

Le tableau ci-dessous répertorie les limites des dossiers publics dans Exchange Server 2013 local. À moins qu’il soit spécifiquement indiqué que les limites sont recommandées, les valeurs répertoriées dans ce tableau sont les limites prises en charge pour les dossiers publics.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous recherchez les limites d’Exchange Online pour Office 365 ? Consultez la rubrique <a href="https://go.microsoft.com/fwlink/?linkid=391188">Limites d’Exchange Online</a>.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément</th>
<th>Limites</th>
<th>Commentaires</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nombre total de boîtes aux lettres de dossiers publics</p></td>
<td><p>100</p></td>
<td><p>Bien qu’il vous soit possible de créer plus de 100 boîtes aux lettres de dossiers publics, cette fonctionnalité n’est pas prise en charge. <a href="create-a-public-folder-mailbox-exchange-2013-help.md">Création d’une boîte aux lettres de dossiers publics</a></p></td>
</tr>
<tr class="even">
<td><p>Nombre total de dossiers publics dans la hiérarchie</p></td>
<td><p>1 000 000</p></td>
<td><p>Bien qu’il vous soit possible de créer plus de 1 000 000 dossiers publics, cette fonctionnalité n’est pas prise en charge. Pour tout déploiement de 100 000 dossiers publics ou plus, nous vous recommandons de consulter la rubrique <a href="considerations-when-deploying-public-folders-exchange-2013-help.md">Considérations relatives au déploiement de dossiers publics</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Sous-dossiers sous le dossier parent</p></td>
<td><p>10,000</p></td>
<td><p>Bien qu’il vous soit possible de créer plus de 1 000 sous-dossiers dans un dossier parent, nous vous déconseillons de le faire.</p>
<p>Paramètre <em>FolderHierarchyChildrenCountReceiveQuota</em> avec la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Profondeur du dossier</p></td>
<td><p>300</p></td>
<td><p>La profondeur du dossier correspond au nombre de niveaux des dossiers imbriqués qui peuvent exister dans une branche d’une arborescence de dossiers publics. Paramètre <em>FolderHierarchyDepthRecieveQuota</em> avec la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Nombre maximal de messages par dossier public</p></td>
<td><p>1 million</p></td>
<td><p>Paramètre <em>MailboxMessagesPerFolderCountRecieveQuota</em> avec la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Taille maximale de chaque dossier public</p></td>
<td><p>10 Go</p></td>
<td><p>Cette limite n’inclut pas les sous-dossiers sous un dossier unique.</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configuration de quotas de stockage pour une boîte aux lettres</a></p></td>
</tr>
<tr class="odd">
<td><p>Taille de la boîte aux lettres de dossier public</p></td>
<td><p>100 Go</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configuration de quotas de stockage pour une boîte aux lettres</a></p></td>
</tr>
<tr class="even">
<td><p>Nombre de connexions utilisateurs par boîte aux lettres de dossiers publics</p></td>
<td><p>2 000 connexions utilisateurs simultanées</p></td>
<td><p>Nous vous recommandons de configurer votre hiérarchie afin que le nombre d’utilisateurs par boîte aux lettres de dossiers publics n’excède pas 2 000. Par exemple, si le nombre d’utilisateurs est de 20 000, le nombre de boîtes aux lettres de dossiers publics doit être de 10.</p></td>
</tr>
<tr class="odd">
<td><p>Rétention des éléments déplacés</p></td>
<td><p>Recommandation de 14 jours</p></td>
<td><p>Utilisez le paramètre <em>DefaultPublicFolderMovedItemRetention</em> avec la cmdlet <strong>Set-OrganizationConfig</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Limite d’âge</p></td>
<td><p>Nous vous recommandons de définir ce paramètre sur la valeur par défaut que vous utilisez pour les boîtes aux lettres ordinaires.</p></td>
<td><p>Ces paramètres peuvent être définis aux niveaux suivants :</p>
<ul>
<li><p><strong>Niveau organisationnel :</strong> Paramètre <em>DefaultPublicFolderAgeLimit</em> avec la cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Niveau de boîte aux lettres :</strong> Paramètre <em>AgeLimit</em> avec la cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Niveau de dossier :</strong> Paramètre <em>AgeLimit</em> avec la cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Rétention des éléments supprimés</p></td>
<td><p>Nous vous recommandons de définir ce paramètre sur la valeur par défaut que vous utilisez pour les boîtes aux lettres ordinaires.</p></td>
<td><p>Ces paramètres peuvent être définis aux niveaux suivants :</p>
<ul>
<li><p><strong>Niveau organisationnel :Paramètre</strong> <em>DefaultPublicFolderMovedItemRetention</em> avec la cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Niveau de boîte aux lettres :</strong> Paramètre <em>RetainDeletedItemsFor</em> avec la cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Niveau de dossier :</strong> Paramètre <em>RetainDeleteItemsFor</em> avec la cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nombre maximal de dossiers publics pouvant être migrés vers Exchange 2013</p></td>
<td><p>500,000</p></td>
<td><p>Il s’agit du nombre maximal de dossiers publics que vous pouvez déplacer vers Exchange 2013 à partir d’une version héritée d’Exchange en une seule migration. Pour plus d’informations sur la migration des dossiers publics, voir <a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">Utiliser la migration par lots pour migrer les dossiers publics vers Exchange 2013 à partir de versions antérieures</a></p></td>
</tr>
</tbody>
</table>

