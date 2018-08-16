---
title: 'Pare-feu d’en-tête: Exchange 2013 Help'
TOCTitle: Pare-feu d’en-tête
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52063007
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- pare-feu d'en-tête, en-têtes X de forêt
- pare-feu d'en-tête, en-têtes X d'organisation
- pare-feu d'en-tête, en-têtes X
- pare-feu d'en-tête, en-têtes de routage
- pare-feu d'en-tête, architecture de transport
- pare-feu d'en-tête, autorisations de pare-feu d'en-tête
ms.translationtype: HT
---

# Pare-feu d’en-tête

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Microsoft Exchange Server 2013, un *pare-feu d'en-tête* est un mécanisme qui supprime certains champs d'en-tête de messages entrants et sortants. Le pare-feu d'en-tête affecte deux types différents de champs d'en-tête :

  - **En-têtes X**   Un *en-tête X* est un champ d'en-tête non officiel défini par l'utilisateur. Les en-têtes X ne sont pas mentionnés spécifiquement dans RFC 2822, mais l'utilisation d'un champ d'en-tête non défini commençant par **X-** est devenue une manière reconnue d'ajouter des champs d'en-tête non officiels à un message. Des applications de messagerie, telles que des applications de blocage du courrier indésirable et des virus, et des serveurs de messagerie, peuvent ajouter leurs propres en-têtes X à un message. Dans Exchange, les champs d'en-tête X contiennent des détails concernant les actions exécutées sur le message par le service de transport, tels que le seuil de probabilité de courrier indésirable (SCL), les résultats du filtrage du contenu et l'état de traitement des règles. La divulgation de ces informations à des sources non autorisées peut constituer un risque pour la sécurité.

  - **En-têtes de routage**   Les en-têtes de routage sont des champs d'en-tête SMTP standard définis dans les normes RFC 2821 et RFC 2822. Ils marquent un message à l'aide d'informations sur les différents serveurs de messagerie utilisés pour remettre le message au destinataire. Des en-têtes de routage insérés dans des messages par des utilisateurs malveillants peuvent induire en erreur sur le chemin de routage qu'un message a parcouru pour atteindre un destinataire.

Le pare-feu d'en-tête empêche la falsification de ces en-têtes X en les supprimant des messages entrants provenant de sources non approuvées qui entrent dans l'organisation Exchange. Le pare-feu d'en-tête empêche la révélation de ces en-têtes X associés à Exchange en les supprimant des messages sortants envoyés à des destinations non approuvées hors de l'organisation Exchange. Le pare-feu d'en-tête empêche également la falsification des en-têtes de routage standard utilisés pour suivre l'historique de routage d'un message.

**Contenu de cette rubrique**

Champs d'en-tête de message affectés par le pare-feu d'en-tête dans Exchange

Mode d'application d'un pare-feu d'en-tête à des connecteurs de réception et d'envoi

Pare-feu d'en-tête pour les messages entrants sur des connecteurs de réception

Pare-feu d'en-tête pour les messages sortants sur des connecteurs d'envoi

Pare-feu d'en-tête pour d'autres sources de messages

En-têtes X d'organisation et de forêt dans Exchange

## Champs d'en-tête de message affectés par le pare-feu d'en-tête dans Exchange

Les types d'en-têtes X et d'en-têtes de routage affectés par le pare-feu d'en-tête sont les suivants :

  - **En-têtes X d'organisation**   Ces champs d'en-tête X commencent par **X-MS-Exchange-Organization-**.

  - **En-têtes X de forêt**   Ces champs d'en-tête X commencent par **X-MS-Exchange-Forest-**.
    
    Pour des exemples d'en-têtes X d'organisation et de forêt, consultez la section En-têtes X d'organisation et de forêt dans Exchange à la fin de cette rubrique.

  - **En-têtes de routage Received:**    Une instance différente de ce champ d'en-tête est ajoutée à l'en-tête de message par chaque serveur de messagerie ayant accepté et transmis le message au destinataire. L'en-tête **Received:**  inclut généralement le nom du serveur de messagerie et un horodateur.

  - **En-têtes de routage Resent-\*:**  Les champs d'en-tête Resent sont des champs informatifs qui permettent de déterminer si un message a été transféré par un utilisateur. Les champs d'en-tête Resent disponibles sont les suivants : **Resent-Date:** , **Resent-From:** , **Resent-Sender:** , **Resent-To:** , **Resent-Cc:** , **Resent-Bcc:**  et **Resent-Message-ID:** . Les champs **Resent-** sont utilisés de façon à ce que le message apparaisse au destinataire comme s'il était envoyé directement par l'expéditeur d'origine. Le destinataire peut afficher l'en-tête de message pour voir qui a transféré le message.

