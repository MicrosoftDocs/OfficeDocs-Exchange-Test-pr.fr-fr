---
title: 'Autorisations de flux de messagerie: Exchange 2013 Help'
TOCTitle: Autorisations de flux de messagerie
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50479565
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorisations de flux de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les autorisations requises pour effectuer les tâches relatives au flux de messagerie varient en fonction de la procédure exécutée ou de la cmdlet que vous voulez exécuter. Pour plus d’informations sur les fonctionnalités de transport, voir [Flux de messagerie](mail-flow-exchange-2013-help.md).

Cette rubrique répertorie les autorisations requises pour gérer les fonctionnalités de flux de messagerie dans Microsoft Exchange Server 2013. Pour plus d’informations sur la liaison entre les autorisations Office 365 et les autorisations Exchange, voir [Autorisations dans Office 365](https://go.microsoft.com/fwlink/p/?linkid=335814).

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
<td>Certaines fonctionnalités que vous souhaitez gérer existent peut-être sur les serveurs de transport Edge. Pour gérer les fonctionnalités sur les serveurs de transport Edge, vous devez être membre du groupe Administrateurs local sur le serveur de transport Edge que vous souhaitez gérer. Les serveurs de transport Edge n’utilisent pas le contrôle d’accès en fonction du rôle (RBAC). Les fonctionnalités qui peuvent être gérées sur les serveurs de transport Edge disposent d’un administrateur local de transport Edge dans la colonne « Autorisations requises » du tableau suivant.</td>
</tr>
</tbody>
</table>


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


## Autorisations de flux de messagerie

Vous pouvez utiliser les fonctions indiquées dans le tableau suivant pour configurer le flux de messagerie dans le service de transport frontal sur les serveurs d’accès au client, dans le service de transport des boîtes aux lettres sur le serveur de boîtes aux lettres et sur les serveurs de transport Edge. Les autorisations requises pour configurer chaque fonctionnalité sont répertoriées.

Les utilisateurs auxquels est affecté le groupe de rôles Affichage seul peuvent visualiser la configuration des fonctionnalités indiquées dans le tableau suivant. Pour plus d'informations, voir [Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).

**Serveurs de boîtes aux lettres et serveurs d'accès client**


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
<td><p>Domaines acceptés</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Gestion du site Active Directory et des liens du site</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Fonctionnalités de blocage du courrier indésirable</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="even">
<td><p>Mises à jour de la fonctionnalité de blocage du courrier indésirable</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des certificats</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Connecteurs d'agent de remise</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="odd">
<td><p>Notifications d'état de remise</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Connecteurs étrangers</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Service de transport frontal</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="odd">
<td><p>Journalisation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Accès aux boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuration des boîtes aux lettres de courrier indésirable</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="help-desk-exchange-2013-help.md">Support technique</a></p></td>
</tr>
<tr class="even">
<td><p>Service de transport de boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="odd">
<td><p>Infos-courrier</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Classifications des messages</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="odd">
<td><p>Suivi des messages</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Transport modéré</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Files d'attente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Connecteurs de réception</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="odd">
<td><p>Domaines distants</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Agrégation de listes fiables</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="odd">
<td><p>Connecteurs d'envoi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="even">
<td><p>Redondance des clichés instantanés</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Test des flux de messages</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Test du traitement des règles de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Agents de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Configuration du transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Journaux de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Règles de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="odd">
<td><p>service de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestion de l’hygiène</a></p></td>
</tr>
<tr class="even">
<td><p>Domaines X.400</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
</tbody>
</table>


**Serveurs de transport Edge**


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
<td><p>Domaines acceptés - Transport Edge</p></td>
<td><p>Administrateur local du transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Réécriture d’adresse - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Serveur de transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Files d'attente - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Connecteurs de réception - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Connecteurs d'envoi - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Configuration du transport - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="odd">
<td><p>Journaux de transport - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
<tr class="even">
<td><p>Règles de transport - Transport Edge</p></td>
<td><p>Administrateur Local de Transport Edge</p></td>
</tr>
</tbody>
</table>

