---
title: 'Gestion des stratégies de config. des BAL de site: Exchange 2013 Help'
TOCTitle: Gestion des stratégies de configuration des boîtes aux lettres de site
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50477799
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des stratégies de configuration des boîtes aux lettres de site

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-21_

Les stratégies de mise en service des boîtes aux lettres de site s'appliquent uniquement aux messages électroniques envoyés à la boîte aux lettres de site ou à partir de celle-ci, ainsi qu'à la taille de la boîte aux lettres de site sur le serveur Exchange.

Pour plus d'informations sur les boîtes aux lettres de site, consultez la rubrique [Boîtes aux lettres de site](site-mailboxes-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Boîtes aux lettres de site » dans la rubrique [Autorisations de partage et de collaboration](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Bien que vous puissiez créer plusieurs stratégies de mise en service de boîtes aux lettres de site, seule la stratégie de mise en service par défaut est appliquée à toutes les boîtes aux lettres de site. Vous ne pouvez pas appliquer plusieurs stratégies dans votre organisation.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer une stratégie de mise en service de boîte aux lettres de site

Cet exemple permet de créer la stratégie de mise en service par défaut SM\_ProvisioningPolicy avec les paramètres suivants :

  - Le quota d'avertissement pour les boîtes aux lettres de site est de 9 Go.

  - Les boîtes aux lettres de site sont interdites depuis les messages de réception lorsque la taille de la boîte aux lettres atteint 10 Go.

  - La taille maximale des messages électroniques pouvant être envoyés vers les boîtes aux lettres de site est de 50 Mo.

<!-- end list -->

    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB

## Afficher les paramètres d'une stratégie de mise en service de boîte aux lettres de site

Cet exemple renvoie des informations détaillées sur toutes les stratégies de mise en service de boîtes aux lettres de site de votre organisation.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List
```

Cet exemple renvoie toutes les stratégies de votre organisation, mais n'affiche que les informations `IsDefault` pour identifier la stratégie par défaut.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List IsDefault
```

## Apporter des modifications à une stratégie de mise en service de boîte aux lettres de site existante

Cet exemple modifie la stratégie d'approvisionnement de boîte aux lettres de site nommée par défaut pour permettre la réception des messages électroniques d'une taille maximale de 25 Mo par la boîte aux lettres de site. (Quand vous installez Exchange, une stratégie de mise en service est créée avec le nom **Par défaut**.)

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB
```

Cet exemple modifie le quota d'avertissement à 9,5 Go et le quota d'interdiction d'envoi et de réception à 10 Go.

    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB

## Configurer le préfixe du nom d'une boîte aux lettres de site

Par défaut, lors de la création d'une boîte aux lettres de site, un préfixe est attribué l'adresse de messagerie de cette dernière. Le préfixe vous permet de rechercher et d'interroger facilement des boîtes aux lettres de site et permet également aux utilisateurs de reconnaître ces dernières. Vous pouvez choisir de désactiver le préfixe ou de modifier celui-ci pour votre client dans Office 365 ou pour une forêt donnée dans un déploiement local. Avec le comportement de préfixe par défaut, si votre boîte aux lettres de site a été créée dans Office 365, le préfixe par défaut est **SMO-**. Autrement, si votre boîte aux lettres de site a été créée dans votre déploiement local, le préfixe est **SM-**. Le comportement par défaut est différent entre ces scénarios de déploiement afin que les clients hybrides ne rencontrent pas de conflits si les boîtes aux lettres ont été créées dans les deux emplacements et sont synchronisées inter-site.

Cet exemple permet de désactiver l'attribution de préfixe en définissant le paramètre *DefaultAliasPrefixEnabled* sur $false.

    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null

Cet exemple permet de modifier la stratégie de mise en service par défaut et de définir le paramètre *AliasPrefix* sur FOREST01.

> [!NOTE]
> Pour des déploiements à plusieurs forêts, nous vous recommandons d'utiliser un préfixe différent dans chaque forêt afin d'éviter les conflits lors de la synchronisation d'objets entre forêts, dans l'éventualité ou les boîtes aux lettres de site auraient été créées avec des noms identiques dans deux forêts ou plus.


    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false

> [!NOTE]
> Dans le cas d'un déploiement hybride où Exchange est installé en local et dans Office 365, toutes les boîtes aux lettres de site en nuage sont créées avec le préfixe <strong>SMO-</strong>. Les préfixes sont différents dans Office 365 et dans Exchange en local afin que les clients hybrides ne rencontrent pas de conflits si les boîtes aux lettres sont créées dans les deux emplacements et sont synchronisées inter-site. Le paramètre AliasPrefix a la priorité sur le paramètre DefaultAliasPrefixEnabled. Par conséquent, si le paramètre <em>AliasPrefix</em> est défini sur une chaîne valide non Null, cette chaîne est ajoutée devant l'alias de chaque nouvelle boîte aux lettres de site.


## Supprimer une stratégie de mise en service de boîte aux lettres de site

Cet exemple supprime la stratégie de boîte aux lettres de site par défaut créée lors de l'installation d'Exchange.

```powershell
Remove-SiteMailboxProvisioningPolicy -Identity Default
```

> [!IMPORTANT]
> Vous devez commencer par créer et désigner une autre stratégie par défaut avant de pouvoir supprimer la stratégie <strong>Par défaut</strong>.


## Pour plus d'informations

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/fr-fr/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/fr-fr/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/fr-fr/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/fr-fr/library/jj218672\(v=exchg.150\))

