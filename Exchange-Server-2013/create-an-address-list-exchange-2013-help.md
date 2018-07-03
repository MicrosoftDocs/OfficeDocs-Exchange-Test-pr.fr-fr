---
title: "Créer une liste d'adresses: Exchange 2013 Help"
TOCTitle: Créer une liste d'adresses
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50479448
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# Créer une liste d'adresses

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-12_

Les listes d’adresses sont un ensemble d’objets destinataire et autres objets Active Directory. Chaque liste d’adresses peut contenir un ou plusieurs types d’objets (par exemple, des utilisateurs, des contacts, des groupes, des dossiers publics, des ressources de conférence et d’autres ressources). Les listes d’adresses fournissent également un mécanisme pour partitionner les objets à extension messagerie d’Active Directory au bénéfice de groupes d’utilisateurs spécifiques.

Pour les autres tâches de gestion relatives aux listes d’adresses, voir [Procédures des listes d'adresses](address-list-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Listes d’adresses » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser la CAE pour créer une liste d’adresses

1.  Accédez à **Organisation** \> **Listes d’adresses**, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans **Liste d'adresses**, saisissez un nom et indiquez les types de destinataire à inclure dans la liste.

3.  Par défaut, Exchange crée des listes d'adresses qui contiennent tous les membres de votre organisation. Pour créer une liste d'adresses personnalisée unique, cliquez sur **Ajouter une règle**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous n'ajoutez aucune règle, vous allez créer une liste d'adresses redondante par rapport à l'une des listes d'adresses par défaut.</td>
    </tr>
    </tbody>
    </table>


4.  Dans la liste, sélectionnez une option de filtrage (par exemple, **Attribut personnalisé 1**).

5.  Dans **Spécifier des mots ou des expressions**, saisissez des mots ou des expressions à appliquer au filtre, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sur **OK**.
    
    Vous pouvez continuer à ajouter plusieurs expressions ou mots en répétant l'étape 4. Le filtre est une déclaration booléenne **OU**. Par exemple, vous pouvez créer un filtre qui appliquera la liste d'adresses aux utilisateurs dont l'attribut Personnalisé 1 est **Oregon**, **Idaho** ou **Washington**.

6.  (Facultatif) Cliquez de nouveau sur **Ajouter une règle** pour ajouter des filtres supplémentaires. Les filtres supplémentaires créent une déclaration booléenne **Et**. Ajouter des filtres réduit le nombre d'utilisateurs auquel la liste d'adresses s'applique.

7.  Cliquez sur **Afficher l'aperçu des destinataires inclus dans les listes d'adresses** pour visualiser les destinataires auxquels cette liste d'adresses va s'appliquer.

8.  Cliquez sur **Enregistrer**.

9.  Un avertissement apparaît pour vous indiquer que la liste d'adresses s'appliquera uniquement lorsque vous l'aurez mise à jour. En fonction de la taille de votre organisation et des filtres que vous avez ajoutés à la liste d'adresses, certaines listes d'adresses peuvent contenir des milliers ou des centaines de milliers de destinataires. Mettre à jour les listes d'adresses peut avoir une incidence sur vos ressources. Il est donc préférable de réaliser cette opération pendant les heures creuses.
    
    Pour plus d'informations sur la mise à jour d'une liste d'adresses, voir [Mettre à jour une liste d'adresses](update-an-address-list-exchange-2013-help.md).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour créer une liste d’adresses

Dans cet exemple, la liste d’adresses MyAddressList est créée à l’aide du paramètre *RecipientFilter* et contient des destinataires qui sont des utilisateurs de boîte aux lettres, et pour lesquels `StateOrProvince` est défini par `Washington` ou `Oregon`.

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

Dans cet exemple, la liste d’adresses enfant nommée Building 34 Meeting Rooms est créée dans le conteneur parent All Rooms à l’aide de conditions intégrées.

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-AddressList](https://technet.microsoft.com/fr-fr/library/aa996912\(v=exchg.150\)).

