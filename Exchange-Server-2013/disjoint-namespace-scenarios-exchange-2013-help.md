---
title: 'Scénarios d’espace de noms disjoint: Exchange 2013 Help'
TOCTitle: Scénarios d’espace de noms disjoint
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50478688
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Scénarios d’espace de noms disjoint

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Cette rubrique contient des informations sur le concept des espaces de noms disjoints et les scénarios pris en charge pour déployer Microsoft Exchange 2013 dans un domaine contenant un espace de noms disjoint.

**Contenu de cette rubrique**

Noms de domaine DNS et NetBIOS

Espaces de noms disjoints

Exchange 2013 et espaces de noms disjoints

Autorisation des serveurs Exchange 2013 à accéder à des contrôleurs de domaine disjoints

Afficher des informations relatives aux noms DNS et NetBIOS d’un ordinateur qui exécute Windows Server 2008

## Noms de domaine DNS et NetBIOS

Tout d’abord, quelques notions. Chaque ordinateur connecté à Internet possède un nom DNS (Domain Name System). également appelé *nom d’ordinateur* ou *nom d’hôte*. Tous les ordinateurs qui exécutent le système d’exploitation Microsoft Windows avec des capacités réseau possède également un nom NetBIOS.

Un ordinateur qui exécute Windows dans un domaine Active Directory possède un nom de domaine DNS et un nom de domaine NetBIOS:

  - **Nom de domaine DNS**   Le nom de domaine DNS comprend un ou plusieurs sous-domaines séparés par un point (**.**) et se termine par un nom de domaine de niveau supérieur. Par exemple, dans le nom de domaine DNS corp.contoso.com, les sous-domaines sont corp et contoso, et le nom de domaine de niveau supérieur est com.

  - **Nom de domaines NetBIOS**   Généralement, le nom de domaine NetBIOS est le sous-domaine du nom de domaine DNS. Par exemple, si le nom de domaine DNS est contoso.com, le nom de domaine NetBIOS est contoso. Si le nom de domaine DNS est corp.contoso.com, le nom de domaine NetBIOS est corp.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour rechercher des informations DNS et NetBIOS pour des ordinateurs qui exécutent Windows Server 2008, consultez la rubrique Afficher des informations relatives aux noms DNS et NetBIOS d’un ordinateur qui exécute Windows Server 2008.</td>
</tr>
</tbody>
</table>


Un ordinateur dans un domaine Active Directory possède également un suffixe DNS principal et peut avoir des suffixes DNS supplémentaires. Par défaut, le suffixe DNS principal est identique au nom de domaine DNS. Pour des instructions détaillées sur la modification du suffixe DNS principal, reportez-vous aux procédures décrites plus loin dans cette rubrique.

