---
title: "Gestion des messages dans les files d'attente: Exchange 2013 Help"
TOCTitle: Gestion des messages dans les files d'attente
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51407209
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des messages dans les files d'attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-05-07_

Dans Microsoft Exchange Server 2013, vous pouvez utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange ou l'environnement de ligne de commande Exchange Management Shell pour gérer les messages dans les files d'attente. Pour plus d'informations sur l'utilisation des cmdlets de gestion des messages dans l'environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Files d'attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Supprimer des messages dans les files d'attente

Un message envoyé à plusieurs destinataires pourrait se trouver dans plusieurs files d'attente. Pour supprimer un message de plusieurs files d'attente en une seule opération, vous devez utiliser un filtre. Vous pouvez choisir d'envoyer ou non une notification d'échec de remise lorsque vous supprimez des messages d'une file d'attente. Vous ne pouvez pas supprimer un message de la file d'attente de soumission.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour supprimer des messages

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Messages**. La liste de tous les messages sur le serveur auquel vous êtes connecté s'affiche. Pour ajuster l'action sur une seule file d'attente, cliquez sur l'onglet **Files d'attente**, double-cliquez sur le nom de la file d'attente, puis cliquez sur l'onglet *Serveur\\File d'attente* qui s'affiche.

4.  Sélectionnez un ou plusieurs messages dans la liste, cliquez dessus avec le bouton droit, puis sélectionnez **Supprimer les messages (avec rapport de non-remise)** ou **Supprimer les messages (sans envoyer de rapport de non-remise)**. Une boîte de dialogue confirmant l'action sélectionnée et demandant **Voulez-vous continuer ?** s'affiche. Cliquez sur **Oui**.

5.  Pour supprimer tous les messages d'une file d'attente en particulier, cliquez sur l'onglet **Files d'attente**. Sélectionnez une file d'attente, cliquez dessus avec le bouton droit, puis sélectionnez **Supprimer les messages (avec rapport de non-remise)** ou **Supprimer les messages (sans envoyer de rapport de non-remise)**. Une boîte de dialogue confirmant l'action sélectionnée et demandant **Voulez-vous continuer ?** s'affiche. Cliquez sur **Oui**.
    
    > [!NOTE]
    > Si vous travaillez avec une liste filtrée, la page affichée peut ne pas inclure tous les éléments du filtre. Dans ce cas, une invite apparaît et indique : <strong>Cette action affectera tous les éléments de cette page. Pour étendre la portée de cette action afin d'inclure tous les éléments dans ce filtre, cochez la case suivante avant de cliquer sur OK.</strong>


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer des messages

Pour supprimer des messages des files d'attente, utilisez la syntaxe suivante :

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

Cet exemple supprime les messages dont l'objet est « Win Big » dans les files d'attente sans envoyer de rapport de non-remise.

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

