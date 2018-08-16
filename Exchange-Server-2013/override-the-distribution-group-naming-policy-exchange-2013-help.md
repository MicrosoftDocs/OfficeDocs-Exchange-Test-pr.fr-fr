---
title: 'Ignorer la stratégie de noms des groupes de distribution: Exchange 2013 Help'
TOCTitle: Ignorer la stratégie de noms des groupes de distribution
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50477291
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ignorer la stratégie de noms des groupes de distribution

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-13_

La stratégie de noms de groupes pour les groupes de distribution est appliquée uniquement aux groupes créés par l'utilisateur. Lorsque d'autres administrateurs ou vous-même utilisez le Centre d'administration Exchange pour créer des groupes de distribution, la stratégie de noms de groupes est ignorée et n'est pas appliquée au nom de groupe.

Toutefois, si vous utilisez l'environnement de ligne de commande Exchange Management Shell pour créer ou renommer un groupe de distribution, la stratégie de noms de groupes est également appliquée aux groupes créés par les administrateurs à moins que vous n'utilisiez le paramètre *IgnoreNamingPolicy* pour remplacer la stratégie de noms de groupes.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande pour remplacer la stratégie de noms de groupes lorsque vous créez un groupe

Pour remplacer la stratégie de noms de groupes, exécutez la commande suivante.

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

Par exemple, si la stratégie de noms de groupes de votre organisation est **DG\_\<Nom de groupe\>\_Utilisateurs**, exécutez la commande suivante pour créer un groupe nommé **All Administrators**.

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Lorsque Microsoft Exchange crée ce groupe, il utilise **All Administrators** pour les paramètres *Name* et *DisplayName*.

## Utiliser l'environnement de ligne de commande pour remplacer la stratégie de noms de groupes lorsque vous renommez un groupe

Pour remplacer la stratégie de noms de groupes lorsque vous renommez un groupe existant avec l'environnement de ligne de commande, exécutez la commande suivante.

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

Imaginons que vous ayez créé une stratégie de noms de groupes un soir tard et que le lendemain matin, vous vous rendiez compte que vous avez fait une faute dans la chaîne de texte du préfixe. Le lendemain matin, vous voyez qu'un nouveau groupe a déjà été créé avec le préfixe mal orthographié. Vous pouvez corriger la stratégie de noms de groupes depuis le Centre d'administration Exchange, mais vous devez utiliser l'environnement de ligne de commande pour renommer le groupe dont le nom est mal orthographié. Exécutez la commande suivante.

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy

> [!NOTE]
> Veillez à inclure le paramètre <em>DisplayName</em> lorsque vous renommez un groupe. Si vous ne le faites pas, l'ancien nom continuera d'apparaître dans le carnet d'adresses partagé et sur les lignes À :, Cc : et De : des messages électroniques.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé ou renommé un groupe de distribution qui ignore la stratégie de noms de groupes, exécutez les commandes suivantes.

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

Si le format du nom d'affichage du groupe est différent de celui mis en application par la stratégie de noms de groupes de votre organisation, vous avez réussi.

