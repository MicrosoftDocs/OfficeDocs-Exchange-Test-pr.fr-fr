﻿---
title: 'Modifications apportées au schéma Active Directory d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Modifications apportées au schéma Active Directory d’Exchange 2013
ms:assetid: 7e879e4e-1124-4a41-94d2-c64500beb24e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb738144(v=EXCHG.150)
ms:contentKeyID: 50478565
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifications apportées au schéma Active Directory d’Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-05-18_

Microsoft Exchange Server 2013 ajoute de nouveaux attributs et classes du schéma Active Directory et en modifie des existants. Cette rubrique de référence fournit un résumé des modifications du schéma Active Directory qui sont effectuées lorsque vous installez la version de publication (RTM) d’Exchange 2013 ou l’un de ses Service Packs ou mises à jour cumulatives. Pour plus d’informations sur les modifications du schéma Active Directory, consultez les fichiers .ldf. Les fichiers .ldf se trouvent dans le répertoire \\amd64\\Setup\\Data\\ des fichiers d’installation Exchange.

Les mises à jour du schéma Exchange 2013 sont cumulatives. Chaque version comprend toutes les modifications incluses dans les versions précédentes. Cela signifie que si vous sautez une version, vous devez quand même appliquer des mises à jour du schéma, même si la version que vous installez n’inclut pas ses propres modifications. Le tableau suivant donne des exemples d’Active Directory lorsqu’il va être mis à jour et lorsqu’il est déjà mis à jour.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Version actuelle d’Exchange 2013 installée</p></th>
<th><p>Nouvelle version d’Exchange 2013 en cours d’installation</p></th>
<th><p>Les mises à jour du schéma sont-elles requises ?</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Service Pack 1</p></td>
<td><p>Mise à jour cumulative 11</p></td>
<td><p><strong>Oui</strong>, les mises à jour sont requises. Les mises à jour du schéma incluses dans CU5, CU6 et CU7 doivent être appliquées.</p></td>
</tr>
<tr class="even">
<td><p>Mise à jour cumulative 6</p></td>
<td><p>Mise à jour cumulative 11</p></td>
<td><p><strong>Oui</strong>, les mises à jour sont requises. Les mises à jour du schéma incluses dans CU7 doivent être appliquées.</p></td>
</tr>
<tr class="odd">
<td><p>Mise à jour cumulative 7</p></td>
<td><p>Mise à jour cumulative 11</p></td>
<td><p><strong>Non</strong>, aucune mise à jour n’est requise. Aucune modification n’a été apportée entre CU7 et CU11.</p></td>
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
<td>Les modifications du schéma Active Directory identifiées dans cette rubrique peuvent ne pas s’appliquer à toutes les éditions d’une version d’Exchange Server.<br />
Pour vous assurer qu’Active Directory a été correctement préparé, consultez la section « Comment savoir si cela a fonctionné ? » dans la rubrique <a href="prepare-active-directory-and-domains-exchange-2013-help.md">Préparation d’Active Directory et des domaines</a>.</td>
</tr>
</tbody>
</table>


Ce document comprend les sections suivantes :

  - Modifications du schéma Active Directory dans les mises à jour cumulatives CU8 et ultérieures d'Exchange 2013

  - Modifications apportées au schéma Active Directory d’Exchange 2013 CU7

  - Modifications apportées au schéma Active Directory d’Exchange 2013 CU6

  - Modifications apportées au schéma Active Directory d’Exchange 2013 CU5

  - Modifications apportées au schéma Active Directory d’Exchange 2013 SP1

  - Modifications apportées au schéma Active Directory d’Exchange 2013 CU3

  - Modifications apportées au schéma Active Directory d’Exchange 2013 CU2

  - Modifications apportées au schéma Active Directory d'Exchange 2013 CU1

  - Modifications apportées au schéma Active Directory Exchange 2013 RTM

## Modifications du schéma Active Directory dans les mises à jour cumulatives CU8 et ultérieures d’Exchange 2013

Aucune modification n’a été apportée au schéma Active Directory dans les mises à jour cumulatives CU8 et ultérieures d’Exchange 2013. La dernière mise à jour cumulative visant à inclure les modifications de schéma est actuellement Exchange 2013 CU7.

Les futures mises à jour cumulatives peuvent contenir des modifications de schéma. Consultez cette page ultérieurement pour chaque version de mise à jour cumulative afin de vérifier que les modifications de schéma ont bien été apportées.

## Modifications apportées au schéma Active Directory d’Exchange 2013 CU7

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU7. Elle inclut les sous-sections suivantes :

  - Classes modifiées par Exchange 2013 CU7

  - Attributs ajoutés par Exchange 2013 CU7

## Classes modifiées par Exchange 2013 CU7

Cette section contient les classes modifiées dans Exchange 2013 CU7.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchStsRefreshTokensValidFrom</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchMultiMailboxGUIDs</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchMultiMailboxLocationsLink</p></td>
</tr>
<tr class="even">
<td><p>Group</p></td>
<td><p>add: auxiliaryClass</p></td>
<td><p>msExchMailStorage</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 CU7

Cette section contient les attributs ajoutés dans Exchange 2013 CU7.

  - ms-Exch-Multi-Mailbox-GUID

  - ms-Exch-Sts-Refresh-Tokens-Valid-From

  - ms-Exch-Multi-Mailbox-Locations-Link

## Modifications apportées au schéma Active Directory d’Exchange 2013 CU6

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU6. Elle inclut les sous-sections suivantes :

  - Classes modifiées par Exchange 2013 CU6

  - Attributs ajoutés par Exchange 2013 CU6

  - Attributs modifiés par Exchange 2013 CU6

## Classes modifiées par Exchange 2013 CU6

Cette section contient les classes modifiées dans Exchange 2013 CU6.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchAuxMailboxParentObjectIdLink</p></td>
</tr>
<tr class="even">
<td><p>Haut</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchAuxMailboxParentObjectIdBL</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 CU6

Cette section contient les attributs ajoutés dans Exchange 2013 CU6.

  - ms-Exch-Aux-Mailbox-Parent-Object-Id-Link

  - ms-Exch-Aux-Mailbox-Parent-Object-Id-BL

## Attributs modifiés par Exchange 2013 CU6

Cette section contient les attributs modifiés dans Exchange 2013 CU6.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Smtp-TLS-Certificate</p></td>
<td><p>replace: rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
</tbody>
</table>


## Modifications apportées au schéma Active Directory d’Exchange 2013 CU5

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU5. Elle inclut les sous-sections suivantes :

  - Classes ajoutées par Exchange 2013 CU5

  - Attributs ajoutés par Exchange 2013 CU5

  - Attributs modifiés par Exchange 2013 CU5

## Classes ajoutées par Exchange 2013 CU5

