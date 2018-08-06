---
title: 'Utilis. la sauvegarde Windows Server pour sauveg. Exchange: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Utiliser la sauvegarde Windows Server pour sauvegarder Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50477687
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utiliser la sauvegarde Windows Server pour sauvegarder Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-18_

Vous pouvez utiliser la Sauvegarde Windows Server pour sauvegarder et restaurer des bases de données Exchange. Exchange contient un plug-in pour la Sauvegarde Windows Server vous permettant d’effectuer des sauvegardes basées sur le service VSS (Volume Shadow Copy Service) des données Exchange.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 1 minute, plus le temps nécessaire pour sauvegarder les données

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Récupération de boîte aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - La fonctionnalité Sauvegarde Windows Server doit être installée sur l’ordinateur local.

  - Lors de l’opération de sauvegarde, une vérification de la cohérence des fichiers de données Exchange est réalisée pour s’assurer que les fichiers sont en bon état et qu’ils peuvent être utilisés à des fins de récupération. Si la vérification de la cohérence réussit, les données Exchange peuvent être récupérées à partir de cette sauvegarde. Dans le cas contraire, les données Exchange ne peuvent pas être récupérées. La sauvegarde Windows Server exécute la vérification de la cohérence sur la capture instantanée prise pour la sauvegarde. Ainsi, avant de copier les fichiers de la capture instantanée vers le média de sauvegarde, la cohérence de la sauvegarde est connue et l’utilisateur reçoit les résultats de la vérification de la cohérence.

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser la Sauvegarde Windows Server pour effectuer une sauvegarde d’Exchange

1.  Démarrez la Sauvegarde Windows Server.

2.  Sélectionnez **Sauvegarde locale**.

3.  Dans le volet Actions, cliquez sur **Sauvegarde unique...** pour démarrer l’Assistant Sauvegarde unique.

4.  Sur la page **Options de sauvegarde**, sélectionnez **D’autres options**, puis cliquez sur **Suivant**.

5.  Sur la page **Sélectionner la configuration de la sauvegarde**, sélectionnez **Personnalisée**, puis cliquez sur **Suivant**.

6.  Sur la page **Sélectionner les éléments à sauvegarder**, cliquez sur **Ajouter des éléments** pour sélectionner les volumes à sauvegarder, puis cliquez sur **OK**.
    
    > [!NOTE]
    > Choisissez des volumes et non des dossiers individuels. La seule façon d’effectuer une sauvegarde ou une restauration de niveau application est de sélectionner un volume entier.


7.  Cliquez sur **Paramètres avancés**. Sur l’onglet **Exclusions**, cliquez sur **Ajouter une exclusion** pour ajouter des fichiers ou types de fichiers que vous souhaitez exclure de la sauvegarde.
    
    > [!NOTE]
    > Par défaut, les volumes contenant les composants ou applications du système d’exploitation sont inclus dans la sauvegarde et ne peuvent pas être exclus.


8.  Sur l’onglet **Paramètres VSS**, sélectionnez **Sauvegarde complète VSS**, cliquez sur **OK**, puis sur **Suivant**.

9.  Sur la page **Spécifier le type de destination**, sélectionnez l’emplacement de stockage de la sauvegarde, puis cliquez sur **Suivant**.
    
      - Si vous choisissez **Lecteurs locaux**, la page **Sélectionner la destination de sauvegarde** s’affiche. Sélectionnez une option dans la liste déroulante **Destination de sauvegarde**, puis cliquez sur **Suivant**.
    
      - Si l’option **Dossier partagé distant** est activée, la page **Spécifier un dossier distant** s’affiche. Spécifiez un chemin d’accès UNC pour les fichiers de sauvegarde, configurez les paramètres de contrôle d’accès. Choisissez **Ne pas hériter** si vous souhaitez que la sauvegarde ne soit accessible que via un compte spécifique. Entrez le nom d’utilisateur et le mot de passe d’un compte disposant d’autorisations d’écriture sur l’ordinateur qui héberge le dossier distant, puis cliquez sur **OK**. Vous pouvez également choisir **Hériter** si vous voulez que la sauvegarde soit accessible par tous les utilisateurs ayant accès au dossier distant. Cliquez sur **Suivant**.

10. Dans la page **Confirmation**, vérifiez les paramètres de sauvegarde, puis cliquez sur **Sauvegarder**.

11. Sur la page **Progression de la sauvegarde**, vous pouvez voir l’état et la progression de l’opération de sauvegarde.

12. Cliquez sur **Fermer** pour quitter la page **Progression de la sauvegarde** à tout moment. Les sauvegardes en cours continueront de s’exécuter en arrière-plan.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement sauvegardé les données, procédez comme suit :

  - Sur le serveur sur lequel la Sauvegarde Windows Server a été exécutée, le dernier état de sauvegarde est affiché, ce doit être Réussite. Vous pouvez également vérifier que la sauvegarde s’est terminée avec succès en affichant les journaux de la Sauvegarde Windows Server.

  - Ouvrez l’observateur d’événements et vérifiez qu’un événement d’achèvement de sauvegarde a été consigné dans le journal d’événements d’applications.

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell pour vérifier que chaque base de données sur les volumes sélectionnés a été correctement sauvegardée :
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    Les propriétés *SnapshotLastFullBackup* et *LastFullBackup* de la base de données indiquent quand la dernière sauvegarde réussie a eu lieu, et s’il s’agissait d’une sauvegarde complète VSS.

