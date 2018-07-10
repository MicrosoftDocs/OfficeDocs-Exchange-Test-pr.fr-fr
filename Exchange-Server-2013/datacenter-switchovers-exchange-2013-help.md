---
title: 'Switchovers de centre de données: Exchange 2013 Help'
TOCTitle: Switchovers de centre de données
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523887
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Switchovers de centre de données

 

_**Sapplique à :** Exchange Server 2013 SP1_

_**Dernière rubrique modifiée :** 2016-03-17_

Dans une configuration de résilience de site, la récupération automatique suite à une défaillance au niveau du site peut se produire dans un DAG, ce qui permet au système de messagerie de conserver un état fonctionnel. Cette configuration nécessite au moins trois emplacements, car elle nécessite le déploiement de membres du DAG dans deux emplacements et le déploiement du serveur témoin du DAG dans un troisième emplacement.

Si vous ne disposez pas de trois emplacements, ou si vous disposez de trois emplacements mais que vous voulez contrôler les actions de récupération au niveau du centre de données, vous pouvez configurer un DAG pour une récupération manuelle en cas de défaillance au niveau du site. Dans ce cas, vous devez exécuter un processus appelé *permutation de centre de données*. Comme dans de nombreux scénarios de récupération d’urgence, la planification et la préparation préliminaires d’une permutation de centre de données permettent de simplifier le processus de récupération et de réduire la durée de la panne.

Une opération de permutation de centre de données s'articule en quatre étapes principales, une fois que vous avez décidé d'activer le deuxième centre de données :

1.  **Fermeture d’un centre de données exécuté partiellement**   Cette étape implique l’arrêt des services Exchange dans le centre de données principal, si ces derniers sont toujours en cours d’exécution. Cette étape est particulièrement importante pour le rôle serveur de boîtes aux lettres, car elle utilise un modèle haute disponibilité actif/passif. Si les services d'un centre de données partiellement défaillant ne sont pas arrêtés, il est possible que les problèmes de ce centre aient un impact négatif sur les services lors d'une nouvelle permutation vers le centre de données principal.
    
    > [!NOTE]
    > Si la fiabilité du réseau ou de l'infrastructure Active Directory a été compromise suite à une défaillance du centre de données principal, nous vous recommandons d'arrêter tous les services de messagerie jusqu'au rétablissement de l'intégrité de ces dépendances.


2.  **Validation et vérification des conditions requises pour le deuxième centre de données**   Cette étape peut être exécutée en parallèle à l'étape 1, car la validation de l'intégrité des dépendances de l'infrastructure dans le deuxième centre de données est largement distincte des services du premier centre de données. Chaque organisation requiert généralement sa propre méthode pour effectuer cette opération. Par exemple, vous pouvez effectuer cette opération en vérifiant les informations d'intégrité collectées et filtrées par une application d'analyse d'infrastructure ou à l'aide d'un outil spécialement adapté à l'infrastructure de votre organisation. Cette étape est essentielle, car l'activation du deuxième centre de données lorsque son infrastructure est défectueuse et instable peut produire des résultats médiocres.

3.  **Activation des serveurs de boîtes aux lettres**   Cette étape marque le début du processus d'activation du deuxième centre de données. Elle peut être exécutée en parallèle à l'étape 4, car les services Microsoft Exchange peuvent gérer les pannes et la récupération de la base de données. L'activation des serveurs de boîtes aux lettres implique que les serveurs défaillants du centre de données principal soient marqués comme indisponibles avant l'activation des serveurs du deuxième centre de données. Le processus d'activation des serveurs de boîtes aux lettres diffère selon si le groupe de disponibilité de base de données (DAG) est en mode de coordination d'activation de la base de données (DAC) ou non. Pour plus d'informations sur le mode de coordination de l'activation de la base de données, voir [Mode de coordination de l’activation du centre de données](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
    Si le DAG est en mode de coordination d'activation de la base de données (DAC), vous pouvez utiliser les cmdlets de résilience de site d'Exchange pour fermer un centre de données partiellement défaillant (si nécessaire) et activer les serveurs de boîtes de données. Par exemple, en mode de coordination d'activation de la base de données, cette opération s'effectue à l'aide de la cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd335133\(v=exchg.150\)). Dans certains cas, les serveurs doivent être marqués comme indisponibles à deux reprises (une fois dans chaque centre de données). La cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351169\(v=exchg.150\)) est ensuite exécutée pour restaurer les autres membres du DAG dans le deuxième centre de données en réduisant le nombre de membres du DAG à ceux qui sont toujours opérationnels, rétablissant ainsi le quorum. Si le DAG n'est pas en mode de coordination d'activation de la base de données, vous devez utiliser les outils de cluster de basculement Windows pour activer les serveurs de boîtes aux lettres. Lorsqu'un processus est terminé, les copies de base de données qui étaient auparavant passives dans le deuxième centre de données peuvent devenir actives et être montées. À ce stade, la récupération du serveur de boîtes aux lettres est terminée.

4.  **Activation des serveurs d’accès au client**   Cette étape suppose l’utilisation des informations de mappage des URL et de la méthodologie de changement DNS (Domain Name System) pour effectuer toutes les mises à jour de DNS requises. Les informations de mappage décrivent les modifications à apporter au DNS. La durée nécessaire pour effectuer la mise à jour dépend de la méthode utilisée et des paramètres de durée de vie (TTL) sur l'enregistrement DNS (et du respect ou non de la durée de vie par l'infrastructure de déploiement).

