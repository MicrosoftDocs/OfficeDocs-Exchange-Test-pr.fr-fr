---
title: 'Modifier une entrée de rôle: Exchange 2013 Help'
TOCTitle: Modifier une entrée de rôle
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50478264
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier une entrée de rôle

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Chaque entrée de rôle de gestion représente une cmdlet unique. En ajoutant ou en supprimant des paramètres dans une entrée de rôle, qui est alors ajoutée à un rôle de gestion, vous contrôlez la disponibilité des paramètres sur la cmdlet. Pour plus d’informations sur les entrées de rôles de gestion dans Microsoft Exchange Server 2013, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Vous ne pouvez pas modifier les entrées de rôle des rôles de gestion intégrés.

> [!NOTE]
> Cette rubrique ne décrit pas comment modifier les entrées des rôles de gestion non délimitées d’un rôle de gestion non délimité. Pour plus d’informations sur la modification des entrées de rôle non délimitées, consultez la rubrique <a href="create-a-role-exchange-2013-help.md">Créer un rôle</a>.


> [!CAUTION]
> Pour ajouter ou supprimer des paramètres dans une entrée de rôle, utilisez les paramètres <em>AddParameter</em> ou <em>RemoveParameter</em>. Si vous omettez de préciser le paramètre <em>AddParameter</em> ou <em>RemoveParameter</em> lors de l’exécution de la cmdlet <strong>Set-ManagementRoleEntry</strong>, seuls les paramètres que vous spécifiez via le paramètre <em>Parameters</em> sont inclus dans l’entrée de rôle. Tous les autres paramètres de l’entrée de rôle seront supprimés.


Souhaitez-vous rechercher les autres tâches de gestion relatives aux rôles ? Consultez la rubrique [Autorisations avancées](advanced-permissions-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Rôles de gestion » dans la rubrique [Autorisations pour la gestion des rôles](role-management-permissions-exchange-2013-help.md).

  - Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell pour effectuer ces procédures.

  - Si vous souhaitez ajouter des paramètres à une entrée de rôle, les paramètres que vous ajoutez doivent exister dans l’entrée de rôle au sein du rôle parent. Les paramètres doivent également exister dans la cmdlet que vous spécifiez.

  - Si vous souhaitez supprimer des paramètres d’une entrée de rôle, ces paramètres ne doivent pas exister dans les entrées de rôle des rôles enfants. Vous devez d’abord supprimer les paramètres des entrées de rôle des rôles enfants. À l’aide de la procédure « Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un ou plusieurs paramètres d’une entrée de rôle », décrite plus bas dans cette rubrique, supprimez les paramètres des entrées de rôle appartenant à tous les rôles enfants.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un ou plusieurs paramètres à une entrée de rôle

Pour ajouter des paramètres à une entrée de rôle, spécifiez les paramètres requis à l’aide du paramètre *Parameters*. Indiquez ensuite le paramètre *AddParameter* pour préciser si vous effectuez un ajout.

Pour ajouter des paramètres à une entrée de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter
```

Cet exemple indique comment ajouter les paramètres *EmailAddresses* et *Type* à la cmdlet **Set-Mailbox** du rôle Administrateurs des destinataires.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un ou plusieurs paramètres d’une entrée de rôle

Pour supprimer des paramètres d’une entrée de rôle, spécifiez les paramètres requis à l’aide du paramètre *Parameters*. Indiquez ensuite le paramètre *RemoveParameter* pour préciser si vous effectuez une suppression.

Pour supprimer des paramètres d’une entrée de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter
```

Cet exemple indique comment supprimer les paramètres *Port*, *ProtocolLoggingLevel* et *SmartHostAuthMechanism* de la cmdlet **Set-SendConnector** du rôle Administrateurs de serveur de niveau 1.

```powershell
Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer tous les paramètres d’une entrée de rôle

Pour supprimer tous les paramètres d’une entrée de rôle, vous devez spécifier la valeur `$Null` dans le paramètre *Parameters*. Vous n’avez pas à utiliser le paramètre *RemoveParameters*.

La suppression globale des paramètres dans une entrée de rôle est utile si seulement quelques paramètres doivent être disponibles dans une cmdlet et que vous souhaitez en exclure tous les autres. Si vous ne voulez pas que le rôle ait accès à une cmdlet, supprimez entièrement l’entrée associée dans le rôle et non pas simplement les paramètres. Pour plus d’informations sur la suppression d’une entrée de rôle, voir [Supprimer une entrée de rôle d'un rôle](remove-a-role-entry-from-a-role-exchange-2013-help.md).

> [!CAUTION]
> Vous ne pouvez pas annuler la suppression de ces opérations. Si vous supprimez par erreur tous les paramètres d’une entrée de rôle, vous devez les ajouter à nouveau manuellement.


Pour supprimer des paramètres d’une entrée de rôle, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 
```

Cet exemple indique comment supprimer tous les paramètres de la cmdlet **Set-CASMailbox** du rôle Administrateurs des destinataires.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour appliquer un ensemble spécifique de paramètres

Si vous souhaitez inclure uniquement un ensemble spécifique de paramètres dans une entrée de rôle, spécifiez seulement le paramètre *Parameters*. N’incluez pas les paramètres *AddParameter* ou *RemoveParameter*. Lorsque vous spécifiez uniquement le paramètre *Parameters*, uniquement les paramètres que vous spécifiez dans la commande sont inclus sur l’entrée de rôle. Tous les autres paramètres sont supprimés.

Pour spécifier un ensemble spécifique de paramètres, utilisez la syntaxe suivante.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

Cet exemple indique comment inclure uniquement les paramètres *Identity*, *DisplayName*, *MissedCallNotificationEnabled* et *PersonalAuthAttendantEnabled* dans la cmdlet **Set-UMMailbox** du rôle Destinataires à Seattle.

```powershell
Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ManagementRoleEntry](https://technet.microsoft.com/fr-fr/library/dd351162\(v=exchg.150\)).

