---
title: 'Activer la publication Internet des calendriers: Exchange 2013 Help'
TOCTitle: Activer la publication Internet des calendriers
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50555468
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer la publication Internet des calendriers

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-08-22_

**Résumé** : Utilisez ces procédures pour permettre aux utilisateurs OWA de votre organisation Exchange 2013 de partager des informations de disponibilité du calendrier avec des organisations externes.

Les utilisateurs des organisations Microsoft Exchange Server 2013 peuvent partager leurs informations de disponibilité (disponible/occupé) de calendrier avec des utilisateurs appartenant à des organisations non Exchange et d’autres personnes disposant d’un accès Internet. La fonctionnalité de publication Internet des calendriers apporte davantage de flexibilité et accroît le nombre des utilisateurs pouvant partager des informations de disponibilité de calendrier.

Le processus d’activation de cette fonctionnalité consiste en trois étapes générales :

1.  Configurez l’URL de proxy web pour le serveur de boîte aux lettres (cette étape est nécessaire uniquement si une URL de proxy web existe déjà dans votre organisation, sinon, passez à l’étape 2).

2.  Activer le répertoire virtuel de publication pour le serveur d’accès au client.

3.  Créer une stratégie de partage dédiée et spécifique de la publication Internet des calendriers ou mettre à jour la stratégie de partage par défaut pour prendre en charge le domaine **Anonyme**. Quelle que soit la méthode employée, celle-ci permet aux utilisateurs de votre organisation Exchange d’inviter d’autres utilisateurs disposant d’un accès Internet à consulter des informations limitées de disponibilité de calendrier via une adresse URL publiée.

> [!IMPORTANT]
> À la fin de l’étape 3, les utilisateurs doivent publier leurs calendriers à partir d’Outlook. La publication des calendriers crée des URL que les utilisateurs peuvent donner à des contacts en dehors de leur organisation. Une URL permet aux destinataires de s’abonner à des calendriers à l’aide d’Outlook ou d’Outlook Web App, et l’autre permet aux destinataires d’afficher un calendrier dans un navigateur web. Chaque utilisateur peut contrôler la quantité de détails visibles.


