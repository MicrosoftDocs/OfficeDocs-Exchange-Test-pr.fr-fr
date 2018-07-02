---
title: 'Configuration requise pour Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuration requise pour Exchange 2013
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50477623
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration requise pour Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Découvrez la configuration requise pour Exchange 2013 avant d’installer Exchange 2013. Par exemple, vous allez découvrir la configuration matérielle, la configuration réseau et la configuration du système d’exploitation requises.

Avant d’installer Microsoft Exchange Server 2013, nous vous recommandons de parcourir les sections de cette rubrique pour vous assurer que votre réseau, votre matériel, vos logiciels, vos clients et autres éléments sont conformes à la configuration requise pour Exchange 2013. Assurez-vous également que vous comprenez les scénarios de coexistence pris en charge par Exchange 2013 et les versions antérieures d’Exchange.

## Scénarios de coexistence pris en charge

Le tableau suivant répertorie les scénarios pour lesquels la coexistence entre Exchange 2013 et les versions précédentes d'Exchange est prise en charge.

### Coexistence entre Exchange 2013 et les versions antérieures d’Exchange Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Exchange</th>
<th>Coexistence d’organisation Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 et versions antérieures</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Prise en charge avec les versions minimales suivantes d’Exchange :</p>
<ul>
<li><p>1Correctif cumulatif 10 pour Exchange 2007 Service Pack 3 (SP3) sur tous les serveurs Exchange 2007 de l’organisation, serveurs de transport Edge inclus.</p></li>
<li><p>Exchange 2013 Correctif cumulatif 2 (CU2) ou version ultérieure sur tous les serveurs Exchange 2013 de l’organisation.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Prise en charge avec les versions minimales suivantes d’Exchange :</p>
<ul>
<li><p>2 Exchange 2010 SP3 sur tous les serveurs Exchange 2010 de l’organisation, serveurs de transport Edge inclus.</p></li>
<li><p>Exchange 2013 CU2 (Correctif cumulatif 2) ou version ultérieure sur tous les serveurs Exchange 2013 de l’organisation.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organisation mixte Exchange 2010 et Exchange 2007</p></td>
<td><p>Prise en charge avec les versions minimales suivantes d’Exchange :</p>
<ul>
<li><p>1Correctif cumulatif 10 pour Exchange 2007 SP3 sur tous les serveurs Exchange 2007 de l’organisation, serveurs de transport Edge inclus.</p></li>
<li><p>2 Exchange 2010 SP3 sur tous les serveurs Exchange 2010 de l’organisation, serveurs de transport Edge inclus.</p></li>
<li><p>Exchange 2013 CU2 (Correctif cumulatif 2) ou version ultérieure sur tous les serveurs Exchange 2013 de l’organisation.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Pour créer un abonnement EdgeSync entre un serveur de transport Hub Exchange 2007 et un serveur de transport Edge Exchange 2013 SP1, vous devez installer le correctif cumulatif 13 pour Exchange 2007 SP3 ou version ultérieure sur le serveur de transport Hub Exchange 2007.

2   Pour créer un abonnement EdgeSync entre un serveur de transport Hub Exchange 2010 et un serveur de transport Edge Exchange 2013 SP1, vous devez installer le correctif cumulatif 5 ou version ultérieure pour Exchange 2010 SP3 sur le serveur de transport Hub Exchange 2010.

## Scénarios de déploiement hybride pris en charge

