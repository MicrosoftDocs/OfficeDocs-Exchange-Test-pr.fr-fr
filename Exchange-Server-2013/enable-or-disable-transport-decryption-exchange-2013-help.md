---
title: 'Activer ou désactiver le déchiffrement du transport: Exchange 2013 Help'
TOCTitle: Activer ou désactiver le déchiffrement du transport
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50478021
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver le déchiffrement du transport

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Décryptage de transport activation permet à l’agent de règles de Transport sur Microsoft Exchange Server 2013 des serveurs de boîtes aux lettres accéder au contenu de messages protégés par Information Rights Management (IRM). Par conséquent, autres agents de transport peuvent accéder au contenu du message et éventuellement apporter des modifications. Par exemple, l’agent de règles de Transport devrez inspecter le contenu du message et d’appliquer des règles de transport (par exemple, les règles qui s’appliquent d’une décharge de responsabilité au message). Pour déchiffrer les messages protégés par IRM avec succès, vous devez ajouter la boîte aux lettres fédéré de remise pour le groupe de super utilisateurs configuré sur votre serveur de [Services AD RMS (Active Directory Rights Management Services) (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .

> [!IMPORTANT]
> Une licence d’utilisation propriétaire est accordée aux membres du groupe de super utilisateurs lorsque ces derniers en font la demande à partir du cluster AD RMS. Cela leur permet de déchiffrer tout le contenu protégé par IRM qui a été créé par ce cluster.


Lors de l’activation du déchiffrement du transport, vous pouvez spécifier les paramètres suivants :

  - **Obligatoire**   Rejette les messages qui ne peuvent pas être déchiffrés et renvoie une notification d’échec de remise à l’expéditeur.

  - **Facultatif**   Utilise une meilleure approche pour le déchiffrement. Si possible, les messages sont déchiffrés et remis même en cas d’échec du déchiffrement. Il s’agit du paramètre par défaut.

Pour plus d’informations sur le déchiffrement du transport, voir [Déchiffrement du transport](transport-decryption-exchange-2013-help.md).

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un serveur AD RMS existe dans la forêt Active Directory et est accessible.

  - La boîte aux lettres de remise fédérée a été ajoutée au groupe de super utilisateurs AD RMS. Pour plus d’informations, voir [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour activer le déchiffrement de transport. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour activer le déchiffrement du transport

Cet exemple active le déchiffrement de transport pour l’organisation Exchange 2013. Les messages qui ne peuvent pas être déchiffrés sont rejetés et un rapport de non-remise est renvoyé à l’expéditeur.

    Set-IRMConfiguration -TransportDecryptionSetting Mandatory

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour désactiver le déchiffrement du transport

Cet exemple désactive le déchiffrement de transport pour l’organisation Exchange 2013.

    Set-IRMConfiguration -TransportDecryptionSetting Disabled

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez effectivement activé ou désactivé le déchiffrement de transport, utilisez la cmdlet **Get-IRMConfiguration** et vérifiez la valeur de la propriété *JournalDecryptionEnabled*.

Pour un exemple sur la manière de vérifier la configuration IRM, voir [Examples](https://technet.microsoft.com/fr-fr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) dans **Get-IRMConfiguration**.

