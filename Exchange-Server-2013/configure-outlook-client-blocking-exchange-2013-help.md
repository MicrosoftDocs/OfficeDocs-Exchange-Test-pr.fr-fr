---
title: 'Configuration du blocage de clients Outlook: Exchange 2013 Help'
TOCTitle: Configuration du blocage de clients Outlook
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51407173
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du blocage de clients Outlook

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Exchange Server 2013, vous pouvez utiliser les stratégies de rétention ou les dossiers gérés pour assurer la gestion des enregistrements de messagerie (MRM). Seuls les utilisateurs de Microsoft Outlook 2010 et versions ultérieures ont accès à l’ensemble des fonctionnalités client des stratégies de rétention. Toutefois, les stratégies de rétention sont appliquées au serveur de boîtes aux lettres par l’Assistant Dossier géré, quelle que soit la version du client Outlook utilisée. Les clients Outlook antérieurs ne présentent pas la fonctionnalité MRM de ces fonctions. Par exemple, comme Outlook 2007 ne prend pas en charge les stratégies de rétention, les utilisateurs ne peuvent pas appliquer de balises personnelles aux éléments ou aux dossiers.

Vous pouvez bloquer les utilisateurs de versions d’Outlook antérieures pour les empêcher d’accéder à leurs boîtes aux lettres Exchange. Vous pouvez également bloquer l’accès par boîte aux lettres ou par serveur d’accès au client.

Pour d’autres tâches de gestion associées à la fonctionnalité MRM, voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Disponibilité de la fonctionnalité de gestion des enregistrements de messagerie par application et version cliente

Le tableau suivant répertorie les fonctionnalités de gestion des enregistrements de messagerie disponibles dans diverses applications et versions clientes.

### Fonctionnalités de gestion des enregistrements de messagerie (MRM)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Application cliente</th>
<th>Fonctionnalités de client MRM disponibles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 et Outlook 2010</p></td>
<td><p>Tout</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Dossiers gérés</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 et versions antérieures</p></td>
<td><p>Non pris en charge</p></td>
</tr>
<tr class="even">
<td><p>Autres logiciels clients de messagerie</p></td>
<td><p>Aucun</p></td>
</tr>
</tbody>
</table>


Le tableau suivant indique les numéros de version pour Outlook.

### Versions d’Outlook

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Version d’Outlook</th>
<th>Numéro de version</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8,5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> Avant d’effectuer toute modification, notez que les correctifs et les versions de Service Packs peuvent avoir un impact sur la chaîne de version du client. Soyez vigilant lorsque vous limitez l’accès client car les composants Exchange côté serveur doivent également utiliser l’interface MAPI pour ouvrir une session. Certains composants signalent leur version du client sous le nom du composant (tel que SMTP ou OLE DB) tandis que d’autres indiquent le numéro de build d’Exchange (par exemple, 6.0.4712.0). Par conséquent, évitez de limiter les clients dont les numéros de version commencent par 6.&lt;<em>x</em>.<em>x</em>.&gt;. Par exemple, pour empêcher totalement l’accès MAPI, spécifiez deux plages au lieu de <strong>0.0.0-6.5535.65535.65535</strong> pour que les composants de serveur puissent ouvrir une session. Spécifiez par exemple : <strong>0.0.0-5.9.9; 7.0.0-</strong>.


En outre, avant d’exécuter ces procédures, sachez que lorsque les utilisateurs se voient refuser l’accès à leur boîte aux lettres, ils reçoivent le message d’avertissement suivant :


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Votre administrateur de serveur Exchange a bloqué la version d’Outlook que vous utilisez. Contactez votre administrateur pour obtenir de l’aide.</p></td>
</tr>
</tbody>
</table>


Pour éviter l’avertissement indiquant que les fonctionnalités de gestion des enregistrements de messagerie ne sont pas prises en charge pour les clients de messagerie exécutant des versions d’Outlook antérieures à Outlook 2010, vous pouvez utiliser le paramètre *ManagedFolderMailboxPolicyAllowed* des cmdlets **New-Mailbox**, **Enable-Mailbox** et **Set-Mailbox** de l’environnement de ligne de commande. Lorsqu’une stratégie de boîte aux lettres de dossier géré est affectée à une boîte aux lettres à l’aide du paramètre *ManagedFolderMailboxPolicy*, l’avertissement s’affiche par défaut, sauf si le paramètre *ManagedFolderMailboxPolicyAllowed* est utilisé.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 1 minute.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour effectuer ces procédures. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell.

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Que souhaitez-vous faire ?

## Bloquer les versions d’Outlook par boîte aux lettres

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Boîtes aux lettres utilisateur » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

Cet exemple bloque toutes les versions d’Outlook antérieures à la version 11.8010.8036.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"

Cet exemple restaure l’accès à une boîte aux lettres bloquée par une version d’Outlook.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Bloquer les versions d’Outlook sur un serveur d’accès au client

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Paramètres d’accès au client RPC » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Cet exemple bloque l’accès à la boîte aux lettres d’un serveur d’accès au client Exchange 2010 ou versions ultérieures pour les clients Outlook dont la version est antérieure à la version 12.0.0.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les valeurs utilisées avec le paramètre <em>BlockedClientVersions</em> sont des exemples. Vous pouvez déterminer les versions correctes du logiciel client en analysant les fichiers journaux d’accès au client RPC situés dans <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</td>
</tr>
</tbody>
</table>


    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

Pour obtenir une définition détaillée de la syntaxe et des paramètres, voir [Set-RpcClientAccess](https://technet.microsoft.com/fr-fr/library/dd351072\(v=exchg.150\)).