Cette section contient les classes ajoutées dans Exchange 2013 CU5.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Unified-Policy</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Unified-Rule</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 CU5

Cette section contient les attributs ajoutés dans Exchange 2013 CU5.

  - ms-Exch-UG-Member-Link

  - ms-Exch-UG-Member-BL

## Attributs modifiés par Exchange 2013 CU5

Cette section contient les attributs modifiés dans Exchange 2013 CU5.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Smtp-Receive-Tls-Certificate-Name</p></td>
<td><p>Remplacez: rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>Remplacez: mayContain</p></td>
<td><p>msExchUGMemberLink</p></td>
</tr>
<tr class="odd">
<td><p>Haut</p></td>
<td><p>Remplacez: mayContain</p></td>
<td><p>msExchUGMemberBL</p></td>
</tr>
</tbody>
</table>


## Modifications apportées au schéma Active Directory d’Exchange 2013 SP1

Cette section récapitule les modifications qui ont été apportées au schéma Active Directory lors de l’installation d’Exchange 2013 Service Pack 1 (SP1). Elle inclut les sous-sections suivantes :

  - Classes ajoutées par Exchange 2013 SP1

  - Classes modifiées par Exchange 2013 SP1

  - Attributs ajoutés par Exchange 2013 SP1

  - Attributs de catalogue global ajoutés par Exchange 2013 SP1

  - Attributs modifiés par Exchange 2013 SP1

## Classes ajoutées par Exchange 2013 SP1

Cette section contient les classes ajoutées dans Exchange 2013 SP1.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Intra-Organization-Connector</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Client-Access-Rule</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
</tbody>
</table>


## Classes modifiées par Exchange 2013 SP1

Cette section contient les attributs ajoutés dans Exchange 2013 SP1.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchMailboxContainerGuid</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchUnifiedMailbox</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OAB</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchOABGeneratingMailboxLink</p></td>
</tr>
<tr class="even">
<td><p>Haut</p></td>
<td><p>add: mayContain</p></td>
<td><p>msExchOABGeneratingMailboxBL</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 SP1

Cette section contient les attributs ajoutés dans Exchange 2013 SP1.

  - ms-Exch-OAB-Generating-Mailbox-Link

  - ms-Exch-OAB-Generating-Mailbox-BL

## Attributs de catalogue global ajoutés par Exchange 2013 SP1

Les attributs de catalogue global suivants sont ajoutés par Exchange 2013 SP1 :

  - ms-Exch-Mailbox-Container-Guid

  - ms-Exch-Unified-Mailbox

## Attributs modifiés par Exchange 2013 SP1

Cette section contient les attributs modifiés dans Exchange 2013 SP1.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ms-exch-schema-version-pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15292</p></td>
</tr>
</tbody>
</table>


## Modifications apportées au schéma Active Directory d’Exchange 2013 CU3

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU3. Elle inclut les sous-sections suivantes :

  - Classes ajoutées par Exchange 2013 CU3

  - Attributs ajoutés par Exchange 2013 CU3

  - Attributs modifiés par Exchange 2013 CU3

## Classes ajoutées par Exchange 2013 CU3

Cette section contient les classes ajoutées dans Exchange 2013 CU3.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>msExchThrottlingPolicy</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 CU3

Cette section contient les attributs ajoutés dans Exchange 2013 CU3.

  - ms-Exch-Encryption-Throttling-Policy-State-Ex

## Attributs modifiés par Exchange 2013 CU3

Cette section contient les attributs modifiés dans Exchange 2013 CU3.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprintms-Exch-Sync-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
</tbody>
</table>


## Modifications apportées au schéma Active Directory d’Exchange 2013 CU2

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU2. Elle inclut les sous-sections suivantes :

  - Classes ajoutées par Exchange 2013 CU2

  - Classes modifiées par Exchange 2013 CU2

  - Attributs ajoutés par Exchange 2013 CU2

  - Attributs modifiés par Exchange 2013 CU2

## Classes ajoutées par Exchange 2013 CU2

Cette section contient les classes ajoutées dans Exchange 2013 CU2.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Config-Settings</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Encryption-Virtual-Directory</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## Classes modifiées par Exchange 2013 CU2

Cette section contient les classes modifiées dans Exchange 2013 CU2.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchTenantCountry</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Account-Forest</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchPartnerId</p></td>
</tr>
</tbody>
</table>


## Attributs ajoutés par Exchange 2013 CU2

Cette section contient les attributs ajoutés dans Exchange 2013 CU2.

  - ms-Exch-Tenant-Country

## Attributs modifiés par Exchange 2013 CU2

Cette section contient les attributs modifiés dans Exchange 2013 CU2.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Sync-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>262144</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15281</p></td>
</tr>
</tbody>
</table>


## Identificateurs d’objets ajoutés par Exchange 2013 CU2

Les identificateurs d’objet de classe suivants sont ajoutés lors de l’installation d’Exchange 2013 CU1 :

  - 1.2.840.113556.1.5.7000.62.50204

  - 1.2.840.113556.1.5.7000.62.50205

Les identificateurs d’objet d’attribut suivants sont ajoutés lors de l’installation d’Exchange 2013 CU1 :

  - 1.2.840.113556.1.4.7000.102.52130

## Modifications apportées au schéma Active Directory d'Exchange 2013 CU1

Cette section récapitule les modifications apportées au schéma Active Directory lors de l’installation d’Exchange 2013 CU1. Elle inclut les sous-sections suivantes :

  - Classes modifiées par Exchange 2013 CU1

  - Classes ajoutées par Exchange 2013 CU1

  - Attributs modifiés par Exchange 2013 CU1

  - Identificateurs d'objets ajoutés par Exchange 2013 CU1

  - Attributs indexés ajoutés par Exchange 2013 CU1

  - Jeux de propriétés modifiés par Exchange 2013 CU1

  - Attributs de catalogue global ajoutés par Exchange 2013 CU1

## Classes modifiées par Exchange 2013 CU1

Cette section contient les classes modifiées dans Exchange 2013 CU1.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveRelease</p></td>
</tr>
<tr class="even">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxRelease</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveRelease</p></td>
</tr>
<tr class="even">
<td><p>Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxRelease</p></td>
</tr>
<tr class="odd">
<td><p>Exch-OAB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchLastUpdateTime</p></td>
</tr>
<tr class="even">
<td><p>Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOfflineOrgIdHomeRealmRecord</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCapabilityIdentifiers</p></td>
</tr>
<tr class="even">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchObjectID</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchProvisioningTags</p></td>
</tr>
<tr class="even">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMaxABP</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMaxOAB</p></td>
</tr>
<tr class="even">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>pFContacts</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Team-Mailbox-Provisioning-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>Exch-MDB-Availability-Group</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEvictedMembersLink</p></td>
</tr>
<tr class="odd">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEvictedMemebersBL</p></td>
</tr>
<tr class="even">
<td><p>Exch-On-Premises-Organization</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTrustedDomainLink</p></td>
</tr>
<tr class="odd">
<td><p>Exch-OWA-Mailbox-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>Exch-OWA-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
</tbody>
</table>


