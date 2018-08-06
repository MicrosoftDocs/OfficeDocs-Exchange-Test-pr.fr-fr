---
title: 'Configuration du service de disponibilité pour des topologies inter-forêts | Microsoft Docs'
TOCTitle: Configuration du service de disponibilité pour des topologies inter-forêts
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52063023
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du service de disponibilité pour des topologies inter-forêts

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-10-22_

Le service de disponibilité optimise les données de disponibilité des professionnels de l’information en fournissant des informations de disponibilité sécurisées, cohérentes et à jour aux clients exécutant Microsoft Outlook. Par défaut, ce service est installé avec Exchange Server 2013. Dans les topologies inter-forêts où tous les clients qui se connectent exécutent Outlook, le service de disponibilité est la seule méthode d’extraction des informations de disponibilité. L’environnement de ligne de commande Exchange Management Shell permet de configurer le service de disponibilité pour des topologies inter-forêts.

> [!NOTE]
> Le Centre d’administration Exchange (CAE) ne permet pas de configurer le service de disponibilité pour des topologies inter-forêts.


## Utilisation du service de disponibilité dans les forêts approuvées et non approuvées

Vous pouvez utiliser le service de disponibilité dans les topologies inter-forêts sur des forêts approuvées ou non. Le type d'informations de disponibilité dépend de l'utilisation d'une forêt approuvée ou non approuvée.

**Forêts approuvées**   Dans les forêts approuvées, vous pouvez configurer le service de disponibilité pour récupérer des informations de disponibilité par utilisateur. Lorsque le service de disponibilité est configuré pour récupérer des informations de disponibilité par utilisateur, il peut effectuer des demandes inter-forêts au nom d'un utilisateur particulier. Cela permet à un utilisateur d'une forêt distante de récupérer les informations de disponibilité détaillées d'une personne qui ne se trouve pas dans la même forêt.

**Forêts non approuvées**   Dans les forêts non approuvées, vous pouvez uniquement configurer le service de disponibilité pour qu’il récupère des informations de disponibilité par organisation. Lorsque le service de disponibilité effectue des demandes inter-forêts de disponibilité au niveau organisationnel, les informations de disponibilité sont renvoyées pour chaque utilisateur au sein de l'organisation. Dans les forêts non approuvées, il est impossible de contrôler le niveau des informations de disponibilité renvoyées par chaque utilisateur.

## Configuration de Windows pour des topologies inter-forêts

Par défaut, une liste d’adresses globale contient les destinataires d’une seule forêt. Si vous travaillez dans un environnement inter-forêts, nous vous recommandons d’utiliser Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) pour vous assurer que la liste d’adresses globale dans une forêt donnée contient tous les destinataires de messagerie d’autres forêts. ILM 2007 FP1 crée des utilisateurs de messagerie qui représentent des destinataires d’autres forêts, ce qui permet aux utilisateurs de les afficher dans la liste d’adresses globale et d’envoyer du courrier. Par exemple, les utilisateurs de la forêt A apparaissent en tant qu’utilisateurs de messagerie dans la forêt B, et inversement. Les utilisateurs de la forêt cible peuvent alors sélectionner l’objet utilisateur de messagerie qui représente un destinataire d’une autre forêt et lui envoyer du courrier.

Pour activer la synchronisation de la liste d’adresses globale, vous créez des agents de gestion qui importent les groupes, contacts et utilisateurs à extension messagerie à partir des services Active Directory indiqués vers un métarépertoire centralisé. Dans le métarépertoire, les objets à extension messagerie sont représentés en tant qu’utilisateurs de messagerie. Les groupes sont représentés en tant que contacts sans aucune appartenance associée. Les agents de gestion exportent alors ces utilisateurs de messagerie vers une unité d’organisation dans la forêt cible spécifiée.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Autorisations du service de disponibilité » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les informations de disponibilité par utilisateur dans une topologie inter-forêts approuvée

Cet exemple configure le service de disponibilité de sorte à récupérer des informations de disponibilité par utilisateur sur un serveur de boîte aux lettres de la forêt cible.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Cet exemple définit la méthode d’accès aux informations de disponibilité utilisée par le service de disponibilité sur le serveur de boîte aux lettres local de la forêt source. Le serveur de boîte aux lettres local est configuré pour accéder aux informations de disponibilité de la forêt ContosoForest.com, par utilisateur. Cet exemple montre comment utiliser le compte de service pour récupérer des informations de disponibilité.

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true

> [!NOTE]
> Pour configurer la disponibilité inter-forêts bidirectionnelle, répétez ces étapes dans la forêt cible.


Si vous choisissez de configurer une disponibilité inter-forêts avec approbation et que vous choisissez également d’utiliser un compte de service (au lieu de spécifier des informations d’identification par utilisateur ou par organisation), vous devez étendre les autorisations comme indiqué dans la section « Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la disponibilité inter-forêts approuvée avec un compte de service ». La réalisation de cette procédure dans la forêt cible donne aux serveurs de boîte aux lettres de la forêt source l’autorisation de sérialiser le contexte utilisateur d’origine.

## Utiliser l'environnement de ligne de commande Management Shell pour configurer une disponibilité inter-forêts approuvée avec un compte de service

Cet exemple montre comment configurer la disponibilité inter-forêts approuvée avec un compte de service.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-MailboxServer](https://technet.microsoft.com/fr-fr/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/fr-fr/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/fr-fr/library/bb124103\(v=exchg.150\))

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les informations de disponibilité au niveau de l'organisation dans une topologie inter-forêts non approuvée

Cet exemple montre comment définir le compte d'organisation sur l'objet de configuration de disponibilité pour configurer le niveau d'accès pour des informations de disponibilité dans la forêt cible.

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

Cet exemple montre comment ajouter l'objet de configuration de l'espace d'adressage de disponibilité pour la forêt source.

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

