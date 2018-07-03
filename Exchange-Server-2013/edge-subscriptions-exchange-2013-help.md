---
title: 'Abonnements Edge: Exchange 2013 Help'
TOCTitle: Abonnements Edge
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61180537
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Abonnements Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les serveurs de transport Edge réduisent la surface d’attaque en traitant tout le flux de messagerie Internet et en fournissant des services d’hôte actif et de relais SMTP pour votre organisation Exchange. Des couches supplémentaires de protection et de sécurité des messages sont fournies par une série d’agents qui s’exécutent sur le serveur de transport Edge dans le réseau de périmètre de votre organisation. Ces agents prennent en charge les fonctionnalités qui fournissent une protection contre les virus et le courrier indésirable et appliquent des règles de transport pour contrôler le flux de messages.

Les abonnements Edge permettent de renseigner l’instance des services AD LDS (Active Directory Lightweight Directory Services) sur le serveur de transport Edge avec les données Active Directory. Bien que la création d’un abonnement Edge soit facultative, l’abonnement d’un serveur de transport Edge à l’organisation Exchange offre une expérience de gestion plus simple et améliore les fonctionnalités de blocage du courrier indésirable. Vous devez créer un abonnement Edge si vous prévoyez d’utiliser les fonctions de recherche de destinataire ou d’agrégation de listes fiables, ou si vous envisagez de renforcer la sécurité des communications SMTP avec des domaines partenaires via l’utilisation du protocole MTLS (Mutual Transport Layer Security).

**Contenu de cette rubrique**

Processus d’abonnement Edge

Service Microsoft Exchange EdgeSync

Gestion des abonnements Edge

## Processus d’abonnement Edge

Un serveur de transport Edge ne dispose pas d’un accès direct à Active Directory. Toutes les informations de configuration et de destinataire que le serveur de transport Edge utilise pour traiter les messages sont stockées dans AD LDS. La création d’un abonnement Edge établit une réplication automatique et sécurisée des informations d’Active Directory vers AD LDS. Le processus d’abonnement Edge fournit les informations d’identification utilisées pour établir une connexion LDAP sécurisée entre les serveurs de boîtes aux lettres Exchange 2013 et un serveur de transport Edge abonné. Le service Microsoft Exchange EdgeSync (EdgeSync) qui s’exécute sur des serveurs de boîtes aux lettres effectue régulièrement une synchronisation monodirectionnelle pour transférer des données à jour vers AD LDS. Ceci réduit les tâches d’administration que vous effectuez dans le réseau de périmètre en vous permettant de configurer le serveur de boîtes aux lettres, puis de synchroniser ces informations sur le serveur de transport Edge.

Vous abonnez un serveur de transport Edge au site Active Directory contenant les serveurs de boîtes aux lettres chargés de transférer des messages vers et à partir de vos serveurs de transport Edge. Le processus d’abonnement Edge crée une affiliation d’appartenance au site Active Directory pour le serveur de transport Edge. L’affiliation au site permet aux serveurs de boîtes aux lettres dans l’organisation Exchange de relayer les messages vers le serveur de transport Edge pour les remettre sur Internet sans qu’il soit nécessaire de configurer des connecteurs d’envoi explicites.

Plusieurs serveurs de transport Edge peuvent être abonnés à un site Active Directory unique. Toutefois, un serveur de transport Edge ne peut être abonné à plusieurs sites Active Directory. Si plusieurs serveurs de transport Edge sont déployés, chaque serveur peut être abonné à un site Active Directory différent. Chaque serveur de transport Edge requiert un abonnement Edge individuel.

Pour déployer un serveur de transport Edge et l’abonner à un site Active Directory, procédez comme suit :

1.  Installez le rôle serveur de transport Edge.

2.  Vérifiez que les serveurs de boîtes aux lettres et le serveur de transport Edge parviennent à se localiser via la résolution de nom DNS.

3.  Sur le serveur de boîte aux lettres, configurez les objets et paramètres devant être répliqués sur le serveur de transport Edge.

4.  Sur le serveur de transport Edge, créez et exportez le fichier d’abonnement Edge.

5.  Copiez le fichier d’abonnement Edge sur un serveur de boîtes aux lettres ou un partage de fichiers accessible à partir du site Active Directory sur lequel se trouvent vos serveurs de boîtes aux lettres.

6.  Importez le fichier d’abonnement Edge dans le site Active Directory.

