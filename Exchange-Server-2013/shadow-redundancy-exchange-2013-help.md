---
title: 'Redondance des clichés instantanés: Exchange 2013 Help'
TOCTitle: Redondance des clichés instantanés
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50478941
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Redondance des clichés instantanés

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La redondance des clichés instantanés a été introduite dans Microsoft Exchange Server 2010 pour fournir des copies redondantes des messages avant leur remise à des boîtes aux lettres. Dans Exchange 2010, la redondance des clichés instantanés retardait la suppression d'un message de la base de données de transport sur un serveur de transport jusqu'à ce que le serveur vérifie le saut suivant dans la remise achevée du chemin de remise du message. Si le saut suivant échouait avant de signaler la réussite de la remise au serveur de transport, ce dernier soumettait de nouveau le message à ce saut suivant. Les serveurs Exchange 2010 utilisaient XSHADOW pour annoncer leur prise en charge de la redondance des clichés instantanés. Si un serveur SMTP ne prenait pas en charge la redondance des clichés instantanés, Exchange 2010 utilisait un accusé de réception retardé basé sur un intervalle de temps configuré sur le connecteur de réception pour faire une copie redondante du message.

L'amélioration majeure apportée à la redondance des clichés instantanés dans Microsoft Exchange Server 2013 est que le serveur de transport effectue maintenant une copie redondante de tous les messages qu'il reçoit avant d'en accuser réception au serveur d'envoi. La prise en charge ou la non-prise en charge par le serveur d'envoi de la redondance des clichés instantanés n'a pas d'importance. Cela permet de s'assurer que tous les messages figurant dans le pipeline de transport Exchange 2013 sont rendus redondants quand il sont en transit. Si Exchange 2013 détermine que le message d'origine a été perdu en transit, la copie redondante du message est remise.

**Contenu de cette rubrique**

Composants de la redondance des clichés instantanés

Exigences relatives à la redondance des clichés instantanés

La redondance des clichés instantanés est activée par défaut

Création des clichés instantanés

Délais d'expiration SMTP

Maintenance des messages instantanés

Traitement des messages après une panne

## Composants de la redondance des clichés instantanés

Le tableau suivant décrit les composants de la redondance des clichés instantanés. Les termes suivants sont utilisés dans cette rubrique.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Terme</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serveur de transport</p></td>
<td><p>Serveur Exchange qui contient des files d'attente de messages et qui est responsable du routage des messages. Dans Exchange 2013, un serveur de transport est un serveur de boîtes aux lettres (service de transport sur ​​le serveur de boîtes aux lettres).</p></td>
</tr>
<tr class="even">
<td><p>Base de données de transport</p></td>
<td><p>Base de données de file d'attente de message sur un serveur de transport Exchange 2013. Les files d'attente de secours et Safety Net sont également stockés dans la base de données de transport.</p></td>
</tr>
<tr class="odd">
<td><p>Limite de la haute disponibilité du transport</p></td>
<td><p>Groupe de disponibilité de base de données (DAG) dans des environnements DAG ou site Active Directory dans les environnements non-DAG. Quand un message arrive sur un serveur de transport dans la limite de haute disponibilité du transport, Exchange tente de maintenir 2 copies redondantes du message sur les serveurs de transport à l'intérieur de la limite. Quand un message sort de la limite de haute disponibilité du transport, Exchange cesse de maintenir des copies redondantes du message.</p></td>
</tr>
<tr class="even">
<td><p>Message principal</p></td>
<td><p>Message déposé dans le pipeline de transport pour remise.</p></td>
</tr>
<tr class="odd">
<td><p>Message de cliché instantané</p></td>
<td><p>Copie redondante du message que le serveur de secours conserve jusqu'à la confirmation que le message principal a été traité avec succès par le serveur principal.</p></td>
</tr>
<tr class="even">
<td><p>Serveur principal</p></td>
<td><p>Serveur de transport occupé à traiter le message principal.</p></td>
</tr>
<tr class="odd">
<td><p>Serveur de clichés instantanés</p></td>
<td><p>Serveur de transport conservant les clichés instantanés pour le serveur principal. Un serveur de transport peut être en même temps le serveur principal pour certains messages et le serveur de secours pour d'autres.</p></td>
</tr>
<tr class="even">
<td><p>File d'attente de clichés instantanés</p></td>
<td><p>File d'attente de remise dans laquelle le serveur de secours stocke les messages instantanés. Pour les messages à plusieurs destinataires, chaque saut suivant pour le message principal nécessite des files d'attente de secours séparées.</p></td>
</tr>
<tr class="odd">
<td><p>État de suppression</p></td>
<td><p>Informations qu'un serveur de transport conserve pour des messages instantanés qui indiquent que le message principal a été traité avec succès.</p></td>
</tr>
<tr class="even">
<td><p>Notification de suppression</p></td>
<td><p>Réponse qu'un serveur de clichés instantanés reçoit d'un serveur principal, indiquant qu'un message peut être supprimé.</p></td>
</tr>
<tr class="odd">
<td><p>Safety Net</p></td>
<td><p>Version améliorée Exchange 2013 de la benne de transport. Les messages traités avec succès ou remis à la boîte aux lettres d'un destinataire par le service de transport sur ​​un serveur de boîtes aux lettres sont déplacés dans Safety Net. Pour plus d'informations, consultez la rubrique <a href="safety-net-exchange-2013-help.md">Safety Net</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gestionnaire de redondance des clichés instantanés</p></td>
<td><p>Composant de transport qui gère la redondance des clichés instantanés.</p></td>
</tr>
<tr class="odd">
<td><p>Pulsation</p></td>
<td><p>Processus qui permet aux serveurs principaux et aux serveurs de secours de vérifier mutuellement leur disponibilité.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Exigences relatives à la redondance des clichés instantanés

