﻿---
title: 'Routage de transport dans les déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Routage de transport dans les déploiements hybrides Exchange
ms:assetid: 36c2cea3-2e2f-40ac-88bd-7e1b6bd27828
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659050(v=EXCHG.150)
ms:contentKeyID: 50479674
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Routage de transport dans les déploiements hybrides Exchange

 

_<strong>Sapplique à :</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-07-29_

Cette rubrique traite des options de routage dont vous disposez pour les messages entrants en provenance d'Internet et les messages sortant vers Internet.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ne placez aucun serveur, service ou périphérique entre vos serveurs Exchange locaux et Office 365 traitant ou modifiant le trafic SMTP. Le flux de messagerie sécurisée entre votre organisation Exchange locale et Office 365 dépend des informations contenues dans les messages envoyés au sein de l’organisation. Les pare-feu autorisant le trafic SMTP sur le port TCP 25 sans modification sont pris en charge. Si un serveur, un service ou un périphérique traite un message envoyé entre votre organisation Exchange locale et Office 365, ces informations sont supprimées. Dans ce cas, le message n’est plus considéré comme interne à votre organisation et est soumis à un filtrage anti-courrier indésirable, aux règles de journal et de transport, ainsi qu’à d’autres stratégies ne s’appliquant normalement pas à celui-ci.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les exemples contenus dans cette rubrique n’incluent pas l’ajout de serveurs de transport Edge dans le déploiement hybride. Les itinéraires empruntés par les messages entre l’organisation locale, l’organisation Exchange Online et Internet ne changent pas avec l’ajout d’un serveur de transport Edge. Seul le routage au sein de l’organisation locale change. Pour plus d’informations sur l’ajout de serveurs de transport Edge à un déploiement hybride, consultez la rubrique <a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Serveurs de transport Edge avec déploiements hybrides</a>.</td>
</tr>
</tbody>
</table>


## Messages entrants en provenance d'Internet

Lors de la planification et de la configuration de votre déploiement hybride, vous devez déterminer si vous souhaitez acheminer tous les messages provenant d’expéditeurs Internet via Exchange Online ou via votre organisation locale. Tous les messages provenant d’expéditeurs Internet seront initialement remis à l’organisation que vous aurez sélectionnée, puis acheminés selon l’emplacement de la boîte aux lettres du destinataire. La décision d’acheminer les messages via Exchange Online ou via votre organisation locale dépend de divers facteurs, parmi lesquels l’application de stratégies de conformité à tous les messages envoyés aux deux organisations, le nombre de boîtes aux lettres dans chaque organisation, etc.

L’itinéraire emprunté par les messages envoyés aux destinataires de votre organisation locale et de votre organisation Exchange Online varie selon la manière dont vous décidez de configurer votre enregistrement MX dans votre déploiement hybride. Nous vous recommandons de le configurer pour qu’il pointe vers Exchange Online Protection (EOP) dans Office 365, car cette configuration garantit un filtrage du courrier indésirable extrêmement précis. L’assistant Configuration hybride ne configure pas le routage pour les messages Internet entrants d’une organisation locale ou Exchange Online. Vous devez configurer manuellement votre enregistrement MX si vous souhaitez modifier la manière dont vos messages Internet entrants sont remis.

  - **Si vous modifiez votre enregistrement MX pour qu’il pointe vers le service Exchange Online Protection dans Office 365**   Nous vous recommandons cette configuration pour les déploiements hybrides. Tous les messages envoyés à un destinataire dans l’une des deux organisations seront d’abord acheminés via l’organisation Exchange Online. Un message adressé à un destinataire situé dans votre organisation locale sera d’abord acheminé via l’organisation Exchange Online, puis remis au destinataire de votre organisation locale. Cet itinéraire est recommandé si votre organisation Exchange Online compte un plus grand nombre de destinataires que votre organisation locale. Cette option de configuration est requise pour qu’Exchange Online Protection puisse analyser et bloquer les courriers indésirables.

  - **Si vous décidez de conserver votre enregistrement MX pointant vers votre organisation locale**   Tous les messages envoyés à un destinataire d’une des deux organisations seront d’abord acheminés via votre organisation locale. Un message adressé à un destinataire situé dans Exchange Online sera d’abord acheminé via votre organisation locale, puis remis au destinataire dans Exchange Online. Cet itinéraire peut être utile aux organisations appliquant des stratégies de conformité qui exigent que les messages envoyés depuis ou vers une organisation soient examinés par une solution de journalisation. Si vous choisissez cette option, Exchange Online Protection ne pourra pas analyser les courriers indésirables de manière efficace.

