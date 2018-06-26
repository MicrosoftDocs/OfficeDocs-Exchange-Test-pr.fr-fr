---
title: 'Configurer IRM pour la recherche et la découverte locale dans Exchange: Exchange 2013 Help'
TOCTitle: Configurer IRM pour la recherche et la découverte locale dans Exchange
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50479320
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer IRM pour la recherche et la découverte locale dans Exchange

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-16_

Dans Microsoft Exchange Server 2013, vous pouvez configurer la gestion des droits relatifs à l’information (IRM) afin que le service de recherche Exchange puisse indexer les messages protégés par IRM.

Lorsque les membres du groupe de rôles Gestion de la découverte effectuent une recherche [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md), les messages protégés par IRM sont renvoyés dans les résultats de recherche et copiés dans la boîte aux lettres de découverte indiquée dans la recherche. En outre, les membres du groupe de rôles Gestion de la découverte peuvent utiliser Outlook Web App pour accéder aux messages protégés par IRM qui ont été copiés dans la boîte aux lettres de découverte à la suite de l’opération de détection.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les membres du groupe de rôles Gestion de la découverte ne peuvent pas accéder aux messages protégés par IRM qui ont été exportés d’une boîte aux lettres de découverte vers une autre boîte aux lettres ou vers un fichier .pst. Les messages protégés par IRM dans une boîte aux lettres de découverte sont accessibles uniquement à l’aide d’Outlook Web App.</td>
</tr>
</tbody>
</table>


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - La gestion des droits relatifs à l’information (IRM) doit être configurée dans votre organisation Exchange 2013. Pour plus d’informations, voir [Activer ou désactiver la technologie IRM pour les messages internes](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - La boîte aux lettres de fédération doit être ajoutée au groupe de super utilisateurs AD RMS (Active Directory Rights Management Services). Pour plus d’informations, voir [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’Administration Exchange pour configurer IRM pour les fonctions de recherche et de découverte électronique locale Exchange. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

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

## Utiliser l’environnement Shell pour configurer IRM pour le service de recherche Exchange

Cet exemple configure IRM afin d’autoriser le service de recherche Exchange à indexer les messages protégés par IRM.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, le paramètre <em>SearchEnabled</em> est défini sur <code>$true</code>. Pour désactiver l’indexation des messages protégés par IRM, définissez-le sur <code>$false</code>. La désactivation de l’indexation des messages protégés par IRM les empêche d’apparaître dans les résultats de recherche lorsque les utilisateurs effectuent une recherche dans leur boîte aux lettres ou lorsque les gestionnaires de découverte utilisent la fonction de découverte électronique locale.</td>
</tr>
</tbody>
</table>


    Set-IRMConfiguration -SearchEnabled $true

Pour des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour configurer IRM pour la découverte électronique locale

Dans cet exemple, nous activons des membres du groupe de rôles Gestion de la découverte pour accéder aux messages protégés par IRM qui se trouvent dans la boîte aux lettres de découverte.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, le paramètre <em>EDiscoverySuperUserEnabled</em> est défini sur <code>$true</code>. Pour désactiver l’accès aux messages protégés par IRM pour les membres du groupe de rôles Gestion de la découverte, définissez-le sur <code>$false</code>.</td>
</tr>
</tbody>
</table>


    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

Pour des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré IRM pour la recherche et la découverte électronique locale, utilisez la cmdlet **Get-IRMConfigurtaion** pour extraire les informations sur la configuration d’IRM. Pour un exemple de la façon de récupérer la configuration IRM, voir [Examples](https://technet.microsoft.com/fr-fr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) dans **Get-IRMConfiguration**.

