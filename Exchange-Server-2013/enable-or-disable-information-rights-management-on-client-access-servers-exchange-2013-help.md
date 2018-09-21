---
title: 'Activer ou désactiver la gestion de droits (IRM) sur les srv d’accès au client'
TOCTitle: Activer ou désactiver la gestion des droits relatifs à l’information (IRM) sur les serveurs d’accès au client
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50479201
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver la gestion des droits relatifs à l’information (IRM) sur les serveurs d’accès au client

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Lorsque vous activez la gestion des droits relatifs à l’information (IRM) sur des serveurs d’accès au client, vous activez les fonctionnalités suivantes :

  - Microsoft Office Outlook Web App

  - Gestion des droits relatifs à l’information (IRM) dans Microsoft Exchange ActiveSync

Lorsque la gestion des droits relatifs à l’information (IRM) est activée sur les serveurs d’accès au client, les utilisateurs Outlook Web App peuvent protéger des messages par IRM en appliquant un modèle [Vue d'ensemble des services AD RMS](https://technet.microsoft.com/fr-fr/library/hh831364.aspx) créé sur votre cluster AD RMS. Les utilisateurs Outlook Web App peuvent aussi afficher les messages protégés par IRM et les pièces jointes prises en charge. Avant d’activer l’IRM sur les serveurs d’accès au client, vous devez ajouter la boîte aux lettres de fédération au groupe de super utilisateurs sur le cluster AD RMS.

> [!IMPORTANT]
> Une licence d’utilisation propriétaire est accordée aux membres du groupe de super utilisateurs lorsque ces derniers en font la demande à partir du cluster AD RMS. Ceci leur permet de déchiffrer tout le contenu protégé par les services RMS dans ce cluster.


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Configuration de la gestion des droits relatifs à l’information (IRM) » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un cluster AD RMS doit être installé dans la forêt Active Directory.

  - La boîte aux lettres de fédération a été ajoutée au groupe des super utilisateurs AD RMS. Pour obtenir des instructions détaillées, consultez la rubrique [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Les fonctionnalités IRM doivent être activées pour l’organisation. Pour obtenir des instructions détaillées, consultez la rubrique [Activer ou désactiver la technologie IRM pour les messages internes](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Vous pouvez utiliser la cmdlet **Set-IRMConfiguration** pour activer ou désactiver la gestion des droits relatifs à l’information dans Outlook Web App et dans Exchange ActiveSync pour l’organisation Exchange dans son intégralité ou à certains niveaux.
    
    Vous pouvez également contrôler la fonctionnalité IRM dans Outlook Web App aux niveaux suivants :
    
      - **Répertoire virtuel de Per-Outlook Web App**   Pour activer ou désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel Outlook Web App, utilisez la cmdlet **Set-OWAVirtualDirectory** et définissez le paramètre *IRMEnabled* à `$false` ou `$true` (par défaut). Ainsi, vous pouvez désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel sur un serveur Exchange 2013 Client Access, tout en la conservant activée pour un autre répertoire virtuel sur un autre serveur d’accès au client.
    
      - **Stratégie de la boîte aux lettres Per-Outlook Web App**   Pour activer ou désactiver la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un répertoire virtuel Outlook Web App, utilisez la cmdlet **Set-OWAMailboxPolicy** et définissez le paramètre *IRMEnabled* à `$false` ou `$true` (par défaut). Ainsi, vous pouvez activer la Gestion des droits relatifs à l’information (IRM) dans Outlook Web App pour un ensemble d’utilisateurs et la désactiver pour un autre ensemble d’utilisateurs en leur attribuant une stratégie de boîte aux lettres Outlook Web App différente.
    
    Vous pouvez également contrôler la gestion des droits relatifs à l’information dans Exchange ActiveSync par stratégie de boîte aux lettres Exchange ActiveSync. Pour désactiver ou activer la gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync pour une stratégie de boîte aux lettres Exchange ActiveSync, utilisez la cmdlet **Set-ActiveSyncMailboxPolicy** et définissez le paramètre *IRMEnabled* sur `$false` ou `$true` (valeur par défaut). Ceci vous permet d’activer la gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync pour un ensemble d’utilisateurs et de la désactiver pour un autre groupe d’utilisateurs en leur attribuant une stratégie de boîte aux lettres Exchange ActiveSync différente.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer ou désactiver la gestion des droits relatifs à l’information sur des serveurs d’accès au client. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer la gestion des droits relatifs à l’information sur des serveurs d’accès au client

Cet exemple active la gestion des droits relatifs à l’information sur un serveur d’accès au client pour une organisation Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $true
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver la gestion des droits relatifs à l’information sur des serveurs d’accès au client

Cet exemple désactive la gestion des droits relatifs à l’information sur un serveur d’accès au client pour une organisation Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé la gestion des droits relatifs à l’information sur les serveurs d’accès au client, procédez comme suit :

  - Exécutez la cmdlet **Get-IRMConfiguration**, puis vérifiez la valeur de la propriété *ClientAccessServerEnabled*.
    
    Pour un exemple de la façon de récupérer la configuration IRM, voir [Examples](https://technet.microsoft.com/fr-fr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) dans **Get-IRMConfiguration**.

  - Utiliser Outlook Web App pour créer ou lire un message protégé par IRM.

