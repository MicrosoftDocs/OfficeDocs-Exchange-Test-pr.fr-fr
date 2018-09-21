---
title: 'Gestion des BDD de BAL dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Gestion des bases de données de boîtes aux lettres dans Exchange 2013
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 50479452
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des bases de données de boîtes aux lettres dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-04-29_

Une base de données de boîtes aux lettres est une unité de granularité où les boîtes aux lettres sont créées et stockées. Une base de données de boîtes aux lettres est stockée sous forme de fichier (.edb) de base de données Exchange. Dans Microsoft Exchange Server 2013, vous pouvez configurer les propriétés spécifiques à chaque base de données de boîtes aux lettres.

Cette rubrique vous indique comment effectuer des tâches de configuration concernant la gestion de vos bases de données de boîtes aux lettres dans Microsoft Exchange Server 2013.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Bases de données de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer une base de données de boîtes aux lettres

## Utiliser le Centre d'administration Exchange (CAE) pour créer une base de données de boîtes aux lettres

1.  Dans le CAE, accédez à **Serveurs**.

2.  Sélectionnez **Bases de données**, puis cliquez sur le symbole **+** pour créer une base de données.

3.  Utilisez l'Assistant Nouvelle base de données pour créer votre base de données.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une base de données de boîtes aux lettres

