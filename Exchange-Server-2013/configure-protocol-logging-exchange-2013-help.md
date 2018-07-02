---
title: "Configuration de l'enregistrement dans le journal de protocole: Exchange 2013 Help"
TOCTitle: Configuration de l'enregistrement dans le journal de protocole
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50479204
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l'enregistrement dans le journal de protocole

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-03-15_

L'enregistrement dans le journal de protocole consigne les conversations SMTP sur les connecteurs d'envoi et de réception dans le cadre de la remise des messages.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Service de transport », « Service de transport frontal », « Service de transport de boîte aux lettres », « Connecteurs de réception » et « Connecteurs d'envoi » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver l'enregistrement dans le journal de protocole pour les connecteurs d'envoi et de réception dans le service de transport sur les serveurs de boîtes aux lettres, et pour les récepteurs d'envoi dans le service de transport frontal sur les serveurs d'accès au client. Vous pouvez aussi utiliser le CAE pour configurer les chemins de journaux de protocole pour le service de transport uniquement. Pour toutes les autres options d'enregistrement dans le journal de protocole, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - L'enregistrement dans le journal de protocole est activé ou désactivé sur chacun des connecteurs. Tous les connecteurs de réception configurés sur le serveur Exchange partagent les mêmes fichiers journaux de protocole et les mêmes options d'enregistrement de protocole. Ces paramètres de journaux de protocole sont distincts des fichiers journaux de protocole et des options d'enregistrement de journal de protocole du connecteur d'envoi situés sur le même serveur.

  - 
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>N’exécutez pas cette procédure sur un serveur de transport Edge qui a été abonné à l’organisation Exchange à l’aide d’EdgeSync. Préférez apporter les modifications au service de transport sur le serveur de boîte aux lettres. Les modifications sont ensuite répliquées sur le serveur de transport Edge lors de la prochaine synchronisation EdgeSync.</td>
    </tr>
    </tbody>
    </table>


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

## Utiliser le Centre d'administration Exchange (CAE) pour configurer l'enregistrement dans le journal de protocole

Pour utiliser le CAE afin d'activer ou de désactiver l'enregistrement dans le journal de protocole sur un connecteur d'envoi ou de réception dans le service de transport sur un serveur de boîtes aux lettres, ou sur un connecteur de réception dans le service de transport frontal sur un serveur d'accès au client, procédez comme suit :

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Connecteurs d'envoi** ou **Flux de messagerie** \> **Connecteurs de réception**.

2.  Sélectionnez le connecteur à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sous l'onglet **Général** de la section **Niveau d'enregistrement dans le journal**, activez l'une des options suivantes :
    
      - **Aucun**   Enregistrement de journal de protocole désactivé sur le connecteur.
    
      - **Détaillée**   Enregistrement de journal de protocole activé sur le connecteur.
    
    Lorsque vous avez terminé, cliquez sur **Enregistrer**.

Pour utiliser le CAE afin de configurer les chemins des journaux de protocole pour les connecteurs d'envoi et de réception dans le service de transport sur un serveur de boîtes aux lettres, procédez comme suit :

1.  Dans le CAE, accédez à **Serveurs** \> **Serveurs**.

2.  Sélectionnez le serveur de boîtes aux lettres à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page des propriétés du serveur, cliquez sur **Journaux de transport**.

4.  Dans la section **Journal de protocole**, modifiez l'un des paramètres suivants :
    
      - **Chemin du journal du protocole d'envoi**   La valeur spécifiée doit se trouver sur le serveur Exchange local. Si le dossier n'existe pas, il sera créé pour vous quand vous cliquerez sur **Enregistrer**.
    
      - **Chemin d'accès au journal du protocole de réception**   La valeur spécifiée doit se trouver sur le serveur Exchange local. Si le dossier n'existe pas, il sera créé pour vous quand vous cliquerez sur **Enregistrer**.
    
    Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré les paramètres du journal de protocole à l'aide du CAE, procédez comme suit :

1.  Accédez à l'emplacement spécifié pour les journaux de protocole du connecteur d'envoi ou de réception.

2.  Si vous avez activé l'enregistrement dans le journal de protocole, vérifiez qu'un fichier journal est créé. Si vous avez désactivé l'enregistrement dans le journal de protocole, vérifiez que le dernier fichier journal n'est plus mis à jour.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l'enregistrement dans le journal de protocole sur un connecteur d'envoi ou de réception

