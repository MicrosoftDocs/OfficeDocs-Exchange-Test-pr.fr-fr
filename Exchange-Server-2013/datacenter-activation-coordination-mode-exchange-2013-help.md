---
title: 'Mode de coordination de l’activation du centre de données: Exchange 2013 Help'
TOCTitle: Mode de coordination de l’activation du centre de données
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 50478249
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mode de coordination de l’activation du centre de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-07-14_

Le mode de coordination de l’activation du centre de données est une propriété de groupe de disponibilité de base de données. Ce mode est désactivé par défaut et doit être activé pour tous les groupes de disponibilité de base de données constitués d’au moins deux membres qui utilisent la réplication continue. Il ne doit pas être activé pour les groupes de disponibilité de base de données en mode de réplication tierce, sauf indication contraire du fournisseur tiers.

Le mode de coordination de l’activation du centre de données permet de contrôler le montage de la base de données au niveau du comportement de démarrage d’un groupe de disponibilité de base de données. Ce contrôle est conçu pour empêcher les situations de Split-Brain au niveau de la base de données lors d’un retour vers une ancienne version d’un centre de données. Une situation de Split-Brain, aussi connue sous le nom de « syndrome Split-Brain », entraîne le montage d’une copie de base de données en tant que copie active sur deux membres du même groupe de disponibilité de base de données qui ne parviennent pas à communiquer. Le mode de coordination de l’activation du centre de données permet d’éviter le syndrome Split-Brain, car ce mode exige que les membres du groupe de disponibilité de base de données obtiennent l’autorisation de monter les bases de données avant de pouvoir le faire.

Par exemple, considérez un scénario pour lequel le centre de données principal contient deux membres d’un groupe de disponibilité de base de données et le serveur témoin, et un second centre de données contient deux autres membres d’un groupe de disponibilité de base de données. Dans ce scénario, le groupe de disponibilité de base de données n’est pas en mode de coordination de l’activation du centre de données. Le centre de données principal subit une coupure d’alimentation ; vous activez donc le groupe de disponibilité de base de données dans le second centre de données. L’alimentation du centre de données principal est finalement rétablie et les membres du groupe de disponibilité de base de données de ce centre, qui disposaient du quorum avant la panne de courant, vont démarrer et monter leurs bases de données. Étant donné que le centre de données principal a été restauré sans connectivité réseau vers le second centre de données et que le groupe de disponibilité de base de données n’était pas en mode de coordination de l’activation du centre de données, les bases de données actives au sein du groupe de disponibilité de base de données se retrouvent dans une situation de Split-Brain.

## Fonctionnement du mode de coordination de l’activation du centre de données

Le mode de coordination de l’activation du centre de données est conçu pour empêcher les situations de « split brain » en incluant un protocole appelé DACP (Activation Coordination Protocol). Lorsque le mode de coordination de l’activation du centre de données est activé, les membres du groupe de disponibilité de base de données ne montent pas automatiquement les bases de données, même si elles disposent d’un quorum. Au lieu de cela, le protocole DACP est utilisé pour déterminer l’état en cours du groupe de disponibilité de base de données et si Active Manager doit essayer de monter les bases de données.

Vous pouvez envisager le mode de coordination de l’activation du centre de données comme niveau d’application du quorum pour le montage des bases de données. Pour comprendre l’utilité du protocole DACP et son mode de fonctionnement, il est essentiel de bien comprendre sa fonction principale. Envisagez le scénario à deux centres de données. Supposons qu’il s’agit d’une panne totale d’alimentation dans le centre de données principal. Dans ce cas, tous les serveurs et le réseau WAN sont en panne. De fait, l’organisation peut décider d’activer le centre de données de secours. Dans la plupart des scénarios de récupération, lorsque l’alimentation est restaurée dans le centre de données principal, la connectivité WAN n’est, en général, pas immédiatement restaurée. Ceci signifie que les membres du groupe de disponibilité de base de données seront sous tension mais ne pourront pas communiquer avec les membres du groupe de disponibilité de base de données dans le centre de données de secours activé. Le centre de données principal devrait toujours contenir la majorité des votants du quorum du groupe de disponibilité de base de données, ce qui signifie que lorsque l’alimentation est restaurée, même en l’absence de connectivité WAN aux membres du groupe de disponibilité de base de données dans le centre de données de secours, les membres du groupe de disponibilité de base de données du centre de données principal ont la majorité et par conséquent le quorum. Il s’agit d’un problème car avec le quorum, ces serveurs peuvent monter leurs bases de données, ce qui risque de provoquer une divergence à partir des bases de données actives réelles qui sont désormais montées dans le centre de données de secours activé.

