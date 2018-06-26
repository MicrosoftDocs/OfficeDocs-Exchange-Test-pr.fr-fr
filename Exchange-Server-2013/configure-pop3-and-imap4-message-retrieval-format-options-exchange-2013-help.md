---
title: 'Configurer les options de format d’extraction de message POP3 et IMAP4: Exchange 2013 Help'
TOCTitle: Configurer les options de format d’extraction de message POP3 et IMAP4
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50555391
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les options de format d’extraction de message POP3 et IMAP4

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Vous pouvez configurer le format de récupération des messages pour les utilisateurs qui se connectent à leur messagerie électronique à l’aide de POP3 et d’IMAP4. Les options de récupération des messages peuvent être configurées au niveau du serveur à l’aide du Centre d’administration Exchange (CAE) ou de l’environnement de ligne de commande Exchange Management Shell ou au niveau de l’utilisateur via l’environnement de ligne de commande Exchange Management Shell.

Pour plus d’informations sur POP3 et IMAP4, voir [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Paramètres POP3 » et « Paramètres IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Configuration du format de récupération des messages POP3 au niveau du serveur

## Configuration du format de récupération des messages POP3 au niveau du serveur à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** \> **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **POP3**.

4.  Sous **Format MIME des messages**, choisissez parmi les paramètres suivants :
    
      - Text
    
      - HTML
    
      - HTML et texte de remplacement
    
      - Texte enrichi
    
      - Texte enrichi et texte de remplacement
    
      - Meilleur format de corps
    
      - TNEF

5.  Cliquez sur **Enregistrer**.

Une fois que vous avez défini les paramètres de format de récupération des messages pour POP3, vous devez redémarrer les services POP3 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Configuration du format de récupération des messages POP3 au niveau du serveur à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple permet de définir l’option de format de récupération des messages sur Texte uniquement pour tous les utilisateurs de POP3 sur le serveur CAS01.

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

Vous pouvez choisir l’un des paramètres suivants : Vous pouvez spécifier la valeur du paramètre *MessageRetrievalMimeFormat* à l’aide d’une valeur numérique ou d’une chaîne de texte.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>format des messages</strong></p></td>
<td><p><strong>Valeur</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> ou  <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou  <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML et texte de remplacement</p></td>
<td><p><code>2</code> ou  <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texte enrichi</p></td>
<td><p><code>3</code> ou  <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texte enrichi et texte de remplacement</p></td>
<td><p><code>4</code> ou  <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Meilleur format de corps</p></td>
<td><p><code>5</code> ou  <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou  <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Une fois que vous avez défini les paramètres de format de récupération des messages pour POP3, vous devez redémarrer les services POP3 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les paramètres de récupération des messages POP3 sur un serveur, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-PopSettings | format-list

2.  Vérifiez que le paramètre *MessageRetrievalMimeFormat* est correctement défini.

## Configuration du format de récupération des messages IMAP4 au niveau du serveur

## Configuration du format de récupération des messages IMAP4 au niveau du serveur à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le Centre d’administration Exchange, rendez-vous sur **Serveurs** \> **Serveurs**.

2.  Dans la liste des serveurs, sélectionnez le serveur d’accès au client, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page des propriétés du serveur, cliquez sur **IMAP4**.

4.  Sous **Format MIME des messages**, choisissez parmi les paramètres suivants :
    
      - Text
    
      - HTML
    
      - HTML et texte de remplacement
    
      - Texte enrichi
    
      - Texte enrichi et texte de remplacement
    
      - Meilleur format de corps
    
      - TNEF

5.  Cliquez sur **Enregistrer**.

Une fois que vous avez défini les paramètres de format de récupération des messages pour IMAP4, vous devez redémarrer les services IMAP4 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Configuration du format de récupération des messages IMAP4 au niveau du serveur à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple permet de définir l’option de format de récupération des messages sur Texte uniquement pour tous les utilisateurs d’IMAP4 sur le serveur CAS01.

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

Vous pouvez choisir l’un des paramètres suivants : Vous pouvez spécifier la valeur du paramètre *MessageRetrievalMimeFormat* à l’aide d’une valeur numérique ou d’une chaîne de texte.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>format des messages</strong></p></td>
<td><p><strong>Valeur</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> ou  <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou  <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML et texte de remplacement</p></td>
<td><p><code>2</code> ou  <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texte enrichi</p></td>
<td><p><code>3</code> ou  <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texte enrichi et texte de remplacement</p></td>
<td><p><code>4</code> ou  <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Meilleur format de corps</p></td>
<td><p><code>5</code> ou  <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou  <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Une fois que vous avez défini les paramètres de format de récupération des messages pour IMAP4, vous devez redémarrer les services IMAP4 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les paramètres de récupération des messages IMAP4 sur un serveur, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-ImapSettings | format-list

2.  Vérifiez que le paramètre *MessageRetrievalMimeFormat* est correctement défini.

## Configuration du format de récupération des messages POP3 pour un utilisateur

## Configuration du format de récupération des messages pour un utilisateur POP3 à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment définir le format de récupération des messages sur Texte uniquement pour l’accès POP3 de l’`USER01`.

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

Vous pouvez choisir l’un des paramètres suivants : Vous pouvez spécifier la valeur du paramètre *PopMessagesRetrievalMimeFormat* à l’aide d’une valeur numérique ou d’une chaîne de texte.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>format des messages</strong></p></td>
<td><p><strong>Valeur</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> ou  <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou  <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML et texte de remplacement</p></td>
<td><p><code>2</code> ou  <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texte enrichi</p></td>
<td><p><code>3</code> ou  <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texte enrichi et texte de remplacement</p></td>
<td><p><code>4</code> ou  <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Meilleur format de corps</p></td>
<td><p><code>5</code> ou  <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou  <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Une fois que vous avez défini les paramètres de format de récupération des messages pour POP3, vous devez redémarrer les services POP3 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services POP3, consultez la rubrique [Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Pour plus d’informations sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les paramètres de récupération des messages POP3 pour un utilisateur, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Vérifiez que la valeur du paramètre *PopMessagesRetrievalMimeFormat* est correcte.

## Configuration du format de récupération des messages IMAP4 pour un utilisateur

## Configuration du format de récupération des messages pour un utilisateur IMAP4 à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment définir le format de récupération des messages sur Texte uniquement pour l’accès IMAP4 de l’`USER01`.

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

Vous pouvez spécifier la valeur du paramètre *ImapMessagesRetrievalMimeFormat* à l’aide d’une valeur numérique ou d’une chaîne de texte.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>format des messages</strong></p></td>
<td><p><strong>Valeur</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> ou  <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> ou  <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML et texte de remplacement</p></td>
<td><p><code>2</code> ou  <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texte enrichi</p></td>
<td><p><code>3</code> ou  <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texte enrichi et texte de remplacement</p></td>
<td><p><code>4</code> ou  <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Meilleur format de corps</p></td>
<td><p><code>5</code> ou  <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> ou  <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Une fois que vous avez défini les paramètres de format de récupération des messages pour IMAP4, vous devez redémarrer les services IMAP4 afin que les paramètres prennent effet. Pour plus d’informations sur le redémarrage des services IMAP4, consultez la rubrique [Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Pour plus d'informations sur la syntaxe et les paramètres, voir [Set-CASMailbox](https://technet.microsoft.com/fr-fr/library/bb125264\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien défini les paramètres de récupération des messages IMAP4 pour un utilisateur, procédez comme suit :

1.  Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Vérifiez que la valeur du paramètre *ImapMessagesRetrievalMimeFormat* est correcte.

## Pour plus d'informations

Une fois que vous avez défini le format de récupération des messages pour les utilisateurs IMAP4 et POP3, vous pouvez également :

[Activer ou désactiver l’accès POP3 pour un utilisateur](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Activation ou désactivation de l'accès IMAP4 pour un utilisateur](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[Configurer les options de calendrier pour IMAP4](configure-calendar-options-for-imap4-exchange-2013-help.md)

[Configurer les options de calendrier pour POP3](configure-calendar-options-for-pop3-exchange-2013-help.md)