Pour appliquer un pare-feu d'en-tête aux en-têtes X d'organisation et de forêt, et aux en-têtes de routage existant dans des messages, Exchange utilise deux méthodes différentes :

  - Des autorisations sont attribuées aux connecteurs d'envoi ou de réception pouvant être utilisés pour conserver ou supprimer des types spécifiques d'en-têtes dans un message quand ce dernier transite par le connecteur.

  - Un pare-feu d'en-tête est automatiquement implémenté pour certains types d'en-têtes au cours d'autres types de dépôt de messages.

Retour au début

## Mode d'application d'un pare-feu d'en-tête à des connecteurs de réception et d'envoi

Un pare-feu d'en-tête est appliqué aux messages qui transitent par des connecteurs d'envoi et de réception en fonction d'autorisations spécifiques attribuées aux connecteurs.

Si l'autorisation est attribuée au connecteur de réception ou d'envoi, aucun pare-feu d'en-tête n'est appliqué aux messages transitant par le connecteur. Les champs d'en-tête affectés sont conservés dans les messages.

Si l'autorisation n'est pas attribuée au connecteur de réception ou d'envoi, un pare-feu d'en-tête est appliqué aux messages transitant par le connecteur. Les champs d'en-tête affectés sont supprimés des messages.

Le tableau suivant décrit les autorisations attribuées aux connecteurs d'envoi et de réception, qui sont utilisées pour appliquer un pare-feu d'en-tête, ainsi que les champs d'en-tête affectés.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de connecteur</th>
<th>Autorisation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Connecteur de réception</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête X d'organisation commençant par <strong>X-MS-Exchange-Organization-</strong> dans les messages entrants.</p></td>
</tr>
<tr class="even">
<td><p>Connecteur de réception</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête X de forêt commençant par <strong>X-MS-Exchange-Forest-</strong> dans les messages entrants.</p></td>
</tr>
<tr class="odd">
<td><p>Connecteur de réception</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête de routage <strong>Received:</strong> et <strong>Resent-*:</strong> dans les messages entrants.</p></td>
</tr>
<tr class="even">
<td><p>Connecteur d'envoi</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête X d'organisation commençant par <strong>X-MS-Exchange-Organization-</strong> dans les messages sortants.</p></td>
</tr>
<tr class="odd">
<td><p>Connecteur d'envoi</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête X de forêt commençant par <strong>X-MS-Exchange-Forest-</strong> dans les messages sortants.</p></td>
</tr>
<tr class="even">
<td><p>Connecteur d'envoi</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Cette autorisation affecte les champs d'en-tête de routage <strong>Received:</strong> et <strong>Resent-*:</strong> dans les messages sortants.</p></td>
</tr>
</tbody>
</table>


## Pare-feu d'en-tête pour les messages entrants sur des connecteurs de réception

Le tableau suivant décrit l'application par défaut des autorisations de pare-feu d'en-tête sur des connecteurs de réception.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorisation</th>
<th>Principaux de sécurité Exchange par défaut auxquels l'autorisation est attribuée</th>
<th>Groupe d'autorisations dont les principaux de sécurité sont membres</th>
<th>Type d'utilisation par défaut qui attribue les groupes d'autorisations au connecteur de réception</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> et <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Serveurs de transport Hub</p></li>
<li><p>Serveurs de transport Edge</p></li>
<li><p>Serveurs Exchange</p>

> [!NOTE]  
> Sur les serveurs de transport Hub uniquement

</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Compte d'utilisateur anonyme</p></td>
<td><p><strong>Anonyme</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Comptes d'utilisateur authentifiés</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (indisponible sur les serveurs de transport Edge)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Serveurs de transport Hub</p></li>
<li><p>Serveurs de transport Edge</p></li>
<li><p>Serveurs Exchange</p>

> [!NOTE]  
> Serveurs de transport Hub uniquement

</li>
<li><p>Serveurs sécurisés de l'extérieur</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Compte de serveur partenaire</p></td>
<td><p><strong>Partenaire</strong></p></td>
<td><p><code>Internet</code> et <code>Partner</code></p></td>
</tr>
</tbody>
</table>


