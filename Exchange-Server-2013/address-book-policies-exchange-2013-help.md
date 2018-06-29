---
title: 'Stratégies de carnet d’adresses: Exchange 2013 Help'
TOCTitle: Stratégies de carnet d’adresses
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50479283
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégies de carnet d’adresses

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Découvrez comment vous pouvez segmenter votre liste d’adresses globale en groupes spécifiques pour créer des listes d’adresses globales (LAG) personnalisées dans Outlook et Outlook Web App.

La segmentation de la liste d’adresses globale (LAG) (également appelée *répartition LAG*) est le processus qui permet aux administrateurs de segmenter des utilisateurs dans des populations spécifiques pour créer des vues personnalisées de la liste d’adresses globale de leur organisation. Les stratégies de carnet d’adresses vous permettent de segmenter des utilisateurs dans des groupes spécifiques pour créer des vues personnalisées de la liste d’adresses globale de votre organisation. Lorsque vous créez une stratégie de carnet d'adresses, vous affectez une LAG, un carnet d'adresses en mode hors connexion, une liste de pièces ainsi qu'une ou plusieurs liste(s) d'adresses à la stratégie. Vous pouvez alors attribuer la stratégie de carnet d'adresses à des utilisateurs de boîtes aux lettres et leur donner accès à une LAG personnalisée dans Outlook et Outlook Web App. L'objectif est de fournir un mécanisme plus simple de segmentation LAG pour des organisations locales nécessitant plusieurs LAG.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les stratégies de carnet d'adresses ont pour but d'optimiser les LAG et les listes d'adresses pour chaque groupe d'utilisateurs, et non de les empêcher de se voir ou de communiquer avec d'autres utilisateurs dans votre organisation. Les stratégies de carnet d'adresses créent une séparation uniquement virtuelle, pas légale, des utilisateurs au niveau des annuaires.</td>
</tr>
</tbody>
</table>


**Contenu de cette rubrique**

Fonctionnement des stratégies de carnet d'adresses

Exemple de stratégie de carnet d'adresses

Entourage, Outlook pour Mac et stratégies de carnet d'adresses

## Fonctionnement des stratégies de carnet d'adresses

Les stratégies de carnet d'adresses contiennent les listes suivantes :

  - Une LAG

  - Un carnet d'adresses en mode hors connexion (OAB)

  - Une liste des salles (à des fins de réservation)

  - Une ou plusieurs listes d'adresses

