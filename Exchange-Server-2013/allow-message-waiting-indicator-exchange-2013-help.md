---
title: "Activation de l'indicateur d'attente des messages: Exchange 2013 Help"
TOCTitle: Activation de l'indicateur d'attente des messages
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54652755
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation de l'indicateur d'attente des messages

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

L'indicateur de message en attente (MWI) est une fonctionnalité disponible dans la plupart des systèmes de messagerie vocale hérités. Il informe les utilisateurs de la réception de messages vocaux nouveaux ou non écoutés. Dans sa forme la plus courante, un voyant s'allume sur le téléphone d'un utilisateur pour lui signaler la présence d'un message nouveau ou non écouté.

**Contenu de cette rubrique**

Vue d'ensemble

Rôle du serveur de boîtes aux lettres dans l’indicateur d’attente des messages

Messages SIP NOTIFY de l'indicateur de message en attente

Résilience de l'indicateur de message en attente

Administration de l'indicateur de message en attente

Notifications par message texte (SMS) pour les messages vocaux et les appels manqués

## Vue d'ensemble

Les notifications de l'indicateur de message en attente peuvent inclure tout mécanisme signalant la présence d'un message vocal nouveau ou non écouté. Il peut s’agir d’un nouveau message électronique ou d’un message marqué comme non lu. La notification de l'indicateur de message en attente peut prendre l'une des formes suivantes :

  - un nouveau message vocal vu dans Microsoft Outlook ou Outlook Web App ;

  - Un message texte ou SMS (Short Messaging Service) envoyé à un téléphone mobile qui est configuré pour recevoir des messages texte.

  - un appel sortant passé à partir d'une messagerie unifiée Exchange ;

  - un voyant allumé sur un téléphone ;

  - une tonalité de numérotation particulière ;

  - des icônes ou des boutons sur l'écran d'affichage d'un téléphone ;

  - une notification mise en surbrillance dans une application logicielle.

Dans une messagerie unifiée, les messages vocaux d'un utilisateur sont stockés dans sa boîtes aux lettres. Elle est accessible à partir d'un téléphone à l'aide d'Outlook Voice Access, à partir d'un ordinateur portable ou de bureau à l'aide d'Outlook ou Outlook Web App, et à partir de clients de téléphonie mobile. Quand un utilisateur reçoit un nouveau message vocal, ce dernier s'affiche dans son dossier de recherche de Messagerie vocale. Si le message est consulté au moyen d'Outlook ou Outlook Web App, un message électronique est inclus dans le message vocal.

Quand des versions précédentes de messagerie unifiée étaient déployées au sein d'une organisation, l'indicateur de message en attente était pris en charge dans un environnement de passerelle VoIP traditionnel ou dans un environnement PBX IP à l'aide d'une solution ou d'une application tierce, ou était incluse dans la messagerie unifiée Exchange. À partir d'Exchange 2010, l'indicateur de message en attente est également pris en charge quand la messagerie unifiée est déployée avec Microsoft Lync Server. Le mécanisme de notification de l'indicateur de message en attente utilisé par Lync Server dépend du type de téléphone compatible VoIP utilisé par Enterprise Voice et l'utilisateur à extension messagerie unifiée, et peut apparaître sur les éléments suivants :

  - un téléphone ;

  - un affichage de téléphone ;

  - un bouton de pavé de numérotation .

Par défaut, l'indicateur de message en attente est activé pour tous les utilisateurs à extension messagerie unifiée. Il est contrôlé à l'aide de paramètres sur une stratégie de boîte aux lettres de messagerie unifiée ou sur les passerelles IP de messagerie unifiée créées et associées à un plan de numérotation de messagerie vocale. Il fonctionne également pour les messages vocaux protégés.

Pour implémenter l'indicateur de message en attente dans un environnement de téléphonie classique avec des passerelles VoIP, des PBX IP ou des PBX compatibles SIP, un serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange envoie un message NOTIFY conforme au protocole SIP de l'indicateur de message en attente à un *homologue SIP*, qui est un PBX IP, une passerelle VoIP utilisée avec un PBX hérité, ou un PBX compatible SIP. Si vous avez déployé Lync Server, les serveurs Lync sont également considérés comme des homologues SIP. Le PBX ou PBX IP allume un voyant sur le téléphone de bureau de l'utilisateur pour informer ce dernier de l'existence d'un message vocal non encore écouté.

