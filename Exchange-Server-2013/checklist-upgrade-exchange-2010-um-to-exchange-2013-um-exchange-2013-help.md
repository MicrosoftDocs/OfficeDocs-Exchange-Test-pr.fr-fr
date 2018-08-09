---
title: 'Liste de ctrl : màn de MU Exchange 2010 vers vrs de 2013: Exchange 2013 Help'
TOCTitle: "Liste de contrôle : mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013"
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54652765
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Liste de contrôle : mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez cette liste de vérification lors de la mise à niveau de la messagerie unifiée Exchange 2010 vers Exchange 2013. Veillez à vous référer à ces informations lors de la mise à niveau de votre organisation Exchange 2010 et de votre déploiement de messagerie unifiée vers Exchange 2013. Pour obtenir des instructions détaillées sur la mise à niveau vers la messagerie unifiée Exchange 2013, consultez la rubrique [Mise à niveau de la messagerie unifiée d'Exchange 2010 vers celle d'Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md).

Avant de commencer à utiliser cette liste de vérification, familiarisez-vous avec les concepts présentés dans :

  - [Planification de la messagerie unifiée](planning-for-unified-messaging-exchange-2013-help.md)

  - [Intégration des systèmes téléphoniques à la messagerie unifiée](telephone-system-integration-with-um-exchange-2013-help.md)

  - [Connexion de votre système de messagerie vocale à votre réseau téléphonique](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)

Pour obtenir des conseils détaillés sur la mise à niveau de la messagerie unifiée Exchange 2007 vers Exchange 2013, consultez la rubrique [Mise à niveau de la messagerie unifiée d’Exchange 2007 vers celle d’Exchange 2013](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md).

## Liste de vérification pour la mise à niveau de la messagerie unifiée Exchange 2010 vers Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Tâches</th>
<th>Rubrique</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Déployer et configurer des composants de téléphonie</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Connecter la messagerie unifiée pour votre système téléphonique</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Consulter la configuration système requise avant de procéder à l’installation d’Exchange 2013</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Vérifier que vous remplissez les conditions requises pour l’installation</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Installer les serveurs d’accès au client et les serveurs de boîtes aux lettres requis</p>
> [!WARNING]
> Vous devez déployer au moins un serveur de boîtes aux lettres Exchange 2013 dans votre organisation avant de configurer les passerelles VoIP ou les PBX IP pour envoyer le trafic SIP ou RTP de messagerie unifiée vers les serveurs d’accès client Exchange 2013.

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Vérifier l’installation et consulter les journaux d’installation du serveur</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Si nécessaire, installer les modules linguistiques de messagerie unifiée requis</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Installer un module linguistique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Déplacer la boîte aux lettres système Exchange 2010 utilisée pour les messages personnalisés de la messagerie unifiée vers Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a></p>
> [!NOTE]
> Si la boîte aux lettres système a déjà été déplacée, vous pouvez toujours importer/exporter manuellement les messages personnalisés à partir d’Exchange 2010 à l’aide de la page <a href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">Importer et exporter des invites, des annonces, des menus et des messages d’accueil personnalisés</a>.

</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exporter et importer des certificats</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">Déploiement de certificats pour la messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurer le mode de démarrage de messagerie unifiée sur tous les serveurs d’accès au client Exchange 2013</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurer le mode de démarrage sur un serveur d'accès au Client</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer le mode de démarrage de messagerie unifiée sur tous les serveurs de boîtes aux lettres Exchange 2013</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configuration du mode de démarrage sur un serveur de boîtes aux lettres</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Créer ou configurer des plans de numérotation de messagerie unifiée</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Créer un plan de numérotation de messagerie unifiée</a></p>
<p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gestion d'un plan de numérotation de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Créer ou configurer des passerelles IP de messagerie unifiée</p></td>
<td><p><a href="create-a-um-ip-gateway-exchange-2013-help.md">Créer une passerelle IP de messagerie unifiée</a></p>
<p><a href="manage-a-um-ip-gateway-exchange-2013-help.md">Gestion d'une passerelle IP de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Créer un groupement de postes de messagerie unifiée</p></td>
<td><p><a href="create-a-um-hunt-group-exchange-2013-help.md">Créer un groupement de postes de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Créer ou configurer des standards automatiques de messagerie unifiée</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Créer un standard automatique de messagerie unifiée</a></p>
<p><a href="manage-a-um-auto-attendant-exchange-2013-help.md">Gérer un standard automatique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Créer ou configurer des stratégies de boîte aux lettres de messagerie unifiée</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Créer une stratégie de boîte aux lettres de messagerie unifiée</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Gérer une stratégie de boîte aux lettres de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Déplacer les boîtes aux lettres à extension de messagerie unifiée existantes vers Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Déplacements de boîtes aux lettres dans Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Activer de nouveaux utilisateurs pour la messagerie unifiée ou configurer des paramètres pour un utilisateur à extension messagerie unifiée existant</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Activation de la messagerie vocale pour un utilisateur</a></p>
<p><a href="manage-voice-mail-settings-for-a-user-exchange-2013-help.md">Gestion des paramètres de messagerie vocale d'un utilisateur</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer vos passerelles VoIP, PBX IP et PBX compatibles SIP pour envoyer tous les appels entrants aux serveurs d’accès au client Exchange 2013</p></td>
<td><p><a href="configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md">Notes de configuration pour les passerelles VoIP, les PBX IP et les PBX pris en charge</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">Connexion d’une passerelle VoIP, d’un IP PBX ou d’un contrôleur SBC à la messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Désactiver la prise d’appels sur les serveurs de messagerie unifiée Exchange 2010</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">Désactiver la messagerie unifiée dans Exchange 2010</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Supprimer un serveur de messagerie unifiée Exchange 2010 d’un plan de numérotation</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">Supprimer un serveur de messagerie UNIFIÉE à partir d’un Plan de numérotation</a></p></td>
</tr>
</tbody>
</table>

