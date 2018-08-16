---
title: 'L’installation d’Exchange sur un contrôleur de domaine n’est pas recommandée'
TOCTitle: L'installation d'Exchange sur un contrôleur de domaine n'est pas recommandée
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50478025
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# L'installation d'Exchange sur un contrôleur de domaine n'est pas recommandée

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2013-03-22_

Le programme d'installation de Microsoft Exchange Server 2013 a détecté que l'ordinateur sur lequel vous tentez d'installer Exchange 2013 se trouve sur un contrôleur de domaine Active Directory. L'installation d'Exchange 2013 sur un contrôleur de domaine n'est pas recommandée.

Si vous installez Exchange 2013 sur un contrôleur de domaine, tenez compte des problèmes suivants :

  - La configuration d’Exchange 2013 pour les autorisations fractionnées Active Directory n’est pas prise en charge.

  - Le groupe universel de sécurité du sous-système approuvé Exchange est ajouté au groupe Administrateurs du domaine quand Exchange est installé sur un contrôleur de domaine. Dans ce cas, des droits d'administrateur de domaine sont accordés à tous les serveurs Exchange de ce domaine.

  - Exchange Server et Active Directory sont deux applications qui consomment énormément de ressources. Il convient de tenir compte des implications sur les performances lorsque toutes deux fonctionnent sur le même ordinateur.

  - Vous devez veiller à installer le contrôleur de domaine Exchange 2013 dans un serveur de catalogue global.

  - Il est possible que les services Exchange ne démarrent pas correctement si le contrôleur de domaine est également un serveur de catalogue global.

  - L’arrêt du système prendra beaucoup plus de temps si les services Exchange ne sont pas stoppés avant l’arrêt ou le redémarrage du serveur.

  - La rétrogradation d'un contrôleur de domaine à un serveur membre n'est pas prise en charge.

  - L’exécution d’Exchange 2013 sur un nœud en cluster qui est également un contrôleur de domaine Active Directory n’est pas prise en charge non plus.

Nous vous recommandons d'installer Exchange 2013 sur un serveur membre.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

