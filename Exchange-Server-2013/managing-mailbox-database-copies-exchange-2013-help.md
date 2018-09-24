---
title: 'Gérer les copies de base de données de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Gestion des copies de base de données de boîtes aux lettres
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 50477784
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des copies de base de données de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-08-26_

Après avoir créé un groupe de disponibilité de base de données, l’avoir configuré et renseigné avec des membres de serveur de boîtes aux lettres, vous pouvez utiliser le Centre d’administration Exchange (CAE) ou l’environnement de ligne de commande Exchange Management Shell pour ajouter des copies de base de données de boîtes aux lettres de manière flexible et granulaire.

## Gestion des copies de base de données

Après avoir créé plusieurs copies d’une base de données, vous pouvez utiliser le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell pour contrôler l’intégrité et l’état de chaque copie, et pour effectuer les autres tâches de gestion associées aux copies de base de données. Voici quelques tâches de gestion que vous devrez peut-être effectuer : interruption ou reprise de la copie d’une base de données, amorçage de la copie d’une base de données, contrôle des copies de base de données, configuration des paramètres de copie de base de données et suppression d’une copie de base de données.

## Interruption et reprise des copies de base de données

Vous pouvez être amené à interrompre et à reprendre la réplication continue de la copie d’une base de données pour plusieurs raisons, telles qu’une opération de maintenance prévue. En outre, certaines tâches administratives, telles que l’amorçage, nécessitent que vous suspendiez d’abord la copie d’une base de données. Il est recommandé de suspendre toute activité de réplication en cas de modification du chemin ou des fichiers journaux de la base de données. Vous pouvez suspendre et reprendre l’activité de copie de base de données à l’aide du CAE ou en exécutant les cmdlets **Suspend-MailboxDatabaseCopy** et **Resume-MailboxDatabaseCopy** dans l’environnement de ligne de commande Exchange Management Shell. Pour obtenir la procédure détaillée de suspension ou de reprise de l’activité de réplication continue d’une copie de base de données, consultez la rubrique [Interruption ou reprise d’une copie de base de données de boîtes aux lettres](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

## Amorçage d’une copie de base de données

L’*amorçage*, ou *mise à jour*, est le processus au cours duquel une base de données, qu’il s’agisse d’une base de données vierge ou de la copie d’une base de données de production, est ajoutée en tant que base de données de production à l’emplacement de copie cible sur un autre serveur de boîtes aux lettres dans le même groupe de disponibilité de base de données que la base de données active. Cela devient la base de données de base pour la copie gérée par ce serveur.

Selon la situation, l’amorçage peut être un processus automatique ou manuel que vous lancez. Quand une copie de base de données est ajoutée, la copie sera automatiquement amorcée si le serveur cible et son stockage sont configurés comme il faut. Si vous souhaitez amorcer manuellement une copie de base de données et que vous ne voulez pas qu’un amorçage automatique s’effectue lors de la création de la copie, vous pouvez utiliser le paramètre *SeedingPostponed* au moment de l’exécution de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)).

Les copies de base de données nécessitent rarement d’être amorcées à nouveau une fois que l’amorçage initial a eu lieu. Toutefois, si un réamorçage s’avère nécessaire ou si vous voulez amorcer manuellement une copie de base de données au lieu de laisser le système amorcer automatiquement la copie, vous pouvez le faire à l’aide de l’Assistant Mise à jour d’une copie de base de données de boîte aux lettres dans le CAE ou à l’aide de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Avant d’amorcer une copie de base de données, vous devez d’abord interrompre la copie de la base de données de boîtes aux lettres. Pour obtenir la procédure détaillée d'amorçage d'une copie de base de données, consultez la rubrique [Mise à jour d'une copie de base de données de boîtes aux lettres](update-a-mailbox-database-copy-exchange-2013-help.md).

Après une opération d’amorçage manuel, la réplication de la copie de base de données de boîtes aux lettres amorcée reprend automatiquement. Si vous ne souhaitez pas que la réplication reprenne automatiquement, utilisez le paramètre *ManualResume* lors de l’exécution de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

## Choix des éléments à amorcer

Lors d’un amorçage, vous pouvez choisir d’amorcer la copie de la base de données de boîtes aux lettres, son catalogue d’index de contenu ou les deux.

Par défaut, l’Assistant Mise à jour de la copie de base de données de boîtes aux lettres et la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) amorcent la copie de la base de données de boîtes aux lettres et la copie du catalogue d’index de contenu. Pour n’amorcer que la copie de base de données de boîtes aux lettres et pas le catalogue d’index de contenu, utilisez le paramètre *DatabaseOnly* lors de l’exécution de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)). Pour n’amorcer que le catalogue d’index de contenu, utilisez le paramètre *CatalogOnly* lors de l’exécution de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

## Sélection de la source d’amorçage

Toute copie de base de données en bon état peut être utilisée comme source d’amorçage pour une copie supplémentaire de cette base de données. Cela s’avère particulièrement utile quand un groupe de disponibilité de base de données a été étendu sur plusieurs emplacements physiques. Par exemple, imaginez le déploiement d’un groupe de disponibilité de base de données de quatre membres, dont deux membres (MBX1 et MBX2) sont situés à Portland dans l’Oregon et deux membres (MBX3 et MBX4) sont situés à New York. Une base de données de boîtes aux lettres appelée DB1 est active sur MBX1 et des copies passives de DB1 se trouvent sur MBX2 et MBX3. Lorsque vous ajoutez une copie de DB1 à MBX4, vous avez la possibilité d’utiliser la copie sur MBX3 comme source pour l’amorçage. Ce faisant, vous évitez l’amorçage sur le réseau étendu (WAN) qui relie Portland à New York.

Pour utiliser une copie spécifique comme source d’amorçage lors de l’ajout d’une nouvelle copie de base de données, il faudrait procéder comme suit :

  - Utilisez le paramètre *SeedingPostponed* lors de l’exécution de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)) pour ajouter la copie de base de données. Si le paramètre *SeedingPostponed* n’est pas utilisé, la copie de base de données sera explicitement amorcée avec la copie active de la base de données comme source.

  - Vous pouvez spécifier le serveur source à utiliser dans le cadre de l’Assistant Mise à jour de la copie de la base de données de boîtes aux lettres dans le CAE, ou vous pouvez utiliser le paramètre *SourceServer* lorsque vous exécutez la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) pour spécifier le serveur source désiré pour l’amorçage. Dans l’exemple précédent, vous indiqueriez MBX3 comme serveur source. Si le paramètre *SourceServer* n’est pas utilisé, la copie de base de données sera explicitement amorcée à partir de la copie active de la base de données.

