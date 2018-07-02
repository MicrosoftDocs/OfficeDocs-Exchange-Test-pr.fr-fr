---
title: 'Gestion des files d’attente: Exchange 2013 Help'
TOCTitle: Gestion des files d’attente
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51407172
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des files d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-01-31_

Dans Microsoft Exchange Server 2013, vous pouvez utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange ou l'environnement de ligne de commande Exchange Management Shell pour gérer les files d'attente. Pour plus d'informations sur l'utilisation des cmdlets de gestion de file d'attente dans l'environnement de ligne de commande Exchange Management Shell, consultez la rubrique [Utilisation de l’environnement de ligne de commande Exchange Management Shell pour gérer les files d’attente](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Files d'attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Afficher les files d'attente

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour afficher les files d'attente

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Files d'attente**. La liste des files d'attente sur le serveur auquel vous êtes connecté s'affiche.

4.  Vous pouvez utiliser le lien **Exporter la liste** du volet Actions pour exporter la liste des files d'attente. Pour plus d'informations, consultez la rubrique [Exporter des listes à partir de l’Afficheur des files d’attente](export-lists-from-queue-viewer-exchange-2013-help.md).

## Utiliser l'environnement de ligne de commande pour afficher les files d'attente

Pour afficher les files d'attente, utilisez la syntaxe suivante.

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

Cet exemple affiche des informations de base concernant toutes les files d'attente non vides sur le serveur de boîtes aux lettres Exchange 2013 nommé Mailbox01.

    Get-Queue -Server Mailbox01 -Exclude Empty

Cet exemple affiche des informations détaillées concernant toutes les files d'attente contenant plus de 100 messages sur le serveur de boîte aux lettres sur lequel la commande est exécutée.

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## Utiliser l'environnement de ligne de commande pour afficher des informations récapitulatives de file s'attente sur plusieurs serveurs Exchange

La cmdlet **Get-QueueDigest** fournit une vue agrégée de niveau supérieur de l’état des files d’attentes sur tous les serveurs au sein d’une étendue spécifique, telle qu’un DAG, un site Active Directory, une liste de serveurs ou la forêt Active Directory entière. Les files d’attente sur un serveur de transport Edge abonné dans le réseau de périmètre ne sont pas incluses dans les résultats. De plus, la cmdlet **Get-QueueDigest** est disponible sur un serveur de transport Edge, mais les résultats sont limités aux files d’attente sur le serveur de transport Edge.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, la cmdlet <strong>Get-QueueDigest</strong> affiche les files d’attente de remise contenant au moins dix messages, et les résultats peuvent dater d’une à deux minutes. Pour obtenir des instructions sur la modification de ces valeurs par défaut, consultez la rubrique Configurer Get-QueueDigest <a href="configure-get-queuedigest-exchange-2013-help.md">Configurer Get-QueueDigest</a>.</td>
</tr>
</tbody>
</table>


Pour afficher des informations récapitulatives concernant les files d'attente sur plusieurs serveurs Exchange, exécutez la commande suivante :

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

Cet exemple montre comment afficher des informations récapitulatives concernant les files d'attente sur tous les serveurs de boîtes aux lettres Exchange 2013 situés dans le site Active Directory nommé FirstSite dont le nombre de messages et supérieur à 100.

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

Cet exemple montre comment afficher des informations récapitulatives concernant les files d'attente sur tous les serveurs de boîtes aux lettres Exchange 2013 au sein du groupe de disponibilité de base de données (DAG) nommé DAG01 où l'état de la file d'attente a la valeur **Nouvelle tentative**.

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## Reprendre des files d'attente

En reprenant une file d'attente, vous redémarrez les activités sortantes d'une file d'attente dont l'état est Suspendu. Pour que cette action ait un effet, l'état de la file d'attente doit être Suspendu. Lorsque vous reprenez une file d'attente, l'état des messages qu'elle contient ne change pas. Les messages dont l'état est Suspendu restent suspendus et ne quittent pas la file d'attente.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour reprendre des files d'attente

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Files d'attente**. La liste des files d'attente sur le serveur auquel vous êtes connecté s'affiche.

4.  Cliquez sur **Créer un filtre**, puis entrez l'expression du filtre comme suit :
    
    1.  Dans la liste déroulante des propriétés de file d'attente, sélectionnez **Status**.
    
    2.  Dans la liste déroulante des opérateurs de comparaison, sélectionnez **Est égal à**.
    
    3.  Dans la liste déroulante des valeurs, sélectionnez **Suspendu**.

5.  Cliquez sur **Appliquer le filtre**. Toutes les files d'attente actuellement suspendues sur le serveur s'affichent.

6.  Sélectionnez une ou plusieurs files d'attente, cliquez dessus avec le bouton droit, puis sélectionnez **Reprendre**.

## Utiliser l'environnement de ligne de commande pour reprendre des files d'attente

Pour reprendre des files d'attente, utilisez la syntaxe suivante.

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

Cet exemple montre comment reprendre toutes les files d'attente dont l'état est Suspendu sur le serveur local.

    Resume-Queue -Filter {Status -eq "Suspended"}

Cet exemple montre comment reprendre la file d'attente de remise suspendue nommée contoso.com sur le serveur nommé Mailbox01.

    Resume-Queue -Identity Mailbox01\contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien repris une file d'attente, procédez comme suit :

1.  Utilisez l'Afficheur des files d'attente ou la cmdlet **Get-Queue** pour rechercher la file d'attente que vous avez tenté de reprendre.

2.  Vérifiez que la propriété **Status** de la file d'attente n'a pas la valeur `Suspended`.

## Réessayer des files d'attente

Quand un serveur de transport ne peut pas se connecter au saut suivant, l'état de la file d'attente de remise est Nouvelle tentative. Lorsque vous relancez une file d'attente de remise à l'aide de l'Afficheur des files d'attente ou de l'environnement de ligne de commande, vous forcez une tentative de connexion immédiate et modifiez l'heure de la prochaine tentative planifiée. Si la connexion échoue, le minuteur d'intervalle de nouvelle tentative est réinitialisé. Pour que cette action ait un effet, la file d'attente de remise doit présenter l'état Nouvelle tentative.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour réessayer une file d'attente

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Files d'attente**. La liste des files d'attente sur le serveur auquel vous êtes connecté s'affiche.

4.  Cliquez sur **Créer un filtre**, puis entrez l'expression du filtre comme suit :
    
    1.  Dans la liste déroulante des propriétés de file d'attente, sélectionnez **Status**.
    
    2.  Dans la liste déroulante des opérateurs de comparaison, sélectionnez **Est égal à**.
    
    3.  Dans la liste déroulante des valeurs, sélectionnez **Nouvelle tentative**.

5.  Cliquez sur **Appliquer le filtre**. Toutes les files d'attente dont l'état actuel est **Réessayer** s'affichent.

6.  Sélectionnez une ou plusieurs files d'attente dans la liste. Cliquez avec le bouton droit, puis sélectionnez **Réessayer la file d'attente**. Si la tentative de connexion réussit, l'état de la file d'attente devient **Active**. Si aucune connexion n'est établie, la file d'attente conserve l'état **Nouvelle tentative** et l'heure de la prochaine tentative est mise à jour.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour réessayer une file d'attente

Pour réessayer des files d'attente, utilisez la syntaxe suivante.

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

Cet exemple montre comment réessayer toutes les files d'attente dont l'état est Nouvelle tentative sur le serveur local.

    Retry-Queue -Filter {status -eq "retry"}

Cet exemple montre comment réessayer la file d'attente nommée contoso.com dont l'état est `Retry` sur le serveur nommé Mailbox01.

    Retry-Queue -Identity Mailbox01\contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien réessayé une file d'attente, procédez comme suit :

1.  Utilisez l'Afficheur des files d'attente ou la cmdlet **Get-Queue** pour rechercher la file d'attente que vous avez tenté de réessayer.

2.  Vérifiez que la propriété **LastRetryTime** de la file d'attente correspond à l'heure à laquelle vous avez tenté de réessayer la file d'attente.

## Resoumettre des messages en file d'attente

Resoumettre de nouveau une file d'attente est similaire à la réessayer, sauf que les messages sont renvoyés à la file d'attente de soumission afin que le catégoriseur les traite une nouvelle fois. Vous pouvez resoumettre des messages dont l'état est le suivant :

  - Files d'attente de remise dont l'état est Nouvelle tentative. Les messages dans les files d'attente ne peuvent pas présenter l'état Suspendu.

  - Messages de la file d'attente inaccessible qui ne présentent pas l'état Suspendu.

  - Messages de la file d'attente de messages incohérents.

## Utiliser l'environnement de ligne de commande pour resoumettre des messages

Pour resoumettre des messages, utilisez la syntaxe suivante :

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

Cet exemple montre comment resoumettre tous les messages situés dans une file d'attente de remise dont l'état est Nouvelle tentative sur le serveur nommé Mailbox01.

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

Cet exemple montre comment resoumettre tous les messages situés dans la file d'attente inaccessible sur le serveur Mailbox01.

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## Resoumettre les messages de la file d'attente de messages incohérents

Vous resoumettez les messages de la file d'attente de messages incohérents en les reprenant. Vous pouvez utiliser l'Afficheur des files d'attente ou l'environnement de ligne de commande pour resoumettre les messages de la file d'attente de messages incohérents. La file d'attente de messages incohérents est visible dans l'Afficheur des files d'attente uniquement si elle contient des messages.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La file d'attente de messages incohérents contient les messages identifiés comme nuisibles pour le système Exchange après une défaillance du serveur. Les messages peuvent être véritablement dangereux par leur contenu ou leur format. Ils peuvent également être les victimes d'un agent mal écrit ayant bloqué le serveur Exchange pendant le traitement des messages supposés incorrects. Si vous n'êtes pas sûr de la fiabilité des messages se trouvant dans la file d'attente de messages incohérents, exportez-les dans des fichiers afin de pouvoir les examiner. Pour plus d'informations, consultez la rubrique <a href="export-messages-from-queues-exchange-2013-help.md">Exportation de messages de files d'attente</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour resoumettre les messages de la file d'attente de messages incohérents

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Files d'attente**. La liste des files d'attente sur le serveur auquel vous êtes connecté s'affiche.

4.  Cliquez sur la file d'attente de messages incohérents. Dans le volet Actions, cliquez sur **Afficher les messages**.

5.  Sélectionnez un ou plusieurs messages, cliquez dessus avec le bouton droit, puis sélectionnez **Reprendre**.

## Utiliser l'environnement de ligne de commande pour resoumettre les messages de la file d'attente de messages incohérents

Pour resoumettre des messages de la file d'attente de messages incohérents, procédez comme suit :

1.  Recherchez l'identité du message en exécutant la commande suivante.
    
        Get-Message -Queue Poison | Format-Table Identity

2.  Utilisez l'identité du message trouvée à l'étape précédente dans la commande suivante.
    
        Resume-Message <PoisonMessageIdentity>
    
    Cet exemple montre comment reprendre un message de la file d'attente de messages incohérents dont la valeur d'identité est 222.
    
        Resume-Message 222

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien resoumis un message de la file d'attente de messages incohérents, procédez comme suit :

1.  Utilisez l'Afficheur des files d'attente ou la cmdlet **Get-Queue** pour afficher la file d'attente de messages incohérents à l'emplacement du message que vous avez tenté de resoumettre.

2.  Vérifiez que le message ne figure plus dans la file d'attente de messages incohérents. Notez qu'une file d'attente de messages incohérents vide n'apparaît pas dans l'Afficheur des files d'attente ou dans le résultat de la cmdlet **Get-Queue**. C'est pourquoi, si le message que vous avez resoumis était le seul message de la file d'attente de messages incohérents, et si cette dernière n'est plus visible, cela constitue également une indication de la réussite de la resoumission du message.

## Suspendre des files d'attente

Lorsque vous suspendez une file d'attente, vous empêchez les messages de la quitter, mais vous ne modifiez pas l'état de ces derniers. Les opérations de remise de messages via SMTP en cours s'achèvent. Vous pouvez suspendre une file d'attente pour arrêter le flux de messagerie, puis suspendre un ou plusieurs messages de la file d'attente. Lorsque vous reprenez la file d'attente, les messages suspendus restent dans celle-ci.

Vous pouvez suspendre une file d'attente présentant l'état Actif ou Nouvelle tentative. Vous pouvez également suspendre la file d'attente inaccessible et la file d'attente de soumission.

Si vous suspendez la file d'attente inaccessible, les éléments ne sont pas resoumis au catégoriseur lorsque des mises à jour de configuration sont reçues par le serveur de transport tant que la file d'attente n'est pas reprise. Si vous suspendez la file d'attente de soumission, les messages ne sont pas collectés par le catégoriseur tant que la file d'attente n'est pas reprise.

## Utiliser l'Afficheur des files d'attente dans la boîte à outils Exchange pour suspendre une file d'attente

1.  Cliquez sur **Démarrer**\>**Tous les programmes**\>**Microsoft Exchange 2013**\>**Boîte à outils Exchange**.

2.  Dans la section **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d'attente** pour ouvrir l'outil dans une nouvelle fenêtre.

3.  Dans l'Afficheur des files d'attente, cliquez sur l'onglet **Files d'attente**. La liste des files d'attente sur le serveur auquel vous êtes connecté s'affiche. Vous pouvez créer un filtre permettant d'afficher uniquement les files d'attente répondant à des critères spécifiques.

4.  Sélectionnez une ou plusieurs files d'attente, cliquez avec le bouton droit, puis sélectionnez **Suspendre**.

## Utiliser l'environnement de ligne de commande pour suspendre une file d'attente

Pour suspendre une file d'attente, utilisez la syntaxe suivante.

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

Cet exemple montre comment suspendre toutes les files d'attente sur le serveur local dont le nombre de messages est supérieur ou égal à 1 000 et dont l'état est Nouvelle tentative.

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

Cet exemple montre comment suspendre la file d'attente nommée contoso.com sur le serveur nommé Mailbox01.

    Suspend-Queue -Identity Mailbox01\contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien suspendu une file d'attente, procédez comme suit :

1.  Utilisez l'Afficheur des files d'attente ou la cmdlet **Get-Queue** pour rechercher la file d'attente que vous avez tenté de suspendre.

2.  Vérifiez que la propriété **Status** de la file d'attente a la valeur `Suspended`.

