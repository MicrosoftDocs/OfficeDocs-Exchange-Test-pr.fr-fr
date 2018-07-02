---
title: "Mise à niveau d'Exchange 2007 vers Exchange 2013: Exchange 2013 Help"
TOCTitle: Mise à niveau d'Exchange 2007 vers Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51407217
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise à niveau d'Exchange 2007 vers Exchange 2013

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Microsoft Exchange Server 2010 et Exchange Server 2007 disposent de plusieurs rôles serveur : accès au client, boîte aux lettres, transport Hub, messagerie unifiée et transport Edge. Avec Exchange Server 2013, nous avons réduit le nombre de rôles serveur, qui étaient cinq et sont désormais trois : accès au client, boîte aux lettres et transport Edge. La messagerie unifiée est maintenant considérée comme un composant ou une sous-fonctionnalité des fonctionnalités vocales proposées dans Exchange 2013. (Pour plus de détails sur les modifications, voir la section « Architecture Exchange 2013 » dans [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).)

Quand vous mettez à niveau votre organisation Exchange 2007 existante vers Exchange 2013, il y a un laps de temps pendant lequel des serveurs Exchange 2007 et Exchange 2013 coexisteront au sein de votre organisation. Vous pouvez maintenir ce mode pour une durée indéfinie, ou vous pouvez effectuer immédiatement la mise à niveau vers Exchange 2013 en déplaçant toutes les ressources d'Exchange 2007 vers Exchange 2013, puis en désactivant les serveurs Exchange 2007. Vous disposez d'un scénario de coexistence si les conditions suivantes sont remplies :

  - Exchange 2013 est déployé dans une organisation Exchange existante.

  - Plus d'une version de Microsoft Exchange fournit des services de messagerie à l'organisation.

Vous ne pouvez pas mettre à niveau une organisation Exchange 2003 existante directement vers Exchange 2013. Vous devez d'abord mettre à niveau l'organisation Exchange 2003 vers une organisation Exchange 2007 ou Exchange 2010. Vous pourrez alors mettre à niveau l'organisation Exchange 2007 ou Exchange 2010 vers Exchange 2013. Nous vous recommandons de mettre à niveau votre organisation Exchange 2003 vers Exchange 2010, puis de mettre à niveau Exchange 2010 vers Exchange 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devez supprimer toutes les instances d'Exchange 2003 de votre organisation avant de pouvoir effectuer une mise à niveau vers Exchange 2013.</td>
</tr>
</tbody>
</table>


Vous pouvez migrer toutes vos boîtes aux lettres Exchange 2003 vers Exchange Online. Pour plus d’informations sur cette approche, voir [Méthodes de migration des comptes de messagerie vers Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

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

## Coexistence en mode mixte d'Exchange 2013 et d'Exchange 2007 avec Exchange 2010

Si vos sites Active Directory possèdent à la fois Exchange 2010 et Exchange 2007, suivez les instructions de mise à niveau applicables aux deux versions et exécutez les étapes de mise à niveau requises à la fois par Exchange 2010 et Exchange 2007.

## Vue d'ensemble du processus de mise à niveau

Pour que vous puissiez avoir une vue d’ensemble du processus de mise à niveau d’Exchange 2007 vers Exchange 2013, nous avons réuni des ressources relatives à chaque tâche clé dans le tableau suivant. Pour obtenir des conseils détaillés spécifiques, consultez la rubrique [Liste de contrôle : mise à niveau à partir d'Exchange 2007](checklist-upgrade-from-exchange-2007-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tâche</th>
<th>Rubrique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>En savoir plus sur les rôles et composants Exchange 2013.</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Nouveautés d'Exchange 2013</a></p>
<p><a href="client-access-server-exchange-2013-help.md">Serveur d’accès au client</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">Serveur de boîtes aux lettres</a></p>
<p><a href="mail-flow-exchange-2013-help.md">Flux de messagerie</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">Messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Installer Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installer le rôle de transport Edge d’Exchange 2013 à l’aide de l’Assistant Installation</a> (facultatif)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Ajouter des certificats numériques sur le serveur d'accès au client</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuration du serveur d’accès au client Exchange 2013</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificats numériques et SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">Créer une demande de certificat numérique</a></p></td>
</tr>
<tr class="even">
<td><p>Configurer des répertoires virtuels liés à Exchange</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Paramètres par défaut pour les répertoires virtuels Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Déplacer des boîtes aux lettres à partir d’Exchange 2010</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurer des composants de transport</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a> (nécessaire uniquement si vous avez installé un serveur de transport Edge)</p>
<p><a href="mail-routing-exchange-2013-help.md">Routage du courrier</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">Redondance des clichés instantanés</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">Rapports de remise pour les administrateurs</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurer et déployer la messagerie unifiée</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planification de la messagerie unifiée</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Déploiement de la messagerie vocale et la messagerie unifiée</a></p></td>
</tr>
</tbody>
</table>