Les utilisateurs doivent avoir accès aux services de messagerie une fois les étapes 3 et 4 terminées. Les étapes 3 et 4 sont décrites en détail plus loin dans cette rubrique.

**Contenu de cette rubrique**

Fermeture d'un centre de données partiellement défaillant

Activation des serveurs de boîtes aux lettres

Activation des serveurs d'accès au client

Restauration du service dans le centre de données principal

Rétablissement de la résilience de site

## Fermeture d'un centre de données partiellement défaillant

Si les membres du groupe de disponibilité de base de données (DAG) du centre de données défaillant sont toujours en cours d'exécution, ils doivent être arrêtés.

Lorsque le DAG est en mode de coordination d'activation de la base de données (DAC), les actions permettant d'arrêter les membres survivants du DAG dans le centre de données principal sont les suivantes :

1.  Les membres du DAG du centre de données principal doivent être marqués comme arrêtés. *Arrêté* est un état d’Active Manager qui empêche le montage des bases de données. Le gestionnaire Active Manager de chaque serveur du centre de données défaillant est placé dans cet état à l’aide de la cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd335133\(v=exchg.150\)). Le paramètre *ActiveDirectorySite* de cette cmdlet permet de marquer l'ensemble des serveurs du centre de données principal comme arrêtés à l'aide d'une seule commande. En fonction de la nature de la panne, il est possible que vous ne puissiez pas effectuer cette opération. Elle doit être effectuée si l'état du centre de données le permet. La cmdlet **Stop-DatabaseAvailabilityGroup** doit être exécutée sur tous les serveurs du centre de données principal. Si le serveur de boîtes aux lettres n'est pas disponible, alors que Active Directory est exécuté dans le centre de données principal, vous devez exécuter la commande **Stop-DatabaseAvailabilityGroup** avec le paramètre *ConfigurationOnly* sur tous les serveurs se trouvant dans cet état dans le centre de données principal. Sinon, vous devez désactiver le serveur de boîtes aux lettres. Si vous ne désactivez pas les serveurs de boîtes aux lettres dans le centre de données défaillant ou si vous n'exécutez pas la commande **Stop-DatabaseAvailabilityGroup** sur les serveurs, un syndrome de « split-brain » peut se produire dans les deux centres de données. Il se peut alors que vous deviez arrêter individuellement les ordinateurs via les appareils de gestion de l'alimentation pour satisfaire cette exigence.

2.  Le deuxième centre de données doit maintenant être mis à jour pour représenter les serveurs du centre de données principal qui sont arrêtés. Cette opération est effectuée en exécutant à nouveau la commande **Stop-DatabaseAvailabilityGroup** avec le paramètre *ConfigurationOnly* à l'aide du même paramètre *ActiveDirectorySite* et en spécifiant le nom du site Active Directory du centre de données principal défaillant. Cette étape vise à informer les serveurs du deuxième centre de données des serveurs de boîtes aux lettres qui peuvent être utilisés pour restaurer le service.

Lorsque le DAG n'est pas en mode de coordination d'activation de la base de données (DAC), les actions permettant d'arrêter les membres survivants du DAG dans le centre de données principal sont les suivantes :