## Classes ajoutées par Exchange 2013 CU1

Cette section contient les classes modifiées dans Exchange 2013 CU1.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Mapi-Virtual-Directory</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>Exch-Push-Notifications-App</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## Attributs modifiés par Exchange 2013 CU1

Cette section contient les attributs modifiés dans Exchange 2013 CU1.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Mailflow-Policy-Transport-Rules-Template-Xml</p></td>
<td><p>rangeUpper</p></td>
<td><p>256000</p></td>
</tr>
<tr class="even">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>rangeUpper</p></td>
<td><p>15254</p></td>
</tr>
</tbody>
</table>


## Identificateurs d'objets ajoutés par Exchange 2013 CU1

Les identificateurs d’objet d’attribut suivants sont ajoutés lors de l’installation d’Exchange 2013 CU1 :

  - 1.2.840.113556.1.4.7000.102.52109

  - 1.2.840.113556.1.4.7000.102.52110

  - 1.2.840.113556.1.4.7000.102.52127

  - 1.2.840.113556.1.4.7000.102.52126

  - 1.2.840.113556.1.4.7000.102.52128

  - 1.2.840.113556.1.4.7000.102.52129

Les identificateurs d'objets de classe suivants sont ajoutés lors de l'installation d'Exchange 2013 CU1 :

  - 1.2.840.113556.1.5.7000.62.50202

  - 1.2.840.113556.1.5.7000.62.50203

## Attributs indexés ajoutés par Exchange 2013 CU1

Le tableau suivant répertorie les attributs ajoutés à la liste des attributs indexés lors de l’installation d’Exchange 2013 CU1.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Valeur de l’indicateur de recherche</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Provisioning-Tags</p></td>
<td><p>1</p></td>
</tr>
</tbody>
</table>


## Jeux de propriétés modifiés par Exchange 2013 CU1

Les jeux de propriétés suivants sont modifiés lors de l’installation d’Exchange 2013 CU1 :

  - Exchange-Information

## Attributs de catalogue global ajoutés par Exchange 2013 CU1

Les attributs de catalogue global suivants sont ajoutés par Exchange 2013 CU1 :

  - ms-Exch-Offline-OrgId-Home-Realm-Record

  - ms-Exch-EvictedMembers-Link

  - ms-Exch-EvictedMemebers-BL

## Modifications apportées au schéma Active Directory Exchange 2013 RTM

Cette section récapitule les modifications apportés au schéma Active Directory lors de l’installation d’Exchange 2013 RTM. Elle inclut les sous-sections suivantes :

  - Classes modifiées par Exchange 2013 RTM

  - Attributs modifiés par Exchange 2013 RTM

  - Classes ajoutées par Exchange 2013 RTM

  - Attributs ajoutés par Exchange 2013 RTM

  - Identificateurs MAPI ajoutés par Exchange 2013 RTM

  - Droits étendus ajoutés par Exchange 2013 RTM

  - Identificateurs d'objets ajoutés par Exchange 2013 RTM

  - Attributs indexés ajoutés par Exchange 2013 RTM

  - Attributs de catalogue global publié par Exchange 2013 RTM

## Classes modifiées par Exchange 2013 RTM

Cette section contient les classes modifiées dans Exchange 2013 RTM.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Attribut/Classe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchLocalizationFlags</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRoleGroupType</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncAuthorityMetadata</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncStatusAck</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEdgeSyncConfigFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHABRootDepartmentLink</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDefaultPublicFolderMailbox</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchForestModeFlag</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncStatus</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchIsDirsyncStatusPending</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousArchiveDatabase</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirSyncServiceInstance</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationUpgradePolicyLink</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-OWA-Mailbox-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWASetPhotoURL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OWA-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWASetPhotoURL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWorkloadManagementPolicyLink</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Altitude</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Latitude</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Longitude</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCustomerExpectationCritical</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDiscretionaryCritical</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchInternalMaintenanceCritical</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchUrgentCritical</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Availability-Address-Space</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchFedTargetAutodiscoverEPR</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Private-MDB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxDatabaseTransportFlags</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRecipientSoftDeletedStatus</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWhenSoftDeletedTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute2</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute3</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute4</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute5</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMRSProxyFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMRSProxyMaxConnections</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Active-Sync-Device</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDeviceClientType</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringDeferAttempts</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringDeferWaitTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringFlags</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringPrimaryUpdatePath</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringSecondaryUpdatePath</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringUpdateFrequency</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringUpdateTimeout</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxExpiration</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxOwners</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxSharePointLinkedBy</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxSharePointUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxShowInClientList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCalendarLoggingQuota</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncNonRecipientCookie</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncRecipientCookie</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncReplayList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAccountForestLink</p></td>
</tr>
<tr class="odd">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAccountForestBL</p></td>
</tr>
<tr class="even">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTrustedDomainBL</p></td>
</tr>
<tr class="odd">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAcceptedDomainBL</p></td>
</tr>
<tr class="even">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationMalwareBL</p></td>
</tr>
<tr class="odd">
<td><p>Haut</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationSpamBL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchELCMailboxFlags</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceArchiveMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetArchiveMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationLink</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportResellerSettingsLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchManagementSiteLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationUpgradePolicyLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Fed-OrgId</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchFedDelegationTrustSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Gateway</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMDBSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Gateway</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveDatabaseLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDisabledArchiveDatabaseLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMDBSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousArchiveDatabaseSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousHomeMDBSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveStorageMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-OAB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOffLineABServerSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Routing-Group-Connector</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Site-Connector</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Tenant-Perimeter-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportResellerSettingsLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentByteEncoderTypeFor7BitCharsets</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentPreferredInternetCodePageForShiftJis</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentRequiredCharSetCoverage</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceOnPremisesSmartHost</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceSecureMailCertificateThumbprint</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceTransportServers</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-group-external-member-count</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-group-member-count</p></td>
</tr>
<tr class="even">
<td><p>Ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-organization-flags-2</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGroupExternalMemberCount</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGroupMemberCount</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchShadowWhenSoftDeletedTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationFlags2</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchUMAvailableLanguages</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineCertificationLocationUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineKeySharingLocationUrl</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineLicensingLocationUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchThrottlingPolicyFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringScanTimeout</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamCountryBlockList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamLanguageBlockList</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamNotifyOutboundRecipients</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Malware-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilterConfigExternalSenderAdminAddress</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Malware-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilterConfigInternalSenderAdminAddress</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchActiveInstanceSleepInterval</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPassiveInstanceSleepInterval</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncDaemonMaxVersion</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncDaemonMinVersion</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderMailbox</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderSmtpAddress</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamDigestFrequency</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamQuarantineRetention</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWACDiscoveryEndpoint</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAdfsAuthenticationRawConfiguration</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchServiceEndPointURL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Public-Folder</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderEntryId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Transport-Rule</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportRuleImmutableId</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportMaxRetriesForLocalSiteShadow</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportMaxRetriesForRemoteSiteShadow</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Account-Forest</p></td>
<td><p>possSuperiors</p></td>
<td><p>msExchContainer</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData0</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData2</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCorrelationId</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantCompletionTargetVector</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantFlags</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantSafeLockdownSchedule</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantSourceForest</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartLockdown</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartRetired</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartSync</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStatus</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantTargetForest</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantTransitionCounter</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncCookie</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAnonymousThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEASThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEWSThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGeneralThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchIMAPThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWAThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPOPThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPowershellThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRCAThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailflow-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchImmutableId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MDB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCalendarLoggingQuota</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Rule</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchImmutableId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncServiceInstanceNewTenantMaxVersion</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncServiceInstanceNewTenantMinVersion</p></td>
</tr>
</tbody>
</table>


