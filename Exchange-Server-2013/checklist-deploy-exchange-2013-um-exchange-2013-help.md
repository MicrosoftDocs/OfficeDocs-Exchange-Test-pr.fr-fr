---
title: 'Liste de contrôle : déploiement de la MU Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Liste de contrôle : déploiement de la messagerie unifiée Exchange 2013'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52062980
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Liste de contrôle : déploiement de la messagerie unifiée Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Cette liste de contrôle vous permet d'installer et de déployer la messagerie unifiée dans votre organisation.

Avant de commencer à utiliser cette liste de contrôle, familiarisez-vous avec les concepts présentés dans :

  - [Messagerie unifiée](unified-messaging-exchange-2013-help.md)

  - [Nouvelles fonctionnalités de messagerie vocale](new-voice-mail-features-exchange-2013-help.md)

  - [Planification de la messagerie unifiée](planning-for-unified-messaging-exchange-2013-help.md)

Pour obtenir un guide détaillé sur le déploiement de la messagerie unifiée et Microsoft Lync Server, consultez la rubrique [Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Liste de contrôle pour le déploiement de la messagerie unifiée


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Actions</th>
<th>Tâches</th>
<th>Rubrique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Déploiement et configuration des composants de téléphonie</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Connecter la messagerie unifiée pour votre système téléphonique</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Consulter la configuration système requise avant de procéder à l'installation d'Exchange 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Vérifier que vous satisfaites aux conditions requises pour l'installation.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Installer les serveurs d'accès au client et les serveurs de boîtes aux lettres requis.</p>

> [!WARNING]  
> Vous devez déployer au moins un serveur de boîtes aux lettres Exchange 2013 dans votre organisation avant de configurer les passerelles VoIP ou les PBX IP pour envoyer le trafic SIP ou RTP de messagerie unifiée vers les serveurs d’accès client Exchange 2013.

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Vérifier l'installation et consulter les journaux d'installation du serveur.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Si nécessaire, installer les modules linguistiques de messagerie unifiée requis.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Installer un module linguistique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Créer le nombre de plans de numérotation nécessaire pour votre organisation.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">Créer un plan de numérotation de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer le paramètre de sécurité du plan de numérotation.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-voip-security-setting">Configuration du paramètre de sécurité VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Configurer le mode de démarrage de messagerie unifiée pour les serveurs d'accès au client et de boîtes aux lettres.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configuration du mode de démarrage sur un serveur de boîtes aux lettres</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurer le mode de démarrage sur un serveur d'accès au Client</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer le nombre d'appels simultanés sur vos serveurs de boîtes aux lettres.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurer les numéros et d'autres paramètres d'Outlook Voice Access.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-dial-plan">Gestion d'un plan de numérotation de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer la numérotation sortante pour la messagerie unifiée.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-using-dialing-rules">Autorisation des appels utilisant des règles de numérotation</a></p>
<p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-users-in-a-dial-plan">Autoriser les appels destinés aux utilisateurs dans un plan de numérotation</a></p>
<p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-a-group-of-users">Autoriser les appels pour un groupe d'utilisateurs</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Créer le nombre requis de standards automatiques.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant">Créer un standard automatique de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Installer et configurer tous les standards automatiques de messagerie unifiée.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/set-up-um-auto-attendant">Configurer un standard automatique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Créer, importer et activer un nouveau certificat Exchange pour la messagerie unifiée ou activer un certificat tiers mutuellement approuvé. Importer également le certificat sur l'ensemble des passerelles VoIP, des PBX IP et des contrôleurs SBC.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Redémarrer le service de messagerie unifiée Microsoft Exchange et le service de routeur des appels de messagerie unifiée sur tous les serveurs Exchange pour charger les certificats requis.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Arrêt du service de messagerie unifiée Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Démarrage du service de messagerie unifiée Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Arrêtez le service Microsoft Exchange Unified Messaging routeur d'appels</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Démarrage du service routeur d'appels de messagerie unifiée Microsoft Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Créer une stratégie de boîte aux lettres de messagerie unifiée ou configurer la stratégie de boîte aux lettres de messagerie unifiée par défaut.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy">Créer une stratégie de boîte aux lettres de messagerie unifiée</a></p>
<p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">Gérer une stratégie de boîte aux lettres de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Activer la messagerie unifiée pour les utilisateurs avec un numéro d'extension et un numéro E.164 si nécessaire.</p></td>
<td><p><a href="https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">Activation de la messagerie vocale pour un utilisateur</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Activer les télécopies entrantes (facultatif).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">Activation de la réception de télécopies pour les utilisateurs de messagerie vocale</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Installer la messagerie vocale protégée (facultatif).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Protéger la messagerie vocale</a></p></td>
</tr>
</tbody>
</table>


Retour au début