Les appelants peuvent laisser des messages vocaux de deux manières : à l'aide d'un répondeur automatique ou de Outlook Voice Access. Avec un répondeur automatique, un serveur de boîtes aux lettres répond à l'appel entrant en permettant à l'appelant de laisser un message vocal destiné à un utilisateur. Avec Outlook Voice Access, quand un appelant compose un numéro Outlook Voice Access, il peut utiliser le système de menus pour laisser un message vocal destiné à un correspondant à extension messagerie unifiée.

Vue d'ensemble

## Rôle du serveur de boîtes aux lettres dans l’indicateur d’attente des messages

Quand un appelant appelle un utilisateur à extension messagerie unifiée et que ce dernier ne répond pas, le service de messagerie unifiée Microsoft Exchange sur un serveur de boîtes aux lettres reçoit des informations de changement d'état de l'indicateur de message en attente, et utilise un message SIP NOTIFY pour envoyer la demande de changement de notification à une passerelle VoIP, un PBX IP ou un PBX compatible SIP. Le changement de notification inclut les informations suivantes :

  - indicateur de message en attente activé (Oui ou Non) ;

  - nombre de messages vocaux nouveaux ou marqués comme non écoutés ;

  - nombre de messages vocaux anciens ou marqués comme écoutés ;

  - nombre de messages vocaux urgents nouveaux ou marqués comme non écoutés ;

  - nombre de messages vocaux urgents anciens ou marqués comme écoutés ;

  - numéro de poste principal dans le plan de numérotation de messagerie unifiée principal ;

  - adresse IP ou nom de domaine complet (FQDN) de l'homologue SIP à utiliser pour les messages SIP NOTIFY ;

  - type de sécurité du plan de numérotation de messagerie unifiée (Non sécurisé, Sécurisé SIP ou Sécurisé). Ces informations sont utilisées pour déterminer si la connexion à la passerelle VoIP ou au PBX IP doit être SIP sur TCP ou SIP sur TLS. Le protocole TLS est pris en charge pour les messages SIP NOTIFY de l'indicateur de message en attente.

Un serveur de boîtes aux lettres utilise les informations de diversion figurant dans l'en-tête de l'appel entrant pour déterminer le numéro de poste ou de téléphone de l'utilisateur à extension messagerie unifiée. Une fois le numéro de poste ou de téléphone déterminé, le serveur de boîtes aux lettres envoie la requête à l'homologue SIP. L’homologue SIP modifie l’état de l’indicateur d’attente de messages, puis active la notification sur le téléphone de l’utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Même si les pannes de PBX sont rares, la messagerie unifiée actualise automatiquement l'état de l'indicateur de message en attente pour chaque boîte aux lettres au moins une fois toutes les 12 heures. Il n'existe aucun moyen de forcer une actualisation. Toutefois, si le PBX ou le PBX IP est mis hors tension, entraînant l'extension de tous les voyants de l'indicateur de message en attente, un délai maximal de 6 heures s'écoule avant le rétablissement de l'état approprié des voyants.</td>
</tr>
</tbody>
</table>


Vue d'ensemble

## Messages SIP NOTIFY de l'indicateur de message en attente

Les notifications de l'indicateur de message en attente utilisent des messages SIP NOTIFY pour communiquer avec les homologues SIP. Des informations de changement d'état de l'indicateur de message en attente sont incluses dans le message SIP NOTIFY. Elles indiquent si les notifications de l'indicateur de message en attente seront ou non envoyées aux utilisateurs. À chaque changement d'état de l'indicateur de message en attente, l'Assistant Boîte aux lettres envoie des informations au service de messagerie unifiée Microsoft Exchange en cours d'exécution sur un serveur de boîtes aux lettres. Lorsque le service de messagerie unifiée reçoit ces informations, il analyse le message pour obtenir l'homologue SIP cible et les informations de changement d'état de l'indicateur de message en attente. Il compose ensuite un message SIP NOTIFY en insérant les informations de changement d'état de l'indicateur de message en attente dans le corps du message, puis envoie ce dernier à l'homologue SIP.