1.  Les membres du DAG du centre de données principal doivent être supprimés du cluster sous-jacent du DAG en exécutant les commandes suivantes sur chaque membre :
    
        net stop clussvc
        cluster <DAGName> node <DAGMemberName> /forcecleanup

2.  Les membres du DAG du deuxième centre de données doivent maintenant être redémarrés, puis utilisés pour effectuer le processus de suppression des serveurs du deuxième centre de données. Arrêtez le service de cluster sur chaque membre du DAG dans le deuxième centre de données en exécutant la commande suivante sur chaque membre :
    
        net stop clussvc

3.  Sur un membre du DAG dans le deuxième centre de données, démarrez le service de cluster en forçant le quorum. Pour cela, exécutez la commande suivante :
    
        net start clussvc /forcequorum

4.  Ouvrez l'outil Gestion du cluster de basculement.et connectez-vous au cluster sous-jacent du DAG. Développez le nœud de cluster, puis les **Nœuds**. Cliquez avec le bouton droit sur chaque nœud du centre de données principal, sélectionnez **Actions supplémentaires**, puis **Supprimer**. Lorsque vous supprimez les membres du DAG du centre de données principal, fermez l'outil Gestion du cluster de basculement.

Retour au début

## Activation des serveurs de boîtes aux lettres

Les étapes nécessaires pour activer les serveurs de boîtes aux lettres au cours d'une permutation de centre de données diffèrent également selon si le DAG est en mode de coordination d'activation de la base de données (DAC) ou non. Avant d'activer les membres du DAG du deuxième centre de données, assurez-vous que les services d'infrastructure dans le deuxième centre de données sont prêts pour l'activation du service de messagerie.

Lorsque le DAG est en mode DAC, pour terminer l'activation des serveurs de boîtes aux lettres dans le deuxième centre de données, procédez comme suit :

1.  Vous devez arrêter le service de cluster sur chaque membre du DAG dans le deuxième centre de données. Vous pouvez utiliser la cmdlet **Stop-Service** pour arrêter le service (par exemple, `Stop-Service ClusSvc`), ou bien `net stop clussvc` à partir d'une invite de commandes avec élévation de privilèges.

2.  Vous devez ensuite activer les serveurs de boîtes aux lettres présents dans le centre de données de secours à l'aide de la cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351169\(v=exchg.150\)). Le site Active Directory du centre de données de secours est transmis à la cmdlet **Restore-DatabaseAvailabilityGroup** pour identifier les serveurs à utiliser pour restaurer le service et configurer le groupe de disponibilité de base de données à utiliser comme autre serveur témoin. Si l’autre serveur témoin n’a pas été configuré auparavant, vous pouvez le configurer à l’aide des paramètres *AlternateWitnessServer* et *AlternateWitnessDirectory* de la cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd351169\(v=exchg.150\)). Si cette commande réussit, les critères du quorum sont réduits aux serveurs du centre de données de secours. Si les serveurs de ce centre de données existent en nombre pair, le DAG utilisera l'autre serveur témoin identifié par le paramètre sur l'objet DAG.

3.  Vous pouvez à présent activer les bases de données. Selon la configuration spécifique utilisée par l'organisation, il est possible que cette opération ne soit pas automatique. Si le paramètre d'activation des serveurs du centre de données de secours est bloqué, le système n'effectuera pas de basculement automatique du centre de données principal vers le centre de données de secours d'une base de données. Si aucune restriction de basculement n'existe pour l'une des copies de bases de données dans le centre de données de secours, le système activera les copies du deuxième centre de données en supposant qu'elles sont saines. Si les bases de données sont configurées avec un paramètre d'activation bloqué qui nécessite une intervention manuelle explicite, vous pouvez procéder de deux manières :
    
    1.  Désactivez le paramètre qui bloque l'activation. Le comportement par défaut du système, c'est à dire, l'activation d'une copie disponible, sera alors rétabli.
    
    2.  Laissez le paramètre inchangé et utilisez la cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)) pour effectuer l'activation de la base de données dans le deuxième centre de données. Pour effectuer cette étape à l'aide de la cmdlet **Move-ActiveMailboxDatabase** lorsque l'activation bloquée est définie, vous devez identifier explicitement la cible à déplacer.

