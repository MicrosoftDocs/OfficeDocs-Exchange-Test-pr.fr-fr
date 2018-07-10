---
title: 'Assistant de configuration hybride: Exchange 2013 Help'
TOCTitle: Assistant de configuration hybride
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50479668
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Assistant de configuration hybride

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

Cette rubrique vous présente le processus de configuration de déploiement hybride Exchange, les fonctions et options de déploiement hybride dont vous disposez ainsi que le moteur de configuration hybride qui exécute les principales actions nécessaires à la fois à la configuration et la mise à jour d’un déploiement hybride.

Pour plus d’informations sur les déploiements hybrides, consultez la rubrique [Déploiements hybrides Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

**Table des matières**

Processus de configuration hybride

Fonctions de la configuration hybride

Options de configuration hybride

Moteur de configuration hybride

## Processus de configuration hybride

Voici une présentation rapide du processus de l’assistant Configuration hybride. Dans un premier temps, l’assistant crée l’objet **HybridConfiguration** dans votre Active Directory local. Cet objet Active Directory stocke les informations de configuration hybride pour le déploiement hybride, puis est mis à jour par l’assistant Configuration hybride. Dans un deuxième temps, l’assistant collecte les données de configuration topologiques locales d’Exchange et d’Active Directory, les données de configuration d’Exchange Online et de l’organisation cliente Office 365, définit plusieurs paramètres d’organisation, puis exécute un ensemble important de tâches de configuration à la fois dans l’organisation locale et l’organisation Exchange Online.

> [!IMPORTANT]
> Vous devez satisfaire plusieurs considérations et conditions préalables importantes avant d’utiliser l’assistant Configuration hybride. Vous devez satisfaire les exigences des déploiements hybrides décrites dans <a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Configuration requise pour un déploiement hybride</a>. Vous pourrez ensuite lancer l’assistant Configuration hybride pour configurer votre organisation Exchange pour le déploiement hybride.


Les phases générales du processus de configuration de déploiement hybride sont les suivantes :

1.  **Vérification des conditions préalables et contrôles de topologie**   L’assistant Configuration hybride vérifie que votre organisation locale et votre organisation Exchange Online peuvent prendre en charge un déploiement hybride. Voici quelques-uns des éléments que l’assistant vérifie et contrôle dans l’organisation locale et l’organisation Exchange Online :
    
      - Les versions des serveurs Exchange locaux
    
      - La version Exchange Online
    
      - La configuration et la présence de synchronisation d’Active Directory
    
      - Les domaines fédérés et acceptés
    
      - Les relations existantes d’organisation et de confiance de fédération
    
      - Les répertoires virtuels des services Web
    
      - Les certificats Exchange

2.  **Contrôle des informations d’identification des comptes**   Les comptes de gestion hybride Office 365 et locaux désignés accèdent à l’organisation locale et à l’organisation Exchange Online pour collecter des informations de vérification des conditions préalables et pour que les modifications de configuration des paramètres d’organisation activent la fonction de déploiement hybride. L’assistant Configuration hybride vérifie que les comptes disposent des informations d’identification appropriées et qu’ils peuvent se connecter à l’organisation locale et à l’organisation Exchange Online. Les comptes de gestion du déploiement hybride pour l’organisation locale et l’organisation Office 365 doivent faire partie du groupe de rôles Gestion de l’organisation pour que l’assistant Configuration hybride puisse mener à bien ces tâches.

3.  **Application de modifications de configuration du déploiement hybride**   Après avoir analysé les comptes de gestion hybride, vérifié et contrôlé la topologie, puis collecté les informations de configuration que vous avez définies dans le processus de l’assistant, l’assistant de configuration hybride applique les modifications de configuration pour créer et activer le déploiement hybride. Toutes les modifications apportées à la configuration hybride sont automatiquement consignées dans le journal de configuration hybride. Par défaut, le journal de configuration hybride se situe sur le serveur de boîtes aux lettres local à l’emplacement `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.
    
    > [!IMPORTANT]
    > Le flux de messagerie entrant est contrôlé par l’enregistrement MX de votre organisation. Les messages électroniques Internet entrants pour un déploiement hybride ne sont pas configurés par l’assistant Configuration hybride.


## Fonctions de la configuration hybride

L’Assistant Configuration hybride active automatiquement toutes les fonctions de déploiement hybride par défaut chaque fois qu’il est lancé. Si vous souhaitez désactiver des fonctions de configuration hybride spécifiques, vous devez utiliser l’Environnement de ligne de commande Exchange Management Shell et la cmdlet **Set-HybridConfiguration**. Les fonctions de déploiement hybride suivantes sont activées par défaut par l’Assistant :

  - **Partage de disponibilité**   La fonction de partage de disponibilité permet de partager les informations de calendrier entre les utilisateurs de l’organisation locale et de l’organisation Exchange Online. La fonction de partage de disponibilité est activée dans le cadre de la configuration des relations des organisations et du partage fédéré pour l’organisation locale et l’organisation Exchange Online. Pour plus d’informations, consultez la rubrique [Partage](https://technet.microsoft.com/fr-fr/library/dd638083\(v=exchg.150\)).

  - **Infos-courrier**   Les infos-courrier sont des messages d’information qui s’affichent lorsque les utilisateurs composent un message. En activant les infos-courrier dans le déploiement hybride, les expéditeurs locaux et Exchange Online peuvent adapter les messages qu’ils rédigent pour éviter des situations indésirables ou des rapports de non-remise entre les organisations. Pour plus d’informations, consultez la rubrique [MailTips](https://technet.microsoft.com/fr-fr/library/jj649091\(v=exchg.150\)).

  - **Archivage en ligne**   La fonction d’archivage en ligne permet à l’organisation Exchange Online d’héberger les archives de messages électroniques tant pour les utilisateurs locaux que pour ceux d’Exchange Online. Pour plus d’informations, consultez la rubrique [Configurer l’archivage Exchange Online](http://go.microsoft.com/fwlink/p/?linkid=266565).

  - **Redirection Outlook sur le web**   La fonction de redirection Outlook sur le web propose une seule URL commune pour accéder aux boîtes aux lettres locales et Exchange Online. Les serveurs Client Access redirigent automatiquement les demandes Outlook sur le web vers les serveurs de boîtes aux lettres locaux ou permettent aux utilisateurs d’accéder à leur boîte aux lettres dans l’organisation Exchange Online.

  - **Redirection Exchange ActiveSync**  Lorsque vous déplacez une boîte aux lettres de votre organisation Exchange locale vers Exchange Online, tous les clients qui accèdent à la boîte aux lettres doivent être mis à jour pour utiliser Exchange Online ; cela inclut les périphériques Exchange ActiveSync. La plupart des clients Exchange ActiveSync sont désormais automatiquement reconfigurés lorsque la boîte aux lettres est déplacée vers Exchange Online. Pour plus d’informations, voir [Paramètres du périphérique Exchange ActiveSync avec des déploiements hybrides Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Courrier sécurisé**    La fonction de courrier sécurisé permet la remise sécurisée des messages entre l’organisation locale et l’organisation Exchange Online, via le protocole TLS (Transport Layer Security). L’organisation locale et l’organisation Exchange Online sont mutuellement authentifiées via des sujets de certificat numérique, et les en-têtes de messagerie ainsi que le format des messages en texte enrichi sont conservés dans les organisations.

## Options de configuration hybride

L’Assistant Configuration hybride vous permet de sélectionner des options spécifiques dans plusieurs domaines pour le déploiement hybride. Si vous souhaitez mettre à jour des options de configuration hybride spécifiques après avoir initialement configuré votre déploiement hybride, vous pouvez utiliser soit l’Assistant Configuration hybride, soit l’Environnement de ligne de commande Exchange Management Shell pour sélectionner différentes options de configuration.

Le tableau ci-dessous indique les principales options que l’assistant Configuration hybride modifie et configure.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Zone de configuration</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domaines</p></td>
<td><p>L’assistant ajoute un domaine accepté à l’organisation locale pour le flux de messagerie hybride et les demandes de découverte automatique de l’organisation en nuage. Ce domaine, appelé <em>domaine de coexistence</em>, est ajouté en tant que domaine de proxy secondaire à toutes les stratégies d’adresse de messagerie électronique dont les modèles de domaine <em>PrimarySmtpAddress</em> sont sélectionnés dans l’assistant Configuration hybride. Par défaut, ce domaine est &lt;domaine&gt;.mail.onmicrosoft.com.</p>
<p>Vous pouvez afficher le domaine accepté en exécutant la commande suivante de l’Environnement de ligne de commande Exchange Management Shell dans Exchange Online.</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>Certificat de courrier sécurisé</p></td>
<td><p>L’Assistant vous demande de sélectionner un certificat spécifique émis par une autorité de certification tierce approuvée (CA) qui est utilisée pour authentifier et sécuriser des messages électroniques échangés entre l’organisation locale et l’organisation Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Partage fédéré Exchange</p></td>
<td><p>L’assistant vérifie s’il existe une relation d’authentification OAuth ou une approbation de fédération avec le système d’authentification Azure Active Directory pour l’organisation locale. Si tel est le cas, l’authentification OAuth l’approbation de fédération existante est utilisée pour prendre en charge le déploiement hybride. Sinon, l’assistant configure l’authentification OAuth ou crée une approbation de fédération pour l’organisation locale avec le système d’authentification Azure AD, en fonction du type de configuration Exchange locale. L’assistant ajoute également tout domaine sélectionné dans l’assistant Configuration hybride à l’approbation de fédération, si nécessaire.</p>
<p>Outre la configuration de l’authentification OAuth ou de l’approbation de fédération, l’assistant crée et configure également des relations organisationnelles pour l’organisation sur site et l’organisation Exchange Online. Ces relations permettent à l’assistant d’activer plusieurs fonctions de déploiement hybride, telles que le partage de disponibilité, la redirection Outlook sur le web et les infos-courrier.</p></td>
</tr>
<tr class="even">
<td><p>Flux de messagerie</p></td>
<td><p>L’Assistant vous permet de sélectionner et de configurer les serveurs Exchange qui vont assurer le transport de messagerie sécurisée entre l’organisation locale et l’organisation Exchange Online. Dans Exchange 2010, il s’agit d’un serveur de transport Hub. Dans Exchange 2013, il s’agit d’un serveur d’accès au client. Dans Exchange 2016 et versions ultérieures, il s’agit d’un serveur de boîte aux lettres.</p>
<p>L’Assistant configure votre organisation locale Exchange et Exchange Online pour l’acheminement de la messagerie hybride. En configurant les connecteurs d’envoi et de réception nouveaux et existants dans l’organisation locale et des connecteurs entrants et sortants dans Exchange Online, l’Assistant vous permet de choisir si les messages sortants vers Internet à partir de l’organisation Exchange Online seront envoyés directement à des destinataires de messagerie externes ou s’ils seront acheminés via vos serveurs Exchange locaux inclus dans le déploiement hybride.</p>

> [!IMPORTANT]
> Le flux de messagerie entrant est contrôlé par l’enregistrement MX de votre organisation. Les messages électroniques Internet entrants pour un déploiement hybride ne sont pas configurés par l’assistant Configuration hybride.

</td>
</tr>
</tbody>
</table>


## Moteur de configuration hybride

Le moteur de configuration hybride exécute les actions essentielles et nécessaires à la configuration et à la mise à jour d’un déploiement hybride. Chargé d’assurer le traitement des actions de la cmdlet `Update-HybridConfiguration`, le moteur de configuration hybride compare l’état de l’objet *HybridConfiguration*Active Directory avec les paramètres actuels de la configuration locale d’Exchange et d’Exchange Online, puis exécute des tâches pour faire correspondre les paramètres de configuration du déploiement avec les paramètres définis dans l’objet *HybridConfiguration*Active Directory. Si les états actuels de la configuration locale de déploiement d’Exchange et d’Exchange Online correspondent déjà aux paramètres définis dans l’objet *HybridConfiguration*Active Directory, le moteur de configuration hybride n’apporte aucune modification à l’organisation locale ou à l’organisation Exchange Online.

Lors de la mise à jour d’un déploiement hybride existant, le moteur de configuration hybride effectue les actions suivantes :

1.  La cmdlet *Update-HybridConfiguration* provoque le démarrage du moteur de configuration hybride.

2.  Le moteur de configuration hybride lit « l’état souhaité » stocké dans l’objet Active Directory`HybridConfiguration`.

3.  Le moteur de configuration hybride détecte les données de topologie et la configuration actuelle à partir de l’organisation Exchange locale.

4.  Le moteur de configuration hybride détecte les données de topologie et la configuration actuelle à partir de l’organisation Exchange Online.

5.  En fonction de l’état souhaité, des données de topologie et de la configuration actuelle, le moteur de configuration hybride établit les « différences » entre l’organisation Exchange locale et l’organisation Exchange Online, puis exécute des tâches de configuration pour mettre en place l’état souhaité.

La figure suivante présente sommairement la façon dont le moteur de configuration hybride récupère et modifie les paramètres de configuration du serveur Exchange local et d’Exchange Online au cours du processus de déploiement hybride.

![Flux de moteur de configuration hybride](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "Flux de moteur de configuration hybride")

