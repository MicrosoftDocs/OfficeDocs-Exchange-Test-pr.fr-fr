---
title: 'Désactiver la publication des calendriers Internet: Exchange 2013 Help'
TOCTitle: Désactiver la publication des calendriers Internet
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50555518
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver la publication des calendriers Internet

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-15_

La manière dont vous désactivez une publication de calendrier Internet dépend de la façon dont vous l’avez activée. Si vous avez créé un stratégie de partage dédiée à la publication de calendrier Internet, vous pouvez désactiver la stratégie ou la supprimer en même temps. Si vous avez configuré une publication de calendrier Internet en tant que règle de partage dans une stratégie de partage par défaut, vous pouvez simplement retirer la règle de partage pour le domaine **Anonyme**.

Lorsque vous désactivez une publication de calendrier Internet, les utilisateurs configurés pour utiliser la stratégie de partage ne seront plus en mesure de partager des informations de calendriers via le domaine Internet **Anonyme** spécifié dans la stratégie. Notez que vous ne pouvez ni supprimer ni désactiver une stratégie de partage dédiée à une publication de calendrier Internet tant que tous les utilisateurs qui sont configurés pour utiliser cette stratégie n’ont pas retiré le paramétrage de cette stratégie de leur boîte aux lettres. Pour plus d’informations sur la modification du paramétrage de la stratégie de partage pour un utilisateur, consultez la rubrique [Gestion des boîtes aux lettres utilisateur](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).

> [!NOTE]
> Si vous désactivez ou supprimez une stratégie de partage, les utilisateurs configurés pour utiliser la stratégie continuent à partager des informations jusqu’a ce que l’Assistant Stratégie de partage soit exécuté. Pour indiquer la fréquence d'exécution de l'Assistant Stratégie de partage, utilisez la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/aa998651(v=exchg.150)">Set-MailboxServer</a> avec le paramètre <em>SharingPolicySchedule</em>.


Pour désactiver complètement la publication de calendriers Internet, vous devez également désactiver le répertoire virtuel d’Outlook Web App utilisé pour la publication des calendriers. Cette opération interdit l’accès aux liens des calendriers publiés et partagés antérieurement par les utilisateurs de votre organisation Exchange avec les utilisateurs externes sur Internet. Cette étape est décrite ci-après dans cette rubrique.

Pour en savoir plus sur la publication Internet de calendriers et les stratégies de partage, consultez la rubrique [Partage](sharing-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations de calendrier et de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Utiliser le Centre d’administration Exchange (EMC) ou l’environnement Shell pour désactiver ou supprimer la stratégie de partage pour la publication des calendriers Internet

## Utilisation du CAE

1.  Accédez à **Organisation**\>**Partage**.

2.  Dans l’affichage de liste, sous **Partage individuel**, exécutez l’une des étapes suivantes :
    
      - Si vous avez créé une stratégie de partage spécifiquement pour la publication de calendrier Internet, sélectionnez cette stratégie, puis décochez l’option dans la colonne **Activé** pour désactiver la stratégie de partage ou cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer") pour la supprimer.
    
      - Si vous avez configuré une publication de calendrier Internet en tant que règle de partage dans la stratégie de partage par défaut, procédez comme suit :
        
        1.  Sélectionnez la stratégie de partage par défaut, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
        
        2.  Dans **stratégie de partage**, sélectionnez la règle de partage **Anonyme**, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour supprimer la règle de partage.
        
        3.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell

Cet exemple illustre la désactivation d’une stratégie de partage de publication des calendriers Internet dédiée nommée **Internet**.

    Set-SharingPolicy -Identity "Internet" -Enabled $false

Cet exemple illustre la suppression d’une stratégie de partage de publication des calendriers Internet dédiée nommée **Internet**.

    Remove-SharingPolicy -Identity "Internet"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd297931\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que la suppression ou la mise à jour de la stratégie de partage s’est effectuée correctement, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell suivante et vérifiez les informations relatives à la stratégie de partage.

    Get-SharingPolicy <policy name> | format-list

Si vous avez supprimé une stratégie de partage de publication des calendriers Internet dédiée, vous ne devez plus voir la stratégie dans les résultats de la cmdlet.

Si vous avez mis à jour la stratégie de partage par défaut, vérifiez que le domaine `Anonymous` a été supprimé du paramètre *Domains*.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd335081\(v=exchg.150\)).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Étape 2 : Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver les fonctions Anonyme du répertoire virtuel d’Outlook Web App

> [!NOTE]
> Vous ne pouvez pas utiliser le CAE pour désactiver les fonctions Anonyme du répertoire virtuel d’Outlook Web App.


Cet exemple illustre la désactivation des fonctions Anonyme pour le répertoire virtuel d’Outlook Web App sur le serveur d’accès au client CAS01.

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement désactivé les fonctions Anonyme pour le répertoire virtuel d’Outlook Web App sur le serveur d’accès au client, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell et vérifiez que la valeur du paramètre *AnonymousFeaturesEnabled* est `$false`.

    Get-OwaVirtualDirectory | format-list

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/aa998588\(v=exchg.150\)).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

