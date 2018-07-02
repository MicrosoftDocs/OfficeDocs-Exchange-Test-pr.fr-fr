---
title: 'L’installation sur des contrôleurs de domaine n’est pas prise en charge avec les autorisations fractionnées: Exchange 2013 Help'
TOCTitle: L’installation sur des contrôleurs de domaine n’est pas prise en charge avec les autorisations fractionnées
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50478771
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# L’installation sur des contrôleurs de domaine n’est pas prise en charge avec les autorisations fractionnées

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-11-12_

Le programme d’installation de Microsoft Exchange Server 2013 a détecté que vous tentez d’exécuter le programme d’installation sur un contrôleur de domaine Active Directory et que l’une des remarques suivante est vraie :

  - L’organisation Exchange est déjà configurée pour les autorisations fractionnées Active Directory.

  - Vous avez sélectionné l’option Autorisations fractionnées Active Directory dans le programme d’installation d’Exchange 2013.

L’installation de Exchange 2013 dans des contrôleurs de domaine n’est pas prise en charge lorsque l’organisation Exchange est configurée pour les autorisations fractionnées Active Directory.

Si vous souhaitez installer Exchange 2013 dans un contrôleur de domaine, vous devez configurer l’organisation pour les autorisations fractionnées ou partagées du contrôle d’accès en fonction du rôle (RBAC).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous ne recommandons pas l’installation d’Exchange 2013 sur des contrôleurs de domaine Active Directory. Pour plus d’informations, consultez la rubrique <a href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">L'installation d'Exchange sur un contrôleur de domaine n'est pas recommandée</a>.</td>
</tr>
</tbody>
</table>


Si vous souhaitez continuer à utiliser les autorisations fractionnées Active Directory, vous devez installer Exchange 2013 sur un serveur membre.

Pour plus d’informations sur les autorisations fractionnées et partagées dans Exchange 2013, consultez les rubriques suivantes :

[Présentation des autorisations fractionnées](understanding-split-permissions-exchange-2013-help.md)

[Configurer Exchange 2013 pour les autorisations divisées](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Configurer Exchange 2013 pour les autorisations partagées](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

