---
title: 'Meilleures pratiques pour la configuration de règles de flux de messagerie: Exchange 2013 Help'
TOCTitle: Meilleures pratiques pour la configuration de règles de flux de messagerie
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65218859
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Meilleures pratiques pour la configuration de règles de flux de messagerie

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Suivez les recommandations suivantes pour Exchange afin d’éviter les erreurs de configuration courantes des règles de transport. Chaque recommandation fournit un lien vers une rubrique comportant un exemple et des instructions pas à pas.

## Tester vos règles

Pour vous assurer que le courrier électronique des utilisateurs ne contient pas d’événement inattendu et pour vous assurer que vous répondez réellement aux intentions commerciales, juridiques ou de conformité de votre règle, veillez à la tester de manière approfondie. Il existe de nombreuses options, et les règles peuvent interagir les unes avec les autres. Il est donc important de vérifier que les messages que vous attendez correspondent à la règle, mais aussi qu’ils n’y correspondent pas si vous avez par erreur rendu une règle trop générale. Pour découvrir toutes les options de test des règles, consultez la rubrique [Tester une règle de flux de messagerie](test-a-mail-flow-rule-exchange-2013-help.md).

## Étendre votre règle

Assurez-vous que votre règle s’applique uniquement aux messages prévus. Par exemple :

  - **Limiter une règle aux messages entrants ou sortants de l’organisation**
    
    Par défaut, une nouvelle règle s’applique aux messages envoyés ou reçus par les membres de votre organisation. Si vous souhaitez que la règle s’applique uniquement dans un sens, veillez à le spécifier dans les conditions de la règle. Pour obtenir un exemple, consultez la rubrique [Scénarios courants de blocage de pièce jointe](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

  - **Restreindre une règle en fonction du domaine de l’expéditeur ou du destinataire**
    
    Par défaut, une nouvelle règle s’applique aux messages envoyés ou reçus à partir d’un domaine. Parfois, vous souhaitez qu’une règle s’applique à tous les domaines à l’exception d’un seul, ou uniquement à un domaine. Pour obtenir des exemples, consultez la rubrique [Création de listes d’expéditeurs bloqués et autorisés à l’échelle de l’organisation dans Office 365](https://technet.microsoft.com/fr-fr/library/dn198251\(v=exchg.150\)).

Pour obtenir une liste complète de toutes les conditions et exceptions disponibles pour les règles de transport, voir :

  - [Exceptions (prédicat) et conditions de règles de flux de messagerie dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919235\(v=exchg.150\))

  - [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [Mail flux conditions et les exceptions (prédicat) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/jj919234\(v=exchg.150\))

## Savoir quand vous avez besoin de deux règles

Parfois, vous avez besoin de deux règles pour obtenir le résultat souhaité. Les règles de transport sont traitées dans l’ordre, plusieurs règles peuvent donc s’appliquer à un même message. Par exemple, si l’une des actions consiste à bloquer le message et que vous souhaitez également appliquer une autre action, comme la copie du message au responsable de l’expéditeur ou la modification de l’objet du message de notification, vous avez besoin de deux règles. La première règle peut copier le message au responsable de l’expéditeur et modifier l’objet, et la deuxième règle peut bloquer le message.

Si vous utilisez deux règles, veillez à ce que les conditions soient identiques. Pour voir des exemples, consultez l’exemple 3 dans [Scénarios courants d’approbation des messages](common-message-approval-scenarios-exchange-2013-help.md), l’exemple 3 dans [Scénarios courants de blocage de pièce jointe](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md) et la rubrique [Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Ne pas répéter une action sur tous les messages d’une conversation

La chaîne de courriers électroniques d’une conversation peut inclure un grand nombre de messages individuels, et le fait de répéter l’action sur chaque message du thread peut devenir gênant. Par exemple, si vous avez une action comme l’ajout d’une clause d’exclusion de responsabilité, vous pouvez l’appliquer uniquement au premier message du thread. Dans ce cas, ajoutez une exception pour les messages qui incluent déjà le texte de la clause d’exclusion de responsabilité. Pour obtenir un exemple, consultez la rubrique [Clauses d’exclusion de responsabilité, signatures, pieds de page ou en-têtes à l’échelle de l’organisation](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Savoir quand arrêter le traitement des règles

Parfois, il est utile d’arrêter le traitement des règles une fois qu’une règle est mise en correspondance. Par exemple, si vous avez une règle pour bloquer les messages comportant des pièces jointes et une autre pour insérer une clause d’exclusion de responsabilité dans les messages qui correspondent à un modèle, vous devriez probablement arrêter le traitement des règles après le blocage du message. Il est inutile d’effectuer une action supplémentaire.

Pour arrêter le traitement des règles après le déclenchement d’une règle, dans cette dernière, cochez la case **Ne plus traiter de règles**.

## Si vous avez un grand nombre de mots clés ou de modèles à mettre en correspondance, chargez-les à partir d’un fichier

Par exemple, vous pouvez empêcher l’envoi de courriers électroniques s’ils contiennent une liste de mots inacceptables ou incorrects. Vous pouvez créer un fichier texte contenant ces mots et expressions, puis utiliser Windows PowerShell pour configurer une règle de transport qui bloque les messages qui les contiennent.

Le fichier texte peut contenir des expressions régulières pour les modèles. Ces expressions ne respectent pas la casse. Voici quelques exemples d’expressions régulières courantes :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expression</strong></p></td>
<td><p><strong>Correspond à</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Tout caractère unique</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Tout caractère supplémentaire</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Tout chiffre décimal</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p>Tout caractère unique dans <em>character_group</em>.</p></td>
</tr>
</tbody>
</table>


Pour obtenir un exemple qui illustre un fichier texte comportant des expressions régulières et les commandes Windows PowerShell du module Exchange à utiliser, consultez la rubrique [Utiliser des règles de flux de messagerie pour acheminer le courrier électronique en fonction d’une liste de mots, d’expressions ou de modèles](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md).

Pour découvrir comment spécifier des modèles à l’aide d’expressions régulières, consultez la rubrique [Langage des expressions régulières - Aide-mémoire](https://go.microsoft.com/fwlink/p/?linkid=532394).

