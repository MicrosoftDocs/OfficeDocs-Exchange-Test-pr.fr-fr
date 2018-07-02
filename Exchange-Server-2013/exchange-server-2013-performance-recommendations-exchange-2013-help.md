---
title: 'Recommandations en matière de performances Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Recommandations en matière de performances Exchange Server 2013
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63892222
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recommandations en matière de performances Exchange Server 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L'optimisation des performances Exchange Server 2013 et la résolution des problèmes sont plus efficaces lorsque votre environnement a été correctement dimensionné et planifiée. Même si Exchange 2013 a été conçu pour simplifier l'infrastructure des ressources sous-jacente, il peut encore consommer une grande quantité de ressources système, telles que la mémoire, la capacité de stockage et la capacité du processeur.

Les articles de cette section ont été écrits par l'équipe de performances Exchange. Ils contiennent l'expertise du groupe de produits Exchange, ainsi que les meilleures pratiques acquises des dossiers de support client. L'objectif de ces articles est de vous aider à comprendre l'impact des modifications introduites dans Exchange 2013 et l'importance de dimensionner correctement votre infrastructure Exchange 2013. Nous avons également inclus des optimisations recommandées et des conseils sur l'identification des problèmes de performances.

## Changements d'architecture dans Exchange 2013 et d'autres ressources

Les changements d’architecture dans Exchange 2013 sont déjà documentés sur TechNet et dans le [blog de l’équipe Exchange](https://go.microsoft.com/fwlink/p/?linkid=35786). Nous allons tout d’abord aborder quelques modifications de haut niveau que vous devez envisager pour mieux comprendre les coûts des performances et le dimensionnement. Ensuite, ci-dessous, nous avons inclus une liste de références recommandées afin de fournir davantage de contexte dans ces domaines importants.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Consultez <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualisation d'Exchange 2013</a> pour obtenir des instructions d'optimisation des performances concernant le déploiement d'Exchange Server 2013 dans un environnement virtualisé.</td>
</tr>
</tbody>
</table>


Dans Exchange 2013, le rôle de serveur d'accès au client est un serveur proxy sans état. La responsabilité principale du rôle du serveur d'accès au client est maintenant d'authentifier les demandes entrantes puis d'envoyer une requête proxy au serveur de boîtes aux lettres approprié, celui hébergeant la copie active de la boîte aux lettres de l'utilisateur. Cela signifie qu'il n'est plus nécessaire de configurer l'affinité entre le serveur d'accès au client et l'équilibreur de charge pour des protocoles spécifiques.

Un autre changement notable dans Exchange 2013 concerne la banque d'informations. Maintenant, la banque d'informations est constituée de deux types de processus : processus hôte et processus de travail. Chaque instance de base de données est associée à son propre processus Microsoft.Exchange.Store.Worker.exe. Cela permet de mieux isoler les problèmes de base de données et peut réduire l'impact sur les performances d'un problème de base de données sur l'instance de travail pour cette base de données uniquement.

Le service de réplication Microsoft Exchange est responsable de tous les services de haute disponibilité relatifs au rôle de serveur de boîtes aux lettres. Ce service de réplication héberge le composant Active Manager, qui est responsable de la surveillance des échecs et de l'action corrective.

Vous trouverez une excellente publication sur les changements d’architecture, ainsi que sur l’impact du redimensionnement d’un environnement Exchange 2013 à partir de versions antérieures, dans la rubrique relative à l’[architecture de rôle de serveur Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=523735).

Vous trouverez plus d'informations sur les changements d'architecture Exchange 2013 et des informations générales sur d'autres domaines, dans les rubriques suivantes :

[Architecture Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523769)

[Planifier correctement : scénarios de dimensionnement Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Suivi et optimisation des performances de Microsoft Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523774)

[Mise en place d’Exchange Server 2013 (01) Mise à niveau et déploiement d’Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[Mise en place d’Exchange Server 2013 (02) Planifier correctement : dimensionnement d’Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523776)

[Mise en place d’Exchange Server 2013 (03) Meilleures pratiques de virtualisation d’Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523777)

[Mise en place d’Exchange Server 2013 (04) Architecture d’Exchange : haute disponibilité et résilience de site](https://go.microsoft.com/fwlink/p/?linkid=523779)

[Mise en place d’Exchange Server 2013 (05) Connectivité Outlook](https://go.microsoft.com/fwlink/p/?linkid=523781)

[Architecture préférée](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Rôle du serveur d’accès au client Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Meilleures pratiques de virtualisation d’Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523783)

[Équilibrage de charge](load-balancing-exchange-2013-help.md)

[Mises à jour d’Exchange Server : numéros de version et dates de sortie](https://technet.microsoft.com/fr-fr/library/hh135098\(v=exchg.150\))

[Notes de publication relatives à Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)

[Mises à jour pour Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)

[Utilisation de thread ASP.NET sur IIS 7.5, IIS 7.0 et IIS 6.0](https://go.microsoft.com/fwlink/p/?linkid=169626)

