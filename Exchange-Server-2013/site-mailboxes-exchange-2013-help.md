---
title: 'Boîtes aux lettres de site: Exchange 2013 Help'
TOCTitle: Boîtes aux lettres de site
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50477728
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Boîtes aux lettres de site

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les courriers électroniques et les documents sont généralement conservés dans deux référentiels de données uniques et indépendants. La plupart des organisations collaborent à l'aide des deux moyens. Le problème vient du fait que la messagerie électronique et les documents sont consultés à l'aide de clients différents. Il en résulte généralement une perte de productivité de la part des utilisateurs et une expérience utilisateur dégradée.

La *boîte aux lettres de site* est un nouveau concept dans Microsoft Exchange 2013 qui tente de résoudre ce problème. Les boîtes aux lettres de site améliorent la collaboration et la productivité des utilisateurs en permettant l'accès aux documents Microsoft SharePoint 2013 et à la messagerie Exchange à l'aide d'une même interface client. Une boîte aux lettres de site comprend fonctionnellement l'appartenance au site SharePoint 2013 (propriétaires et membres), le stockage partagé par le biais d'une boîte aux lettres Exchange 2013 pour les messages électroniques et un site SharePoint 2013 pour les documents, ainsi qu'une interface de gestion qui se charge de répondre aux besoins de configuration et de cycle de vie.

Les boîtes aux lettres de site nécessitent une configuration et une intégration à Exchange 2013 et SharePoint Server 2013. Pour plus d'informations sur la configuration de votre organisation Exchange 2013 afin qu'elle fonctionne avec votre organisation SharePoint Server 2013, consultez les rubriques suivantes :

  - [Configurer des boîtes aux lettres du site dans SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264).

  - [Intégration à SharePoint et Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)

Pour plus d'informations sur les fonctionnalités de collaboration dans Exchange Server 2013, consultez la rubrique [Collaboration](collaboration-exchange-2013-help.md).

**Contenu de cette rubrique**

Fonctionnement des boîtes aux lettres de site

Stratégies de mise en service des boîtes aux lettres de site

## Fonctionnement des boîtes aux lettres de site

Quand un membre du projet archive des messages électroniques ou des documents à l'aide de la boîte aux lettres de site, n'importe quel autre membre du projet peut alors accéder à ce contenu. Les boîtes aux lettres de site sont exposées dans Outlook 2013 et permettent aux utilisateurs d'accéder facilement aux messages électroniques et documents des projets qui les intéressent. D'autre part, il est possible d'accéder au même ensemble de contenu directement depuis le site SharePoint lui-même. Avec les boîtes aux lettres de site, le contenu est conservé à son emplacement correspondant. Exchange stocke les messages électroniques, offrant ainsi aux utilisateurs le même affichage de message pour les conversations par message électronique que ce qu'ils utilisent tous les jours dans leur propre boîte aux lettres. SharePoint stocke quant à lui les documents pour proposer la co-création et la gestion des versions. Exchange synchronise uniquement les métadonnées nécessaires à partir de SharePoint pour créer une vue du document dans Outlook (par exemple, titre du document, date de dernière modification, auteur de la dernière modification, taille).

![Diagramme de stockage et d’utilisation des boîtes aux lettres de site](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "Diagramme de stockage et d’utilisation des boîtes aux lettres de site")

## Stratégies de mise en service des boîtes aux lettres de site

Des quotas de boîtes aux lettres de site peuvent être définis à l'aide des cmdlets **SiteMailboxProvisioningPolicy** dans l'environnement de ligne de commande Exchange Management Shell. Les stratégies de mise en service des boîtes aux lettres de site s'appliquent uniquement aux messages électroniques envoyés à la boîte aux lettres de site ou à partir de celle-ci, ainsi qu'à la taille de la boîte aux lettres de site sur le serveur Exchange. Les paramètres du référentiel de documents sont configurés dans SharePoint. Bien que vous puissiez créer plusieurs stratégies de mise en service de boîtes aux lettres de site à l'aide de la cmdlet **New-SiteMailboxProvisioningPolicy**, seule la stratégie de mise en service par défaut sera appliquée à toutes les boîtes aux lettres de site. Vous ne pouvez pas appliquer plusieurs stratégies dans votre organisation. Les stratégies de mise en service permettent de définir les quotas suivants :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Description</th>
<th>Paramètre par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p>Le paramètre <em>IssueWarningQuota</em> spécifie la taille des boîtes aux lettres de site qui déclenchent un message d'avertissement vers la boîte aux lettres de site</p></td>
<td><p>4,5 Go</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p>Le paramètre <em>MaxReceiveSize</em> spécifie la taille maximale des messages électroniques que peut recevoir la boîte aux lettres de site.</p></td>
<td><p>36 Mo</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p>Le paramètre <em>ProhibitSendReceiveQuota</em> spécifie la taille à partir de laquelle la boîte aux lettres de site ne peut plus envoyer ou recevoir de messages.</p></td>
<td><p>5 Go</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la configuration de stratégies de mise en service de la boîte aux lettres de site, consultez la rubrique [Gestion des stratégies de configuration des boîtes aux lettres de site](manage-site-mailbox-provisioning-policies-exchange-2013-help.md).

