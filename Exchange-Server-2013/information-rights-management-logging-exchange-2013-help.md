---
title: 'Journalisation de la gestion des droits relatifs à l’information: Exchange 2013 Help'
TOCTitle: Journalisation de la gestion des droits relatifs à l’information
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50479413
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Journalisation de la gestion des droits relatifs à l’information

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Dans Microsoft Exchange Server 2013, les opérations de gestion des droits relatifs à l'information (IRM) sont consignées dans des journaux IRM. Les journaux IRM vous permettent de contrôler et de résoudre les problèmes d’interaction entre le client RMS (Rights Management Services) sur un serveur Exchange 2013 et le cluster AD RMS (Active Directory Rights Management Services) dans votre organisation.

Pour en savoir plus sur IRM, voir [Gestion des droits relatifs à l’information](information-rights-management-exchange-2013-help.md).

**Contenu de cette rubrique**

Structure des journaux IRM

Processus d’enregistrement

Informations écrites dans les journaux IRM

Gestion des journaux IRM

Souhaitez-vous rechercher les tâches de gestion liées à IRM ? Voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Structure des journaux IRM

Par défaut, les journaux IRM se trouvent dans C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs.

La convention d’affectation de noms des fichiers journaux IRM est \<*Processus*\>\_\<*Identificateur de processus* ou *Identificateur du pool d’applications IIS*\>\_IRMLOG*aaammjj*-*nnnn*.log, où :

  - \<*Processus*\>= processus qui a généré le fichier journal. Par exemple, sur des serveurs de transport, ce sera EdgeTransport.

  - \<*Identificateur de processus* ou *Identificateur du pool d’applications IIS\>* =ID numérique du processus.

  - *aaaammjj* = Date au format UTC à laquelle le fichier journal a été créé.

  - *nnnn* = numéro d’instance, qui commence à 1 pour chaque jour.

Voici un exemple de nom pour un fichier journal IRM : EdgeTransport\_1056\_IRMLOG20101201-1.log.

Le tableau suivant présente les journaux générés sur différents rôles serveur.

### Journaux sur les rôles serveur

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Rôle serveur</th>
<th>Nom du fichier journal IRM</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>service de transport</p></td>
<td><p>EdgeTransport_&lt;<em>Identificateur de processus</em>&gt;_IRMLOG<em>aaaammjj</em>-<em>nnnn</em>.log</p></td>
<td><p>Ce journal est utilisé pour enregistrer toutes les transactions RMS réalisées par le pipeline de transport sur les serveurs de transport (par exemple, les règles de protection de transport et le déchiffrement des rapports de journal). L’identificateur de processus (PID) du processus edgetransport.exe est utilisé pour générer le nom du fichier journal.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres</p></td>
<td><p>msftefd_&lt;<em>Identificateur de processus</em>&gt;_IRMLOG<em>aaaammjj</em>-<em>nnnn</em>.log</p></td>
<td><p>Ce journal est utilisé pour enregistrer toutes les transactions RMS qui se produisent au cours des requêtes de recherche et d’indexation. Les serveurs de boîtes aux lettres Exchange 2013 utilisent le processus msftefd.exe pour indexer le contenu. Le PID du processus msftefd.exe est utilisé pour générer le nom du fichier journal.</p></td>
</tr>
<tr class="odd">
<td><p>Accès au client</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>aaaammjj</em>-<em>nnnn</em>.log</p></td>
<td><p>Ce journal est utilisé pour enregistrer toutes les transactions concernant IRM dans Microsoft OfficeOutlook Web App.</p></td>
</tr>
<tr class="even">
<td><p>Tous les rôles serveur Exchange 2013</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>aaaammjj</em>-<em>nnnn</em>.log</p></td>
<td><p>Ce journal est utilisé pour enregistrer toutes les transactions RMS IRM émanant de Windows PowerShell, par exemple, lors de l’exécution de la cmdlet <strong>Test-IRMConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


Structure des journaux IRM

## Processus d’enregistrement

Les informations sont écrites dans le fichier journal jusqu’à ce que la taille du fichier atteigne sa valeur maximale spécifiée. Lorsque la taille maximale est atteinte, un fichier journal doté d’un numéro d’instance incrémentiel est créé. Ce processus est répété au cours de la journée. L’enregistrement circulaire supprime les fichiers journaux les plus anciens lorsque le répertoire des journaux IRM atteint sa taille maximale spécifiée ou lorsqu’un fichier journal atteint l’âge maximal spécifié dans la configuration d’enregistrement IRM sur chaque serveur.