Sur l'illustration suivante, la stratégie de carnet d'adresses A consiste en un sous-ensemble des différents objets d'adresses qui existent dans l'organisation (voir la moitié inférieure de l'illustration). Le champ d'application de la stratégie de carnet d'adresses qui en résulte est égal à celui de la LAG contenue dans la stratégie, dans le cas présent LAG1. Lorsque la stratégie de carnet d'adresses est créée et affectée à un utilisateur, les objets d'adresses dans le carnet d'adresses en mode hors connexion font partie des objets que l'utilisateur peut afficher.

![Aperçu des stratégies de carnet d’adresses](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "Aperçu des stratégies de carnet d’adresses")

Vous pouvez utiliser les méthodes suivantes pour affecter des stratégies de carnet d'adresses à des utilisateurs de boîtes aux lettres individuels :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Boîte aux lettres nouvelle ou existante ?</th>
<th>Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nouveau</p></td>
<td><p>Cmdlet <a href="https://technet.microsoft.com/fr-fr/library/aa997663(v=exchg.150)">New-Mailbox</a>, avec le paramètre <em>AddressBookPolicy</em></p></td>
</tr>
<tr class="even">
<td><p>Existante</p></td>
<td><p>Cmdlet <a href="https://technet.microsoft.com/fr-fr/library/bb123981(v=exchg.150)">Set-Mailbox</a>, avec le paramètre <em>AddressBookPolicy</em></p>
<p></p></td>
</tr>
</tbody>
</table>


Les stratégies de carnet d'adresses prennent effet quand l'application cliente d'un utilisateur se connecte à un serveur d'accès au client Exchange 2013. Si vous modifiez les stratégies de carnet d'adresses, les stratégies mises à jour ne prennent pas effet tant que l'utilisateur ne redémarre ou ne reconnecte pas le client ou tant que vous ne redémarrez pas les serveurs d'accès au client RPC sur le serveur de boîtes aux lettres Exchange 2013.

## Agent de routage des stratégies de carnet d'adresses

Dans une organisation Exchange qui n’utilise pas de stratégies de carnet d’adresses, les événements suivants se produisent lorsqu’un courrier électronique est créé dans Outlook ou Outlook Web App et envoyé à un autre destinataire dans votre organisation Exchange :

1.  L'adresse de messagerie se résout. Par exemple, si vous entrez **kweku@contoso.com** dans le champ **À**, l’adresse de messagerie SMTP serait résolue sur le nom d’affichage de l’utilisateur **Kweku Ako-Adjei**.

2.  Vous pouvez afficher la carte de visite de l’autre personne. Une fois le nom résolu, vous pouvez double-cliquer sur le nom de l’utilisateur et afficher ses coordonnées, par exemple ses numéros de téléphone personnel et professionnel.

Si vous utilisez les stratégies de carnet d’adresses et si vous ne voulez pas que les utilisateurs faisant partie d’organisations virtuelles séparées puissent consulter des informations potentiellement personnelles, vous pouvez activer l’agent de routage des stratégies de carnet d’adresses. L'agent de routage des stratégies de carnet d'adresses est un agent de transport qui contrôle la manière dont les destinataires sont résolus dans voter organisation. Quand l’agent de routage des stratégies de carnet d’adresses est installé et configuré, les utilisateurs affectés à plusieurs LAG apparaissent en tant que destinataires externes, dans le sens où ils ne peuvent pas afficher les cartes de visite de destinataires externes.

Pour plus d'informations sur l'activation de l'agent de routage des stratégies de carnet d'adresses dans Exchange Online, consultez la rubrique [Activation du routage des stratégies de carnet d’adresses](https://technet.microsoft.com/fr-fr/library/jj891095\(v=exchg.150\)).

Pour plus d'informations sur l'activation de l'agent de routage des stratégies de carnet d'adresses dans Exchange Online, consultez la rubrique [installation et configuration de l'agent de routage des stratégies de carnet d'adresses](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Exemple de stratégie de carnet d'adresses

Dans le diagramme suivant, Fabrikam et Tailspin Toys partagent la même organisation Exchange et le même PDG. Le PDG est la seule personne commune aux deux sociétés.

![Deux sociétés et un PDG](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Deux sociétés et un PDG")

Cette configuration compte trois stratégies de carnet d'adresses :

  - L'une contient les employés Fabrikam et le PDG

  - Une autre contient les employés Tailspin Toys et le PDG

  - La dernière contient uniquement le PDG

Les stratégies de carnet d'adresses obéissent aux règles suivantes :

  - Les utilisateurs présents dans Tailspin Toys peuvent uniquement voir les employés Tailspin Toys et le PDG quand ils parcourent la liste d'adresses globale.

  - Les utilisateurs présents dans Fabrikam peuvent uniquement voir les employés Fabrikam et le PDG quand ils parcourent la liste d'adresses globale.

  - Le PDG peut voir l'ensemble des employés Fabrikam et Tailspin Toys quand il parcourt la liste d'adresses globale.

  - Les utilisateurs qui consultent l'appartenance au groupe du PDG ne peuvent voir que les groupes qui appartiennent à la société de l'utilisateur. Ils ne peuvent pas voir les groupes existant dans l'autre société.

## Entourage, Outlook pour Mac et stratégies de carnet d'adresses

Les stratégies de carnet d’adresses ne fonctionneront pas pour les utilisateurs d’Entourage ou d’Outlook pour Mac qui sont connectés à leur réseau d’entreprise. Ceci est valable lorsque, à l'intérieur du réseau d'entreprise, les clients Entourage et Outlook pour Mac se connectent directement au serveur de catalogue global et interrogent directement Active Directory au lieu d'utiliser le serveur d'accès au client. Cependant, les clients Outlook pour Mac 2011se connectant depuis Internet peuvent utiliser un carnet d'adresses en mode hors connexion (OAB) ou les services Exchange Web (EWS). Il en résulte que ces clients peuvent rechercher dans les LAG en fonction des stratégies de carnet d'adresses affectées. Pour en savoir plus sur l'administration d'Outlook pour Mac 2011, consultez la rubrique [Planification pour Outlook pour Mac 2011](https://go.microsoft.com/fwlink/?linkid=231878)

## Pour plus d'informations

[Scénario : Déploiement de stratégies de carnet d’adresses](scenario-deploying-address-book-policies-exchange-2013-help.md)

[Procédures relatives aux stratégies de carnet d'adresses](https://technet.microsoft.com/fr-fr/library/jj891096\(v=exchg.150\)) dans Exchange Online

