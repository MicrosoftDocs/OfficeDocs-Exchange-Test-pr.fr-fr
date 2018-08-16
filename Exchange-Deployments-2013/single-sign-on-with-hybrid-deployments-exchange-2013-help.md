---
title: 'Authentification unique avec les déploiements hybrides: Exchange 2013 Help'
TOCTitle: Authentification unique avec les déploiements hybrides
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50479660
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Authentification unique avec les déploiements hybrides

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-01-29_

L’authentification unique permet aux utilisateurs d’accéder à la fois à l’organisation locale et à l’organisation Office 365 avec un nom d’utilisateur et un mot de passe uniques. Elle offre aux utilisateurs une expérience d’authentification familière et permet aux administrateurs de contrôler facilement les stratégies de compte pour les boîtes aux lettres de l’organisation Exchange Online à l’aide des outils de gestion Active Directory locaux. Bien que vous ne soyez pas obligé de configurer un déploiement hybride avec l’authentification unique activée, nous vous recommandons vivement de le faire. Sans l’authentification unique, les utilisateurs doivent se souvenir de deux ensembles d’informations d’identification, un pour votre organisation locale et un pour Office 365. L’authentification unique présente d’autres avantages :

  - **Archivage Exchange Online**   Lorsque l’authentification unique est déployée, les utilisateurs Outlook locaux sont invités à saisir leurs informations d’identification quand ils accèdent au contenu archivé de l’organisation Exchange Online pour la première fois. Un utilisateur peut temporairement éviter les futures invites de saisie des informations d’identification en choisissant « Enregistrer le mot de passe ». Toutefois, il devra à nouveau saisir ces informations si son mot de passe de compte local est modifié. Si l’authentification unique n’est pas déployée dans des organisations Exchange et que l’archivage Exchange Online est activé, le nom d’utilisateur principal (UPN) local doit correspondre au compte Exchange Online et les utilisateurs seront toujours invités à indiquer leurs informations d’identification locales lors de l’accès à leur archive.

  - **Contrôle de stratégies**   Vous pouvez contrôler les stratégies de compte via Active Directory, ce qui lui donne la possibilité de gérer des stratégies de mot de passe, des restrictions de station de travail, des contrôles de verrouillage, et bien plus encore, sans avoir à effectuer de tâches supplémentaires dans votre organisation Office 365.

  - **Nombre réduit d'appels au support technique**   L'oubli de mot de passe est une source courante d'appels au support technique dans toutes les sociétés. Si les utilisateurs ont moins de mots de passe à mémoriser, ils seront moins susceptibles de les oublier.

Vous disposez de deux options lors du déploiement de l’authentification unique : la synchronisation de mot de passe et les services AD FS (Active Directory Federation Services). Les deux options sont fournies par Azure Active Directory Connect. Nous vous recommandons vivement d’utiliser la méthode de synchronisation de mot de passe, sauf si vous devez spécifiquement utiliser AD FS. La synchronisation de mot de passe fournit en grande partie les mêmes avantages qu’AD FS, mais avec un déploiement moins complexe. Le tableau suivant répertorie quelques avantages et inconvénients courants pour chaque option.

> [!NOTE]
> Par défaut, si vous déployez AD FS et que vos serveurs AD FS locaux ne sont pas accessibles à partir d’Internet pour quelque raison que ce soit, Office 365 revient à la synchronisation de mot de passe pour authentifier les utilisateurs. Cela permet aux utilisateurs disposant de boîtes aux lettres Office 365 de poursuivre leur travail sans interruption, même si vos serveurs locaux ne sont pas disponibles.


Pour en savoir plus sur chaque option, voir [Options d’authentification de l’utilisateur via Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Méthode d’authentification unique</p></th>
<th><p>Avantages</p></th>
<th><p>Inconvénients</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Synchronisation de mot de passe (recommandé)</p></td>
<td><ul>
<li><p>Beaucoup moins complexe qu’AD FS</p></li>
<li><p>Les utilisateurs peuvent se connecter à Office 365 même si votre système Active Directory local n’est pas disponible.</p></li>
<li><p>Moins de serveurs supplémentaires sont requis pour déployer la synchronisation de mot de passe.</p></li>
<li><p>Aucun certificat tiers n’est nécessaire.</p></li>
<li><p>L’accès externe à votre serveur Active Directory local via AD FS n’est pas requis.</p></li>
<li><p>Le déploiement peut souvent être effectué en quelques heures seulement.</p></li>
</ul></td>
<td><ul>
<li><p>La désactivation d’un compte utilisateur dans votre système Active Directory local ne le désactive pas dans Office 365. Vous devez désactiver manuellement le compte dans le portail d’administration Office 365.</p></li>
<li><p>Un système Active Directory local est exigé. Les autres services d’annuaire ne sont pas pris en charge.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>Les modifications de mot de passe sont immédiates.</p></li>
<li><p>La désactivation d’un utilisateur dans votre système Active Directory local désactive son accès au réseau local et son compte Office 365.</p></li>
<li><p>Prise en charge des services d’annuaire autres qu’Active Directory.</p></li>
<li><p>Prise en charge d’une grande variété de déploiements, ainsi que de ceux très volumineux.</p></li>
<li><p>Prise en charge de l’authentification à deux facteurs.</p></li>
</ul></td>
<td><ul>
<li><p>Davantage de serveurs requis, sachant qu’au moins l’un d’entre eux doit se trouver sur votre réseau de périmètre.</p></li>
<li><p>L’adresse IP publique et le port TCP 443 doivent être ouverts sur votre pare-feu.</p></li>
<li><p>La connectivité avec votre système Active Directory local est requise pour détecter les modifications apportées aux mots de passe de compte avec un compte récemment activé ou désactivé.</p></li>
</ul></td>
</tr>
</tbody>
</table>