Bien que cela puisse sembler évident, la redondance des clichés instantanés nécessite plusieurs serveurs de boîtes aux lettres Exchange 2013. Le serveur de boîtes aux lettres peut être constitué de serveurs autonomes ou de serveurs de boîtes aux lettres et d'accès client installés sur le même ordinateur.

  - Si le serveur de boîtes aux lettres n'est pas membre d'un DAG, les autres serveurs de boîtes aux lettres doivent se trouver dans le site Active Directory local.

  - Si le serveur de boîtes aux lettres est membre d'un DAG, les autres serveurs de boîtes aux lettres doivent appartenir au même DAG. Les autres serveurs de boîtes aux lettres appartenant au DAG peuvent se trouver dans le site Active Directory local ou dans un site Active Directory distant. Si le DAG s'étend sur plusieurs sites Active Directory, la redondance des clichés instantanés préfère créer une copie redondante du message dans un site Active Directory distant pour la résilience du site.

Les situations dans lesquelles la redondance des clichés instantanés ne peut pas protéger les messages en transit sont les suivantes :

  - Dans des environnements de serveur Exchange unique.

  - Dans des DAG sous-mis en service.

  - En cas de panne simultanée d'au moins deux serveurs de transport impliqués dans la redondance des clichés instantanés d'un message.

Retour au début

## La redondance des clichés instantanés est activée par défaut

Par défaut, la redondance des clichés instantanés est activée globalement dans le service de transport sur ​​tous les serveurs de boîtes aux lettres en utilisant le paramètre *ShadowRedundancyEnabled* avec la cmdlet **Set-TransportConfig**. Par défaut, si le service de transport sur ​​un serveur de boîtes aux lettres ne peut pas créer une copie redondante d'un message, ce dernier n'est pas rejeté. Toutefois, vous pouvez configurer Exchange 2013 pour qu'il rejette un message si une copie redondante de ce dernier n'a pas été créée en utilisant paramètre *RejectMessageOnShadowFailure* avec la cmdlet **Set-TransportConfig**. Le message est rejeté après un échec passager, mais le serveur d'envoi peut transmettre le message à nouveau. Le code de réponse SMTP est `451 4.4.0 Message failed to be made redundant.` Vous devez configurer Exchange 2013 pour qu'il rejette les messages qui ne peuvent pas être rendus redondants uniquement lorsque votre organisation compte plusieurs serveurs de boîtes aux lettres Exchange 2013 disponibles.

