---
title: 'Autorisations de haute disponibilité et de résilience des sites: Exchange 2013 Help'
TOCTitle: Autorisations de haute disponibilité et de résilience des sites
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 50478318
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations de haute disponibilité et de résilience des sites

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-11-12_

Les autorisations requises pour configurer une haute disponibilité varient en fonction de la procédure en cours ou de la cmdlet que vous voulez exécuter. Pour plus d'informations sur la haute disponibilité, voir [Haute disponibilité et résilience de site](high-availability-and-site-resilience-exchange-2013-help.md).

Pour trouver les autorisations dont vous avez besoin pour effectuer la procédure ou exécuter la cmdlet, procédez comme suit :

1.  Dans le tableau suivant, recherchez la fonctionnalité la plus adaptée à la procédure que vous souhaitez effectuer ou à la cmdlet que vous souhaitez exécuter.

2.  Ensuite, examinez les autorisations requises pour la fonctionnalité. Un de ces groupes de rôles, un groupe de rôles personnalisé équivalent ou un rôle de gestion équivalent doit vous être attribué. Vous pouvez également cliquer sur un groupe de rôles pour visualiser ses rôles de gestion. Si une fonctionnalité affiche plusieurs groupes de rôles, seul l’un de ces groupes de rôles doit vous être attribué pour que vous puissiez exploiter cette même fonctionnalité. Pour plus d’informations sur les groupes de rôles et les rôles de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

3.  Maintenant, exécutez la cmdlet **Get-ManagementRoleAssignment** pour vérifier si les groupes de rôles ou les rôles de gestion qui vous ont été attribués vous permettent de bénéficier des autorisations nécessaires pour gérer la fonctionnalité.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le rôle de gestion de rôle doit vous être attribué pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>. Si vous ne bénéficiez pas des autorisations pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>, demandez à votre administrateur Exchange de récupérer les groupes de rôles ou les rôles de gestion qui vous sont attribués.</td>
    </tr>
    </tbody>
    </table>


Si vous souhaitez déléguer la possibilité de gérer une fonctionnalité à un autre utilisateur, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

## Autorisations du groupe de disponibilité de base de données

Vous pouvez utiliser les fonctionnalités décrites dans le tableau suivant pour ajouter, supprimer et configurer des paramètres pour les groupes de disponibilité de base de données.

Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Appartenance au groupe de disponibilité de base de données</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
</tr>
<tr class="even">
<td><p>Propriétés du groupe de disponibilité de base de données</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
</tr>
<tr class="odd">
<td><p>Groupes de disponibilité de base de données</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
</tr>
<tr class="even">
<td><p>Réseaux de groupes de disponibilité de bases de données</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rôle des groupes de disponibilité de base de données</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de copie de base de données de boîtes aux lettres

Vous pouvez utiliser les fonctionnalités décrites dans le tableau suivant pour ajouter, supprimer, mettre à jour et activer des copies de bases de données de boîtes aux lettres.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Autorisations requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Basculement de base de données</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="databases-role-exchange-2013-help.md">Rôle des bases de données</a></p></td>
</tr>
<tr class="even">
<td><p>Copies de bases de données de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Rôle des copies de base de données</a></p></td>
</tr>
<tr class="odd">
<td><p>Basculement de serveur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="databases-role-exchange-2013-help.md">Rôle des bases de données</a></p></td>
</tr>
<tr class="even">
<td><p>Mise à jour d'une copie de base de données de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Rôle des copies de base de données</a></p></td>
</tr>
</tbody>
</table>