Pour activer ou désactiver l'enregistrement dans le journal de protocole sur un connecteur d'envoi ou de réception, exécutez la commande suivante :

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

Cet exemple active l'enregistrement dans le journal de protocole pour le connecteur de réception nommé Connection de Contoso.com.

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé l'enregistrement dans le journal de protocole, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l'enregistrement dans le journal de protocole sur le connecteur d'envoi intra-organisationnel

Pour activer ou désactiver l'enregistrement dans le journal de protocole sur le connecteur d'envoi intra-organisationnel implicite et invisible qui existe dans le service de transport sur un serveur de boîtes aux lettres et dans le service de transport frontal sur un serveur d'accès au client, exécutez la commande suivante :

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

Cet exemple active l'enregistrement dans un journal de protocole sur le connecteur d'envoi intra-organisationnel dans le service de transport sur un serveur de boîtes aux lettres nommé Mailbox01.

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé l'enregistrement dans le journal de protocole sur le connecteur d'envoi intra-organisationnel, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l'enregistrement dans le journal de protocole sur le connecteur d'envoi de remise de boîte aux lettres

Pour activer ou désactiver l'enregistrement dans le journal de protocole sur le connecteur d'envoi de remise de boîte aux lettres implicite et invisible qui existe dans le service de transport de boîte aux lettres sur un serveur de boîtes aux lettres, exécutez la commande suivante :

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

Cet exemple active l'enregistrement dans un journal de protocole sur le connecteur de réception de remise de boîte aux lettres dans le service de transport de boîte aux lettres sur un serveur de boîtes aux lettres nommé Mailbox01.

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé l'enregistrement dans le journal de protocole sur le connecteur de remise de boîte aux lettres, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les paramètres de l'enregistrement dans le journal de protocole

Pour configurer les paramètres de journal de protocole, exécutez la commande suivante :

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

Cet exemple définit les paramètres de journal de protocole suivants dans le service de transport sur un serveur de boîtes aux lettres nommé Mailbox01 :

  -  
    Définit l'emplacement de l'ensemble des journaux de protocole du connecteur de réception sur D:\\Hub Receive SMTP Log et de l'ensemble des journaux de protocole du connecteur d'envoi D:\\Hub Send SMTP Log. Notez bien que si le dossier n'existe pas, il sera créé pour vous.

  -  
    Définit la taille maximale d'un fichier journal de protocole du connecteur de réception et d'envoi sur 20 Mo.

  -  
    Définit la taille maximale d'un dossier de journaux de protocole du connecteur de réception et d'envoi sur 400 Mo.

  -  
    Définit l'âge maximal d'un fichier journal de protocole du connecteur de réception et d'envoi sur 45 jours.

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00

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
<li><p>Pour configurer les paramètres de journal de protocole dans le service de transport de boîte aux lettres sur un serveur de boîtes aux lettres, utilisez la cmdlet <strong>Set-MailboxTransportService</strong>. Pour configurer les paramètres de journal de protocole dans le service de transport frontal sur un serveur d'accès au client, utilisez la cmdlet <strong>Set-FrontEndTransportService</strong>.</p></li>
<li><p>Définir les paramètres <em>SendProtocolLogPath</em> ou <em>ReceiveProtocolLogPath</em> sur la valeur <code>$null</code> désactive l'enregistrement dans le journal de protocole pour tous les connecteurs d'envoi et de réception sur le serveur. Toutefois, le fait de définir l'un de ces paramètres sur <code>$null</code> lorsque l'enregistrement dans le journal de protocole est activé pour tout connecteur d'envoi sur le serveur, y compris le connecteur d'envoi intra-organisationnel ou le connecteur d'envoi de remise de boîte aux lettres, génère des erreurs dans le journal des événements.</p></li>
<li><p>Définir les paramètres <em>ReceiveProtocolLogMaxAge</em> ou <em>SendProtocolLogMaxAge</em> sur la valeur <code>00:00:00</code> empêche la suppression automatique des fichiers journaux de protocole en raison de leur âge.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier que les paramètres de journal de protocole sont configurés correctement, procédez comme suit :

1.  Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante :
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