Retour au début

## Pare-feu d'en-tête sur des connecteurs de réception personnalisés

Pour appliquer un pare-feu d'en-tête à des messages dans un scénario de connecteur de réception personnalisé, utilisez l'une des méthodes suivantes :

  - Créez le connecteur de réception avec un type d'utilisation qui applique automatiquement le pare-feu d'en-tête aux messages. Notez que vous pouvez définir le type d'utilisation uniquement lorsque vous créez le connecteur de réception.
    
      - Pour supprimer les en-têtes X d'organisation ou de forêt des messages, créez un connecteur de réception, puis sélectionnez un type d'utilisation autre que `Internal`.
    
      - Pour supprimer les en-têtes de routage des messages, effectuez l'une des opérations suivantes :
        
          - Créez un connecteur de réception, puis sélectionnez le type d'utilisation `Custom`. N'attribuez pas de groupes d'autorisations au connecteur de réception.
        
          - Modifiez un connecteur de réception existant, puis définissez le paramètre *PermissionGroups* sur la valeur `None`.
        
        Notez que si vous avez un connecteur de réception auquel aucun groupe d'autorisations n'est attribué, vous devez ajouter des principaux de sécurité au connecteur de réception en procédant de la manière décrite à la dernière étape.

  - La cmdlet **Remove-ADPermission** permet de supprimer les autorisations **Ms-Exch-Accept-Headers-Organization**, **Ms-Exch-Accept-Headers-Forest** et **Ms-Exch-Accept-Headers-Routing** d'un principal de sécurité configuré sur le connecteur de réception. Cette méthode ne fonctionne pas si l'autorisation a été attribuée au principal de sécurité à l'aide d'un groupe d'autorisations sur le connecteur de réception, car vous ne pouvez pas modifier les attributions d'autorisations ou l'appartenance à un groupe d'autorisations.

  - La cmdlet **Add-ADPermission** permet d'ajouter les principaux de sécurité requis pour le flux de messagerie sur le connecteur de réception. Assurez-vous qu'aucune des autorisations **Ms-Exch-Accept-Headers-Organization**, **Ms-Exch-Accept-Headers-Forest** et **Ms-Exch-Accept-Headers-Routing** ne sont attribuées aux principaux de sécurité. Si nécessaire, utilisez la cmdlet **Add-ADPermission** pour refuser les autorisations **Ms-Exch-Accept-Headers-Organization**, **Ms-Exch-Accept-Headers-Forest** et **Ms-Exch-Accept-Headers-Routing** aux principaux de sécurité configurés sur le connecteur de réception.

Pour plus d'informations, consultez les rubriques suivantes :

  - [Connecteurs de réception](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/fr-fr/library/aa996048\(v=exchg.150\))

Retour au début

## Pare-feu d'en-tête pour les messages sortants sur des connecteurs d'envoi

Le tableau suivant décrit l'application par défaut des autorisations de pare-feu d'en-tête sur des connecteurs d'envoi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorisation</th>
<th>Principaux de sécurité Exchange par défaut auxquels l'autorisation est attribuée</th>
<th>Type d'utilisation par défaut qui attribue les principaux de sécurité au connecteur d'envoi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> et <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Serveurs de transport Hub</p></li>
<li><p>Serveurs de transport Edge</p></li>
<li><p>Serveurs Exchange</p>

> [!NOTE]  
> Sur les serveurs de transport Hub uniquement

</li>
<li><p>Serveurs sécurisés de l'extérieur</p></li>
<li><p>Groupe universel de sécurité <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Serveurs de transport Hub</p></li>
<li><p>Serveurs de transport Edge</p></li>
<li><p>Serveurs Exchange</p>

> [!NOTE]  
> Sur les serveurs de transport Hub uniquement

</li>
<li><p>Serveurs sécurisés de l'extérieur</p></li>
<li><p>Groupe universel de sécurité <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Compte d'utilisateur anonyme</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Serveurs partenaires</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


Retour au début

## Pare-feu d'en-tête sur des connecteurs d'envoi personnalisés