Pour plus d’informations, voir [Meilleures pratiques en matière de flux de messagerie pour Exchange Online et Office 365 (aperçu)](https://technet.microsoft.com/fr-fr/library/jj937232\(v=exchg.150\)).

Lisez la section ci-dessous correspondant au mode d’acheminement souhaité pour les messages envoyés par des destinataires Internet à vos destinataires locaux et Exchange Online. Dans chacune des sections, le « serveur Exchange local » peut être un serveur d’accès au client Exchange 2013 ou un serveur de boîtes aux lettres Exchange 2016.

## Acheminer les messages Internet entrants via l'organisation Exchange Online

Les étapes et le schéma qui suivent illustrent l'itinéraire que les messages Internet entrants emprunteront dans votre déploiement hybride si vous décidez de modifier votre enregistrement MX pour désigner le service EOP dans l'organisation Office 365. L'itinéraire des messages diffère selon que vous choisissez ou non d'activer le transport de courrier centralisé.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151301.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous devrez éventuellement acheter des licences EOP pour chaque boîte aux lettres locale qui reçoit des messages d'abord remis à EOP, puis acheminés via l'organisation Exchange Online. Pour de plus amples informations, contactez votre distributeur Microsoft.</td>
</tr>
</tbody>
</table>


Lorsque le transport de courrier centralisé est **désactivé** (configuration par défaut), les messages Internet entrants sont acheminés comme suit dans un déploiement hybride :

1.  Un message entrant est envoyé par un expéditeur Internet aux destinataires julie@contoso.com et david@contoso.com. La boîte aux lettres de Julie se trouve sur un serveur de boîtes aux lettres Exchange dans l’organisation locale. La boîte aux lettres de David se situe dans Exchange Online.

2.  Comme les deux destinataires ont contoso.com dans leur adresse de messagerie et que l’enregistrement MX de contoso.com désigne EOP, le message est remis à EOP.

3.  EOP achemine les messages des deux destinataires vers Exchange Online.

4.  Exchange Online analyse les messages pour détecter d’éventuels virus et effectue une recherche pour chaque destinataire. Au cours de la recherche, il détermine que la boîte aux lettres de Julie est située dans l’organisation locale, alors que celle de David se trouve dans l’organisation Exchange Online.

5.  Exchange Online divise le message en deux exemplaires. Un exemplaire du message est remis à la boîte aux lettres de David.

6.  Le deuxième exemplaire est renvoyé de Exchange Online à EOP.

7.  EOP envoie le message à un serveur Exchange local dans l’organisation locale.

8.  Un élément Exchange envoie le message au serveur de boîtes aux lettres Exchange local, où il est remis dans la boîte aux lettres de Julie.

**Routage du courrier électronique via l’organisation Exchange Online pour les deux organisations, locale et Exchange Online, avec transport de courrier centralisé désactivé (configuration par défaut)**

![Entrant centralisé vers EXO](images/JJ659050.f98341e0-088d-49f0-bf8e-09f35255bf9e(EXCHG.150).png "Entrant centralisé vers EXO")

Lorsque le transport de courrier centralisé est **activé**, les messages Internet entrants sont acheminés comme suit dans un déploiement hybride :

1.  Un message entrant est envoyé par un expéditeur Internet aux destinataires julie@contoso.com et david@contoso.com. La boîte aux lettres de Julie se trouve sur un serveur de boîtes aux lettres Exchange dans l’organisation locale. La boîte aux lettres de David se situe dans Exchange Online.

2.  Comme les deux destinataires ont contoso.com dans leur adresse de messagerie et que l’enregistrement MX de contoso.com désigne EOP, le message est remis à EOP et analysé pour détecter d’éventuels virus.

3.  Étant donné que le transport de courrier centralisé est activé, EOP achemine les messages des deux destinataires vers un serveur Exchange local.

4.  Le serveur Exchange local exécute une recherche pour chaque destinataire. Au cours de la recherche, il détermine que la boîte aux lettres de Julie est située dans l’organisation locale, alors que celle de David se trouve dans l’organisation Exchange Online.

5.  Le serveur Exchange local divise le message en deux exemplaires. Un exemplaire du message est envoyé à la boîte aux lettres de Julie sur le serveur de boîtes aux lettres Exchange local.

6.  Le deuxième exemplaire est renvoyé du serveur Exchange local à EOP.

7.  EOP envoie le message à Exchange Online.

8.  Exchange remet le message à la boîte aux lettres de David.

**Acheminer le courrier électronique via l'organisation Exchange Online pour les deux organisations, locale et Exchange Online, avec transport de courrier centralisé activé**

![EXO entrant, centralisation activée](images/JJ659050.062422d5-9cb6-42c2-9ec0-31962cd7ada6(EXCHG.150).png "EXO entrant, centralisation activée")

## Acheminer les messages Internet entrants dans votre organisation locale

Les étapes et le schéma qui suivent illustrent l’itinéraire que les messages Internet entrants emprunteront dans votre déploiement hybride si vous décidez de conserver votre enregistrement MX désignant votre organisation locale.

1.  Un message entrant est envoyé par un expéditeur Internet aux destinataires julie@contoso.com et david@contoso.com. La boîte aux lettres de Julie se trouve sur un serveur de boîtes aux lettres Exchange dans l’organisation locale. La boîte aux lettres de David se situe dans Exchange Online.

2.  Comme les deux destinataires ont contoso.com dans leur adresse de messagerie et que l’enregistrement MX de contoso.com désigne l’organisation locale, le message est remis à un serveur Exchange local.

3.  Le serveur Exchange local effectue une recherche pour chaque destinataire utilisant un serveur de catalogue global local. Par une recherche dans le catalogue global, il détermine que la boîte aux lettres de Julie est située sur un serveur de boîtes aux lettres Exchange local alors que la boîte aux lettres de David se trouve dans l’organisation Exchange Online et dispose d’une adresse de routage hybride david@contoso.mail.onmicrosoft.com.

4.  Le serveur Exchange local divise le message en deux exemplaires. Un exemplaire du message est envoyé au serveur de boîtes aux lettres Exchange local, où il est remis à la boîte aux lettres de Julie.

5.  Le deuxième exemplaire du message est envoyé par le serveur Exchange local à EOP, qui reçoit des messages envoyés à l’organisation Exchange Online, à l’aide d’un connecteur d’envoi configuré pour utiliser TLS.

6.  EOP envoie le message à l’organisation Exchange Online, dans laquelle le message est analysé pour détecter d’éventuels virus avant d’être remis à la boîte aux lettres de David.

**Routage du courrier électronique via l’organisation locale pour les deux organisations, locale et Exchange Online**

![Courrier entrant centralisé, sur site](images/JJ659050.a246a1e2-7593-4d13-9426-73622a545c9a(EXCHG.150).png "Courrier entrant centralisé, sur site")

## Messages sortants vers Internet

Outre le choix du mode de routage des messages entrants adressés aux destinataires de vos organisations, vous pouvez également choisir la manière dont les messages sortants envoyés par des destinataires Exchange Online sont acheminés. Lorsque vous lancez l’assistant Configuration hybride, vous avez le choix entre les deux options suivantes :

  - **Ne pas activer le transport de courrier centralisé**   Sélectionnée par défaut dans l’assistant Configuration hybride, cette option achemine des messages sortants envoyés par l’organisation Exchange Online directement vers Internet. Utilisez cette option si vous n’avez pas besoin d’appliquer de stratégies de conformité locales ou d’autres règles de traitement aux messages qui sont envoyés par les destinataires de l’organisation Exchange Online.

  - **Activer le transport de courrier centralisé**   Cette option achemine les messages sortants envoyés par l’organisation Exchange Online via votre organisation locale. À l’exception des messages envoyés à d’autres destinataires de la même organisation Exchange Online, tous les messages provenant de destinataires de l’organisation Exchange Online sont envoyés via l’organisation locale. Cela vous permet d’appliquer des règles de conformité à ces messages et tout autre processus ou exigence applicable à tous vos destinataires, qu’ils concernent l’organisation Exchange Online ou l’organisation locale.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le transport de courrier centralisé est recommandé uniquement pour les organisations qui présentent des besoins de transport spécifiques liés à la conformité. Nous recommandons aux organisations Exchange types de ne pas activer le transport de courrier centralisé.</td>
    </tr>
    </tbody>
    </table>


Les messages provenant de destinataires locaux sont toujours envoyés directement à des destinataires Internet via le DNS, quelle que soit l'option sélectionnée dans l'Assistant Configuration hybride.

Les étapes et le schéma qui suivent illustrent l’itinéraire emprunté par les messages sortants envoyés par des destinataires locaux.

1.  Julie, qui dispose d’une boîte aux lettres sur le serveur de boîtes aux lettres Exchange local, envoie un message à un destinataire Internet externe, erin@cpandl.com.

2.  Le serveur Exchange consulte l’enregistrement MX de cpandl.com et envoie le message aux serveurs de messagerie cpandl.com situés sur Internet.

**Messages envoyés par des expéditeurs locaux à des destinataires Internet**

![Messages sortants à partir d’une organisation sur site](images/JJ659050.71f287d6-b814-4820-a0dc-575f17d13894(EXCHG.150).png "Messages sortants à partir d’une organisation sur site")

Lisez la section ci-dessous correspondant au mode d'acheminement souhaité pour les messages envoyés par des destinataires de l'organisation Exchange Online à des destinataires Internet.

## Remise de messages Internet sortants à partir de l’organisation Exchange Online à l’aide de DNS (transport de courrier centralisé désactivé)

Les étapes et le schéma suivants illustrent l'itinéraire emprunté par les messages sortants envoyés par des destinataires Exchange Online à un destinataire Internet lorsque l'option **Activer le transport de courrier centralisé** n'est pas sélectionnée dans l'Assistant Configuration hybride, correspondant à la configuration par défaut.

1.  David, qui dispose d’une boîte aux lettres dans l’organisation Exchange Online, envoie un message à un destinataire Internet externe, erin@cpandl.com.

2.  Exchange Online analyse le message pour détecter d’éventuels virus, puis l’envoie à la société EOP Exchange Online.

3.  EOP consulte l’enregistrement MX de cpandl.com et envoie le message aux serveurs de messagerie cpandl.com situés sur Internet.

**Courrier électronique d'expéditeurs Exchange Online directement acheminé vers Internet avec le transport de courrier centralisé désactivé (configuration par défaut)**

![Messages sortants directs EXO](images/JJ659050.fe1c4241-0d6e-47bf-b61d-5af732d2dbbc(EXCHG.150).png "Messages sortants directs EXO")

## Acheminer les messages Internet entrants et sortants d’Exchange Online via votre organisation locale (transport de courrier centralisé activé)

Les étapes et le schéma suivants illustrent l'itinéraire emprunté par les messages sortants envoyés par des destinataires Exchange Online à un destinataire Internet lorsque vous sélectionnez l'option **Activer le transport de courrier centralisé** dans l'Assistant Configuration hybride.

1.  David, qui dispose d'une boîte aux lettres dans l'organisation Exchange Online, envoie un message à un destinataire Internet externe, erin@cpandl.com.

2.  Exchange Online analyse le message pour détecter d'éventuels virus, puis l'envoie à EOP.

3.  EOP est configuré pour envoyer tous les messages Internet entrants et sortants à un serveur local de sorte que le message soit acheminé vers un serveur Exchange local. Le message est envoyé à l’aide de TLS.

4.  Le serveur Exchange local effectue une analyse de conformité, une recherche de virus et tout autre processus configuré par l’administrateur, sur le message de David.

5.  Le serveur Exchange local consulte l’enregistrement MX de cpandl.com et envoie le message aux serveurs de messagerie cpandl.com situés sur Internet.

**Courrier électronique d’expéditeurs Exchange Online acheminé via l’organisation locale avec transport de courrier centralisé activé**

![Messages EXO sortants via une organisation sur site](images/JJ659050.7ea9ffee-944b-45ae-ba4d-c3484100399b(EXCHG.150).png "Messages EXO sortants via une organisation sur site")

