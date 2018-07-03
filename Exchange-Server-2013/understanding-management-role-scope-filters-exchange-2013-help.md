---
title: 'Présentation des filtres d’attribution du rôle de gestion: Exchange 2013 Help'
TOCTitle: Présentation des filtres d’attribution du rôle de gestion
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50478372
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation des filtres d’attribution du rôle de gestion

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les filtres de l’étendue du rôle de gestion servent à définir des étendues de gestion personnalisables. Les filtres d’étendue vous permettent de créer une étendue correspondant à la manière dont vous segmentez vos destinataires, bases de données et serveurs pour que les administrateurs gèrent uniquement les objets auxquels ils doivent accéder. Les filtres d’étendue de gestion peuvent utiliser presque toutes les propriétés d’objet destinataire, base de données ou serveur.

Pour utiliser ces filtres, vous devez bien connaître les étendues du rôle de gestion. Pour plus d’informations sur les étendues de rôle de gestion, consultez la rubrique [Présentation des portées du rôle de gestion](understanding-management-role-scopes-exchange-2013-help.md).

Les étendues filtrées personnalisées dans Microsoft Exchange Server 2013 sont créées à l’aide de la cmdlet **New-ManagementScope**. Les deux types d’étendue filtrée, destinataire et configuration (qui se compose d’étendues de serveur et de base de données), sont subdivisées en catégories normale et exclusive. La liste suivante présente quel paramètre de la cmdlet **New-ManagementScope** sert à créer chaque type d’étendue filtrée :

  - **Étendue filtrée destinataire - normale**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *RecipientRestrictionFilter*.

  - **Étendue filtrée destinataire de type - exclusive**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *RecipientRestrictionFilter* associé au commutateur *Exclusive*.

  - **Étendue filtrée de configuration basée sur serveur - normale**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *ServerRestrictionFilter*.

  - **Étendue filtrée de configuration basée sur serveur - exclusive**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *ServerRestrictionFilter* associé au commutateur *Exclusive*.

  - **Étendue filtrée de configuration basée sur base de données - normale**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *DatabaseRestrictionFilter*.

  - **Étendue filtrée de configuration basée sur base de données - exclusive**   Pour créer ce type d’étendue filtrée, utilisez le paramètre *DatabaseRestrictionFilter* associé au commutateur *Exclusive*.

Lorsque vous créez une étendue filtrée personnalisée, l’étendue tente de faire correspondre le filtre avec les objets accessibles dans la portée de lecture implicite du rôle de gestion. Tout objet trouvé est inclus dans les résultats de la recherche du filtre et l’objet est mis à la disposition du rôle de gestion par l’étendue personnalisée. Un filtre ne peut pas retourner des résultats qui ne font pas partie de la portée de lecture implicite du rôle de gestion.

Si vous utilisez le paramètre *RecipientRestrictionFilter* pour spécifier un filtre destinataire, vous pouvez utiliser le paramètre *RecipientRoot* pour spécifier une unité d’organisation à laquelle sera limité le filtre. Lorsque vous spécifiez une unité d’organisation dans le paramètre *RecipientRoot*, le filtre destinataire tente de trouver une correspondance uniquement avec les destinataires résidant dans cette unité d’organisation au lieu d’effectuer la recherche sur l’ensemble de la portée de lecture implicite.

