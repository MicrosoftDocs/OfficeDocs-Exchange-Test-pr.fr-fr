---
title: 'Configurer des quotas d’archivage local pour une archive personnelle (locale)'
TOCTitle: Configurer des quotas d’archivage local pour une archive personnelle (locale)
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50555511
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer des quotas d’archivage local pour une archive personnelle (locale)

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-12-04_

Lors de déploiements locaux, des archivages locaux sont créés avec des quotas de stockage illimités par défaut. En conséquence, vous devez modifier les propriétés d’une boîte aux lettres pour établir des quotas de stockage pour l’archivage. Vous pouvez définir les quotas suivants pour un archivage :

  - **Quota d’avertissement d’archivage**   Lorsqu’un archivage local dépasse le quota d’avertissement d’archivage spécifié, un événement est consigné à l’attention de l’administrateur d’Exchange et un message d’avertissement est envoyé à l’utilisateur de la boîte aux lettres.

  - **Quota d’archivage**   Lorsqu’un archivage local dépasse le quota d’archivage spécifié, les messages ne sont plus déplacés vers l’archivage et un message d’avertissement est envoyé à l’utilisateur de la boîte aux lettres.

Pour plus d’informations sur les archivages locaux, consultez la rubrique [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Dans le Centre d’administration Exchange (EAC), utilisez la liste déroulante comprenant des valeurs fixes pour configurer le quota d’archivage et le quota d’avertissement d’archivage. Pour définir un quota à une valeur qui n’est pas répertoriées dans le Centre d’administration Exchange (EAC), utilisez l’environnement de ligne de commande Exchange Management Shell.

  - Configurez le quota d’avertissement d’archivage à une valeur inférieure à celle du quota d’archivage. Selon le taux de croissance de l’archivage pour un utilisateur, la différence entre le quota d’avertissement d’archivage et le quota d’archivage doit permettre à l’utilisateur de disposer de suffisamment de temps pour entreprendre les actions appropriées, comme supprimer des éléments de l’archivage ou demander à un administrateur ou au support technique de l’informatique d’accroître le quota d’archivage.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour configurer le quota d’archivage et le quota d’avertissement d’archivage d’une boîte aux lettres

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**

2.  Dans l’affichage de liste, sélectionnez une boîte aux lettres,

3.  Dans le volet de détails, sous **Archivage local**, cliquez sur **Afficher les détails**.

4.  Dans **Boîte aux lettres d’archivage**, utilisez les listes **Valeur de quota (Go)** et **Émettre un avertissement à (Go)** pour sélectionner les valeurs désirées.

5.  Cliquez sur **OK**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le quota d'archivage et le quota d'avertissement d'archivage d'une boîte aux lettres

Dans cet exemple, nous définissons le quota d’archivage de la boîte aux lettres de Chris Ashton à 10 gigaoctet (Go) et à partir de quel moment l’utilisateur doit recevoir un message d’avertissement signalant que l’archivage local est plein et qu’il ne sera plus possible de déplacer des éléments vers l’archivage. Dans cet exemple, nous définissons également le quota d’avertissement d’archivage à 9,5 Go et à quel moment l’utilisateur doit recevoir un message d’avertissement signalant que l’archivage local est presque plein.

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier l'activation avec succès d'une archive locale avec une boîte aux lettres existante, exécutez l'une des actions suivantes :

  - Dans le centre d’administration Exchange, accédez à **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez la boîte aux lettres de votre choix. Dans le volet de détails, sous **Archivage local**, cliquez sur **Afficher les détails** et vérifiez les paramètres de quota de l’archivage.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher des informations de quota concernant l’archivage.
    
        Get-Mailbox <Name> | FL Name,Archive*Quota