Vous définissez les noms de domaine DNS et NetBIOS d’un domaine Active Directory lorsque vous configurez le premier contrôleur de domaine dans le domaine. Pour plus d’informations sur la configuration des contrôleurs de domaine, voir [Rôles des contrôleurs de domaine](https://go.microsoft.com/fwlink/p/?linkid=268367) et [Présentation des services de domaine Active Directory](https://go.microsoft.com/fwlink/p/?linkid=268366).

## Espaces de noms disjoints

Dans la plupart des topologies de domaine, le suffixe DNS principal des ordinateurs du domaine est identique au nom de domaine DNS.

Dans certains cas, vous pouvez avoir des espaces de noms différents. C’est ce qu’on appelle un *espace de noms disjoint*. Par exemple, une fusion ou acquisition peut nécessiter une topologie avec un espace de noms disjoint. En outre, si la gestion du serveur DNS de votre société est répartie entre des administrateurs gérant Active Directory et des administrateurs gérant des réseaux, vous aurez peut-être une topologie avec un espace de noms disjoint.

Un espace de noms disjoint est le scénario dans lequel le suffixe DNS principal d’un ordinateur ne correspond pas au nom de domaine DNS dans lequel réside l’ordinateur. L’ordinateur dont le suffixe DNS principal ne correspond pas est désigné comme *disjoint*. Autre scénario d’espace de noms disjoint : le nom de domaine NetBIOS d’un contrôleur de domaine ne correspond pas au nom de domaine DNS.

## Exchange 2013 et espaces de noms disjoints

Exchange 2013 prend en charge les trois scénarios suivants pour le déploiement de Microsoft Exchange dans un domaine ayant un espace de noms disjoint :

  - **Le suffixe DNS principal et le nom de domaine DNS sont différents**   Le suffixe DNS principal du contrôleur de domaine est différent du nom de domaine DNS. Les ordinateurs appartenant ou non au domaine peuvent être disjoints ou non.

  - **L’ordinateur membre est disjoint**   Un ordinateur membre d’un domaine Active Directory est disjoint, même si le contrôleur de domaine n’est pas disjoint.

  - **Le nom NetBIOS d’un contrôleur de domaine diffère du sous-domaine de son nom de domaine DNS**   Le nom de domaine NetBIOS du contrôleur de domaine est différent du sous-domaine du nom de domaine DNS de ce contrôleur de domaine.

Ces scénarios sont détaillés dans les sections suivantes.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il est accepté d’exécuter Exchange 2013 selon les scénarios d’espaces de noms disjoints décrits dans cette rubrique. Cependant, si vous êtes confronté à un scénario d’espaces de noms disjoints différent des scénarios décrits dans cette rubrique, vous devez utiliser les services Microsoft pour déployer Exchange 2013. Pour plus d’informations, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=94845">Services Microsoft</a>.</td>
</tr>
</tbody>
</table>


## Scénario : Le suffixe DNS principal et le nom de domaine DNS sont différents

Dans ce scénario, le suffixe DNS principal du contrôleur de domaine est différent du nom de domaine DNS. Dans ce scénario, le contrôleur de domaine est disjoint. Les ordinateurs appartenant au domaine, notamment les serveurs Exchange et les ordinateurs clients Microsoft Outlook, peuvent avoir un suffixe DNS principal qui correspond au suffixe DNS principal du contrôleur de domaine ou au nom de domaine DNS.

## Scénario : L'ordinateur membre est disjoint

Dans ce scénario, le suffixe DNS principal d’un ordinateur membre sur lequel Exchange 2013 est installé est différent du nom de domaine DNS, bien que le suffixe DNS principal du contrôleur de domaine soit identique au nom de domaine DNS. Dans ce scénario, il existe un contrôleur de domaine non disjoint et un ordinateur membre disjoint. Les ordinateurs membres exécutant Outlook peuvent avoir un suffixe DNS principal qui correspond au suffixe DNS principal du serveur Exchange disjoint ou au nom de domaine DNS.

## Scénario : Le nom NetBIOS du contrôleur de domaine diffère du sous-domaine de son nom de domaine DNS

Dans ce scénario, le nom de domaine NetBIOS du contrôleur de domaine est différent du nom de domaine DNS de ce même contrôleur de domaine.

**Le nom de domaine NetBIOS ne correspond pas au nom de domaine DNS**

![Le nom de domaine NetBIOS ne correspond pas au nom de domaine DNS](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "Le nom de domaine NetBIOS ne correspond pas au nom de domaine DNS")

## Autorisation des serveurs Exchange 2013 à accéder à des contrôleurs de domaine disjoints

Pour permettre aux serveurs Exchange 2013 d’accéder à des contrôleurs de domaine disjoints, vous devez modifier l’attribut **msDS-AllowedDNSSuffixes**Active Directory sur le conteneur d’objet de domaine. Vous devez ajouter les deux suffixes DNS à l’attribut. Pour la procédure détaillée de modification de l’attribut, consultez la page [Le suffixe DNS principal de l’ordinateur ne correspond pas au nom de domaine complet du domaine sur lequel il réside](https://go.microsoft.com/fwlink/p/?linkid=98848).

En outre, pour vous assurer que la liste de recherche de suffixe DNS contient tous les espaces de noms DNS déployés au sein de l’organisation, vous devez configurer la liste de recherche pour chaque ordinateur dans le domaine disjoint. La liste d’espaces de noms doit non seulement inclure le suffixe DNS principal du contrôleur de domaine et le nom de domaine DNS, mais également les espaces de noms supplémentaires pour les autres serveurs avec lesquels Exchange est susceptible d’interagir (tels que des serveurs de surveillance ou des serveurs pour applications tierces). Pour ce faire, définissez la stratégie de groupe pour le domaine. Pour plus d’informations sur la stratégie de groupe, consultez les rubriques suivantes :

  - [Forum aux questions (FAQ) à propos des stratégies de groupe](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Nouvelles stratégies de groupe pour DNS dans Windows Server 2003](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=294785)

  - [Stratégie de groupe](https://go.microsoft.com/fwlink/p/?linkid=268043)

Pour obtenir la procédure détaillée de configuration de la stratégie de groupe de la liste de recherche de suffixe DNS, consultez la rubrique [Configuration d’une liste de recherche de suffixe DNS pour un espace de noms disjoint](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md).

## Afficher des informations relatives aux noms DNS et NetBIOS d’un ordinateur qui exécute Windows Server 2008

1.  Cliquez sur **Démarrer**, cliquez avec le bouton droit sur **Ordinateur**, puis cliquez sur **Propriétés**.

2.  Sous **Système**, le nom d’hôte DNS et le suffixe DNS principal s’affichent sous **Paramètres de nom d’ordinateur, de domaine et de groupe de travail**, en regard de **Nom complet de l’ordinateur**. Le nom de domaine DNS s’affiche en regard de **Domaine**.

3.  Cliquez sur **Modifier les paramètres**.

4.  Sous **Propriétés du système**, sous l’onglet **Nom de l’ordinateur**, cliquez sur **Modifier**.

5.  Sous **Modification du nom ou du domaine de l’ordinateur**, cliquez sur **Plus**. Le suffixe DNS principal s’affiche sous **Suffixe DNS principal de cet ordinateur**. Le nom d’ordinateur NetBIOS s’affiche en regard de **Nom NetBIOS de l’ordinateur**.
    
    Pour modifier le suffixe DNS principal, entrez le nouveau suffixe DNS principal sous **Suffixe DNS principal de cet ordinateur**, puis cliquez sur **OK**.

6.  À partir de la fenêtre d’invite de commandes, tapez **set**. La variable USERDNSDOMAIN affiche le nom de domaine DNS. La variable USERDNSDOMAIN affiche le nom de domaine NetBIOS.

