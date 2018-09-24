---
title: 'Scénario : Déploiement de stratégies de carnet d’adresses: Exchange 2013 Help'
TOCTitle: 'Scénario : Déploiement de stratégies de carnet d’adresses'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50478369
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Scénario : Déploiement de stratégies de carnet d’adresses

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

## Scénarios de déploiement

Les trois scénarios de déploiement suivants décrivent des solutions de déploiement possibles pour trois types d'organisations différents. Bien qu'il existe de nombreux autres scénarios, les plus courants sont évoqués ici. Les listes d'adresses et listes d'adresses globales (LAG) utilisés dans le cadre de ces scénarios ont été créées sur la base de filtres, comme des attributs personnalisés, qui regroupent les objets de manière logique.

## Scénario 1 : deux sociétés séparées, une organisation Exchange

Ce scénario s'applique aux agences, divisions ou services de l'État qui partagent une infrastructure, mais aucune chaîne de rapports hiérarchiques, et qui n'ont pas d'employés en commun. De plus, les divisions ne rencontrent pas de problèmes particuliers en matière de sécurité ou de confidentialité des données. Dans ce scénario, deux stratégies de carnet d'adresses sont créées. Avec ces stratégies, les employés peuvent uniquement voir les membres de la même organisation lorsqu'ils consultent la liste d'adresses globale ou les membres des autres groupes de distribution. En outre, aucun utilisateur ne sera membre des groupes de distribution qui recouvrent l'ensemble de l'organisation.

![Stratégies de carnet d’adresses avec deux entreprises distinctes](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "Stratégies de carnet d’adresses avec deux entreprises distinctes")

Les stratégies de carnet d'adresses Contoso et Humungous Insurance ont été créées à l'aide des listes d'adresses, listes d'adresses globales, listes de salles et carnets d'adresses en mode hors connexion suivants, qui ont été créés par le biais d'un filtre de destinataires qui regroupait les objets avec un filtre comme Attribut personnalisé. Étant donné que les deux sociétés sont séparées sans aucune interaction entre elles, elles n'ont pas de listes d'adresses communes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humungous Insurance</p></td>
</tr>
<tr class="even">
<td><p>Listes d'adresses</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Liste d'adresses globale</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>Liste d'adresses de salle</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>Carnet d'adresses en mode hors connexion</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## Scénario 2 : deux sociétés partageant un PDG

Dans ce scénario, Fabrikam et Tailspin Toys partagent la même organisation Exchange et le même PDG. Le PDG est la seule personne commune entre les deux sociétés. Ce scénario nécessite trois stratégies de carnet d'adresses qui présentent les caractéristiques suivantes :

  - Les utilisateurs présents dans Tailspin Toys peuvent uniquement voir les utilisateurs Tailspin Toys quand ils parcourent la liste d'adresses globale.

  - Les utilisateurs présents dans Fabrikam peuvent uniquement voir les utilisateurs Fabrikam quand ils parcourent la liste d'adresses globale.

  - Dans chaque société se trouve un groupe de distribution SeniorLeaders, qui inclut les cadres supérieurs de cette société et le PDG.

  - Les utilisateurs qui consultent l'appartenance au groupe du PDG ne peuvent voir que les groupes qui appartiennent à la société de l'utilisateur. Ils ne voient pas les groupes qui ne font pas partie de leur propre société.

  - Trois stratégies de carnet d'adresses sont créées : **Fab**, **Tail** et **PDG**.

