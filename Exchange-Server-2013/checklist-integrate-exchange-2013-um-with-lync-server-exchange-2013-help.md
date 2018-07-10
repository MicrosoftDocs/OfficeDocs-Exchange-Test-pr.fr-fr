---
title: "Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server: Exchange 2013 Help"
TOCTitle: "Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server"
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52062952
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez cette liste de contrôle pour installer et déployer la messagerie unifiée et Microsoft Lync Server 2013. Dans cette rubrique, « Lync Server » désigne également Lync Server 2010. Toutefois, Microsoft Office Communications Server 2007 R2 peut aussi être déployé à l'aide de la messagerie unifiée.

> [!NOTE]
> 


Avant de commencer à utiliser cette liste de vérification, familiarisez-vous avec les concepts présentés dans :

  - [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Coexistence avec Office Communications Server 2007 R2 et Lync Server](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Pour plus d’informations sur l’exécution des tâches à effectuer pour Lync Server, consultez la rubrique [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Liste de contrôle pour le déploiement de Microsoft Lync Server et de la messagerie unifiée


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
<td><p>Consulter la configuration système requise avant de procéder à l'installation d'Exchange Server 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Vérifier que vous satisfaites aux conditions requises pour l'installation.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Consulter la configuration requise pour l'intégration de Microsoft Lync Server 2013 et Microsoft Exchange Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Configuration requise pour l’intégration de Microsoft Lync Server 2013 et Microsoft Exchange Server 2013</a></p>
> [!TIP]
> Unified Communications Managed API (UCMA) 4.0 Runtime est requis pour Exchange 2013 et Lync Server 2010 et 2013. Il est installé au cours de l’installation. Pour télécharger et obtenir des informations sur UCMA 4.0, consultez la rubrique <a href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</a>

</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Installer les serveurs d'accès au client et les serveurs de boîtes aux lettres requis.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installer Exchange 2013 à l’aide de l’Assistant Installation</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Vérifier l’installation et consulter les journaux d’installation du serveur</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Vérifier une installation d’Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Si nécessaire, installer les modules linguistiques de messagerie unifiée requis.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Installer un module linguistique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Créer le nombre de plans de numérotation URI SIP nécessaires à votre organisation.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Créer un plan de numérotation de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer le paramètre de sécurité du plan de numérotation.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Configuration du paramètre de sécurité VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurer le nombre d'appels simultanés sur vos serveurs de boîtes aux lettres.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurer le nombre d'appels entrants sur un serveur de boîtes aux lettres</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer les numéros et d'autres paramètres d'Outlook Voice Access.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gestion d'un plan de numérotation de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Ajouter tous les serveurs d'accès au client et de boîtes aux lettres à chaque plan de numérotation URI SIP.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurer la numérotation sortante pour la messagerie unifiée Autoriser les appels sur les plans de numérotation URI SIP et les stratégies de boîte aux lettres de messagerie unifiée correspondantes.</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autoriser les appels destinés aux utilisateurs dans un plan de numérotation</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autoriser les appels pour un groupe d'utilisateurs</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Créer le nombre requis de standards automatiques.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Créer un standard automatique de messagerie unifiée</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Installer et configurer tous les standards automatiques de messagerie unifiée.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configurer un standard automatique de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Créer, importer et activer un nouveau certificat Exchange pour la messagerie unifiée ou activer un certificat tiers mutuellement approuvé.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Configurer le mode de démarrage de la messagerie unifiée Double ou TLS (Transport Layer Security) pour chaque serveur d'accès au client et de boîtes aux lettres.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configuration du mode de démarrage sur un serveur de boîtes aux lettres</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurer le mode de démarrage sur un serveur d'accès au Client</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Redémarrer le service de messagerie unifiée Microsoft Exchange et le service de routeur des appels de messagerie unifiée sur tous les serveurs Exchange pour charger les certificats requis.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Arrêt du service de messagerie unifiée Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Démarrage du service de messagerie unifiée Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Arrêtez le service Microsoft Exchange Unified Messaging routeur d'appels</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Démarrage du service routeur d'appels de messagerie unifiée Microsoft Exchange</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Créer une stratégie de boîte aux lettres de messagerie unifiée ou configurer la stratégie de boîte aux lettres de messagerie unifiée par défaut.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Créer une stratégie de boîte aux lettres de messagerie unifiée</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Gérer une stratégie de boîte aux lettres de messagerie unifiée</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Activer la messagerie unifiée pour les utilisateurs à l'aide d'une adresse SIP et les associer à un plan de numérotation URI SIP.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Activation de la messagerie vocale pour un utilisateur</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Consulter la documentation de planification de Lync Server 2013</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">Planification</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Installer et déployer Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Déploiement de Microsoft Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Importer le certificat PKI interne mutuellement approuvé ou le certificat tiers importé sur les serveurs de messagerie unifiée Exchange.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">Configuration des certificats pour les serveurs</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">Configurer les certificats sur le serveur exécutant la messagerie unifiée Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Si nécessaire, démarrer les services Lync sur les serveurs pour charger les certificats.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">Démarrage des services sur les serveurs</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Ouvrir l'environnement de ligne de commande Exchange Management Shell et exécuter le script exchucutil.ps1 situé dans le dossier %Program Files%\Microsoft\Exchange Server\V15\Scripts.</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Configurer la messagerie unifiée pour qu’elle fonctionne avec Lync Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Consulter la configuration requise pour Voix Entreprise.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Conditions préalables logicielles pour Voix Entreprise</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">Conditions préalables de configuration et de sécurité requises pour Voix Entreprise</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Déployer et configurer les passerelles multimédias ou les serveurs de médiation, puis définir les homologues.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">Déploiement des serveurs de médiation et définition des homologues</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurer une jonction entre un serveur de médiation et un ou plusieurs des homologues pour fournir une connectivité réseau téléphonique commuté (RTC).</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">Configuration de jonctions</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Créer et configurer un plan de numérotation Lync, puis créer, définir et associer des règles de normalisation.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">Configuration des plans de numérotation</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurer des stratégies de voix et définir l'utilisation du téléphone et les itinéraires d'appel sortant.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">Configuration des stratégies de voix, des enregistrements d’utilisation PSTN et des itinéraires des communications vocales</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exécuter l'utilitaire d'intégration Exchange (ocsumutil.exe) qui crée les objets contact pour Outlook Voice Access et les standards automatiques.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Configuration de Lync Server 2013 pour fonctionner avec la messagerie unifiée sur Microsoft Exchange Server</a>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Définir, configurer et déployer les fonctionnalités avancées Voix Entreprise requises.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">Déploiement des fonctionnalités avancées de Voix Entreprise</a>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Activer les utilisateurs pour Voix Entreprise. Entrer un URI de ligne, attribuer une stratégie de voix et un plan de numérotation Lync.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">Activer les utilisateurs pour Voix Entreprise</a></p></td>
</tr>
</tbody>
</table>