Le tableau suivant décrit les paramètres qui activent la redondance des clichés instantanés.

### Paramètres qui activent la redondance des clichés instantanés

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
<td><p><em>ShadowRedundancyEnabled</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> permet la redondance des clichés instantanés sur tous les serveurs de transport dans l'organisation.</p></li>
<li><p><code>$false</code>désactive la redondance des clichés instantanés sur tous les serveurs de transport dans l'organisation.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RejectMessageOnShadowFailure</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   Quand un cliché instantané du message ne peut pas être créé, le message principal est accepté de toute façon par les serveurs de transport au sein de l'organisation. Les messages qui ne sont pas persistants de façon redondante quand ils sont en transit.</p></li>
<li><p><code>$true</code>   Aucun message n'est accepté ou ne fait l'objet d'un accusé de réception par un serveur de transport au sein de l'organisation tant qu'un cliché instantané du message n'a pas été créé avec succès. Si un cliché instantané du message ne peut pas être créé, le message principal est rejeté avec une erreur passagère. Tous les messages dans l'organisation sont persistants de façon redondante quand ils sont en transit.</p>
<p>Vous devez définir cette valeur sur <code>$true</code> uniquement si vous disposez de plusieurs serveurs de boîtes aux lettres Exchange 2013 dans un DAG ou un site Active Directory où un cliché instantané du message peut être créé.</p></li>
</ul>
<p>Ce paramètre est significatif uniquement quand la valeur de <em>ShadowRedundancyEnabled</em> est <code>$true</code>.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Création des clichés instantanés

L'objectif principal de redondance des clichés instantanés est de toujours avoir deux copies d'un message dans une limite de haute disponibilité du transport quand le message est en transit. L'emplacement et le moment où la copie redondante du message est créée dépendent de l'origine et de la destination du message. Il existe trois principaux facteurs déterminants :

  - Messages reçus de l'extérieur d'une limite de haute disponibilité du transport.

  - Messages envoyés à l'extérieur d'une limite de haute disponibilité du transport.

  - Messages reçus du service de dépôt de transport de boîte aux lettres d'un serveur de boîtes dans la limite de haute disponibilité du transport.

Une *limite de haute disponibilité du transport* peut être ce qui suit :

  - Un DAG, pour les serveurs de boîtes aux lettres qui sont membres d'un DAG. Il peut s'agir d'un DAG s'étendant sur plusieurs sites Active Directory.

  - Un site Active Directory pour les serveurs de boîtes aux lettres qui n'appartiennent pas à un DAG.

La redondance des clichés instantanés n'effectue jamais le suivi des messages instantanés à travers une limite de haute disponibilité du transport. Lorsqu'un message franchit la limite de haute disponibilité du transport, la redondance des clichés instantanés commence ou redémarre. Cela réduit le trafic de maintenance des messages instantanés et empêche un nouveau dépôt des messages instantanés à travers la limite de haute disponibilité du transport. Exchange 2010 Les serveurs de transport Hub constituent un cas particulier abordé plus loin dans cette rubrique.

## Messages reçus en provenance de l'extérieur d'une limite de haute disponibilité du transport

Lorsque le service de transport sur ​​un serveur de boîtes aux lettres Exchange 2013 reçoit un message en provenance de l'extérieur de la limite de haute disponibilité du transport, le serveur de boîtes aux lettres ne se préoccupe pas de la prise en charge ou non de la redondance des clichés instantanés par le serveur d'envoi. Tant que la redondance des clichés instantanés est activée, le serveur de boîtes aux lettres qui reçoit le message crée une copie redondante de ce dernier sur un autre serveur de boîtes aux lettres dans la limite de haute disponibilité du transport avant d'accuser réception du message au serveur d'envoi. Voici un exemple de la manière dont fonctionne le processus :

![Création de messages de cliché instantané](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "Création de messages de cliché instantané")

1.  Un serveur SMTP transmet un message au service de transport sur ​​un serveur de boîtes aux lettres. Le serveur de boîtes aux lettres est le serveur principal, et le message est le message principal.

