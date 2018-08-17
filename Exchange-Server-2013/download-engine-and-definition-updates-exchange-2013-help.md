---
title: 'Télécharger les màj des définitions et des moteurs: Exchange 2013 Help'
TOCTitle: Télécharger les mises à jour des définitions et des moteurs
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50478697
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Télécharger les mises à jour des définitions et des moteurs

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Les administrateurs de Microsoft Exchange Server 2013 peuvent télécharger manuellement les mises à jour du moteur anti-programmes malveillants et des définitions (signature). Nous vous recommandons fortement de télécharger les mises à jour du moteur et des définitions sur votre serveur Exchange avant de le mettre en production.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Pour télécharger des mises à jour, votre ordinateur doit pouvoir accéder à Internet et être en mesure d'établir une connexion sur le port TCP 80 (HTTP).

  - UNRESOLVED\_TOKEN\_VAL(PD\_Shell\_Only\_Procedure)

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Anti-programme malveillant » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour télécharger manuellement les mises à jour du moteur et des définitions

Pour télécharger les mises à jour du moteur et des définitions, exécutez la commande suivante :

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

Dans cet exemple, nous téléchargeons les mises à jour du moteur et des définitions sur un serveur nommé mailbox01.contoso.com :

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

Vous pouvez également spécifier le paramètre –EngineUpdatePath qui vous permet de télécharger les mises à jour à partir d’un emplacement autre que celui par défaut de http://forefrontdl.microsoft.com/server/scanengineupdate. Il peut s’agir d’une adresse HTTP ou d’un chemin d’accès UNC ; s’il s’agit de ce dernier, le service réseau doit avoir accès au chemin d’accès. Dans cet exemple, nous téléchargeons les mises à jour du moteur et des définitions à partir d’un répertoire local sur un serveur nommé mailbox01.contoso.com :

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\Server\sharename

## Comment savoir si cela a fonctionné ?

Pour vérifier que le téléchargement des mises à jour s’est correctement effectué, accédez à l’Observateur d’événements et affichez le journal des événements. Nous recommandons de ne filtrer que les événements FIPFS, comme décrit dans la procédure suivante.

1.  Dans le menu **Démarrer**, cliquez sur **Tous les programmes** \> **Outils d’administration** \> **Observateur d’événements**.

2.  Dans l’Observateur d’événements, développez **Journaux Windows**, puis cliquez sur **Application**.

3.  Dans le menu **Action**, cliquez sur **Filtrer le journal actuel**.

4.  Dans la boîte de dialogue **Filtrer le journal actuel**, dans la liste déroulante **Sources de l’événement**, activez la case à cocher **FIPFS**, puis cliquez sur **OK**.

Si le téléchargement des mises à jour du moteur s’est correctement effectué, l’ID d'événement 6033 doit apparaître comme ceci :

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## Pour plus d'informations

[Configurer des stratégies anti-programmes malveillants](configure-anti-malware-policies-exchange-2013-help.md)

