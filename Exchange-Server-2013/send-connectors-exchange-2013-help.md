---
title: "Connecteurs d'envoi: Exchange 2013 Help"
TOCTitle: Connecteurs d'envoi
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50478367
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connecteurs d'envoi

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-15_

Dans Microsoft Exchange Server 2013, un connecteur d’envoi contrôle le flux des messages sortants vers le serveur de réception. Ils sont configurés sur les serveurs de boîtes aux lettres exécutant le service de transport. Le plus souvent, vous configurez un connecteur d’envoi pour envoyer les messages électroniques sortants vers un hôte actif ou directement vers leur destinataire, via DNS.

Les serveurs de boîtes aux lettres Exchange 2013 qui exécutent le service de transport requièrent des connecteurs d’envoi pour remettre les messages au prochain saut sur le chemin de leur destination. Les connecteurs d’envoi créés sur les serveurs de boîtes aux lettres sont stockés dans Active Directory et sont disponibles pour tous les serveurs de boîtes aux lettres exécutant le service de transport dans l’organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous déployez Exchange 2013, le flux de messagerie sortant ne peut pas être mis en œuvre tant que vous n’avez pas configuré un connecteur d’envoi pour router les messages sortants vers Internet. Pour plus d’informations, voir <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Créer un connecteur d’envoi pour les messages électroniques envoyés vers Internet</a>.</td>
</tr>
</tbody>
</table>


## Sélection du type pour un connecteur d’envoi

Généralement, vous créez un connecteur d’envoi dans la section **Flux de messagerie** du Centre d’administration Exchange. Lorsque vous créez un nouveau connecteur d’envoi, vous choisissez le **Type** disponible approprié à votre scénario de connexion. Le type détermine les ensembles d’autorisations par défaut affectés au connecteur et accorde ces autorisations aux principaux de sécurité approuvés. Les principaux de sécurité incluent des utilisateurs, des ordinateurs et des groupes de sécurité.

Les procédures qui expliquent les sélections d’un **Type** spécifique sont [Créer un connecteur d’envoi pour router le courrier sortant via un hôte actif](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) et [Créer un connecteur d’envoi pour envoyer un courrier électronique à un partenaire, avec le protocole TLS (TLS)](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md).

Si vous préférez utiliser le Exchange Management Shell à la place du Centre d’administration Exchange, vous pouvez créer un connecteur d’envoi et spécifier un type à l’aide de la cmdlet [New-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998936\(v=exchg.150\)).

## Fonctions du nouveau connecteur d’envoi dans Exchange 2013

Grâce à la relation entre le service de transport frontal sur les serveurs d’accès au client et le service de transport sur ​​les serveurs de boîtes aux lettres dans Exchange 2013, un nouveau comportement est disponible pour les connecteurs d’envoi. Tout d’abord, vous pouvez définir un connecteur d’envoi dans le service de transport d’un serveur de boîtes aux lettres pour qu’il route les messages sortants via un serveur de transport frontal sur le site Active Directory local, au moyen du paramètre *FrontEndProxyEnabled* de la cmdlet [Set-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998294\(v=exchg.150\)), ce qui consolide la façon dont les messages sont routés à partir du service de transport. [Routage du courrier](mail-routing-exchange-2013-help.md) fournit davantage d’informations sur les services de transport, le comportement de routage et les destinations dans Exchange 2013. [Flux de messagerie](mail-flow-exchange-2013-help.md) offre un aperçu du pipeline de transport et des descriptions de chaque service de transport.

Le paramètre *IsCoexistenceConnector* est obsolète. Dans la plupart des cas, lorsque vous souhaitez configurer un environnement hybride dans lequel une partie de vos boîtes aux lettres est hébergée localement et une autre partie est hébergée dans le nuage, nous vous recommandons d’utiliser l’Assistant de configuration hybride.

*LinkedReceiveConnector* est obsolète. Ce paramètre était utilisé pour créer les connecteurs pouvant router les messages vers un service tiers de blocage du courrier indésirable, par exemple. Aujourd’hui, dans la plupart des cas, vous routez les messages vers votre service de blocage du courrier indésirable au moyen de votre enregistrement MX, et le comportement de connecteur lié n’est pas nécessaire.

La taille de message maximale par défaut, spécifiée par le paramètre *MaxMessageSize*, a été augmentée de 10 Mo à 25 Mo. [Set-SendConnector](https://technet.microsoft.com/fr-fr/library/aa998294\(v=exchg.150\)) fournit davantage d’informations sur la façon de définir les paramètres sur un connecteur d’envoi.

*TlsCertificateName* a été ajouté. Il permet d’authentifier le certificat local à utiliser pour les connexions sortantes et de diminuer le risque de certificats frauduleux.

