---
title: 'Connecteurs étrangers: Exchange 2013 Help'
TOCTitle: Connecteurs étrangers
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50477755
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connecteurs étrangers

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-09-25_

Un connecteur étranger remet des messages à un serveur ou un système étranger qui n’utilise pas SMTP comme mécanisme de transport principal. On peut citer en exemple un serveur de passerelle de télécopie. Un connecteur étranger utilise un répertoire de dépôt local ou partagé pour envoyer des messages sortants au système étranger en transférant des fichiers. Les connecteurs étrangers sont créés dans le service de transport d’un serveur de boîtes aux lettres Microsoft Exchange Server 2013.

Les serveurs de passerelle étrangers peuvent envoyer des messages dans l’organisation Exchange 2013 en utilisant les répertoires de collecte ou de relecture présents dans le service de transport d’un serveur de boîtes aux lettres. Les fichiers de messages électroniques correctement formatés que vous copiez dans chaque répertoire sont soumis à une boîte aux lettres Exchange en vue d’être remis.

> [!TIP]
> Dans la plupart des cas où vous devez communiquer des messages sortants à un système autre que SMTP, nous recommandons l’utilisation de connecteurs d’agent de remise, parce qu’ils permettent la gestion de file d’attente de messages, que les messages n’ont pas à être écrits dans le système de fichiers, et pour d’autres raisons avantageuses. La rubrique <a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agents de remise et connecteurs d’agent de remise</a> fournit de plus amples détails.


## Pour plus d'informations

[Créer un connecteur étranger pour remettre les messages vers une passerelle non-SMTP télécopie](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[Agents de remise et connecteurs d’agent de remise](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/fr-fr/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/fr-fr/library/bb123789\(v=exchg.150\))