DACP a été créé pour résoudre ce problème. Active Manager stocke un bit en mémoire (0 ou 1) qui indique si le groupe de disponibilité de base de données est autorisé à monter des bases de données locales attribuées comme actives sur le serveur. Lorsqu’un groupe de disponibilité de base de données s’exécute en mode de coordination de l’activation du centre de données et chaque fois qu’Active Manager démarre, le bit est défini sur 0, ce qui signifie qu’il n’est pas autorisé à monter les bases de données. Puisque le mode de coordination de l’activation du centre de données est activé, le serveur doit essayer de communiquer avec tous les autres membres du groupe de disponibilité de base de données qu’il connaît pour obtenir un autre membre du groupe de disponibilité afin de lui fournir une réponse pour qu’il sache s’il peut monter des bases de données locales qui lui sont attribuées comme étant actives. La réponse est fournie sous la forme d’un paramètre de bit pour d’autres serveurs Active Manager dans le groupe de disponibilité de base de données. Si un autre serveur répond que son bit est défini à 1, cela signifie que les serveurs sont autorisés à monter des bases de données. Ainsi, au démarrage, le serveur définit son bit à 1 et monte ses bases de données.

Cependant, lorsque vous effectuez une récupération après une coupure de courant du centre de données principal et dans le cas où les serveurs ont été récupérés mais que la connectivité WAN n’a pas été restaurée, tous les membres du groupe de disponibilité de base de données dans le centre de données principal auront une valeur de bit DACP définie à 0. Par conséquent, aucun des serveurs effectuant la sauvegarde dans le centre de données principal récupéré ne montera les bases de données parce qu’aucun d’entre eux ne peut communiquer avec un membre du groupe de disponibilité de base de données ayant une valeur de bit DACP définie à 1.

## Mode de coordination de l’activation du centre de données pour les groupes de disponibilité de base de données comptant deux membres

Les groupes de disponibilité de base de données ayant deux membres comportent des limitations qui empêchent le bit DACP seul d’être pleinement protégé contre le syndrome de « split brain » au niveau de l’application. Pour un groupe de disponibilité de base de données comptant uniquement deux membres, le mode de coordination de l’activation du centre de données utilise également l’heure d’amorçage du serveur témoin du groupe pour déterminer s’il peut monter des bases de données au démarrage. L’heure d’amorçage du serveur témoin est comparée à celle à laquelle le bit DACP a été défini sur 1.

  - Si l’heure de définition du bit DACP est antérieure à l’heure d’amorçage du serveur témoin, le système part du principe que le membre DAG et le serveur témoin ont été redémarrés en même temps (probablement en raison d’une panne de courant du centre de données principal), et le membre n’est donc pas autorisé à monter des bases de données.

  - Si l’heure à laquelle le bit DACP a été défini est plus récente que l’heure d’amorçage du serveur témoin, le système suppose que le membre DAG a été redémarré pour une autre raison (peut-être une interruption programmée durant laquelle une opération de maintenance a été menée, un blocage du système ou une panne de courant isolée du membre DAG) et l’autorise à monter des bases de données.

> [!IMPORTANT]
> Dans la mesure où l’heure d’amorçage du serveur témoin permet de déterminer si un membre DAG peut monter ses bases de données actives au démarrage, vous ne devez jamais redémarrer simultanément le serveur témoin et le membre DAG. Sinon, le membre du DAG sera dans l’incapacité de monter les bases de données au démarrage. Si cela se produit, vous devez exécuter la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</a> sur le groupe de disponibilité de base de données. Le bit DACP sera alors réinitialisé et le membre DAG pourra monter les bases de données.


## Autres avantages du mode de coordination de l’activation du centre de données

Outre la prévention du syndrome de « split brain » au niveau de l’application, le mode de coordination de l’activation du centre de données permet d’utiliser les cmdlets intégrées de résilience de site pour effectuer des permutations de centre de données. parmi lesquelles  :

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd335076\(v=exchg.150\))

L’exécution d’une permutation de centre de données pour les groupes de disponibilité de base de données non définis en mode de coordination d’activation du centre de données implique l’utilisation d’une combinaison d’outils Exchange et d’outils de gestion de clusters. Pour plus d’informations, voir [Switchovers de centre de données](datacenter-switchovers-exchange-2013-help.md).

## Activation du mode de coordination de l’activation du centre de données

Le mode de coordination de l’activation du centre de données peut être activé uniquement à l’aide de l’environnement de ligne de commande Exchange Management Shell. Plus spécifiquement, vous pouvez utiliser la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) pour activer le mode de coordination de l’activation du centre de données, comme illustré dans l’exemple suivant.

    Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly

Dans l’exemple précédent, DAG2 est activé pour le mode de coordination d’activation du centre de données.

Pour plus d’informations sur le fonctionnement du mode de coordination de l’activation du centre de données, voir [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md) et [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)).