## Attributs modifiés par Exchange 2013 RTM

Cette section contient les attributs modifiés dans Exchange 2013 RTM.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Classe</th>
<th>Remplacez</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15137</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-HAB-Root-Department-Link</p></td>
<td><p>remplacez: isMemberOfPartialAttributeSet</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Archive-GUID</p></td>
<td><p>remplacez: searchFlags</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accepted-Domain-Name</p></td>
<td><p>remplacez: searchFlags</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Bypass-Audit</p></td>
<td><p>remplacez: searchFlags</p></td>
<td><p>19</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Audit-Enable</p></td>
<td><p>remplacez: searchFlags</p></td>
<td><p>19</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-1</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-2</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-3</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-4</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-5</p></td>
<td><p>isMemberOfPartialAttributeSet</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-On-Premises-Smart-Host</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID : 1.2.840.113556.1.4.7000.102.51992 isMemberOfPartialAttributeSet : Indicateurs de recherche FALSE (pas dans le catalogue global) : 0 (pas d'index)</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprint</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID : 1.2.840.113556.1.4.7000.102.51991 isMemberOfPartialAttributeSet : Indicateurs de recherche FALSE (pas dans le catalogue global) : 0 (pas d'index)</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-Transport-Servers</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID : 1.2.840.113556.1.4.7000.102.51990 isMemberOfPartialAttributeSet : Indicateurs de recherche FALSE (pas dans le catalogue global) : 0 (pas d'index)</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-ELC-Mailbox-Flags</p></td>
<td><p>remplacez: attributeSecurityGuid</p></td>
<td><p>F6SzsVXskUGzJ7cuM+OK8g==</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Malware-Filtering-Update-Frequency</p></td>
<td><p>rangeUpper</p></td>
<td><p>38880</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Forward-Sync-Non-Recipient-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>20480</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Forward-Sync-Recipient-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>20480</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Role-Entries</p></td>
<td><p>rangeUpper</p></td>
<td><p>8192</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Group-External-Member-Count</p></td>
<td><p>ntdsSchemaModify</p></td>
<td><p>isMemberOfPartialAttributeSet: TRUE MAPIID:36066</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Group-Member-Count</p></td>
<td><p>ntdsSchemaModify</p></td>
<td><p>remplacez: isMemberOfPartialAttributeSetisMemberOfPartialAttributeSet : TRUE MAPIID: 36067</p></td>
</tr>
</tbody>
</table>


## Classes ajoutées par Exchange 2013 RTM

Les classes suivantes sont ajoutées lors de l'installation d'Exchange 2013 RTM :

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold

  - ms-Exch-MSO-Forward-Sync-Divergence

  - ms-Exch-MSO-Sync-Service-Instance

  - ms-Exch-Organization-Upgrade-Policy

  - ms-Exch-Workload-Policy

  - ms-Exch-Resource-Policy

  - ms-Exch-Team-Mailbox-Provisioning-Policy

  - ms-Exch-Account-Forest

  - ms-Exch-Hosted-Content-Filter-Config

  - ms-Exch-Hygiene-Configuration

  - ms-Exch-Malware-Filter-Config

  - ms-Exch-Protocol-Cfg-SIP-Container

  - ms-Exch-Protocol-Cfg-SIP-FE-Server

  - ms-Exch-Exchange-Transport-Server

  - ms-Exch-Auth-Auth-Config

  - ms-Exch-Auth-Auth-Server

  - ms-Exch-Auth-Partner-Application

  - ms-Exch-Mailflow-Policy-Collection

  - ms-Exch-Mailflow-Policy

## Attributs ajoutés par Exchange 2013 RTM

Les attributs suivants regroupent un ensemble de modifications requises pour de nouvelles fonctionnalités et sont ajoutés lors de l'installation d'Exchange 2013 RTM :

  - ms-Exch-ActiveSync-Device-AutoBlock-Duration

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Duration

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Limit

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Type

  - ms-Exch-Dirsync-Authority-Metadata

  - ms-Exch-Dirsync-Status

  - ms-Exch-Dirsync-Status-Ack

  - ms-Exch-Edge-Sync-Config-Flags

  - ms-Exch-Is-Dirsync-Status-Pending,

  - ms-Exch-Localization-Flags

  - ms-Exch-Previous-Archive-Database

  - ms-Exch-RoleGroup-Type

  - ms-Exch-External-Directory-Object-Class

  - ms-Exch-MSO-Forward-Sync-Divergence-Count

  - ms-Exch-MSO-Forward-Sync-Divergence-Timestamp

  - ms-Exch-MSO-Forward-Sync-Divergence-Related-Object-Link

  - ms-Exch-Default-Public-Folder-Mailbox

  - ms-Exch-Forest-Mode-Flag

  - ms-Exch-Dir-Sync-Service-Instance

  - ms-Exch-Organization-Upgrade-Policy-Date

  - ms-Exch-Organization-Upgrade-Policy-Enabled

  - ms-Exch-Organization-Upgrade-Policy-MaxMailboxes

  - ms-Exch-Organization-Upgrade-Policy-Priority

  - ms-Exch-Organization-Upgrade-Policy-Source-Version

  - ms-Exch-Organization-Upgrade-Policy-Status

  - ms-Exch-Organization-Upgrade-Policy-Target-Version

  - ms-Exch-OWA-Set-Photo-URL

  - ms-Exch-Organization-Upgrade-Policy-Link

  - ms-Exch-Organization-Upgrade-Policy-BL

  - ms-Exch-Workload-Classification

  - ms-Exch-Workload-Management-Is-Enabled

  - ms-Exch-Workload-Type

  - ms-Exch-Workload-Management-Policy-Link

  - ms-Exch-Workload-Management-Policy-BL

  - ms-Exch-Workload-Management-Policy

  - ms-Exch-Customer-Expectation-Overloaded

  - ms-Exch-Customer-Expectation-Underloaded

  - ms-Exch-Discretionary-Overloaded

  - ms-Exch-Discretionary-Underloaded

  - ms-Exch-Internal-Maintenance-Overloaded

  - ms-Exch-Internal-Maintenance-Underloaded

  - ms-Exch-Resource-Type

  - ms-Exch-Urgent-Overloaded

  - ms-Exch-Urgent-Underloaded

  - ms-DS-GeoCoordinates-Altitude

  - ms-DS-GeoCoordinates-Latitude

  - ms-DS-GeoCoordinates-Longitude

  - ms-Exch-Customer-Expectation-Critical

  - ms-Exch-Discretionary-Critical

  - ms-Exch-Internal-Maintenance-Critical

  - ms-Exch-Urgent-Critical

  - ms-Exch-Mailbox-Database-Transport-Flags

  - ms-Exch-Extension-Custom-Attribute-1

  - ms-Exch-Extension-Custom-Attribute-2

  - ms-Exch-Extension-Custom-Attribute-3

  - ms-Exch-Extension-Custom-Attribute-4

  - ms-Exch-Extension-Custom-Attribute-5

  - ms-Exch-MRS-Proxy-Flags

  - ms-Exch-MRS-Proxy-Max-Connections

  - ms-Exch-Recipient-SoftDeleted-Status

  - ms-Exch-When-Soft-Deleted-Time

  - ms-Exch-Device-Client-Type

  - ms-Exch-Malware-Filtering-Defer-Attempts

  - ms-Exch-Malware-Filtering-Defer-Wait-Time

  - ms-Exch-Malware-Filtering-Flags

  - ms-Exch-Malware-Filtering-Primary-Update-Path

  - ms-Exch-Malware-Filtering-Secondary-Update-Path

  - ms-Exch-Malware-Filtering-Update-Frequency

  - ms-Exch-Malware-Filtering-Update-Timeout

  - ms-Exch-Team-Mailbox-Expiration

  - ms-Exch-Team-Mailbox-Expiry-Days

  - ms-Exch-Team-Mailbox-Owners

  - ms-Exch-Team-Mailbox-SharePoint-Linked-By

  - ms-Exch-Team-Mailbox-SharePoint-Url

  - ms-Exch-Team-Mailbox-Show-In-Client-List

  - ms-Exch-Account-Forest-Link

  - ms-Exch-Account-Forest-BL

  - ms-Exch-Trusted-Domain-Link

  - ms-Exch-Trusted-Domain-BL

  - ms-Exch-Archive-Database-Link-SL

  - ms-Exch-Disabled-Archive-Database-Link-SL

  - ms-Exch-Fed-Delegation-Trust-SL

  - ms-Exch-Home-MDB-SL

  - ms-Exch-Home-MTA-SL

  - ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Source-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Storage-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-MDB-Link-SL

  - ms-Exch-Malware-Filter-Config-Alert-Text

  - ms-Exch-Malware-Filter-Config-External-Body

  - ms-Exch-Malware-Filter-Config-External-Subject

  - ms-Exch-Malware-Filter-Config-Flags

  - ms-Exch-Malware-Filter-Config-From-Address

  - ms-Exch-Malware-Filter-Config-From-Name

  - ms-Exch-Malware-Filter-Config-Internal-Body

  - ms-Exch-Malware-Filter-Config-Internal-Subject

  - ms-Exch-Management-Site-Link-SL

  - ms-Exch-Off-Line-AB-Server-SL

  - ms-Exch-Organization-Upgrade-Policy-Link-SL

  - ms-Exch-Previous-Archive-Database-SL

  - ms-Exch-Previous-Home-MDB-SL

  - ms-Exch-RMS-Computer-Accounts-Link-SL

  - ms-Exch-Spam-Add-Header

  - ms-Exch-Spam-Asf-Settings

  - ms-Exch-Spam-Asf-Test-Bcc-Address

  - ms-Exch-Spam-False-Positive-Cc

  - ms-Exch-Spam-Flags

  - ms-Exch-Spam-Modify-Subject

  - ms-Exch-Spam-Outbound-Spam-Cc

  - ms-Exch-Spam-Redirect-Address

  - ms-Exch-Transport-Reseller-Settings-Link-SL

  - ms-Exch-Hygiene-Configuration-Link

  - ms-Exch-Accepted-Domain-BL

  - ms-Exch-Malware-Filter-Config-Link

  - ms-Exch-Hygiene-Configuration-Malware-BL

  - ms-Exch-Hosted-Content-Filter-Config-Link

  - ms-Exch-Hygiene-Configuration-Spam-BL

  - ms-Exch-Content-Byte-Encoder-Type-For-7-Bit-Charsets

  - ms-Exch-Content-Preferred-Internet-Code-Page-For-Shift-Jis

  - ms-Exch-Content-Required-Char-Set-Coverage

  - ms-Exch-Group-External-Member-Count

  - ms-Exch-Group-Member-Count

  - ms-Exch-Organization-Flags-2

  - ms-Exch-RMSOnline-Certification-Location-Url

  - ms-Exch-RMSOnline-Key-Sharing-Location-Url

  - ms-Exch-RMSOnline-Licensing-Location-Url

  - ms-Exch-Shadow-When-Soft-Deleted-Time

  - ms-Exch-Throttling-Policy-Flags

  - ms-Exch-Malware-Filter-Config-External-Sender-Admin-Address

  - ms-Exch-Malware-Filter-Config-Internal-Sender-Admin-Address

  - ms-Exch-Malware-Filtering-Scan-Timeout

  - ms-Exch-Spam-Country-Block-List

  - ms-Exch-Spam-Language-Block-List

  - ms-Exch-Spam-Notify-Outbound-Recipients

  - ms-Exch-Auth-App-Secret

  - ms-Exch-Auth-Application-Identifier

  - ms-Exch-Auth-Auth-Server-Type

  - ms-Exch-Auth-Authorization-Url

  - ms-Exch-Auth-Certificate-Data

  - ms-Exch-Auth-Certificate-Thumbprint

  - ms-Exch-Auth-Flags

  - ms-Exch-Auth-Issuer-Name

  - ms-Exch-Auth-Issuing-Url

  - ms-Exch-Auth-Linked-Account

  - ms-Exch-Auth-Metadata-Url

  - ms-Exch-Auth-Realm

  - ms-Exch-Mailflow-Policy-Countries

  - ms-Exch-Mailflow-Policy-Keywords

  - ms-Exch-Mailflow-Policy-Publisher-Name

  - ms-Exch-Mailflow-Policy-Transport-Rules-Template-Xml

  - ms-Exch-Mailflow-Policy-Version

  - ms-Exch-Public-Folder-EntryId

  - ms-Exch-Public-Folder-Mailbox

  - ms-Exch-Public-Folder-Smtp-Address

  - ms-Exch-Spam-Digest-Frequency

  - ms-Exch-Spam-Quarantine-Retention

  - ms-Exch-Transport-MaxRetriesForLocalSiteShadow

  - ms-Exch-Transport-MaxRetriesForRemoteSiteShadow

  - ms-Exch-Transport-Rule-Immutable-Id

  - ms-Exch-WAC-Discovery-Endpoint

  - ms-Exch-Anonymous-Throttling-Policy-State-Ex

  - ms-Exch-Canary-Data-0

  - ms-Exch-Canary-Data-1

  - ms-Exch-Canary-Data-2

  - ms-Exch-Correlation-Id

  - ms-Exch-EAS-Throttling-Policy-State-Ex

  - ms-Exch-EWS-Throttling-Policy-State-Ex

  - ms-Exch-General-Throttling-Policy-State-Ex

  - ms-Exch-IMAP-Throttling-Policy-State-Ex

  - ms-Exch-OWA-Throttling-Policy-State-Ex

  - ms-Exch-POP-Throttling-Policy-State-Ex

  - ms-Exch-Powershell-Throttling-Policy-State-Ex

  - ms-Exch-RCA-Throttling-Policy-State-Ex

  - ms-Exch-Relocate-Tenant-Completion-Target-Vector

  - ms-Exch-Relocate-Tenant-Flags

  - ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule

  - ms-Exch-Relocate-Tenant-Source-Forest

  - ms-Exch-Relocate-Tenant-Start-Lockdown

  - ms-Exch-Relocate-Tenant-Start-Retired

  - ms-Exch-Relocate-Tenant-Start-Sync

  - ms-Exch-Relocate-Tenant-Status

  - ms-Exch-Relocate-Tenant-Target-Forest

  - ms-Exch-Relocate-Tenant-Transition-Counter

  - ms-Exch-Sync-Cookie

  - ms-Exch-Adfs-Authentication-Raw-Configuration

  - ms-Exch-Service-End-Point-URL

  - ms-Exch-Sync-Service-Instance-New-Tenant-Max-Version

  - ms-Exch-Sync-Service-Instance-New-Tenant-Min-Version

## Identificateurs MAPI ajoutés par Exchange 2013 RTM

Les identificateurs MAPI suivants sont ajoutés lors de l'installation d'Exchange 2013 RTM :

  - 36066

  - 36067

## Droits étendus ajoutés par Exchange 2013 RTM

Le tableau suivant répertorie les droits étendus ajoutés lors de l'installation d'Exchange 2013 RTM. L'installation d'Exchange 2013RTM ne modifie aucune étendue de droits existant.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Identifiant</th>
<th>Valeurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CN=ms-Exch-SMTP-Accept-XProxyFrom,CN=Extended-Rights,&lt;ConfigurationContainerDN&gt;</p></td>
<td><p>changetype: ntdsSchemaAdd</p>
<p>displayName : Accept XProxyFrom</p>
<p>objectClass: controlAccessRight</p>
<p>rightsGuid : 5bee2b72-50d7-49c7-ba66-39a25daa1e92</p>
<p>validAccesses : 256</p></td>
</tr>
</tbody>
</table>


## Identificateurs d'objets ajoutés par Exchange 2013 RTM

Les identificateurs d'objets d'attribut suivants sont ajoutés lors de l'installation d'Exchange 2013 RTM :

  - 1.2.840.113556.1.4.7000.102.51794

  - 1.2.840.113556.1.4.7000.102.51795

  - 1.2.840.113556.1.4.7000.102.51792

  - 1.2.840.113556.1.4.7000.102.51791

  - 1.2.840.113556.1.4.7000.102.51789

  - 1.2.840.113556.1.4.7000.102.51787

  - 1.2.840.113556.1.4.7000.102.51788

  - 1.2.840.113556.1.4.7000.102.51786

  - 1.2.840.113556.1.4.7000.102.51790

  - 1.2.840.113556.1.4.7000.102.51774

  - 1.2.840.113556.1.4.7000.102.51773

  - 1.2.840.113556.1.4.7000.102.51775

  - 1.2.840.113556.1.4.7000.102.51798

  - 1.2.840.113556.1.4.7000.102.51801

  - 1.2.840.113556.1.4.7000.102.51800

  - 1.2.840.113556.1.4.7000.102.51799

  - 1.2.840.113556.1.4.7000.102.51805

  - 1.2.840.113556.1.4.7000.102.51796

  - 1.2.840.113556.1.4.7000.102.51797

  - 1.2.840.113556.1.4.7000.102.51814

  - 1.2.840.113556.1.4.7000.102.51813

  - 1.2.840.113556.1.4.7000.102.51815

  - 1.2.840.113556.1.4.7000.102.51816

  - 1.2.840.113556.1.4.7000.102.51818

  - 1.2.840.113556.1.4.7000.102.51812

  - 1.2.840.113556.1.4.7000.102.51819

  - 1.2.840.113556.1.4.7000.102.51806

  - 1.2.840.113556.1.4.7000.102.51820

  - 1.2.840.113556.1.4.7000.102.51821

  - 1.2.840.113556.1.4.7000.102.51811

  - 1.2.840.113556.1.4.7000.102.51807

  - 1.2.840.113556.1.4.7000.102.51810

  - 1.2.840.113556.1.4.7000.102.51808

  - 1.2.840.113556.1.4.7000.102.51809

  - 1.2.840.113556.1.4.7000.102.51830

  - 1.2.840.113556.1.4.7000.102.51829

  - 1.2.840.113556.1.4.7000.102.51824

  - 1.2.840.113556.1.4.7000.102.51823

  - 1.2.840.113556.1.4.7000.102.51827

  - 1.2.840.113556.1.4.7000.102.51826

  - 1.2.840.113556.1.4.7000.102.51822

  - 1.2.840.113556.1.4.7000.102.51833

  - 1.2.840.113556.1.4.7000.102.51832

  - 1.2.840.113556.1.4.2183

  - 1.2.840.113556.1.4.2184

  - 1.2.840.113556.1.4.2185

  - 1.2.840.113556.1.4.7000.102.51838

  - 1.2.840.113556.1.4.7000.102.51836

  - 1.2.840.113556.1.4.7000.102.51837

  - 1.2.840.113556.1.4.7000.102.51839

  - 1.2.840.113556.1.4.7000.102.51840

  - 1.2.840.113556.1.4.7000.102.51876

  - 1.2.840.113556.1.4.7000.102.51877

  - 1.2.840.113556.1.4.7000.102.51878

  - 1.2.840.113556.1.4.7000.102.51879

  - 1.2.840.113556.1.4.7000.102.51880

  - 1.2.840.113556.1.4.7000.102.51851

  - 1.2.840.113556.1.4.7000.102.51852

  - 1.2.840.113556.1.4.7000.102.51859

  - 1.2.840.113556.1.4.7000.102.51860

  - 1.2.840.113556.1.4.7000.102.51861

  - 1.2.840.113556.1.4.7000.102.51864

  - 1.2.840.113556.1.4.7000.102.51863

  - 1.2.840.113556.1.4.7000.102.51862

  - 1.2.840.113556.1.4.7000.102.51865

  - 1.2.840.113556.1.4.7000.102.51866

  - 1.2.840.113556.1.4.7000.102.51867

  - 1.2.840.113556.1.4.7000.102.51868

  - 1.2.840.113556.1.4.7000.102.51871

  - 1.2.840.113556.1.4.7000.102.51870

  - 1.2.840.113556.1.4.7000.102.51872

  - 1.2.840.113556.1.4.7000.102.51875

  - 1.2.840.113556.1.4.7000.102.51874

  - 1.2.840.113556.1.4.7000.102.51873

  - 1.2.840.113556.1.4.7000.102.51869

  - 1.2.840.113556.1.4.7000.102.51915

  - 1.2.840.113556.1.4.7000.102.51883

  - 1.2.840.113556.1.4.7000.102.51914

  - 1.2.840.113556.1.4.7000.102.51931

  - 1.2.840.113556.1.4.7000.102.51932

  - 1.2.840.113556.1.4.7000.102.51939

  - 1.2.840.113556.1.4.7000.102.51930

  - 1.2.840.113556.1.4.7000.102.51940

  - 1.2.840.113556.1.4.7000.102.51933

  - 1.2.840.113556.1.4.7000.102.51934

  - 1.2.840.113556.1.4.7000.102.51935

  - 1.2.840.113556.1.4.7000.102.51936

  - 1.2.840.113556.1.4.7000.102.51952

  - 1.2.840.113556.1.4.7000.102.51923

  - 1.2.840.113556.1.4.7000.102.51927

  - 1.2.840.113556.1.4.7000.102.51926

  - 1.2.840.113556.1.4.7000.102.51922

  - 1.2.840.113556.1.4.7000.102.51929

  - 1.2.840.113556.1.4.7000.102.51928

  - 1.2.840.113556.1.4.7000.102.51925

  - 1.2.840.113556.1.4.7000.102.51924

  - 1.2.840.113556.1.4.7000.102.51941

  - 1.2.840.113556.1.4.7000.102.51942

  - 1.2.840.113556.1.4.7000.102.51937

  - 1.2.840.113556.1.4.7000.102.51943

  - 1.2.840.113556.1.4.7000.102.51944

  - 1.2.840.113556.1.4.7000.102.51938

  - 1.2.840.113556.1.4.7000.102.51882

  - 1.2.840.113556.1.4.7000.102.51881

  - 1.2.840.113556.1.4.7000.102.51921

  - 1.2.840.113556.1.4.7000.102.51918

  - 1.2.840.113556.1.4.7000.102.51920

  - 1.2.840.113556.1.4.7000.102.51916

  - 1.2.840.113556.1.4.7000.102.51919

  - 1.2.840.113556.1.4.7000.102.51917

  - 1.2.840.113556.1.4.7000.102.51945

  - 1.2.840.113556.1.4.7000.102.51946

  - 1.2.840.113556.1.4.7000.102.51948

  - 1.2.840.113556.1.4.7000.102.51949

  - 1.2.840.113556.1.4.7000.102.51947

  - 1.2.840.113556.1.4.7000.102.51950

  - 1.2.840.113556.1.4.7000.102.51951

  - 1.2.840.113556.1.4.7000.102.51954

  - 1.2.840.113556.1.4.7000.102.51955

  - 1.2.840.113556.1.4.7000.102.51953

  - 1.2.840.113556.1.4.7000.102.51993

  - 1.2.840.113556.1.4.7000.102.51995

  - 1.2.840.113556.1.4.7000.102.51994

  - 1.2.840.113556.1.4.7000.102.51998

  - 1.2.840.113556.1.4.7000.102.51997

  - 1.2.840.113556.1.4.7000.102.52004

  - 1.2.840.113556.1.4.7000.102.52003

  - 1.2.840.113556.1.4.7000.102.52002

  - 1.2.840.113556.1.4.7000.102.52001

  - 1.2.840.113556.1.4.7000.102.52005

  - 1.2.840.113556.1.4.7000.102.52007

  - 1.2.840.113556.1.4.7000.102.52006

  - 1.2.840.113556.1.4.7000.102.51996

  - 1.2.840.113556.1.4.7000.102.52008

  - 1.2.840.113556.1.4.7000.102.52017

  - 1.2.840.113556.1.4.7000.102.52014

  - 1.2.840.113556.1.4.7000.102.52021

  - 1.2.840.113556.1.4.7000.102.52020

  - 1.2.840.113556.1.4.7000.102.52012

  - 1.2.840.113556.1.4.7000.102.52011

  - 1.2.840.113556.1.4.7000.102.52013

  - 1.2.840.113556.1.4.7000.102.52018

  - 1.2.840.113556.1.4.7000.102.52019

  - 1.2.840.113556.1.4.7000.102.52022

  - 1.2.840.113556.1.4.7000.102.52015

  - 1.2.840.113556.1.4.7000.102.52016

  - 1.2.840.113556.1.4.7000.102.52029

  - 1.2.840.113556.1.4.7000.102.52030

  - 1.2.840.113556.1.4.7000.102.52039

  - 1.2.840.113556.1.4.7000.102.52041

  - 1.2.840.113556.1.4.7000.102.52037

  - 1.2.840.113556.1.4.7000.102.52035

  - 1.2.840.113556.1.4.7000.102.52034

  - 1.2.840.113556.1.4.7000.102.52036

  - 1.2.840.113556.1.4.7000.102.52032

  - 1.2.840.113556.1.4.7000.102.52033

  - 1.2.840.113556.1.4.7000.102.52031

  - 1.2.840.113556.1.4.7000.102.52024

  - 1.2.840.113556.1.4.7000.102.52040

  - 1.2.840.113556.1.4.7000.102.52023

  - 1.2.840.113556.1.4.7000.102.52042

  - 1.2.840.113556.1.4.7000.102.52051

  - 1.2.840.113556.1.4.7000.102.52052

  - 1.2.840.113556.1.4.7000.102.52053

  - 1.2.840.113556.1.4.7000.102.52065

  - 1.2.840.113556.1.4.7000.102.52043

  - 1.2.840.113556.1.4.7000.102.52044

  - 1.2.840.113556.1.4.7000.102.52045

  - 1.2.840.113556.1.4.7000.102.52046

  - 1.2.840.113556.1.4.7000.102.52047

  - 1.2.840.113556.1.4.7000.102.52048

  - 1.2.840.113556.1.4.7000.102.52049

  - 1.2.840.113556.1.4.7000.102.52050

  - 1.2.840.113556.1.4.7000.102.52063

  - 1.2.840.113556.1.4.7000.102.52061

  - 1.2.840.113556.1.4.7000.102.52059

  - 1.2.840.113556.1.4.7000.102.52058

  - 1.2.840.113556.1.4.7000.102.52055

  - 1.2.840.113556.1.4.7000.102.52056

  - 1.2.840.113556.1.4.7000.102.52054

  - 1.2.840.113556.1.4.7000.102.52060

  - 1.2.840.113556.1.4.7000.102.52057

  - 1.2.840.113556.1.4.7000.102.52062

  - 1.2.840.113556.1.4.7000.102.52064

Les identificateurs d'objets de classe suivants sont ajoutés lors de l'installation d'Exchange 2013 RTM :

  - 1.2.840.113556.1.5.7000.62.50161

  - 1.2.840.113556.1.5.7000.62.50162

  - 1.2.840.113556.1.5.7000.62.50163

  - 1.2.840.113556.1.5.7000.62.50166

  - 1.2.840.113556.1.5.7000.62.50164

  - 1.2.840.113556.1.5.7000.62.50165

  - 1.2.840.113556.1.5.7000.62.50167

  - 1.2.840.113556.1.5.7000.62.50170

  - 1.2.840.113556.1.5.7000.62.50172

  - 1.2.840.113556.1.5.7000.62.50171

  - 1.2.840.113556.1.5.7000.62.50173

  - 1.2.840.113556.1.5.7000.62.50178

  - 1.2.840.113556.1.5.7000.62.50174

  - 1.2.840.113556.1.5.7000.62.50176

  - 1.2.840.113556.1.5.7000.62.50177

  - 1.2.840.113556.1.5.7000.62.50187

  - 1.2.840.113556.1.5.7000.62.50188

  - 1.2.840.113556.1.5.7000.62.50190

  - 1.2.840.113556.1.5.7000.62.50189

  - 1.2.840.113556.1.5.7000.62.50191

  - 1.2.840.113556.1.5.7000.62.50192

## Attributs indexés ajoutés par Exchange 2013 RTM

Le tableau suivant répertorie les attributs ajoutés à la liste des attributs indexés lors de l'installation d'Exchange 2013 RTM.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Valeur de l’indicateur de recherche</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Is-Dirsync-Status-Pending</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Archive-GUID</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accepted-Domain-Name</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Audit</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Audit-Enable</p></td>
<td><p>19</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Default-Public-Folder-Mailbox</p></td>
<td><p>19</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OWA-Set-Photo-URL</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Upgrade-Policy-Link</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-DS-GeoCoordinates-Altitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-DS-GeoCoordinates-Latitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-DS-GeoCoordinates-Longitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Database-Transport-Flags</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-1</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-2</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-3</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-4</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-5</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Recipient-SoftDeleted-Status</p></td>
<td><p>27</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-When-Soft-Deleted-Time</p></td>
<td><p>17</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Device-Client-Type</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-Expiration</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-Expiry-Days</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-Owners</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-SharePoint-Linked-By</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-SharePoint-Url</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-Show-In-Client-List</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Home-MDB-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Home-MTA-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Move-Source-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Upgrade-Policy-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Previous-Archive-Database-SL</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Previous-Home-MDB-SL</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Auth-Issuer-Name</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Auth-Application-Identifier</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Rule-Immutable-Id</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Public-Folder-EntryId</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Public-Folder-Mailbox</p></td>
<td><p>24</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Public-Folder-Smtp-Address</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Completion-Target-Vector</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Flags</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Start-Lockdown</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Start-Retired</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Start-Sync</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Transition-Counter</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Sync-Cookie</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Source-Forest</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Status,</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Target-Forest</p></td>
<td><p>9</p></td>
</tr>
</tbody>
</table>


## Attributs de catalogue global publié par Exchange 2013 RTM

Les attributs de catalogue global suivants sont ajoutés par Exchange 2013 RTM :

  - ms-Exch-Dirsync-Authority-Metadata

  - ms-Exch-Dirsync-Status

  - ms-Exch-Dirsync-Status-Ack

  - ms-Exch-Edge-Sync-Config-Flags

  - ms-Exch-Is-Dirsync-Status-Pending

  - ms-Exch-Localization-Flags

  - ms-Exch-Previous-Archive-Database

  - ms-Exch-RoleGroup-Type

  - ms-Exch-HAB-Root-Department-Link

  - ms-Exch-Default-Public-Folder-Mailbox

  - ms-Exch-Team-Mailbox-Expiration

  - ms-Exch-Team-Mailbox-Expiry-Days

  - ms-Exch-Team-Mailbox-Owners

  - ms-Exch-Team-Mailbox-SharePoint-Linked-By

  - ms-Exch-Team-Mailbox-SharePoint-Url

  - ms-Exch-Team-Mailbox-Show-In-Client-List

  - ms-Exch-Recipient-SoftDeleted-Status

  - ms-Exch-When-Soft-Deleted-Time

  - ms-Exch-Device-Client-Type

  - ms-Exch-Extension-Custom-Attribute-1

  - ms-Exch-Extension-Custom-Attribute-2

  - ms-Exch-Extension-Custom-Attribute-3

  - ms-Exch-Extension-Custom-Attribute-4

  - ms-Exch-Extension-Custom-Attribute-5

  - ms-Exch-Archive-Database-Link-SL

  - ms-Exch-Disabled-Archive-Database-Link-SL

  - ms-Exch-Home-MDB-SL

  - ms-Exch-Home-MTA-SL

  - ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Source-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Storage-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-MDB-Link-SL

  - ms-Exch-Previous-Archive-Database-SL

  - ms-Exch-Previous-Home-MDB-SL

  - ms-Exch-RMS-Computer-Accounts-Link-SL

  - ms-Exch-Group-Member-Count

  - ms-Exch-Group-External-Member-Count

  - ms-Exch-Correlation-Id

  - ms-Exch-Relocate-Tenant-Completion-Target-Vector,

  - ms-Exch-Relocate-Tenant-Flags

  - ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule

  - ms-Exch-Relocate-Tenant-Source-Forest

  - ms-Exch-Relocate-Tenant-Start-Lockdown

  - ms-Exch-Relocate-Tenant-Start-Retired

  - ms-Exch-Relocate-Tenant-Start-Sync

  - ms-Exch-Relocate-Tenant-Status

  - ms-Exch-Relocate-Tenant-Target-Forest

  - ms-Exch-Relocate-Tenant-Transition-Counter

  - ms-Exch-Sync-Cookie

