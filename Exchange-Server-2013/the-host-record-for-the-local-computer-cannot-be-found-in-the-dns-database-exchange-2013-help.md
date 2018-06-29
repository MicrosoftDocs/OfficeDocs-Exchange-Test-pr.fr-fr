---
title: "L'enregistrement d'hôte pour l'ordinateur local est introuvable dans la base de données DNS: Exchange 2013 Help"
TOCTitle: L'enregistrement d'hôte pour l'ordinateur local est introuvable dans la base de données DNS
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50477826
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# L'enregistrement d'hôte pour l'ordinateur local est introuvable dans la base de données DNS

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2016-12-09_

Le programme d’installation de Microsoft Exchange Server 2013 ne peut pas poursuivre son exécution, car l’enregistrement d’hôte (A) pour cet ordinateur ne figure pas dans la base de données DNS (Domain Name System).

Le programme d'installation d'Exchange 2013 nécessite que l'ordinateur local ait un enregistrement d'hôte (A) valide inscrit auprès de la base de données DNS faisant autorité pour le domaine.

Exchange dépend des enregistrements d'hôte (A) DNS pour connaître l'adresse IP du serveur de destination suivant, interne ou externe.

Pour résoudre ce problème :

  - Vérifiez que la configuration TCP/IP locale pointe vers le serveur DNS correct. Pour plus d'informations, consultez la rubrique [Configurer les paramètres TCP/IP](https://go.microsoft.com/fwlink/p/?linkid=108281).

  - Nslookup.exe permet de vérifier que l'enregistrement d'hôte (A) existe sur le serveur DNS. Pour plus d'informations, consultez la rubrique [Pour vérifier si des enregistrements de ressource A figurent dans DNS](https://go.microsoft.com/fwlink/?linkid=63001).

Pour plus d'informations sur la résolution de noms DNS, le dépannage et les enregistrements d'hôte (A), consultez les documents suivants :

  - [Résolution des problèmes DNS](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [Gestion des enregistrements de ressources](https://go.microsoft.com/fwlink/p/?linkid=294829)

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

