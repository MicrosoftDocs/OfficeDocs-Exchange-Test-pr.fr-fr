---
title: 'Configuration de la journalisation de l’agent anti-courrier indésirable: Exchange 2013 Help'
TOCTitle: Configuration de la journalisation de l’agent anti-courrier indésirable
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50479354
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de la journalisation de l’agent anti-courrier indésirable

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

La journalisation de l’agent permet d’enregistrer les actions effectuées par des agents de blocage du courrier indésirable Exchange spécifiques. Les informations écrites dans le journal de l'Agent dépendent de l'Agent, de l'événement SMTP et de l'action réalisée sur le message.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Service de transport » et « Serveur de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

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


## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour configurer la journalisation de l’agent de blocage du courrier indésirable

Exécutez la commande suivante :

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

Cet exemple définit les paramètres de journal d’agent suivants sur un serveur de boîtes aux lettres nommé Mailbox01 :

  -  
    Définit l’emplacement des fichiers journaux de l’agent sur D:\\Anti-Spam Agent Log. Notez bien que si le dossier n’existe pas, il sera créé pour vous.

  -  
    Définit la taille maximale d’un fichier journal de l’agent sur 20 Mo.

  -  
    Définit la taille maximale du répertoire de journaux de l’agent sur 400 Mo.

  -  
    Définit l’âge maximal d’un fichier journal d’agent sur 14 jours.

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00

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
<li><p>Si vous définissez le paramètre <em>AgentLogPath</em> sur la valeur <code>$null</code>, vous désactivez effectivement la journalisation de l’agent. Toutefois, si vous définissez <em>AgentLogPath</em> sur <code>$null</code> lorsque la valeur du paramètre <em>AgentLogEnabled</em> est <code>$true</code>, des erreurs de journal d’événements sont générées. La méthode privilégiée pour désactiver la journalisation de l’agent consiste à définir <em>AgentLogEnabled</em> sur <code>$false</code>.</p></li>
<li><p>Le fait de définir le paramètre <em>AgentLogMaxAge</em> sur la valeur <code>00:00:00</code> empêche la suppression automatique des fichiers journaux de l’agent en raison de leur ancienneté.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les paramètres *AgentLog* dans [Set-TransportService](https://technet.microsoft.com/fr-fr/library/jj215682\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré la journalisation de l’agent de blocage du courrier indésirable, procédez comme suit :

1.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

