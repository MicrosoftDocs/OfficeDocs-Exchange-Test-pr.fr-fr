---
title: 'Configuration clonée de serveur de transport Edge: Exchange 2013 Help'
TOCTitle: Configuration clonée de serveur de transport Edge
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61180539
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration clonée de serveur de transport Edge

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les serveurs de transport Edge stockent leurs informations de configuration dans les services AD LDS. Vous pouvez installer plusieurs serveurs de transport Edge dans le réseau de périmètre et utiliser un tourniquet (round robin) DNS pour équilibrer le trafic réseau entre les serveurs de transport Edge. Le tourniquet est un mécanisme simple utilisé par les serveurs DNS pour partager et distribuer les charges pour les ressources réseau.

Pour vous assurer que tous les serveurs de transport Edge utilisent les mêmes informations de configuration, utilisez les scripts de configuration clonés pour dupliquer la configuration de votre serveur source sur un serveur cible.

La *configuration clonée* permet de déployer de nouveaux serveurs de transport Edge basés sur un serveur source configuré. Les informations de configuration du serveur source sont dupliquées, puis exportées vers un fichier XML. Le fichier XML est ensuite importé dans le serveur cible.

Cette rubrique fournit une vue d’ensemble du processus de configuration clonée. Pour obtenir la procédure détaillée sur la configuration des serveurs de transport Edge à l’aide de la configuration clonée, voir [Configurer un serveur de transport Edge à l’aide de la configuration clonée](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md).

**Contenu de cette rubrique**

Configuration clonée et EdgeSync

Processus de configuration clonée

Informations de configuration de transport

## Configuration clonée et EdgeSync

Exécutez le processus EdgeSync après avoir importé la configuration clonée. Pour effectuer des tâches de recherche de destinataire ou de sécurité des messages, le serveur de transport Edge requiert des données résidant dans Active Directory. *EdgeSync* est un ensemble de processus exécutés sur un serveur de boîtes aux lettres Exchange 2013 afin d’établir une réplication unidirectionnelle des informations du destinataire et de configuration à partir d’Active Directory vers l’instance AD LDS sur un serveur de transport Edge. EdgeSync ne copie que les informations dont le serveur de transport Edge a besoin pour exécuter des tâches de blocage du courrier indésirable et celles relatives à la configuration du connecteur requise pour activer un flux de messagerie de bout en bout. EdgeSync exécute des mises à jour planifiées de façon à ce que les informations disponibles dans AD LDS soient toujours à jour.

La configuration clonée ne duplique pas les paramètres d’abonnement Edge d’un serveur. Les certificats utilisés par EdgeSync ne sont pas clonés. Vous devez exécuter le processus EdgeSync séparément pour chaque serveur de transport Edge. EdgeSync remplace tous les paramètres inclus dans les informations de configuration clonées et dans les informations de réplication EdgeSync. Ces paramètres incluent les connecteurs d’envoi, les connecteurs de réception, les domaines acceptés et les domaines distants.

## Processus de configuration clonée

Le processus de configuration clonée se compose de trois étapes :

1.  Exportation de la configuration à partir du serveur source.
    
    Exécutez le script ExportEdgeConfig.ps1 (situé dans le dossier %ExchangeInstallPath%Scripts) pour exporter les informations de configuration du serveur source vers un fichier XML intermédiaire.

2.  Validation de la configuration du serveur cible.
    
    Exécutez le script ImportEdgeConfig.ps1 (situé dans le dossier %ExchangeInstallPath%Scripts). Ce script vérifie les informations existantes dans le fichier XML intermédiaire pour voir si les paramètres exportés sont valides pour le serveur cible, puis crée un fichier de réponses. Le fichier de réponses indique les informations propres au serveur utilisées lors de l’importation de la configuration sur le serveur cible. Le fichier de réponses contient des entrées pour chaque paramètre du serveur source non valide pour le serveur cible. Vous pouvez modifier ces paramètres de façon à ce qu’ils soient valides pour le serveur cible. Si tous les paramètres sont valides, le fichier de réponses ne contient pas d’entrées.