Pour appliquer un pare-feu d'en-tête à des messages dans un scénario de connecteur d'envoi personnalisé, utilisez l'une des méthodes suivantes :

  - Créez le connecteur d'envoi avec un type d'utilisation qui applique automatiquement le pare-feu d'en-tête aux messages. Notez que vous pouvez définir le type d'utilisation uniquement lorsque vous créez le connecteur d'envoi.
    
      - Pour supprimer les en-têtes X d'organisation ou de forêt des messages, créez un connecteur d'envoi, puis sélectionnez un type d'utilisation autre que `Internal` ou `Partner`.
    
      - Pour supprimer les en-têtes de routage des messages, créez un connecteur d'envoi, puis sélectionnez le type d'utilisation `Custom`. L'autorisation **Ms-Exch-Send-Headers-Routing** est attribuée à tous les types d'utilisations du connecteur d'envoi, à l'exception de `Custom`.

  - Supprimez du connecteur un principal de sécurité attribuant les autorisations **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** et **Ms-Exch-Send-Headers-Routing**.

  - La cmdlet **Remove-ADPermission** permet de supprimer les autorisations **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** et **Ms-Exch-Send-Headers-Routing** d'un principal de sécurité configuré sur le connecteur d'envoi.

  - La cmdlet **Add-ADPermission** permet de refuser les autorisations **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** et **Ms-Exch-Send-Headers-Routing** à un principal de sécurité configuré sur le connecteur d'envoi.