2.  Alors que la session SMTP d'origine avec le serveur SMTP est toujours active, le service de transport sur ​​le serveur principal ouvre une nouvelle session SMTP simultanée avec le service de transport sur ​​un autre serveur de boîtes aux lettres au sein de l'organisation pour créer une copie redondante du message.
    
      - Si le serveur primaire est membre d'un DAG, le serveur principal se connecte à un autre serveur de boîtes aux lettres dans la même DAG. Si le DAG s'étend sur plusieurs sites Active Directory, un serveur de boîtes aux lettres dans un autre site Active Directory est préféré par défaut. Ce comportement est contrôlé par le paramètre *ShadowMessagePreference* de la cmdlet **Set-TransportService**. La valeur par défaut est `PreferRemote`, mais vous pouvez la remplacer par `RemoteOnly` ou `LocalOnly`.
    
      - Si le serveur principal n'est pas membre d'un DAG, il se connecte à un autre serveur de boîtes aux lettres dans le même site Active Directory, quelle que soit la valeur du paramètre *ShadowMessagePreference*.

3.  Le serveur principal transmet une copie du message au service de transport sur un autre serveur de boîtes aux lettres dont le service de transport confirme que la copie du message a bien été créée. La copie du message est le cliché instantané et le serveur de boîtes aux lettres qui le conserver est le serveur de secours pour le serveur principal. Le message existe dans une file d'attente de clichés instantanés sur le serveur de secours.

4.  Après avoir reçu l'accusé de réception du serveur de secours, le serveur principal accuse à son tour réception du message principal au serveur SMTP d'origine dans la session SMTP d'origine, puis la session SMTP est fermée.

## Messages envoyés à l'extérieur d'une limite de haute disponibilité du transport

Quand un serveur de transport Exchange 2013 transmet un message à l'extérieur de la limite de haute disponibilité du transport et que le serveur SMTP de l'autre côté accuse réception du message, le serveur de transport déplace le message vers Safety Net. Aucun nouveau dépôt du message à partir de Safety Net ne peut se produire après que le message principal a été transmis avec succès à travers la limite de haute disponibilité du transport. Pour plus d'informations sur Safety Net, consultez la rubrique [Safety Net](safety-net-exchange-2013-help.md).

## Messages transmis à l'intérieur d'une limite de haute disponibilité du transport

Le routage des messages étant optimisé dans Exchange 2013, lorsque la destination finale est dans un DAG ou un site Active Directory, plusieurs sauts dans le service de transport sur ​​des serveurs de boîtes aux lettres de ce DAG ou de ce site Active Directory ne sont généralement pas nécessaires. Une fois le message accepté par le service de transport sur ​​un serveur de boîtes aux lettres dans le DAG ou le site Active Directory où se trouve la destination finale du message, le saut suivant pour le message est généralement la destination finale elle-même. L'objectif de la redondance des clichés instantanés qui est de conserver deux copies d'un message en transit est atteint quand un cliché instantané du message existe quelque part dans le DAG ou le site Active Directory. En règle générale, seuls des scénarios de basculement dans un DAG qui nécessitent la cmdlet **Redirect-Message** pour drainer les files d'attentes actives sur un serveur de boîtes aux lettres nécessitent plusieurs sauts à l'intérieur de la même limite de haute disponibilité du transport.

## Redondance des clichés avec serveurs de transport Hub Exchange 2010 dans le même site Active Directory

Quand un serveur de transport Hub Exchange 2010 transmet un message à un serveur de boîtes aux lettres Exchange 2013 situé dans le même site Active Directory, le serveur de transport Hub Exchange 2010 annonce la prise en charge de la redondance des clichés instantanés à l'aide de la commande XSHADOW, mais le serveur de boîtes aux lettres n'annonce pas cette prise en charge. Cela empêche le serveur de transport Hub Exchange 2010 de créer un cliché instantané du message sur un serveur de boîtes aux lettres Exchange 2013.

