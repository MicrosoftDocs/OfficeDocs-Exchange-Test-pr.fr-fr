---
title: 'Autorisations pour la gestion des rôles: Exchange 2013 Help'
TOCTitle: Autorisations pour la gestion des rôles
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 50479245
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations pour la gestion des rôles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les autorisations requises pour effectuer les tâches de configuration des rôles de gestion varient en fonction de la procédure exécutée ou de la cmdlet que vous voulez exécuter. Pour plus d'informations sur les rôles de gestion, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Pour trouver les autorisations dont vous avez besoin pour effectuer la procédure ou exécuter la cmdlet, procédez comme suit :

1.  Dans le tableau suivant, recherchez la fonctionnalité la plus adaptée à la procédure que vous souhaitez effectuer ou à la cmdlet que vous souhaitez exécuter.

2.  Ensuite, examinez les autorisations requises pour la fonctionnalité. Un de ces groupes de rôles, un groupe de rôles personnalisé équivalent ou un rôle de gestion équivalent doit vous être attribué. Vous pouvez également cliquer sur un groupe de rôles pour visualiser ses rôles de gestion. Si une fonctionnalité affiche plusieurs groupes de rôles, seul l’un de ces groupes de rôles doit vous être attribué pour que vous puissiez exploiter cette même fonctionnalité. Pour plus d’informations sur les groupes de rôles et les rôles de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

3.  Maintenant, exécutez la cmdlet **Get-ManagementRoleAssignment** pour vérifier si les groupes de rôles ou les rôles de gestion qui vous ont été attribués vous permettent de bénéficier des autorisations nécessaires pour gérer la fonctionnalité.
    
    > [!NOTE]
    > Le rôle de gestion de rôle doit vous être attribué pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>. Si vous ne bénéficiez pas des autorisations pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>, demandez à votre administrateur Exchange de récupérer les groupes de rôles ou les rôles de gestion qui vous sont attribués.


Si vous souhaitez déléguer la possibilité de gérer une fonctionnalité à un autre utilisateur, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

## Autorisations pour la gestion des rôles

Vous pouvez utiliser les fonctionnalités du tableau ci-après pour gérer les groupes de rôles de gestion, les rôles, les stratégies d’attribution, les attributions et les étendues qui définissent les autorisations que vous pouvez appliquer aux administrateurs et aux utilisateurs finaux. Les utilisateurs auxquels est affecté le groupe de rôles de gestion de l’organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d’informations, consultez la rubrique Afficher uniquement la gestion de l’organisation[Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Rôles de gestion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Rôles de gestion sans portée</p></td>
<td><p>Rôle de gestion <a href="unscoped-role-management-role-exchange-2013-help.md">Rôle de gestion de rôle non délimité</a></p></td>
</tr>
<tr class="odd">
<td><p>Groupes de rôles</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Stratégies d'attribution</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Attributions de rôle</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Étendues de gestion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Entrées de rôles de gestion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Autorisations héritées</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Autorisations fractionnées Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>

> [!NOTE]  
> Pour exécuter la commande <code>setup.exe</code> à l’aide des paramètres <em>PrepareAD</em> and <em>ActiveDirectorySplitPermissions</em>, le compte doit être membre des groupes Administrateurs du schéma et Administrateurs d’entreprise.

</td>
</tr>
</tbody>
</table>

