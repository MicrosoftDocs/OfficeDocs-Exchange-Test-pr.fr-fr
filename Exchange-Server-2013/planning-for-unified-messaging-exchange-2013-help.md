---
title: 'Planification de la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Planification de la messagerie unifiée
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 50478754
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planification de la messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Lorsque vous planifiez votre déploiement de votre messagerie unifiée, de nombreux facteurs doivent être pris en compte pour aboutir à un déploiement correct. Vous devez connaître les différents éléments de la messagerie unifiée, ainsi que chaque composant et fonction de façon à pouvoir planifier correctement l’infrastructure et le déploiement de la messagerie unifiée. L'allocation de temps à la planification et à la résolution de ces problèmes contribue à éviter des problèmes lors du déploiement d'une messagerie unifiée au sein de vitre organisation.

Vous allez peut-être déployer une messagerie unifiée dans une nouvelle organisation Exchange ou effectuer une mise à niveau à partir d’une solution de messagerie vocale héritée ou tierce. S’il s’agit d’une mise à niveau, vous devez décider s’il faut convertir les périphériques qui acceptent des protocoles basés sur des circuits de téléphonie en un réseau de données utilisant IP ou s’il faut déployer une solution Enterprise Voice comme Microsoft Lync Server. Il s’agit ici de la première étape du processus qui va vous préparer à mieux comprendre et à déployer une messagerie unifiée au sein de votre organisation.

## Planification de votre système de messagerie vocale

La messagerie unifiée fournit des services de messagerie vocale, de télécopie et messagerie électronique dans une banque unique qui est accessible à partir d’un téléphone, d’un ordinateur personnel et d’un appareil mobile. Les utilisateurs peuvent accéder à des services de messages vocaux, de messagerie électronique, d’informations de calendrier et de contacts personnels figurant dans leur boîte aux lettres Exchange à partir de clients de messagerie électronique comme Outlook et Outlook Web App.

Les serveurs d’accès au client qui exécutent le service Routeur d’appel de messagerie unifiée Microsoft Exchange et les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée de Microsoft Exchange sont conçus pour fournir des fonctionnalités de messagerie vocale aux utilisateurs de votre organisation.

Les serveurs de boîtes aux lettres s’appuient sur des serveurs d’accès au client pour transférer le trafic SIP provenant des appels entrants, puis établissent une connexion avec une passerelle VoIP, un système IP-PBX ou un contrôleur SBC (Session Border Controller), et acceptent le trafic multimédia RTP/SRTP. Toute la messagerie vocale et tous les messages de télécopie sont soumis à partir du service de messagerie unifiée de Microsoft Exchange sur un serveur de boîtes aux lettres pour être remis dans la boîte aux lettres de l’utilisateur. Pour qu’un utilisateur puisse utiliser les fonctionnalités de messagerie vocale avec la messagerie unifiée, celui-ci doit disposer d’une boîte aux lettres Exchange.

## Planification de votre déploiement de messagerie unifiée

D’une manière générale, plus la topologie de messagerie unifiée est simple, plus son déploiement et sa maintenance sont faciles. Installez le moins possible de serveurs d’accès au client et de boîtes aux lettres, et créez le moins possible de composants de messagerie unifiée (comme des plans de numérotation, des standards automatiques et des stratégies de boîte aux lettres de messagerie unifiée) pour prendre en charge vos objectifs professionnels et organisationnels. Les grandes entreprises disposant d’environnements de réseau et de téléphonie complexes, de plusieurs divisions autonomes ou d’autres systèmes complexes nécessitent davantage de planification que les petites organisations avec des besoins de messagerie relativement simples.

Voici quelques uns des domaines à prendre en considération lorsque vous planifiez le déploiement d’une messagerie unifiée au sein de votre organisation :

  - **Exigences d’organisation**   Evaluez vos besoins professionnels, l’utilité du déploiement d’un système de messagerie vocale, la topologie du réseau physique et d’entreprise et les exigences en matière de sécurité au sein de votre organisation.

  - **Exigences en téléphonie**   Examinez votre système de téléphonie, votre réseau de commutation de circuits et votre système de messagerie vocale existants.

  - **Exigences réseau**   Analysez la topologie de votre réseau, la conception actuelle de votre réseau IP de commutation de paquets, y compris vos points de connectivité du réseau local (LAN) et du réseau étendu (WAN), et aussi les périphériques.

  - **Active Directory (service de répertoire)**   Inspectez votre implémentation et conception actuelles et envisagez comment intégrer une messagerie unifiée.

  - **Modèle de déploiement**   Déterminez si vous voulez avoir un déploiement de messagerie unifiée hybride, uniquement en ligne ou sur site.

  - **Exigences Exchange**   Déterminer ce qui suit :
    
      - Combien d’utilisateurs vont utiliser la messagerie vocale.
    
      - Quelles fonctionnalités de messagerie unifiée souhaitez-vous déployer : appels simultanées, accès internes et externes pour les utilisateurs, télécopies entrantes, aperçu de la messagerie vocale, etc.
    
      - Le nombre de serveurs d’accès au client et de boîtes aux lettres à déployer.
    
      - Les besoins et quotas en matière de stockage pour les utilisateurs de la messagerie vocale.
    
      - La meilleure conception en termes de haute disponibilité et de résilience de site. Ceci inclut une configuration requise pour la messagerie unifiée, la fourniture d’un déploiement de messagerie unifiée hautement disponible et modulable, ainsi qu’une configuration requise en termes de matériel afin de garantir les performances.

  - **Intégration avec des composants et des périphériques de téléphonie**   Déterminez s’il faut utiliser des équipements de téléphonie traditionnels ou Microsoft Lync Server. Envisagez la disposition des passerelles VoIP, des équipements de téléphonie et des serveurs d’accès au client et de boîtes aux lettres, et si vous souhaitez activer Enterprise Voice dans votre organisation.