4.  La dernière étape consiste à analyser tous les messages d'erreur et d'avertissement résultant des tâches. Tous les avertissements indiqués doivent être suivis et corrigés. Le modèle de conception des tâches pour ces commandes n'échouera que si elles ne peuvent pas atteindre l'objectif premier de leur conception. Par exemple, la cmdlet **Restore-DatabaseAvailabilityGroup** échouera si elle ne parvient pas à réduire le quorum du DAG pour permettre le redémarrage du deuxième centre de données à des fins de traitement sans provoquer une panne du quorum. Cependant, le résultat de chaque tâche doit être également utilisé pour identifier les problèmes nécessitant un suivi de la part de l'administrateur. Nous vous conseillons vivement d'enregistrer les résultats de toutes les tâches et de les analyser pour déterminer les actions de suivi.

Lorsque le DAG n'est pas en mode DAC, pour terminer l'activation des serveurs de boîtes aux lettres dans le deuxième centre de données, procédez comme suit :

1.  Le quorum doit être modifié pour refléter le nombre de membres du DAG du deuxième centre de données.
    
    1.  Si le nombre des membres du DAG est impair, remplacez le modèle de quorum du DAG « Nœud et partage de fichiers majoritaires » par « Nœud majoritaire » en exécutant la commande suivante :
        
            cluster <DAGName> /quorum /nodemajority
    
    2.  Si le nombre des membres du DAG est pair, reconfigurez le serveur témoin et le répertoire témoin en exécutant la commande suivante dans l'environnement de ligne de commande Exchange Management Shell :
        
            Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>

2.  Démarrez le service de cluster sur les membres restants du DAG dans le deuxième centre de données en exécutant la commande suivante :
    
        net start clussvc

3.  Procédez aux permutations de serveurs pour activer les bases de données de boîtes aux lettres dans le DAG en exécutant la commande suivante pour chaque membre du DAG :
    
        Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>

4.  Montez les bases de données de boîtes aux lettres sur chaque membre du DAG dans le deuxième site en exécutant la commande suivante :
    
        Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database

Retour au début

## Activation des serveurs d'accès au client

Les clients se connectent aux points de terminaison de service (par exemple Outlook Web App, le service de découverte automatique Autodiscover, Exchange ActiveSync, Outlook Anywhere, POP3, IMAP4 et le groupe d’accès au client RPC) pour accéder aux services et aux données Exchange. L’activation des serveurs d’accès au client implique donc de modifier le mappage des enregistrements DNS pour ces points de terminaison de service entre les adresses IP dans le centre de données principal et les adresses IP du deuxième centre de données qui ont été configurées comme nouveaux points de terminaison de service. Selon votre configuration DNS, les enregistrements DNS à modifier peuvent ou non se trouver dans la même zone DNS.

## Activation des serveurs d’accès au client

Les clients se connectent ensuite automatiquement aux nouveaux points de terminaison de service d'une des manières suivantes :

  - Les clients continuent à tenter de se connecter et ils doivent se connecter automatiquement une fois que la durée de vie a expiré pour l'entrée DNS d'origine et que l'entrée a expiré dans leur cache DNS. Les utilisateurs peuvent également exécuter la commande `ipconfig /flushdns` à partir d'une invite de commandes pour effacer manuellement leur cache DNS.

  - Les clients qui démarrent ou redémarrent effectuent une recherche DNS au démarrage et obtiennent la nouvelle adresse IP pour le point de terminaison de service, qui représente un serveur ou un groupe de serveurs d'accès au client du deuxième centre de données.

En supposant que toutes les modifications de configuration appropriées ont été apportées pour définir et configurer les services dans le deuxième centre de données de manière à ce qu'ils fonctionnent de la même manière que dans le centre de données principal, et en partant du principe que la configuration DNS définie est correcte, aucune autre modification ne sera nécessaire pour activer les serveurs d'accès au client.

## Activation des services de transport

Les clients et autres serveurs qui envoient des messages identifient généralement ces serveurs via DNS. Pour activer les services de transport dans le deuxième centre de données, vous devez modifier les enregistrements DNS afin qu’ils pointent vers les adresses IP des serveurs de boîtes aux lettres du deuxième centre de données. Les clients et les serveurs d’envoi se connecteront ensuite automatiquement aux serveurs du deuxième centre de données d’une des manières suivantes :

  - Les clients continuent à tenter de se connecter et ils doivent se connecter automatiquement une fois que la durée de vie a expiré pour l'entrée DNS d'origine et que l'entrée a expiré dans leur cache DNS. Les utilisateurs peuvent également exécuter la commande `ipconfig /flushdns` à partir d'une invite de commandes pour effacer manuellement leur cache DNS.

  - Les clients qui démarrent ou redémarrent effectuent une recherche DNS au démarrage et obtiennent la nouvelle adresse IP pour le point de terminaison SMTP, qui représente un serveur de boîtes aux lettres du deuxième centre de données.

