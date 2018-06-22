---
title: 'Autorisations dans les déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Autorisations dans les déploiements hybrides Exchange
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51406945
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorisations dans les déploiements hybrides Exchange

 

_<strong>Sapplique à :</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2018-05-02_

L’organisation Exchange Online dans Office 365 est basée sur Exchange Server et, comme les organisations locales, elle utilise le contrôle d’accès en fonction du rôle (RBAC) pour contrôler les autorisations. Les administrateurs disposent des autorisations d’utilisation des groupes de rôles de gestion alors que les utilisateurs finaux disposent des autorisations d’utilisation des stratégies d’attribution de rôle de gestion.

Pour en savoir plus sur les autorisations dans Exchange Online et Exchange sur site, consultez la ressource : [Autorisations](https://technet.microsoft.com/fr-fr/library/dd351175\(v=exchg.150\))

## Autorisations d'administrateur

Par défaut, l’utilisateur utilisé pour créer le client Office 365 devient membre du groupe de rôles Gestion de l’organisation dans l’organisation Exchange Online. Cet utilisateur peut gérer toute l’organisation Exchange Online, y compris la configuration des paramètres d’organisation et la gestion des destinataires Exchange Online.

Vous pouvez ajouter des administrateurs supplémentaires dans l'organisation Exchange Online, selon le type de gestion à mettre en place. Par exemple, vous pouvez ajouter des administrateurs d'organisation et de destinataires supplémentaires, permettre aux utilisateurs spécialistes d'effectuer des tâches de conformité telles que la détection, configurer des autorisations personnalisées et davantage. La gestion de toutes les autorisations Exchange Online pour les administrateurs Office 365 doit être effectuée dans l'organisation Exchange Online à l'aide du Centre d'administration Exchange (CAE) ou Remote PowerShell.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il n'existe pas de transfert d'autorisations entre l'organisation locale et l'organisation Office 365. Les autorisations que vous avez définies dans l'organisation locale doivent être recréées dans l'organisation Office 365.</td>
</tr>
</tbody>
</table>


Pour plus d'informations, consultez les rubriques [Gérer des groupes de rôles](https://technet.microsoft.com/fr-fr/library/jj657480\(v=exchg.150\)) et [Gérer les membres de groupes de rôles](https://technet.microsoft.com/fr-fr/library/jj657492\(v=exchg.150\)).

## Octroi d’autorisations de boîte aux lettres à des délégués

Dans les déploiements d’Exchange sur site, les utilisateurs peuvent être accordées à une variété d’autorisations aux boîtes aux lettres d’autres utilisateurs. On parle alors des autorisations de boîte aux lettres déléguées et ses utile lorsqu’un assistant administratif doit gérer une partie de la boîte aux lettres d’un autre utilisateurs. par exemple, gérer le calendrier d’un cadre. Déploiements Exchange hybride prend en charge l’utilisation des autorisations de boîte aux lettres de certains, mais pas toutes, entre les boîtes aux lettres que qui se trouve dans une organisation d’Exchange sur place et des boîtes aux lettres situées dans Office 365. Les sections suivantes détaillent l’autorisation sont et ne sont pas pris en charge ; configuration supplémentaire requise pour prendre en charge les autorisations de boîte aux lettres hybride ; et comment les autorisations de boîte aux lettres sont synchronisées entre votre organisation sur place et l’Office 365.

## Autorisations de boîtes aux lettres prises en charge dans des environnements hybrides

Les autorisations suivantes **sont** prises en charge :

  - **Accès total** Il est possible d’octroyer à une boîte aux lettres se trouvant sur un serveur Exchange local l’autorisation **Accès total** à une boîte aux lettres Office 365, et inversement. Par exemple, il est possible d’octroyer à une boîte aux lettres Office 365 l’autorisation **Accès total** à une boîte aux lettres partagée locale. Les utilisateurs doivent ouvrir leur boîte aux lettres à l’aide du client de bureau Outlook. Les autorisations de boîtes aux lettres déléguées ne sont pas prises en charge dans Outlook sur le web.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les utilisateurs peuvent être invités à entrer des informations d’identification supplémentaires lorsqu’ils accèdent pour la première fois à une boîte aux lettres qui se trouve dans l’autre organisation et l’ajoutent à leur profil Outlook.</td>
    </tr>
    </tbody>
    </table>


  - **Envoyer de la part de** Il est possible d’octroyer à une boîte aux lettres se trouvant sur un serveur Exchange local l’autorisation **Envoyer de la part de** à une boîte aux lettres Office 365, et inversement. Par exemple, il est possible d’octroyer à une boîte aux lettres Office 365 l’autorisation **Envoyer de la part de** à une boîte aux lettres partagée locale. Les utilisateurs doivent ouvrir leur boîte aux lettres à l’aide du client de bureau Outlook. Les autorisations de boîtes aux lettres déléguées ne sont pas prises en charge dans Outlook sur le web.
    
    Certains changements sur votre serveur Azure Active Directory Connect sont nécessaires pour que les autorisations Envoyer de la part de se synchronisent entre vos serveurs Exchange locaux et Exchange Online. Pour plus d’informations, consultez la section Activation de la prise en charge des autorisations de boîtes aux lettres hybrides dans Azure Active Directory Connect plus loin dans cette rubrique.

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **Éléments privés** Lors de l’ajout d’un délégué, l’option peut être configurée pour autoriser un utilisateur avec des autorisations de dossier pour afficher les éléments de calendrier privés.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>À partir de février 2018 la fonctionnalité prise en charge d’un accès complet, envoyer sur place et dossier droits entre forêts est déployée et devrait être terminé en avril 2018.</td>
</tr>
</tbody>
</table>


Les autorisations ou fonctionnalités suivantes **ne sont pas** prises en charge :

  - **Send-As** Permet à un utilisateur d’envoyer du courrier comme s’il provenait de la boîte aux lettres d’un autre utilisateur.

  - **Mappage automatique** Permet à Outlook, lors de son démarrage, d’ouvrir automatiquement des boîtes aux lettres pour lesquelles un utilisateur a reçu l’autorisation **Accès total**.

Les boîtes aux lettres qui reçoivent ces autorisations à partir d’une autre boîte aux lettres doivent être déplacées en même temps que cette boîte aux lettres. Si une boîte aux lettres reçoit des autorisations à partir de plusieurs boîtes aux lettres, cette boîte aux lettres et toutes les boîtes aux lettres lui octroyant des autorisations doivent être déplacées simultanément.

## Configurer vos serveurs Exchange locaux pour prendre en charge les autorisations de boîtes aux lettres hybrides

Pour activer les autorisations Accès total et Envoyer de la part de dans un déploiement hybride, des modifications supplémentaires de la configuration peuvent être nécessaires en fonction de la version d’Exchange que vous avez installée. Le tableau suivant indique quelles versions d’Exchange prennent en charge les autorisations de boîtes aux lettres déléguées dans un déploiement hybride avec Office 365 et quelle configuration supplémentaire est nécessaire. Pour savoir comment configurer les serveurs et boîtes aux lettres Exchange 2013 et 2010 pour prendre en charge des listes de contrôle d’accès (ACL), consultez la rubrique [Configurer Exchange pour prendre en charge des autorisations de boîtes aux lettres déléguées dans un déploiement hybride](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Exchange</th>
<th>Conditions préalables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>Aucune configuration supplémentaire requise.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Les serveurs Exchange 2013 nécessitent les éléments suivants :</p>
<ul>
<li><p>La dernière mise à jour cumulative (CU) ou immédiatement antérieure. Les serveurs Exchange 2013 fonctionnant avec les anciennes mises à jour cumulatives ne sont pas pris en charge et peuvent ne pas fonctionner avec des autorisations de boîtes aux lettres déléguées dans un déploiement hybride.</p></li>
<li><p>L’organisation Exchange est configurée pour autoriser le marquage des listes de contrôle d’accès (ACL) dans les objets de courrier et leur synchronisation avec Office 365.</p></li>
<li><p>Les boîtes aux lettres locales à distance associées à des boîtes aux lettres déplacées vers Office 365 avant la CU10 Exchange 2013 doivent être configurées manuellement pour prendre en charge des ACL. Les boîtes aux lettres à distance, créées sur les serveurs fonctionnant avec la CU10 Exchange 2013 ou ultérieure, et après que l’organisation Exchange a été configurée pour autoriser les ACL, sont configurées automatiquement.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Les serveurs Exchange 2010 SP3 nécessitent les éléments suivants :</p>
<ul>
<li><p>Le dernier correctif cumulatif (RU) ou immédiatement antérieur. Les serveurs Exchange 2010 SP3 fonctionnant avec les anciens correctifs cumulatifs ne sont pas pris en charge et peuvent ne pas fonctionner avec des autorisations de boîtes aux lettres déléguées dans un déploiement hybride.</p></li>
<li><p>Les boîtes aux lettres locales à distance associées à des boîtes aux lettres Office 365 doivent être configurées pour prendre en charge des ACL. Cela doit être effectué pour chaque boîte aux lettres locale à distance associée à une boîte aux lettres Office 365.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 ou une version antérieure</p></td>
<td><p>Non prise en charge.</p></td>
</tr>
</tbody>
</table>


## Activation de la prise en charge des autorisations de boîtes aux lettres hybrides dans Azure Active Directory Connect

En plus de configurer vos serveurs Exchange locaux, vous devez également vérifier que le serveur Azure Active Directory Connect (AAD Connect) est configuré pour synchroniser les autorisations de boîtes aux lettres hybrides. Voici ce que vous devez faire pour vous assurer que votre serveur AAD Connect est prêt à prendre en charge ces autorisations :

  - **Mise à niveau DAS se connecter** Se connecter le DAS doit être mis à niveau au moins vers la version 1.1.553.0. Vous pouvez télécharger la dernière version de DAS Connect à partir de [Microsoft Azure Active Directory se connecter](http://go.microsoft.com/fwlink/p/?linkid=510956).

  - **Activer Exchange hybride dans AAD Connect** Pour synchroniser les attributs qui activent les autorisations de boîtes aux lettres hybrides (plus précisément, l’autorisation Envoyer de la part de), vous devez vous assurer que l’option de configuration **Déploiement Exchange hybride** est activée dans AAD Connect. Pour plus d’informations sur l’exécution de l’Assistant Installation AAD Connect pour mettre à jour sa configuration, consultez l’article [Synchronisation Azure AD Connect : Exécuter l’Assistant Installation une deuxième fois](https://docs.microsoft.com/fr-fr/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## Comment les autorisations de boîtes aux lettres sont synchronisées entre votre organisation locale et votre organisation Office 365

## Autorisations d'utilisateur final

Comme pour les autorisations d'administrateur, les utilisateurs finaux dans Exchange Online peuvent recevoir des autorisations. Par défaut, les utilisateurs finaux peuvent se voir accorder des autorisations via la stratégie d'attribution de rôle par défaut. Cette stratégie est appliquée à chaque boîte aux lettres dans l'organisation Exchange Online. Si les autorisations accordées par défaut sont suffisantes, il n'est pas nécessaire d'effectuer des modifications.

Si vous souhaitez personnaliser des autorisations d'utilisateur final, vous pouvez modifier la stratégie d'attribution de rôle par défaut ou créer de nouvelles stratégies d'attribution. Si vous créez de nombreuses stratégies d'attribution de rôle, vous pouvez attribuer différentes stratégies à différents groupes de boîtes aux lettres, ce qui vous permet de contrôler les autorisations accordées à chaque groupe en fonction de leurs besoins. La gestion de toutes les autorisations pour les utilisateurs finaux d'Exchange Online doit être effectuée dans l'organisation Exchange Online à l'aide du CAE ou de Remote PowerShell.

Comme les autorisations d'administrateur, les autorisations d'utilisateur final ne sont pas transférées entre l'organisation locale et l'organisation Exchange Online. Les autorisations que vous avez définies dans l'organisation locale doivent être recréées dans l'organisation Exchange Online.

Pour plus d'informations, consultez les rubriques [Gérer les stratégies d’attribution des rôles](https://technet.microsoft.com/fr-fr/library/jj657511\(v=exchg.150\)) et [Modifier la stratégie d’attribution sur une boîte aux lettres](https://technet.microsoft.com/fr-fr/library/dd638076\(v=exchg.150\)).

Le tableau suivant répertorie les autorisations accordées par les stratégies d'attribution de rôle par défaut dans l'organisation Exchange Online.

### Autorisations de stratégie d'attribution de rôle par défaut

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle de gestion</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p>Le rôle de gestion <code>MyTeamMailboxes</code> permet aux utilisateurs individuels de créer des boîtes aux lettres de site et de les associer à des sites Microsoft SharePoint.</p></td>
</tr>
<tr class="even">
<td><p>My Marketplace Apps</p></td>
<td><p>Le rôle de gestion <code>My Marketplace Apps</code> permet aux utilisateurs individuels d'afficher et de modifier leurs applications Marketplace Microsoft Office.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>Le rôle de gestion <code>MyBaseOptions</code> permet à chaque utilisateur d'afficher et de modifier la configuration de base de sa propre boîte aux lettres et des paramètres associés.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p>Le rôle de gestion <code>MyContactInformation</code> permet aux utilisateurs individuels de modifier leurs informations de contact, notamment l'adresse et les numéros de téléphone.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>Le rôle de gestion <code>MyDistributionGroupMembership</code> permet à chaque utilisateur d'afficher et de modifier son appartenance aux groupes de distribution d'une organisation, à condition que ces groupes de distribution permettent la modification de l'appartenance.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p>Le rôle de gestion <code>MyDistributionGroups</code> permet à chaque utilisateur de créer, de modifier et d'afficher les groupes de distribution, et de modifier, d'afficher, de supprimer et d'ajouter des membres dans les groupes de distribution qu'ils possèdent.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p>Le rôle <code>MyMailSubscription</code> permet à chaque utilisateur d'afficher et de modifier ses paramètres d'abonnement de courrier électronique, tels que le format du message et les valeurs par défaut du protocole.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p>Le rôle de gestion <code>MyProfileInformation</code> permet à chaque utilisateur de modifier son nom.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>Le rôle de gestion <code>MyRetentionPolicies</code> permet à chaque utilisateur d'afficher ses balises de rétention et d'afficher et de modifier les paramètres et valeurs par défaut de ces balises.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p>Le rôle de gestion <code>MyTextMessaging</code> permet à chaque utilisateur de créer, d'afficher et de modifier ses paramètres de messagerie texte.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p>Le rôle de gestion <code>MyVoiceMail</code> permet à chaque utilisateur d'afficher et de modifier ses paramètres de messagerie vocale.</p></td>
</tr>
<tr class="even">
<td><p>Mes applications ReadWriteMailbox</p></td>
<td><p>Le rôle de gestion <code>My ReadWriteMailbox Apps</code> permet aux utilisateurs d’installer des applications avec des autorisations ReadWriteMailbox.</p></td>
</tr>
<tr class="odd">
<td><p>Mes applications personnalisées</p></td>
<td><p>Le rôle de gestion <code>My Custom Apps</code> permet aux utilisateurs d’afficher et de modifier leurs applications personnalisées.</p></td>
</tr>
</tbody>
</table>

