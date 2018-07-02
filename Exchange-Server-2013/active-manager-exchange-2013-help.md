---
title: 'Active Manager: Exchange 2013 Help'
TOCTitle: Active Manager
ms:assetid: f4be27b7-1d7c-47b4-87ac-bfdfcc046f00
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd776123(v=EXCHG.150)
ms:contentKeyID: 50479549
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Manager

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Microsoft Exchange Server 2013 inclut un composant nommé *Active Manager* qui gère la plateforme haute disponibilité qui comprend le groupe de disponibilité de la base de données (DAG) et les copies de la base de données de boîte aux lettres. Active Manager s'exécute dans le service de réplication Microsoft Exchange (MSExchangeRepl.exe) sur tous les serveurs de boîtes aux lettres. Sur les serveurs de boîtes aux lettres qui ne sont pas membres d’un groupe de disponibilité de base de données (DAG), il existe un seul rôle Active Manager : *gestionnaire Active Manager autonome*. Deux rôles Active Manager sont disponibles sur les serveurs membres d’un groupe de disponibilité de base de données : *gestionnaire Active Manager principal* (PAM) et *gestionnaire Active Manager de secours* (SAM). Le rôle Active Manager principal est le gestionnaire dans un groupe de disponibilité de base de données qui détermine les copies qui seront actives et passives. Il est chargé d'obtenir les notifications de modification de topologie et de réagir aux défaillances de serveur. Le membre du groupe de disponibilité de base de données détenant le rôle PAM est toujours le membre qui est actuellement propriétaire de la ressource quorum de cluster (groupe de clusters par défaut). En cas de défaillance du serveur propriétaire de la ressource quorum de cluster, le rôle PAM est automatiquement déplacé vers un serveur opérationnel qui s'approprie la ressource quorum de cluster. De plus, si vous devez procéder à une mise hors connexion du serveur qui héberge la ressource quorum de cluster à des fins de maintenance ou de mise à niveau, vous devez au préalable déplacer le gestionnaire Active Manager principal vers un autre serveur du groupe de disponibilité de base de données. Le gestionnaire Active Manager principal gère tous les déplacements de désignations actives entre les copies d’une base de données. (Une seule copie peut être active à la fois, et cette copie peut être montée ou démontée.) Il prend également en charge les fonctions assurées par le rôle gestionnaire Active Manager de secours (SAM) sur le système local (détection des défaillances des bases de données locales et de la banque d'informations locales).

Le rôle gestionnaire Active Manager de secours fournit des informations sur le serveur qui héberge la copie active d'une base de données de boîtes aux lettres aux autres composants d'Exchange qui exécutent un composant client Active Manager (ex. services Accès client ou Transport). Le gestionnaire Active Manager de secours détecte les défaillances des bases de données locales et de la banque d'informations locales. Il réagit aux défaillances en demandant au gestionnaire Active Manager principal d'opérer un basculement (si la base de données est répliquée). Un gestionnaire Active Manager de secours ne détermine pas la cible d’un basculement. Il ne met pas non plus à jour l’état de l’emplacement d’une base de données dans le gestionnaire Active Manager principal. Il accèdera à l'état de l'emplacement de la copie de base de données active pour répondre aux requêtes pour la copie active de la base de données qu'il reçoit.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 n’est pas une application en cluster. Exchange 2010 utilise les fonctions de la bibliothèque d'API de cluster implémentées dans le fichier clusapi.dll pour les fonctions de cluster, groupe, réseau de cluster (pulsations), gestion des nœuds, Registre de cluster, et quelques fonctions de code de contrôle. De plus, Active Manager conserve les informations de la base de données de boîtes aux lettres actuelle (ex. les données actives et passives, et les données montées) dans la base de données de clusters (également appelée registre de cluster). Bien que les informations soient stockées directement dans la base de données de clusters, aucun autre composant n'y accède directement.</td>
</tr>
</tbody>
</table>


Dans Exchange 2013, le service de réplication Microsoft Exchange contrôle régulièrement l'intégrité de toutes les bases de données montées. En outre, il contrôle également le moteur de stockage extensible (ESE, Extensible Storage Engine) afin de détecter d’éventuelles défaillances ou erreurs d’E/S. Lorsque le service détecte une défaillance, il informe le gestionnaire Active Manager. Ce dernier détermine alors la copie de base de données devant être montée, ainsi que les exigences pour le montage de cette base de données. De plus, Active Manager suit la copie active d'une base de données de boîtes aux lettres (en fonction de la dernière copie montée de la base de données) et fournit les résultats du suivi au serveur d'accès client auquel le client est connecté.

## Sélection de la meilleure copie