Pour consulter un exemple de création d'une base de données de boîtes aux lettres, reportez-vous à l'exemple 1 dans [New-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997976\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une base de données, procédez comme suit :

  - Dans le CAE, vérifiez que la base de données de boîtes aux lettres que vous avez créée figure dans la page **Bases de données**.

  - Dans l'environnement de ligne de commande Exchange Management Shell, vérifiez que la base de données a été créée sur le serveur Mailbox01 en exécutant la commande suivante :
    
    ```powershell
Get-MailboxDatabase -Server "Mailbox01"
```

## Obtenir les propriétés d'une base de données de boîtes aux lettres

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour obtenir les propriétés d'une base de données de boîtes aux lettres

Pour consulter un exemple d'obtention des propriétés d'une base de données de boîtes aux lettres, reportez-vous à l'exemple 2 dans [New-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997976\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien récupéré les informations sur la base de données de boîtes aux lettres, procédez comme suit :

Dans l'environnement de ligne de commande Exchange Management Shell, vérifiez que toutes les informations sur votre base de données de boîtes aux lettres sont représentées correctement.

## Définir les propriétés d'une base de données de boîtes aux lettres

## Utiliser le Centre d'administration Exchange (CAE) pour définir les propriétés d'une base de données de boîtes aux lettres

1.  Dans le CAE, accédez à **Serveurs**.

2.  Sélectionnez **Bases de données**, puis sélectionnez la base de données de boîtes aux lettres à configurer.

3.  Cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour configurer les attributs d'une base de données de boîtes aux lettres.

4.  L'onglet **Général** permet d'afficher les informations d'état relatives au chemin d'accès de la base de données de boîtes aux lettres, y compris le chemin d'accès de la base de données de boîtes aux lettres, la dernière sauvegarde et l'état de la base de données de boîtes aux lettres :
    
      - **Chemin d'accès à la base de données**   Ce champ en lecture seule affiche le chemin d'accès complet au fichier de base de données Exchange 2013 (.edb) pour la base de données de boîtes aux lettres sélectionnée. Pour afficher le chemin d'accès complet, cliquez sur le chemin d'accès et utilisez la touche fléchée vers la droite. Vous ne pouvez pas utiliser ce champ pour modifier le chemin d'accès. Pour modifier l'emplacement des fichiers de base de données, utilisez la cmdlet [Move-DatabasePath](https://technet.microsoft.com/fr-fr/library/bb124742\(v=exchg.150\)).
    
      - **Dernière sauvegarde complète**   Ce champ en lecture seule affiche les date et heure de la dernière sauvegarde complète de la base de données de boîtes aux lettres.
    
      - **Dernière sauvegarde incrémentielle**   Ce champ en lecture seule affiche les date et heure de la dernière sauvegarde incrémentielle de la base de données de boîtes aux lettres.
    
      - **État**   Ce champ en lecture seule indique si la base de données de boîtes aux lettres est montée ou démontée.
    
      - **Monté sur le serveur**   Ce champ en lecture seule indique sur quel serveur la base de données est montée.
    
      - **Maître**   Ce champ en lecture seule affiche le serveur maître pour la base de données de boîtes aux lettres. Le serveur de boîtes aux lettres qui héberge la copie active de la base de données est le maître de la base de données de boîtes aux lettres.
    
      - **Type principal**   Ce champ en lecture seule affiche le type de boîte aux lettres de base de données principal.
    
      - **Modifié**   Ce champ en lecture seule affiche les dernières date et heure auxquelles la base de données a été modifiée pour la dernière fois.
    
      - **Serveurs hébergeant une copie de cette base de données**   Ce champ en lecture seule affiche les autres serveurs possédant une copie de cette base de données.

5.  L'onglet **Maintenance** permet de configurer les paramètres de la base de données de boîtes aux lettres, notamment la spécification d'un destinataire de journal, l'établissement d'un planning de maintenance et le montage de la base de données au démarrage :
    
      - **Destinataire du journal**   Cliquez sur **Parcourir** pour spécifier un destinataire afin d'activer la journalisation sur cette base de données de boîtes aux lettres. Supprimez le destinataire répertorié pour désactiver la journalisation.
    
      - **Planification de la maintenance**   Cette liste permet de sélectionner l'une des planifications de maintenance prédéfinies. Vous pouvez également créer une planification personnalisée. Pour configurer une planification personnalisée, cliquez sur **Personnaliser**.
    
      - **Activer la maintenance de la base de données en arrière-plan (analyse ESE 24 h/24, 7 j/7)   **Sélectionnez cette case à cocher pour activer l'analyse en ligne de la base de données, qui s'exécute en continu et en arrière-plan. L'analyse en ligne de la base de données effectue un calcul de somme de contrôle sur la base de données et réalise des opérations permettant à Exchange d'analyser l'espace perdu dans la base de données et de le récupérer. Si cochez cette case, Exchange analyse la base de données une fois par jour au maximum et émet un événement d'avertissement s'il n'est pas en mesure de terminer l'analyse de la base de données sur une période de sept jours.
    
      - **Ne pas monter cette base de données au démarrage**   Activez cette case à cocher pour éviter que Exchange monte la base de données de boîtes aux lettres au démarrage.
    
      - **Cette base de données peut être remplacée par une restauration**   Cochez cette case pour autoriser le remplacement de la base de données de boîtes aux lettres lors d'une procédure de restauration.
    
      - **Activer la journalisation circulaire**   Cliquez sur cette case à cocher pour activer la journalisation circulaire.

6.  L'onglet **Limites** permet de spécifier les limites de stockage, l'intervalle entre les messages d'avertissement et les paramètres de suppression d'une base de données de boîtes aux lettres :
    
      - **Émettre un avertissement à (Go)**   Cette case à cocher permet d'avertir automatiquement les utilisateurs d'une boîte aux lettres que celle-ci approche de la limite de stockage. Pour spécifier la limite de stockage, cochez la case, puis spécifiez en gigaoctets (Go) le volume du contenu pouvant être stocké dans la boîte aux lettres avant l'envoi d'un message électronique d'avertissement aux utilisateurs de la boîte aux lettres. Vous pouvez entrer une valeur comprise entre 0 et 2 097 151 mégaoctets (Mo) (soit 2 téraoctets).
    
      - **Interdire l'envoi à (Go)**   Cochez cette case pour empêcher les utilisateurs d'envoyer de nouveaux messages électroniques lorsque leur boîte aux lettres a atteint la limite spécifiée. Pour spécifier cette limite, cochez la case, puis entrez la taille de la boîte aux lettres en gigaoctets (Go) pour laquelle vous souhaitez interdire l'envoi de nouveaux messages électroniques et en informer les utilisateurs. Vous pouvez entrer une valeur comprise entre 0 et 2 097 151 Mo (soit 2 téraoctets).
    
      - **Interdire l'envoi et la réception à (Go)**   Cochez cette case pour empêcher les utilisateurs d'échanger des messages électroniques quand leur boîte aux lettres a atteint la limite spécifiée. Pour spécifier cette limite, cochez la case, puis tapez la taille de la boîte aux lettres en gigaoctets (Go) pour laquelle vous souhaitez interdire l'envoi et la réception de messages électroniques et en informer les utilisateurs. Vous pouvez entrer une valeur comprise entre 0 et 2 097 151 Mo (soit 2 téraoctets).
    
      - **Conserver les éléments supprimés pendant (jours)**   Cochez cette case pour définir le nombre de jours pendant lesquels les éléments supprimés sont conservés dans une boîte aux lettres. Vous pouvez entrer une valeur comprise entre 0 et 24 855 jours.
    
      - **Conserver les boîtes aux lettres supprimées pendant (jours)**   Cochez cette case pour définir le nombre de jours pendant lesquels les boîtes aux lettres supprimées sont conservées. Vous pouvez entrer une valeur comprise entre 0 et 24 855 jours.
    
      - **Ne pas supprimer définitivement les éléments tant que la base de données n'a pas été sauvegardée**   Cochez cette case pour empêcher la suppression définitive des boîtes aux lettres et des messages électroniques jusqu'à la sauvegarde de la base de données de boîtes aux lettres.

7.  Utilisez l'onglet **Paramètres du client** pour sélectionner le carnet d'adresses en mode hors connexion pour la boîte aux lettres :
    
      - **Carnet d'adresses en mode hors connexion**   Pour sélectionner un carnet d'adresses en mode hors connexion, cliquez sur **Parcourir**, puis sélectionnez le carnet d'adresses en mode hors connexion.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir les propriétés d'une base de données de boîtes aux lettres

Pour un exemple de la façon de définir les propriétés de la base de données de boîtes aux lettres, consultez l'exemple 1 [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les attributs, procédez comme suit :

  - Vérifiez que vos modifications sont enregistrées dans le CAE.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour récupérer les propriétés d'une base de données de boîtes aux lettres.
    
    ```powershell
Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List
```

## Déplacer un chemin d'accès à la base de données de boîtes aux lettres

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Move-DatabasePath](https://technet.microsoft.com/fr-fr/library/bb124742\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour déplacer un chemin d'accès à une base de données de boîtes aux lettres

Pour un exemple de la façon de définir les propriétés de la base de données de boîtes aux lettres, consultez l'exemple 1 [Move-DatabasePath](https://technet.microsoft.com/fr-fr/library/bb124742\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien déplacé le chemin d'accès à la base de données, procédez comme suit :

1.  Dans le CAE, sélectionnez **Serveurs** \> **Bases de données**, puis sélectionnez la boîte aux lettres appropriée.

2.  Cliquez sur le symbole du **stylo** et vérifiez que le chemin d'accès à la base de données est correct.

## Monter une base de données de boîtes aux lettres

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour monter une base de données de boîtes aux lettres

Pour consulter un exemple de montage d'une base de données de boîtes aux lettres, reportez-vous à l'exemple 1 dans [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien monté la base de données de boîte aux lettres, procédez comme suit :

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour récupérer les propriétés de toutes les bases de données de boîtes aux lettres.
    
    ```powershell
Get-MailboxDatabase -IncludePreExchange2013
```

## Démonter une base de données de boîtes aux lettres

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\)).

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour démonter une base de données de boîtes aux lettres

Pour consulter un exemple de démontage d'une base de données de boîtes aux lettres, reportez-vous à l'exemple 1 dans [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement démonté la base de données, procédez comme suit :

1.  Dans le CAE, sélectionnez **Serveurs** \> **Bases de données**, puis sélectionnez la boîte aux lettres appropriée.

2.  Cliquez sur le symbole du **stylo** et vérifiez que l'état de la base de données est **Démonté**.

## Supprimer une base de données de boîtes aux lettres

## Utiliser le Centre d'administration Exchange (CAE) pour supprimer une base de données de boîtes aux lettres

1.  Dans le CAE, sélectionnez **Serveurs** \> **Bases de données**, puis sélectionnez la boîte aux lettres appropriée.

2.  Cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer") pour supprimer la base de données de boîtes aux lettres.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une base de données de boîtes aux lettres

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Remove-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/aa997931\(v=exchg.150\)).

1.  Exécutez la commande suivante pour supprimer la base de données de boîtes aux lettres MyDatabase.
    
    ```powershell
Remove-MailboxDatabase -Identity "MyDatabase"
```

2.  Lorsque vous êtes invité à confirmer l'exécution de cette action, tapez **Y**.

3.  Lorsque la boîte de dialogue s'affiche indiquant que la base de données a été supprimée avec succès, notez l'emplacement du fichier de base de données (.edb) Exchange 2013. Si vous voulez supprimer le fichier du disque dur, vous devez le faire manuellement.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé la base de données de boîtes aux lettres, procédez comme suit :

  - Dans le CAE, accédez à **Serveurs** \> **Bases de données**.

  - Vérifiez que la base de données de boîtes aux lettres a été supprimée.

