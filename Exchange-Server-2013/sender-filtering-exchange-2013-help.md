---
title: 'Filtrage des expéditeurs: Exchange 2013 Help'
TOCTitle: Filtrage des expéditeurs
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 50478921
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrage des expéditeurs

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-12_

Le filtrage des expéditeurs s’appuie sur l’en-tête SMTP MAIL FROM: pour déterminer l’action à effectuer (le cas échéant) pour un message entrant. Le filtrage des expéditeurs est fourni par l'agent de filtrage des expéditeurs.

L'agent de filtrage des expéditeurs agit sur les messages provenant d'expéditeurs spécifiques externes à l'organisation. Les administrateurs tiennent à jour une liste d’expéditeurs dont les messages envoyés à l’organisation sont bloqués. En tant qu’administrateur, vous pouvez bloquer des expéditeurs individuels (par exemple, kim@contoso.com), des domaines entiers (contoso.com) ou des domaines et tous leurs sous-domaines (\*.contoso.com). Vous pouvez également configurer l'action que l'agent de filtrage des expéditeurs doit effectuer quand un message dont l'expéditeur est bloqué est identifié. Vous pouvez configurer les actions suivantes :

  - L’agent de filtrage des expéditeurs rejette la demande SMTP avec une erreur de session SMTP « `554 5.1.0 Sender Denied` » et ferme la connexion.

  - L'agent de filtrage des expéditeurs accepte le message et le met à jour pour indiquer qu'il provient d'un expéditeur bloqué. Étant donné que le message provient d'un expéditeur bloqué et est marqué comme tel, l'agent de filtrage du contenu utilise cette information pour calculer le seuil de probabilité de courrier indésirable.

Vous pouvez désigner des expéditeurs bloqués et définir la manière dont l’agent doit traiter les messages d’expéditeurs bloqués. Pour plus d'informations sur la configuration de l'agent de filtrage des expéditeurs, voir [Gérer le filtrage des expéditeurs](manage-sender-filtering-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les en-têtes MAIL FROM: SMTP peuvent être usurpées. C'est pourquoi vous ne devez pas vous appuyer uniquement sur l'agent de filtrage des expéditeurs. Utilisez l'agent de filtrage des expéditeurs et l'agent d'ID de l'expéditeur conjointement. L’agent d’ID de l’expéditeur utilise l’adresse IP du serveur d’envoi pour vérifier que le domaine dans l’en-tête MAIL FROM: SMTP correspond au domaine qui est enregistré. Pour plus d'informations sur l'agent d'ID de l'expéditeur, consultez la rubrique <a href="sender-id-exchange-2013-help.md">ID de l'expéditeur</a>.</td>
</tr>
</tbody>
</table>


## Utilisation de l’agent de filtrage des expéditeurs pour bloquer des messages

Quand l’agent de filtrage des expéditeurs est activé sur un serveur Exchange, le filtrage des expéditeurs bloque tous les messages entrants qui proviennent d’Internet et ne sont pas authentifiés. Ces messages sont traités comme des messages externes. Vous pouvez désactiver l’agent de filtrage des expéditeurs dans des configurations d’ordinateur individuelles. Pour plus d’informations, voir [Gérer le filtrage des expéditeurs](manage-sender-filtering-exchange-2013-help.md).

Lorsque vous activez l’agent de filtrage des expéditeurs sur un serveur Exchange, il filtre tous les messages en provenance de tous les connecteurs de réception sur cet ordinateur. Comme indiqué précédemment dans cette rubrique, seuls les messages provenant de sources externes sont filtrés. Les *sources externes* sont définies comme sources non authentifiées. et sont considérées comme des sources Internet anonymes.

Nous vous conseillons de ne pas filtrer les messages électroniques provenant de partenaires approuvés ou de l’intérieur de votre organisation. Lorsque vous exécutez des filtres anti-spam, il est toujours possible que les filtres détectent des faux positifs. Configurez les agents de blocage du courrier indésirable de manière à ce qu’ils s’exécutent uniquement sur les messages de sources potentiellement non approuvées et inconnues. Cela réduira le risque que les filtres de blocage du courrier indésirable filtrent incorrectement des messages légitimes. Vous pouvez activer et désactiver l’agent de filtrage des expéditeurs pour qu’il s’exécute sur les messages de n’importe quelle source. Pour plus d’informations, voir [Gérer le filtrage des expéditeurs](manage-sender-filtering-exchange-2013-help.md).

Vous pouvez configurer l'agent de filtrage des expéditeurs pour bloquer les messages entrants qui ne spécifient pas un expéditeur et un domaine dans l'en-tête MAIL FROM: SMTP. Vous pouvez utiliser cette fonction pour empêcher les attaques de rapports de non-remise sur le serveur Exchange. La plupart des messages SMTP légitimes proviennent de serveurs SMTP qui fournissent un expéditeur et un domaine dans la commande MAIL FROM: SMTP.

## Spécification de l’action de blocage

Après avoir spécifié les expéditeurs et les domaines bloqués, vous devez spécifier la manière dont l'agent de filtrage des expéditeurs agit sur les messages provenant d'expéditeurs et de domaines bloqués. Il est conseillé de rejeter les messages. Lorsque vous utilisez l’agent de filtrage des expéditeurs pour bloquer des adresses de messagerie et des domaines qui sont indiqués par un administrateur Exchange, la probabilité d’obtenir des faux positifs est relativement inférieure à celle en cas d’utilisation d’autres agents de blocage du courrier indésirable. Par exemple, l'agent de filtrage du contenu est un agent de blocage du courrier indésirable qui s'appuie sur de nombreuses variables différentes pour déterminer si un message est du courrier indésirable.

Il n'existe que deux scénarios dans lesquels les messages légitimes peuvent être rejetés par l'agent de filtrage des expéditeurs :

  - Si vous commettez une erreur de saisie d’adresse de messagerie ou de nom de domaine, il se peut alors que l’expéditeur mal saisi soit bloqué.

  - Si un nom de domaine est réenregistré auprès d'une société légitime après l'ajout du domaine à la liste des expéditeurs bloqués, vous bloquez alors involontairement les messages légitimes.

Dans l'un ou l'autre de ces cas, il est recommandé de rejeter les messages.