Pour créer une étendue de gestion à l’aide des propriétés filtrables présentées dans cette rubrique, voir [Créer une étendue normale ou exclusive](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Syntaxe de filtre

Les filtres de destinataire et de configuration emploient la même syntaxe pour créer une requête de filtre. Toutes les requêtes de filtre doivent avoir au minimum les composants suivants :

  - **Accolade ouvrante**   L’accolade ouvrante ({) indique le début de la requête de filtre.

  - **Propriété à examiner**   La propriété est la valeur d’un objet que vous voulez tester. Ce peut être, par exemple, la ville ou le service d’un objet destinataire, un nom de site Active Directory, un nom de serveur d’un objet de configuration, ou un nom de base de données d’un objet de configuration de base de données.

  - **Opérateur de comparaison**   L’opérateur de comparaison indique comment la requête doit évaluer la valeur que vous spécifiez par rapport à la valeur stockée dans la propriété. Les opérateurs de comparaison sont par exemple **Eq** (égal à), **Ne** (différent de), **Like** (similaire à), etc. Pour obtenir la liste complète des opérateurs de comparaison utilisables dans l’environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Opérateurs de comparaison](https://technet.microsoft.com/fr-fr/library/bb125229\(v=exchg.150\)).

  - **Valeur à comparer**   La valeur que vous spécifiez dans la requête de filtre sera comparée à la valeur stockée dans la propriété spécifiée. La valeur spécifiée doit être placée entre guillemets ("). Pour spécifier une chaîne partielle, placez-la entre des caractères génériques (\*) et utilisez un opérateur de comparaison qui accepte les caractères génériques (par exemple, **Like**). N’importe quelle chaîne qui contient la chaîne partielle correspondra à la requête de filtre.

  - **Accolade fermante**   L’accolade fermante (}) indique la fin de la requête de filtre.

Les composants suivants sont disponibles en option et vous permettent de créer des requêtes de filtre plus complexes :

  - **Parenthèses**   Comme en mathématiques, les parenthèses, ( ), contenues dans une requête de filtre vous permettent d’imposer l’ordre dans lequel l’opération est effectuée. La requête de filtre commence par évaluer les parenthèses les plus intérieures, puis passe aux parenthèses les plus extérieures.

  - **Opérateurs logiques**   Les opérateurs logiques relient une ou plusieurs opérations de comparaison et obligent la requête de filtre à évaluer l’instruction complète. Par exemple, les opérateurs logiques incluent **And**, **Or** et **Not**.

Une fois les éléments rassemblés, une requête simple ressemble à `{ City -Eq "Vancouver" }`. Ce filtre établit la correspondance avec tous les destinataires dont la propriété **City** à une valeur égale à la chaîne « Vancouver ».

Une autre requête plus complexe est `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`. La requête de filtre est évaluée dans l’ordre suivant :

1.  Les propriétés **City** et **Department** sont évaluées. Chacune est définie sur `True` ou sur `False` en fonction des valeurs stockées dans chaque propriété.

2.  Les résultats des instructions **City** et **Department** sont ensuite évalués. Si les deux sont `True`, l’instruction complète **And** devient `True`. Si une ou les deux sont `False`, l’instruction complète **And** devient `False`. Les principes suivants s’appliquent :
    
      - Si l’instruction **And** est évaluée comme `True`, la requête de filtre complète devient `True` puisque l’opérateur **Or** indique qu’un des deux éléments de la requête doit être `True`. L’objet est exposé à l’attribution de rôle.
    
      - Si l’instruction **And** est `False`, la requête de filtre poursuit l’évaluation de la propriété **Title**.

3.  La propriété **Title** est ensuite évaluée. Elle est définie sur `True` ou `False` en fonction de la valeur stockée dans la propriété **Title**. Les principes suivants s’appliquent :
    
      - Si la propriété **Title** est évaluée comme `True`, la requête de filtre complète devient `True` puisque l’opérateur **Or** indique qu’un des deux éléments de la requête doit être `True`. L’objet est exposé à l’attribution de rôle.
    
      - Si la propriété **Title** est évaluée comme `False`, la requête de filtre complète est évaluée comme `False`, et l’objet n’est pas exposé à l’attribution de rôle.

Le tableau suivant présente un exemple avec des valeurs indiquant quand la requête complexe serait évaluée comme `True` ou `False`.

### Requête complexe

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ville</th>
<th>Service</th>
<th>Titre</th>
<th>Résultat</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Ventes (True)</p></td>
<td><p>Directeur général (False)</p></td>
<td><p>True car les propriétés <strong>City</strong> et <strong>Department</strong> sont évaluées comme True. La propriété <strong>Title</strong> n’est pas évaluée car les conditions de requête de filtre sont déjà remplies.</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Ventes (True)</p></td>
<td><p>Responsable informatique (True)</p></td>
<td><p>True, car <strong>Title</strong> est évalué comme True. Les résultats de la comparaison entre <strong>City</strong> et <strong>Department</strong> sont ignorés parce que <strong>Title</strong> est évalué comme True et remplit donc les conditions de requête de filtre.</p>
> [!NOTE]
> Le Responsable informatique est conforme à la requête de filtre puisque l’opérateur de comparaison <strong>Like</strong> a été utilisé et offre une correspondance avec des chaînes partielles lorsque les caractères génériques (*) sont utilisés dans la requête de filtre.

</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Rédacteur (False)</p></td>
<td><p>False parce que <strong>City</strong> et <strong>Department</strong> ne sont pas évalués comme True, et <strong>Title</strong> n’a pas non plus été évalué comme True.</p></td>
</tr>
</tbody>
</table>


## Propriétés filtrables du destinataire

Presque toutes les propriétés d’un objet destinataire peuvent être utilisées pour créer un filtre destinataire. Pour obtenir la liste des propriétés filtrables, consultez la rubrique [Propriétés filtrables pour le paramètre -RecipientFilter](https://technet.microsoft.com/fr-fr/library/bb738157\(v=exchg.150\)). Bien que cette rubrique porte sur les propriétés pouvant être utilisées avec le paramètre *RecipientFilter* sur d’autres cmdlets, la plupart de ces propriétés fonctionnent aussi avec le paramètre *RecipientRestrictionFilter* de la cmdlet **New-ManagementScope**.

## Propriétés filtrables du serveur

Les propriétés de serveur suivantes peuvent être utilisées pour créer une étendue de gestion avec le paramètre *ServerRestrictionFilter* :

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## Propriétés filtrables de base de données

Les propriétés de base de données suivantes peuvent être utilisées pour créer une étendue de gestion avec le paramètre *DatabaseRestrictionFilter* :

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

