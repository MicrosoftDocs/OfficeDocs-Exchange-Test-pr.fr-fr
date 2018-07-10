---
title: 'Autorisations de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Autorisations de messagerie unifiée
ms:assetid: d326c3bc-8f33-434a-bf02-a83cc26a5498
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638193(v=EXCHG.150)
ms:contentKeyID: 50479235
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations de messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les autorisations nécessaires pour effectuer des tâches sur les serveurs d’accès au client qui exécutent le service routeur des appels de messagerie unifiée Microsoft Exchange et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange varient selon la procédure en cours ou la cmdlet que vous souhaitez exécuter.

Pour trouver les autorisations dont vous avez besoin pour effectuer la procédure ou exécuter la cmdlet, procédez comme suit :

1.  Dans le tableau suivant, recherchez la fonctionnalité la plus adaptée à la procédure que vous souhaitez effectuer ou à la cmdlet que vous souhaitez exécuter.

2.  Ensuite, examinez les autorisations requises pour la fonctionnalité. Un de ces groupes de rôles, un groupe de rôles personnalisé équivalent ou un rôle de gestion équivalent doit vous être attribué. Vous pouvez également cliquer sur un groupe de rôles pour visualiser ses rôles de gestion. Si une fonctionnalité affiche plusieurs groupes de rôles, seul l’un de ces groupes de rôles doit vous être attribué pour que vous puissiez exploiter cette même fonctionnalité. Pour plus d’informations sur les groupes de rôles et les rôles de gestion, consultez la rubrique [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md).

3.  Maintenant, exécutez la cmdlet **Get-ManagementRoleAssignment** pour vérifier si les groupes de rôles ou les rôles de gestion qui vous ont été attribués vous permettent de bénéficier des autorisations nécessaires pour gérer la fonctionnalité.
    
    > [!NOTE]
    > Le rôle de gestion de rôle doit vous être attribué pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>. Si vous ne bénéficiez pas des autorisations pour exécuter la cmdlet <strong>Get-ManagementRoleAssignment</strong>, demandez à votre administrateur Exchange de récupérer les groupes de rôles ou les rôles de gestion qui vous sont attribués.


Si vous souhaitez déléguer la possibilité de gérer une fonctionnalité à un autre utilisateur, voir [Déléguer les attributions de rôles](delegate-role-assignments-exchange-2013-help.md).

## Autorisations des composants de messagerie unifiée

Vous pouvez configurer les paramètres des composants et des fonctionnalités de messagerie unifiée dans le tableau suivant.

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
<td><p>Standards automatiques de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Règles de répondeur automatique de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p>Données d’appel de messagerie unifiée et rapports de synthèse</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Serveur d’accès au client (service routeur des appels de messagerie unifiée)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p>Plans de numérotation de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Groupes de recherche de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p>Passerelles IP de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Stratégies de boîte aux lettres de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Messages de messagerie unifiée</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p>Serveur de boîtes aux lettres (service de messagerie unifiée)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
</tbody>
</table>