![Deux sociétés et un PDG](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Deux sociétés et un PDG")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>PDG</p></td>
</tr>
<tr class="even">
<td><p>Listes d'adresses</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Liste d'adresses globale</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>LAG par défaut</p></td>
</tr>
<tr class="even">
<td><p>Liste d'adresses de salle</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>Toutes les salles par défaut</p></td>
</tr>
<tr class="odd">
<td><p>Carnet d'adresses en mode hors connexion</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>Carnet d'adresses en mode hors connexion par défaut</p></td>
</tr>
</tbody>
</table>


Lorsque le PDG est ajouté aux groupes de distribution de chaque société et entre dans le champ d'application de la stratégie de carnet d'adresses de chaque société, il devient visible pour chaque société. Le PDG peut créer des groupes de distribution qui recouvrent les deux sociétés et seront visibles dans la liste d'adresses globale de chaque société, mais les membres du groupe de distribution pourront seulement voir les membres du groupe qui font partie de leur propre organisation.

## Scénario 3 : éducation

Ce scénario s'applique aux écoles ou universités dans lesquelles une division des salles de classe est nécessaire pour protéger les données personnelles des étudiants. Le scénario Éducation possède les caractéristiques suivantes :

  - Les étudiants de chaque classe peuvent seulement voir les autres étudiants de leur classe, leur professeur et le proviseur.

  - Les professeurs peuvent seulement voir les étudiants de leurs propres salles de classe.

  - Les professeurs peuvent voir tous les autres professeurs et le proviseur.

  - Les groupes de distribution sont créés pour les parents de chaque classe et le corps enseignant.

![Scénario d'éducation des stratégies de carnet d’adresses](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "Scénario d'éducation des stratégies de carnet d’adresses")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>Directeur</p></td>
</tr>
<tr class="even">
<td><p>Listes d'adresses</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>Liste d'adresses globale</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>Liste d'adresses de salle</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>Toutes les salles par défaut</p></td>
</tr>
<tr class="odd">
<td><p>Carnet d'adresses en mode hors connexion</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>Carnet d'adresses en mode hors connexion par défaut</p></td>
</tr>
</tbody>
</table>


## Considérations et recommandations

Prenez les éléments suivants en considération lors de l'utilisation de stratégies de carnet d'adresses dans votre organisation :

  - Pour que les stratégies de carnet d'adresses fonctionnent correctement, la boîte aux lettres utilisateur à laquelle vous appliquez la stratégie de carnet d'adresses doit se trouver sur un serveur Exchange 2010 SP3 ou Exchange 2013.

  - N’exécutez pas le rôle serveur d’accès au client Exchange 2010 sur le serveur de catalogue global. Ceci entraînerait l'utilisation d'Active Directory pour l'interface NSPI (Name Service Provider Interface) au lieu du service de carnet d'adresses Microsoft Exchange. Vous pouvez exécuter des rôles serveur Exchange 2013 sur un serveur de catalogue global sans que cela n’affecte le fonctionnement des stratégies de carnet d’adresses. Cependant, nous vous déconseillons d’installer Exchange sur un contrôleur de domaine.

  - Vous ne pouvez pas utiliser simultanément des carnets d'adresses hiérarchiques (HAB) et des stratégies de carnet d'adresses. Pour plus d'informations, consultez la rubrique [Carnets d’adresses hiérarchiques](https://docs.microsoft.com/fr-fr/exchange/address-books/hierarchical-address-books/hierarchical-address-books).

  - Tout utilisateur auquel une stratégie de carnet d'adresses est attribuée devrait exister sans sa propre LAG.

  - Si vous autorisez des applications clientes à accéder directement à Active Directory via LDAP, elles ignoreront la logique intrinsèque des stratégies de carnet d'adresses. Étant donné qu’Outlook pour Mac 2011 et Entourage 2008 utilisent des requêtes LDAP directes pour accéder à Active Directory, ces applications clientes ne fonctionneront pas correctement avec des stratégies de carnet d’adresses si un contrôleur de domaine ou un serveur de catalogue global est spécifié ou leur est fourni par le service de découverte automatique. Outlook pour Mac 2011 peut utiliser les services web Exchange ou un carnet d'adresses en mode hors connexion local pour accéder à des informations du répertoire. Cependant, si Outlook pour Mac 2011 peut accéder directement à un service LDAP, il tentera de le faire.

  - La LAG utilisée dans une stratégie de carnet d'adresses doit, au minimum, contenir toutes les listes d'adresses, y compris la liste des adresses de salles, définies et spécifiées dans une stratégie de carnet d'adresses. Ne créez pas de LAG contenant moins d’objets qu’une des listes d’adresses de la même stratégie de carnet d’adresses.

  - Nous vous recommandons de créer des groupes de distribution qui ne dépassent pas les frontières de l'organisation virtuelle. La création de groupes de distribution contenant des membres de plusieurs organisations virtuelles est à l'origine des problèmes suivants :
    
      - Si des membres du groupe demandent des accusés de réception ou des confirmations de lecture lors de l’envoi d’un courrier électronique au groupe de distribution, ils pourront voir les adresses de messagerie des membres du groupe d’autres organisations virtuelles
    
      - Si un message chiffré est envoyé au groupe de distribution et que certains membres du groupe n’ont pas d’identifiant numérique valide, l’expéditeur recevra un message d’avertissement incluant le nombre total de membres n’ayant pas d’identifiant valide ainsi qu’une liste de leurs adresses de messagerie. Cependant, si certains de ces membres sans identifiant numérique valide appartiennent à une organisation autre que celle de l’expéditeur, le message d’avertissement inclura le nombre correct, mais pas les adresses de messagerie des membres de l’autre organisation. Il en résulte que le nombre total ne correspondra pas à la liste des adresses des membres.
        
        Par exemple, supposons qu’un groupe de distribution comprend au total cinq membres de deux organisations, l’agence A et l’agence B. Trois membres du groupe font partie de l’agence A et l’un de ces membres a un identifiant numérique non valide. Les deux autres membres font partie de l’agence B et tous deux ont des identifiants numériques non valides. Si un membre de l'agence A envoie un message chiffré au groupe de distribution, il recevra un message d'avertissement indiquant que trois destinataires au total n'ont pas d'identifiants numériques valides. Cependant, seule l'adresse de messagerie du destinataire de l'agence A sera mentionnée dans le message d'avertissement.
    
      - Les stratégies de carnet d’adresses ne s’appliquent pas aux cmdlets **Get-Group**. Pour cette raison, tout utilisateur ou processus pouvant exécuter **Get-Group** verra tous les membres de chaque groupe auquel il a accès.
        
        Il est recommandé de modifier les paramètres de gestion de groupe des options d’OWA, de manière à ce que les utilisateurs ne puissent pas utiliser Outlook Web App pour gérer des groupes. Pour empêcher les utilisateurs d'utiliser les options d'OWA pour gérer des groupes, excluez les utilisateurs du rôle RBAC MyDistributionGroupMembership. Pour plus d'informations, consultez la rubrique [Rôle MyDistributionGroupMembership](mydistributiongroupmembership-role-exchange-2013-help.md).
    
      - Si vous permettez aux utilisateurs d'utiliser Outlook ou Outlook Web App pour gérer des groupes, les propriétaires des groupes doivent voir l'intégralité de la liste des membres du groupe.

  - Toutes les stratégies de carnet d'adresses contiennent une liste d'adresses des salles. Cependant, si votre organisation n'utilise pas de listes d'adresses des salles, vous pouvez créer une liste d'adresses des salles vide par défaut.

  - Le déploiement de stratégies de carnet d'adresses n'empêche pas les utilisateurs d'une organisation virtuelle d'envoyer des courriers électroniques à des utilisateurs d'une autre organisation virtuelle. Si vous voulez empêcher les utilisateurs d'envoyer des courriers électroniques à d'autres organisations, nous vous recommandons de créer une règle de transport. Par exemple, pour créer une règle de transport destinée à empêcher les utilisateurs Contoso de recevoir des messages d’utilisateurs Fabrikam tout en permettant à un cadre supérieur de Fabrikam d’envoyer des messages à des utilisateurs Contoso, exécutez la commande d’environnement Shell suivante :
    
    ```powershell
    New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com
    ```

  - Si vous voulez appliquer une fonctionnalité similaire à la stratégie de carnet d'adresses dans le client Lync, vous pouvez définir l'attribut `msRTCSIP-GroupingID` sur des objets utilisateur spécifiques. Pour plus d'informations, consultez la rubrique [PartitionByOU remplacé par msRTCSIP-GroupingID](https://go.microsoft.com/fwlink/p/?linkid=232306).

## Étapes générales du déploiement

## Migration de la segmentation des listes d'adresses vers les stratégies de carnet d'adresses

Si votre organisation a configuré à la place la solution de répartition de listes d'adresses Exchange 2007 en suivant les instructions du livre blanc [Configuration d'organisations virtuelles et répartition de listes d'adresses dans Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=109601), effectuez d'abord la migration vers Exchange Server 2010 en suivant la procédure décrite dans [Migrer vers des stratégies de carnet d'adresses Exchange 2010 à partir de la répartition de la liste d'adresses Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=235967). Cette procédure nécessite des temps d'arrêt pour votre organisation et vous devez les planifier en conséquence.

## Nouveau déploiement de stratégies de carnet d'adresses

Si votre organisation déploie des stratégies de carnet d’adresses Exchange 2013 et n’a pas utilisé la répartition de listes d’adresses Exchange 2007, vous pouvez suivre ces instructions pour déployer les stratégies de carnet d’adresses dans votre organisation.

Les étapes de cette section vous guident au cours du scénario 2 : Scénario 2 : deux sociétés partageant un PDG. Dans ce scénario, deux sociétés (Fabrikam et Tailspin Toys) sont séparées, mais partagent un PDG et une équipe de cadres supérieurs.

## Étape 1 : installation et configuration de l'agent de routage des stratégies de carnet d'adresses

Si vous utilisez les stratégies de carnet d’adresses et si vous ne voulez pas que les utilisateurs faisant partie d’organisations virtuelles séparées puissent consulter des informations potentiellement personnelles, vous pouvez activer l’agent de routage des stratégies de carnet d’adresses. Il s'agit d'un agent de transport exécuté sur un serveur de boîtes aux lettres qui contrôle la manière dont les destinataires sont résolus dans l'organisation. Quand l’agent de routage des stratégies de carnet d’adresses est installé et configuré, les utilisateurs affectés à plusieurs LAG apparaissent en tant que destinataires externes dans le sens où ils ne peuvent pas afficher les cartes de visite de destinataires externes.

Pour obtenir des instructions détaillées, consultez la rubrique [installation et configuration de l'agent de routage des stratégies de carnet d'adresses](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Étape 2 : division de vos organisations virtuelles

Vous devrez mettre au point une manière de diviser vos organisations. Nous vous conseillons d'utiliser la propriété CustomAttribute1-15 sur les boîtes aux lettres, contacts et groupes à la place des attributs conditionnels prédéfinis comme Company, Department ou StateOrProvince afin de diviser les organisations virtuelles pour les raisons suivantes :

  - Les types de destinataires des objets n'ont pas tous des attributs conditionnels prédéfinis dans Active Directory. Par exemple, Groupe de distribution et Groupe de distribution dynamique ne prennent pas en charge les attributs company, department ou state.

  - Tous les attributs conditionnels prédéfinis ne sont pas exposés dans des cmdlets pour certains destinataires. Par exemple, les paramètres *Company*, *department* et *StateOrProvince* ne sont pas disponibles dans les éléments exposés des cmdlets pour les utilisateurs de messagerie, les contacts, les groupes de distribution et les dossiers publics à extension messagerie.

  - Plusieurs cmdlets sont requises pour répartir le destinataire quand vous utilisez l'attribut conditionnel prédéfini. Par exemple, vous devez exécuter Set-User afin de baliser *Company*, *Department*, *StateOrProvince* pour un UserMailbox une fois que vous avez exécuté les cmdlets **New-Mailbox** ou **Set-Mailbox**.

  - Les paramètres *CustomAttributeX* sont tous exposés pour la cmdlet Set-\* pour chaque type de destinataire ; nous pouvons effectuer toute la répartition pour ce type via la seule cmdlet Set-.

  - Les attributs CustomAttributeX sont explicitement réservés à la personnalisation d'une organisation et sont entièrement sous le contrôle des administrateurs de l'organisation.

Une autre recommandation à respecter lors de la répartition de votre organisation est l'utilisation d'identifiants de société dans les noms des groupes de distribution et des groupes de distribution dynamique. Exchange comporte une fonctionnalité de stratégie de noms de groupes qui ajoute automatiquement un suffixe ou un préfixe au nom du groupe de distribution en fonction des nombreux attributs de l'utilisateur qui crée le groupe de distribution, dont le créateur des attributs Company, StateorProvince, Title et CustomAttribute1 à CustomAttribute15 du groupe de distribution. La stratégie de noms de groupes est particulièrement importante si vous permettez à des utilisateurs de créer leurs propres groupes de distribution. Pour plus d'informations, consultez la rubrique [Créer une stratégie de noms de groupe de distribution](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

Les stratégie de noms de groupes ne s'appliquent pas aux groupes de distribution dynamique. Vous devrez donc les répartir manuellement et appliquer manuellement une stratégie de noms.

## Étape 3 : création des listes d'adresses, des listes d'adresses globales et des carnets d'adresses en mode hors connexion

Quand vous créez les listes d'adresses et les listes d'adresses globales, n'utilisez pas les paramètres « IncludedRecipient » et « ConditionalX », tels que ConditionalCompany et ConditionalCustomAttribute5. Vous devez plutôt utiliser un filtre de destinataires. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour créer des filtres de destinataires. Pour plus d'informations sur les filtres de destinataires, consultez la rubrique [Filtrage des destinataires sur les serveurs de transport Edge](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Quand vous créez les stratégies de carnet d'adresses, vous pouvez créer plusieurs listes d'adresses en fonction de la façon dont vous voulez que vos utilisateurs affichent les listes d'adresses dans Outlook ou Outlook Web App. Cette organisation a quatre listes d'adresses :

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

Cet exemple concerne la liste d'adresses AL\_TAIL\_Users\_DGs. La liste d'adresses contient tous les utilisateurs et groupes de distribution où CustomAttribute15 est égal à TAIL.

```powershell
New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}
```

Pour plus d'informations sur la création de listes d'adresses à l'aide de filtres de destinataires, consultez la rubrique [Création d’une liste d’adresses à l’aide de filtres de destinataires](https://docs.microsoft.com/fr-fr/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list).

Afin de créer une stratégie de carnet d'adresses, vous devez fournir une liste d'adresses de salle. Si votre organisation n'a pas de boîtes aux lettres de ressources (par exemple, des boîtes aux lettres de salle ou d'équipement), nous vous recommandons de créer une liste d'adresses de salles vide. L'exemple suivant présente la création d'une liste d'adresses de salles vide, car il n'y a aucune boîte aux lettres de salles dans l'organisation.

```powershell
New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}
```

Toutefois, dans ce scénario, Fabrikam et Contoso ont toutes deux des boîtes aux lettres de salles. Cet exemple crée la liste de salles pour Fabrikam à l'aide d'un filtre de destinataires où CustomAttribute15 est égal à FAB.

```powershell
New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}
```

La liste d'adresses globale utilisée dans une stratégie de carnet d'adresses doit être un sur-ensemble des listes d'adresses. Ne créez pas de liste d'adresses globale contenant moins d'objets que dans une des listes d'adresses de la stratégie de carnet d'adresses ou que dans toutes ces listes. Cet exemple crée la liste d'adresses globale pour Tailspin Toys, qui inclut tous les destinataires existant dans les listes d'adresses et la liste d'adresses de salles.

```powershell
New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}
```

Pour plus d'informations, consultez la rubrique [Création d’une liste d’adresses globale](https://docs.microsoft.com/fr-fr/exchange/address-books/address-lists/create-global-address-list).

Quand vous créez le carnet d'adresses en mode hors connexion, vous devez inclure la liste d'adresses globale appropriée au moment où vous spécifiez le paramètre *AddressLists* de New- ou Set-OfflineAddressBook, afin de vous assurer qu'aucune entrée n'est manquante par inadvertance. Vous pouvez en fait personnaliser le groupe d'entrées visualisées par un utilisateur ou bien réduire la taille de téléchargement du carnet d'adresses en mode hors connexion en spécifiant une liste d'AddressLists dans les AddressLists de New/Set-OfflineAddressBook. Cependant, si vous voulez que les utilisateurs voient toutes les entrées de la liste d'adresses globale dans le carnet d'adresses en mode hors connexion, veillez à inclure la liste d'adresses globale dans les AddressLists.

Cet exemple crée le carnet d'adresses en mode hors connexion OAB\_FAB pour Fabrikam.

```powershell
New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"
```

Pour plus d'informations, consultez la rubrique [Création d’un carnet d’adresses en mode hors connexion](https://docs.microsoft.com/fr-fr/exchange/address-books/offline-address-books/create-offline-address-book).

## Étape 4 : création des stratégies de carnet d'adresses

Une fois que vous avez créé tous les objets requis, vous pouvez créer la stratégie de carnet d'adresses. Cet exemple crée la stratégie de carnet d'adresses nommée ABP\_TAIL.

```powershell
New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"
```

Pour plus d'informations, consultez la rubrique [Création d’une stratégie de carnet d’adresses](https://docs.microsoft.com/fr-fr/exchange/address-books/address-book-policies/create-an-address-book-policy).

## Étape 5 : attribution des stratégies de carnet d'adresses aux boîtes aux lettres

L'attribution de la stratégie de carnet d'adresses à l'utilisateur est la dernière étape du processus. Les stratégies de carnet d'adresses prennent effet lorsqu'une application cliente se connecte au service de carnet d'adresses Microsoft Exchange sur le serveur d'accès au client. Si l'utilisateur est déjà connecté à Outlook ou à Outlook Web App quand la stratégie de carnet d'adresses est appliquée à son compte, il devra fermer puis redémarrer l'application cliente avant de pouvoir consulter ses nouvelles listes d'adresses et la liste d'adresses globale.

Cet exemple attribue ABP\_FAB à toutes les boîtes aux lettres où CustomAttribute15 est égal à « FAB ».

```powershell
Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"
```

Pour plus d'informations, consultez la rubrique [Attribuer une stratégie de carnet d’adresses à des utilisateurs de messagerie](https://docs.microsoft.com/fr-fr/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users).