## Amorçage et réseaux

En plus de choisir un serveur source spécifique pour l’amorçage d’une copie de base de données de boîtes aux lettres, vous pouvez aussi utiliser l’environnement de ligne de commande Exchange Management Shell pour indiquer quels réseaux DAG vous souhaitez utiliser et éventuellement remplacer les paramètres de compression et de chiffrement du réseau DAG pendant l’opération d’amorçage.

> [!NOTE]
> L’amorçage d’un catalogue d’index de contenu n’est possible que par le biais d’un réseau MAPI. Cela est avéré même si vous utilisez le paramètre <code>-Network</code> dans la cmdlet Update-MailboxDatabaseCopy.


Pour indiquer les réseaux que vous souhaitez utiliser pour l’amorçage, utilisez le paramètre *Network* lors de l’exécution de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)) et indiquez les réseaux DAG que vous voulez utiliser. Si vous n’utilisez pas le paramètre *Network*, le système utilise la procédure par défaut pour le choix du réseau à utiliser pour l’amorçage :

  - Si le serveur source et le serveur cible sont sur le même sous-réseau et qu’un réseau de réplication a été configuré incluant le sous-réseau, le réseau de réplication sera utilisé.

  - Si le serveur source et le serveur cible sont sur différents sous-réseaux, même si un réseau de réplication contenant ces sous-réseaux a été configuré, le réseau client (MAPI) sera utilisé pour l’amorçage.

  - Si le serveur source et le serveur cible se trouvent dans des centres de données différents, le réseau client (MAPI) sera utilisé pour l’amorçage.

Au niveau du groupe de disponibilité de base de données (DAG), les réseaux DAG sont configurés pour le chiffrement et la compression. Les paramètres par défaut n’utilisent le chiffrement et la compression que pour les communications sur des sous-réseaux différents. Si la source et la cible sont sur différents sous-réseaux et que le groupe de disponibilité de base de données (DAG) est configuré avec les valeurs par défaut pour *NetworkCompression* et *NetworkEncryption*, vous pouvez remplacer ces valeurs à l’aide des paramètres *NetworkCompressionOverride* et *NetworkEncryptionOverride*, respectivement, lors de l’exécution de la cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)).

## Processus d’amorçage

Lorsque vous lancez le processus d’amorçage à l’aide de la cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298105\(v=exchg.150\)) ou [Update-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd335201\(v=exchg.150\)), les tâches suivantes sont effectuées :

1.  Les propriétés de base de données d’Active Directory sont lues pour valider la base de données et les serveurs indiqués et pour vérifier que les serveurs sources et cibles exécutent Exchange 2013, qu’ils sont tous les deux des membres du même groupe de disponibilité de base de données et que la base de données indiquée n’est pas une base de données de récupération. Les chemins d’accès aux fichiers de base de données sont également lus.

2.  Il y a une préparation aux contrôles de réamorçage à partir du service de réplication Microsoft Exchange sur le serveur cible.

3.  Le service de réplication Microsoft Exchange du serveur cible contrôle la présence de fichiers journaux des bases de données et des transactions dans le répertoire de fichiers lu lors des contrôles Active Directory à l’étape 1.

4.  Le service de réplication Microsoft Exchange renvoie les informations sur l’état du serveur cible à l’interface d’administration à partir de l’emplacement d’exécution de la cmdlet.

5.  Si tous les contrôles préliminaires ont été effectués avec succès, vous serez invité à confirmer l’opération avant de continuer. Si vous confirmez l’opération, le processus se poursuit. Si une erreur se produit lors des contrôles préliminaires, elle est signalée et l’opération échoue.

6.  L’opération d’amorçage est lancée à partir du service de réplication Microsoft Exchange sur le serveur cible.

7.  Le service de réplication Microsoft Exchange suspend la réplication de base de données de la copie de base de données active.

8.  Les informations sur l’état de la base de données sont mises à jour par le service de réplication Microsoft Exchange pour rendre compte de l’état de l’amorçage.

9.  Si le serveur cible ne contient pas déjà les répertoires pour les fichiers journaux et de base de données cibles, ils sont alors créés.

10. Une demande d’amorçage de la base de données est transmise du service de réplication Microsoft Exchange du serveur cible au service de réplication Microsoft Exchange du serveur source à l’aide du protocole TCP. Cette demande et les communications qui suivent pour l’amorçage de la base de données ont lieu sur un réseau DAG qui a été configuré comme réseau de réplication.

11. Le service de réplication Microsoft Exchange du serveur source lance une sauvegarde en continu ESE (Extensible Storage Engine) via l’interface du service de banque d’informations Microsoft Exchange.

12. Le service de banque d’informations Microsoft Exchange transmet les données de la base de données au service de réplication Microsoft Exchange.

13. Les données de la base sont transférées du service de réplication Microsoft Exchange du serveur source au service de réplication Microsoft Exchange du serveur cible.

14. Le service de réplication Microsoft Exchange du serveur cible écrit la copie de la base de données dans un répertoire temporaire situé dans le répertoire principal de la base de données appelé *temp-seeding*.

15. L’opération de sauvegarde en continu sur le serveur source se termine à la fin de la base de données.

16. L’écriture sur le serveur cible se termine et la base de données est déplacée du répertoire temp-seeding à l’emplacement final. Le répertoire temp-seeding est supprimé.

17. Sur le serveur cible, le service de réplication Microsoft Exchange traite la demande et la communique au service de recherche Microsoft Exchange pour monter le catalogue d’index de contenu de la copie de base de données, s’il existe. S’il y a des fichiers du catalogue qui n’ont pas été mis à jour depuis la fois précédente sur la copie de base de données, l’opération de montage échoue, ce qui entraîne la nécessité de répliquer le catalogue du serveur source. De la même manière, si le catalogue n’existe pas et qu’il n’existe pas sur un nouvel exemplaire de la copie de base de données du serveur cible, il faut une copie du catalogue. Le service de réplication Microsoft Exchange dirige le service de recherche Microsoft Exchange pour qu’il interrompe l’indexation de la copie de base de données pendant qu’un nouveau catalogue est copié à partir de la source.