Exchange 2013 prend en charge les déploiements hybrides avec les locataires Office 365 mis à niveau vers la dernière version d’Office 365. Pour plus d’informations sur les déploiements hybrides spécifiques, voir [Configuration requise pour un déploiement hybride](https://technet.microsoft.com/fr-fr/library/hh534377\(v=exchg.150\)).

## Serveurs réseau et d’annuaire

Le tableau suivant présente la configuration requise pour les serveurs réseau et d’annuaire au sein de votre organisation Exchange 2013.

**Configuration requise des serveurs réseau et d’annuaire pour Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant</th>
<th>Conditions requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contrôleur de schéma</p></td>
<td><p>Par défaut, le contrôleur de schéma s’exécute sur le premier contrôleur de domaine Active Directory installé dans une forêt. Le contrôleur de schéma doit exécuter l’une des configurations suivantes :</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2003 Standard Edition avec Service Pack 2 (SP2) ou version ultérieure (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition avec SP2 ou version ultérieure (32 bits ou 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Serveur de catalogue global</p></td>
<td><p>Chaque site Active Directory où vous prévoyez d’installer Exchange 2013 doit disposer d’au moins un serveur de catalogue global exécutant l’une des configurations suivantes :</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2003 Standard Edition avec Service Pack 2 (SP2) ou version ultérieure (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition avec SP2 ou version ultérieure (32 bits ou 64 bits)</p></li>
</ul>
<p>Pour plus d’informations sur les serveurs de catalogue global, voir <a href="http://go.microsoft.com/fwlink/p/?linkid=178996">Qu’est-ce que le catalogue global ?</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Contrôleur de domaine</p></td>
<td><p>Chaque site Active Directory où vous prévoyez d’installer Exchange 2013 doit disposer d’au moins un contrôleur de domaine accessible en écriture exécutant l’une des configurations suivantes :</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise SP1 ou version ultérieure</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise SP1 ou version ultérieure (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou version ultérieure</p></li>
<li><p>Windows Server 2003 Standard Edition avec Service Pack 2 (SP2) ou version ultérieure (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition avec SP2 ou version ultérieure (32 bits ou 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Forêt Active Directory</p></td>
<td><p>Active Directory doit être en mode de fonctionnalité de forêt Windows Server 2003 ou supérieur2.</p></td>
</tr>
<tr class="odd">
<td><p>Prise en charge des espaces de noms DNS</p></td>
<td><p>Exchange 2013 prend en charge les espaces de noms DNS (Domain Name System) suivants :</p>
<ul>
<li><p>Contigu</p></li>
<li><p>Non contigu</p></li>
<li><p>Domaines en une seule partie</p></li>
<li><p>Disjoint</p></li>
</ul>
<p>Pour plus d’informations sur les espaces de noms DNS pris en charge par Exchange, consultez l’article 2269838 de la Base de connaissances Microsoft, <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2269838">Compatibilité de Microsoft Exchange avec les domaines en une seule partie, les espaces de noms disjoints et les espaces de noms discontinus</a>.</p></td>
</tr>
<tr class="even">
<td><p>Prise en charge IPv6</p></td>
<td><p>Dans Exchange 2013, le protocole IPv6 est pris en charge uniquement lorsque le protocole IPv4 est également installé et activé. En cas de déploiement d’Exchange 2013 dans cette configuration, et si le réseau prend en charge les protocoles IPv4 et IPv6, tous les serveurs Exchange peuvent échanger des données avec des périphériques, des serveurs et des clients utilisant des adresses IPv6. Pour plus d’informations, voir <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Prise en charge du protocole IPv6 dans Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 est pris en charge uniquement avec Exchange 2013 SP1 ou version ultérieure.

2   Le mode de fonctionnalité de forêt Windows Server 2012 R2 est pris en charge uniquement avec Exchange 2013 SP1 ou version ultérieure.

## Architecture du serveur d’annuaire

L’utilisation de contrôleurs de domaine Active Directory 64 bits augmente les performances du service d’annuaire d’Exchange 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans le cas d’environnements à domaines multiples dans lesquels le japonais a été défini comme langue locale d’Active Directory pour les contrôleurs de domaine Windows Server 2008, les serveurs peuvent ne pas recevoir certains attributs stockés sur un objet pendant la réplication entrante. Pour plus d’informations, consultez l’article 949189 de la Base de connaissances Microsoft, <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=949189">Un contrôleur de domaine Windows Server 2008 qui est configuré avec les paramètres régionaux japonais peut ne pas appliquer des mises à jour aux attributs d’un objet lors la réplication entrante</a>.</td>
</tr>
</tbody>
</table>


## Installation d’Exchange 2013 sur des serveurs d’annuaire

Pour des raisons de sécurité et de performances, nous vous recommandons d’installer Exchange 2013 sur des serveurs membres uniquement et non sur des serveurs d’annuaire Active Directory. Toutefois, vous ne pouvez pas exécuter DCPromo sur un ordinateur exécutant Exchange 2013. Après l’installation d’Exchange 2013, la modification de son rôle de serveur membre en serveur d’annuaire, ou inversement, n’est pas prise en charge.

## Matériel

La configuration matérielle recommandée pour les serveurs Exchange 2013 varie en fonction d’un certain nombre de facteurs incluant les rôles serveurs installés et la charge anticipée qui sera placée sur les serveurs.

Pour plus d’informations sur la façon de dimensionner correctement et de configurer votre déploiement, consultez la rubrique [Recommandations en matière de dimensionnement et de configuration d'Exchange 2013](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md).

Pour plus d’informations sur le déploiement d’Exchange dans un environnement virtualisé, voir [Virtualisation d'Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md).

**Configuration matérielle requise pour Exchange 2013**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant</th>
<th>Conditions requises</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processeur</p></td>
<td><ul>
<li><p>ordinateur basé sur une architecture x64 équipé d'un processeur Intel prenant en charge l'architecture 64 d'Intel (Intel EM64T)</p></li>
<li><p>processeur AMD prenant en charge la plate-forme AMD64</p></li>
<li><p>les processeurs Intel Itanium IA64 ne sont pas pris en charge</p></li>
</ul></td>
<td><p>Consultez la section « Système d’exploitation » dans cette rubrique pour connaître les systèmes d’exploitation pris en charge.</p></td>
</tr>
<tr class="even">
<td><p>Mémoire</p></td>
<td><p>Varie en fonction des rôles Exchange installés :</p>
<ul>
<li><p><strong>Boîte aux lettres</strong>   8 Go au minimum</p></li>
<li><p><strong>Accès au client</strong>   4 Go au minimum</p></li>
<li><p><strong>Boîte aux lettres et Accès au client combinés</strong>   8 Go au minimum</p></li>
<li><p><strong>Transport Edge</strong>   4 Go au minimum</p></li>
</ul></td>
<td><p>Aucun.</p></td>
</tr>
<tr class="odd">
<td><p>Taille de fichier d'échange</p></td>
<td><p>Les tailles minimale et maximale du fichier d’échange doivent être définies sur la quantité de RAM physique plus 10 Mo, jusqu’à une taille maximale de 32 778 Mo si vous utilisez plus de 32 Go de RAM.</p></td>
<td><p>Pour obtenir des recommandations détaillées sur le fichier d’échange, consultez la section « Fichier d’échange » dans <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Recommandations en matière de dimensionnement et de configuration d'Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espace disque</p></td>
<td><ul>
<li><p>Au moins 30 Go sur le lecteur sur lequel vous installez Exchange</p></li>
<li><p>500 Mo supplémentaires d'espace disque disponible pour chaque module linguistique de la messagerie unifiée que vous prévoyez d'installer</p></li>
<li><p>200 Mo d'espace disque disponible sur le lecteur système</p></li>
<li><p>Un disque dur qui héberge la base de données des files d’attente de messages avec au moins 500 Mo d’espace libre.</p></li>
</ul></td>
<td><p>Pour plus d’informations sur les recommandations en matière de stockage, consultez la rubrique <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Options de configuration du stockage Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Lecteur</p></td>
<td><p>lecteur de DVD-ROM, local ou accessible sur le réseau</p></td>
<td><p>Aucun.</p></td>
</tr>
<tr class="even">
<td><p>Résolution d'écran</p></td>
<td><p>1 024 x 768 pixels ou supérieure</p></td>
<td><p>Aucun.</p></td>
</tr>
<tr class="odd">
<td><p>Format de fichier</p></td>
<td><p>Partitions de disque formatées comme systèmes de fichiers NTFS, ce qui s'applique aux partitions suivantes :</p>
<ul>
<li><p>partition système</p></li>
<li><p>partitions qui stockent des fichiers binaires Exchange ou des fichiers générés par la journalisation des diagnostics Exchange</p></li>
</ul>
<p>Les partitions de disque contenant les types de fichier suivants peuvent être formatées en ReFS :</p>
<ul>
<li><p>partitions contenant des fichiers du journal des transactions</p></li>
<li><p>partitions contenant des fichiers de base de données</p></li>
<li><p>partitions contenant des fichiers d’indexation de contenu</p></li>
</ul></td>
<td><p>Aucun.</p></td>
</tr>
</tbody>
</table>


## Système d’exploitation

Le tableau suivant répertorie les systèmes d’exploitation pris en charge pour Exchange 2013.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous n’assurons pas la prise en charge de l’installation d’Exchange 2013 sur un ordinateur qui s’exécute en mode Windows Server Core. L’ordinateur doit exécuter l’installation complète de Windows Server. Pour installer Exchange 2013 sur un ordinateur qui s’exécute en mode Windows Server Core, vous devez convertir le serveur en installation complète de Windows Server en procédant comme suit :
<ul>
<li><p><strong>Windows Server 2008 R2</strong>   Réinstallez Windows Server et sélectionnez l’option <strong>Installation complète</strong>.</p></li>
<li><p><strong>Windows Server 2012 R2</strong> ou <strong>Windows Server 2012</strong>   Convertissez votre serveur en mode Windows Server Core en installation complète en exécutant la commande suivante.</p>
<pre><code>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</code></pre></li>
</ul></td>
</tr>
</tbody>
</table>


**Systèmes d’exploitation pris en charge pour Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant</th>
<th>Conditions requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rôles serveur de boîtes aux lettres, d’accès au client et de transport Edge</p></td>
<td><p>Une des possibilités suivantes :</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard avec Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise avec Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou version ultérieure</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outils de gestion</p></td>
<td><p>Une des possibilités suivantes :</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard avec SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise avec SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou version ultérieure</p></li>
<li><p>Édition 64 bits de Windows 8.12</p></li>
<li><p>Édition 64 bits de Windows 8</p></li>
<li><p>Édition 64 bits de Windows 7 Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 est uniquement pris en charge avec Exchange 2013 SP1 ou version ultérieure.

2   Windows 8.1 est uniquement pris en charge avec Exchange 2013 SP1 ou version ultérieure.

**Versions de Windows Management Framework prises en charge pour Exchange 2013**

Exchange 2013 prend uniquement en charge la version de Windows Management Framework qui est intégrée à la version de Windows sur laquelle vous installez Exchange. N’installez pas de versions de Windows Management Framework disponibles en téléchargement autonome sur les serveurs qui exécutent Exchange.

## .NET Framework

Nous vous recommandons vivement d’utiliser la dernière version d’.NET Framework prise en charge par la version d’Exchange que vous installez.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Clients pris en charge

Exchange 2013 prend en charge les versions suivantes d’Outlook et d’Entourage pour Mac :

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 pour Mac, Web Services Edition

  - Outlook pour Mac pour Office 365

  - Outlook pour Mac 2011

Pour obtenir la liste des versions Outlook prises en charge par Exchange, voir [Mises à jour Outlook](https://go.microsoft.com/fwlink/p/?linkid=513459).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous conseillons vivement d’installer les derniers Service Packs et mises à jour disponibles pour que vos utilisateurs bénéficient de la meilleure expérience possible lors de leur connexion à Exchange.</td>
</tr>
</tbody>
</table>


Les clients Outlook antérieurs à Outlook 2007 ne sont pas pris en charge. Les clients de messagerie sur les systèmes d'exploitation Mac qui nécessitent le protocole DAV, tels qu'Entourage 2008 pour Mac RTM et Entourage 2004, ne sont pas pris en charge.

Outlook Web App prend en charge plusieurs navigateurs sur divers systèmes d’exploitation et périphériques. Pour plus d'informations, consultez la rubrique [Nouveautés Outlook Web App dans Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

