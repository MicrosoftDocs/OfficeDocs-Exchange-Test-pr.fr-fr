---
title: 'Configurer la journalisation de connectivité: Exchange 2013 Help'
TOCTitle: Configurer la journalisation de connectivité
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50477670
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer la journalisation de connectivité

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-18_

L'enregistrement de la connectivité enregistre l'activité de connexion sortante utilisée pour transmettre des messages en provenance d'un service de transport sur le serveur Exchange. L'enregistrement de la connectivité recueille des données sur la source de connexion, la destination, le nombre de messages et les octets transmis, ainsi que des informations sur les échecs de connexion.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Service de transport », « Service de transport frontal » et « Service de transport de boîte aux lettres » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver l'enregistrement de la connectivité, ou définir le chemin d'accès au journal de connectivité pour le service de transport seulement. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour toutes les autres options d'enregistrement de la connectivité dans d'autres services de transport.

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

## Utiliser le Centre d'administration Exchange (CAE) pour configurer l'enregistrement de la connectivité dans le service de transport

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Sélectionnez le serveur de boîtes aux lettres à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés du serveur, cliquez sur **Journaux de transport**.

4.  Dans la section **Journal de connectivité**, modifiez l'un des paramètres suivants :
    
      - **Activer le journal de connectivité**   Pour désactiver l'enregistrement de la connectivité sur le serveur, décochez la case. Pour activer l'enregistrement de la connectivité sur le serveur, cochez la case.
    
      - **Chemin du journal de connectivité**   La valeur que vous spécifiez doit être sur le serveur Exchange local. Si le dossier n'existe pas, il sera créé pour vous quand vous cliquerez sur **Enregistrer**.
    
    Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer l'enregistrement de la connectivité

Pour activer l'enregistrement de la connectivité, exécutez la commande suivante :

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

Cet exemple définit les paramètres du journal de connectivité suivants dans le service de transport sur le serveur de boîtes aux lettres nommé Mailbox01 :

  -  
    Définit l'emplacement des fichiers journaux de connectivité dans D:\\Hub Connectivity Log. Notez bien que si le dossier n'existe pas, il sera créé pour vous.

  -  
    Définit la taille maximale d'un fichier journal de connectivité à 20 Mo.

  -  
    Définit la taille maximale du répertoire des journaux de connectivité à 1,5 Go.

  -  
    Définit l'âge maximal d'un fichier journal de connectivité sur 45 jours.

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00

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
<li><p>Pour configurer les paramètres du journal de connectivité dans le service de transport de la boîte aux lettres sur un serveur de boîtes aux lettres, utilisez la cmdlet <strong>Set-MailboxTransportService</strong>. Pour configurer les paramètres du journal de connectivité dans le service de transport frontal sur un serveur d'accès au client, utilisez la cmdlet <strong>Set-FrontEndTransportService</strong>.</p></li>
<li><p>La définition de la valeur du paramètre <em>ConnectivityLogPath</em> sur <code>$null</code> désactive effectivement l'enregistrement de la connectivité. Toutefois, si la valeur du paramètre <em>ConnectivityLogEnabled</em> est <code>$true</code>, des erreurs sont générées dans le journal des événements.</p></li>
<li><p>Le fait de définir la valeur du paramètre <em>ConnectivityLogMaxAge</em> sur <code>00:00:00</code> empêche la suppression automatique des fichiers journaux de connectivité en raison de leur ancienneté.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré l'enregistrement de la connectivité, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