Pour connaître les tâches de gestion supplémentaires relatives aux stratégies de partage, consultez la rubrique [Stratégies de partage](sharing-policies-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations de calendrier et de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Un serveur d’accès au client Exchange 2013 existe dans l’organisation Exchange qui partage les informations de calendrier des utilisateurs.

  - Les boîtes aux lettres utilisateur sont sur des serveurs de boîtes aux lettres Exchange 2013 dans l’organisation Exchange qui partage les informations de calendrier des utilisateurs.

  - Seuls les utilisateurs d’Outlook 2010 (ou version ultérieure) et d’Outlook Web App peuvent créer des invitations de partage.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer l’URL du proxy Web

> [!NOTE]
> Cette étape est nécessaire uniquement si une URL de proxy web existe déjà dans votre organisation. Si ce n’est pas le cas, passez à l’étape 2.
> Vous ne pouvez pas utiliser le Centre d’Administration Exchange (CAE) pour configurer l’URL du proxy web.


Cet exemple configure une URL du proxy Web sur le serveur de boîtes aux lettres MAIL01.

    Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ExchangeServer](https://technet.microsoft.com/fr-fr/library/bb123716\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que la configuration de l’adresse URL du proxy Web a été correctement effectuée, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell suivante et vérifiez les informations du paramètre *InternetWebProxy*.

    Get-ExchangeServer | format-list

## Étape 2 : Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer le répertoire virtuel de publication

> [!NOTE]
> Vous ne pouvez pas utiliser le CAE pour créer un répertoire virtuel de publication.


Cet exemple active le répertoire virtuel de publication sur le serveur d’accès au client CAS01.

    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true

Où l’identité `CAS01\owa (Default Web Site)` est à la fois le nom du serveur et le répertoire virtuel Outlook Web App.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que l’activation du répertoire virtuel de publication s’est correctement effectuée, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell suivante et vérifiez les informations du paramètre *ExternalURL*.

    Get-OwaVirtualDirectory | format-list

## Étape 3 : Créer ou configurer une stratégie de partage exclusivement consacrée à la publication Internet de calendriers

> [!NOTE]
> Les options suivantes de l’étape 3 s’appliquent uniquement aux environnements Exchange Online.


Vous pouvez créer une stratégie de partage pour la publication Internet de calendriers (option 1) ou configurer la stratégie de partage par défaut pour la publication Internet de calendriers (option 2). Les deux options vous donnent le choix d’utiliser le Centre d’administration Exchange ou le Shell.

## Option 1 : Créer une stratégie de partage exclusivement consacrée à la publication Internet de calendriers

Pour créer une stratégie de partage spécifiquement pour la publication Internet des calendriers, procédez comme suit.

## Utilisation du CAE

1.  Accédez à **Organisation**\>**Partage**.

2.  Dans l’affichage de liste, sous **Partage individuel**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans **Stratégie de partage**, entrez un nom convivial pour la stratégie de partage dans le champ **Nom de la stratégie** (par exemple **Internet**.

4.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour définir les règles de partage pour la stratégie de partage.

5.  Dans **Règle de partage**, cliquez sur **Partage avec un domaine spécifique**, puis entrez **Anonymous** dans la zone correspondante.

6.  Pour spécifier les niveaux de partage de calendrier à appliquer pour la stratégie de partage, activez la case à cocher **Partager votre dossier de calendrier**, puis sélectionnez l’une des cases d’options suivantes :
    
      - **Informations de disponibilité de calendrier avec les heures de disponibilité uniquement**
    
      - **Informations de disponibilité de calendrier avec heure, objet et lieu**
    
      - **Toutes les informations de calendrier des rendez-vous, y compris l’heure, l’objet, le lieu et le titre**

7.  Cliquez sur **Enregistrer** pour définir les règles de la stratégie de partage.

8.  Dans **Stratégie de partage**, cliquez sur **Enregistrer** pour créer la stratégie.

## Utiliser l’environnement de ligne de commande Exchange Management Shell

Dans cet exemple, nous créons une stratégie de partage de publication Internet de calendriers intitulée « Internet » et configurons la stratégie afin de partager uniquement les informations de disponibilité. La stratégie est activée.

    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Cet exemple ajoute la stratégie de partage Internet à la boîte aux lettres d’un utilisateur.

    Set-Mailbox -Identity <user name> -SharingPolicy "Internet"

Cet exemple ajoute la stratégie de partage Internet à une unité d’organisation.

    Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [New-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd298186\(v=exchg.150\)) et [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que la création de la stratégie de partage s’est effectuée correctement, exécutez la commande de l’environnement de ligne de commande Exchange Management Shell suivante et vérifiez les informations relatives à la stratégie de partage.

    Get-SharingPolicy <policy name> | format-list

## Option 2 : Configurer la stratégie de partage par défaut pour la publication des calendriers Internet

Pour configurer la stratégie de partage par défaut pour la publication Internet des calendriers, procédez comme suit.

## Utilisation du CAE

1.  Accédez à **Organisation**\>**Partage**.

2.  Dans l’affichage de liste, sous **Partage individuel**, sélectionnez une stratégie de partage par défaut, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **Stratégie de partage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter une règle de partage à la stratégie.

4.  Dans **Règle de partage**, cliquez sur **Partage avec un domaine spécifique**, puis entrez **Anonymous** dans la zone correspondante.

5.  Pour spécifier les niveaux de partage de calendrier à appliquer pour la stratégie de partage, activez la case à cocher **Partager votre dossier de calendrier**, puis sélectionnez l’une des cases d’options suivantes :
    
      - **Informations de disponibilité de calendrier avec les heures de disponibilité uniquement**
    
      - **Informations de disponibilité de calendrier avec heure, objet et lieu**
    
      - **Toutes les informations de calendrier des rendez-vous, y compris l’heure, l’objet, le lieu et le titre**

6.  Cliquez sur **Enregistrer** pour définir les règles de la stratégie de partage.

7.  Dans **Stratégie de partage**, cliquez sur **Enregistrer** pour enregistrer les modifications.

## Utiliser l’environnement de ligne de commande Exchange Management Shell

Dans cet exemple, nous mettons à jour la stratégie de partage par défaut et configurons la stratégie pour ne partager que des informations de disponibilité. La stratégie est activée.

    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que la mise à jour de la stratégie de partage par défaut s’est effectuée correctement, exécutez la commande suivante de l’environnement de ligne de commande Exchange Management Shell pour vérifier les informations de la stratégie de partage.

    Get-SharingPolicy <policy name> | format-list