Lorsqu’une panne qui empêche d'accéder à la copie active d'une base de données de boîtes aux lettres répliquée se produit, Active Manager prend diverses mesures pour remédier à la panne et sélectionne la meilleure copie passive possible de la base de données en panne qu’il active. Cette procédure appelée « sélection de la meilleure copie » (BCS) dans Exchange 2010 est maintenant appelée « sélection de la meilleure copie et du serveur » (BCSS) dans Exchange 2013. Cette procédure est la suivante :

1.  La fonction de disponibilité gérée ou Active Manager détecte une défaillance ou lorsqu’un administrateur initie un basculement non ciblé.

2.  La PAM exécute l'algorithme interne BCSS.

3.  Un processus appelé *tentative de copie des derniers journaux* tente de copier les fichiers journaux manquants depuis le serveur qui a hébergé la copie de la base de données active avant que la panne ou le basculement n’ait lieu.

4.  Lorsque la procédure de tentative de copie des derniers journaux est terminée, la valeur du paramètre *AutoDatabaseMountDial* pour les serveurs de boîtes aux lettres qui hébergent des copies de la base de données est comparée à la longueur de la file d’attente de copie de la base de données activée. À ce stade, deux cas de figure sont possibles :
    
      - Le nombre de fichiers journaux manquants est inférieur ou égal à la valeur du paramètre *AutoDatabaseMountDial*, auquel cas l’étape 5 intervient.
    
      - Le nombre de fichiers journaux manquants est supérieur à la valeur du paramètre *AutoDatabaseMountDial*, auquel cas Active Manager tente d’activer la meilleure copie suivante disponible, s’il en existe une.

5.  Le gestionnaire Active Manager principal envoie une demande de montage à la Banque d'informations Microsoft Exchange via un appel de procédure distante (RPC). À ce stade, deux cas de figure sont possibles :
    
      - La base de donnée est montée et rendue accessible aux clients.
    
      - La base de données n’est pas montée et le gestionnaire Active Manager principal exécute les étapes 3 et 4 sur la meilleure copie suivante (si disponible).

Dans Exchange 2010, le processus de sélection de la meilleure copie (BCS) a évalué plusieurs aspects de chaque copie de base de données pour déterminer la meilleure copie à activer. Il s'agit notamment des points suivants :

  - Longueur de la file d'attente de copie

  - Longueur de la file d’attente de relecture

  - État de la base de données

  - Statut de l’index de contenu

Dans Exchange 2013, Active Manager exécute tous les mêmes contrôles et phases BCS, mais il comprend également une contrainte en ordre décroissant de tous les états de fonctionnement correct. Plus spécifiquement, le processus de sélection de la meilleure copie et du serveur (BCSS) inclut plusieurs nouveaux contrôles d’intégrité qui font partie des composants de contrôle intégrés de la fonction de disponibilité gérée d’Exchange 2013. Il y a quatre nouveaux contrôles supplémentaires effectués par Active Manager (répertoriés dans l'ordre dans lequel ils sont effectués) :

1.  **Tous sains**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de contrôle est sain.

2.  **Jusqu’à une intégrité normale**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance ayant une priorité normale est intègre.

3.  **Tous meilleurs que la source**   Recherche un serveur hébergeant une copie de la base de données concernée dont l’état de tous les composants de surveillance est un meilleur que celui du serveur hébergeant actuellement la copie concernée.

4.  **Identique à la source**   Recherche un serveur hébergeant une copie de la base de données concernée dont tous les composants de contrôle sont dans le même état que le serveur hébergeant la copie concernée.

Si le processus de sélection de la meilleure copie et du serveur est appelé à la suite d’un basculement déclenché par un composant de contrôle (c.à.d. via un répondeur de basculement), une contrainte obligatoire supplémentaire est appliquée, selon laquelle l’état d’intégrité du composant du serveur cible doit être meilleur que celui du serveur où le basculement s’est produit. Par exemple, si une défaillance de Microsoft Office Outlook Web App déclenche un basculement via un répondeur de basculement, le processus de sélection de la meilleure copie et du serveur doit sélectionner un serveur qui héberge une copie de la base de données touchée dans laquelle l’état de Microsoft Office Outlook Web App est sain.

## Sélection de la meilleure copie

S'agissant des défaillances de bases de données (non des défaillances de protocoles), dans Exchange 2013, Active Manager effectue les mêmes contrôles que précédemmentt dans Exchange 2010. Le gestionnaire Active Manager commence le processus de sélection de la meilleure copie en créant une liste des copies de base de données pouvant être activées. Toute copie de base de données qui n'est pas joignable ou dont l'activation est bloquée administrativement est ignorée ; elle n'est pas utilisée lors de la sélection. L’ordre de la liste dépend de la valeur du paramètre *AutoDatabaseMountDial* :

  - Si le paramètre *AutoDatabaseMountDial* est configuré avec une valeur autre que `Lossless` sur tous les serveurs qui hébergent une copie de la base de données, Active Manager trie la liste obtenue en utilisant la longueur de la file d’attente de copie comme clé principale. Le calcul se base sur LastLogInspected (du point de vue de la copie) ; la liste des copies potentielles est donc triée d'après la valeur la plus élevée de LastLogInspected (qui est la copie ayant la plus petite longueur de la file d'attente de copie). Si nécessaire, Active Manager trie la liste une deuxième fois en utilisant la valeur de préférence d’activation comme clé secondaire pour mettre fin aux conditions de liaison où deux copies passives ou plus ont la même longueur de la file d’attente de copie. La copie ayant la plus petite valeur de préférence d’activation obtient la priorité supérieure dans la liste.

  - Si le paramètre *AutoDatabaseMountDial* est défini sur `Lossless` pour tous les serveurs qui hébergent une copie de la base de données, Active Manager trie la liste obtenue dans l’ordre croissant en utilisant la valeur de préférence d’activation comme clé principale. En outre, lorsqu’un administrateur exécute un basculement de serveur ou de base de données sans perte sans spécifier une cible, Active Manager trie également la liste obtenue dans l’ordre croissant en utilisant la valeur de préférence d’activation comme clé principale.