18. Le service de réplication Microsoft Exchange du serveur cible envoie alors une demande d’amorçage du catalogue au service de réplication Microsoft Exchange du serveur source.

19. Sur le serveur source, le service de réplication Microsoft Exchange demande les informations de répertoire du service de recherche Microsoft Exchange et demande la suspension de l’indexation.

20. Le service de recherche Microsoft Exchange du serveur source renvoie les informations du répertoire du catalogue de recherche au service de réplication Microsoft Exchange.

21. Le service de réplication Microsoft Exchange du serveur source lit les fichiers de catalogue du répertoire.

22. Le service de réplication Microsoft Exchange du serveur source déplace les données de catalogue vers le service de réplication Microsoft Exchange du serveur cible à l’aide d’une connexion sur le réseau de réplication. Une fois la lecture finie, le service de réplication Microsoft Exchange envoie une demande au service de recherche Microsoft Exchange pour qu’il reprenne l’indexation de la base de données source.

23. Si des fichiers de catalogue existent déjà sur le serveur cible du répertoire, le service de réplication Microsoft Exchange sur le serveur cible les supprime.

24. Le service de réplication Microsoft Exchange du serveur cible écrit les données de catalogue dans un répertoire temporaire appelé *CiSeed.Temp* jusqu’à ce que les données soient complètement transférées.

25. Le service de réplication Microsoft Exchange déplace les données de catalogue complètes vers l’emplacement final.

26. Le service de réplication Microsoft Exchange du serveur cible reprend l’indexation de recherche sur la base de données cible.

27. Le service de réplication Microsoft Exchange du serveur cible renvoie un état d’exécution.

28. Le résultat final de l’opération est transmis à l’interface d’administration à partir de laquelle la cmdlet a été exécutée.

## Configuration de copies de base de données

