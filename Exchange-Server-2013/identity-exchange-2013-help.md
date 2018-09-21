---
title: 'Identité: Exchange 2013 Help'
TOCTitle: Identité
ms:assetid: e90fae91-37e7-4fdc-9170-44f0dc965c66
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125042(v=EXCHG.150)
ms:contentKeyID: 50479479
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-04_

Le paramètre *Identity* est un paramètre spécial que vous pouvez utiliser avec la plupart des cmdlets. Le paramètre *Identity* vous donne accès aux identificateurs uniques faisant référence à un objet particulier dans Microsoft Exchange Server 2013. Cela vous permet d’appliquer des actions à un objet Exchange 2013 spécifique.

Les sections suivantes décrivent le paramètre Identity et donnent des exemples vous montrant comment l’utiliser efficacement :

Characteristics of the Identity parameter

Wildcard characters in Identity

Examples of the Identity parameter

## Caractéristiques du paramètre Identity

L’identificateur unique principal d’un objet dans Exchange 2013 est toujours un GUID. Un GUID est un identificateur de 128 bits, tel que `63d64005-42c5-4f8f-b310-14f6cb125bf3`. Le GUID n’est jamais répété et est donc toujours unique. En revanche, vous ne pouvez pas entrer de tels GUID régulièrement. C’est pourquoi le paramètre *Identity* comprend également les valeurs d’autres paramètres ou un jeu combiné de valeurs de plusieurs paramètres d’un objet unique. Ces valeurs sont également uniques. Vous pouvez spécifier les valeurs de ces autres paramètres, tels que *Name* et *DistriguishedName* ou bien elles peuvent générées par le système. Les paramètres supplémentaires éventuellement utilisés et la manière dont ils sont renseignés dépend de l’objet auquel vous faites référence.

