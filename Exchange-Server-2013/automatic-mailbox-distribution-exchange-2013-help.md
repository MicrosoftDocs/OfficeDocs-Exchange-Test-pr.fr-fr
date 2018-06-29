---
title: 'Distribution automatique de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Distribution automatique de boîtes aux lettres
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59634347
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Distribution automatique de boîtes aux lettres

 

_**Sapplique à :**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-08-13_

Lorsque vous créez ou déplacez une boîte aux lettres, ou que vous activez la messagerie d’un utilisateur existant, cette boîte aux lettres doit être stockée dans une base de données de boîtes aux lettres. Dans Microsoft Exchange Server 2013, vous pouvez décider de laisser Exchange choisir la base de données à votre place à l’aide de la distribution automatique de boîtes aux lettres.

Avec la distribution automatique de boîtes aux lettres, Exchange examine les bases de données de boîtes aux lettres dans votre organisation, exclut celles qui ne conviennent pas à l’aide de filtres qui seront abordés ultérieurement dans cette rubrique, puis choisit aléatoirement une base de données où doit se trouver la boîte aux lettres. Ce processus distribue aléatoirement les boîtes aux lettres sur toutes les bases de données de boîtes aux lettres appropriées dans votre organisation.

La distribution automatique est utilisée quand vous ne spécifiez pas le paramètre *Database* sur les cmdlets **New-Mailbox** et **Enable-Mailbox** ou le paramètre *TargetDatabase* sur la cmdlet **New-MoveRequest**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La distribution automatique de boîtes aux lettres s’effectue seulement quand une boîte aux lettres est créée sur un serveur Exchange 2013, déplacée sur un serveur Exchange 2013 ou lorsqu’un utilisateur est activé pour la messagerie. Les cmdlets <strong>New-Mailbox</strong>, <strong>New-MoveRequest</strong> et <strong>Enable-Mailbox</strong> doivent être exécutées à partir d’un serveur qui exécute Exchange 2013. Exchange ne redistribue pas les boîtes aux lettres afin de distribuer automatiquement la charge sur les bases de données en fonction de la charge du serveur.</td>
</tr>
</tbody>
</table>


Le processus suivant sert à trouver une base de données de boîtes aux lettres appropriée où doit se trouver une nouvelle boîte aux lettres ou une boîte aux lettres déplacée :

1.  Exchange récupère la liste de toutes les bases de données de boîtes aux lettres dans l’organisation Exchange 2013.

2.  Toute base de données de boîtes aux lettres marquée pour exclusion à partir du processus de distribution est supprimée de la liste des bases de données disponibles. Vous pouvez contrôler quelles bases de données sont exclues. Pour plus d’informations, consultez la rubrique Exclure des bases de données de la distribution automatique plus loin dans cette rubrique.

3.  Toute base de données de boîtes aux lettres se trouvant en dehors des étendues de gestion de bases de données appliquées à l’administrateur effectuant l’opération est supprimée de la liste des bases de données disponibles. Pour plus d’informations, consultez la section Étendues de base de données plus loin dans cette rubrique.

4.  Toute base de données de boîtes aux lettres se trouvant en dehors du site Active Directory local où est exécutée l’opération est supprimée de la liste des bases de données disponibles.

5.  Dans le reste de la liste des bases de données de boîtes aux lettres, Exchange choisit une base de données de manière aléatoire. Si la base de données est en ligne et saine, elle est utilisée par Exchange. Si elle est en mode hors connexion ou en mauvais état, une autre base de données est choisie de manière aléatoire. Si aucune base de données en ligne et saine n’est trouvée, l’opération échoue avec une erreur.