## Connexion de votre réseau de téléphonie

La messagerie unifiée nécessite l'intégration de votre déploiement Exchange Server dans votre circuit de téléphonie existant ou son intégration dans Microsoft Lync Server. Vous devez réaliser une analyse attentive de votre infrastructure de téléphonie existante et de Microsoft Lync Server, et suivre ensuite les étapes de planification appropriées afin de pouvoir déployer et gérer correctement la messagerie vocale de la messagerie unifiée.

**Passerelles VoIP** Le choix approprié en matière de passerelle VoIP, système IP-PBX, PBX compatible SIP ou contrôleur SBC ne constitue que la première étape dans l’intégration de votre réseau de téléphonie avec la messagerie unifiée. Vous devez configurer ces périphériques pour qu’ils fonctionnent avec la messagerie unifiée, déployer les serveurs d’accès au client et de boîtes aux lettres et créer tous les composants de messagerie unifiée nécessaires. Ces composants vous permettent d’établir la connexion entre votre réseau avec protocoles basés sur les circuits et votre réseau de données IP et d’activer la messagerie vocale pour vos utilisateurs.

**Microsoft Lync Server**   La messagerie unifiée peut utiliser Microsoft Lync Server pour faire converger les fonctions de messagerie vocale, de messagerie instantanée, d’indicateur de présence amélioré, de conférence audio/vidéo et de messagerie électronique dans un environnement de communication intégré et familier. L’intégration de la messagerie unifiée et de Microsoft Lync Server présente les avantages suivants :

  - Notifications de présence améliorées grâce à une gamme d'applications qui tiennent les utilisateurs informés de la disponibilité de leurs contacts.

  - Intégration de la messagerie instantanée, de la messagerie vocale, de la téléconférence, de la messagerie électronique et d’autres méthodes de communication permettant aux utilisateurs de sélectionner la méthode la mieux adaptée à leur tâche. Les utilisateurs peuvent également passer d’une méthode à une autre en fonction de leurs besoins.

  - Disponibilité des options de communication depuis tout site équipé d'une connexion Internet.

  - Client actif (Microsoft Lync) pour la téléphonie, la messagerie instantanée et la conférence.

  - Continuité de l’expérience utilisateur sur plusieurs périphériques.

Pour plus d'informations sur Microsoft Lync Server, consultez la rubrique [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La planification et le déploiement de la messagerie unifiée peuvent constituer certains défis. Selon votre compétence technique dans Exchange et les systèmes de messagerie vocale, vous pourriez souhaiter obtenir l’assistance d’un spécialise de la messagerie unifiée. Un spécialiste en messagerie unifiée Exchange va vous aider à assurer une transition homogène d’un système de messagerie vocale hérité ou tiers vers la messagerie unifiée Exchange. L’exécution d’un nouveau déploiement ou la mise à niveau d’un système de messagerie vocale hérité nécessite une très bonne connaissance des passerelles IP, des PBX et de la messagerie unifiée. Pour plus d’informations sur comment contacter un spécialiste de la messagerie unifiée, consultez <a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists</a>.</td>
</tr>
</tbody>
</table>


## Étapes de déploiement

De nombreuses options de déploiement sont possibles pour la messagerie unifiée. Chaque option possède plusieurs étapes en commun qui sont obligatoires pour créer un système évolutif à haute disponibilité prenant en charge des nombres importants d’utilisateurs. Ces étapes sont les suivantes :

1.  Déployez et configurez vos composants de téléphonie ou Microsoft Lync Server pour la messagerie unifiée.

2.  Vérifiez que vous avez installé correctement les serveurs d’accès au client et de boîtes aux lettres nécessaires pour la messagerie unifiée.

3.  Créez et configurez les composants de messagerie unifiée requis, notamment des plans de numérotation de messagerie unifiée, des passerelles IP de messagerie unifiée, des groupements de postes de messagerie unifiée et des stratégies de boîte aux lettres de messagerie unifiée.

4.  Procédez aux tâches consécutives au déploiement, notamment l'obtention des certificats pour l’authentification TLS, la création des standards automatiques de messagerie unifiée et la configuration des télécopies.

Pour obtenir des informations détaillées sur le déploiement de la messagerie unifiée, voir [Déploiement de la messagerie unifiée Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Si vous intégrez votre environnement de messagerie unifiée à Office Communications Server, plusieurs éléments supplémentaires sont à prendre en compte pour la planification. Pour plus d’informations, consultez la rubrique [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

