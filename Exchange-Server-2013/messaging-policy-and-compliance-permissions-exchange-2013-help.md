---
title: 'Stratégie de messagerie et autorisations de conformité: Exchange 2013 Help'
TOCTitle: Stratégie de messagerie et autorisations de conformité
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50479500
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégie de messagerie et autorisations de conformité

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Les autorisations requises pour configurer une stratégie de messagerie et les fonctionnalités de compatibilité varient en fonction de la procédure en cours ou de la cmdlet que vous voulez exécuter. Pour plus d'informations sur la stratégie de messagerie et la conformité, voir [Stratégie et conformité de messagerie](messaging-policy-and-compliance-exchange-2013-help.md).

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


## Stratégie de messagerie et autorisations de conformité

Les fonctionnalités présentées dans le tableau suivant permettent de configurer une stratégie de messagerie et les fonctionnalités de conformité. Les groupes de rôles requis pour configurer chaque fonctionnalité sont répertoriés.

Les utilisateurs auxquels est affecté le groupe de rôles Gestion de l'organisation en affichage seul peuvent visualiser la configuration des fonctionnalités dans le tableau suivant. Pour plus d'informations, voir [Gestion de l’organisation en affichage seul](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Prévention des pertes de données (DLP)</p></td>
<td><p>Si vous utilisez Office 365 :</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrateur global d’Office 365</a>, qui inclut automatiquement Exchange <a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrateur de service d’Office 365</a>, plus le groupe de rôles d’administration <a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a> dans Exchange</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrateur de mots de passe Office 365</a></p></li>
</ul>
<p>Si vous utilisez Exchange Server 2013 ou Exchange Online uniquement :</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Suppression du contenu de la boîte aux lettres (à l’aide de la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dd298173(v=exchg.150)">Search-Mailbox</a> avec l’indicateur <em>DeleteContent</em>)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a> <strong>et</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">Rôle d’importation et d’exportation de boîtes aux lettres</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, le rôle d’importation et d’exportation de boîte aux lettres n’est affecté à aucun groupe de rôles. Vous pouvez attribuer un rôle de gestion à un groupe de rôles, un utilisateur ou un groupe de sécurité universel intégré ou personnalisé. Il est conseillé d'attribuer un rôle à un groupe de rôles. Pour plus d’informations, consultez la rubrique <a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Ajouter un rôle à un utilisateur ou un groupe de sécurité universel</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres de découverte - Créer</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="even">
<td><p>Journalisation</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="odd">
<td><p>Enregistrement d’audit dans les boîtes aux lettres</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Classifications des messages</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Gestion des enregistrements de messagerie</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Découverte électronique locale</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, le groupe de rôles Gestion de la découverte ne possède aucun membre. Aucun utilisateur, y compris les administrateurs, ne dispose des autorisations requises pour rechercher des boîtes aux lettres. Pour plus d’informations, voir <a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Attribution d’autorisations eDiscovery dans Exchange</a>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>Blocage local</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestion de la détection</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour créer une archive permanente basée sur une demande, un utilisateur a besoin des rôles Recherche de boîte aux lettres et Mise en attente pour litige afin d'être assigné directement, ou via abonnement, à un groupe de rôles auquel les deux rôles sont attribués. Pour créer une archive permanente sans utiliser de demande, qui met en attente tous les éléments de boîtes aux lettres, vous devez disposer du rôle Mise en attente pour litige. Les deux rôles sont assignés au groupe de rôles Gestion de la découverte.<br />
Le rôle Mise en attente pour litige est assigné au groupe de rôles Gestion de l'organisation. Les membres du groupe de rôles Gestion de l'organisation peuvent placer tous les éléments dans une archive permanente dans une boîte aux lettres, mais ne peuvent pas créer une archive permanente basée sur une demande.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Archive sur site</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p></td>
</tr>
<tr class="odd">
<td><p>Archive sur site – Tester la connexion</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="server-management-exchange-2013-help.md">Gestion du serveur</a></p></td>
</tr>
<tr class="even">
<td><p>Configuration de la gestion des droits relatifs à l'information (IRM)</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gestion de la conformité</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p></td>
</tr>
<tr class="odd">
<td><p>Stratégies de rétention – Appliquer</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestion des destinataires</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
<tr class="even">
<td><p>Stratégies de rétention - Créer</p></td>
<td><p>Consultez l'entrée concernant la Gestion des enregistrements de messagerie</p></td>
</tr>
<tr class="odd">
<td><p>Règles de transport</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestion de l’organisation</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestion des enregistrements</a></p></td>
</tr>
</tbody>
</table>