Le processus de sélection d’une base de données de boîtes aux lettres est exécuté par l’agent d’extension de cmdlet Agent de gestion des ressources de boîtes aux lettres. L’agent d’extension de cmdlet `Mailbox Resources Management Agent` fait partie de plusieurs agents d’extension de cmdlet qui renforcent la fonctionnalité d’exécution des cmdlets. Pour plus d’informations sur les agents d’extension de cmdlet, consultez la rubrique [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

Si vous souhaitez ne jamais distribuer les boîtes aux lettres automatiquement, vous pouvez désactiver l’agent d’extension de cmdlet `Mailbox Resources Management Agent`. Quand vous le désactivez, la modification est appliquée à l’organisation Exchange dans son intégralité. Pour plus d’informations sur la désactivation d’agents d’extension de cmdlet, consultez la rubrique [Gérer des agents d’extension de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Exclure des bases de données de la distribution automatique

Par défaut, toutes les boîtes aux lettres en ligne et saines sur les serveurs Exchange 2013 dans le site Active Directory local peuvent être choisies par la distribution automatique de boîtes aux lettres pour stocker une nouvelle boîte aux lettres ou une boîte aux lettres déplacée. Toutefois, vous pouvez exclure certaines bases de données du processus de distribution pour diverses raisons. Vous pouvez, par exemple, désigner une base de données de boîtes aux lettres comme base de données de journalisation dans laquelle doivent se trouver uniquement les boîtes aux lettres que vous spécifiez manuellement. Vous pouvez aussi décider de supprimer temporairement une boîte aux lettres de la rotation pour effectuer une maintenance planifiée. Exchange 2013 vous offre la possibilité d’exclure temporairement ou définitivement les bases de données du processus d’exclusion avec le paramètre *IsExcludedFromProvisioning*, qui peut être défini à l’aide de la cmdlet **Set-MailboxDatabase**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Deux autres paramètres, <em>IsSuspendedFromProvisioning</em> et <em>IsExcludedFromInitialProvisioning</em>, sont également disponibles sur la cmdlet <strong>Set-MailboxDatabase</strong>. Ces paramètres seront supprimés dans une version ultérieure d’Exchange et leur utilisation n’est pas prise en charge.</td>
</tr>
</tbody>
</table>


Le paramètre *IsExcludedFromProvisioning* a deux valeurs valides, `$True` et `$False`. Lorsque vous définissez cette propriété sur `$True`, la base de données de boîtes aux lettres est exclue du processus de distribution automatique. Lorsque vous la définissez sur `$False`, la base de données de boîtes aux lettres est incluse dans le processus de distribution automatique. La valeur par défaut est `$False`.

Pour exclure une base de données de boîtes aux lettres de la distribution automatique, utilisez la commande suivante :

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

Quand une base de données de boîtes aux lettres est exclue de la distribution automatique, le seul moyen de créer une boîte aux lettres dans la base de données ou d’y déplacer une boîte aux lettres consiste à utiliser le paramètre *Database* sur les cmdlets **New-Mailbox** et **Enable-Mailbox** ou le paramètre *TargetDatabase* sur la cmdlet **New-MoveRequest**.

## Étendues de base de données

Les étendues de gestion de bases de données représentent un niveau de contrôle supplémentaire sur le processus de distribution automatique de boîtes aux lettres qui sont disponibles dans Exchange 2013. Si une base de données de boîtes aux lettres est en ligne et saine, elle se trouve dans le site Active Directory local. Si elle n’est pas exclue du processus de distribution automatique, Exchange 2013 vérifie si la base de données de boîtes aux lettres fait partie d’une étendue de base de données appliquée à l’administrateur exécutant la cmdlet. Si elle ne fait pas partie de l’étendue de base de données, elle est incluse dans la liste des bases de données disponibles pour cet administrateur.

Les étendues de bases de données font partie du modèle d’autorisations de contrôle d’accès basé sur les rôles (Role Based Access Control ou RBAC). Pour plus d’informations sur RBAC et les étendues de bases de données, consultez les rubriques suivantes :

  - [Présentation du contrôle d'accès basé sur un rôle](understanding-role-based-access-control-exchange-2013-help.md)

  - [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md)

Les étendues de bases de données peuvent s’avérer utiles si vous avez de nombreuses base de données de boîtes aux lettres dans votre site Active Directory local disponibles pour la distribution automatique, mais que vous souhaitez limiter les bases de données pouvant être utilisées par certains groupes d’administrateurs. Par exemple, vos serveurs Exchange 2013 peuvent desservir plusieurs agences, mais vous souhaitez uniquement autoriser chacune d’entre elles à créer ou déplacer des boîtes aux lettres sur les bases de données de boîtes aux lettres qui leur sont attribuées.

Par défaut, tous les administrateurs dans une organisation Exchange 2013 peuvent voir toutes les bases de données de boîtes aux lettres dans l’organisation. Pour limiter les bases de données qu’ils peuvent voir, et par conséquent limiter les bases de données dans ou sur lesquelles ils peuvent créer ou déplacer des boîtes aux lettres, vous devez procéder comme suit :

1.  Créer une étendue de gestion de bases de données personnalisée en utilisant la cmdlet **New-ManagementScope** qui inclut uniquement les bases de données de boîtes aux lettres que vous souhaitez que l’administrateur utilise.

2.  Associer la nouvelle étendue de base de données à une attribution de rôle de gestion de l’une des façons suivantes :
    
      - En ajoutant la nouvelle étendue de base de données à une attribution de rôle de gestion existante à l’aide du paramètre *CustomConfigWriteScope* sur la cmdlet **Set-ManagementRoleAssignment**. L’étendue de base de données est maintenant appliquée au groupe de rôles de gestion, au groupe de sécurité universel ou à un utilisateur auquel une attribution de rôle est associée.
    
      - En créant une attribution de rôle de gestion à l’aide de la cmdlet **New-ManagementRoleAssignment** et en utilisant le paramètre *CustomConfigWriteScope* pour spécifier la nouvelle étendue de base de données. Vous pouvez créer une attribution de rôle entre un rôle de gestion et un groupe de rôles, un groupe de sécurité universel ou un utilisateur.

3.  Si vous avez créé une attribution de rôle sur un groupe de rôles ou un groupe de sécurité universel, ajoutez les utilisateurs au groupe de rôles ou au groupe de sécurité universel afin que l’attribution de rôle et l’étendue de base de données soient appliquées aux utilisateurs.

4.  Le cas échéant, supprimez l’utilisateur (ou les utilisateurs membres des groupes de rôles ou des groupes de sécurité universels créés lors des étapes précédentes) à qui vous avez affecté la nouvelle attribution de rôle de tout autre groupe de rôles ou groupe de sécurité universel auquel peut être attribuée une étendue de base de données contenant des bases de données auxquelles vous ne souhaitez pas qu’ils accèdent.

5.  Vérifiez que les administrateurs ont accès uniquement aux bases de données auxquelles ils doivent avoir accès.

Une fois cette procédure terminée, les administrateurs auxquels sont attribués les attributions de rôles avec les étendues de bases de données que vous avez créées pourront seulement créer ou déplacer des boîtes aux lettres dans les bases de données spécifiées.

Pour plus d’informations sur l’utilisation des étendues de bases de données pour limiter les bases de données de boîtes aux lettres disponibles pour les administrateurs, consultez la rubrique [Contrôler la distribution automatique de boîtes aux lettres à l’aide d’étendues de base de données](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md).

