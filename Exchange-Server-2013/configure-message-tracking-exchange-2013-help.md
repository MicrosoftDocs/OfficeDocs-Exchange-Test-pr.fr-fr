---
title: 'Configuration du suivi des messages: Exchange 2013 Help'
TOCTitle: Configuration du suivi des messages
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51407184
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du suivi des messages

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-18_

Le suivi des messages enregistre l'activité de transport SMTP de tous les messages transférés depuis et vers le service de transport ou les boîtes aux lettres sur un serveur de boîtes aux lettres Microsoft Exchange Server 2013. Les journaux de suivi des messages sont utiles pour les investigations sur les messages ainsi que pour l'analyse, les rapports et le dépannage du flux de messagerie.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Service de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md) ou l'entrée « Configuration du serveur de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver le suivi, ou pour définir le chemin d'accès au journal de suivi des messages. Pour toutes les autres options de suivi des messages, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Sur un serveur de boîtes aux lettres Exchange 2013, vous pouvez utiliser la cmdlet **Set-TransportService** ou **Set-MailboxServer** pour configurer les options de suivi des messages. Les procédures décrites dans cette rubrique utilisent la cmdlet **Set-TransportService**.

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


## Utiliser le Centre d'administration Exchange pour configurer le suivi des messages sur des serveurs de boîtes aux lettres

1.  Dans le Centre d'administration Exchange, accédez à **Serveurs** \> **Serveurs**.

2.  Sélectionnez le serveur de boîtes aux lettres à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés du serveur, cliquez sur **Journaux de transport**.

4.  Dans la section **Journal de suivi des messages**, modifiez l'un des paramètres suivants :
    
      - **Activer le journal de suivi des messages**   Pour désactiver le suivi des messages sur le serveur, décochez la case. Pour activer cette fonctionnalité sur le serveur, cochez la case.
    
      - **Chemin du journal de suivi de messages**   La valeur que vous spécifiez doit être sur le serveur Exchange local. Si le dossier n'existe pas, il sera créé pour vous quand vous cliquerez sur **Enregistrer**.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le suivi des messages

Pour configurer le suivi des messages, exécutez la commande suivante :

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

Cet exemple définit les paramètres de journal de suivi des messages suivants sur le serveur de boîtes aux lettres intitulé Mailbox01 :

  -  
    Définit l'emplacement des fichiers journaux de suivi des messages sur D:\\Message Tracking Log. Notez bien que si le dossier n'existe pas, il sera créé pour vous.

  -  
    Définit la taille maximale d'un fichier journal de suivi des messages à 20 Mo.

  -  
    Définit la taille maximale du répertoire des journaux de suivi des messages à 1,5 Go.

  -  
    Définit l'âge maximal d'un fichier journal de suivi des messages à 45 jours.

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00

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
<li><p>La définition de la valeur du paramètre <em>MessageTrackingLogPath</em> sur <code>$null</code> désactive effectivement le suivi des messages. Toutefois, si la valeur du paramètre <em>MessageTrackingLogEnabled</em> est <code>$true</code>, des erreurs sont générées dans le journal des événements.</p></li>
<li><p>Le fait de définir la valeur du paramètre <em>MessageTrackingLogMaxAge</em> sur <code>00:00:00</code> empêche la suppression automatique des fichiers journaux de suivi des messages en raison de leur ancienneté.</p></li>
<li><p>Pour les serveurs de boîtes aux lettres Exchange 2013, la taille maximale du répertoire des journaux de suivi des messages est égale à trois fois la valeur du paramètre <em>MessageTrackingLogMaxDirectorySize</em>. Si les fichiers journaux de suivi des messages générés par les quatre différents services portent des préfixes de nom différents, la quantité de données et la fréquence d'écriture de ces dernières dans les fichiers journaux <strong>MSGTRKMA</strong> sont négligeables en comparaison des fichiers journaux portant les trois autres préfixes. Pour plus d'informations, consultez la section « Structure des fichiers journaux de suivi des messages » dans la rubrique <a href="message-tracking-exchange-2013-help.md">Suivi des messages</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Cet exemple désactive la journalisation des objets des messages dans le journal de suivi des messages sur le serveur de boîtes aux lettres intitulé Mailbox01 :

    Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false

Cet exemple désactive le suivi des messages sur le serveur de boîtes aux lettres intitulé Mailbox01 :

    Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré le suivi des messages, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

