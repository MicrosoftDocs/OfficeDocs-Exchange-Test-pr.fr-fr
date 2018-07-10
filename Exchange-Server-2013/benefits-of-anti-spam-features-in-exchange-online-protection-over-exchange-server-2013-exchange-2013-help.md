---
title: 'Avantages des fonctionnalités de blocage du courrier indésirable dans Exchange Online Protection sur Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Avantages des fonctionnalités de blocage du courrier indésirable dans Exchange Online Protection sur Exchange Server 2013
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50477414
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Avantages des fonctionnalités de blocage du courrier indésirable dans Exchange Online Protection sur Exchange Server 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-05-26_

> [!NOTE]
> Exchange Online Protection (EOP) est la prochaine version de Forefront Online Protection for Exchange (FOPE). Exchange Online intègre les fonctionnalités EOP de protection contre le courrier indésirable.


L'utilisation de la protection Exchange contre le courrier indésirable dans le cloud (Microsoft Exchange Online ou Microsoft Exchange Online Protection) présente les avantages suivants par rapport à Microsoft Exchange Server 2013 qui dispose de la plupart des fonctionnalités anti-spam intégrées de Microsoft Exchange Server 2010 :

  - **Contrôle accru et configuration plus aisée**   Les administrateurs peuvent utiliser la console de gestion web « Centre d'administration Exchange » (CAE) pour personnaliser les paramètres de filtrage du courrier indésirable en fonction des besoins de votre organisation. Exchange Server 2013 ne dispose d'aucune interface utilisateur anti-spam.

  - **Meilleur filtrage des connexions**   Dans Exchange 2013, les listes d’adresses IP autorisées et d’adresses IP bloquées pour le filtrage des connexions ne sont disponibles que si vous installez un serveur de transport Edge sur votre réseau de périmètre. Pour plus d’informations, voir [Serveurs de transport Edge](edge-transport-servers-exchange-2013-help.md). Dans le cloud, vous pouvez choisir d'ignorer le filtrage du courrier indésirable pour les messages électroniques provenant d'expéditeurs approuvés (réunis à partir de diverses sources tierces). Cela vous permet de vous assurer que ces messages ne sont pas marqués comme courrier indésirable par erreur. En outre, le service de filtrage hébergé utilise les propres listes d’adresses IP bloquées de Microsoft, ainsi que des listes recueillies par des fournisseurs, pour garantir un meilleur filtrage au niveau IP.

  - **Meilleur filtrage de contenu**   Vous pouvez configurer facilement votre stratégie de filtrage de contenu pour :
    
      - filtrer les messages rédigés dans des langues spécifiques ;
    
      - filtrer les messages provenant de pays ou régions spécifiques ;
    
      - identifier les messages électroniques envoyés en masse (tels que des publicités et des e-mails marketing) comme du courrier indésirable ;
    
      - rechercher des attributs dans un message et agir sur le message s'il correspond à un attribut d'option anti-spam avancée spécifique. Si vous craignez le hameçonnage, sachez que certaines de ces options intègrent des technologies ID de l'expéditeur et SPF pour authentifier les messages et vérifier qu'ils ne sont pas falsifiés.
    
    Outre les options de filtrage de contenu sus-mentionnées que vous pouvez configurer dans le CAE, le service de filtrage hébergé utilise d'autres listes d'URL pour bloquer les messages suspects qui contiennent des URL spécifiques dans le corps du message.

  - **Mises à jour plus rapides**   Les mises à jour anti-spam sont diffusées plus rapidement sur le réseau. Dans Exchange Server 2013, les mises à jour ont lieu deux fois par mois, tandis que le service est mis à jour plusieurs fois par heure.

  - **Filtrage du courrier sortant**   Le filtrage du courrier indésirable sortant est toujours activé si vous utilisez le service hébergé pour l'envoi de messages sortants, ce qui permet de protéger les organisations utilisant le service ainsi que leurs destinataires.