Pour plus d'informations, consultez les rubriques suivantes :

  - [Connecteurs d'envoi](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/fr-fr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/fr-fr/library/aa996048\(v=exchg.150\))

Retour au début

## Pare-feu d'en-tête pour d'autres sources de messages

Les messages peuvent entrer dans le pipeline de transport sur un serveur de boîtes aux lettres ou un serveur de transport Edge sans utiliser de connecteurs d'envoi ou de réception. Le pare-feu d'en-tête est appliqué à ces autres sources de messages de la manière décrite dans la liste suivante :

  - **Répertoire de collecte et répertoire de relecture**   Le répertoire de collecte est utilisé par les administrateurs ou les applications pour déposer des fichiers de messages. Le répertoire de relecture permet de déposer à nouveau des messages exportés à partir des files d'attente des messages Exchange. Pour plus d'informations sur les répertoires de collecte et de relecture, consultez la rubrique [Répertoire de collecte et répertoire de relecture](pickup-directory-and-replay-directory-exchange-2013-help.md).
    
    Les en-têtes X d'organisation et de forêt, ainsi que les en-têtes de routage sont supprimés des fichiers de messages dans le répertoire de collecte.
    
    Les en-têtes de routage sont conservés dans les messages déposés par le répertoire de relecture.
    
    La conservation ou non des en-têtes X d'organisation et de forêt des messages dans les répertoire de relecture est contrôlée par le champ d'en-tête **X-CreatedBy:**  dans les fichier de messages :
    
      - Si la valeur de **X-CreatedBy:**  est `MSExchange15`, les en-têtes X d'organisation et de forêt sont conservés dans les messages.
    
      - Si la valeur de **X-CreatedBy:**  n'est pas `MSExchange15`, les en-têtes X d'organisation et de forêt sont supprimés des messages.
    
      - Si le champ d'en-tête **X-CreatedBy:**  n'existe pas dans les fichiers de messages, les en-têtes X d'organisation et de forêt sont supprimés des messages.

  - **Répertoire de dépôt**   Le répertoire de dépôt est utilisé par les connecteurs étrangers sur les serveurs de boîtes aux lettres pour envoyer des messages à des serveurs de messagerie qui n'utilisent pas le protocole SMTP pour transférer les messages. Pour plus d'informations sur les connecteurs étrangers, consultez la rubrique [Connecteurs étrangers](foreign-connectors-exchange-2013-help.md).
    
    Les en-têtes X d'organisation et de forêt sont supprimés des fichiers de messages avant leur placement dans le répertoire de dépôt.
    
    Les en-têtes de routage sont conservés dans les messages déposés par le répertoire de dépôt.

  - **Transport de boîtes aux lettres**   Le service de transport de boîtes aux lettres existant sur les serveurs de boîtes aux lettres permet l'échange de messages entre boîtes aux lettres sur ces serveurs. Pour plus d'informations sur le service de transport de boîtes aux lettres, consultez la rubrique [Flux de messagerie](mail-flow-exchange-2013-help.md).
    
    Les en-têtes X d'organisation et de forêt, ainsi que les en-têtes de routage sont supprimés des messages sortants expédiés à partir de boîtes aux lettres par le service de dépôt du transport de boîtes aux lettres.
    
    Les en-têtes de routage sont conservés pour les messages entrants adressés à des destinataires de boîte aux lettres par le service de remise de transport de boîtes aux lettres. Les en-têtes X d'organisation suivantes sont conservés pour les messages entrants adressés à des destinataires de boîte aux lettres par le service de remise de transport de boîtes aux lettres.
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **Messages de notification d'état de remise (DSN)**   Les en-têtes X d'organisation et de forêt, ainsi que les en-têtes de routage sont supprimés du message d'origine ou de l'en-tête de message d'origine joint au message DSN. Pour plus d'informations sur les messages de notification d'état de remise, consultez la rubrique [Notifications d’état de remise et notifications d’échec de remise dans Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Dépôt par l'agent de transport**   Les en-têtes X d'organisation et de forêt, ainsi que les en-têtes de routage sont conservés dans les messages déposés par des agents transport.

Retour au début

## En-têtes X d'organisation et de forêt dans Exchange

Le service de transport sur des serveurs de boîtes aux lettres ou des serveurs de transport Edge insère des champs d'en-tête X personnalisés dans les en-têtes de messages.

Les en-têtes X d'organisation commencent par **X-MS-Exchange-Organization-**. Les en-têtes X de forêt commencent par **X-MS-Exchange-Forest-**. Le tableau suivant décrit certains en-têtes X d'organisation et de forêt utilisés dans les messages au sein d'une organisation Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>En-tête X</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>Règles de transport appliquées au message.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>Résumé des résultats du filtrage du courrier indésirable appliqués au message par l'Agent de filtrage du contenu.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>Spécifie la source d'authentification. Cet en-tête X est toujours présent lorsque la sécurité d'un message a été évaluée. Les valeurs possibles sont <code>Anonymous</code>, <code>Internal</code>, <code>External</code> ou <code>Partner</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>Renseigné durant l'authentification sécurisée de domaine. La valeur est le nom de domaine complet (FQDN) du domaine authentifié distant.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>Spécifie le mécanisme d'authentification utilisé pour le dépôt du message. La valeur est un nombre hexadécimal à deux chiffres.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>Spécifie le nom de domaine complet (FQDN) du serveur qui a évalué l'authentification du message pour le compte de l'organisation.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>Identifie les états de journal dans le transport. Dès que le message quitte le service de transport, l'en-tête devient <strong>X-MS-Journal-Report</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>Identifie l'heure à laquelle le message est entré pour la première fois dans l'organisation Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>Identifie l'expéditeur d'origine d'un message mis en quarantaine lorsqu'il est entré pour la première fois dans l'organisation Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>Identifie la taille d'origine d'un message mis en quarantaine lorsqu'il est entré pour la première fois dans l'organisation Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>Identifie le seuil de probabilité de courrier indésirable (SCL) d'origine d'un message mis en quarantaine lorsqu'il est entré pour la première fois dans l'organisation Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>Identifie le seuil de probabilité de courrier d'hameçonnage. La plage des valeurs de seuil de probabilité de courrier d'hameçonnage possibles s'étend de 1 à 8. Une valeur élevée indique un message suspect. Pour plus d'informations, consultez la rubrique <a href="anti-spam-stamps-exchange-2013-help.md">Marquages de courrier indésirable</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>Indique que le message a été mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable et qu'une notification d'état de remise (DSN) a été envoyée. Cela peut également indiquer que le message a été mis en quarantaine, puis libéré par l'administrateur. Ce champ d'en-tête X empêche le nouveau dépôt du message libéré dans la boîte aux lettres de mise en quarantaine du courrier indésirable. Pour plus d'informations, consultez la rubrique <a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>Identifie le seuil de probabilité de courrier indésirable (SCL) du message. La plage des valeurs de SCL possibles s'étend de 0 à 9. Une valeur élevée indique un message suspect. La valeur spéciale -1 exempte le message de tout traitement par l'Agent de filtrage du contenu. Pour plus d'informations, consultez la rubrique <a href="content-filtering-exchange-2013-help.md">Filtrage du contenu</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>Contient les résultats de l'Agent d'ID de l'expéditeur. L'Agent d'ID de l'expéditeur utilise le SPF (Sender Policy Framework) pour comparer l'adresse IP source du message au domaine utilisé dans l'adresse de messagerie de l'expéditeur. Les résultats de l'ID de l'expéditeur permettent de calculer le SCL d'un message. Pour plus d'informations, consultez la rubrique <a href="sender-id-exchange-2013-help.md">ID de l'expéditeur</a>.</p></td>
</tr>
</tbody>
</table>


Retour au début

