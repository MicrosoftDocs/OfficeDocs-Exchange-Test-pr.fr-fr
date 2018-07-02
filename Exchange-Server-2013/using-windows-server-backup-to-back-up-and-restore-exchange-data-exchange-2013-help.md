---
title: 'Utilisation de la Sauvegarde Windows Server pour sauvegarder et restaurer des données Exchange: Exchange 2013 Help'
TOCTitle: Utilisation de la Sauvegarde Windows Server pour sauvegarder et restaurer des données Exchange
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50477513
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilisation de la Sauvegarde Windows Server pour sauvegarder et restaurer des données Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

[l’architecture de choix](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) pour Exchange Server 2013 de Microsoft s’appuie sur un concept appelé Exchange Protection des données natives. Exchange Protection de données native s’appuie sur les fonctionnalités de native Exchange pour protéger vos données de boîte aux lettres, sans l’utilisation de sauvegardes traditionnelles. Mais si vous souhaitez créer des sauvegardes, Exchange inclut un plug-in Windows Server sauvegarde (WSB) qui vous permet de créer des sauvegardes de basé sur Volume Shadow Copy Service VSS Exchange prenant en charge des données de Exchange. Pour effectuer des sauvegardes Exchange prenant en charge, vous devez disposer de la fonctionnalité sauvegarde Windows Server est installée.

Le plug-in, WSBExchange.exe, fonctionne comme un service appelé extension Microsoft Exchange Server pour la Sauvegarde Windows Server (le nom abrégé de ce service est WSBExchange). Ce service est automatiquement installé et configuré pour un démarrage manuel sur tous les serveurs de boîtes aux lettres. Ce plug-in permet à la fonctionnalité WSB de créer des sauvegardes VSS compatibles Exchange.

Avant d’utiliser la fonctionnalité WSB pour sauvegarder des données Exchange, il est recommandé de se familiariser avec les fonctionnalités et options du plug-in suivantes :

  - Les sauvegardes effectuées avec WSB se produisent au niveau du volume, et la seule façon d’effectuer une sauvegarde au niveau de l’application ou une restauration est de sélectionner un volume entier. Pour sauvegarder une base de données et son flux de journal, vous devez sauvegarder le volume entier qui les contient, et pas uniquement les dossiers individuels. Vous ne pouvez pas sauvegarder des données sans sauvegarder le volume entier qui les contient.

  - La sauvegarde doit être exécutée localement sur le serveur en cours de sauvegarde. Vous ne pouvez pas utiliser le plug-in pour effectuer des sauvegardes VSS à distance. La fonctionnalité WSB ou le plug-in ne sont pas administrés à distance. Vous pouvez toutefois utiliser les services Bureau à distance ou Terminal Server pour gérer les sauvegardes à distance.

  - La sauvegarde peut être créée sur un disque local ou sur un partage réseau distant.

  - Seules des sauvegardes complètes doivent être effectuées. La troncature des journaux se produit uniquement après l’exécution d’une sauvegarde complète VSS d’un volume ou de dossiers contenant une base de données Exchange.

  - Lors de la restauration des données, seules les données Exchange peuvent être restaurées. à leur emplacement d’origine ou à un autre emplacement. Si vous restaurez les données à leur emplacement d’origine, la fonctionnalité WSB et le plug-in traitent automatiquement le processus de récupération, y compris le démontage des bases de données existantes et la relecture des journaux dans la base de données récupérée.

  - Le processus de restauration ne prend pas directement en charge la base de données de récupération (RDB) Exchange. Si vous souhaitez utiliser une RDB, vous devez restaurer les données à un autre emplacement, puis copier ou déplacer manuellement les données restaurées à partir de cet emplacement vers la structure du dossier RDB.

  - Lors de la restauration des données Exchange, toutes les bases de données sauvegardées doivent être restaurées en même temps. Vous ne pouvez pas restaurer une seule base de données.

  - Les restaurations complètes sont prises en charge si vous utilisez WSB. Toutefois, pour les serveurs Exchange, il est recommandé de récupérer le serveur Exchange, puis de restaurer les données. Si vous utilisez une application de sauvegarde tierce (c’est-à-dire une application non Microsoft), votre fournisseur d’applications de sauvegarde peut vous assurer la prise en charge des restaurations complètes d’Exchange.

Le tableau suivant décrit la prise en charge des options de sauvegarde et de récupération disponibles pour Exchange 2013 avec WSB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si vous...</th>
<th>Procédez comme suit...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sauvegardez la totalité du serveur...</p></td>
<td><p>Une sauvegarde de copie VSS sera effectuée et les journaux de transactions pour les bases de données sur le serveur ne seront pas tronqués.</p></td>
</tr>
<tr class="even">
<td><p>Effectuez une sauvegarde personnalisée et sélectionnez un ou plusieurs volumes à sauvegarder...</p></td>
<td><p>Une sauvegarde complète VSS peut être sélectionnée, ce qui permet aux journaux de transaction pour les bases de données sur les volumes sélectionnés d’être tronqués lorsqu’une sauvegarde réussit.</p></td>
</tr>
<tr class="odd">
<td><p>Effectuez une sauvegarde personnalisée et sélectionnez un ou plusieurs dossiers à sauvegarder...</p></td>
<td><p>Une sauvegarde complète VSS peut être sélectionnée et les fichiers journaux seront tronqués. Toutefois, la restauration de la sauvegarde sera limitée à la restauration de fichier, car l’option de restauration au niveau de l’application ne sera pas disponible.</p></td>
</tr>
</tbody>
</table>


Pour obtenir la procédure détaillée de la sauvegarde d’Exchange avec WSB, voir [Utiliser la sauvegarde Windows Server pour sauvegarder Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md).

Pour obtenir la procédure détaillée de la restauration de données à partir d’une sauvegarde effectuée avec WSB, voir [Utiliser la Sauvegarde Windows Server pour restaurer une sauvegarde d’Exchange](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md).