En supposant que toutes les modifications de configuration appropriées ont été apportées pour définir et configurer les services dans le deuxième centre de données de manière à ce qu’ils fonctionnent de la même manière que dans le centre de données principal, et en partant du principe que la configuration DNS définie est correcte, aucune autre modification supplémentaire ne sera nécessaire pour activer les services de transport.

## Activation des serveurs de messagerie unifiée

Les services de messagerie unifiée (MU) se connectent au système PBX et aux lignes téléphoniques d’une organisation. La connexion logique entre le système PBX et le service de messagerie unifiée est établie par une passerelle IP. Les passerelles IP incluent une fonctionnalité de haute disponibilité et peuvent basculer entre plusieurs services de messagerie unifiée lorsqu’une défaillance est détectée.

Si des services de messagerie unifiée du deuxième centre de données se trouvaient dans un état désactivé du fait qu’ils sont dédiés à la solution de résilience de site, vous pouvez les activer à l’aide de la cmdlet [Activé-UMService](https://technet.microsoft.com/fr-fr/library/jj552411\(v=exchg.150\)) (par exemple, `Enable-UMService EX4`).

En supposant que les passerelles IP sont associées aux services de messagerie unifiée à l’aide de serveurs DNS, l’activation des services de messagerie unifiée requiert donc la modification des enregistrements DNS afin qu’ils pointent vers les nouvelles adresses IP qui seront configurées pour le service de messagerie unifiée du deuxième centre de données. En supposant que toutes les modifications de configuration appropriées ont été apportées pour définir et configurer les services dans le deuxième centre de données de manière à ce qu’ils fonctionnent de la même manière que dans le centre de données principal, et en partant du principe que la configuration DNS définie est correcte, aucune autre modification supplémentaire ne sera nécessaire pour activer les services de messagerie unifiée.

Si la passerelle IP utilisée ne prend pas en charge les noms DNS pour résoudre les services de messagerie unifiée, des étapes de configuration manuelle supplémentaires seront nécessaires pour que la passerelle IP pointe vers les adresses IP des services de messagerie unifiée dans le deuxième centre de données.

## Activation des serveurs de transport Edge

Les étapes d'activation du rôle serveur de transport Edge varient en fonction de la configuration choisie. Vous pouvez configurer les serveurs de transport Edge de deux centres de données en mode actif/passif ou actif/actif. Dans une configuration active/passive, le serveur de transport Edge du deuxième centre de données est inactif tant que le deuxième centre de données n'a pas été activé. Dans une configuration active/active, les serveurs de transport Edge des deux centres de données délivrent le courrier en permanence.

Dans une configuration active/active, aucune étape n'est nécessaire pour activer les serveurs de transport Edge du deuxième centre de données, car ils sont déjà en cours d'exécution. Dans une configuration active/passive, vous devez mettre l'enregistrement de ressource DNS MX de chaque domaine SMTP à jour dans le cadre de la permutation du centre de données principal avec le centre de données de secours. Bien que la configuration de type actif/actif constitue une solution de permutation de centre de données simple, elle exige un suivi attentif de la charge pour qu'une fois le centre de données permuté, les serveurs de transport Edge du deuxième centre de données puissent offrir une capacité suffisante pour supporter la charge accrue qui lui est maintenant imposée en conséquence de l'indisponibilité des serveurs de transport Edge dans le centre de données principal.

Même dans une configuration de type actif/actif, il peut être nécessaire de mettre les enregistrements de ressources MX à jour pour vos serveurs de transport Edge lors d'une permutation du centre de données. Si l'enregistrement de ressource MX du centre de données défaillant continue à pointer vers ce dernier et que la récupération du centre de données commence, il peut être confronté à des tentatives de connexion avec ses serveurs de transport Edge. Cette situation peut se produire lorsque les services de transport Edge sont instables (par exemple, en raison de la restauration des services dépendants dans le centre de données).

En supposant que les enregistrements DNS sont contrôlés par l'organisation, l'activation des serveurs de transport Edge implique la mise à jour de l'enregistrement de ressource MX pour chaque domaine SMTP hébergé par le serveur.

> [!NOTE]
> Si l'enregistrement de ressource MX utilisé par votre organisation n'est pas hébergé par un serveur DNS contrôlé par celle-ci, il est préférable de référencer un enregistrement CNAME dans l'enregistrement de ressource MX et d'utiliser un enregistrement CNAME contrôlé par l'organisation que vous pourrez ensuite mettre à jour.


Les mises à jour du DNS autorisent le trafic entrant, et le trafic sortant est géré par l'activation des bases de données de boîtes aux lettres dans un site contenant des serveurs de transport Edge opérationnels :

  - Lorsque les connexions SMTP entrantes sont établies à l'aide des informations de résolution de noms mises à jour, les clients SMTP se connectent aux serveurs de transport Edge du deuxième centre de données. Le trafic est routé de façon appropriée par le serveur de transport Edge et aucune modification supplémentaire n'est nécessaire.

  - Lorsque les connexions SMTP sortantes sont établies, elles effectuent une tentative sur le serveur de transport Edge local disponible, et ces messages sont mis en file d'attente ou immédiatement envoyés en fonction de l'état du serveur de réception.

Retour au début

## Restauration du service dans le centre de données principal

En règle générale, les défaillances du centre de données sont temporaires ou permanentes. Dans le cas d'une défaillance permanente, tel qu'un tel événement ayant provoqué la destruction permanente d'un centre de données principal, le centre de données principal n'a aucune chance d'être activé. Cependant, dans le cas d'une défaillance temporaire (par exemple, une panne de courant générale ou des dommages importants, mais réparables), le centre de données aura des chances d'être pleinement rétabli.

Le processus de restauration du service dans un centre de données auparavant défaillant s'appelle une *commutation*. Les étapes de commutation d'un centre de données défaillant sont similaires à celles d'une permutation de centre de données. La seule différence significative est que les commutations de centres de données sont planifiées et la panne est souvent d'une durée beaucoup plus courte.

Il est essentiel que la commutation soit effectuée une fois les dépendances de l'infrastructure d'Exchange réactivées, opérationnelles, stables et validées. Si ces dépendances ne sont pas disponibles ou saines, il est probable que le processus de commutation provoque une panne plus longue que nécessaire et que le processus échoue.

## Commutation du rôle serveur de boîtes aux lettres

Le rôle serveur de boîtes aux lettres doit être le premier rôle commuté dans le centre de données principal. Les étapes suivantes analysent de manière détaillée le processus de commutation du rôle serveur de boîtes aux lettres :

1.  Dans le cadre du processus de permutation du centre de données, les serveurs de boîtes aux lettres du centre de données principal ont été placés à l'état d'arrêt. Lorsque l'environnement (tel que le centre de données principal, les dépendances d'Exchange et la connectivité du réseau étendu (WAN)) est prêt, la première étape consiste à placer les serveurs de boîtes aux lettres dans le centre de données principal restauré à l'état démarré et à les intégrer au DAG. La manière dont cela est réalisé diffère selon si le DAG est en mode de coordination d'activation de la base de données (DAC) ou non.
    
    1.  Si le DAG est en mode DAC, vous pouvez réincorporer les membres du DAG dans le site principal à l'aide de la cmdlet [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd335076\(v=exchg.150\)). Ensuite, pour vous assurer que le modèle de quorum utilisé par le groupe de disponibilité de base de données est le bon, exécutez la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) sur ce dernier sans définir aucun paramètre.
    
    2.  Si le DAG n'est pas en mode DAC, vous pouvez réincorporer les membres du DAG à l'aide de la cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd298049\(v=exchg.150\)).

