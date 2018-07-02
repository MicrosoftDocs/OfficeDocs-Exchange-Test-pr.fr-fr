---
title: 'Centre d’administration Exchange dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Centre d’administration Exchange dans Exchange 2013
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50478853
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Centre d’administration Exchange dans Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-17_

Le Centre d’administration Exchange (CAE) et la console de gestion web de Microsoft Exchange Server 2013 optimisée pour les déploiements Exchange locaux, en ligne et hybrides. Le CAE remplace la Console de gestion Exchange (EMC) et le Panneau de configuration Exchange (ECP) qui étaient les deux interfaces utilisées pour la gestion d’Exchange Server 2010.

L’un des avantages du CAE est qu’il vous permet de partitionner l’accès à Internet et à l’intranet à partir du répertoire virtuel IIS de l’ECP. Grâce à cette fonctionnalité, vous pouvez contrôler si des utilisateurs sont autorisés à accéder via Internet au CAE à partir de l’extérieur de votre organisation, tout en autorisant un utilisateur final à accéder aux options d’Outlook Web App. Pour plus d’informations, consultez la rubrique [Désactivation de l’accès au Centre d’administration Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Vous recherchez la version Exchange Online correspondant à cette rubrique ? Consultez la rubrique [Centre d’administration Exchange dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200743\(v=exchg.150\)).

Vous recherchez la version Exchange Online Protection correspondant à cette rubrique ? Consultez la rubrique [Centre d’administration Exchange dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj723141\(v=exchg.150\)).

Contenu de cette rubrique

Accès au CAE

Éléments d’interface utilisateur communs dans le CAE

Navigateurs pris en charge

## Accès au CAE

Le CAE étant une console de gestion basée sur le web, vous devez utiliser l’URL du répertoire virtuel de l’ECP pour accéder à la console à partir de votre navigateur. Dans la plupart des cas l’URL du CAE ressemble à ceci :

  - **URL interne : `https://<CASServerName>/ecp`**   L’URL interne permet d’accéder au CAE depuis l’intérieur du pare-feu de votre organisation.

  - **URL externe : `https://mail.contoso.com/ecp`**   L’URL externe permet d’accéder au CAE depuis l’extérieur du pare-feu de votre organisation. Il se peut que certaines organisations souhaitent désactiver l’accès externe au CAE. Pour plus d’informations, consultez la rubrique [Désactivation de l’accès au Centre d’administration Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

La cmdlet [Get-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd351058\(v=exchg.150\)) vous permet de rechercher les adresses URL interne et externe du CAE. Pour plus d’informations, consultez la rubrique [Recherche des URL interne et externe du Centre d'administration Exchange](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md).

Si vous vous trouvez dans une situation de coexistence, dans laquelle vous exécutez Exchange Server 2010 et Exchange Server 2013 au sein de la même organisation, et que votre boîte aux lettres est toujours hébergée sur le serveur de boîtes aux lettres Exchange 2010, le navigateur utilise par défaut l’ECP d’Exchange Server 2010. Vous pouvez accéder au CAE en ajoutant la version d’Exchange à l’URL. Par exemple, pour accéder au CAE dont le répertoire virtuel est hébergé sur le serveur d’accès au client CAS15-NA, utilisez l’URL suivante : `https://CAS15-NA/ecp/?ExchClientVer=15`. Inversement, pour accéder à l’ECP d’Exchange 2010 alors que votre boîte aux lettres réside sur un serveur de boîtes aux lettres Exchange 2013, utilisez l’URL suivante : `https://CAS14-NA/ecp/?ExchClientVer=14`.

## Éléments d’interface utilisateur communs dans le CAE

Cette section décrit les éléments d’interface utilisateur communs dans le Centre d’administration Exchange.

![Centre d’administration Exchange](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Centre d’administration Exchange")

## Navigation intersites

La navigation intersite vous permet de basculer facilement entre vos déploiements Exchange Online et Exchange local. Si vous n’avez pas d’organisation Exchange Online, le lien vous dirige vers la page d’inscription à Office 365. Pour en savoir plus, consultez la rubrique [Déploiements hybrides Exchange Server](https://technet.microsoft.com/fr-fr/library/jj200581\(v=exchg.150\)).

## Volet des fonctionnalités

Il s’agit du premier niveau de navigation pour la plupart des tâches que vous exécuterez au sein du CAE. Le volet des fonctions est similaire à l’arborescence de la console EMC dans Exchange 2010. Cependant, dans Exchange 2013, le volet des fonctions est organisé par domaines de fonctions par opposition aux rôles serveur, et les recherches nécessitent moins de clics.

  - **Destinataires   **C’est ici que vous gérerez les boîtes aux lettres, les groupes, les boîtes aux lettres de ressources, les contacts, les boîtes aux lettres partagées, ainsi que les migrations et les déplacements de boîtes aux lettres.

  - **Autorisations   **C’est ici que vous gérerez les rôles d’administrateur, les rôles d’utilisateur et les stratégies d’Outlook Web App.

  - **Gestion de la conformité   **C’est ici que vous gérerez la découverte électronique inaltérable, la conservation inaltérable, l’audit, la protection contre la perte de données (DLP), les stratégies de rétention, les balises de rétention et les règles de journal.

  - **Organisation   **C’est ici que vous gérerez les tâches appartenant à votre organisation Exchange, y compris le partage fédéré, les applications Outlook et les listes d’adresses.

  - **Protection   **C’est ici que vous gérerez la protection contre les programmes malveillants pour votre organisation.

  - **Flux de messagerie   **C’est ici que vous gérerez les règles, rapports de remise, domaines acceptés, stratégies d’adresse de messagerie et connecteurs d’envoi et de réception.

  - **Mobile   **C’est ici que vous gérerez les appareils mobiles que vous autorisez à se connecter à votre organisation. Vous pouvez gérer les stratégies d’accès aux appareils mobiles et de boîtes aux lettres des appareils mobiles.

  - **Dossiers publics   **Dans Exchange 2010, vous deviez gérer les dossiers publics via la Console de gestion des dossiers publics, qui se trouvait en dehors de l’EMC dans la boîte à outils. Dans Exchange 2013, vous pouvez gérer des dossiers publics à partir de la zone de fonctionnalités **dossiers publics**.

  - **Messagerie unifiée   **C’est ici que vous gérerez les plans de numérotation de messagerie unifiée et les passerelles IP de messagerie unifiée.

  - **Serveurs   **C’est ici que vous gérerez vos serveurs de boîtes aux lettres et d’accès au client, bases de données, groupes de disponibilité de base de données (DAG), répertoires virtuels et certificats.

  - **Hybride   **C’est ici que vous installerez et configurerez une organisation hybride.

## Onglets

Les onglets constituent votre deuxième niveau de navigation. Chaque zone de fonctionnalités contient différents onglets représentant chacun une fonctionnalité complète. La seule exception à cette règle est la zone de fonctionnalité Hybride. Vous devez en premier lieu préparer votre organisation à un déploiement hybride en utilisant l’Assistant Configuration hybride.

## Barre d’outils

Lorsque vous cliquez sur la plupart des onglets, une barre d’outils s’affiche. La barre d’outils contient des icônes qui correspondent à une action spécifique. Le tableau suivant décrit les icônes les plus courantes et leurs actions. Pour afficher l’action associée à une icône, il suffit de positionner le pointeur de la souris au-dessus de l’icône.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Icône</th>
<th>Nom</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icône Ajouter" alt="Icône Ajouter" /></p></td>
<td><p>Ajouter, Nouveau</p></td>
<td><p>Permet de créer un objet. Certaines de ces icônes sont associées à une flèche vers le bas sur laquelle vous pouvez cliquer pour afficher des objets supplémentaires que vous pouvez créer. Par exemple, dans <strong>Destinataires</strong>&gt;<strong>Boîtes aux lettres</strong>, un clic sur la flèche vers le bas affiche <strong>Boîte aux lettres utilisateur</strong> et <strong>Boîte aux lettres liée</strong> comme options supplémentaires.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" /></p></td>
<td><p>Modifier</p></td>
<td><p>Permet de modifier un objet.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="Icône Supprimer" alt="Icône Supprimer" /></p></td>
<td><p>Supprimer</p></td>
<td><p>Permet de supprimer un objet. Certaines des icônes de suppression comportent une flèche vers le bas, sur laquelle vous pouvez cliquer pour afficher des options supplémentaires.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="Icône Recherche" alt="Icône Recherche" /></p></td>
<td><p>Rechercher</p></td>
<td><p>Permet d’ouvrir une zone de recherche dans laquelle vous pouvez entrer une expression pour rechercher un objet. Consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/jj156853(v=exchg.150)">Destinataires &gt; Recherche avancée</a> pour afficher d’autres options de recherche.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Icône Actualiser" alt="Icône Actualiser" /></p></td>
<td><p>Actualiser</p></td>
<td><p>Permet d'actualiser l'affichage Liste.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icône Options supplémentaires" alt="Icône Options supplémentaires" /></p></td>
<td><p>Plus d’options</p></td>
<td><p>Utilisez cette icône pour afficher d’autres actions que vous pouvez effectuer pour des objets de cet onglet. Par exemple, dans <strong>Destinataires</strong> &gt; <strong>Boîtes aux lettres</strong>, cliquez sur cette icône pour afficher les options suivantes : <strong>Désactiver</strong>, <strong>Ajouter/Supprimer des colonnes</strong>, <strong>Exporter des données dans un fichier CSV</strong>, <strong>Connecter une boîte aux lettres</strong> et <strong>Recherche avancée</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="Icône flèche vers le haut" alt="Icône flèche vers le haut" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="Icône de flèche vers le bas" alt="Icône de flèche vers le bas" /></p></td>
<td><p>Flèche vers le haut et flèche vers le bas</p></td>
<td><p>Utilisez ces icônes pour relever ou abaisser la priorité d’un objet. Par exemple, dans <strong>Flux de messagerie</strong> &gt; <strong>Stratégies d’adresse de messagerie</strong>, cliquez sur la flèche vers le haut pour élever la priorité d’une stratégie d’adresse de messagerie. Vous pouvez aussi utiliser ces flèches pour naviguer dans la hiérarchie des dossiers publics et pour déplacer des règles vers le haut ou vers le bas dans l’affichage Liste.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="Icône Copier" alt="Icône Copier" /></p></td>
<td><p>Copier</p></td>
<td><p>Cette icône permet de copier un objet et d’y apporter des modifications sans avoir à modifier l’objet d’origine. Par exemple, dans <strong>Autorisations</strong>&gt;<strong>Rôles d’administrateur</strong>, sélectionnez un rôle dans l’affichage Liste, puis cliquez sur cette icône pour créer un groupe de rôles basé sur un groupe existant.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="Icône Suppression" alt="Icône Suppression" /></p></td>
<td><p>Supprimer</p></td>
<td><p>Cette icône permet de supprimer un élément d’une liste. Par exemple, dans la boîte de dialogue <strong>Autorisations des dossiers publics</strong>, vous pouvez supprimer des utilisateurs de la liste des utilisateurs autorisés à accéder au dossier public en les sélectionnant, puis en cliquant sur cette icône.</p></td>
</tr>
</tbody>
</table>


## Affichage Liste

Lorsque vous sélectionnez un onglet, dans la plupart des cas, vous devez voir un affichage Liste. L’affichage Liste du CAE a été conçu pour supprimer les limites existantes de l’ECP. L’ECP ne peut afficher que jusqu’à 500 objets et, pour afficher des objets qui ne sont pas répertoriés dans le volet d’informations, vous devez utiliser des options de recherche et de filtre pour retrouver ces objets spécifiques. Dans Exchange 2013, la limite d’affichage au sein de la liste Affichage du CAE est d’environ 20 000 objets pour des déploiements locaux et de 10 000 objets dans Exchange Online. En outre, la pagination est incluse pour vous permettre de paginer les résultats. Dans l’affichage Liste **Destinataires**, vous pouvez également configurer la taille de page et exporter les données dans un fichier CSV.

## Volet d’informations

Quand vous sélectionnez un objet dans l’affichage Liste, les informations relatives à ce dernier apparaissent dans le volet d’informations. Dans certains cas (par exemple, avec des objets de destinataires), le volet d’informations inclut des tâches de gestion rapides. Par exemple, si vous accédez à **Destinataires**\> **Boîtes aux lettres**, puis sélectionnez une boîte aux lettres dans l’affichage Liste, le volet d’informations affiche une option permettant d’activer ou de désactiver l’archivage pour cette boîte aux lettres. Le volet d’informations permet également de modifier en bloc plusieurs objets. Pour cela, il suffit d’appuyer sur la touche Ctrl, de sélectionner les objets à modifier en bloc et d’utiliser les options du volet d’informations. Par exemple, la sélection de plusieurs boîtes aux lettres vous permet de mettre à jour en bloc, pour plusieurs utilisateurs, des informations de contact et d’organisation, des attributs personnalisés, un quota de boîtes aux lettres, des paramètres Outlook Web App, etc.

## Notifications

Le CAE inclut une visionneuse de notification qui affiche l’état des processus longs et fournit des notifications lorsqu’ils s’achèvent. En outre, dans le cas des processus particulièrement longs (comme des demandes de déplacement), vous pouvez accepter de recevoir des notifications par courrier électronique.

## Vignette de l’utilisateur en cours et Aide

La *vignette de l’utilisateur en cours* vous permet de fermer votre session du CAE pour ouvrir ensuite la session d’un autre utilisateur. Depuis le menu contextuel d’Aide ![Icône d’aide](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icône d’aide"), vous pouvez exécuter les actions suivantes :

  - **Aide**   Cliquez sur ![Icône d’aide](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icône d’aide") pour afficher le contenu de l’aide en ligne.

  - **Désactiver la bulle d’aide**   La bulle d’aide affiche une aide contextuelle pour des champs spécifiques quand vous créez ou modifiez un objet. Vous pouvez désactiver l’aide de la bulle d’aide ou l’activer si elle a été désactivée.

  - **Copyright et confidentialité   **Cliquez sur le lien de confidentialité et de copyright pour lire les informations de copyright et de confidentialité relatives à Exchange 2013.

## Navigateurs pris en charge

Pour avoir la meilleure expérience avec le CAE, utilisez un des ensembles système d’exploitation et navigateur appelé « Premium ».

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>D'autres ensembles systèmes d'exploitation et navigateur non répertoriés dans le tableau ci-avant ne sont pas pris en charge.</td>
</tr>
</tbody>
</table>


  - **Premium** : Toutes les fonctionnalités sont prises en charge et entièrement testées.

  - **Prise en charge** : A la même prise en charge fonctionnelle que premium. Toutefois, les navigateurs pris en charge ne seront pas dotés des fonctionnalités que l’ensemble système d’exploitation et navigateur ne prend pas en charge.

  - **Non prise en charge** : L’ensemble navigateur et système d’exploitation n’est pas pris en charge ou testé.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Navigateur Web</p></td>
<td><p>Windows XP et Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 et Windows Server 2008</p></td>
<td><p>Windows 8 et Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 ou version ultérieure</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 ou version ultérieure</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 ou version ultérieure</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Non pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 ou version ultérieure</p></td>
<td><p>Pris en charge</p></td>
<td><p>Pris en charge</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Non pris en charge</p></td>
</tr>
</tbody>
</table>

