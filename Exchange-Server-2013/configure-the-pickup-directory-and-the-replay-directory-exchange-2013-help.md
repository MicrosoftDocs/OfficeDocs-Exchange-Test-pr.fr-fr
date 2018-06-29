﻿---
title: 'Configurer le répertoire de collecte et le répertoire de relecture: Exchange 2013 Help'
TOCTitle: Configurer le répertoire de collecte et le répertoire de relecture
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50479228
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le répertoire de collecte et le répertoire de relecture

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Le répertoire de collecte et le répertoire de relecture sont utilisés par le service de transport sur les serveurs de boîtes aux lettres et sur les serveurs de transport Edge pour insérer des fichiers de messages directement dans le pipeline de transport. Les fichiers de message électronique correctement mis en forme que vous copiez dans le répertoire de collecte ou de relecture sont soumis à des fins de remise. Le répertoire de collecte est utilisé par des administrateurs pour tester le flux de messagerie ou par des applications qui doivent créer et soumettre leurs propres messages. Le répertoire de relecture reçoit des messages provenant de serveurs de passerelle étrangers non SMTP et retransmet les messages que vous avez exportés à partir des files d’attente des serveurs Microsoft Exchange.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Règles de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - La valeur du paramètre *PickupDirectoryMaxMessagesPerMinute* sur la cmdlet **Set-TransportService** est utilisée par les répertoires de collecte et de relecture.

  - La modification de l’emplacement du répertoire de collecte ou de relecture n’entraîne pas la copie de fichiers de messages existants de l’ancien emplacement vers le nouvel emplacement. Le nouvel emplacement du répertoire de collecte ou de relecture est actif presque immédiatement après le changement de configuration, mais tous les fichiers de messages existants sont laissés dans l’ancien emplacement.

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


## Que voulez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer le répertoire de collecte

Pour configurer le répertoire de collecte, utilisez la syntaxe suivante.

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

Cet exemple apporte les modifications suivantes au répertoire de collecte situé sur le serveur de boîtes aux lettres qui est nommé Exchange01:

  - L’emplacement du répertoire de collecte est défini sur D:\\Pickup Directory.

  - La taille maximale autorisée pour les en-têtes des messages dans un fichier de message passe à 96 Ko.

  - Le nombre maximal de destinataires autorisés dans un fichier de message passe à 250.

  - Le taux maximal de traitement des messages pour les répertoires de ramassage et de relecture est porté à 200 messages par minute.

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Définir le paramètre <em>PickupDirectoryPath</em> sur la valeur <code>$null</code> désactive le répertoire de collecte.</p></li>
<li><p>Les répertoires spécifiés par le paramètre <em>PickupDirectoryPath</em> et le paramètre <em>ReplayDirectoryPath</em> ne peuvent pas être identiques.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer le répertoire de relecture

Pour configurer le répertoire de relecture, utilisez la syntaxe suivante.

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

Cet exemple apporte les modifications suivantes au répertoire de relecture situé sur le serveur de boîtes aux lettres qui est nommé Exchange01:

  - L’emplacement du répertoire de relecture est défini sur D:\\Replay Directory.

  - Le taux maximal de traitement des messages pour les répertoires de ramassage et de relecture est porté à 200 messages par minute.

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Définir le paramètre <em>ReplayDirectoryPath</em> sur la valeur <code>$null</code> désactive le répertoire de relecture.</p></li>
<li><p>Les répertoires spécifiés par le paramètre <em>PickupDirectoryPath</em> et le paramètre <em>ReplayDirectoryPath</em> ne peuvent pas être identiques.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier si les répertoires de collecte et de relecture sont configurés correctement, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