Lorsque le service de transport sur ​​un serveur de boîtes aux lettres Exchange 2013 transmet un message à un serveur de transport Hub Exchange 2010 situé dans le même site Active Directory, le serveur de boîtes aux lettres Exchange 2013 crée un cliché du message pour le serveur de transport Hub Exchange 2010. Lorsque le serveur de boîtes aux lettres Exchange 2013 reçoit un accusé de réception du serveur de transport Hub Exchange 2010, le serveur de boîtes aux lettres Exchange 2013 déplace le message traité avec succès vers Safety Net. Toutefois, les messages traités avec succès stockés dans Safety Net par le serveur de boîtes aux lettres Exchange 2013 ne sont jamais déposés à nouveau aux serveurs de transport Hub Exchange 2010.

Retour au début

## Délais d'expiration SMTP

Lors de la tentative de création d'une copie redondante du message, la connexion SMTP entre le serveur SMTP d'envoi et le serveur principal, ou la session SMTP entre le serveur principal et le serveur de secours peut expirer. Les connecteurs de réception et d'envoi ont un paramètre *ConnectionInactivityTimeOut* utile lorsque des données sont réellement en cours de transmission sur le connecteur. Les connecteurs de réception ont également un paramètre *ConnectionTimeOut* absolu.

Si l'une des sessions SMTP expire avant que le cliché instantané du message ait été créé et ait fait l'objet d'un accusé de réception, le résultat est contrôlé par le paramètre *RejectMessageOnShadowFailure* avec la cmdlet **Set-TransportConfig**. Par défaut, la valeur de ce paramètre est `$false`, ce qui signifie que le message principal est accepté sans création d'un cliché instantané. Si la valeur de ce paramètre est `$true`, le message principal est rejeté avec l'erreur passagère `451 4.4.0`.

Si le cliché instantané d'un message est créé avec succès, mais que la session SMTP entre le serveur SMTP d'envoi et le serveur principal expire, le serveur principal accepte et traite le message principal. Le serveur SMTP d'envoi remet à nouveau le message n'ayant pas fait l'objet d'un accusé de réception, mais la détection de message en double empêche les utilisateurs de boîte aux lettres Exchange de voir les messages en double. Lorsque le serveur SMTP d'envoi dépose à nouveau le message, le serveur principal crée un autre cliché instantané du message. Il n'y a pas de relation entre les clichés instantanés créées au cours des nouveaux dépôts de messages par le serveur SMTP d'envoi.

Le tableau suivant décrit les paramètres qui contrôlent la création des clichés instantanés

