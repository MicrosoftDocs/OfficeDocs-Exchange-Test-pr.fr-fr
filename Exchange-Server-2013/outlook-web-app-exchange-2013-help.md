---
title: 'Outlook Web App: Exchange 2013 Help'
TOCTitle: Outlook Web App
ms:assetid: 3814b665-01e8-4881-9a44-163f14789ee4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657718(v=EXCHG.150)
ms:contentKeyID: 50477889
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Découvrez Outlook Web App, autrement connu sous le nom Outlook Web Access dans les versions de Microsoft Exchange antérieures à 2010. Cet article fournit un vue d’ensemble rapide, ainsi que des liens vers des informations utiles.

Par défaut, lorsque vous installez MicrosoftExchange 2013, vous activez Outlook Web App. MicrosoftOutlook Web App permet aux utilisateurs d’accéder à leurs boîtes aux lettres Exchange à partir de presque tous les navigateurs Web.

Le rôle de serveur d’accès au client fournit des services de proxy et de redirection pour Outlook Web App.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook Web App était appelé Outlook Web Access dans les versions d’Microsoft Exchange antérieures à Exchange 2010.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les nouvelles fonctionnalités, consultez la rubrique [Nouveautés d'Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md). Pour plus d’informations sur le rôle serveur d’accès au client dans Exchange 2013, consultez la rubrique [Serveur d’accès au client](client-access-server-exchange-2013-help.md).

## Vue d’ensemble d’Outlook Web App

Les navigateurs Web pris en charge donnent aux utilisateurs un accès à des fonctionnalités telles que l’afficheur de conversation, les règles de boîte de réception, le volet de lecture et l’Assistant Planification. Les navigateurs qui ne sont pas entièrement pris en charge peuvent toujours être utilisés, mais les utilisateurs ne voient que la version allégée de Outlook Web App qui propose moins de fonctionnalités. Pour plus d’informations sur les nouvelles fonctionnalités dans Outlook Web App, consultez la rubrique [Nouveautés Outlook Web App dans Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

## Gestion d’Outlook Web App

Dans Exchange 2013, les tâches de gestion les plus courantes d’Outlook Web App peuvent être accomplies dans le Centre d’administration Exchange (CAE). Toutes ces tâches, entre autres, peuvent être accomplies avec l’environnement de ligne de commande Exchange Management Shell. Vous utiliserez toujours des outils tels que le Gestionnaire des services IIS pour certaines tâches, comme, par exemple, la configuration de SSL (Secure Sockets Layer) ou l’établissement d’URL simples pour les utilisateurs.

## Accès à Outlook Web App

Vos utilisateurs et vous-même pouvez vous connecter à Outlook Web App en utilisant une URL semblable à celle-ci : **https://\<nom de domaine\>/OWA** ou **https://mail.\<nom de domaine\>/OWA**

Si, par exemple, le domaine de votre organisation est contoso.com, utilisez https://contoso.com/OWA ou https://mail.contoso.com/OWA. Pour plus d’informations sur l’accès à Outlook Web App, cliquez [ici](https://support.microsoft.com/fr-fr/kb/2897680). Pour modifier l’URL de connexion ou pour forcer la redirection vers SSL, reportez-vous à [Simplification de l'URL d'Outlook Web App](simplify-the-outlook-web-app-url-exchange-2013-help.md).

Si vous utilisez Exchange Online ou Office 365 pour la messagerie électronique, vous et vos utilisateurs pouvez accéder à Outlook Web App à l’aide de l’URL **outlook.office365.com/owa** ou en [cliquant ici](http://go.microsoft.com/fwlink/p/?linkid=402333). Pour en savoir plus, reportez-vous à [Se connecter à Outlook Web App](http://go.microsoft.com/fwlink/p/?linkid=511341) et [Où se connecter à Office 365](http://go.microsoft.com/fwlink/p/?linkid=522691).

