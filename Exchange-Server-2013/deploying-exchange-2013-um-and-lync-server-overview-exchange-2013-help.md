---
title: 'Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server: Exchange 2013 Help'
TOCTitle: Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50478748
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée et Microsoft Lync Server peuvent être déployés simultanément afin de fournir aux utilisateurs de l’organisation une messagerie vocale, une messagerie instantanée, un indicateur de présence utilisateur amélioré, une fonctionnalité de conférence audio/vidéo ainsi qu’une expérience de messagerie et de courrier électronique intégrée. La messagerie unifiée est utilisée pour assurer les services de répondeur automatique, Outlook Voice Access et de standard automatique. Microsoft Lync Server permet de tirer parti des fonctions plus avancées d’Enterprise Voice, comme la messagerie instantanée, une fonctionnalité de conférence ainsi que des appels entrants et sortants. Cette rubrique décrit la procédure de configuration de la messagerie unifiée et de Microsoft Lync Server de sorte que ces fonctionnalités soient prises en charge.

> [!TIP]
> Microsoft Office Communications Server 2007 R2 peut également être déployé avec la messagerie unifiée. Dans cette rubrique, « Microsoft Lync Server » se rapporte à Microsoft Lync Server 2010 ou Microsoft Lync Server 2013.


Vous cherchez plus d’informations sur Microsoft Lync Server ? Voir [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

**Contenu de cette rubrique**

Présentation du déploiement de la messagerie unifiée Exchange et Lync Server

Recommandations relatives à la configuration du certificat

Étapes de déploiement

Pour plus d’informations

## Présentation du déploiement de la messagerie unifiée Exchange et Lync Server

La messagerie unifiée combine la messagerie vocale et la messagerie électronique en une infrastructure unique. Microsoft Lync Server Enterprise Voice tire parti de l’infrastructure de messagerie unifiée pour proposer une messagerie vocale, Outlook Voice Access, des notifications d’appels et des standards automatiques.

La liste suivante montre les étapes faciles du déploiement pour la messagerie unifiée et Lync Server. Les informations détaillées sur chaque étape figurent plus loin dans cette rubrique.

1.  Installez Microsoft Lync Server sur la topologie où sont installés les serveurs d’accès au client qui exécutent le service Microsoft Exchange Unified Messaging Call Router et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de Microsoft Exchange. Confirmez qu’au moins un pool Lync est créé.

2.  Installez un certificat valide et signé par une autorité de certification privée ou publique, et approuvé par Lync Server.

3.  Installez les serveurs d’accès au client et les serveurs de boîtes aux lettres. Vérifiez l’installation.

4.  Installez un certificat valide et signé par la même autorité de certification que le certificat que vous avez installé sur vos serveurs Lync.

5.  Créez et configurez un plan de numérotation URI de protocole SIP (Session Initiation Protocol).

6.  Ajoutez tous les serveurs d’accès au client et de boîtes aux lettres au plan de numérotation URI SIP. Cependant, si vous avez plusieurs plans de numérotation URI SIP, vous devez ajouter tous les serveurs d’accès au client et les serveurs de boîtes aux lettres à tous les plans de numérotation URI SIP.

7.  Exécutez le script ExchUcUtil.ps1 à partir du \<dossier d’installation Exchange\>\\Exchange Server\\Script sur le serveur de boîtes aux lettres.
    
    > [!NOTE]
    > Le script ExchUcUtil.ps1 crée une ou plusieurs passerelles IP de messagerie unifiée pour l’intégration Lync. Vous devez désactiver les appels sortants sur toutes les passerelles IP de messagerie unifiée à l’exception de celle que le script a créée. Ceci inclut la désactivation des appels sortants sur les passerelles IP de messagerie unifiée qui ont été créées avant l’exécution du script. Pour désactiver les appels sortants sur une passerelle IP de messagerie unifiée, consultez la rubrique <a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Désactiver les appels sortants sur les passerelles IP de messagerie unifiée</a>.


8.  Exécutez **OcsUmUtil.exe** à partir du dossier %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support sur un Lync Server.

9.  Déployez le serveur de médiation et les passerelles multimédias.

10. Sur votre serveur de médiation, installez un certificat valide et signé par la même autorité de certification que le certificat que vous avez installé sur vos serveurs Lync.

11. Activez vos utilisateurs pour la messagerie unifiée et Enterprise Voice.

## Recommandations relatives à la configuration du certificat

Votre certificat doit être approuvé aussi bien par les ordinateurs exécutant Exchange que par les ordinateurs exécutant Lync Server. Dans un environnement composé de Lync Server et de la messagerie unifiée, suivez ces indications pour déployer un certificat approuvé :

  - Sur vos serveurs Lync, serveurs d’accès au client, serveurs de boîtes aux lettres, serveur de médiation et passerelles multimédias, importez un certificat valide et signé par une autorité de certification privée ou publique. Il devrait s’agir d’un certificat commercial tiers approuvé ou d’un certificat d’infrastructure à clé publique (PKI).

  - La procédure sera plus simple si vous importez le même certificat commercial tiers ou PKI sur chaque serveur Exchange. Installez également ce certificat approuvé sur chaque ordinateur exécutant Microsoft Lync Server et le serveur de médiation. Cela vous rendra le déploiement de certificat plus facile et réduira la charge administrative liée à cette tâche. Il est recommandé d’utiliser un certificat approuvé prenant en charge l’attribut Autres noms d’objet.
    
    Lorsque vous déployez le protocole TLS avec la messagerie unifiée, les certificats utilisés sur le serveur d’accès au client et le serveur de boîtes aux lettres doivent tous deux contenir le nom de domaine complet (FQDN) de l’ordinateur local dans le nom du sujet du certificat. Pour contourner ce problème, utilisez un certificat public et importez le certificat sur tous les serveurs d’accès au client et serveurs de boîte aux lettres, toutes les passerelles VoIP, les PBX IP et tous les serveurs Lync.
    
    Si votre déploiement comprend des passerelles VoIP ou PBX IP, et si vous utilisez un plan de numérotation en mode SIP sécurisé ou en mode sécurisé, un certificat approuvé est requis entre les serveurs d’accès au client et les serveurs de boîte aux lettres, et les passerelles VoIP ou PBX IP. Un certificat approuvé est également requis si une connexion SIP directe est utilisée. Si vous utilisez un plan de numérotation en mode SIP sécurisé ou en mode sécurisé, vous pouvez utiliser le même certificat approuvé sur vos serveurs Lync et Exchange que sur vos passerelles VoIP ou PBX IP.

  - Lorsque vous connectez des serveurs d’accès au client Exchange et des serveurs de boîtes aux lettres à des serveurs Microsoft Lync ou à des passerelles SIP tierces ou à des équipements de téléphonie PBX (Private Branch eXchange), pour établir des sessions sécurisées, vous devez utiliser un certificat valide et signé par une autorité de certification tierce, publique ou privée. Vous pouvez utiliser un seul certificat sur tous les serveurs d’accès au client et les serveurs de boîtes aux lettres tant que les noms de domaine complets de tous les serveurs d’accès au client et les serveurs de boîtes aux lettres sont inclus dans la liste des SAN du certificat. Ou bien, vous pouvez générer un certificat différent pour chaque serveur d’accès au client et serveur de boîte aux lettres, avec le nom de domaine complet de l’ordinateur local présent dans le nom commun sujet ou la liste des SAN du certificat pour ce serveur. La messagerie unifiée Exchange ne prend pas en charge les certificats avec caractères génériques avec Microsoft Lync Server.
    
    Un nom d’objet non générique est requis pour que Lync Server et Exchange fonctionnent conjointement. La messagerie unifiée et Lync Server utilisent le nom d’objet comme moyen d’indiquer qu’ils sont des homologues SIP approuvés. Lync Server nécessite également un nom d’objet non générique dans certains scénarios de routage d’appels. Le nom de domaine complet doit être utilisé comme valeur « Délivré à ».
    
    Pour la messagerie unifiée d’Exchange, l’utilisation de caractères génériques dans le nom de certificat n’est pas prise en charge. Toutefois, vous pouvez mettre un caractère générique dans le SAN.

Le tableau suivant indique les exigences de certificat pour l’installation et la configuration de certificats pour la messagerie unifiée d’Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologie</th>
<th>Configuration du certificat</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès au client et boîte aux lettres sur le même serveur (sans Lync 2010 ou 2013 ; plans de numérotation non SIP)</p></td>
<td><p>Un certificat est nécessaire entre des serveurs d’accès au client et des serveurs de boîtes aux lettres. C’est le même certificat qui est utilisé entre les serveurs d’accès client et les serveurs de boîtes aux lettres, et les passerelles VoIP, PBX IP ou SBC.</p></td>
</tr>
<tr class="even">
<td><p>Accès au client et boîte aux lettres sur des serveurs différents (sans Lync 2010 ou 2013 ; plans de numérotation non SIP)</p></td>
<td><p>Un certificat est requis. Le certificat doit correspondre sur les serveurs d’accès au client et les serveurs de boîtes aux lettres. Un certificat est également requis entre les serveurs d’accès au client et les serveurs de boîtes aux lettres, et la passerelle VoIP, PBX IP ou SBC. Il peut s’agir du même certificat ou d’un certificat différent par rapport à celui utilisé entre les serveurs d’accès au client et les serveurs de boîtes aux lettres. Pour les serveurs d’accès au client et de boîtes aux lettres, vous pouvez exécuter la cmdlet <strong>Create-ExchangeCertificate</strong> à partir de n’importe quel serveur.</p></td>
</tr>
<tr class="odd">
<td><p>Accès au client et boîte aux lettres sur le même serveur (avec Lync 2010 ou 2013 et des plans de numérotation SIP)</p></td>
<td><p>Un certificat est requis. Les serveurs d’accès au client et de boîtes aux lettres doivent avoir le même certificat racine que les serveurs Lync 2010 ou Lync 2013.</p></td>
</tr>
<tr class="even">
<td><p>Accès au client et boîte aux lettres sur des serveurs différents (avec Lync 2010 ou 2013 et des plans de numérotation SIP)</p></td>
<td><p>Un certificat est requis. Les serveurs d’accès au client et de boîtes aux lettres doivent avoir le même certificat racine que les serveurs Lync 2010 ou Lync 2013.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Étapes de déploiement

Après avoir installé les serveurs requis dans votre organisation, il est recommandé d’effectuer un certain nombre d’étapes sur vos déploiements de messagerie unifiée Exchange et Lync Server afin de déployer correctement Enterprise Voice pour vos utilisateurs.

Pour plus d’informations sur Microsoft Lync Server, voir [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

Vous devez réaliser les étapes suivantes pour configurer la messagerie unifiée afin qu’elle marche avec les fonctionnalités Enterprise Voice dans Lync Server :

1.  Créez un ou plusieurs plans de numérotation URI SIP de messagerie unifiée, chacun correspondant à un profil d’emplacement Lync Server. Vous devez créer un profil d’emplacement Enterprise Voice pour chaque plan de commutation des appels de messagerie unifiée Exchange. Vous pouvez utiliser la cmdlet **Get-UMDialPlan** pour obtenir le nom de domaine complet d’un plan de numérotation URI SIP. Pour plus d’informations sur la création d’un plan de numérotation avec un URI SIP, voir [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).
    
    > [!NOTE]
    > Au moment d’intégrer la messagerie unifiée Exchange et Lync Server, vous jugerez sans doute inutile de configurer des règles de numérotation ou des groupes de règles de numérotation dans la messagerie unifiée Exchange. Lync Server est conçu pour acheminer des appels (routage) et convertir des numéros pour les utilisateurs de votre organisation. Il procède également de même lorsque les appels sont effectués par la messagerie unifiée Exchange pour le compte des utilisateurs.


2.  Sur les serveurs d’accès au client et de boîtes aux lettres, installez un certificat valide et signé par une autorité de certification privée ou publique. Il s’agit de la même autorité de certification qui a été utilisée sur les serveurs Lync.

3.  Pour chiffrer le trafic VoIP (Voice over IP), configurez le plan de numérotation avec un URI SIP comme une Protection SIP ou Sécurisé.
    
    > [!CAUTION]
    > Si vous avez défini le paramètre de sécurité en mode sécurisé SIP afin de requérir le chiffrement du trafic SIP uniquement, ce paramètre n’est pas suffisant dans un plan de numérotation si le pool frontal est configuré pour requérir le chiffrement (ce qui signifie que le pool requiert le chiffrement pour trafic RTP et SIP). Lorsque le plan de numérotation et les paramètres de sécurité du pool ne sont compatibles, tous les appels vers la messagerie unifiée Exchange à partir du pool frontal échouent, ce qui provoque une erreur de type « Paramètre de sécurité incompatible ».
    
    Bien qu’un plan de numérotation de messagerie unifiée puisse être configuré en mode SIP sécurisé ou en mode sécurisé, il est recommandé d’utiliser la configuration en mode sécurisé pour permettre un fonctionnement correct de Lync Phone Edition. Cela est dû aux paramètres du niveau de chiffrement par défaut de Lync Server. Un périphérique Lync Phone Edition ne fonctionnera que si les paramètres de chiffrement sont configurés comme indiqué dans le tableau suivant. Ce tableau décrit la relation entre les paramètres de chiffrement pour Lync Server et les plans de numérotation de messagerie unifiée.
    
    **Paramètres de chiffrement pour Lync Phone Edition**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>Plan de numérotation de messagerie unifiée</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Chiffrement requis (valeur par défaut)</p></td>
    <td><p>Sécurisé</p></td>
    </tr>
    <tr class="even">
    <td><p>Chiffrement facultatif</p></td>
    <td><p>Sécurisé SIP/Sécurisé</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aucun chiffrement</p></td>
    <td><p>Protection SIP</p></td>
    </tr>
    </tbody>
    </table>


4.  Ajoutez tous les serveurs d’accès au client et de boîtes aux lettres au plan de numérotation SIP. Pour activer le serveur afin de répondre aux appels entrants, vous devez ajouter tous les serveurs Exchange à un plan de numérotation si vous voulez qu’ils répondent aux appels provenant de Lync Server.

5.  Définissez le mode de démarrage et le port d’écoute TLS sur les serveurs d’accès au client et de boîte aux lettres qui sont ajoutés au plan de numérotation URI SIP sur Double puis redémarrez le service de messagerie unifiée MicrosoftExchange sur chaque serveur de boîte aux lettres et le service MicrosoftExchange Unified Messaging Call Router sur chaque serveur d’accès au client.

6.  Créez et configurez un standard automatique de messagerie unifiée. Pour plus d’informations, consultez la rubrique [Configurer un standard automatique de messagerie unifiée](set-up-a-um-auto-attendant-exchange-2013-help.md).

7.  Lorsque vous activez la messagerie vocale pour les utilisateurs, créez une adresse SIP pour les utilisateurs qui utiliseront Enterprise Voice. Dans la plupart des cas, cette adresse SIP sera la même adresse SIP qui sera utilisée lorsqu’un utilisateur est activé pour Enterprise Voice. Pour plus d’informations, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).
    
    > [!NOTE]
    > Les utilisateurs qui sont associés à un plan de numérotation URI SIP ne peuvent pas recevoir de télécopies entrantes. Ceci est dû au fait que les appels vocaux et de télécopie entrants sont routés via un serveur de médiation et que la télécopie n’est pas prise en charge lorsque vous utilisez un serveur de médiation.


8.  Ouvrez l’environnement de ligne de commande Exchange Management Shell et exécutez le script exchucutil.ps1 situé dans le dossier %Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts. Le script exchucutil.ps1 effectue les opérations suivantes :
    
      - Il donne la permission à Lync Server de lire les composants Active Directory de la messagerie unifiée Exchange, notamment le plan de numérotation URI SIP qui a été créé au cours de la tâche précédente. Pour des informations détaillées sur la configuration des permissions dans Active Directory, voir [Utilisation d’ADSI Edit pour appliquer les autorisations](https://go.microsoft.com/fwlink/p/?linkid=82751).
    
      - Il crée une passerelle IP de messagerie unifiée pour chaque pool Lync Server ou chaque serveur exécutant Lync Server Standard Edition qui héberge des utilisateurs activés pour Enterprise Voice. Pour plus d’informations, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Il crée un groupement de postes de messagerie unifiée Exchange pour chaque passerelle IP de messagerie unifiée. L’identificateur de pilote pour le groupement de postes sera le nom du plan de numérotation associé à la passerelle IP de messagerie unifiée correspondante. Le groupement de postes doit spécifier le plan de numérotation SIP de messagerie unifiée utilisé avec la passerelle IP de messagerie unifiée.

9.  Activez les utilisateurs pour la messagerie vocale. Lors de l’activation, assurez-vous d’entrer une adresse SIP valide pour les utilisateurs et associez-les à un plan de numérotation SIP. Pour plus d’informations, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

Vous devez également exécuter les tâches suivantes pour configurer Lync Server afin qu’il fonctionne avec la messagerie unifiée Exchange :

  - Créez des profils d’emplacement ou des plans de numérotation Lync. Le nom de profil d’emplacement n’a pas besoin de correspondre au nom de domaine complet des plans de numérotation de messagerie unifiée correspondants.

  - Affectez les profils d’emplacement aux pools Lync Server.

  - Déployez et configurez les passerelles multimédias et les serveurs de médiation. Vous devez également importer un certificat provenant de la même autorité de certification approuvée qui a été utilisée pour les certificats des serveurs d’accès au client et de boîte aux lettres, et Lync Server.

  - Définissez l’utilisation du téléphone, créez et assignez les stratégies de voix et les routes d’appels sortants.

  - Configurez les utilisateurs pour Enterprise Voice et ajoutez un identificateur SIP et URI TEL.

  - Exécutez la commande **ocsumutil.exe** qui crée les objets contact pour Outlook Voice Access et les standards automatiques.
    
    > [!NOTE]
    > Lorsque vous installez Lync Server, l’attribut <strong>msRTC-SIPLine</strong> est ajouté à Active Directory. Si vous n’avez pas installé Lync Server dans votre environnement, cet attribut n’est pas ajouté à Active Directory et la résolution de nom d’ID de l’appelant parmi les plans de numérotation dans des scénarios de forêt unique et inter-forêts ne doit pas fonctionner correctement, à moins de configurer des adresses proxy de messagerie unifiée pour les utilisateurs sans extension messagerie unifiée.


Après avoir configuré Lync Server et les serveurs de messagerie unifiée, vous devez permettre à l’utilisateur d’utiliser Lync Server et installer Lync sur l’ordinateur client de l’utilisateur.

> [!NOTE]
> Lors de l’intégration de la messagerie unifiée et de Lync Server, les notifications d’appels manqués ne sont pas disponibles pour les utilisateurs qui ont une boîte aux lettre située sur un serveur de boîtes aux lettres Exchange 2007 ou Exchange 2010. Une notification d’appel manqué est générée lorsqu’un utilisateur se déconnecte avant l’envoi de l’appel vers un serveur de boîtes aux lettres.


Retour au début

## Pour plus d’informations

Pour plus d’informations sur l’exécution des tâches à effectuer pour Microsoft Lync Server, voir [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

