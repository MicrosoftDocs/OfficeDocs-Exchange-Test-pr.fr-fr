---
title: "Déchiffrement de l'état de journal: Exchange 2013 Help"
TOCTitle: Déchiffrement de l'état de journal
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50479071
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Déchiffrement de l'état de journal

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Dans Microsoft Exchange Server 2013, la gestion des droits relatifs à l’information (IRM) permet aux utilisateurs de Microsoft Outlook 2010, et versions ultérieures, ainsi que de Microsoft Office Outlook Web App de protéger leurs messages. Vous pouvez créer des règles de protection Outlook pour appliquer automatiquement la protection IRM aux messages avant leur envoi à partir d’un client Outlook 2010. Vous pouvez également créer des règles de protection de transport pour appliquer la protection IRM aux messages en transit qui répondent aux conditions des règles.

Pour plus d’informations sur les règles de protection Outlook, voir [Règles de protection Outlook](outlook-protection-rules-exchange-2013-help.md).

## Limites des solutions de chiffrement standard

Si votre organisation chiffre les messages à l’aide de solutions traditionnelles, telles que S/MIME, le contenu chiffré ne pourra pas être inspecté par les responsables des enregistrements ni faire l’objet de recherche. L’archivage de messages chiffrés qui comportent du contenu inaccessible ou ne pouvant pas être recherché risque de ne pas répondre aux obligations commerciales, règlementaires ou de conformité. Si votre organisation est dans l’impossibilité de répondre à une demande de découverte électronique (eDiscovery) en raison de messages comportant du contenu indéchiffrable ou ne pouvant être recherché, elle s’expose à des risques juridiques et financiers.

En outre, les stratégies de messagerie de votre organisation peuvent exiger le déchiffrement de messages journalisés pour rendre le contenu accessible aux outils de découverte électronique, aux processus automatisés et aux responsables des enregistrements qui accèdent à la boîte aux lettres de journalisation. Le déchiffrement du rapport de journalisation d’Exchange 2010 peut vous aider à répondre à ces exigences.

Pour en savoir plus sur la journalisation, voir [Journalisation](journaling-exchange-2013-help.md).

## Déchiffrement du rapport de journal

Le déchiffrement du rapport de journalisation permet d’enregistrer en plus des messages protégés par IRM d’origine, une copie déchiffrée de ces messages dans des rapports de journalisation. Si les messages protégés par IRM contiennent des pièces jointes prises en charge préalablement protégées par le cluster AD RMS (Active Directory Rights Management Services) de votre organisation, celles-ci sont également déchiffrées.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour utiliser le déchiffrement du rapport de journalisation, vous devez posséder une licence d’accès client entreprise Exchange. Le déchiffrement du rapport de journalisation ne prend en charge que la journalisation étendue.</td>
</tr>
</tbody>
</table>


Le déchiffrement est effectué par l’agent de déchiffrement du rapport de journalisation, un agent de transport axé sur la conformité. Cet agent déclenche l’événement **OnCategorizedMessage**. Les messages protégés en transit qui font appel aux règles de protection du transport sont déjà chiffrés par l’agent de chiffrement, qui déclenche l’événement **OnRoutedMessage**, avant qu’ils ne parviennent à l’agent de déchiffrement du rapport de journalisation. L’agent de déchiffrement du rapport de journalisation déchiffre ces messages.

> [!NOTE]
> Dans Exchange 2013, l’agent de déchiffrement du rapport de journalisation est un agent intégré. Les agents intégrés ne figurent pas dans la liste d’agents retournée par la cmdlet <strong>Get-TransportAgent</strong>. Pour plus d’informations, voir <a href="transport-agents-exchange-2013-help.md">Agents de transport</a>.


L’agent déchiffre les types de message protégés par IRM suivants :

  - messages auxquels l’utilisateur a appliqué une protection IRM dans Outlook Web App

  - messages auxquels l’utilisateur a appliqué une protection IRM dans Outlook 2010

  - messages auxquels une protection IRM a été automatiquement appliquée dans Outlook 2010 à l’aide de règles de protection Outlook.

  - messages auxquels une protection IRM a été automatiquement appliquée pendant le transit à l’aide de règles de protection du transport.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Seuls les messages auxquels une protection IRM a été appliquée par le serveur AD RMS de votre organisation sont déchiffrés par l’agent de déchiffrement du rapport de journalisation. L’agent ne déchiffre pas les pièces jointes si celles-ci ne sont pas protégées en même temps que le message (et de ce fait ne sont pas soumises à la même licence) ou si un fichier protégé par IRM est joint à un message non protégé.</td>
</tr>
</tbody>
</table>


## Configuration du déchiffrement du rapport de journalisation

Le déchiffrement de rapport de journalisation est configuré à l’aide de la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Toutefois, avant de pouvoir configurer le déchiffrement du rapport de journalisation, vous devez attribuer aux serveurs Exchange 2013 les permissions de déchiffrement du contenu faisant l’objet d’une protection IRM appliquée par le serveur AD RMS. Pour ce faire, vous devez ajouter la boîte aux lettres de fédération au groupe de super utilisateurs sur le cluster AD RMS de votre organisation. Pour plus d’informations, consultez la rubrique [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans le cas de déploiements AD RMS inter-forêts où un cluster AD RMS est déployé dans chaque forêt, vous devez ajouter la boîte aux lettres de fédération au groupe de super utilisateurs au cluster AD RMS dans chaque forêt pour permettre au service de transport Exchange 2013 de déchiffrer les messages protégés sur chaque cluster AD RMS.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la configuration du déchiffrement du rapport de journalisation, voir [Activer ou désactiver le cryptage de rapport de journal](enable-or-disable-journal-report-decryption-exchange-2013-help.md).

Une fois que vous avez activé le déchiffrement du rapport de journalisation, la boîte aux lettres de journalisation peut contenir des rapports comportant des informations sensibles non chiffrées. Il est recommandé de surveiller l’accès à la boîte aux lettres de journalisation et de le restreindre aux personnes autorisées uniquement. Cette recommandation est valable même si vous n’appliquez pas de protection IRM aux courriers électroniques.