Fonctionnement des boîtes aux lettres de site

## Stratégie du cycle de vie et rétention

Le cycle de vie d'une boîte aux lettres de site est géré via un site SharePoint. C'est par le biais du site SharePoint que vous effectuez toutes les tâches de boîte aux lettres de site, telles que la création et la suppression de boîtes aux lettres de site. De plus, vous pouvez créer une stratégie de cycle de vie SharePoint pour gérer le cycle de vie d'une boîte aux lettres de site. Par exemple, vous pouvez créer une stratégie de cycle de vie dans SharePoint qui ferme automatiquement toutes les boîtes aux lettres de site après six mois. Si l'utilisateur souhaite encore utiliser la boîte aux lettres de site, il peut la réactiver dans SharePoint. Nous vous recommandons d'utiliser l'application Cycle de vie située dans la batterie. La suppression manuelle de boîtes aux lettres de site actives d'Exchange se traduit par des boîtes aux lettres de site orphelines. .

Quand l'application Cycle de vie dans SharePoint ferme une boîte aux lettres de site, celle-ci est conservée pendant la période indiquée dans la stratégie du cycle de vie dans l'état Fermé. La boîte aux lettres peut ensuite être réactivée par un utilisateur final ou par un administrateur à partir de SharePoint. Après la période de rétention, la boîte aux lettres de site Exchange qui est hébergée dans la base de données de boîtes aux lettres aura son nom précédé par **MDEL:**  pour indiquer qu'elle a été marquée pour suppression. Vous devrez supprimer manuellement ces boîtes aux lettres de site de la base de données de boîtes aux lettres afin de libérer de l'espace de stockage ainsi que l'alias. Si la stratégie de cycle de vie de SharePoint n’est pas activée, vous perdrez la possibilité de déterminer quelles boîtes aux lettres du site sont marquées pour la suppression. Tant qu'un administrateur n'a pas supprimé la boîte aux lettres de site, son contenu est toujours récupérable.

Vous pouvez utiliser la commande suivante pour rechercher et supprimer des boîtes aux lettres de site qui ont été marquées pour suppression.

```powershell
Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false
```

Les boîtes aux lettres de site ne prennent pas en charge la rétention au niveau de l’élément. La rétention s'applique au niveau du projet pour les boîtes aux lettres de site. Par conséquent, quand l'ensemble de la boîte aux lettres de site est supprimé, les éléments conservés le sont aussi.

## Conformité

À l'aide de la console eDiscovery (découverte électronique) dans SharePoint, les boîtes aux lettres de site peuvent être incluses dans l'étendue de la découverte électronique locale pour que vous puissiez faire des recherches par mots clés dans les boîtes aux lettres d'utilisateur ou de site. En outre, vous pouvez placer une boîte aux lettres de site en suspens pour raisons juridiques. Pour plus d'informations, consultez la rubrique [Découverte électronique locale](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).

> [!NOTE]
> Pour placer une boîte aux lettres de site en conservation légale dans Office 365, elle doit disposer d’une licence Exchange Online (Plan 2). Si une boîte aux lettres de site dispose d’une licence Exchange Online (Plan 1), vous devez lui attribuer une licence Archivage Exchange Online distincte pour la placer en conservation légale.


Fonctionnement des boîtes aux lettres de site

## Sauvegarde et restauration

La sauvegarde et la restauration des boîtes aux lettres de site Exchange hébergées sur le serveur de boîtes aux lettres utiliseront la même méthode de sauvegarde et restauration que vous utilisez pour toutes les boîtes aux lettres Exchange. Pour plus d'informations, consultez la rubrique [Groupe de disponibilité de base de données (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Pour les documents SharePoint, nous vous recommandons de sauvegarder et de restaurer dans le même emplacement. Si vous restaurez votre contenu SharePoint vers la même URL, alors la boîte aux lettres de site continuera de fonctionner et aucune configuration supplémentaire ne sera nécessaire. Si vous effectuez une restauration vers une URL différente, vous devrez alors exécuter la cmdlet **Set-SiteMailbox** pour mettre à jour la propriété *SharePointURL*. Nous vous recommandons de ne pas restaurer SharePoint vers une nouvelle forêt.