Cet exemple supprime le message portant l'ID de message 3 de la file d'attente inaccessible sur le serveur Mailbox01 et envoie un rapport de non-remise.

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé les messages des files d'attente, procédez comme suit :

  - Dans l'Afficheur des files d'attente, sélectionnez la file d'attente ou créez un filtre permettant de vérifier que les messages n'existent plus.

  - Utilisez la cmdlet **Get-Message** avec le paramètre *Queue* ou *Filter* pour vérifier que les messages n'existent plus. Pour plus d'informations, consultez la rubrique [Get-Message](https://technet.microsoft.com/fr-fr/library/bb124738\(v=exchg.150\)).

## Reprise des messages en files d'attente

Vous pouvez reprendre un message dont l'état est Suspendu. En reprenant un message, vous permettez sa remise. Si vous reprenez un message figurant dans la file d'attente de messages incohérents, le message est envoyé au catégoriseur pour traitement. Un message en cours d'envoi à plusieurs destinataires pourrait se trouver dans plusieurs files d'attente. Pour reprendre un message dans plusieurs files d'attente en une seule opération, vous devez utiliser un filtre.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour reprendre des messages

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Messages**. La liste de tous les messages sur le serveur auquel vous êtes connecté s'affiche. Pour ajuster l'action afin de se concentrer sur une seule file d'attente, cliquez sur l'onglet **Files d'attente**, double-cliquez sur le nom de la file d'attente, puis cliquez sur l'onglet *Serveur\\File d'attente* qui s'affiche.

4.  Cliquez sur **Créer un filtre**, puis entrez l'expression du filtre comme suit :
    
    1.  Dans la liste déroulante des propriétés de message, sélectionnez **État**.
    
    2.  Dans la liste déroulante des opérateurs de comparaison, sélectionnez **Est égal à**.
    
    3.  Dans la liste déroulante des valeurs, sélectionnez **Suspendu**.

5.  Cliquez sur **Appliquer le filtre**. Tous les messages dont l'état est Suspendu s'affichent.

6.  Sélectionnez un ou plusieurs messages, cliquez dessus avec le bouton droit, puis sélectionnez **Reprendre**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour reprendre des messages

Pour reprendre des messages, utilisez la syntaxe suivante :

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

Cet exemple indique comment reprendre tous les messages envoyés par un expéditeur faisant partie du domaine Contoso.com.

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

Cet exemple montre comment reprendre le message avec l'ID 3 dans la file d'attente inaccessible sur le serveur Hub01.

    Resume-Message -Identity Hub01\Unreachable\3

Pour renvoyer des messages de la file d'attente de messages incohérents, procédez comme suit :

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien repris les messages dans les files d'attente, procédez comme suit :

  - Dans l'Afficheur des files d'attente, sélectionnez la file d'attente ou créez un filtre permettant de vérifier que les messages n'ont plus l'état Suspendu.

  - Utilisez la cmdlet **Get-Message** avec le paramètre *Queue* ou *Filter* pour vérifier que les messages n'ont plus l'état Suspendu. Pour plus d'informations, consultez la rubrique [Get-Message](https://technet.microsoft.com/fr-fr/library/bb124738\(v=exchg.150\)).

Notez que si vous ne trouvez le message dans aucune des files d'attente sur le serveur, cela signifie probablement que le message a bien été remis au saut suivant.

## Suspendre des messages en files d'attente

Quand vous suspendez un message, vous empêchez sa remise. Un message qui apparaît dans la file d'attente mais qui est déjà en cours de remise n'est pas suspendu. La remise se poursuit et l'état du message est **PendingSuspend**. En cas d'échec de la remise, le message retourne dans la file d'attente, puis est suspendu. Vous ne pouvez pas suspendre un message figurant dans la file d'attente de soumission ou la file d'attente de messages incohérents.

Un message en cours d'envoi à plusieurs destinataires pourrait se trouver dans plusieurs files d'attente. Pour suspendre un message dans plusieurs files d'attente en une seule opération, vous devez utiliser un filtre.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour suspendre des messages

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Messages**. La liste de tous les messages sur le serveur auquel vous êtes connecté s'affiche. Pour limiter l'affichage à une seule file d'attente, cliquez sur l'onglet **Files d'attente**, double-cliquez sur le nom de la file d'attente, puis cliquez sur l'onglet *Serveur\\File d'attente* qui s'affiche.

4.  Sélectionnez un ou plusieurs messages, cliquez dessus avec le bouton droit, puis sélectionnez **Suspendre**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour suspendre des messages

Pour suspendre des messages, utilisez la syntaxe suivante :

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

Cet exemple montre comment suspendre tous les messages des files d'attente provenant d'un expéditeur du domaine contoso.com.

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

Cet exemple montre comment suspendre le message avec l'ID 3 dans la file d'attente inaccessible sur le serveur Mailbox01 :

    Suspend-Message -Identity Mailbox01\Unreachable\3

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien suspendu les messages dans les files d'attente, procédez comme suit :

  - Dans l'Afficheur des files d'attente, sélectionnez la file d'attente ou créez un filtre permettant de vérifier que les messages ont l'état Suspendu.

  - Utilisez la cmdlet **Get-Message** avec le paramètre *Queue* ou *Filter* pour vérifier que les messages ont l'état Suspendu. Pour plus d'informations, consultez la rubrique [Get-Message](https://technet.microsoft.com/fr-fr/library/bb124738\(v=exchg.150\)).