## Actions générées lors de la création d’un abonnement Edge

Lorsque vous créez un fichier d’abonnement Edge (en exécutant la cmdlet **New-EdgeSubscription** sur le serveur de transport Edge), les actions suivantes se produisent :

  - Un compte AD LDS compte appelé le compte de réplication d’amorçage EdgeSync (ESBRA) est créé. Les informations d’identification du compte ESBRA permettent d’authentifier la première connexion EdgeSync au serveur de transport Edge. Ce compte est configuré pour expirer 24 heures après sa création. Par conséquent, vous devez terminer le processus d’abonnement en six étapes décrit dans la section précédente dans les 24 heures. Si l’expiration du compte ESBRA intervient avant la fin du processus d’abonnement Edge, vous devrez à nouveau exécuter la cmdlet **New-EdgeSubscription** pour créer un fichier d’abonnement Edge.

  - Les informations d’identification du compte ESBRA sont récupérées depuis AD LDS et écrites dans le fichier d’abonnement Edge. La clé publique du certificat auto-signé du serveur de transport Edge est également exportée vers le fichier d’abonnement Edge. Les informations d’identification écrites dans le fichier d’abonnement Edge sont propres au serveur qui a exporté le fichier.

  - Tout objet de configuration précédemment créé sur le serveur de transport Edge qui est sur le point d’être répliqué dans AD LDS à partir d’Active Directory est supprimé d’AD LDS et les cmdlets de l’environnement Exchange Management Shell utilisées pour configurer ces objets sont désactivées. Toutefois, vous pouvez toujours utiliser les cmdlets **Get-\*** pour afficher ces objets. L’exécution de la cmdlet **New-EdgeSubscription** désactive les cmdlets suivantes sur le serveur de transport Edge :
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

Lorsque vous importez le fichier d’abonnement Edge sur le serveur de boîtes aux lettres en exécutant la cmdlet **New-EdgeSubscription** sur le serveur de boîtes aux lettres :

  - L’abonnement Edge est créé, associant ainsi un serveur de transport Edge à une organisation Exchange. EdgeSync propagera les données de configuration dans ce serveur de transport Edge, créant ainsi un objet de configuration Edge dans Active Directory.

  - Chaque serveur de boîtes aux lettres dans le site Active Directory reçoit une notification d’Active Directory signalant l’abonnement d’un nouveau serveur de transport Edge. Le serveur de boîtes aux lettres récupère le compte ESBRA à partir du fichier d’abonnement Edge. Le serveur de boîtes aux lettres chiffre ensuite le compte ESBRA en utilisant la clé publique du certificat auto-signé du serveur de transport Edge. Les informations d’identification chiffrées sont ensuite écrites sur l’objet de configuration Edge.

  - Chaque serveur de boîtes aux lettres chiffre également le compte ESBRA en utilisant sa propre clé publique, puis stocke les informations d’identification dans son propre objet de configuration.

  - Les comptes de réplication EdgeSync (ESRA) sont créés dans Active Directory pour chaque paire de serveurs de transport Edge et de boîtes aux lettres. Chaque serveur de boîtes aux lettres stocke ses informations d’identification de compte ESRA en tant qu’attributs de l’objet de configuration du serveur de boîtes aux lettres.

  - Les connecteurs d’envoi sont automatiquement créés pour relayer les messages à l’extérieur, du serveur de transport Edge vers Internet et à l’intérieur, du serveur de transport Edge vers l’organisation Exchange.

  - Le service Microsoft Exchange EdgeSync exécuté sur les serveurs de boîtes aux lettres utilise les informations d’identification du compte ESBRA pour établir une connexion LDAP sécurisée entre un serveur de boîtes aux lettres et le serveur de transport Edge et procède à la réplication initiale des données. Les données suivantes sont répliquées dans AD LDS :
    
      - données de topologie ;
    
      - données de configuration ;
    
      - données des destinataires ;
    
      - informations d’identification du compte ESRA.

  - Le service d’informations d’identification de Microsoft Exchange exécuté sur le serveur de transport Edge installe les informations d’identification du compte ESRA. Ces informations d’identification permettent d’authentifier et de sécuriser les connexions de synchronisation ultérieures.

  - La planification de la synchronisation EdgeSync est établie.