Le paramètre *Identity* est également considéré comme paramètre positionnel. Le premier argument d’une cmdlet est supposé être le paramètre *Identity* si aucune étiquette de paramètre n’est spécifiée. Cela réduit le nombre de frappes lorsque vous tapez les commandes. Pour plus d’informations sur les paramètres positionnels, voir [Paramètres](https://technet.microsoft.com/fr-fr/library/bb124388\(v=exchg.150\)).

L’exemple suivant illustre l’utilisation du paramètre *Identity* en utilisant la valeur unique du paramètre *Name* du connecteur de réception. Cet exemple montre également comment omettre le nom de paramètre *Identity*, car le paramètre *Identity* est un paramètre positionnel.

    Get-ReceiveConnector -Identity "From the Internet"
    Get-ReceiveConnector "From the Internet"

Comme tous les objets dans Exchange 2013, ce connecteur de réception peut également être désigné par son GUID unique. Par exemple, si le connecteur de réception nommé `"From the Internet"` est également associé au GUID `63d64005-42c5-4f8f-b310-14f6cb125bf3`, vous pouvez extraire le connecteur de réception à l’aide de la commande suivante :

```powershell
Get-ReceiveConnector 63d64005-42c5-4f8f-b310-14f6cb125bf3
```

Retour au début

## Caractères génériques dans Identity

Certaines cmdlet **Get** que vous exécutez peuvent accepter le caractère générique (`*`) dans la valeur que vous soumettez à *Identity*. En utilisant ce caractère générique avec le paramètre *Identity*, vous pouvez spécifier un nom partiel et extraire une liste des objets correspondant à ce nom partiel. Vous pouvez placer le caractère générique au début ou à la fin de la valeur du paramètre *Identity* mais vous ne pouvez pas le placer au milieu d’une chaîne. Par exemple, les commandes `Get-Mailbox David*` et `Get-Mailbox *anders*` sont valides mais la commande `Get-Mailbox Reb*ca` ne l’est pas.

Certaines cmdlets **Get** permettent d’extraire des objets dans Exchange 2013, organisés dans une relation hiérarchique ou de parent et enfants. En d’autres termes, une collection d’objets parents peut donc contenir ses propres objets enfants. Les objets organisés dans une relation parent et enfants peuvent comporter un paramètre *Identity* avec la syntaxe `<parent>\<child>`.

Lorsqu’un paramètre *Identity* a la syntaxe `<parent>\<child>`, certaines cmdlets vous permettent d’utiliser le caractère générique (\*) pour remplacer tous les noms d’objet parents ou enfants ou seulement certains. Par exemple, si vous souhaitez rechercher tous les objets enfants nommés « Contoso » dans tous les objets parents, utilisez la syntaxe `"*\Contoso"`. De même, si vous souhaitez rechercher tous les objets enfants avec le nom partiel « Auth » qui existent sous l’objet parent `"ServerA" `, utilisez la syntaxe `"ServerA\Auth*"`.

Certaines des cmdlets, mais pas toutes, vous permettent de spécifier seulement la partie enfant du paramètre Identity lorsque vous exécutez une commande. Dans ce cas, les cmdlets s’exécutent par défaut sur l’objet parent actuel de l’objet enfant recherché. Par exemple, deux connecteurs de réception appelés « Contoso Receive Connector » existent sur les serveurs MBX1 et MBX2. Si vous exécutez la commande `Get-ReceiveConnector "Contoso Receive Connector"` sur MBX2, seul le connecteur de réception sur le serveur MBX2 est obtenu.

Le comportement du paramètre Identity et des caractères génériques dépend de la cmdlet qui est exécutée. Pour plus d’informations sur la cmdlet que vous exécutez, examinez son contenu.

Retour au début

## Exemples du paramètre Identity

Les exemples décrits dans cette rubrique montrent comment le paramètre *Identity* peut accepter plusieurs valeurs uniques pour faire référence à des objets spécifiques au sein de l’organisation Exchange 2013. Ils montrent également comment omettre l’étiquette du paramètre *Identity* pour réduire le nombre de frappes nécessaires pour taper les commandes.

## messages DSN

Les exemples fournis dans cette section font référence aux messages de notification d’état de remise (DSN) que vous pouvez configurer dans une organisation Exchange 2013. Le premier exemple montre comment extraire DSN 5.4.1 à l’aide de la cmdlet **Get-SystemMessage**. Dans la cmdlet **Get-SystemMessage**, le paramètre *Identity* comporte plusieurs éléments de données configurés sur chaque objet de message DSN. Ces éléments de données indiquent la langue dans laquelle la DSN est écrite, si sa portée est interne ou externe et le code du message DSN comme dans l’exemple suivant :

```powershell
Get-SystemMessage en\internal\5.4.1
```

Vous pouvez également extraire ce message DSN à l’aide de son GUID comme dans l’exemple suivant, car tous les objets dans Exchange 2013 ont un GUID :

```powershell
Get-SystemMessage 82ca7bde-1c2d-4aa1-97e1-f298a6f10222
```

Pour plus d’informations sur la composition du paramètre *Identity* en cas d’utilisation avec les cmdlets **SystemMessage**, voir [Identité du message DSN](dsn-message-identity-exchange-2013-help.md).

## Entrées de rôles de gestion

Les exemples de cette section font référence aux entrées de rôle de gestion qui constituent les rôles de gestion dans Exchange 2013. Les rôles de gestion permettent de contrôler les autorisations qui sont accordées aux administrateurs et aux utilisateurs finaux. Les entrées de rôle de gestion sont constituées de deux parties : le rôle de gestion auquel elles sont associées et une cmdlet. Le paramètre Identity est de même constitué du nom du rôle de gestion et du nom de la cmdlet. L’exemple suivant montre l’entrée de rôle pour la cmdlet **Set-Mailbox** sur le rôle `Mail Recipients` :

```powershell
Mail Recipients\Set-Mailbox
```

L’entrée de rôle `Mail Recipients\Set-Mailbox` est l’une des centaines d’entrées pour le rôle `Mail Recipients`. Pour afficher toutes les entrées de rôle pour le rôle `Mail Recipients`, utilisez la commande suivante :

    Get-ManagementRoleEntry "Mail Recipients\*"

Pour afficher toutes les entrées de rôle pour le rôle `Mail Recipients` contenant la chaîne « `Mailbox` », utilisez la commande suivante :

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*"

Pour afficher tous les rôles de gestion pour lequel **Set-Mailbox** est l’une des entrées de rôle, utilisez la commande suivante :

    Get-ManagementRoleEntry *\Set-Mailbox

Les entrées de rôle vous permettent d’utiliser le caractère générique (\*) de différentes manières pour rechercher les informations dont vous avez besoin dans Exchange 2013.

Pour plus d’informations sur les rôles de gestion, voir [Présentation des rôles de gestion](understanding-management-roles-exchange-2013-help.md).

Retour au début