3.  Importation de la configuration sur le serveur cible.
    
    Le script ImportEdgeConfig.ps1 utilise le fichier XML intermédiaire et le fichier de réponses pour cloner la configuration existante ou pour restaurer une configuration spécifique du serveur.

## Étape 1 : Exportation de la configuration à partir du serveur source

Après avoir installé et configuré le rôle serveur de transport Edge, exécutez le script ExportEdgeConfig.ps1 (situé dans le dossier %ExchangeInsallPath%Scripts). Ce script extrait les informations de configuration du serveur source et les stocke dans un fichier XML intermédiaire.

Les informations suivantes sont exportées du serveur source et stockées dans le fichier XML intermédiaire :

  - Informations relatives au service de transport et informations sur les chemins des fichiers journaux :
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - Informations relatives à l’agent de transport, y compris l’état et les paramètres de priorité de chaque agent de transport.

  - Toutes les informations relatives au connecteur d’envoi. Si des connecteurs d’envoi sont configurés pour utiliser des informations d’identification, le mot de passe est écrit dans le fichier XML intermédiaire comme chaîne chiffrée. Vous pouvez utiliser le paramètre *-key* avec les scripts ImportEdgeConfig.ps1 et ExportEdgeConfig.ps1 pour spécifier la chaîne de 32 octets à utiliser pour le chiffrement et le déchiffrement du mot de passe. Si vous n’utilisez pas le paramètre *-key*, une clé de chiffrement par défaut est utilisée.

  - Informations relatives au connecteur de réception. Pour modifier la liaison réseau locale et les propriétés de port, vous devez modifier les informations de configuration dans le fichier de réponses créé à l’étape de validation de la configuration.

  - Configuration de domaine accepté.

  - Configuration de domaine distant.

  - Configuration des fonctionnalités de blocage du courrier indésirable :
    
      - Informations sur les listes d’adresses IP autorisées. Seules les entrées de liste d’adresses IP autorisées configurées manuellement par l’administrateur sont exportées.
    
      - Informations sur les listes d’adresses IP bloquées.
    
      - Configuration du filtre du contenu.
    
      - Configuration du filtre destinataire.
    
      - Entrées de réécriture d’adresses.
    
      - Entrées de filtrage des pièces jointes.

Retour au début

## Étape 2 : Validation de la configuration sur le serveur cible

Le serveur cible est un serveur Exchange 2013 disposant d’une nouvelle installation du rôle serveur de transport Edge. Pour commencer, exécutez le script ImportEdgeConfig.ps1 (situé dans le dossier %ExchangeInsallPath%Scripts) sur le serveur cible pour valider les informations existantes dans le fichier XML intermédiaire et pour créer le fichier de réponses. Le fichier de réponses indique les informations propres au serveur utilisées lors de l’importation de la configuration sur le serveur cible. Le fichier de réponses contient des entrées pour chaque paramètre du serveur source non valide pour le serveur cible. Vous devrez modifier ces paramètres de façon à ce qu’ils soient valides pour le serveur cible. Si tous les paramètres sont valides, le fichier de réponses ne contient pas d’entrées. Le fichier XML intermédiaire peut être utilisé pour différents serveurs cibles. Le fichier de réponses est spécifique à un serveur cible.

Le script ImportEdgeConfig.ps1 (situé dans le dossier %ExchangeInsallPath%Scripts) effectue les tâches suivantes :

  - Le script vérifie que les chemins de données et les chemins des journaux peuvent être créés sur le serveur cible. S’il n’est pas possible de créer les chemins, un chemin vide est inséré dans le fichier de réponses.

  - Pour chaque connecteur d’envoi dans le fichier XML, le script ajoute une entrée vide pour l’adresse IP source dans le fichier de réponses.

  - Pour chaque connecteur de réception dans le fichier XML, le script ajoute une entrée vide pour les liaisons réseau locales dans le fichier de réponses.

