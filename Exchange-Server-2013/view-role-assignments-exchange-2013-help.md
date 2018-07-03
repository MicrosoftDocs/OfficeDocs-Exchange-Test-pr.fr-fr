---
title: 'Consulter les attributions de rôle: Exchange 2013 Help'
TOCTitle: Consulter les attributions de rôle
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50477493
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Consulter les attributions de rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Les attributions du rôle de gestion affectent un rôle de gestion à l’utilisateur. Pour plus d’informations sur les attributions de rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des attributions de rôles de gestion](understanding-management-role-assignments-exchange-2013-help.md).

Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Attribution des rôles » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Cette rubrique décrit l’utilisation du pipelining et de la cmdlet **Format-List**. Pour plus d’informations sur ces concepts, consultez les rubriques suivantes :
    
      - [Traitement en pipeline](https://technet.microsoft.com/fr-fr/library/aa998260\(v=exchg.150\))
    
      - [Utilisation de la sortie de la commande](working-with-command-output-exchange-2013-help.md)

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Afficher une liste de toutes les attributions de rôles

Vous pouvez afficher la liste de toutes les attributions de rôles configurées dans votre organisation en exécutant la cmdlet **Get-ManagementRoleAssignment**. Si vous souhaitez récupérer la liste des attributions de rôles correspondant à une chaîne partielle que vous spécifiez, utilisez des caractères génériques (\*). Cet exemple récupère une liste de toutes les attributions de rôle qui commencent par la chaîne « Tier 1 ».

    Get-ManagementRoleAssignment "Tier 1*"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher les détails d’une attribution de rôle spécifique

Vous pouvez afficher les détails d’une attribution de rôle en transférant les résultats de la cmdlet **Get-ManagementRoleAssignment** sur la cmdlet **Format-List**. Utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment <assignment name> | Format-List

Cet exemple montre comment récupérer les détails de l’attribution de rôle Attribution Help Desk.

    Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste des attributions de rôle d’un utilisateur de rôle spécifique

Pour afficher la liste des attributions de rôle associées à un groupe de rôles de gestion, à un rôle ou à une stratégie d’attribution de rôle, ou bien associées à un utilisateur ou à un groupe de sécurité universel, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RoleAssignee <role assignee name>

Cet exemple récupère toutes les attributions de rôle associées au groupe de rôle Gestion du serveur.

    Get-ManagementRoleAssignment -RoleAssignee "Server Management"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher les attributions de rôle associées à un rôle spécifique

Chaque rôle peut avoir plusieurs attributions de rôle. Vous pouvez utiliser la cmdlet **Get-ManagementRoleAssigment** pour afficher la liste des attributions de rôle associées à un rôle spécifié.

Pour afficher la liste des attributions de rôle associées à un rôle spécifié, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -Role <role name>

Cet exemple récupère toutes les attributions de rôle associées au groupe de rôle Destinataires des messages.

    Get-ManagementRoleAssignment -Role "Mail Recipients"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste des attributions de rôle qui utilisent une portée spécifique prédéfinie

Pour afficher la liste des attributions de rôle qui utilisent une portée spécifique prédéfinie, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

Cet exemple récupère toutes les attributions de rôle associées à la portée prédéfinie Organisation.

    Get-ManagementRoleAssignment -RecipientWriteScope Organization

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste des attributions de rôle qui ont été étendues vers une unité d’organisation spécifique

Pour afficher la liste des attributions de rôle qui ont été étendues vers une unité d’organisation spécifique, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>

Cet exemple extrait toutes les attributions de rôles qui ont été étendues à l’unité d’organisation Amérique du Nord\\Ingénierie\\Utilisateurs dans le domaine contoso.com.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste des attributions qui utilisent une portée personnalisée spécifique

Pour afficher la liste des attributions de rôle qui utilisent une portée personnalisée spécifique, vous devez d’abord déterminer si la portée est une portée de destinataires, de configuration, de destinataires exclusive ou de configuration exclusive. Chaque type de portée utilise un paramètre différent sur la cmdlet **Get-ManagementRoleAssignment**. La liste suivante répertorie chaque portée et son paramètre associé :

  - **Portées de destinataire** *CustomRecipientWriteScope*

  - **Portées de configuration** *CustomConfigWriteScope*

  - **Portées de destinataire exclusives** *ExclusiveRecipientWriteScope*

  - **Portées de configuration exclusives** *ExclusiveConfigWriteScope*

La syntaxe est identique pour chaque paramètre. Spécifiez le nom de la portée avec le paramètre qui correspond au type de portée dont il s’agit.

Cet exemple récupère toutes les attributions de rôle qui utilisent la portée prédéfinie Destinataires Vancouver.

    Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"

Cet exemple récupère toutes les attributions de rôle qui utilisent la portée de configuration exclusive Site AD Seattle.

    Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste de portées exclusives ou ordinaires

Pour afficher la liste des attributions de rôle exclusives ou ordinaires, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -Exclusive < $True | $False >

Par exemple, pour afficher la liste des portées exclusives, exécutez la commande suivante :

    Get-ManagementRoleAssignment -Exclusive $True

Cet exemple récupère la liste des portées ordinaires sans portée exclusive.

    Get-ManagementRoleAssignment -Exclusive $False

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher qui peut modifier un destinataire ou un serveur spécifique

Pour afficher la liste des attributions de rôle pouvant modifier un destinataire ou un serveur spécifique, utilisez les paramètres *WritableRecipient* et *WritableServer*. Spécifiez le nom du destinataire avec le paramètre *WritableRecipient* et le nom du serveur avec le paramètre *WritableServer*.

Cet exemple récupère la liste de toutes les attributions de rôle pouvant modifier le destinataire Bob.

    Get-ManagementRoleAssignment -WritableRecipient "Brian"

Vous pouvez associer les paramètres *WritableRecipient* et *WritableServer* à d’autres paramètres tels que le paramètre *RoleAssignee* et le commutateur *GetEffectiveUsers* pour affiner votre requête et développer des groupes de rôles ou des groupes de sécurité universels. Cet exemple récupère tous les utilisateurs pouvant modifier le serveur EX02 et qui sont attribués au groupe de rôle Gestion du serveur.

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher les utilisateurs qui reçoivent les autorisations d’une attribution via un groupe de rôle ou un groupe de sécurité universel

Pour afficher la liste des utilisateurs qui reçoivent les autorisations d’une attribution de rôle, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers

Cet exemple montre comment récupérer la liste des utilisateurs de l’attribution de rôle Help Desk Assignment.

    Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers

Vous pouvez aussi associer le commutateur *GetEffectiveUsers* avec plusieurs autres paramètres sur la cmdlet **Get-ManagementRoleAssignment** pour développer les groupes de rôle et les groupes de sécurité universels auxquels les attributions de rôle sont affectées. Pour obtenir un exemple d’utilisation du commutateur *GetEffectiveUsers* avec d’autres paramètres, consultez la section « Afficher qui peut modifier un destinataire ou un serveur spécifique » précédemment dans cette rubrique.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

## Afficher la liste des attributions de rôles qui sont activées ou désactivées

Pour afficher la liste des attributions de rôle activées ou désactivées, utilisez la syntaxe suivante.

    Get-ManagementRoleAssignment -Enabled < $True | $False >

Cet exemple montre comment récupérer la liste des attributions de rôle désactivées.

    Get-ManagementRoleAssignment -Enabled $False

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ManagementRoleAssignment](https://technet.microsoft.com/fr-fr/library/dd351024\(v=exchg.150\)).