2.  Une fois que les serveurs de boîtes aux lettres du centre de données principal ont été intégrés dans le DAG, ils ont besoin de temps pour synchroniser leurs copies de base de données. Selon la nature de l'erreur, la durée de la panne et les actions menées par un administrateur durant la panne, un réamorçage des copies de base de données peut s'avérer nécessaire. Par exemple, si au cours de la panne, vous supprimez les copies de base de données du centre de donnés principal défaillant pour permettre la troncature des fichiers journaux pour les copies actives valides dans le deuxième centre de données, un réamorçage sera nécessaire. Chaque base de données peut continuer individuellement à partir de ce point. Une fois que la copie de base de données répliquée du centre de données principal est saine, elle peut passer à l'étape suivante.
    
    > [!NOTE]
    > Ce processus ne nécessite pas le déplacement simultané de toutes les bases de données. Nous vous conseillons de déplacer simultanément la plupart des bases de données de votre organisation. Toutefois, certaines bases de données peuvent rester dans le deuxième centre de données s'il existe des problèmes associés aux copies de base de données dans le centre de données principal.


3.  Si la plupart des bases de données sont saines dans le centre de données principal, vous pouvez planifier le processus de commutation. Lorsque l'heure planifiée parvient à échéance, vous devez effectuer les opérations suivantes :
    
    1.  Lors du processus de permutation du centre de données, le DAG a été configuré pour utiliser un autre serveur témoin. Vous devez reconfigurer le DAG afin qu'il utilise un serveur témoin dans le centre de données principal. Si vous utilisez le même serveur et répertoire témoin qu'avant la panne du centre de données principal, vous pouvez exécuter la commande `Set-DatabaseAvailabilityGroup -Identity DAGName`. Si vous envisagez d’utiliser un serveur témoin ou un répertoire témoin différent du serveur ou répertoire témoin d’origine, utilisez la commande [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) pour configurer les paramètres de ce serveur et de ce répertoire témoin avec les valeurs adéquates.
    
    2.  Les bases de données réactivées dans le centre de données principal doivent être démontées dans le deuxième centre de données. Pour cela, vous pouvez utiliser la cmdlet [Dismount-Database](https://technet.microsoft.com/fr-fr/library/bb124936\(v=exchg.150\)).
    
    3.  Une fois les bases de données démontées, les URL du serveur d'accès au client doivent être déplacées du deuxième centre de données vers le centre de données principal. Pour cela, vous devez modifier l'enregistrement DNS des URL afin qu'il pointe vers le serveur d'accès au client ou le groupe de serveurs d'accès au client dans le centre de données principal. Le système réagira comme si un basculement de base de données s'était produit pour chaque base de données déplacée.
        
        > [!NOTE]
        > Ne passez à l'étape suivante qu'une fois que les URL du serveur d'accès au client ont été déplacées et que les entrées du cache DNS et TTL ont expirée. L'activation des bases de données dans le centre de données principal avant le déplacement des URL du serveur d'accès au client vers le centre de données invalidera la configuration (par exemple, une base de données montée ne comportant aucun serveur d'accès au client dans son site Active Directory).
    
    4.  Étant donné que chacune des bases de données du centre de données principal est saine, elles peuvent être activées dans ce dernier en procédant à leur permutation. Cette opération est effectuée à l'aide de la cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/fr-fr/library/dd298068\(v=exchg.150\)) pour chaque base de données à activer.
    
    5.  Après avoir déplacé chaque base de données vers le centre de données principal, vous pouvez les monter à l'aide de la cmdlet [Mount-Database](https://technet.microsoft.com/fr-fr/library/aa998871\(v=exchg.150\)).