L'indicateur de message en attente est basé sur la norme RFC 3842. Cette dernière stipule que des notifications d'événement SIP doivent être utilisées pour les notifications de message en attente. L'indicateur de message en attente est basé sur le modèle SIP, et actionné par les points de terminaison détectés dans un système de messagerie unifiée. Les points de terminaison SIP, également appelés homologues SIP, qui obtiennent des informations de l'indicateur de message en attente doivent envoyer un message SIP SUBSCRIBE au service de messagerie unifiée. Le service répond par un message NOTIFY indiquant que l'abonnement a été accepté. Toutes les informations de changement d'état de l'indicateur de message en attente sont acheminées à partir du système de messagerie unifiée vers un point de terminaison SIP à l'aide de messages NOTIFY qui sont incorporés dans l'abonnement précédemment créé. La syntaxe exacte du message SIP NOTIFY à envoyer à l'homologue SIP est basée sur le format décrit dans la norme RFC 3842.

Quand le service de messagerie unifiée sur un serveur de boîtes aux lettres envoie un message MWI NOTIFY à l'homologue SIP, l'en-tête de l'événement est « message-summary », ce qui indique qu'il s'agit d'un message NOTIFY lié à l'indicateur de message en attente. Le champ d'en-tête À indique le point de terminaison SIP pour lequel le service de l'indicateur de message en attente doit être fourni. L'en-tête État d'abonnement doit être défini sur « terminé » et non sur « actif ». Les actions qui se produisent en réponse au message SIP NOTIFY sont les suivantes :

1.  L'homologue transmet ces informations au PBX à l'aide d'un protocole à commutation de circuit, tel que SMDI.

2.  Le PBX envoie un message de réussite via un protocole à commutation de circuit.

3.  L'homologue SIP peut répondre avec l'un des messages suivants : 200 OK (Réussite) ou 480 (Temporairement indisponible). Un serveur de boîtes aux lettres peut gérer toutes ces réponses et des réponses supplémentaires en cas d'échec.

## Indicateur de message en attente dans un environnement téléphonique classique

Dans un environnement téléphonique classique, un appel entrant est reçu par le PBX puis envoyé à la passerelle VoIP, ou reçu par le PBX IP ou le PBX compatible SIP. Le serveur de boîtes aux lettres et l'Assistant Boîte aux lettres sont utilisés pour déterminer l'état de l'indicateur de message en attente pour l'utilisateur à extension messagerie unifiée. Ils sont responsables du renvoi de la notification SIP à la passerelle VoIP ainsi qu'au PBX, au PBX IP ou au PBX compatible SIP hérités.

Dans un environnement téléphonique classique, le flux d'appels et la notification de l'indicateur de message en attente se déroulent comme suit :

1.  L'appel entrant est reçu par le PBX hérité, transmis à la passerelle VoIP ou à un PBX IP ou compatible SIP, puis transmis au numéro de poste de l'utilisateur à extension messagerie unifiée. L'utilisateur ne répond pas et l'appelant est invité à laisser un message vocal.

2.  La passerelle VoIP ou le PBX IP soumet l'appel au serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange.

3.  Le serveur de boîtes aux lettres effectue une requête LDAP pour localiser les informations de l’utilisateur à extension messagerie unifiée, telles que le numéro de poste et le message d’accueil personnel de l’utilisateur. Le message d'accueil de l'utilisateur à extension messagerie unifiée est lu.

4.  Le message vocal créé par le service de messagerie unifiée est soumis au service de transport Microsoft Exchange sur le même serveur de boîtes aux lettres.

5.  Le service de transport sur le serveur de boîtes aux lettres soumet le message vocal au serveur de boîtes aux lettres qui contient la boîte aux lettres de l’utilisateur. L'Assistant Boîte aux lettres reçoit un événement MAPI pour un nouveau message vocal.

6.  L'Assistant Boîte aux lettres lit le plan de numérotation de messagerie unifiée et la stratégie de boîte aux lettres de messagerie unifiée pour déterminer si des notifications de l'indicateur de message en attente doivent être envoyées à l'utilisateur à extension messagerie unifiée. L'Assistant Boîte aux lettres recherche tous les serveurs de messagerie unifiée associés au plan de numérotation de messagerie unifiée de l'utilisateur à extension messagerie unifiée. L'Assistant Boîte aux lettres essaie d'envoyer l'événement RPC au premier serveur de boîtes aux lettres renvoyé. En cas d"échec, il fait une nouvelle tentative sur le serveur suivant. Il poursuit ses tentatives pendant 5 minutes, ou jusqu'à ce que tous les serveurs aient été testés. Si tous les appels RPC échouent, l'Assistant Boîte aux lettres consigne l'erreur dans l'Observateur d'événements. Le serveur de boites aux lettres recherche toutes les passerelles IP de messagerie unifiée qui sont associées au plan de numérotation de messagerie unifiée de la boîte aux lettres de l'utilisateur à extension messagerie unifiée.