### Paramètres de création de clichés instantanés

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Source</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowMessagePreferenceSetting</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   Essayez de créer un cliché instantané du message sur un serveur de boîtes aux lettres se trouvant dans un autre site Active Directory. Si l'opération échoue, essayez de créer un cliché instantané du message sur un serveur se trouvant dans le site Active Directory local.</p></li>
<li><p><code>LocalOnly</code>  Un cliché instantané du message doit être créé uniquement sur un serveur se trouvant dans le site Active Directory local.</p></li>
<li><p><code>RemoteOnly</code> Un cliché instantané du message doit être créé uniquement sur un serveur de transport situé dans un autre site Active Directory.</p></li>
</ul>
<p>Ce paramètre est significatif uniquement lorsque le serveur principal qui tente de créer un cliché instantané du message est un serveur de boîtes aux lettres membre d'un DAG qui s'étend sur plusieurs sites Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxRetriesForRemoteSiteShadow</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>4</p></td>
<td><p>Ce paramètre est utilisé lorsque le serveur de boîtes aux lettres est membre d'un DAG qui s'étend sur plusieurs sites Active Directory.</p>
<ul>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> est réglé sur <code>PreferRemote</code>, tout d'abord, le serveur de boîtes aux lettres essaie de créer un cliché instantané du message sur un autre serveur de boîtes aux lettres dans un site Active Directory distant au nombre de fois spécifié par <em>MaxRetriesForRemoteSiteShadow</em>. Si cela ne fonctionne pas, le serveur de messagerie tente de créer un cliché instantané du message sur un serveur de boîtes aux lettres différentes dans le site Active Directory local au nombre de fois que spécifié par <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> est défini sur <code>RemoteOnly</code>, le serveur de boîtes aux lettres essaie uniquement de créer un cliché instantané du message sur un serveur de boîtes aux lettres se trouvant dans un site Active Directory distant le nombre de fois spécifié par <em>MaxRetriesForRemoteSiteShadow</em>.</p></li>
<li><p>Le</p></li>
</ul>
<p>Lorsqu'un cliché instantané du message ne peut pas être créé avec succès :</p>
<ul>
<li><p>Si <em>RejectMessageOnShadowFailure</em> is <code>$true</code>, le message principal est rejeté avec une erreur passagère.</p></li>
<li><p>Si <em>RejectMessageOnShadowFailure</em> est <code>$false</code>, le message principal est acceptée quand même, mais n'est pas persisté de façon redondante.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MaxRetriesForLocalSiteShadow</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>2</p></td>
<td><p>Ce paramètre est utilisé dans les circonstances suivantes :</p>
<ul>
<li><p>Si le serveur de boîtes aux lettres est membre d'un DAG qui s'étend sur plusieurs sites Active Directory.</p>
<ol>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> est réglé sur <code>PreferRemote</code>, tout d'abord, le serveur de boîtes aux lettres essaie de créer un cliché instantané du message sur un autre serveur de boîtes aux lettres dans un site Active Directory distant au nombre de fois spécifié par <em>MaxRetriesForRemoteSiteShadow</em>. Si cela ne fonctionne pas, le serveur de messagerie tente de créer un cliché instantané du message sur un serveur de boîtes aux lettres différentes dans le site Active Directory local au nombre de fois que spécifié par <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> est défini sur <code>LocalOnly</code>, le serveur de boîtes aux lettres essaie uniquement de créer un cliché instantané du message sur un autre serveur de boîtes aux lettres se trouvant dans le site Active Directory local le nombre de fois spécifié par <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ol></li>
<li><p>Si le serveur de boîtes aux lettres n'est pas membre d'un DAG, ou s'il est membre d'un DAG se trouvant dans un seul site Active Directory, le serveur de boîtes aux lettres essaie uniquement de créer un cliché instantané du message sur un autre serveur de boîtes aux lettres se trouvant dans le site active Directory local le nombre de fois spécifié par <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ul>
<p>Lorsqu'un cliché instantané du message ne peut pas être créé avec succès :</p>
<ul>
<li><p>Si <em>RejectMessageOnShadowFailure</em> is <code>$true</code>, le message principal est rejeté avec une erreur passagère.</p></li>
<li><p>Si <em>RejectMessageOnShadowFailure</em> est <code>$false</code>, le message principal est acceptée quand même, mais n'est pas persisté de façon redondante.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeout</em> sur <strong>Set-ReceiveConnector</strong></p></td>
<td><p>5 minutes dans le service de Transport sur les serveurs de boîtes aux lettres</p>
<p>5 minutes pour une application frontale sur un serveur d'accès au client.</p>
<p>1 minute sur les serveurs de transport Edge.</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP ouverte avec un serveur de messagerie source peut rester inactive avant d'être interrompue. La valeur de ce paramètre doit être inférieure à la valeur spécifiée par le paramètre <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionTimeout</em> sur <strong>Set-ReceiveConnector</strong></p></td>
<td><p>10 minutes dans le service de Transport sur les serveurs de boîtes aux lettres</p>
<p>10 minutes pour une application frontale sur un serveur d'accès au client.</p>
<p>5 minutes sur les serveurs de transport Edge.</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP avec un serveur de messagerie source peut rester ouverte, même si le serveur de messagerie source transmet des données. La valeur de ce paramètre doit être supérieure à la valeur spécifiée par le paramètre <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeOut</em> sur <strong>Set-SendConnector</strong></p></td>
<td><p>10 minutes</p></td>
<td><p>Ce paramètre spécifie la durée maximale pendant laquelle une connexion SMTP ouverte avec un serveur de messagerie de destination peut rester inactive avant d'être interrompue.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Maintenance des messages instantanés

Après la création d'un cliché instantané, le travail de redondance des clichés instantanés ne fait que commencer. Le serveur principal et le serveur de secours doivent rester en contact pour suivre la progression du message.