Lorsqu'une ou plusieurs bases de données sont actives et montées dans le centre de données principal, vous pouvez exécuter les procédures de commutation des autres rôles serveur.

## Commutation du serveur d’accès au client

Dans le cadre du processus de permutation, les enregistrements DNS internes et externes utilisés par les clients, d’autres serveurs, et les passerelles IP pour résoudre les points de terminaison de service pour les serveurs d’accès au client, les services de transport et de messagerie unifiée et les serveurs de transport Edge ont été modifiés afin de pointer vers les points de terminaison correspondants du deuxième centre de données. Le processus de commutation des autres rôles serveur implique la modification de ces enregistrements afin qu'ils pointent vers les points de terminaison de service restaurés du centre de données principal.

Comme pour les modifications du DNS qui ont été apportées durant la permutation vers le deuxième centre de données, les clients, les serveurs et les passerelles IP continueront à tenter de se connecter, et ils devront se connecter automatiquement une fois que la durée de vie a expiré pour l'entrée DNS d'origine, et une fois que l'entrée a expiré dans leur cache DNS.

Retour au début

## Rétablissement de la résilience de site

Une fois la commutation du centre de données principal réussie, vous pouvez rétablir sa résilience de site en vérifiant l'intégrité et l'état de chaque copie de base de données de boîtes aux lettres dans le deuxième centre de données. En outre, si des copies de base de données du deuxième centre de données ont été initialement bloquées pour activation, vous pouvez reconfigurer ces paramètres à ce stade.

Retour au début

