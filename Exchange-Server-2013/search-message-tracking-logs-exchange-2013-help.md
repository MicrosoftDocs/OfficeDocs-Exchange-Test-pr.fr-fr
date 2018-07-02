---
title: 'Recherche des journaux de suivi des messages: Exchange 2013 Help'
TOCTitle: Recherche des journaux de suivi des messages
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51407248
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recherche des journaux de suivi des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-25_

Dans Microsoft Exchange Server 2013, le journal de suivi des messages est un enregistrement détaillé de toute l'activité de messagerie, regroupant les messages échangés avec le service de transport sur les serveurs de boîtes aux lettres, les boîtes aux lettres sur les serveurs de boîtes aux lettres et les serveurs de transport Edge.

La cmdlet **Get-MessageTrackingLog** dans l'environnement de ligne de commande Exchange Management Shell permet de rechercher des entrées du journal de suivi des messages en utilisant des critères de recherche spécifiques.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 30 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Suivi des messages » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour rechercher dans les journaux de suivi des messages, le service de recherche des journaux de transport Microsoft Exchange doit être en cours d'exécution. Si vous désactivez ou arrêtez ce service, vous ne pourrez ni effectuer de recherche dans les journaux de suivi des messages, ni exécuter des rapports de remise. En revanche, l'arrêt de ce service n'a aucune incidence sur les autres fonctionnalités d'Exchange.

  - Les noms des champs affichés dans les résultats de l'exécution de la cmdlet **Get-MessageTrackingLog** sont similaires aux noms des champs actuels utilisés dans les journaux de suivi des messages. Les principales différences sont les suivantes :
    
      - Les tirets sont supprimés des noms de champs. Par exemple, **internal-message-id** est affiché sous la forme `InternalMessageId`.
    
      - Le champ **date-time** est affiché sous la forme `Timestamp`.
    
      - Le champ **recipient-address** est affiché sous la forme `Recipients`.
    
      - Le champ **sender-address** est affiché sous la forme `Sender`.

  - Le champ **date-time** du journal de suivi des messages stocke des informations au format de temps universel coordonné (UTC). Toutefois, nous vous recommandons d'entrer vos critères de recherche date-time pour les paramètres *Start* ou *End* dans le format date-time régional de l'ordinateur que vous utilisez pour effectuer la recherche.

  - Vous ne pouvez pas copier les fichiers journaux de suivi des messages à partir d'un autre serveur Exchange, puis les rechercher à l'aide de la cmdlet **Get-MessageTrackingLog**. De même, si vous enregistrez manuellement un journal de suivi des messages existant, toute modification des informations d'horodatage date-time du fichier brise la logique de requête qu'utilise Exchange pour effectuer des recherches dans les journaux de suivi des messages.

  - La cmdlet Exchange 2013**Get-MessageTrackingLog** peut effectuer des recherches dans les journaux de suivi des messages sur des serveurs Exchange 2007 et Exchange 2010 dans le même site Active Directory.

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

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher dans les journaux de suivi des messages

Pour rechercher des entrées correspondant à des événements spécifiques dans le journal de suivi des messages, utilisez la syntaxe suivante :

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

Pour afficher les 1 000 entrées du journal de suivi des messages les plus récentes sur le serveur, exécutez la commande suivante :

    Get-MessageTrackingLog

Cet exemple recherche dans les journaux de suivi des messages sur le serveur local toutes les entrées enregistrées entre le 28/03/2013 à 8h et le 28/03/2013 à 17h pour tous les événements **FAIL** envoyés par pat@contoso.com.

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour contrôler la sortie d'une recherche dans le journal de suivi des messages

Utilisez la syntaxe suivante.

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

Cet exemple effectue une recherche dans les journaux de suivi des messages à l'aide des critères de recherche suivants :

  - Renvoie des résultats correspondant aux 1 000 premiers événements **Send**.

  - Affiche les résultats sous forme de liste.

  - Affiche uniquement les champs dont le nom commence par `Send` ou `Recipient`.

  - Écrit la sortie dans un nouveau fichier intitulé `D:\Send Search.txt`.

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour rechercher dans les journaux de suivi des messages les entrées de messages sur plusieurs serveurs

Généralement, la valeur dans le champ d'en-tête **MessageID:**  demeure constante tant que le message se déplace dans l'organisation Exchange. Cette propriété est appelée **InternetMessageId** dans les utilitaires d'affichage des files d'attente et **MessageId** dans les utilitaires d'affichage des journaux de suivi des messages. Après avoir déterminé la valeur de la propriété `MessageID:` d'un message spécifique, vous pouvez rechercher des informations concernant ce message dans les journaux de suivi des messages sur chaque serveur de boîtes aux lettres de votre organisation Exchange.

Pour rechercher toutes les entrées des journaux de suivi des messages correspondant à un message spécifique sur tous les serveurs de boîtes aux lettres, utilisez la syntaxe suivante :

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

Cet exemple recherche dans les journaux de suivi des messages sur tous les serveurs de boîtes aux lettres Exchange 2013 à l'aide des critères de recherche suivants :

  - Recherche les entrées associées à un message dont la valeur de la propriété **MessageID:**  correspond à `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`. Notez que vous pouvez omettre les crochets (`<``>`). Si ce n'est pas le cas; vous devez mettre la valeur de **MessageID:**  entre guillemets.

  - Pour chaque entrée, affiche les champs **date-time**, **server-hostname**, **client-hostname**, **source**, **event-id** et **recipient-address**.

  - Trie les résultats en fonction du champ **date-time**.

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## Utiliser le Centre d'administration Exchange (CAE) pour rechercher dans les journaux de suivi des messages

Vous pouvez utiliser la fonctionnalité Rapports de remise pour les administrateurs dans le CAE pour rechercher dans des journaux de suivi des messages des informations concernant les messages envoyés ou reçus par une boîte aux lettres spécifique dans votre organisation. Pour plus d'informations, consultez la rubrique [Suivre les messages avec des rapports de remise](track-messages-with-delivery-reports-exchange-2013-help.md).

