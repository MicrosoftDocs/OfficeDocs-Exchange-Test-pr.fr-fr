---
title: 'Autorisations d’infrastructure Exchange et Shell: Exchange 2013 Help'
TOCTitle: Autorisations d’infrastructure Exchange et Shell
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 50477894
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations d’infrastructure Exchange et Shell

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les autorisations nécessaires pour effectuer les tâches de configuration de plusieurs composants Microsoft Exchange Server 2013 dépendent de la procédure réalisée ou de la cmdlet que vous souhaitez exécuter. Reportez-vous à chacune des sections de cette rubrique pour obtenir plus d’informations sur leurs fonctions respectives.

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

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Certaines fonctionnalités nécessitent peut-être des autorisations de type administrateur local sur le serveur que vous souhaitez gérer. Pour gérer ces fonctionnalités, vous devez être membre d’un groupe Administrateurs local sur ce serveur.</td>
</tr>
</tbody>
</table>


## Autorisations d’infrastructure d’Exchange

Le tableau suivant répertorie les autorisations nécessaires à la réalisation de tâches de configuration des paramètres généraux d’Exchange 2013.

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
<td><p>Connexion au service d’audit administrateur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de configuration du Centre d’administration Exchange</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p></td>
</tr>
<tr class="odd">
<td><p>Connectivité du Centre d’Administration Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Paramètres de configuration du serveur Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Paramètres d’aide d’Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Catégories de message</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="odd">
<td><p>Clé de produit</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Intégrité du système de test</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Affichage seul du journal d’audit de l’administrateur</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez également attribuer manuellement le rôle de gestion Journaux d’audit en affichage seul à un groupe de rôles de gestion. Pour plus d’informations, voir <a href="view-only-audit-logs-role-exchange-2013-help.md">Rôle Journaux d’audit en affichage seul</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Écriture dans le journal d’audit</p></td>
<td><p>Les utilisateurs qui sont membres d’un groupe de rôles ou auxquels est attribué un rôle de gestion peuvent écrire dans le journal d’audit administrateur.</p></td>
</tr>
</tbody>
</table>


## Autorisations d’infrastructure de l’environnement de ligne de commande Exchange Management Shell

Le tableau suivant répertorie les autorisations nécessaires pour réaliser les tâches de configuration des fonctions contrôlant la façon dont Exchange Management Shell s’exécute.

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
<td><p>Paramètres de serveur de services de domaine Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestion de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p>Agents d’extension des cmdlets</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Répertoires virtuels PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Installation de PowerShell et de la gestion à distance de Windows</p></td>
<td><p>Administrateur de serveur local</p></td>
</tr>
<tr class="odd">
<td><p>Environnement de ligne de commande Exchange Management Shell distant</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


## Autorisations de fédération et de certificats

Le tableau suivant répertorie les autorisations nécessaires pour réaliser des tâches relatives aux approbations de fédération, à la configuration OAuth, à la gestion des certificats, ainsi qu’à la configuration de déploiement hybride.

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
<td><p>Gestion des certificats</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Approbations de fédération, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Approbations de fédération de test, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestion de l’organisation en affichage seul</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Configuration de déploiement hybride</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Connecteurs intra-organisationnels</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
</tbody>
</table>

