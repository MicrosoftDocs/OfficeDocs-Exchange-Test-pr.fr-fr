---
title: 'Domaines distants: Exchange 2013 Help'
TOCTitle: Domaines distants
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50477519
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Domaines distants

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Vous pouvez créer des entrées de domaine distant pour définir les paramètres de transfert de messages entre l’organisation Microsoft Exchange Server 2013 et les domaines à l’extérieur de votre organisation Exchange. Lorsque vous créez une entrée de domaine distant, vous contrôlez les types de messages envoyés à ce domaine. Vous pouvez également appliquer des stratégies de format de message et des jeux de caractères acceptables aux messages envoyés par des utilisateurs de votre organisation au domaine distant. Les paramètres pour les domaines distants sont des paramètres de configuration globaux pour l’organisation Exchange.

Les paramètres du domaine distant sont appliqués aux messages pendant la catégorisation dans le service de transport sur des serveurs de boîtes aux lettres. Lors de la résolution de destinataire, le domaine du destinataire est comparé aux domaines distants configurés. Si une configuration de domaine distant bloque l’envoi d’un type de message particulier à des destinataires dans ce domaine, le message est supprimé. Si vous spécifiez un format de message particulier pour le domaine distant, les en-têtes et contenus des messages sont modifiés. Les paramètres s’appliquent à tous les messages traités par l’organisation Exchange.

> [!NOTE]
> Si vous configurez les paramètres de message par utilisateur, les paramètres par utilisateur remplacent la configuration de l’organisation.


Par défaut, il n’y a qu’une seule entrée de domaine distant. L’espace d’adressage du domaine est configuré comme un astérisque (\*). Ce signe représente tous les domaines distants. Si vous ne créez pas d’entrées de domaine distant supplémentaires, les mêmes paramètres sont appliqués à tous les messages envoyés à tous les destinataires dans tous les domaines distants.

Lorsque vous configurez des domaines distants, vous pouvez empêcher l’envoi de certains types de messages à ce domaine. Ces types de messages sont les messages de notification d’absence du bureau, les messages de réponse automatique, les notifications d’échec de remise et les notifications de transfert de réunion. Si vous avez un environnement à plusieurs forêts, vous pouvez autoriser l’envoi de ces types de messages à ces domaines. Toutefois, si vous avez identifié un domaine à l’origine du courrier indésirable, vous pouvez bloquer l’envoi de ces types de messages à ces domaines distants.

**Contenu de cette rubrique**

format des messages

Paramètres de réponses automatiques

Contrôle des informations relatives aux notifications d’échec de remise

## format des messages

Vous pouvez spécifier le format de message et le jeu de caractères à utiliser pour les messages électroniques envoyés aux domaines distants. Ces paramètres peuvent être utiles pour vous assurer que les messages envoyés par des expéditeurs de votre domaine à destination du domaine distant sont compatibles avec le système de messagerie destinataire. Par exemple, si vous savez que le système de messagerie du domaine distant est Exchange, vous pouvez spécifier de toujours utiliser le format RTF (rich text format) Exchange. Pour plus d’informations, voir [conversion de contenu.](content-conversion-exchange-2013-help.md).

## Paramètres de réponses automatiques

Dans Exchange 2013, les utilisateurs peuvent définir différentes réponses automatiques pour les destinataires internes et externes. En outre, les types de réponse automatique disponibles au sein de votre organisation dépendent également de la version de Microsoft Outlook utilisée.

Dans Exchange 2013, il existe trois types de réponses automatiques :

  - **Externe**   Pris en charge par Exchange 2013 et Exchange 2010. Peut uniquement être défini par Outlook 2010 ou Office Outlook 2007 ou en utilisant Microsoft Office Outlook Web App.

  - **Interne**   Pris en charge par Exchange 2013 et Exchange 2010. Peut uniquement être défini par Outlook 2010 ou Outlook 2007 ou en utilisant Outlook Web App.

Le tableau suivant décrit plusieurs combinaisons client et serveur et les types de réponse automatique utilisables dans chaque scénario.

**Prise en charge du client et du serveur pour les réponses automatiques**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Version du client</th>
<th>Version d’Exchange</th>
<th>Réponses automatiques prises en charge</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 ou Outlook 2007</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Interne, Externe</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Interne, Externe</p></td>
</tr>
</tbody>
</table>


## Contrôle des informations relatives aux notifications d’échec de remise

Comme indiqué au début de cette rubrique, vous pouvez empêcher l’envoi de ce type de rapport à un domaine distant. En bloquant la transmission de notifications d’échec de remise à un domaine distant, vous pouvez empêcher les informations contenues dans ce type de message de quitter votre organisation, ce qui évite ainsi aux utilisateurs malveillants d’en savoir plus sur votre organisation. Toutefois, les expéditeurs légitimes ne peuvent pas recevoir non plus des rapports de non-remise, ce qui génère de la confusion et une perte de productivité.

Exchange 2013 assure un contrôle plus précis sur le contenu des notifications d’échec de remise destinées à un domaine distant. Avec Exchange 2013, vous pouvez désormais autoriser l’envoi d’une notification d’échec de remise à un domaine distant, tout en retirant les informations de diagnostic. De cette façon, les informations sur votre déploiement Exchange ne quittent pas le périmètre de votre organisation, mais des notifications de non-remise sont quand même fournies aux expéditeurs externes.

Cette fonctionnalité est contrôlée grâce au paramètre *NDRDiagnosticInfoEnabled* de la cmdlet **Set-RemoteDomain**. Ce paramètre étant configurable pour chaque domaine distant, vous pouvez utiliser différents paramètres selon vos besoins. Par exemple, vous pouvez choisir de supprimer les informations de diagnostic pour le domaine distant par défaut, mais autoriser ces informations pour les domaines distants qui représentent vos partenaires.

Pour plus d’informations sur ce nouveau paramètre, consultez la rubrique [Set-RemoteDomain](https://technet.microsoft.com/fr-fr/library/aa997857\(v=exchg.150\)).