7.  La messagerie unifiée envoie un message SIP NOTITY à la première passerelle VoIP ou au premier PBX IP renvoyé par la recherche. En cas d'échec, le serveur de boîtes aux lettres passe à la passerelle VoIP ou au PBX IP suivant. Le serveur de boîtes aux lettres continue à essayer les passerelles VoIP ou PBX IP pendant cinq minutes. Si toutes les tentatives de recherche de passerelle VoIP ou de PBX IP échouent, le serveur de boîtes aux lettres consigne une erreur. En cas de détection d'une passerelle VoIP ou d'un PBX IP, la passerelle envoie la notification au PBX, qui envoie à son tour une notification de l'événement de l'indicateur de message en attente au téléphone de l'utilisateur pour allumer le voyant. Si un PBX IP est utilisé, la notification de l’indicateur de message en attente est traitée par le PBX IP et il allume ensuite le voyant du téléphone de l’utilisateur. Les autres mécanismes de notification de l'indicateur de message en attente sont énumérés dans la Vue d'ensemble. Le type de notification dépend du matériel du PBX ou du PBX IP et de l'utilisation ou non de Lync Server. Cela dépend également du type de téléphone (analogique, numérique ou VoIP) qui est utilisé.

Vue d'ensemble

## Indicateur de message en attente dans un environnement Lync Server

Dans les environnements téléphoniques disposant de Lync Server, un appel entrant peut être envoyé à partir d'un téléphone externe à un serveur de médiation, ou bien envoyé à partir d'un client Lync ou d'un téléphone UC (Unified Communications) ou compatible VoIP. L'appel reçu est envoyé au pool de serveurs frontaux Lync Server. Le serveur de boîtes aux lettres et l'Assistant Boîte aux lettres sont utilisés pour déterminer l'état de l'indicateur de message en attente pour l'utilisateur à extension messagerie unifiée, et pour remettre cette notification au client ou au téléphone analogique, numérique, UC ou VoIP.

Dans un environnement téléphonique disposant de Lync Server, le flux d'appels et la notification de l'indicateur de message en attente se présentent comme suit :

1.  L'appel est envoyé à partir de l'un des dispositifs suivants :
    
      - un téléphone externe à l'organisation (via un serveur de médiation) ;
    
      - un client Lync ;
    
      - un téléphone UC ou compatible VoIP.

2.  L'appel entrant est reçu par le pool de serveurs frontaux Lync Server, puis envoyé au téléphone ou au point de terminaison SIP de l'utilisateur à extension messagerie unifiée. L'utilisateur ne répond pas et l'appelant est invité à laisser un message vocal.

3.  Le pool de serveurs frontaux Lync Server soumet l’appel à un serveur de boîtes aux lettres au sein du réseau local et la boîte aux lettres de l’utilisateur est trouvée.

4.  Le serveur de boîtes aux lettres effectue une requête LDAP pour trouver des informations sur l'utilisateur à extension messagerie unifiée, telles que son numéro de poste et son messages d'accueil. Le message d'accueil est lus et l'appelant est invité à laisser un message vocal.

5.  Le message vocal créé par le service de messagerie unifiée est soumis au service de transport sur le même serveur de boîtes aux lettres dans le même site.

6.  Le service de transport soumet le message vocal au serveur de boîtes aux lettres qui contient la boîte aux lettres de l’utilisateur. L'Assistant Boîte aux lettres reçoit un événement MAPI pour le nouveau message vocal.

7.  L'Assistant Boîte aux lettres lit le plan de numérotation de messagerie unifiée et la stratégie de boîte aux lettres de messagerie unifiée pour déterminer si des notifications de l'indicateur de message en attente doivent être envoyées à l'utilisateur. L'Assistant Boîte aux lettres interroge tous les serveurs de boîtes aux lettres associés au plan de numérotation de messagerie unifiée de l'utilisateur. L'Assistant Boîte aux lettres essaie d'envoyer l'événement RPC au premier serveur de boîtes aux lettres renvoyé. En cas d'échec, l'Assistant Boîte aux lettres effectue une tentative sur le serveur suivant. Il continue à rechercher un serveur de boîtes aux lettres pendant cinq minutes ou jusqu'à ce que tous les serveurs aient été testés. Si tous les appels RPC échouent, l'Assistant Boîte aux lettres consigne une erreur dans l'Observateur d'événements. Le serveur de boites aux lettres recherche Active Directory pour toutes les passerelles IP de messagerie unifiée qui sont associées au plan de numérotation de messagerie unifiée de l'utilisateur à extension messagerie unifiée.