Structure des journaux IRM

## Informations écrites dans les journaux IRM

Les fichiers journaux IRM sont des fichiers texte contenant des données au format CSV (valeurs séparées par des virgules). Chaque journal IRM comporte un en-tête qui stipule les informations suivantes :

  - **\#Software**   Nom du logiciel ayant créé le fichier journal IRM. La valeur par défaut est généralement `Microsoft Exchange Server`.

  - **\#Version**   Numéro de version du logiciel ayant créé le fichier journal IRM.

  - **\#Log-type**   Type de journal, la valeur est `Rms Client Manager Log`.

  - **\#Date**   Date et heure UTC de création du fichier journal. La date et l’heure UTC sont représentées au format de date-heure ISO 8601 : *aaaa*-*mm*-*jj*T*hh*:*mm*:*ss.fff*Z, où :
    
      - aaaa = année
    
      - *mm* = mois
    
      - *jj* = jour
    
      - T = indicateur temporel spécifiant le début du composant temporel
    
      - *hh* = heure
    
      - *mm* = minute
    
      - *ss* = seconde
    
      - *fff* = fractions d’une seconde
    
      - Z = Zulu, qui est une autre manière de désigner le temps universel (UTC)

  - **\#Fields**   Noms de champ séparés par des virgules utilisés dans les fichiers journaux IRM.
    
    Le journal IRM stocke chaque événement de transaction RMS sur une seule ligne, dans des champs séparés par une virgule. Le tableau suivant répertorie les champs des journaux IRM pour tous les rôles serveur pour lesquels les fonctionnalités IRM sont activées.
    
    ### Champs utilisés dans les journaux IRM
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Champ</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>Indique l’horodateur UTC.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>Indique la fonctionnalité client RMS utilisée. Les valeurs valides sont les suivantes :</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>Vérification de signature</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>Indique le type d’événement. Les valeurs valides sont les suivantes :</p>
    <ul>
    <li><p><code>Acquire</code>   Une licence RMS ou un modèle est demandé.</p></li>
    <li><p><code>Success</code>   Une licence RMS ou un modèle a été acquis.</p></li>
    <li><p><code>Exception</code>   Une erreur s’est produite.</p></li>
    <li><p><code>Queued</code>   Une requête est en attente.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>Réservé à l’usage Microsoft interne.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>Indique l’URL du serveur RMS qui a été consultée au cours de l’opération.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>Champ utilisé par le processus appelant pour rassembler plusieurs transactions RMS. Les valeurs valides sont les suivantes :</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>Identifie une transaction unique. Tous les événements qui se produisent au cours d’une transaction portent le même identifiant de transaction.</p></td>
    </tr>
    </tbody>
    </table>


Structure des journaux IRM

## Gestion des journaux IRM

Sur chaque rôle serveur sur lequel des fonctionnalités IRM sont activées, l’enregistrement IRM est activé par défaut. Pour chaque rôle serveur, vous pouvez modifier la configuration suivante des journaux IRM à l’aide de la cmdlet **Set** correspondante du rôle serveur. Par exemple, pour configurer l’enregistrement IRM sur un serveur de boîte aux lettres, utilisez la cmdlet **Set-MailboxServer**.

### Paramètres de configuration des journaux IRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>Active l’enregistrement des transactions IRM. L’enregistrement des transactions IRM est activé par défaut. Pour désactiver l’enregistrement IRM pour un rôle serveur, définissez le paramètre sur <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>Indique l’âge maximal d’un fichier journal IRM. Les fichiers plus anciens que l’âge spécifié sont supprimés. La valeur par défaut est <code>30.00:00:00</code> (30 jours).</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>Indique la taille maximale de tous les journaux IRM dans le répertoire des journaux de connectivité. Si un répertoire atteint sa taille maximale de fichier, le serveur supprime d’abord les fichiers journaux les plus anciens. La valeur par défaut est <code>250 MB</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>Indique la taille de fichier maximale pour un seul fichier journal. Lorsqu’un fichier atteint la taille spécifiée, un fichier journal est créé et le numéro d’instance est incrémenté. La valeur par défaut est <code>10 MB</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>Indique l’emplacement du journal IRM. Le chemin d'accès par défaut est %ExchangeInstallPath%Logging\IRMLogs.</p></td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/fr-fr/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/fr-fr/library/jj215682\(v=exchg.150\))

Structure des journaux IRM