Après la création d’une copie de base de données, vous pouvez afficher et modifier ses paramètres de configuration, si nécessaire. Vous pouvez afficher certaines informations de configuration sur la page **Propriétés** d’une copie de base de données dans le CAE. Vous pouvez aussi utiliser les cmdlets [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\)) et [Set-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298104\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell pour afficher et configurer les paramètres de copie de base de données, tels que le délai d’attente de relecture, le délai d’attente de troncation et l’ordre de préférence pour l’activation. Pour obtenir la procédure détaillée d’affichage et de configuration des paramètres de copie de base de données, consultez la rubrique [Configurer les propriétés des copies de la base de données de boîtes aux lettres](configure-mailbox-database-copy-properties-exchange-2013-help.md).

## Utilisation des options de délai d’attente de relecture et de troncation

Les copies de base de données de boîtes aux lettres prennent en charge l’utilisation d’un *délai d’attente de relecture* et d’un *délai d’attente de troncation* ; les deux sont définis en minutes. Le paramétrage d’un délai d’attente de relecture vous permet de renvoyer la copie de base de données à un certain moment dans le temps. Le paramétrage d’un délai d’attente de troncation vous permet d’utiliser les fichiers journaux sur une copie passive de base de données à récupérer après la perte de fichiers journaux sur la copie active de base de données. Parce que ces deux fonctionnalités entraînent l’accumulation temporaire des fichiers journaux, leur utilisation aura des répercussions sur votre conception de stockage.

## Délai d’attente de relecture

Le délai d’attente de relecture est une propriété de la copie de base de données de boîtes aux lettres qui indique la durée, en minutes, du retard de relecture du journal de la copie de base de données. Le minuteur de retard de relecture se déclenche quand un fichier journal est répliqué dans la copie passive et passe l’inspection avec succès. En retardant la relecture des journaux de la copie de base de données, vous avez la possibilité de récupérer la base de données à un certain moment dans le temps passé. Une copie de base de données de boîtes aux lettres configurée avec un délai d’attente de relecture supérieur à 0 s’appelle une *copie retardée de base de données de boîtes aux lettres* ou simplement une *copie retardée*.

Une stratégie qui utilise des copies de bases de données et des fonctionnalités de mise en attente pour litige dans Exchange 2013 peut offrir une protection contre un large éventail de défaillances habituellement responsables d’une perte de données. Toutefois, ces fonctionnalités ne peuvent pas fournir de protection contre la perte de données en cas d’altération logique qui, bien que rare, peut entraîner une perte de données. Les copies retardées sont faites pour éviter la perte de données en cas d’altération logique. En règle générale, il existe deux types d’altération logique :

  - **Corruption logique de la base de données**   Le total de contrôle des pages de la base de données correspond, mais les données sur les pages sont erronées au niveau logique. Cela peut arriver quand l’ESE tente d’écrire sur une page de base de données et, même si le système d’exploitation envoie un message de succès, soit les données ne sont pas écrites sur le disque soit elles sont écrites à la mauvaise place. Il s’agit d’un *vidage perdu*. Afin d’éviter la perte de données par les vidages perdus, l’ESE comporte un mécanisme de détection des vidages perdus dans la base de données ainsi qu’une fonctionnalité de mise à jour corrective (restauration d’une seule page).

  - **Corruption logique de banque d’informations**   Les données sont ajoutées, supprimées ou manipulées d’une manière à laquelle l’utilisateur ne s’attend pas. Ces cas sont généralement provoqués par des applications tierces. Ce n’est généralement de la corruption que dans le sens où l’utilisateur voit cela comme une altération. La banque d’informations Exchange considère la transaction qui est à l’origine de l’altération logique comme une série d’opérations MAPI valides. La fonction de suspension pour litige d’Exchange 2013 assure une protection contre l’altération logique de la banque d’informations (car elle évite que le contenu soit supprimé définitivement par un utilisateur ou une application). Toutefois, dans certains cas, une boîte aux lettres d’utilisateur est si endommagée qu’il serait plus facile de la restaurer à un point antérieur à l’altération, et d’exporter ensuite la boîte aux lettres de l’utilisateur pour récupérer les données intactes.

La combinaison des copies de base de données, de la stratégie de rétention et de la restauration ESE des pages uniques ne laisse que les cas rares mais catastrophiques d’altération logique de banque d’informations. Votre choix d’utiliser une copie de base de données avec retard de relecture (une copie retardée) dépendra des applications tierces que vous utilisez et de l’historique de votre organisation quant à l’altération logique de banque d’informations.

Les copies retardées peuvent se gérer elles-mêmes dans Exchange 2013 lorsque vous appelez la relecture automatique des journaux pour lire les fichiers journaux dans certains scénarios :

  - Lorsque le seuil d’espace disque faible est atteint

  - Lorsque la copie retardée est physiquement endommagée et doit faire l’objet d’une mise à jour corrective de pages

  - Quand il y a moins de trois copies intègres disponibles (actives ou passives uniquement, les copies de base de données retardées ne sont pas comptées) pendant plus de 24 heures

La mise à jour corrective de pages est disponible pour les copies retardées via cette fonction de lecture automatique. Si le système détecte qu’une mise à jour corrective de page est nécessaire pour une copie retardée, les journaux sont automatiquement relus dans la copie retardée pour exécuter la mise à jour corrective de page. Les copies retardées appellent également cette fonction de relecture automatique lorsque le seuil d’espace disque faible est atteint et lorsque la copie retardée a été détectée comme étant la seule copie disponible pendant une période spécifique.

Le comportement de lecture de copie retardée est désactivé par défaut, mais peut être activé en exécutant la commande suivante :

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true
```

Une fois activée, la lecture a lieu lorsque le nombre de copies est inférieur à trois. Vous pouvez modifier la valeur 3 par défaut en changeant la valeur de registre DWORD suivante :

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Pour activer la lecture pour les seuils d’espace disque faible, vous devez configurer l’entrée de registre suivante :

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Après avoir configuré un de ces paramètres de registre, redémarrez le service de gestion des groupes de disponibilité de base de données (DAG) Microsoft Exchange pour que les modifications prennent effet.

À titre d’exemple, prenons un environnement où une base de données dispose de 4 copies (3 copies hautement disponibles et une copie retardée), et où le paramètre par défaut est utilisé pour ReplayLagManagerNumAvailableCopies. Si une copie non retardée est hors de service pour une raison quelconque (elle est par exemple suspendue, etc.), la copie retardée lira automatiquement ses fichiers journaux dans les 24 heures.

Si vous choisissez d’utiliser des copies retardées sans activer le paramètre `ReplayLagManagerEnabled`, prenez en compte les conséquences suivantes :

  - Le délai d’attente de relecture est une valeur configurée par l’administrateur qui est désactivée par défaut.

  - Par défaut, le paramètre de délai d’attente de relecture est défini sur 0 jour et le paramètre maximal sur 14 jours.

  - Les copies retardées ne sont pas considérées comme des copies hautement disponibles. Elles sont plutôt prévues à des fins de récupération d’urgence pour éviter l’altération logique de la banque d’informations.

  - Plus le délai d’attente de relecture est important, plus le processus de récupération de base de données est long. Selon le nombre de fichiers journaux qui doivent être relus pendant la récupération, et selon la vitesse à laquelle votre matériel peut les relire, le processus peut mettre plusieurs heures à récupérer une base de données.

  - Nous vous recommandons de déterminer si les copies retardées sont essentielles à votre stratégie générale de récupération d’urgence. Si elles sont essentielles à votre stratégie, nous vous recommandons d’utiliser plusieurs copies retardées ou un RAID (Redundant array of independant disks) pour protéger une seule copie retardée, si vous n’avez pas plusieurs copies retardées. Si vous perdez un disque ou si une altération se produit, vous ne perdez pas votre moment retardé dans le temps.

  - Les copies retardées ne peuvent pas être corrigées avec la fonctionnalité de restauration de page unique ESE. Si une copie retardée rencontre une altération de page de base de données (par exemple, une erreur -1018), elle devra être réamorcée (ce qui entraînera la perte de l’aspect retardé de la copie).

L’activation et la récupération d’une copie retardée de base de données de boîtes aux lettres est un processus simple si vous voulez que la base de données relise tous les fichiers journaux et actualise la copie de la base de données. Si vous souhaitez relire les fichiers journaux jusqu’à un moment spécifique dans le temps, l’opération se complique car il vous faut manipuler manuellement les fichiers journaux et exécuter les utilitaires de base de données d’Exchange Server (Eseutil.exe).

Pour obtenir la procédure détaillée d’activation d’une copie retardée de base de données de boîtes aux lettres, consultez la rubrique [Activation d’une copie de la base de données de boîtes aux lettres retardée](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md).

## Délai d’attente de troncation

Le délai d’attente de troncation est une propriété de la copie de base de données de boîtes aux lettres qui indique le temps, en minutes, du retard de suppression de la copie de base de données après relecture du fichier journal dans la copie de base de données. Le minuteur de délai d’attente de troncature se déclenche quand un fichier journal est répliqué dans la copie passive, a passé l’inspection avec succès et a été relu avec succès dans la copie de la base de données. En retardant la troncation des fichiers journaux de la copie de base de données, vous avez la possibilité de récupérer des échecs concernant les fichiers journaux de la copie active de la base de données.

## Copies de la base de données et troncation de journaux

La troncation de journaux fonctionne de la même manière dans Exchange 2013 que dans Exchange 2010. Le comportement de troncation est déterminé par les paramètres de délai d’attente de relecture et de délai d’attente de troncation de la copie.

Les critères suivants doivent être remplis pour que le fichier journal d’une copie de base de données soit tronqué lorsque les paramètres sont laissés par défaut sur 0 (désactivé) :

  - Le fichier journal doit avoir été sauvegardé ou la journalisation circulaire doit être activée.

  - Le fichier journal doit être en-dessous du point de contrôle (fichier journal minimum nécessaire pour la récupération) de la base de données.

  - Toutes les autres copies retardées doivent avoir inspecté le fichier journal.

  - Toutes les autres copies (copies non retardées) doivent avoir relu le fichier journal.

Pour la troncation d’une copie retardée de base de données, les critères suivants doivent être remplis :

  - Le fichier journal doit être inférieur au point de contrôle de la base de données.

  - Le fichier journal doit être plus ancien que ReplayLagTime + TruncationLagTime.

  - Le fichier journal doit avoir été tronqué sur la copie active.

La troncation de journal Exchange 2013 ne s’effectue pas sur la copie de base de données de boîtes aux lettres active si au moins une copie passive est interrompue. Si des activités de maintenance planifiées doivent s’effectuer sur une période prolongée (par exemple, plusieurs jours), la création de fichiers journaux risque d’être considérable. Afin d’éviter le remplissage du lecteur de journaux de transactions, vous pouvez supprimer la copie de base de données passive concernée au lieu de l’interrompre. Lorsque la maintenance planifiée est terminée, vous pouvez rajouter la copie de base de données passive.

Exchange 2013 Service Pack 1 (SP1) contient une nouvelle fonctionnalité appelée *troncation souple*, qui est désactivée par défaut. En temps normal, chaque copie de base de données conserve les journaux devant être envoyés vers d’autres copies de base de données jusqu’à ce que toutes les copies d’une base de données confirment qu’elles ont relu (copies passives) et reçu (copies retardées) les fichiers journaux. Il s’agit du comportement de troncation de journal par défaut. Si une copie de base de données est hors ligne pour une raison quelconque, les fichiers journaux s’accumulent sur les disques utilisés par les autres copies de la base de données. Si la copie de base de données concernée reste déconnectée pendant une période prolongée, les autres copies de base de données risquent d’arriver à court d’espace disque.

Lorsque la troncation souple est activée, le comportement de troncation est différent. Chaque copie de base de données suit la disponibilité de son propre espace disque et applique le comportement de troncation souple si l’espace disponible devient faible. Pour la copie active, la copie de base de données passive la plus en retard dans la relecture du journal est ignorée et la troncation respecte les copies passives restantes les plus anciennes. La troncation globale est calculée dans la copie de base de données active. Les copies passives tenteront de respecter la décision relative à la troncation prise sur la copie active. Malgré l’implication du nom MinCopiesToProtect, Exchange ignorera uniquement la copie de base de données passive la plus ancienne connue au moment de l’exécution de la troncation. Si l’espace est faible, une copie passive tronquera indépendamment ses fichiers journaux à l’aide des paramètres configurés décrits ci-dessous.

Les fichiers journaux ayant été supprimés des autres copies saines seront manquants sur la base de données déconnectée lorsque celle-ci sera remise en ligne, et son statut sera FailedAndSuspended. Dans ce cas, si Autoreseed est configuré, la copie concernée sera réamorcée automatiquement. Si Autoreseed n’est pas activé, la copie de base de données devra être amorcée manuellement par un administrateur.

Le nombre requis de copies saines, le seuil d’espace disque libre et le nombre de journaux à conserver sont tous des paramètres configurables. Par défaut, le seuil d’espace disque disponible est de 204 800 Mo (200 Go) et le nombre de journaux à conserver est de 100 000 (100 Go) pour les copies passives et de 10 000 (10 Go) pour les copies actives.

Pour activer la troncation souple et en configurer les paramètres, vous devez modifier le Registre Windows sur chaque membre du DAG. Trois valeurs de Registre peuvent être configurées ; elles sont toutes stockées sous HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation. La clé BackupInformation et les valeurs DWORD suivantes n’existent pas par défaut et doivent être créées manuellement. Les valeurs du Registre DWORD sous BackupInformation sont décrites dans le tableau suivant :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valeur de Registre</th>
<th>Description</th>
<th>Valeur par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>Cette clé permet d’activer la troncation souple. Elle représente le nombre de copies passives à protéger de la troncation souple sur la copie active d’une base de données. Si la valeur de cette clé est définie sur 0, la troncation souple est désactivée.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>Seuil d’espace disque disponible (en Mo) pour le déclenchement de la troncation souple. Si l’espace disque disponible descend en dessous de cette valeur, la troncation souple est déclenchée.</p></td>
<td><p>Si cette valeur de registre n’est pas configurée, la valeur par défaut utilisée par la troncation souple est 200 Go.</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>Nombre minimal de fichiers journaux à conserver sur les copies saines dont les journaux sont tronqués. Si cette valeur de registre est configurée, la valeur configurée s’applique alors aux copies actives et passives.</p></td>
<td><p>Si cette valeur de registre n’est pas configurée, les valeurs par défaut 100 000 pour les copies de base de données passives et 10 000 pour les copies de base de données actives sont utilisées.</p></td>
</tr>
</tbody>
</table>


Lors de l’utilisation de la valeur de registre LooseTruncation\_MinLogsToProtect, vous remarquerez que le comportement est différent pour les copies de base de données actives et passives. Sur la copie de base de données active, il s’agit du nombre de journaux supplémentaires conservés avant ceux requis par les copies passives protégées et la plage requise de la copie active. Sur une copie de base de données passive, il s’agit du nombre de journaux conservés depuis le dernier journal disponible. Un dixième de ce nombre est également utilisé pour conserver des journaux avant la plage requise de cette copie passive. Les deux limites permettent de veiller à ce que les copies retardées de base de données n’utilisent pas trop d’espace, car leur plage requise est généralement très étendue.

## Stratégie d’activation de la base de données

Les stratégies d’activation de la base de données sont des scénarios dans lesquels vous voulez créer une copie de base de données de boîtes aux lettres et éviter que le système active automatiquement cette copie en cas de panne, par exemple :

  - Si vous déployez une ou plusieurs copies de base de données de boîtes aux lettres dans un centre de données de remplacement ou de veille.

  - Si vous configurez une copie retardée de base de données à des fins de récupération.

  - Si vous effectuez la maintenance ou la mise à niveau d’un serveur.

Dans chacun des scénarios évoqués ci-dessus, vous avez des copies de base de données que vous ne voulez pas voir activées automatiquement par le système. Si vous voulez éviter que le système active automatiquement une copie de base de données de boîtes aux lettres, vous pouvez configurer la copie pour qu’elle soit bloquée (suspendue) à l’activation. Cela permet au système de maintenir l’actualité de la base de données par l’envoi de fichiers journaux et la relecture, mais l’empêche d’activer et d’utiliser automatiquement la copie. Les copies bloquées pour l’activation doivent être activées manuellement par un administrateur. Vous pouvez configurer la stratégie d’activation de base de données pour l’ensemble d’un serveur à l’aide de la cmdlet [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\)) ou pour une copie de base de données individuelle à l’aide de la cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/fr-fr/library/dd298104\(v=exchg.150\)) pour définir le paramètre *DatabaseCopyAutoActivationPolicy* sur Blocked.

Pour plus d’informations sur la configuration des stratégies d’activation de la base de données, consultez la rubrique [Configurer la stratégie d’activation pour une copie de base de données de boîte aux lettres](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md).

## Impact des déplacements de boîtes aux lettres sur la réplication continue

Sur une base de données de boîtes aux lettres très occupée avec une fréquence élevée de génération des journaux, il y a plus de risques de perdre des données si la réplication sur les copies passives de base de données ne parvient pas à suivre la génération des journaux. Un déplacement de boîtes aux lettres peut provoquer une fréquence élevée de génération de journaux. Exchange 2013 inclut une API de garantie des données qui est utilisée par des services tels que le service de réplication de boîte aux lettres Microsoft Exchange (MRS) pour vérifier l’intégrité de l’architecture de copie de base de données en fonction de la valeur du paramètre *DataMoveReplicationConstraint* qui a été définie par le système ou un administrateur. Plus précisément, l’API de garantie des données peut servir à :

  - **Vérifier l’intégrité de la réplication**   Elle confirme que le nombre requis de copies de base de données est disponible.

  - **Vérifier le vidage de réplication**   Elle confirme que les fichiers journaux requis ont été relus selon le nombre requis de copies de base de données.

Lorsqu’elle est exécutée, l’API retourne les informations d’état suivantes à l’application appelante :

  - **Retry** (Nouvelle tentative)   Signifie qu’il y a des erreurs temporaires qui empêchent une condition d’être vérifiée par rapport à la base de données.

  - **Satisfied** (Satisfait)   Signifie que la base de données remplit les conditions requises ou que la base de données n’est pas répliquée.

  - **NotSatisfied** (Non satisfait)   Signifie que la base de données ne respecte pas les conditions requises. De plus, des informations sont fournies à l’application appelante sur le motif du retour de la réponse **NotSatisfied**.

La valeur du paramètre *DataMoveReplicationConstraint* pour la base de données de boîtes aux lettres détermine combien de copies de base de données doivent être évaluées dans le cadre de la requête. Le paramètre *DataMoveReplicationConstraint* accepte les valeurs suivantes :

  - `None`   Lorsque vous créez une base de données de boîtes aux lettres, cette valeur est définie par défaut. Lorsque cette valeur est définie, les conditions de l’API de garantie des données sont ignorées. Ce paramètre doit être utilisé uniquement pour les bases de données de boîtes aux lettres qui ne sont pas répliquées.

  - `SecondCopy`   C’est la valeur par défaut lorsque vous ajoutez la deuxième copie d’une base de données de boîtes aux lettres. Lorsque cette valeur est définie, au moins une copie passive de base de données doit respecter les conditions de l’API de garantie des données.

  - `SecondDatacenter`   Lorsque cette valeur est définie, au moins une copie passive de base de données dans un autre site Active Directory doit respecter les conditions de l’API de garantie des données.

  - `AllDatacenters`   Lorsque cette valeur est définie, au moins une copie passive de base de données dans un chaque site Active Directory doit respecter les conditions de l’API de garantie des données.

  - `AllCopies`   Lorsque cette valeur est définie, toutes les copies de base de données de boîtes aux lettres doivent respecter les conditions de l’API de garantie des données.

**Vérifier l’intégrité de la réplication**

Lorsque l’API de garantie des données est exécutée pour évaluer l’intégrité de l’infrastructure de la copie de base de données, plusieurs éléments sont évalués.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si le paramètre <em>DataMoveReplicationConstraint</em> est défini sur…</th>
<th>Alors, pour une certaine base de données...</th>
<th>Conditions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>Au moins une copie passive de base de données pour une base de données répliquée doit respecter les conditions dans la colonne suivante.</p></td>
<td><p>La copie passive de base de données doit :</p>
<ul>
<li><p>Être intègre.</p></li>
<li><p>Avoir une file d’attente de relecture comprise dans les 10 minutes du délai d’attente de relecture.</p></li>
<li><p>Avoir une longueur de file d’attente de copie inférieure à 10 journaux.</p></li>
<li><p>Avoir une longueur moyenne de file d’attente de copie inférieure à 10 journaux. La longueur moyenne de file d’attente de copie est calculée en fonction du nombre de fois où l’application a demandé l’état de la base de données.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>Au moins une copie passive de base de données dans un autre site Active Directory doit respecter les conditions dans la colonne suivante.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>La copie active doit être montée, et une copie passive dans chaque site Active Directory doit respecter les conditions dans la colonne suivante.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>La copie active doit être montée, et toutes les copies passives de base de données doivent respecter les conditions dans la colonne suivante.</p></td>
<td></td>
</tr>
</tbody>
</table>


**Vérifier le vidage de réplication**

L’API de garantie des données permet également de valider qu’un nombre préalablement requis de copies de base de données ont relu les journaux des transactions requis. Ceci est vérifié en comparant l’horodatage du dernier journal relu à celui de validation du service d’appel (dans la plupart des cas, c’est l’horodatage du dernier fichier journal qui contient les données requises) plus cinq secondes supplémentaires (pour tenir compte des variations ou des décalages de l’horloge système). Si l’horodatage de relecture est supérieur à celui de validation, le paramètre *DataMoveReplicationConstraint* est respecté. Si l’horodatage de relecture est inférieur à celui de validation, le paramètre *DataMoveReplicationConstraint* n’est pas respecté.

Avant de déplacer de grands nombres de boîtes aux lettres vers ou à partir de bases de données de réplication au sein d’un DAG, nous vous recommandons de configurer le paramètre *DataMoveReplicationConstraint* sur chaque base de données de boîtes aux lettres selon ce qui suit :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si vous déployez...</th>
<th>Définissez la valeur DataMoveReplicationConstraint sur...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Des bases de données de boîtes aux lettres qui ne possèdent aucune copie de base de données</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>Un DAG dans un site Active Directory unique</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>Un DAG dans plusieurs centres de données à l’aide d’un site Active Directory étiré</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>Un DAG qui s’étend sur deux sites Active Directory et vous aurez des copies de base de données à haute disponibilité dans chaque site</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>Un DAG qui s’étend sur deux sites Active Directory et vous aurez seulement des copies de base de données retardées dans le second site</p></td>
<td><p><code>SecondCopy</code></p>
<p>En effet, l’API de garantie des données ne garantira pas des données en cours de validation avant la relecture du fichier journal dans la copie de base de données et, en raison de la nature de la copie de base de données étant retardée, cette contrainte va faire échouer la demande de déplacement, à moins que la valeur de ReplayLagTime de la copie de base de données retardée soit inférieure à 30 minutes.</p></td>
</tr>
<tr class="even">
<td><p>Un DAG qui s’étend sur trois sites Active Directory ou plus, et chaque site contiendra des copies de base de données à haute disponibilité</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## Équilibrage des copies de base de données

De par la nature inhérente des groupes de disponibilité de base de données, lorsqu’un basculement ou une permutation de base de données se produit, les copies de base de données de boîtes aux lettres actives changent d’hôte plusieurs fois tout au long du cycle de vie d’un groupe de disponibilité de base de données. Par conséquent, les groupes de disponibilité de base de données se trouvent en déséquilibre au niveau de la distribution des copies de base de données de boîtes aux lettres actives. Le tableau suivant illustre un exemple de groupe de disponibilité de base de données comportant quatre bases de données et quatre copies de chacune (pour un total de 16 bases de données sur chaque serveur) avec une distribution inéquitable des copies de base de données actives.

### Groupe de disponibilité de base de données avec une distribution inéquitable des copies actives

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveur</th>
<th>Nombre de bases de données actives</th>
<th>Nombre de bases de données passives</th>
<th>Nombre de bases de données montées</th>
<th>Nombre de bases de données démontées</th>
<th>Liste de décompte des préférences</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


Dans l’exemple précédent, on dénombre quatre copies de chaque base de données et donc, seulement quatre valeurs possibles pour la préférence d’activation (1, 2, 3 ou 4). La colonne **Liste de décompte des préférences** indique le nombre de bases de données avec chacune de ces valeurs. Par exemple, sur EX3, il existe 13 copies de base de données avec la préférence d’activation 1, deux copies avec la préférence d’activation 2, une copie avec la préférence d’activation 3 et aucune copie avec la préférence d’activation 4.

Comme vous pouvez le voir, ce groupe de disponibilité de base de données n’est pas équilibré en termes de nombre de bases de données actives hébergées par chaque membre du groupe, de nombre de bases de données passives hébergées par chaque membre du groupe ou de décompte de préférences d’activation des bases de données hébergées.

Vous pouvez utiliser le script RedistributeActiveDatabases.ps1 pour équilibrer les copies de base de données de boîtes aux lettres actives sur un DAG. Ce script déplace les bases de données d’une copie vers une autre afin d’essayer d’obtenir un nombre équitable de bases de données montées sur chaque serveur dans le groupe de disponibilité de base de données. Si nécessaire, le script essaie également d’équilibrer les bases de données actives dans les sites.

Le script inclut deux options permettant d’équilibrer les copies de base de données actives dans un groupe de disponibilité de base de données :

  - **BalanceDbsByActivationPreference**   Lorsque cette option est spécifiée, le script tente de déplacer les bases de données vers leur copie préférée (en fonction de la préférence d’activation), indépendamment du site Active Directory.

  - **BalanceDbsBySiteAndActivationPreference**   Lorsque cette option est spécifiée, le script tente de déplacer les bases de données actives vers leur copie préférée, tout en essayant d’équilibrer les bases de données actives dans chaque site Active Directory.

Après avoir exécuté le script avec la première option, le groupe de disponibilité déséquilibré précédent est rééquilibré, comme l’illustre le tableau suivant.

### Groupe de disponibilité de base de données avec une distribution équitable des copies actives

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveur</th>
<th>Nombre de bases de données actives</th>
<th>Nombre de bases de données passives</th>
<th>Nombre de bases de données montées</th>
<th>Nombre de bases de données démontées</th>
<th>Liste de décompte des préférences</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


Comme indiqué dans le tableau précédent, ce groupe de disponibilité de base de données est à présent équilibré en termes de nombre de bases de données actives et passives sur chaque serveur et de préférence d’activation sur les serveurs.

Le tableau suivant répertorie les paramètres disponibles pour le script RedistributeActiveDatabases.ps1.

### Paramètres du script RedistributeActiveDatabases.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Indique le nom du groupe de disponibilité de base de données que vous souhaitez rééquilibrer. Si ce paramètre est omis, le groupe de disponibilité de base de données dont fait partie le serveur local est utilisé.</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>Indique que le script doit déplacer les bases de données vers leur copie préférée, indépendamment du site Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>Indique que le script doit essayer de déplacer les bases de données actives vers leur copie préférée, tout en essayant d’équilibrer les bases de données actives dans chaque site Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>Indique qu’un rapport de distribution des bases de données actuelles doit s’afficher une fois la redistribution terminée.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>Spécifie l’écart autorisé des bases de données actives dans les sites, exprimé en pourcentage. La valeur par défaut est de 20 %. Par exemple, si 99 bases de données ont été distribuées entre trois sites, la distribution idéale serait de 33 bases de données dans chaque site. Si l’écart autorisé est de 20 %, le script tente d’équilibrer les bases de données afin que chaque site ne contienne pas plus de 10 % par rapport à ce nombre. 10 % de 33 équivaut à 3,3, chiffre arrondi à 4. Par conséquent, le script essaie d’avoir entre 29 et 37 bases de données dans chaque site.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>Indique que le script doit créer, pour chaque base de données, un rapport indiquant la manière dont celle-ci a été déplacée et si elle est maintenant active sur sa copie préférée.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>Indique que le script doit générer un rapport décrivant la distribution des bases de données pour chaque serveur.</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>Indique que le script s’exécute uniquement sur le membre du groupe de disponibilité de base de données exerçant actuellement le rôle de gestionnaire Active Manager principal (PAM). Le script vérifie qu’il est exécuté à partir du gestionnaire Active Manager principal. Si tel n’est pas le cas, le script prend fin.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>Indique que le script consigne un événement (événement 4115 MsExchangeRepl) contenant un résumé des actions.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>Indique que le script doit inclure les bases de données non répliquées (bases de données sans copies) lors de la détermination du mode de redistribution des bases de données actives. Même si les bases de données non répliquées ne peuvent pas être déplacées, elles peuvent influencer la distribution des bases de données répliquées.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Le commutateur Confirm peut être utilisé pour supprimer la boîte de dialogue de confirmation qui s’affiche par défaut lorsque ce script est exécuté. Pour supprimer la boîte de dialogue de confirmation, utilisez la syntaxe de -Confirm:$False. Vous devez inclure un signe deux-points ( : ) dans la syntaxe.</p></td>
</tr>
</tbody>
</table>


## Exemples de script RedistributeActiveDatabases.ps1

Cet exemple illustre la distribution des bases de données actuelles pour un groupe de disponibilité de base de données, notamment la liste de décompte des préférences.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table
```

Cet exemple illustre la redistribution et l’équilibrage des copies de base de données de boîtes aux lettres actives dans un groupe de disponibilité de base de données utilisant la préférence d’activation sans intervention de l’utilisateur.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False
```

Cet exemple illustre la redistribution et l’équilibrage des copies de base de données de boîtes aux lettres actives dans un groupe de disponibilité de base de données utilisant la préférence d’activation, ainsi que la création d’un récapitulatif de la distribution.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution
```

## Surveillance des copies de base de données

Une copie de base de données est votre premier recours en cas de panne touchant la copie active de la base de données. Il est donc essentiel de contrôler l’intégrité et l’état des copies de base de données pour s’assurer qu’elles seront disponibles, si nécessaire. En examinant les détails d’une copie de base de données dans le CAE, vous pouvez consulter une variété d’informations, dont la longueur de la file d’attente de copie, la longueur de la file d’attente de relecture, des informations d’état d’index de contenu et de statut. Vous pouvez aussi utiliser la cmdlet **Get-MailboxDatabaseCopyStatus** dans l’environnement de ligne de commande Exchange Management Shell pour afficher les diverses informations sur l’état d’une copie de base de données.

Pour plus d’informations sur la surveillance des copies de base de données, consultez la rubrique [Surveillance des groupes de disponibilité des bases de données](monitoring-database-availability-groups-exchange-2013-help.md).

## Suppression d’une copie de base de données

Une copie de base de données peut être supprimée à tout moment à l’aide du CAE ou de la cmdlet **Remove-MailboxDatabaseCopy** dans l’environnement de ligne de commande Exchange Management Shell. Après suppression d’une copie de base de données, vous devez manuellement supprimer tout fichier journal de transaction et de base de données du serveur à partir duquel la copie de base de données est en cours de suppression. Pour obtenir la procédure détaillée de suppression d’une copie de base de données, consultez la rubrique [Supprimer une copie de base de données de boîtes aux lettres](remove-a-mailbox-database-copy-exchange-2013-help.md).

## Permutation de base de données

Le serveur de boîtes aux lettres qui héberge la copie active de la base de données est le maître de la base de données de boîtes aux lettres. Le processus d’activation d’une copie de base de données active modifie le maître de la base de données de boîtes aux lettres et convertit la copie passive en nouvelle copie active. Ce processus est appelé basculement de base de données. Dans un basculement de base de données, la copie active de la base de données est démontée d’un serveur de boîtes aux lettres et une copie passive de cette base est montée en tant que nouvelle base de données de boîtes aux lettres active sur un autre serveur de boîtes aux lettres. Lorsque vous effectuez un basculement, vous pouvez éventuellement remplacer les paramètres de numérotation de montage de la base de données sur le nouveau maître de la base de données de boîtes aux lettres.

Vous pouvez rapidement identifier le serveur de boîtes aux lettres qui est actuellement le maître de la base de données de boîtes aux lettres en examinant la colonne de droite sous l’onglet **Copies de base de données** dans le CAE. Vous pouvez effectuer un basculement à l’aide du lien **Activer** dans le CAE ou à l’aide de la cmdlet **Move-ActiveMailboxDatabase** dans l’environnement de ligne de commande Exchange Management Shell.

Plusieurs vérifications internes seront effectuées avant l’activation de la copie passive :

  - L’état de la copie de base de données est contrôlé. Si la copie de base de données est indisponible, le basculement est bloqué. Vous pouvez modifier ce comportement et éviter le contrôle d’état en utilisant le paramètre *SkipHealthChecks* de la cmdlet **Move-ActiveMailboxDatabase**. Ce paramètre vous permet de déplacer la copie active vers une copie de base de données indisponible.

  - La copie de base de données active est vérifiée pour voir si elle est actuellement une source d’amorçage pour toute copie de base de données passive. Si la copie active est actuellement utilisée comme source d’amorçage, le basculement est bloqué. Vous pouvez modifier ce comportement et éviter le contrôle de source d’amorçage en utilisant le paramètre *SkipActiveCopyChecks* de la cmdlet **Move-ActiveMailboxDatabase**. Ce paramètre vous permet de déplacer une copie active qui est utilisée comme source d’amorçage. L’utilisation de ce paramètre entraîne l’annulation de l’opération d’amorçage qui est alors considérée défectueuse.

  - Les longueurs de la file d’attente de copie et de relecture de la copie de base de données sont contrôlées afin de veiller à ce que les valeurs correspondent aux critères configurés. De même, la copie de base de données est vérifiée pour s’assurer qu’elle n’est pas utilisée actuellement comme source d’amorçage. Si les valeurs des longueurs de file d’attente ne font pas partie des critères configurés ou si la base de données est actuellement utilisée comme source d’amorçage, le basculement est bloqué. Vous pouvez modifier ce comportement et éviter ces contrôles en utilisant le paramètre *SkipLagChecks* de la cmdlet **Move-ActiveMailboxDatabase**. Ce paramètre permet d’activer une copie disposant de files d’attente de relecture et de copie en dehors des critères configurés.

  - L’état du catalogue de recherche (index du contenu) de la copie de base de données est contrôlé. Si le catalogue de recherche n’est pas à jour, n’est pas en bon état ou est endommagé, le basculement est bloqué. Vous pouvez modifier ce comportement et éviter le contrôle du catalogue de recherche en utilisant le paramètre *SkipClientExperienceChecks* de la cmdlet **Move-ActiveMailboxDatabase**. Grâce à ce paramètre, la recherche n’effectue pas le contrôle d’état du catalogue. Si le catalogue de recherche de la copie de base de données que vous activez n’est pas en bon état ou est inexploitable et que vous utilisez ce paramètre pour passer le contrôle d’état du catalogue et activer la copie de base de données, il vous faudra à nouveau analyser ou amorcer le catalogue de recherche.

Lorsque vous effectuez un basculement de base de données, vous avez la possibilité de remplacer les paramètres de numérotation de montage configurés pour le serveur hébergeant la copie passive de base de données en train d’être activée. Le paramètre *MountDialOverride* de la cmdlet **Move-ActiveMailboxDatabase** donne l’ordre au serveur cible de remplacer ses propres paramètres de numérotation de montage et d’utiliser ceux indiqués par le paramètre *MountDialOverride*.

Pour obtenir la procédure détaillée de basculement d’une copie de base de données, consultez la rubrique [Activer une copie de la base de données de boîtes aux lettres](activate-a-mailbox-database-copy-exchange-2013-help.md).

