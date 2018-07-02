---
title: 'Déchiffrement du transport: Exchange 2013 Help'
TOCTitle: Déchiffrement du transport
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50477981
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Déchiffrement du transport

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-07_

Dans Microsoft Exchange Server 2013, Microsoft Outlook 2010 et les versions ultérieures, et Microsoft Office Outlook Web App, les utilisateurs peuvent recourir à la fonctionnalité de gestion des droits relatifs à l’information (IRM) pour protéger leurs messages. Vous pouvez créer des règles de protection Outlook pour appliquer automatiquement la protection IRM aux messages avant qu’ils ne soient envoyés depuis un client Outlook 2010. Vous pouvez également créer des règles de protection de transport pour appliquer la protection IRM aux messages en transit qui répondent aux conditions des règles. Le déchiffrement du transport permet d’accéder au contenu de la messagerie protégée par IRM pour appliquer des stratégies de messagerie.

Pour les tâches de gestion liées à la gestion de l’IRM, voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Limites des autres solutions de chiffrement

Si la protection des informations confidentielles, notamment des informations ayant un impact significatif sur l’activité et les informations d’identification personnelle, est essentielle pour votre entreprise, envisagez de chiffrer les messages électroniques et les pièces jointes. Les solutions de chiffrement du courrier électronique, telles que S/MIME, existent sur le marché depuis longtemps. Ces solutions ont été plus ou moins adoptées par des organisations de types différents. Cependant, elles présentent les limitations suivantes :

  - **Incapacité à appliquer les stratégies de messagerie**   Les organisations sont également confrontées à des exigences de conformité qui requièrent la vérification du contenu de la messagerie pour s’assurer qu’il participe aux stratégies de messagerie. Toutefois, les messages chiffrés avec la plupart des solutions de chiffrement basées sur un client, notamment S/MIME, empêchent toute vérification du contenu sur le serveur. Sans vérification du contenu, une organisation ne peut pas vérifier que tous les messages envoyés ou reçus par ses utilisateurs sont conformes aux stratégies de messagerie. Par exemple, dans un souci de respect d’une réglementation, vous avez configuré une règle de transport pour détecter des informations d’identification personnelle, tel qu’un numéro de sécurité sociale, et appliquer automatiquement une clause d’exclusion de responsabilité au message. Si le message est chiffré, l’agent de règles de transport sur le service de transport ne peut pas accéder au contenu du message et n’appliquera donc pas la clause d’exclusion de responsabilité. Il en résulte une violation de la règle.

  - **Diminution de la sécurité**   Les logiciels antivirus ne peuvent pas analyser le contenu des messages chiffrés, exposant ainsi une organisation à des risques de contenu malveillant, tel que des virus ou des vers. Les messages chiffrés sont généralement considérés comme approuvés par la plupart des utilisateurs, ce qui accroît les risques de propagation des virus au sein de votre organisation. Par exemple, vous avez configuré une règle de protection Outlook pour appliquer automatiquement la protection IRM à tous les messages envoyés à la liste de distribution Tous les employés à l’aide du modèle RMS (Rights Management Services) confidentiel de l’entreprise. La station de travail d’un utilisateur est contaminée par un virus qui se propage en utilisant automatiquement l’option Répondre à tous pour répondre aux messages. Si le message porteur du virus est chiffré, le logiciel antivirus ne peut pas analyser le message.

  - **Impact sur les agents de transport personnalisés**   La plupart des organisations développent des agents de transport personnalisés à différentes fins, comme par exemple, pour satisfaire aux conditions requises de traitement supplémentaires de la conformité, de la sécurité ou du routage de messages personnalisés. Les agents de transport personnalisés mis au point par une organisation pour vérifier ou modifier des messages sont incapables de traiter les messages chiffrés. Si les agents de transport personnalisés créés par votre organisation ne peuvent pas accéder au contenu des messages, leur chiffrement peut empêcher votre organisation d’atteindre les objectifs pour lesquels elle a élaboré ces agents.

## Utilisation du chiffrement du transport pour le contenu chiffré

Dans Exchange 2013, les fonctionnalités de gestion des droits relatifs à l’information répondent à ces défis. Si les messages sont protégés par IRM, le déchiffrement du transport permet de les déchiffrer en cours de transit. Les messages protégés par IRM sont déchiffrés par l’agent de déchiffrement, un agent de transport axé sur la conformité.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange 2013, l’agent de déchiffrement est un agent intégré. Les agents intégrés ne figurent pas dans la liste des agents renvoyés par la cmdlet <strong>Get-TransportAgent</strong>. Pour de plus amples informations, consultez la rubrique <a href="transport-agents-exchange-2013-help.md">Agents de transport</a>.</td>
</tr>
</tbody>
</table>


L’agent de déchiffrement déchiffre les types de messages protégés par IRM suivants :

  - Messages protégés par IRM par l’utilisateur dans Outlook Web App.

  - Messages protégés par IRM par l’utilisateur dans Outlook 2010.

  - Messages automatiquement protégés par IRM via des règles de protection Outlook dans Exchange 2013 et Outlook 2010.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Seuls les messages protégés par IRM via le serveur AD RMS de votre organisation sont déchiffrés par l’agent de déchiffrement.</td>
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
<td>Les messages protégés pendant leur transit à l’aide de règles de protection du transport n’ont pas besoin d’être déchiffrés par l’agent de déchiffrement. L’agent de déchiffrement est déclenché lors des événements de transport <strong>OnEndOfData</strong> et <strong>OnSubmit</strong>. Les règles de protection du transport sont appliquées par l’Agent de règles de transport, qui est déclenché lors de l’événement <strong>OnRoutedMessage</strong> et la protection par IRM est appliquée par l’agent de chiffrement lors de l’événement <strong>OnRoutedMessage</strong>. Pour de plus amples informations sur les agents de transport et obtenir une liste des événements SMTP au cours desquels ils peuvent être enregistrés, consultez la rubrique <a href="transport-agents-exchange-2013-help.md">Agents de transport</a>.</td>
</tr>
</tbody>
</table>