Lorsque le serveur principal transmet correctement le message au saut suivant, et que le saut suivant accuse réception du message, le serveur principal met à jour l'*état de suppression* du message comme remise complète. L'état ​​de suppression est fondamentalement un message contenant la liste des messages surveillés. Un message remis avec succès n'ayant pas besoin d'être conservé dans une file d'attente de clichés instantanés, une fois que le serveur de secours est informé que le serveur principal a transmis avec succès le message au saut suivant, le serveur de secours déplace le cliché instantané de la file d'attente des clichés instantanés vers Safety Net.

Le serveur de secours détermine l'état de suppression des clichés instantanés dans ses files d'attente de clichés instantanés en interrogeant le serveur principal. Si le serveur de secours ouvre une session SMTP avec le serveur principal pour une raison quelconque, y compris la transmission d'autres messages sans rapport, le serveur de secours émet la commande **XQDISCARD** pour déterminer l'état de suppression des messages principaux. Si le serveur de secours n'a pas ouvert de session SMTP avec le serveur principal après un intervalle de temps préconfiguré, le serveur de secours ouvre une session SMTP avec le serveur principal et émet la commande **XQDISCARD**. La valeur d'expiration est contrôlée par le paramètre *ShadowHeartbeatFrequentcy* de la cmdlet **Set-TransportConfig**. La valeur par défaut est 2 minutes. Lorsque le serveur de secours ouvre une session SMTP avec le serveur principal, ce dernier répond par des *notifications de suppression* pour les messages qui s'appliquent au serveur de secours qui l'interroge. Dans Exchange 2013, les notifications de suppression sont stockées sur le disque, pas dans la mémoire. Par conséquent, si le service de transport Microsoft Exchange redémarre, les notifications de suppression sont conservées. Après le démarrage du service, le serveur principal connaît encore les messages qu'il a traités avec succès, et ces informations sont disponibles pour le serveur de secours.

La communication SMTP entre le serveur de secours et le serveur principal est utilisée en tant que *pulsation* qui détermine la disponibilité des serveurs. Si le serveur de secours ne peut pas ouvrir de session SMTP avec le serveur principal après un intervalle de temps préconfiguré, ou si la base de données de transport du serveur principal possède un ID de base de données différent, le serveur de secours se promeut comme serveur principal, promeut les clichés instantanés comme messages principaux et transmet les messages au saut suivant. La valeur d'expiration est contrôlée par le paramètre *ShadowResubmitTimeSpan* de la cmdlet **Set-TransportConfig**. La valeur par défaut est 3 heures.

Le *Gestionnaire de redondance des clichés instantanés* est le composant d'un serveur de transport Exchange 2013 qui est responsable de la gestion de la redondance des clichés instantanés. Le Gestionnaire de redondance des clichés instantanés est responsable de la gestion des informations suivantes pour tous les messages principaux traités par un serveur :

  - Serveur de secours pour chaque message principal en cours de traitement.

  - État de suppression à envoyer aux serveurs de secours.

Le Gestionnaire de redondance des clichés instantanés est responsable de ce qui suit pour tous les clichés instantanés se trouvant dans les files d'attente de clichés instantanés d'un serveur de secours :

  - Gestion de la liste des serveurs principaux pour chaque cliché instantané.

  - Comparaison de l'ID de base de données originale et de l'ID actuel de la base de données de files d'attente dans laquelle la copie principale du message est stockée.

  - Vérification de la disponibilité de chaque serveur principal pour lequel un cliché instantané est mis en file d'attente.

  - Traitement des notifications de suppression provenant des serveurs principaux.

  - Suppression des clichés instantanés des files d'attentes après réception de toutes les notifications de suppression.

  - Choix du moment où le serveur de secours doit acquérir la propriété des clichés instantanés en devenant serveur principal.

  - Suivi des bifurcations des messages et d'autres messages d'effet secondaire tels que des notifications d'état de remise (DSN) et des rapports de journal pour vérifier que la copie redondante du message n'est pas libérée tant que tous les embranchements du message n'ont pas été entièrement traités.