8.  La messagerie unifiée envoie un message SIP NOTITY à la première passerelle VoIP ou au premier PBX IP renvoyé par la recherche. En cas d'échec, le serveur de boîtes aux lettres passe à la passerelle VoIP ou au PBX IP suivant. Le serveur de boîtes aux lettres continue à essayer de trouver une passerelle VoIP ou un PBX IP pendant cinq minutes. Si toutes les tentatives de recherche de passerelle VoIP ou de PBX IP échouent, le serveur de boîtes aux lettres consigne une erreur. Si la tentative aboutit, la passerelle VoIP ou le PBX IP envoient la notification au pool de serveurs frontaux Lync Server, qui envoie à son tour une notification de l'événement de l'indicateur de message en attente à un point de terminaison SIP utilisé par l'utilisateur, le téléphone de l'utilisateur ou un client Lync.

Vue d'ensemble

## Résilience de l'indicateur de message en attente

Lorsque vous déployez des serveurs de boîtes aux lettres et d’accès au client, des plans de numérotation de messagerie unifiée et des passerelles IP de messagerie unifiée, si vous utilisez l’indicateur de message en attente pour des utilisateurs à extension messagerie unifiée, nous vous recommandons de déployer plusieurs serveurs de boîtes aux lettres et d’accès au client, ainsi que plusieurs passerelles VoIP et PBX IP afin de créer une résilience et une tolérance aux pannes. Cette solution contribue également à la résilience de l'indicateur de message en attente, car elle permet d'envoyer les notifications de l'indicateur de message en attente de plusieurs manières, comme décrit dans la section précédente.

Pour activer la tolérance aux pannes pour l'indicateur de message en attente dans la messagerie unifiée, vous devez créer et configurer un ou plusieurs des éléments suivants :

  - un plan de numérotation de messagerie unifiée associé à l'utilisateur à extension messagerie unifiée qui recevra des notifications de l'indicateur de message en attente ;

  - une stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur à extension messagerie unifiée qui recevra des notifications de l'indicateur de message en attente ;

  - une passerelle IP de messagerie unifiée associée au plan de numérotation de messagerie unifiée, lui-même lié à l'utilisateur à extension messagerie unifiée qui recevra des notifications de l'indicateur de message en attente.

  - En cas d'utilisation de Lync Server, tous les serveurs d'accès au client et de boîtes aux lettres doivent être ajoutés au plan de numérotation URI SIP de messagerie unifiée qui est associé à l'utilisateur à extension messagerie unifiée qui recevra des notifications de l'indicateur de message en attente.

## Administration de l'indicateur de message en attente

Vous pouvez administrer l'indicateur de message en attente en configurant les paramètres sur deux composants de messagerie unifiée : les stratégies de boîte aux lettres de messagerie unifiée et les passerelles IP de messagerie unifiée. Pour ces deux composants, vous pouvez activer ou désactiver les notifications de l'indicateur de message en attente en utilisant la cmdlet **Set-UMMailboxPolicy** ou la cmdlet **Set-UMIPgateway** dans l'environnement de ligne de commande Exchange Management Shell. Vous pouvez également configurer les paramètres à l'aide du Centre d'administration Exchange (EAC). Vous pouvez afficher l'état des notifications de l'indicateur de message en attente à l'aide de la cmdlet **Get-UMMailboxPolicy** et de la cmdlet **Get-UMIPgateway** dans l'environnement de ligne de commande Exchange Management Shell, ou en affichant les paramètres dans le CAE.

## Stratégies de boîte aux lettres de messagerie unifiée et indicateur de message en attente

Vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée pour appliquer un ensemble courant de paramètres de stratégie de messagerie unifiée à une collection de boîtes aux lettres à extension messagerie unifiée. Par exemple, vous pouvez utiliser une stratégie de boîte aux lettres de messagerie unifiée pour appliquer des paramètres de stratégie de code confidentiel, des restrictions d'appel et des paramètres de l'indicateur de message en attente. Si vous activez ou désactivez l'indicateur de message en attente sur une stratégie de boîte aux lettres de messagerie unifiée, l'activation ou la désactivation prendra effet pour tous les utilisateurs à extension messagerie unifiée associés à la stratégie. Le paramètre de l'indicateur de message en attente peut également s'appliquer à un sous-ensemble d'utilisateurs associés au plan de numérotation de messagerie unifiée. Pour en savoir plus sur les stratégies de boîtes aux lettres de messagerie unifiée, notamment l'activation et la désactivation de l'indicateur de message en attente pour un groupe d'utilisateurs à extension messagerie unifiée, consultez la rubrique [Procédures de stratégie de boîte aux lettres de messagerie unifiée](um-mailbox-policy-procedures-exchange-2013-help.md).

Vous pouvez utiliser le CAE ou la cmdlet **Set-UMMailboxPolicy** dans l'environnement de ligne de commande Exchange Management Shell pour configurer le paramètre de l'indicateur de message en attente, comme illustré dans le tableau suivant.

### Paramètre de l'indicateur de message en attente sur une stratégie de boîte aux lettres de messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre de l'environnement de ligne de commande Exchange Management Shell</th>
<th>Paramètre disponible dans le CAE ?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>AllowMessageWaitingIndicator</em> spécifie si les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée peuvent recevoir des notifications de l'indicateur de message en attente lors de la réception d'un nouveau message vocal. La valeur par défaut est <code>$true</code>.</p>
<p>Si ce paramètre est activé, les notifications de l'indicateur de message en attente sont envoyées aux utilisateurs associés à une stratégie unique de boîte aux lettres de messagerie unifiée pour les appels pris par une passerelle IP de messagerie unifiée. Ce paramètre autorise la passerelle IP de messagerie unifiée à recevoir et envoyer des messages SIP NOTIFY sur le téléphone d'utilisateurs à extension messagerie unifiée ou à des points de terminaison SIP.</p>
<p></p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la gestion des paramètres de l'indicateur de message en attente sur une stratégie de boîte aux lettres de messagerie vocale, consultez les rubriques suivantes :

  - [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Activer le Message en attente indicateur (MWI) pour les utilisateurs](enable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Désactiver les messages en attente indicateur (MWI) pour les utilisateurs](disable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/fr-fr/library/bb124903\(v=exchg.150\))

## Passerelles IP de messagerie unifiée et indicateur de message en attente

Si vous désactivez l'indicateur de message en attente sur une passerelle IP de messagerie unifiée, les notifications sont désactivées pour tous les utilisateurs qui se connectent à la passerelle VoIP ou PBX IP qu'elle représente. La désactivation de l’indicateur de message en attente sur une seule passerelle IP de messagerie unifiée liée à un plan de numérotation de messagerie unifiée peut désactiver les notifications de l’indicateur de message en attente pour tous les utilisateurs à extension messagerie unifiée associés à un ou plusieurs plans de numérotation de messagerie unifiée, ou à une ou plusieurs stratégies de boîte aux lettres de messagerie unifiée. Pour en savoir plus sur les stratégies de boîtes aux lettres de messagerie unifiée, notamment l'activation et la désactivation de l'indicateur de message en attente pour un groupe d'utilisateurs à extension messagerie unifiée, consultez la rubrique [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md).

Vous pouvez utiliser le CAE ou la cmdlet **Set-UMMailboxPolicy** dans l'environnement de ligne de commande Exchange Management Shell pour configurer le paramètre de l'indicateur de message en attente, comme illustré dans le tableau suivant.