Le déchiffrement du transport est exécuté sur le premier service de transport Exchange 2013 qui traite un message dans une forêt Active Directory. Si un message est transmis à un service de transport dans une autre forêt Active Directory, les message est à nouveau déchiffré. Une fois déchiffré, le contenu est accessible aux autres agents de transport situés sur ce serveur. Par exemple, l’agent de règles de transport sur un service de transport peut vérifier le contenu d’un message et appliquer des règles de transport. Toutes les opérations spécifiées dans la règle, telles que l’application d’une clause d’exclusion de responsabilité ou la modification du message d’une autre manière quelconque, peuvent être réalisées sur le message déchiffré. Les agents de transport tiers, tels que les logiciels antivirus, peuvent rechercher la présence de virus et de logiciels malveillants dans le message. Une fois que les autres agents de transport ont vérifié le message et y ont éventuellement apporté des modifications, le message est de nouveau chiffré avec les mêmes droits d’utilisateur que ceux utilisés avant son déchiffrement par l’agent de déchiffrement. Le même message ne fait pas l’objet d’un nouveau déchiffrement par un autre service de transport sur les serveurs de boîtes aux lettres de l’organisation.

Les messages déchiffrés par l’agent de déchiffrement ne quittent pas le service de transport sans être à nouveau chiffrés. Si une erreur passagère est renvoyée lors du déchiffrement ou du chiffrement du message, le service de transport retente l’opération à deux reprises. Après le troisième échec, l’erreur est considérée comme permanente. Lorsqu’une erreur permanente se produit, notamment lorsque des erreurs passagères sont considérées comme permanentes après plusieurs tentatives, le service de transport les traite comme suit :

  - Si l’erreur permanente se produit pendant le déchiffrement, une notification d’échec de remise (NDR) n’est envoyée que si le déchiffrement du transport est défini sur `Mandatory` et le message chiffré envoyé en même temps que la notification. Pour plus d’informations sur les options de configuration disponibles pour le déchiffrement du transport, consultez la section Configuring Transport Decryption plus loin dans cette rubrique.

  - Si l’erreur permanente se produit pendant le rechiffrement, une notification d’échec de remise est toujours envoyée sans le message déchiffré.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tous les agents personnalisés ou tiers installés sur un service de transport ont accès au message déchiffré. Vous devez tenir compte du comportement de ces agents de transport. Nous vous recommandons de tester minutieusement tous les agents de transport personnalisés et tiers avant de les déployer dans un environnement de production.<br />
Une fois un message déchiffré par l’agent de déchiffrement, si un agent de transport crée un nouveau message et incorpore (lie) le message d’origine au nouveau, seul le nouveau message est protégé. Le message d’origine, qui devient une pièce jointe au nouveau message, n’est pas rechiffré. Un destinataire qui reçoit ce message peut ouvrir le message joint et effectuer des opérations sur ce dernier, comme par exemple, le transférer ou y répondre, ayant pour conséquence d’ignorer l’application des droits.</td>
</tr>
</tbody>
</table>


## Configuration du déchiffrement du transport

Le déchiffrement du transport est configuré à l’aide de la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Cependant, vous devez préalablement attribuer aux serveurs Exchange 2013 l’autorisation de déchiffrer le contenu protégé par votre serveur AD RMS. Pour cela, vous devez ajoutez la boîte aux lettres de fédération au groupe des super utilisateurs configuré sur le cluster AD RMS de votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans les déploiements AD RMS inter-forêts où un cluster AD RMS est déployé dans chaque forêt, vous devez ajouter la boîte aux lettres de fédération au groupe des super utilisateurs sur le cluster de chaque forêt pour autoriser le service de transport sur un serveur de boîtes aux lettres Exchange 2013 ou un serveur de transport Hub Exchange 2010 à déchiffrer les messages protégés dans chaque cluster AD RMS.</td>
</tr>
</tbody>
</table>


Pour plus d’informations, consultez la rubrique [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

Exchange 2013 propose deux configurations différentes pour activer le déchiffrement du transport :

  - **Obligatoire**   Lorsque le déchiffrement du transport est défini sur `Mandatory`, l’agent de déchiffrement rejette le message et renvoie une notification d’échec de remise à l’expéditeur si une erreur permanente est renvoyée lors du déchiffrement d’un message. Si votre organisation ne souhaite pas remettre un message parce qu’il est impossible de le déchiffrer ou que des actions, telles que l’analyse antivirus, et des règles de transport sont appliquées, vous devez choisir cette configuration.

  - **Facultatif**   Lorsque le déchiffrement du transport est défini sur Facultatif, l’agent de déchiffrement adopte une meilleure approche. Non seulement les messages ne présentant aucun problème particulier sont déchiffrés, mais les messages dont le déchiffrement produit une erreur permanente sont également remis. Si votre organisation accorde plus d’importance à la remise des messages qu’à la stratégie de messagerie, optez plutôt pour cette configuration.

Pour de plus amples informations sur la configuration du déchiffrement du transport, consultez la rubrique [Activer ou désactiver le déchiffrement du transport](enable-or-disable-transport-decryption-exchange-2013-help.md).