Le service Microsoft Exchange EdgeSync exécuté sur les serveurs de boîtes aux lettres dans le site Active Directory abonné effectue ensuite régulièrement une réplication monodirectionnelle des données à partir d’Active Directory vers AD LDS. Vous pouvez également utiliser la cmdlet **Start-EdgeSynchronization** pour ignorer la planification de la synchronisation EdgeSync et démarrer immédiatement la synchronisation.

Pour plus d’informations sur les comptes ESRA, ainsi que leur utilisation pour renforcer la sécurité du processus de synchronisation EdgeSync, consultez la rubrique [Informations d’identification d’abonnement Edge](edge-subscription-credentials-exchange-2013-help.md).

Cet exemple abonne un serveur de transport Edge au site spécifié et crée automatiquement le connecteur d’envoi Internet et le connecteur d’envoi du serveur de transport Edge aux serveurs de boîtes aux lettres créés.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 

> [!NOTE]
> Les valeurs par défaut des paramètres <em>CreateInternetSendConnector</em> et <em>CreateInboundSendConnector</em> sont définies sur <code>$true</code> pour les deux. Elles sont présentées ici uniquement à titre d’illustration.


Cet exemple exporte un fichier d’abonnement Edge.

    New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"

> [!NOTE]
> Lorsque la cmdlet <strong>New-EdgeSubscription</strong> est exécutée sur le serveur de transport Edge, vous êtes invité à confirmer les commandes qui seront désactivées et la configuration qui sera remplacée sur le serveur de transport Edge. Pour contourner cette confirmation, vous devez utiliser le paramètre <em>Force</em>. Ce paramètre est utile lorsque vous scriptez la cmdlet <strong>New-EdgeSubscription</strong>. Le paramètre <em>Force</em> permet également de remplacer un fichier existant portant le même nom que le fichier que vous créez lorsque vous réabonnez un serveur de transport Edge.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-EdgeSubscription](https://technet.microsoft.com/fr-fr/library/bb123800\(v=exchg.150\)).

## Connecteurs d’envoi créés au cours du processus d’abonnement Edge

Par défaut, lorsque vous exécutez le processus d’abonnement Edge recommandé en important le fichier d’abonnement Edge sur un serveur de boîtes aux lettres, les connecteurs d’envoi requis pour activer un flux de messagerie de bout en bout entre Internet et l’organisation Exchange sont créés automatiquement et les connecteurs d’envoi présents sur le serveur de transport Edge sont supprimés. Dans certains scénarios, vous pouvez choisir de supprimer la création automatique des connecteurs d’envoi et de les configurer manuellement. Pour plus d’informations sur la configuration manuelle des connecteurs d’envoi, consultez les rubriques [Configuration manuelle du flux de messagerie du serveur de transport Edge](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md) et [Configurer le flux de messagerie Internet via un serveur de transport Edge sans utiliser EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md).

Le processus d’abonnement Edge approvisionne les connecteurs d’envoi suivants :

  - Un connecteur d’envoi configuré pour relayer les messages électroniques de l’organisation Exchange vers Internet.

  - un connecteur d’envoi configuré pour relayer les messages électroniques du serveur de transport Edge vers l’organisation Exchange.

En outre, l’abonnement d’un serveur de transport Edge à l’organisation Exchange permet aux serveurs de boîtes aux lettres du site Active Directory abonné d’utiliser le connecteur d’envoi intra-organisationnel pour relayer les messages vers ce serveur de transport Edge.

## Création automatique d’un connecteur d’envoi entrant pour recevoir des messages d’Internet

Par défaut, lorsque vous exécutez la cmdlet **New-EdgeSubscription** sur le serveur de boîtes aux lettres, le paramètre de connecteur d’envoi entrant *CreateInboundSendConnector* est défini sur la valeur `$true`. Ainsi, le connecteur d’envoi requis pour envoyer des messages vers l’organisation Exchange est créé. Le tableau suivant explique la configuration de ce connecteur d’envoi.

### Configuration du connecteur d’envoi entrant automatique

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Entrant vers &lt;<em>Nom de site</em></p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>La valeur <code>--</code> dans l’espace d’adressage représente tous les domaines acceptés de relais interne et faisant autorité pour l’organisation Exchange. Chaque message reçu par le serveur de transport Edge pour ces domaines acceptés sont routés vers ce connecteur d’envoi et relayés vers les hôtes actifs.</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nom d’abonnement Edge</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>La valeur <code>--</code> dans la liste des hôtes actifs représente tous les serveurs de boîtes aux lettres dans le site Active Directory abonné. Les serveurs de boîtes aux lettres ajoutés au site Active Directory abonné après l’établissement de l’abonnement Edge ne sont pas inclus dans le processus de synchronisation EdgeSync. Toutefois, ils sont automatiquement ajoutés à la liste des hôtes actifs pour le connecteur d’envoi entrant créé automatiquement. Si plusieurs serveurs de boîtes aux lettres se trouvent dans le site Active Directory abonné, la charge liée aux connexions entrantes est équilibrée entre les hôtes actifs.</p></td>
</tr>
</tbody>
</table>


Vous ne pouvez pas modifier l’espace d’adressage ou la liste des hôtes actifs au moment de la création automatique du connecteur d’envoi entrant. Cependant, vous pouvez définir le paramètre *CreateInboundSendConnector* sur la valeur `$false` lors de la création d’un abonnement Edge. Ainsi, vous pouvez configurer manuellement un connecteur d’envoi à partir du serveur de transport Edge vers l’organisation Exchange.

## Création automatique d’un connecteur d’envoi sortant pour envoyer des messages vers Internet

Par défaut, lorsque vous exécutez la cmdlet **New-EdgeSubscription** sur le serveur de boîtes aux lettres, le paramètre du connecteur d’envoi sortant *CreateInternetSendConnector* est défini sur la valeur `$true`. Ainsi, le connecteur d’envoi requis pour envoyer des messages vers Internet est créé. Le tableau suivant montre la configuration par défaut de ce connecteur d’envoi.

### Configuration automatique du connecteur d’envoi vers Internet

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>Nom de site</em>&gt; vers Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nom d’abonnement Edge</em>&gt;</p>
> [!NOTE]
> Le nom de l’abonnement Edge est le même que le nom du serveur de transport Edge abonné.

</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Si plusieurs serveurs de transport Edge sont abonnés au même site Active Directory, aucun connecteur d’envoi vers Internet supplémentaire n’est créé. En revanche, tous les abonnements Edge sont ajoutés au même connecteur d’envoi que le serveur source. Cette charge de connexions sortantes vers Internet est équilibrée entre les serveurs de transport Edge abonnés.

Le connecteur d’envoi sortant est configuré pour envoyer des messages électroniques à partir de l’organisation Exchange vers tous les domaines SMTP distants, à l’aide du routage DNS pour résoudre les noms de domaine en enregistrements de ressource MX. Pour plus d’informations sur la configuration manuelle d’un connecteur, consultez l’article [Configuration manuelle du flux de messagerie du serveur de transport Edge](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md).

## Service Microsoft Exchange EdgeSync

Après avoir abonné un serveur de transport Edge à un site Active Directory, EdgeSync répliquera la configuration et les données des destinataires vers les serveurs de transport Edge. Le service réplique les données suivantes d’Active Directory vers AD LDS :

  - Configuration du connecteur d’envoi

  - Domaines acceptés

  - Domaines distants

  - Classifications des messages

  - Listes des expéditeurs approuvés

  - Listes des expéditeurs bloqués

  - Destinataires

  - Liste ses domaines d’envoi et de réception servant les communications de domaines sécurisés avec les partenaires

  - Liste des serveurs SMTP indiqués comme internes à la configuration de transport de votre organisation

  - Liste des serveurs de boîtes aux lettres dans le site Active Directory abonné

Pour plus d’informations sur les données répliquées dans AD LDS et leur utilisation, consultez la rubrique [Données de réplication EdgeSync](edgesync-replication-data-exchange-2013-help.md).

EdgeSync utilise un canal LDAP sécurisé mutuellement authentifié et autorisé pour transférer des données à partir du serveur de boîtes aux lettres sur le serveur de transport Edge.

Pour répliquer des données vers AD LDS, le serveur de boîtes aux lettres établit la liaison avec un serveur de catalogue global pour récupérer des données actualisées. EdgeSync démarre une session LDAP sécurisée entre un serveur de boîtes aux lettres et le serveur de transport Edge sur le port TCP non standard 50636.

Lorsque vous abonnez pour la première fois un serveur de transport Edge à un site Active Directory, la réplication initiale qui transmet les données d’Active Directory à AD LDS peut prendre du temps, en fonction de la quantité de données dans le service d’annuaire. Après la réplication initiale, EdgeSync synchronise uniquement les objets nouveaux et modifiés et supprime tous les objets supprimés.

## Planification de la synchronisation

Différents types de données sont synchronisés lors de différentes planifications. La planification de la synchronisation EdgeSync indique l’intervalle maximal entre les synchronisations EdgeSync. La synchronisation EdgeSync se produit aux intervalles suivants :

  - Données de configuration ; 3 minutes.

  - Données des destinataires ; 5 minutes.

  - Données de topologie : 5 minutes.

Pour modifier ces intervalles, utilisez la cmdlet **Set-EdgeSyncServiceConfig**. L’utilisation de la cmdlet **Start-EdgeSynchronization** sur le serveur de boîtes aux lettres pour forcer la synchronisation d’abonnement Edge remplace le minuteur pour la prochaine synchronisation EdgeSync planifiée et démarre immédiatement EdgeSync.

## Sélection des serveurs de boîtes aux lettres

Chaque serveur de transport Edge abonné est associé à un site Active Directory particulier. Si plusieurs serveurs de boîtes aux lettres existent dans le site, tous peuvent répliquer des données sur les serveurs de transport Edge abonnés. Pour éviter toute contention entre les serveurs de boîtes aux lettres lors de la synchronisation, le serveur de boîtes aux lettres privilégié est choisi selon les critères suivants :

1.  Le premier serveur de boîtes aux lettres dans Active Directory qui effectue une analyse de la topologie et découvre le nouvel abonnement Edge effectue la réplication initiale. Comme cette découverte est basée sur la durée de l’analyse de la topologie, n’importe quel serveur de boîtes aux lettres du site peut effectuer la réplication initiale.

2.  Le serveur de boîtes aux lettres qui effectue la réplication initiale établit une option de bail EdgeSync et définit un verrou pour l’abonnement Edge. L’option de bail établit ce serveur de boîtes aux lettres spécifique comme serveur privilégié pour la fourniture des services de synchronisation à ce serveur de transport Edge. Le verrou empêche qu’une instance du service EdgeSync exécutée sur un autre serveur de boîtes aux lettres reprenne l’option de bail.

3.  L’option de bail EdgeSync est activée pendant une heure. Au cours de cette heure, aucun autre service EdgeSync ne peut reprendre l’option, à moins qu’une synchronisation manuelle ne soit démarrée avant la fin de l’heure. Si le serveur de boîtes aux lettres privilégié n’est pas disponible pour fournir un service EdgeSync au démarrage de la synchronisation manuelle, après une période d’attente de cinq minutes, le verrou est libéré et un autre service EdgeSync peut reprendre l’option de bail et effectuer la synchronisation.

4.  À moins qu’une synchronisation manuelle ne soit effectuée, la synchronisation intervient sur la base de la planification de synchronisation EdgeSync. Si le serveur privilégié n’est pas disponible lors de la synchronisation planifiée, après une période d’attente de cinq minutes, le verrou est libéré et un autre service EdgeSync peut reprend l’option de bail et exécuter la synchronisation.

Cette méthode de verrouillage et de bail empêche que plusieurs instances du service EdgeSync envoient simultanément des données au même serveur de transport Edge.

> [!NOTE]
> Si des serveurs de boîtes aux lettres Exchange 2010 ou Exchange 2007 sont également présents dans le site Active Directory abonné, les serveurs de boîtes aux lettres Exchange 2013 seront toujours prioritaires et effectueront la réplication.


> [!NOTE]
> Lorsque vous abonnez un serveur de transport Edge à un site Active Directory, tous les serveurs de boîtes aux lettres installés dans ce site Active Directory à ce moment-là peuvent être inclus dans le processus de synchronisation EdgeSync. Si l’un de ces serveurs est supprimé, le service EdgeSync qui s’exécute sur les serveurs de boîtes aux lettres restants poursuit le processus de synchronisation des données. Toutefois, si vous installez ultérieurement de nouveaux serveurs de boîtes aux lettres dans le site Active Directory, ils ne seront pas automatiquement inclus à la synchronisation EdgeSync. Pour activer l’inclusion de ces nouveaux serveurs de boîtes aux lettres à la synchronisation EdgeSync, vous devez vous réabonner au serveur de transport Edge.


Le tableau suivant répertorie les propriétés EdgeSync liées au verrouillage et au bail. La cmdlet **Set-EdgeSyncServiceConfig** permet de configurer ces propriétés.

### Propriétés de bail EdgeSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code> (5 minutes)</p></td>
<td><p>Ce paramètre détermine la durée pendant laquelle un service EdgeSync particulier acquiert un verrou. Si le service EdgeSync sur le serveur de boîtes aux lettres détenteur du verrou ne répond pas, au bout de cinq minutes, le service EdgeSync sur un autre serveur de boîtes aux lettres reprendra le bail. Le fait de forcer une synchronisation EdgeSync immédiate ne modifie pas cette valeur.</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code> (1 heure)</p></td>
<td><p>Ce paramètre détermine la durée pendant laquelle un service EdgeSync peut déclarer une option de bail sur un serveur de transport Edge. Si le service EdgeSync qui détient le bail est indisponible et ne redémarre pas pendant cette période d’option, aucun autre service Exchange EdgeSync ne reprendra l’option de bail, sauf si vous forcez la synchronisation EdgeSync.</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code> (1 minute)</p></td>
<td><p>Ce paramètre détermine la fréquence à laquelle le champ de verrou est mis à jour quand un service EdgeSync a acquis un verrou sur un serveur de transport Edge.</p></td>
</tr>
</tbody>
</table>


## Préparation de l’exécution du service EdgeSync

Avant de pouvoir abonner votre serveur de transport Edge à votre organisation Exchange, vous devez vous assurer que votre infrastructure et que vos serveurs de boîtes aux lettres sont préparés pour le service EdgeSync. Pour préparer la synchronisation EdgeSync, procédez comme suit :

  - Vérifiez que le pare-feu du réseau de périmètre qui sépare le serveur de transport Edge de l’organisation Exchange est configuré pour permettre des communications via les ports appropriés. Le serveur de transport Edge utilise des ports LDAP non standard. Si votre environnement nécessite des ports spécifiques, vous pouvez modifier les ports utilisés par AD LDS à l’aide du script ConfigureAdam.ps1 fourni avec Exchange. Pour plus d’informations, consultez la rubrique [Modifier la configuration d’AD LDS](modify-ad-lds-configuration-exchange-2013-help.md). Modifiez les ports avant de créer l’abonnement Edge. Si vous modifiez les ports après avoir créé l’abonnement Edge, vous devrez supprimer l’abonnement Edge puis le recréer. Par défaut, les ports LDAP suivants sont utilisés pour accéder à AD LDS :
    
      - **LDAP**   Le port 50389/TCP est utilisé localement pour établir la liaison avec l’instance AD LDS. Ce port ne doit pas être ouvert sur le pare-feu du réseau de périmètre.
    
      - **LDAP sécurisé**   Le port 50636/TCP est utilisé pour la synchronisation d’annuaires depuis les serveurs de boîtes aux lettres vers AD LDS. Ce port doit être ouvert sur le pare-feu pour que la synchronisation EdgeSync réussisse.

  - Vérifiez que la résolution de nom d’hôte DNS du serveur de transport Edge vers les serveurs de boîtes aux lettres, et des serveurs de boîtes aux lettres vers le serveur de transport Edge a réussi.

  - Attribuez une licence au serveur de transport Edge. Les informations de licence pour le serveur de transport Edge sont enregistrées lors de la création de l’abonnement Edge. L’abonnement des serveurs de transport Edge à l’organisation Exchange doit se faire après l’application de la clé de licence sur le serveur de transport Edge. Si la clé de licence est appliquée au serveur de transport Edge après l’exécution du processus d’abonnement Edge, les informations de licence ne seront pas mises à jour dans l’organisation Exchange et vous devrez réabonner le serveur de transport Edge.

  - Configurez les paramètres de transport suivants pour la propagation vers le serveur de transport Edge :
    
      - **Serveurs SMTP internes**   Utilisez le paramètre *InternalSMTPServers* sur la cmdlet **Set-TransportConfig** pour indiquer la liste des plages d’adresses IP ou d’adresses IP de serveur SMTP interne que l’agent d’ID de l’expéditeur et l’agent de filtrage des connexions doivent ignorer sur le serveur de transport Edge.
    
      - **Domaines acceptés**   Configurez l’ensemble des domaines faisant autorité, des domaines de relais interne et des domaines de relais externes.
    
      - **Domaines distants**   Configurez les paramètres de domaine distant.

Retour au début

## Gestion des abonnements Edge

Pour obtenir des instructions détaillées sur les tâches de gestion d’abonnement Edge, consultez l’article [Gestion des abonnements Edge](manage-edge-subscriptions-exchange-2013-help.md).

