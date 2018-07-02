---
title: 'Configurer les paramètres de routage de messagerie Exchange dans Active Directory: Exchange 2013 Help'
TOCTitle: Configurer les paramètres de routage de messagerie Exchange dans Active Directory
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50479267
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les paramètres de routage de messagerie Exchange dans Active Directory

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Par défaut, Microsoft Exchange Server 2013 fait référence aux objets de lien de site IP dans Active Directory pour faciliter l’identification du chemin de routage le moins coûteux. Cependant, si vous constatez que les coûts propres aux liens de sites IP et les schémas de flux de trafic Active Directory ne sont pas optimaux pour le routage de la messagerie dans Exchange, vous pouvez configurer les paramètres d’Active Directory qui sont uniquement utilisés par Exchange pour faciliter l’optimisation du flux de messagerie.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « site Active Directory et gestion des liens de ce site » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour configurer un coût spécifique à Exchange sur un lien de site IP Active Directory

Déterminez le nom du lien de site IP Active Directory pour lequel vous voulez définir un coût Exchange. Une valeur de coût inférieure indique un chemin de routage favori. Vous pouvez examiner le contenu des journaux de la table de routage et consulter les données de la section **ADTopologyPath ID** pour afficher les détails relatifs au chemin de routage le moins coûteux calculé entre deux sites Active Directory.

Pour définir un coût spécifique à Exchange sur un lien de site Active Directory, exécutez la commande suivante :

``` 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

Dans cet exemple, un coût spécifique à Exchange de 10 est défini sur le lien de site IP nommé IPSiteLinkAB.

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10

Cet exemple montre comment effacer le coût spécifique à Exchange du lien de site IP nommé IPSiteLinkAB.

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini un coût Exchange sur un lien de site Active Directory, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-AdSiteLink | Format-List Name,ExchangeCost

2.  Vérifiez que le coût Exchange est configuré sur le lien de site Active Directory.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer un site Active Directory comme site hub

Lorsqu’un site hub existe sur le chemin de routage le moins coûteux pour un message, ce dernier doit être acheminé via le site hub. Examinez le contenu des journaux de la table de routage et consultez les données de la section **ADTopologyPath ID** pour vérifier que le site sélectionné existe sur le chemin de routage le moins coûteux entre deux sites Active Directory. Si ce n’est pas le cas, vous devez affecter des coûts spécifiques à Exchange aux liens de sites IP de sorte que le chemin de routage le moins coûteux passe par les sites sélectionnés.

Pour configurer un site Active Directory en tant que site hub, exécutez la commande suivante :

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

Dans cet exemple, le site Active Directory nommé site A est configuré comme un site hub.

    Set-AdSite "Site A" -HubSiteEnabled $true

Cet exemple montre comment supprimer l’attribut de site hub du site Active Directory nommé site B.

    Set-AdSite "Site B" -HubSiteEnabled $false

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré un site Active Directory en tant que site hub, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-AdSite | Format-List Name,HubSiteEnabled

2.  Vérifiez que la valeur de *HubSiteEnabled* est `True` pour le site Active Directory.

