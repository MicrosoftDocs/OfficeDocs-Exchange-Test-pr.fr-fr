---
title: 'Utiliser la Sauvegarde Windows Server pour restaurer une sauvegarde d’Exchange: Exchange 2013 Help'
TOCTitle: Utiliser la Sauvegarde Windows Server pour restaurer une sauvegarde d’Exchange
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 50477816
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utiliser la Sauvegarde Windows Server pour restaurer une sauvegarde d’Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-18_

Vous pouvez utiliser la Sauvegarde Windows Server pour sauvegarder et restaurer des bases de données Exchange. Exchange inclut un plug-in pour la Sauvegarde Windows Server vous permettant d’effectuer des sauvegardes basées sur le service VSS (Volume Shadow Copy Service) des données Exchange. Pour plus d’informations, consultez la rubrique [Utilisation de la Sauvegarde Windows Server pour sauvegarder et restaurer des données Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute, plus le temps nécessaire pour restaurer les données

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Récupération de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - La fonctionnalité Sauvegarde Windows Server doit être installée sur l’ordinateur local.

  - Lorsque vous restaurez une base de données vers son emplacement d’origine, cette base peut rester dans un état « Arrêt incorrect » et être montée par le système. Lors de la restauration vers un autre emplacement (par exemple, lors de la préparation pour utiliser une base de données de récupération), la base de données doit être mise manuellement dans un état d’arrêt correct à l’aide des utilitaires de base de données de serveur Exchange (Eseutil.exe).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Utiliser la Sauvegarde de Windows Server pour restaurer une sauvegarde d’Exchange

1.  Démarrez la Sauvegarde Windows Server.

2.  Sélectionnez **Sauvegarde locale**.

3.  Dans le volet Actions, cliquez sur **Récupérer...** pour démarrer l’Assistant Récupération.

4.  Dans la page **Mise en route**, effectuez l’une des opérations suivantes :
    
      - Si les données en cours de récupération ont été sauvegardées sur le serveur local, sélectionnez **Ce serveur (nom du serveur)**, puis cliquez sur **Suivant**.
    
      - Si les données en cours de récupération proviennent d’un autre serveur, ou si la sauvegarde en cours de récupération se situe sur un autre ordinateur, sélectionnez **Un autre serveur**, puis cliquez sur **Suivant**. Dans la page **Spécifiez un type d’emplacement**, sélectionnez **Lecteurs locaux** ou **Dossier partagé distant**, puis cliquez sur **Suivant**. Si vous choisissez **Disques locaux**, sélectionnez le disque contenant la sauvegarde dans la page **Sélectionnez un emplacement de sauvegarde**, puis cliquez sur **Suivant**. Si vous choisissez **Dossier partagé distant**, tapez le chemin UNC des données de sauvegarde dans la page **Spécifiez un dossier distant**, puis cliquez sur **Suivant**.

5.  Dans la page **Sélectionner une date de sauvegarde**, sélectionnez la date et l’heure de la sauvegarde que vous voulez récupérer, puis cliquez sur **Suivant**.

6.  Dans la page **Sélectionnez le type de récupération**, sélectionnez **Applications**, puis cliquez sur **Suivant**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si l’option <strong>Applications</strong> ne peut pas être sélectionnée, cela indique que la sauvegarde sélectionnée pour la restauration était une sauvegarde au niveau du dossier, et non une sauvegarde au niveau du volume. Vous devez effectuer des sauvegardes au niveau du volume lors de la sauvegarde des données Exchange avec la Sauvegarde Windows Server.</td>
    </tr>
    </tbody>
    </table>


7.  Dans la page **Sélectionnez une application**, vérifiez qu’Exchange est sélectionné dans le champ **Applications**. Cliquez sur **Afficher les détails** pour afficher les composants d’application des sauvegardes. Si la sauvegarde en cours de récupération est la plus récente, la case à cocher **Ne pas exécuter une récupération de type restauration par progression des bases de données d’application** sera affichée. Activez cette case si vous voulez empêcher la Sauvegarde Windows Server d’effectuer une implémentation de la restauration en validant tous les journaux de transaction non validés. Cliquez sur **Suivant**.

8.  Sur la page **Spécifiez les options de récupération**, sélectionnez l’emplacement de destination des données récupérées, puis cliquez sur **Suivant**:
    
      - Choisissez **Restaurer à l’emplacement d’origine** si vous souhaitez restaurer les données Exchange directement à leur emplacement d’origine. Si vous utilisez cette option, vous ne pouvez pas choisir les bases de données qui sont restaurées. Toutes les bases de données sauvegardées sur le volume seront restaurées à leur emplacement d’origine.
    
      - Sélectionnez **Restaurer à un autre emplacement** pour restaurer les bases de données et fichiers individuels à un emplacement spécifié. Cliquez sur **Parcourir** pour spécifier l’autre emplacement. Si vous utilisez cette option, vous pouvez choisir les bases de données qui sont restaurées. Après avoir été restaurés, les fichiers de données peuvent être déplacés dans une base de données de récupération, déplacés manuellement vers leur emplacement d’origine ou montés ailleurs dans l’organisation Exchange à l’aide de la [Portabilité des bases de données](database-portability-exchange-2013-help.md). Lorsque vous restaurez des bases de données à un autre emplacement, elles ont été correctement arrêtées. Une fois le processus de restauration terminé, vous aurez besoin d’arrêter correctement la base de données manuellement à l’aide de l’utilitaire Eseutil.exe.

9.  Dans la page **Confirmation**, vérifiez les paramètres de récupération, puis cliquez sur **Récupérer**.

10. Dans la page **Statut de la récupération**, vous pouvez voir le statut et la progression de l’opération de récupération.

11. Cliquez sur **Fermer** lorsque l’opération de récupération est terminée.

## Comment savoir si cela a fonctionné ?

La page **Statut de la récupération** indique si le processus de récupération a été accompli avec succès ou non. Pour vérifier que vous avez bien restauré les données, procédez comme suit :

  - Examinez le répertoire cible de la sauvegarde et vérifiez que les données restaurées existent.

  - Sur le serveur sur lequel la sauvegarde Windows Server a été exécutée, vérifiez que la tâche a été effectuée correctement en affichant les journaux de la sauvegarde.

  - Ouvrez l’Observateur d’événements et vérifiez qu’un événement de fin de restauration a été consigné dans le journal des événements d’applications.