Le tableau suivant décrit les paramètres qui contrôlent la manière dont les clichés instantanés sont gérés.


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
<td><p><em>ShadowHeartbeatFrequency</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>2 minutes</p></td>
<td><p>Le temps maximal qu'un serveur de secours attend avant d'ouvrir une connexion SMTP sur le serveur principal pour vérifier l'état de suppression des messages.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowResubmitTimeSpan</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>3 heures</p></td>
<td><p>Le délai qu'un serveur observe avant de déterminer qu'un serveur principal a échoué et de s'approprier les clichés instantanés figurant dans la file d'attente des clichés instantanés pour le serveur principal inaccessible.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShadowMessageAutoDiscardInterval</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>2 jours</p></td>
<td><p>Le temps pendant lequel un serveur conserve les événements de suppression pour les messages remis avec succès. Un serveur principal met en file d'attente les événements de suppression jusqu'à ce que le serveur de secours l'interroge. Toutefois, si le serveur de secours n'interroge pas le serveur principal au cours de la période spécifiée par ce paramètre, le serveur principal supprime les événements de suppression en file d'attente.</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> sur <strong>Set-TransportConfig</strong></p></td>
<td><p>2 jours</p></td>
<td><p>Temps pendant lequel les messages traités avec succès sont conservés dans Safety Net. Les clichés instantanés n'ayant pas fait l'objet d'un accusé de réception expirent dans Safety Net après un délai correspondant à la somme des valeurs <em>SafetyNetHoldTime</em> et <em>MessageExpirationTimeout</em> sur <strong>Set-TransportService</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> sur <strong>Set-TransportService</strong></p></td>
<td><p>2 jours</p></td>
<td><p>La durée de temps pendant laquelle un message peut rester dans une file d'attente avant d'expirer.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Traitement des messages après une panne

La redondance des clichés instantanés limite la perte des messages due à des pannes de serveur. Lorsqu'un serveur de transport revient en ligne après une panne, deux scénarios sont possibles :

  - **Le serveur revient en ligne avec une nouvelle base de données de transport**   Dans ce scénario, la base de données de transport est irrécupérable en raison d'une panne de matériel ou parce que des données sont endommagées. Dans ce cas, étant donné que le serveur de transport a un nouvel ID de base de données, il est reconnu comme nouvel itinéraire par les autres serveurs de transport de l'organisation. Cela est également le cas lorsqu'un serveur est irrécupérable et qu'un nouveau serveur est installé en remplacement.

  - **Le serveur revient en ligne avec la même base de données de transport**   Dans ce scénario, le serveur de transport n'est pas tombé en panne, mais a été hors ligne assez longtemps pour que le serveur de secours s'approprie les messages et les dépose à nouveau. Par exemple, une panne de carte réseau ou une longue opération de maintenance sur le serveur peut être à l'origine de ce scénario.

Le tableau suivant résume la manière dont la redondance des clichés instantanés réagit à ces deux scénarios. Par souci de clarté, supposons que le serveur qui a été en panne se nomme Mailbox01.

### Traitement des messages dans les scénarios de récupération

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scénario de récupération</th>
<th>Actions prises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 revient en ligne avec une nouvelle base de données.</p></td>
<td><p>Lorsque Mailbox01 devient indisponible, chaque serveur qui a des clichés instantanés en file d'attente pour Mailbox01 s'approprie ces derniers et les dépose à nouveau. Les messages sont ensuite remis à leurs destinations.</p>
<p>Le retard maximum de messages est la valeur du paramètre <em>ShadowHeartbeatFrequency</em> sur le cmdlet <strong>Set-TransportConfig</strong>. La valeur par défaut est 2 minutes.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 revient en ligne avec la même base de données.</p></td>
<td><p>Une fois Mailbox01 revenu en ligne, il livre les messages figurant dans ses files d'attente qui ont déjà été remis par les serveurs contenant les clichés instantanés de messages pour Mailbox01. Cela entraîne une remise en double de ces messages. Les utilisateurs de boîtes aux lettres Exchange ne voient pas de messages en double en raison de la détection des messages en double. Toutefois, les destinataires sur des systèmes de messagerie non-Exchange peuvent recevoir des copies des messages en double.</p>
<p>Le retard maximum de messages est la valeur du paramètre <em>ShadowResubmitTimeSpan</em> sur le cmdlet <strong>Set-TransportConfig</strong>. La valeur par défaut est 3 heures.</p></td>
</tr>
</tbody>
</table>


Retour au début

