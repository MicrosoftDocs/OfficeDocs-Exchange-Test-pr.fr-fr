---
title: 'Impossible de contacter le serveur DNS principal'
TOCTitle: Impossible de contacter le serveur DNS principal_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50478267
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossible de contacter le serveur DNS principal\_PrimaryDNSTestFailed

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car il est impossible d’établir la communication avec le serveur DNS principal (Domain Name System).

L’installation d’Exchange 2007 nécessite une communication entre l’ordinateur local et la base de données DNS faisant autorité pour le domaine.

Microsoft Exchange dépend du DNS pour résoudre l’adresse IP de son serveur de destination interne ou externe suivant.

La communication avec le serveur DNS principal peut échouer pour les raisons suivantes :

  - La configuration TCP/IP locale ne pointe pas vers le serveur DNS correct.

  - Le serveur DNS est arrêté ou inaccessible en raison d’une défaillance du réseau ou pour d’autres motifs.

Pour résoudre ce problème :

  - Vérifiez que la configuration TCP/IP locale pointe vers le serveur DNS correct.

Pour vérifier la configuration TCP/IP locale

1.  Passez en revue la configuration TCP/IP locale :
    
    Pour plus d’informations, consultez « Configurer TCP/IP pour utiliser DNS » ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - Vérifiez que le serveur DNS est en cours d’exécution et peut être contacté.

Pour vérifier que le serveur DNS est en cours d’exécution et peut être contacté

1.  Pour vérifier que le serveur DNS est en cours d’exécution, effectuez au moins l’une des vérifications suivantes :
    
      - Examinez l’état du serveur DNS à partir du programme d’administration DNS sur le serveur DNS.
    
      - Redémarrez le serveur DNS.
        
        Pour plus d’informations, consultez « Démarrer, arrêter, suspendre ou redémarrer un serveur DNS » ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - Vérifiez le temps de réponse du serveur DNS à l’aide de la commande **nslookup**.
        
        Pour plus d’informations, consultez les instructions de « Vérifier la réactivité du serveur DNS à l’aide de la commande nslookup » ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

