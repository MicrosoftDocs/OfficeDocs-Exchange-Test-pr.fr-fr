---
title: 'Gestion de l’accès des utilisateurs aux applications pour Outlook'
TOCTitle: Gestion de l’accès des utilisateurs aux applications pour Outlook
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52063015
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de l’accès des utilisateurs aux applications pour Outlook

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2018-04-17_

Vous pouvez utiliser le Centre d’administration Exchange (EAC) ou Exchange PowerShell pour gérer l’accès utilisateur aux compléments pour Outlook.

  - À l’aide du CAE, vous pouvez gérer les paramètres d’accès de base aux compléments pour les utilisateurs au niveau de l’organisation. Par exemple, vous pouvez configurer si un complément est activé ou désactivé pour les utilisateurs. Vous pouvez également spécifier si l’utilisation d’un complément est obligatoire ou facultative pour les utilisateurs.

  - Grâce à l’environnement de ligne de commande Exchange Management Shell ou Exchange Online PowerShell, vous pouvez gérer les mêmes paramètres que dans le CAE, ainsi que d’autres. Par exemple, vous pouvez limiter la disponibilité d’une application à des utilisateurs spécifiques au sein de votre organisation.

Pour des tâches de gestion supplémentaires, consultez la rubrique [Applications pour Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Pour plus d’informations sur le Centre d’administration Exchange, consultez la rubrique [Centre d’administration Exchange dans Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) ou [Centre d’administration Exchange dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj200743\(v=exchg.150\)).

  - Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Compléments pour Outlook » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Spécifier si un complément est disponible, activé ou désactivé

## Utiliser le Centre d’administration Exchange pour spécifier si un complément est disponible, activé ou désactivé

1.  Dans le CAE, accédez à **Organisation** \> **Compléments**.

2.  Dans la vue Liste, sélectionnez le complément pour lequel vous souhaitez modifier les paramètres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Si vous ne voulez pas que les utilisateurs puissent utiliser le complément, désélectionnez la case **Mettre ce complément à disposition des utilisateurs dans votre organisation**, puis cliquez sur **Enregistrer**.

4.  Si vous voulez que les utilisateurs puissent utiliser le complément, cochez la case **Mettre ce complément à disposition des utilisateurs dans votre organisation**, puis sélectionnez l’option souhaitée.
    
      - **Facultatif, option activée par défaut :**  utilisez ce paramètre si vous souhaitez autoriser les utilisateurs à désactiver le complément.
    
      - **Facultatif, option désactivée par défaut :**  utilisez ce paramètre si vous souhaitez autoriser les utilisateurs à activer le complément.
    
      - **Obligatoire, option toujours activée. Les utilisateurs ne peuvent pas désactiver ce complément :**  utilisez ce paramètre si vous ne voulez pas que les utilisateurs puissent désactiver le complément.

5.  Cliquez sur **Enregistrer**.

## Utiliser Exchange PowerShell pour spécifier si un complément est disponible, activé ou désactivé

Exécutez d’abord la commande suivante pour rechercher les noms d’affichage et les ID de complément pour tous les compléments pour Outlook installés au sein de votre organisation.

    Get-App -OrganizationApp | Format-List DisplayName,AppId

La valeur **AppId** représente un GUID qui identifie le complément de manière unique (par exemple, `fe93bfe1-7947-460a-a5e0-7a5906b51360`). Vous utilisez la valeur **AppId** pour identifier et modifier les paramètres du complément.

Pour désactiver et masquer un complément à partir de tous vos utilisateurs, remplacez *\<AppId\>* par la valeur **AppId** réelle et exécutez la commande suivante :

    Set-App -Identity <AppId> -OrganizationApp -Enabled $false

Pour activer un complément par défaut, mais autoriser vos utilisateurs à le désactiver, remplacez *\<AppId\>* par la valeur **AppId** réelle et exécutez la commande suivante :

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Enabled

Pour désactiver un complément par défaut, mais autoriser vos utilisateurs à l’activer, remplacez *\<AppId\>* par la valeur **AppId** réelle et exécutez la commande suivante :

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Disabled

Si vous souhaitez que le complément soit obligatoire pour tous vos utilisateurs, remplacez *\<AppId\>* par la valeur **AppId** réelle et exécutez la commande suivante :

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser AlwaysEnabled

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [Set-App](https://technet.microsoft.com/fr-fr/library/jj218630\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré un complément, utilisez l’une des méthodes suivantes :

  - Dans le centre d’administration Exchange, accédez à **Organisation** \> **Compléments** et passer en revue les valeurs dans les colonnes **Utilisateur par défaut** et **Fourni à**.

  - Dans Exchange Online PowerShell, exécutez la commande suivante et vérifier les valeurs des propriétés **DefaultStateForUser** et **Enabled** :
    
        Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser

## Utiliser Exchange PowerShell pour limiter la disponibilité d’un complément à des utilisateurs spécifiques

Vous ne pouvez pas utiliser le Centre d’administration Exchange pour limiter la disponibilité d’un complément à des utilisateurs spécifiques. Vous pouvez utiliser uniquement l’environnement de ligne de commande Exchange Management Shell ou Exchange Online PowerShell.

Cet exemple limite le complément LinkedIn avec la valeur **AppId** hypothétique `ac83a9d5-5af2-446f-956a-c583adc94d5e` pour les membres du groupe de distribution nommé Marketing.

    $a = Get-DistributionGroupMember Marketing

    Set-App -Identity ac83a9d5-5af2-446f-956a-c583adc94d5e -OrganizationApp -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [Set-App](https://technet.microsoft.com/fr-fr/library/jj218630\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement limité la disponibilité d’un complément à des utilisateurs spécifiques, exécutez la commande suivante dans Exchange PowerShell et vérifiez la valeur des propriétés **ProvidedTo** et **UserList** :

    Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser,ProvidedTo,UserList