Vous devrez modifier manuellement le fichier de réponses pour fournir les informations suivantes sur les paramètres propres au serveur :

  - Complétez les chemins des données et les chemins des journaux. Si ces chemins sont vides dans le fichier de réponses, les chemins configurés dans le fichier XML intermédiaire seront utilisés à l’étape suivante lors de l’importation de la configuration sur le serveur cible.

  - Pour chaque entrée de connecteur d’envoi, complétez l’adresse IP source. Si ce champ est vide, une erreur surviendra à l’étape d’importation de la configuration.

  - Pour chaque entrée de connecteur de réception, spécifiez les liaisons réseau locales. Si les liaisons réseau locales sont vides, une erreur surviendra lors de la tentative d’importation de la configuration sur le serveur cible.

Retour au début

## Étape 3 : Importation de la configuration sur le serveur cible.

Vous pouvez exécuter cette étape sur tout serveur cible pour cloner la configuration d’un serveur de transport Edge existant ou pour restaurer une configuration spécifique du serveur. Exécutez le script ImportEdgeConfig.ps1 (situé dans le dossier %ExchangeInsallPath%Scripts) pour valider et importer la nouvelle configuration. Une fois le script exécuté, la configuration du serveur cible correspondra aux paramètres spécifiés dans le fichier XML intermédiaire et dans le fichier de réponses.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous recommandons de sauvegarder la configuration de serveur existante avant d’exécuter le processus d’importation de la configuration, pour qu’en cas d’échec de l’opération de clonage, vous puissiez rétablir l’état stable précédent du serveur.</td>
</tr>
</tbody>
</table>


Cette étape utilise les informations spécifiques du serveur contenues dans le fichier de réponses. Si un paramètre n’est pas spécifié dans le fichier de réponses, les données du fichier XML intermédiaire sont utilisées. Avant de modifier la configuration, le script valide les données dans le fichier XML intermédiaire et le fichier de réponses.

L’importation de la configuration modifie les paramètres de configuration de serveur cible suivants :

  - La configuration de l’agent de transport est modifiée.

  - Les connecteurs existants sur le serveur cible sont supprimés et les connecteurs présents dans le fichier XML intermédiaire sont ajoutés.

  - Les domaines acceptés existants sont supprimés et les entrées de domaine accepté dans le fichier XML intermédiaire sont ajoutées.

  - Les domaines distants existants sont supprimés et les entrées de domaine distant dans le fichier XML intermédiaire sont ajoutées.

  - Les listes d’adresses IP autorisées existantes sont supprimées et les entrées de liste d’adresses IP autorisées dans le fichier XML intermédiaire sont ajoutées.

  - Les listes d’adresses IP bloquées existantes sont supprimées et les entrées de liste d’adresses IP bloquées dans le fichier XML intermédiaire sont ajoutées.

  - La configuration de blocage du courrier indésirable suivante est répliquée sur le serveur cible :
    
      - Configuration du filtre du contenu
    
      - Configuration du filtre destinataire
    
      - Entrées de réécriture d’adresses
    
      - Entrées de filtrage des pièces jointes

Retour au début

## Informations de configuration de transport

Les paramètres de l’objet de configuration du transport définissent les paramètres de transport des messages électroniques au niveau du serveur pour un serveur de transport Edge. Après importation du fichier XML intermédiaire sur le serveur cible, tous les paramètres de l’objet de configuration de transport sont importés, sauf les suivants :

  - Noms généraux et création de dates à partir du fichier XML exporté

  - Envoyer des informations au connecteur

  - Recevoir des informations du connecteur

  - Entrées de filtrage des pièces jointes

  - Entrée d’attribut **MaxDumpsterSizePerStorageGroup**