### Paramètre de l'indicateur de message en attente sur une passerelle IP de messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre de l'environnement de ligne de commande Exchange Management Shell</th>
<th>Paramètre disponible dans le CAE ?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>MessageWaitingIndicatorAllowed</em> spécifie si la passerelle IP de messagerie unifiée est activée pour permettre l'envoi de messages SIP NOTIFY à des utilisateurs associés à un plan de numérotation de messagerie unifiée. La valeur par défaut est <code>$true</code>.</p>
<p>Si ce paramètre est activé, des notifications de message vocal peuvent être envoyées aux utilisateurs pour les appels reçus par la passerelle IP de messagerie unifiée. Ce paramètre autorise la passerelle IP de messagerie unifiée à envoyer des notifications de message en attente à des utilisateurs à extension messagerie unifiée.</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la gestion des paramètres de l'indicateur de message en attente, consultez les rubriques suivantes :

  - [Gestion d'une passerelle IP de messagerie unifiée](manage-a-um-ip-gateway-exchange-2013-help.md)

  - [Autoriser les messages en attente indicateur (MWI) sur une passerelle IP de messagerie unifiée](allow-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Empêcher le Message en attente indicateur (MWI) sur une passerelle IP de messagerie unifiée](prevent-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Set-UMIPGateway](https://technet.microsoft.com/fr-fr/library/aa996577\(v=exchg.150\))

Vue d'ensemble

## Notifications par message texte (SMS) pour les messages vocaux et les appels manqués

Comme indiqué précédemment, une notification d'indicateur de message en attente est un mécanisme signalant la présence d'un nouveau message vocal. Outre les mécanismes déjà décrits, les utilisateurs peuvent être informés de la présence d'un message vocal en attente via un message texte, ou SMS (Short Message Service). Il s'agit d'un type de notification de l'indicateur de message en attente pour les nouveaux messages vocaux différent du signal lumineux classique ou d'autres mécanismes.

Un SMS est envoyé sur le téléphone mobile d'un utilisateur quand un appelant laisse un nouveau message vocal. Les utilisateurs peuvent également recevoir un SMS qui les informe lorsqu’ils manquent un appel téléphonique et qu’aucun message vocal n’est laissé. Le SMS de notification d'appel en absence peut être envoyé à l'utilisateur en même temps que la notification de nouveau message vocal.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le SMS envoyé à un utilisateur comporte un aperçu du message vocal.</td>
</tr>
</tbody>
</table>


Les notifications par SMS utilisent des paramètres différents de ceux de l'indicateur de message en attente sur la passerelle IP de messagerie unifiée ou la stratégie de boîte aux lettres de messagerie unifiée. Les notifications par SMS de nouveaux messages vocaux et d'appels manqués sont configurées dans les stratégies de boîtes aux lettres de messagerie unifiée et les boîtes aux lettres de messagerie unifiée. Vous pouvez activer ou désactiver les notifications par SMS à l'aide de la cmdlet **Set-UMMailboxPolicy** et de la cmdlet **Set-UMMailbox** dans l'environnement de ligne de commande Exchange Management Shell. Vous pouvez afficher l'état des notifications par SMS à l'aide des cmdlets **Get-UMMailboxPolicy** et **Get-UMMailbox**. Il n’est pas possible de configurer des notifications par SMS dans le Centre d’administration Exchange.

Le tableau suivant montre le paramètre d'une boîte aux lettres de messagerie unifiée qui doit être configuré pour qu'un utilisateur reçoive des SMS de notification de message vocal et d'appel en absence :

### Paramètres de notification par SMS sur une boîte aux lettres d’utilisateur

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>Non</p></td>
<td><p>Le paramètre <em>UMSMSNotificationOption</em> spécifie si un utilisateur à extension messagerie unifiée peut recevoir des notifications par SMS pour les messages vocaux uniquement, pour les messages vocaux et les appels manqués, ou s'il n'est pas autorisé à recevoir de notifications. Les valeurs pour ce paramètre sont les suivantes : <code>VoiceMail</code>, <code>VoiceMailAndMissedCalls</code> et <code>None</code>. La valeur par défaut est <code>None</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la gestion des paramètres de notification par SMS d’une boîte aux lettres d’utilisateur, consultez les rubriques suivantes :

  - [Gestion des paramètres de messagerie vocale d'un utilisateur](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/fr-fr/library/bb124893\(v=exchg.150\))

Le tableau suivant montre le paramètre d'une stratégie de boîte aux lettres de messagerie unifiée qui doit être configuré pour qu'un utilisateur reçoive des SMS de notification de message vocal et d'appel en absence :

### Paramètres de notification par SMS d'appel en absence sur une stratégie de boîte aux lettres de messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre de l'environnement de ligne de commande Exchange Management Shell</th>
<th>Paramètre disponible dans le CAE ?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>Non</p></td>
<td><p>Le paramètre <em>AllowSMSNotification</em> spécifie si les utilisateurs à extension messagerie vocale dont les boîtes aux lettres sont associées à la stratégie de boîte aux lettres de messagerie vocale sont autorisés à recevoir des notifications par SMS sur leur téléphone mobile. Si ce paramètre est défini sur <code>$true</code>, vous devez également utiliser la cmdlet <strong>Set-UMMailbox</strong> et définir le paramètre <em>UMSMSNotificationOption</em> pour l'utilisateur à extension messagerie unifiée sur <code>voicemail</code> ou <code>VoiceMailAndMissedCalls</code>. La valeur par défaut est <code>$true</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la gestion des paramètres de notification par SMS, consultez les rubriques suivantes :

  - [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/fr-fr/library/bb124903\(v=exchg.150\))

Pour que les notifications par SMS pour les messages vocaux et les appels manqués fonctionnent correctement, vous devez effectuer les tâches suivantes :

1.  Utilisez le CAE ou l'environnement de ligne de commande Exchange Management Shell pour activer la messagerie unifiée pour un utilisateur et l'associer à la stratégie de boîte aux lettres de messagerie unifiée appropriée.

2.  Sur la stratégie de boîte aux lettres de messagerie unifiée qui est liée à l’utilisateur, vérifiez que le paramètre *AllowSMSNotification* est défini sur `$true`. Pour le définir sur `$true`, exécutez la commande suivante : `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  Sur la boîte aux lettres de l’utilisateur, activez les notifications par SMS en définissant le paramètre *UMSMSNotificationOption* sur `VoiceMailAndMissedCalls` ou `VoiceMail`.

4.  Le paramètre par défaut étant `None`, vous devez exécuter la commande suivante à partir de l'environnement de ligne de commande Exchange Management Shell et définir l'option de notification par SMS sur `VoiceMailAndMissedCalls` ou `VoiceMail`. Par exemple : `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le paramètre <em>AllowSMSNotification</em> sur la stratégie de boîte aux lettres de messagerie unifiée et le paramètre <em>UMSMSNotificationOption</em> sur la boîte aux lettres de l’utilisateur doivent avoir la valeur <code>$true</code> pour que les notifications par SMS fonctionnent.</td>
    </tr>
    </tbody>
    </table>


Outre le fait que vous configuriez la stratégie de boîte aux lettres de messagerie unifiée et la boîte aux lettres de l’utilisateur pour activer les notifications par SMS pour les nouveaux messages vocaux et les appels manqués, l’utilisateur doit activer et configurer les notifications par SMS quand il se connecte à Outlook Web App. Pour définir et configurer les notifications de message texte, il doit procéder ainsi :

1.  Se connecter à Outlook Web App et accéder à **Options** \> **Téléphone** \> **Messagerie vocale**.

2.  Dans la page **Messagerie vocale**, sous **Notifications**, cliquer sur **Définir les notifications**.

3.  Dans la page **Messagerie texte**, cliquer sur le bouton **Activer les notifications**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ne cliquez pas sur <strong>Notifications de messagerie vocale</strong> sinon vous reviendrez à la page <strong>Messagerie vocale</strong>.</td>
    </tr>
    </tbody>
    </table>


4.  Dans la page **Messagerie texte**, sous **Paramètres régionaux**, sélectionner les paramètres régionaux ou l'emplacement de l'opérateur mobile de messagerie texte dans la liste déroulante.

5.  Dans la page **Messagerie texte**, sous **Opérateur mobile**, sélectionner l'opérateur mobile de messagerie texte dans la liste déroulante, puis cliquer sur **Suivant**.

6.  Sur la page **Messagerie texte**, dans la zone **Saisissez votre numéro de téléphone et cliquez sur Suivant**, entrez le numéro de téléphone mobile qui est utilisé pour les notifications par SMS, puis cliquez sur **Suivant**. Un code secret à six chiffres est envoyé sur le téléphone mobile de l'utilisateur. Si vous n’avez pas reçu de code secret, cliquez sur **Je n’ai pas reçu de mot de passe et j’ai besoin qu’il me soit renvoyé**.

7.  Entrer le code secret dans la zone **Code secret**, puis cliquer sur **Terminer**.

8.  Une fois les notifications par SMS activées, l'utilisateur peut cliquer sur **Définir les notifications de messagerie vocale** dans la page **Messagerie texte**. Il est alors renvoyé à la page de messagerie vocale, où il peut accéder à la section **Notifications** pour définir les options de notification par SMS pour les appels manqués et les messages vocaux.

Vue d'ensemble