Ensuite, le gestionnaire Active Manager tente de trouver dans la liste une copie de base de données de boîtes aux lettres présentant un état Sain, Déconnecté et sain, Déconnecté et resynchronisation ou Source d’amorçage, puis il évalue le potentiel d’activation de chacune des copies dans la liste en utilisant dix ensembles de critères dans un ordre défini. Le gestionnaire Active Manager détermine si l’une des copies pouvant être activées correspond au premier ensemble de critères :

  - L'index de contenu présente un état Sain.

  - La longueur de la file d'attente de copie est inférieure à 10 fichiers journaux.

  - La longueur de sa file d’attente de relecture est inférieure à 50 fichiers journaux.

Si aucune des copies de base de données ne correspond au premier ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au deuxième ensemble de critères :

  - L'index de contenu présente un état Analyse.

  - La longueur de la file d'attente de copie est inférieure à 10 fichiers journaux.

  - La longueur de sa file d’attente de relecture est inférieure à 50 fichiers journaux.

Si aucune des copies de base de données ne correspond au deuxième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au troisième ensemble de critères :

  - L'index de contenu présente un état Sain.

  - La longueur de sa file d’attente de relecture est inférieure à 50 fichiers journaux.

Si aucune des copies de base de données ne correspond au troisième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au quatrième ensemble de critères :

  - L'index de contenu présente un état Analyse.

  - La longueur de sa file d’attente de relecture est inférieure à 50 fichiers journaux.

Si aucune des copies de base de données ne correspond au quatrième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au cinquième ensemble de critères :

  - La longueur de sa file d’attente de relecture est inférieure à 50 fichiers journaux.

Si aucune des copies de base de données ne correspond au cinquième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au sixième ensemble de critères :

  - L'index de contenu présente un état Sain.

  - La longueur de la file d'attente de copie est inférieure à 10 fichiers journaux.

Si aucune des copies de base de données ne correspond au sixième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au septième ensemble de critères :

  - L'index de contenu présente un état Analyse.

  - La longueur de la file d'attente de copie est inférieure à 10 fichiers journaux.

Si aucune des copies de base de données ne correspond au septième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au huitième ensemble de critères :

  - L'index de contenu présente un état Sain.

Si aucune des copies de base de données ne correspond au huitième ensemble de critères, le gestionnaire Active Manager tente de trouver une copie de base de données correspondant au neuvième ensemble de critères :

  - L'index de contenu présente un état Analyse.

Si aucune des copies de base de données ne correspond au neuvième ensemble de critères, le gestionnaire Active Manager tente d’activer une copie de base de données qui présente un état Sain, Déconnecté et sain, Déconnecté et resynchronisation ou Source d’amorçage (le dixième ensemble de critères). S’il ne parvient pas à trouver une copie de base de données correspondant au dixième ensemble de critères, il ne peut pas activer automatiquement une copie de base de données.

Après avoir trouvé des copies répondant à un ou à plusieurs ensembles de critères, le processus de tentative de copie des derniers journaux s’exécute pour copier tous les fichiers journaux de la source d’origine dans la nouvelle copie active potentielle. Une fois ce processus arrivé à son terme, le gestionnaire Active Manager principal émet une demande de montage. Lorsque cela est fait, soit la base de données est montée et rendue accessible aux clients, soit elle n’est pas montée et le gestionnaire Active Manager principal recherche la meilleure copie suivante (si disponible).