Après que le processus d’importation est terminé, vous pouvez également configurer les paramètres en utilisant la cmdlet **Set-TransportConfig**. Pour plus d’informations, consultez la rubrique [Set-TransportConfig](https://technet.microsoft.com/fr-fr/library/bb124151\(v=exchg.150\)).

Les attributs présentés dans le tableau suivant sont associés à l’objet de configuration de transport et aux valeurs par défaut. Vous pouvez configurer cet objet sur les serveurs de boîtes aux lettres et de transport Edge. Cependant, de nombreux attributs s’appliquent uniquement au service de transport sur les serveurs de boîtes aux lettres Exchange 2013. La configuration de ces attributs sur un serveur de transport Edge n’aura aucun effet.

### Attributs de configuration de transport et valeurs par défaut

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Description</th>
<th>Valeur par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>Cet attribut indique si les catégories Microsoft Outlook doivent être supprimées lors de la conversion de contenu.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>Cet attribut spécifie les codes de notification d’état de remise permettant de copier le message de notification d’état de remise vers l’adresse de messagerie de l’administrateur. Les codes de notification d’état de remise sont entrés sous la forme <em>x.y.z</em> avec des virgules de séparation.</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>Cet attribut spécifie une liste d’adresses IP de serveur SMTP interne ou des plages d’adresses IP qui doivent être ignorées par l’ID de l’expéditeur et le filtrage des connexions.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>Cet attribut spécifie l’adresse de messagerie à laquelle les états de journal sont envoyés si la boîte aux lettres de journalisation est indisponible. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>Cet attribut spécifie la taille maximale de la benne de transport sur un serveur de boîtes aux lettres. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>18 Mo</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>Cet attribut spécifie le délai pendant lequel un message électronique doit rester dans la benne de transport sur un serveur de boîtes aux lettres. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>Cet attribut spécifie la taille maximale des messages que des destinataires de l’organisation peuvent recevoir. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>10 Mo</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>Cet attribut spécifie le nombre maximal de destinataires pouvant être inclus dans un seul message électronique. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>Cet attribut spécifie la taille maximale des messages que des expéditeurs de l’organisation peuvent envoyer. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>10 Mo</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>Cet attribut spécifie les domaines distants qui utiliseront l’authentification TLS (Transport Layer Security) via des connecteurs de réception configurés pour prendre en charge la sécurité de domaine. Plusieurs domaines peuvent être séparés par des virgules. Le caractère générique (*) n’est pas pris en charge dans les domaines répertoriés dans cet attribut.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>Cet attribut spécifie les domaines distants utilisant l’authentification Mutual TLS (Transport Layer Security) lorsqu’un message électronique est envoyé via un connecteur d’envoi configuré pour prendre en charge la sécurité de domaine et l’espace d’adressage du domaine cible. Plusieurs domaines peuvent être séparés par des virgules. Le caractère générique (*) n’est pas pris en charge dans les domaines répertoriés dans cet attribut.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>Cet attribut vérifie que les clients de messagerie électronique qui envoient des messages à partir de boîtes aux lettres sur des serveurs de boîtes aux lettres utilisent un envoi MAPI chiffré. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge. Les valeurs valides pour cet attribut sont <code>$true</code> ou <code>$false</code>.</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>Cet attribut spécifie si les messages vocaux de messagerie unifiée sont journalisés par l’Agent de journalisation. Cet attribut ne s’applique pas à la configuration d’un serveur de transport Edge.</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si le serveur de transport Edge est abonné ultérieurement à l’organisation Exchange, la valeur de l’attribut <strong>InternalSMTPServers</strong> est remplacée au cours du processus EdgeSync. Pour plus d’informations, voir <a href="edge-subscriptions-exchange-2013-help.md">Abonnements Edge</a>.</td>
</tr>
</tbody>
</table>


Retour au début

