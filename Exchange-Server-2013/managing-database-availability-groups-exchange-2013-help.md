---
title: 'Gestion de groupes de disponibilité de base de données: Exchange 2013 Help'
TOCTitle: Gestion de groupes de disponibilité de base de données
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50478468
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion de groupes de disponibilité de base de données

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-10-04_

Un groupe de disponibilité de base de données (DAG) est composé d’un maximum de 16 serveurs de boîtes aux lettres Microsoft Exchange Server 2013 qui permettent une récupération automatique au niveau de la base de données en cas de défaillance d’une base de données, d’un serveur ou du réseau. Les groupes de disponibilité de base de données (DAG) utilisent la réplication continue et un sous-ensemble de technologies de clustering avec basculement Windows pour fournir la haute disponibilité et la résilience de site. Les serveurs de boîtes aux lettres d’un groupe de disponibilité de base de données (DAG) se surveillent mutuellement pour détecter les défaillances. Lorsqu’un serveur de boîtes aux lettres est ajouté à un groupe de disponibilité de base de données, il fonctionne avec les autres serveurs du groupe de disponibilité de base de données pour assurer la récupération automatique des défaillances de la base de données.

Lorsque vous créez un DAG, il est vide. Lorsque vous ajoutez le premier serveur au DAG, un cluster de basculement est automatiquement créé pour le DAG. En outre, l’infrastructure qui surveille les serveurs pour détecter les défaillances de réseau ou de serveur est lancée. Le mécanisme de pulsation du cluster de basculement et la base de données du cluster sont alors utilisés pour effectuer le suivi des informations liées au DAG et les gérer. Ces informations, qui peuvent changer rapidement, sont notamment l’état de montage de la base de données, l’état de réplication et le dernier emplacement monté.

**Contenu de cette rubrique**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## Création de groupes de disponibilité de base de données

Un groupe de disponibilité de base de données (DAG) peut être créé à l’aide de l’Assistant Nouveau groupe de disponibilité de base de données dans le Centre d’administration Exchange (CAE) ou en exécutant la cmdlet **New-DatabaseAvailabilityGroup** dans l’environnement de ligne de commande Exchange Management Shell. Lorsque vous créez un DAG, vous lui donnez un nom, et accessoirement un serveur témoin ainsi que des paramètres de répertoire témoin. En outre, vous pouvez affecter une ou plusieurs adresses IP au DAG soit par le biais d’adresses IP statiques, soit en permettant au DAG d’affecter automatiquement les adresses IP nécessaires à l’aide du protocole DHCP (Dynamic Host Configuration Protocol). Vous pouvez affecter manuellement des adresses IP au groupe de disponibilité de base de données en utilisant le paramètre *DatabaseAvailabilityGroupIpAddresses*. Si vous omettez ce paramètre, le DAG tentera d’obtenir une adresse IP en utilisant un serveur DHCP sur votre réseau.

Si vous créez un DAG destiné à contenir des serveurs de boîtes aux lettres exécutant Windows Server 2012 R2, vous avez également la possibilité de créer un DAG sans point d’accès administratif de cluster. Dans ce cas, le groupe n’aura pas d’objet nom de cluster (CNO) dans Active Directory et le groupe de ressources de base du cluster ne contiendra pas de ressource de nom de réseau ni de ressource d’adresse IP.

Pour obtenir la procédure détaillée de création d’un DAG, voir [Créer un groupe de disponibilité de base de données](create-a-database-availability-group-exchange-2013-help.md).

Lorsque vous créez un DAG, un objet vide représentant le DAG portant le nom que vous avez indiqué et une classe d’objet du**msExchMDBAvailabilityGroup** sont créés dans Active Directory.

Les DAG utilisent un sous-ensemble de technologies de clustering avec basculement Windows ; il peut s’agir notamment de la pulsation de clusters, de réseaux de clusters et d’une base de données de clusters (pour stocker les données qui changent ou qui peuvent changer rapidement, par exemple lorsque l’état d’une base de données passe d’actif à passif et inversement ou de montée à démontée et inversement). Comme les groupes de disponibilité de base de données (DAG) reposent sur le clustering avec basculement Windows, ils peuvent uniquement être créés sur des serveurs de boîtes aux lettres Exchange 2013 fonctionnant sous Windows Server 2008 R2 Enterprise ou Datacenter, sous Windows Server 2012 Standard ou Datacenter, ou sous Windows Server 2012 R2 Standard ou Datacenter.

> [!NOTE]
> Le cluster de basculement créé et utilisé par le groupe de disponibilité de base de données (DAG) doit être dédié au DAG. Le cluster ne peut pas être utilisé pour toute autre solution de disponibilité élevée ou pour tout autre rôle. Par exemple, le cluster de basculement ne peut pas être utilisé pour mettre en cluster d’autres applications ou services. L’utilisation d’un cluster de basculement du groupe de disponibilité de base de données pour des rôles autres que le DAG n’est pas prise en charge.


## Serveur témoin et répertoire témoin de groupe de disponibilité de base (DAG)

Lorsque vous créez un DAG, vous devez lui donner un nom contenant 15 caractères au maximum et unique dans la forêt Active Directory. En outre, chaque DAG est configuré avec un serveur et un répertoire témoins. Le serveur témoin et son répertoire ne sont utilisés que lorsqu’il y a un nombre pair de membres dans le groupe de disponibilité de base (DAG), puis seulement à des fins de quorum. Il n’est pas nécessaire de créer le répertoire témoin à l’avance. Exchange crée et sécurise automatiquement le répertoire pour vous sur le serveur témoin. Le répertoire ne doit pas être utilisé pour autre chose que le serveur DAG témoin.

La configuration requise pour le serveur témoin est la suivante :

  - Le serveur témoin ne peut pas être membre DAG.

  - Le serveur témoin doit se trouver dans la même forêt Active Directory que le groupe de disponibilité de base de données.

  - Le serveur témoin doit exécuter une version prise en charge de Windows Server. Pour plus d’informations, consultez [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Un serveur unique peut servir de témoin pour plusieurs groupes de disponibilité de base de données. Cependant, chaque groupe de disponibilité nécessite son propre répertoire témoin.

Quel que soit le serveur utilisé comme serveur témoin, si le pare-feu Windows est activé sur le serveur témoin désigné, vous devez activer l’exception du pare-feu Windows pour le partage de fichiers et d’imprimantes.

> [!important]
> Si le serveur témoin que vous spécifiez n’est pas un serveur Exchange 2013 ou Exchange 2010, vous devez ajouter le groupe de sécurité universel (USG) du sous-système approuvé Exchange au groupe Administrateurs local sur le serveur témoin avant de créer le groupe de disponibilité de base de données (DAG). Ces autorisations de sécurité sont nécessaires pour garantir que Exchange peut créer un répertoire et un partage sur le serveur témoin au besoin.
> Le serveur témoin utilise le port SMB 445.


Il n’est pas nécessaire que le serveur témoin et le répertoire témoin aient une tolérance de panne ni une autre forme de redondance ou de haute disponibilité. Il n’est pas nécessaire d’utiliser un serveur de fichiers en cluster pour le serveur témoin ni d’employer une autre forme de résilience pour le serveur témoin. et ce pour plusieurs raisons. Dans les grands DAG (par exemple, avec six membres ou plus), il faut plusieurs pannes avant d’avoir besoin d’un serveur témoin. Comme un DAG à six membres peut tolérer un maximum de deux pannes de serveur sans perdre de quorum, il faudrait que trois membres tombent en panne avant que le serveur témoin soit nécessaire pour maintenir le quorum. De même, si une panne touche votre serveur témoin actuel (par exemple, si vous perdez le serveur témoin à cause d’une défaillance matérielle), vous pouvez employer la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) pour configurer un nouveau serveur témoin et un répertoire témoin (si vous avez un quorum).

> [!NOTE]
> Vous pouvez aussi utiliser la cmdlet <strong>Set-DatabaseAvailabilityGroup</strong> pour configurer le serveur témoin et le répertoire témoin à l’emplacement d’origine si le serveur témoin a perdu son stockage ou si quelqu’un a modifié les autorisations de partage ou du répertoire témoin.


## Considérations relatives au placement du serveur témoin

Le placement du serveur témoin d’un DAG dépend des besoins de votre entreprise et des options disponibles pour votre organisation. Exchange 2013 inclut la prise en charge de nouvelles options de configuration de DAG qui ne sont pas recommandées ou qui n’existent pas dans les versions précédentes d’Exchange. Ces options incluent l’utilisation d’un troisième emplacement, comme un troisième centre de données, une filiale ou un réseau virtuel Microsoft Azure.

Le tableau suivant répertorie les recommandations générales en matière de placement du serveur témoin pour différents scénarios de déploiement.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scénario de déploiement</th>
<th>Recommandations</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DAG unique déployé dans un seul centre de données</p></td>
<td><p>Placer le serveur témoin dans le même centre de données que les membres du DAG</p></td>
</tr>
<tr class="even">
<td><p>DAG unique déployé dans deux centres de données ; aucun emplacement supplémentaire disponible</p></td>
<td><p>Placer le serveur témoin dans un réseau virtuel Microsoft Azure pour permettre le basculement automatique du centre de données, ou</p>
<p>Placer le serveur témoin dans le centre de données principal</p></td>
</tr>
<tr class="odd">
<td><p>Plusieurs DAG déployés dans un seul centre de données</p></td>
<td><p>Placer le serveur témoin dans le même centre de données que les membres du DAG. Les options supplémentaires suivantes sont disponibles :</p>
<ul>
<li><p>Utilisation du même serveur témoin pour plusieurs DAG</p></li>
<li><p>Utilisation d’un membre du DAG qui servira de serveur témoin pour un autre DAG</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Plusieurs DAG déployés dans deux centres de données</p></td>
<td><p>Placer le serveur témoin dans un réseau virtuel Microsoft Azure pour permettre le basculement automatique du centre de données, ou</p>
<p>Placer le serveur témoin dans le centre de données considéré comme le centre principal pour chaque DAG. Les options supplémentaires suivantes sont disponibles :</p>
<ul>
<li><p>Utilisation du même serveur témoin pour plusieurs DAG</p></li>
<li><p>Utilisation d’un membre du DAG qui servira de serveur témoin pour un autre DAG</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Un ou plusieurs DAG déployés dans plus de deux centres de données</p></td>
<td><p>Dans cette configuration, le serveur témoin doit être situé dans le centre de données dans lequel vous souhaitez que la plupart des votes de quorum figurent.</p></td>
</tr>
</tbody>
</table>


Lorsqu’un groupe de disponibilité de base (DAG) a été déployé dans deux centres de données, une nouvelle option de configuration dans Exchange 2013 permet d’utiliser un troisième emplacement pour héberger le serveur témoin. Si votre organisation dispose d’un troisième emplacement avec une infrastructure réseau protégée contre les pannes de réseau qui affectent les deux centres de données dans lesquels votre groupe de disponibilité de base (DAG) est déployé, vous pouvez déployer le serveur témoin du DAG dans ce troisième emplacement. Cela permet de configurer votre DAG afin qu’il bascule automatiquement les bases de données vers l’autre centre de données en cas de défaillance de niveau centre de données. Si votre organisation n'a que deux emplacements physiques, vous pouvez utiliser un réseau virtuel Microsoft Azure comme troisième emplacement pour placer votre serveur témoin.

## Spécification d’un serveur témoin et d’un répertoire témoin lors de la création d’un groupe de disponibilité de base (DAG)

Lorsque vous créez un groupe de disponibilité de base de données, vous devez lui donner un nom. Vous pouvez aussi éventuellement spécifier un serveur témoin et un répertoire témoin.

Lors de la création d’un DAG, les combinaisons de comportements et d’options suivantes sont disponibles :

  - Vous pouvez n’indiquer que le nom du DAG et laisser les champs **Serveur témoin** et **Répertoire témoin** vides. Dans ce scénario, l’Assistant recherche sur le site Active Directory local un serveur d’accès au client où le serveur de boîtes aux lettres n’est pas installé et crée automatiquement le répertoire par défaut (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) et le partage par défaut (\<*DAGFQDN*\>) sur ce serveur, puis utilise ce serveur d’accès au client comme serveur témoin. Par exemple, prenons le serveur témoin CAS3 sur lequel nous avons installé le système d’exploitation sur le lecteur C. Un groupe de disponibilité de base (DAG) nommé DAG1 dans le domaine contoso.com doit utiliser un répertoire témoin par défaut de C:\\DAGFileShareWitnesses\\DAG1.contoso.com, qui doit être partagé en tant que \\\\CAS3\\DAG1.contoso.com.

  - Vous pouvez donner un nom au groupe de disponibilité de base de données, au serveur témoin que vous souhaitez utiliser et au répertoire qui sera créé et partagé sur le serveur témoin.

  - Vous pouvez donner un nom au DAG et au serveur témoin que vous voulez utiliser et laisser le champ **Répertoire témoin** vide. Dans ce scénario, l’Assistant va créer le répertoire par défaut sur le serveur témoin spécifié.

  - Vous pouvez donner un nom au DAG, laisser le champ **Serveur témoin** vide et spécifier le répertoire que vous voulez créer et partager sur le serveur témoin. Dans ce scénario, l’Assistant recherche un serveur d’accès au client où le serveur de boîtes aux lettres n’est pas installé et crée automatiquement le groupe de disponibilité de base (DAG) spécifié sur ce serveur, partage le répertoire, puis utilise ce serveur d’accès au client comme serveur témoin.

Une fois le DAG formé, il utilisera d’abord le modèle de quorum Nœud Majoritaire. Une fois la deuxième boîte aux lettres ajoutée au DAG, le quorum est automatiquement changé en un modèle de quorum de nœuds et partage de fichiers majoritaire. Lorsque ce changement se produit, le cluster du groupe de disponibilité de base (DAG) commence à utiliser le serveur témoin pour conserver le quorum. Si le répertoire témoin n’existe pas, Exchange le crée automatiquement, le partage et lui fournit les autorisations de contrôle total sur le compte d’ordinateur de l’objet nom de cluster du DAG.

> [!NOTE]
> L’utilisation d’un partage de fichiers intégré à l’espace de noms du système de fichiers distribués (DFS) n’est pas prise en charge.


Si le pare-feu Windows est activé sur le serveur témoin avant la création du DAG, celle-ci risque d’être bloquée. Exchange utilise Windows WMI (Windows Management Instrumentation) pour créer le répertoire et le partage de fichiers sur le serveur témoin. Si le pare-feu Windows est activé sur le serveur témoin et qu’aucune exception de pare-feu n’est configurée pour WMI, la cmdlet **New-DatabaseAvailabilityGroup** va échouer en indiquant une erreur. Si vous spécifiez un serveur témoin mais pas de répertoire témoin, vous obtiendrez le message d’erreur suivante.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>La tâche n’a pas réussi à créer le répertoire témoin par défaut sur le serveur &lt;<em>Nom de serveur</em>&gt;. Indiquez manuellement un répertoire témoin.</p></td>
</tr>
</tbody>
</table>


Si vous spécifiez un serveur témoin mais pas de répertoire témoin, vous obtiendrez le message d’avertissement suivant.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossible d’accéder aux partages de fichiers sur le serveur témoin ’<em>ServerName</em>’. Le groupe de disponibilité de base de données risque d’être plus vulnérable aux échecs tant que ce problème n’aura pas été résolu. Vous pouvez utiliser la cmdlet Set-DatabaseAvailabilityGroup pour retenter l’opération. Erreur : Le chemin réseau n’a pas été trouvé.</p></td>
</tr>
</tbody>
</table>


Si le pare-feu Windows est activé sur le serveur témoin après création du DAG mais avant l’ajout des serveurs, l’ajout ou le retrait des membres du DAG risque d’être bloqué. Si le pare-feu Windows est activé sur le serveur témoin et qu’aucune exception de pare-feu n’est configurée pour WMI, la cmdlet **Add-DatabaseAvailabilityGroupServer** va échouer en indiquant une erreur.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossible de créer le répertoire témoin de partage de fichiers ’C:\DAGFileShareWitnesses\DAG_FQDN’ sur le serveur témoin <em>’ServerName’</em>. Le groupe de disponibilité de base de données risque d’être plus vulnérable aux échecs tant que ce problème n’aura pas été résolu. Vous pouvez utiliser la cmdlet Set-DatabaseAvailabilityGroup pour retenter l’opération. Erreur : Une exception WMI s’est produite sur le serveur <em>’ServerName’</em> : Le serveur RPC n’est pas disponible. (Exception de HRESULT : 0x800706BA)</p></td>
</tr>
</tbody>
</table>


Pour corriger cette erreur et les avertissements, effectuez une des opérations suivantes :

  - Créez manuellement le répertoire témoin et effectuez le partage sur le serveur témoin. Puis attribuez l’objet réseau de cluster (CNO) pour le contrôle total du groupe de disponibilité de base de données pour le répertoire et le partage.

  - Activez l’exception WMI dans le pare-feu Windows.

  - Désactivez le pare-feu Windows.

Retour au début

## Appartenance au groupe de disponibilité de base (DAG)

Après avoir créé un groupe de disponibilité de base (DAG), vous pouvez ajouter des serveurs au DAG ou en supprimer à l’aide de l’Assistant Gestion de groupe de disponibilité de base de données du Centre d’administration Exchange (EAC) ou à l’aide des cmdlets **Add-DatabaseAvailabilityGroupServer** ou **Remove-DatabaseAvailabilityGroupServer** dans l’environnement de ligne de commande Exchange Management Shell. Pour obtenir la procédure détaillée de gestion de l’appartenance aux DAG, voir [Gérer l’appartenance au groupe de disponibilité de la base de données](manage-database-availability-group-membership-exchange-2013-help.md).

> [!NOTE]
> Chaque serveur de boîtes aux lettres membre d’un groupe de disponibilité de la base de données constitue également un nœud dans le cluster sous-jacent, utilisé par le groupe de disponibilité de la base de données. Par conséquent, un serveur de boîtes aux lettres peut être membre d’un seul groupe de disponibilité de la base de données.


Si le serveur de boîte aux lettres ajouté au DAG n’a pas le composant de clustering avec basculement, la méthode utilisée pour ajouter le serveur (par exemple, la cmdlet **Add-DatabaseAvailabilityGroupServer** ou l’Assistant de gestion du groupe de disponibilité de base de données) installera la fonction de clustering avec basculement.

Voici ce qui se passe quand le premier serveur de boîte aux lettres est ajouté à un DAG :

  - Le composant de clustering avec basculement Windows est installé, s’il ne l’est pas déjà.

  - Un cluster de basculement est créé avec le nom du DAG. Ce cluster de basculement est utilisé uniquement par le groupe de disponibilité de base de données (DAG) et ce cluster doit être dédié au DAG. L’utilisation du cluster à d’autres fins n’est pas prise en charge.

  - Un objet réseau de cluster (CNO) est créé dans le conteneur des ordinateurs par défaut.

  - Le nom et l’adresse IP du DAG figurent comme enregistrement d’hôte (A) dans DNS (Domain Name System).

  - Le serveur est ajouté à l’objet DAG dans Active Directory.

  - La base de données du cluster est mise à jour avec les informations sur les bases de données montées sur le serveur ajouté.

Dans les grands environnements ou à sites multiples, ceux dans lesquels le DAG est étendu à plusieurs sites Active Directory, vous devez attendre la réplication Active Directory de l’objet DAG contenant le premier membre DAG à traiter. Si cet objet Active Directory n’est pas répliqué dans tout l’environnement, l’ajout du second serveur risque de provoquer la création d’un nouveau cluster (ainsi qu’un nouvel objet réseau de cluster) pour le DAG. Cela est dû au fait que l’objet DAG apparaît vide dans la perspective du second membre ajouté, ce qui provoquera par conséquent la création d’un cluster et d’un objet réseau de cluster pour le DAG par le biais de la cmdlet **Add-DatabaseAvailabilityGroupServer**, même si ces objets existent déjà. Pour vérifier que l’objet DAG contenant le premier serveur DAG a été répliqué, utilisez la cmdlet **Get-DatabaseAvailabilityGroup** sur le second serveur en cours d’ajout et vérifiez que le premier serveur ajouté est répertorié en tant que membre DAG.

Voici ce qui se passe quand les serveurs suivants sont ajoutés au DAG :

  - Le serveur est joint au cluster de basculement Windows pour le DAG.

  - Le modèle de quorum est automatiquement réglé :
    
      - Un modèle de quorum Nœud majoritaire est utilisé pour les DAGs ayant un nombre impair de membres.
    
      - Un modèle de quorum Nœud et partage de fichiers majoritaire est utilisé pour les DAGs ayant un nombre de membres pair.

  - Le répertoire témoin et le partage témoin sont automatiquement créés par Exchange si nécessaire.

  - Le serveur est ajouté à l’objet DAG dans Active Directory.

  - La base de données du cluster est mise à jour avec les informations sur les bases de données montées.

> [!NOTE]
> Le changement de modèle de quorum doit se produire automatiquement. Toutefois, si le modèle de quorum n’est pas changé automatiquement vers le modèle approprié, vous pouvez exécuter la cmdlet <strong>Set-DatabaseAvailabilityGroup</strong> avec seulement le paramètre <em>Identity</em> pour modifier les réglages de quorum du DAG.


## Préconfiguration de l’objet nom de cluster pour un groupe de disponibilité de base de données (DAG)

L’objet réseau de cluster (CNO) est un compte d’ordinateur qui est créé dans Active Directory et associé à la ressource Nom du cluster. La ressource Nom du cluster est liée à l’objet réseau de cluster représentant un objet Kerberos qui agit comme identité du cluster et fournit le contexte de sécurité du cluster. Comme indiqué précédemment, la formation du cluster sous-jacent DAG et de l’objet réseau de cluster pour ce cluster est effectuée lorsque le premier membre est ajouté au DAG. Lorsque le premier serveur est ajouté au DAG, l’instance PowerShell distante contacte le service de réplication d’Microsoft Exchange sur le serveur de boîtes aux lettres ajouté. Le service de réplication Microsoft Exchange installe la fonctionnalité de cluster de basculement (si celle-ci n’est pas déjà installée) et commence le processus de création du cluster. Le service de réplication Microsoft Exchange s’exécute dans le contexte de sécurité du système local et c’est dans ce contexte que la création du cluster est effectuée.

> [!WARNING]
> Si les membres de votre groupe de disponibilité de base de données (DAG) exécutent Windows Server 2012, vous devez préconfigurer l’objet réseau de cluster (CNO) avant d’ajouter le premier serveur au groupe de disponibilité de base de données (DAG). Si les membres du DAG exécutent Windows Server 2012 R2 et que vous créez un DAG sans point d’accès administratif de cluster, aucun CNO n’est créé et il n’est pas nécessaire de créer de CNO pour le DAG.


Dans des environnements où la création de compte d’ordinateur est restreinte ou lorsque des comptes d’ordinateur sont créés dans un conteneur autre que le conteneur d’ordinateurs par défaut, vous pouvez préconfigurer et approvisionner l’objet réseau de cluster. Vous pouvez créer et désactiver un compte d’ordinateur pour l’objet réseau de cluster, puis vous pouvez :

  - attribuer le contrôle total du compte d’ordinateur au compte d’ordinateur du premier serveur de boîte aux lettres ajoutée au groupe de disponibilité de base de données.

  - attribuer le contrôle total du compte d’ordinateur au groupe de sécurité universel du sous-système approuvé Exchange.

L’attribution du contrôle total du compte d’ordinateur au compte d’ordinateur du premier serveur de boîte aux lettres que vous ajoutez au DAG garantit que le contexte de sécurité du système local pourra gérer le compte d’ordinateur préconfiguré. L’attribution du contrôle total du compte d’ordinateur au groupe de sécurité universel du sous-système approuvé Exchange peut être utilisée à la place car le groupe de sécurité universel du sous-système approuvé Exchange contient les comptes d’ordinateur de tous les serveurs Exchange du domaine.

Pour obtenir la procédure détaillée pour préconfigurer et approvisionner l’objet réseau de cluster pour un DAG, consultez la rubrique [Préinstallation de l’objet nom de cluster pour un groupe de disponibilité de base de données](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

## Suppression des serveurs d’un groupe de disponibilité de base de données (DAG)

Les serveurs de boîtes aux lettres peuvent être supprimés d’un groupe de disponibilité de base de données (DAG) à l’aide de l’Assistant Gestion des groupes de disponibilité de base de données du Centre d’administration Exchange (EAC) ou à l’aide de la cmdlet **Remove-DatabaseAvailabilityGroupServer** dans l’environnement de ligne de commande Exchange Management Shell. Toutes les bases de données de boîtes aux lettres répliquées doivent être retirées du serveur avant de pouvoir supprimer un serveur de boîte aux lettres d’un DAG. Si vous essayez de supprimer un serveur de boîte aux lettres comprenant des bases de données de boîtes aux lettres répliquées, la tâche échouera.

Dans le cadre de certaines procédures, il faut supprimer un serveur de boîte aux lettres d’un DAG avant d’effectuer certaines opérations. Ces différents cas de figure sont présentés ci-dessous :

  - **Opération de récupération d’un serveur**   Si un serveur de boîtes aux lettres membre d’un groupe de disponibilité de base de données est perdu ou tombe en panne et s’avère irrécupérable et nécessite d’être remplacé, vous pouvez effectuer une opération de récupération de serveur à l’aide du commutateur **Setup /m:RecoverServer**. Toutefois, avant de pouvoir effectuer cette opération, il vous faut d’abord supprimer le serveur du DAG à l’aide de la cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/fr-fr/library/dd297956\(v=exchg.150\)) avec le paramètre *ConfigurationOnly*.

  - **Suppression du groupe de disponibilité de base de données**   Dans certains cas, vous aurez peut-être besoin de supprimer un DAG (par exemple, si vous désactivez le mode de réplication tiers). Si vous avez besoin de supprimer un DAG, il vous faut d’abord en effacer tous les serveurs. Si vous essayez de supprimer un DAG qui contient des membres, la tâche échouera.

Retour au début

## Configuration des propriétés du groupe de disponibilité de base de données (DAG)

Une fois les serveurs ajoutés au DAG, vous pouvez utiliser le Centre d’administration Exchange (EAC) ou l’environnement de ligne de commande Exchange Management Shell pour configurer les propriétés d’un DAG, y compris le serveur et le répertoire témoins utilisés par le DAG, ainsi que les adresses IP affectées à celui-ci.

Les propriétés configurables sont les suivantes :

  - **Serveur témoin**   Nom du serveur que vous avez choisi pour héberger le partage de fichiers pour le témoin de partage de fichiers. Nous vous recommandons de spécifier un serveur d’accès au client en tant que serveur témoin. Cela permet au système de configurer, de sécuriser et d’utiliser automatiquement le partage si nécessaire, mais permet également à l’administrateur de messagerie de connaître la disponibilité du serveur témoin.

  - **Répertoire témoin**   Nom du répertoire qui sera utilisé pour stocker les données du témoin de partage de fichiers. Ce répertoire sera automatiquement créé par le système sur le serveur témoin spécifié.

  - **Adresses IP du groupe de disponibilité de base de données**   Une ou plusieurs adresses IP doivent être affectées au DAG, sauf si les membres du DAG exécutent Windows Server 2012 R2 et que vous créez un DAG sans adresse IP. Dans le cas contraire, les adresses IP du DAG peuvent être configurées à l’aide d’adresses IP statiques affectées manuellement, ou être automatiquement affectées au DAG à l’aide d’un serveur DHCP de votre organisation.

L’environnement de ligne de commande Exchange Management Shell vous permet de configurer des propriétés du groupe de disponibilité de base de données (DAG) qui ne sont pas accessibles dans le Centre d’administration Exchange (EAC) comme les adresses IP du DAG, les paramètres de chiffrement et de compression réseau, la découverte du réseau, le port TCP utilisé pour la réplication et d’autres paramètres de serveur témoin et de répertoire témoin, et aussi pour activer le mode de coordination de l’activation du centre de données.

Pour obtenir la procédure détaillée sur la configuration des propriétés DAG, voir [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md).

## Chiffrement du réseau DAG

Les DAG prennent en charge l’utilisation du chiffrement en tirant parti des capacités de chiffrement du système d’exploitation Windows Server. Les DAG utilisent l’authentification Kerberos entre les serveurs Exchange. Les API EncryptMessage et DecryptMessage du SSP (Security Support Provider) de Microsoft Kerberos gèrent le chiffrement du trafic réseau DAG. Le SSP de Microsoft Kerberos prend en charge plusieurs algorithmes de chiffrement. (Pour obtenir la liste complète, consultez la section 3.1.5.2, « Encryption Types » (Types de chiffrement) du fichier sur les [extensions du protocole Kerberos](https://go.microsoft.com/fwlink/p/?linkid=179131)). Le protocole de liaison d’authentification Kerberos choisit les meilleurs protocoles de chiffrement pris en charge dans la liste : généralement l’algorithme d’encodage AES (Advanced Encryption Standard) 256 bits, potentiellement avec HMAC (Hash-based Message Authentication Code) SHA pour conserver l’intégrité des données. Pour plus d’informations, voir [HMAC](https://fr.wikipedia.org/wiki/keyed-hash_message_authentication_code).

Le chiffrement de réseau est une propriété du DAG, et non un réseau DAG. Vous pouvez configurer le chiffrement du réseau DAG à l’aide de la cmdlet **Set-DatabaseAvailabilityGroup** dans l’environnement de ligne de commande Exchange Management Shell. Les paramètres de chiffrement possibles pour les communications d’un réseau DAG figurent dans le tableau suivant.

### Paramètres de chiffrement des communications d’un réseau DAG

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
<td><p>Désactivé</p></td>
<td><p>Le chiffrement réseau n’est pas utilisé.</p></td>
</tr>
<tr class="even">
<td><p>Activé</p></td>
<td><p>Le chiffrement de réseau est utilisé sur tous les réseaux DAG pour la réplication et l’amorçage.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>Le chiffrement de réseau est utilisé sur les réseaux DAG lors de la réplication entre différents sous-réseaux. Il s’agit du paramètre par défaut.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>Le chiffrement de réseau est utilisé sur tous les réseaux DAG pour l’amorçage uniquement.</p></td>
</tr>
</tbody>
</table>


## Compression d’un réseau DAG

Les DAG prennent également en charge la compression intégrée. Lorsque la compression est activée, la communication de réseau DAG utilise XPRESS, l’implémentation Microsoft de l’algorithme LZ77. Pour plus d’informations, voir [Explication de l’algorithme de décompression](http://www.zlib.net/feldspar.html) et la section 3.1.4.11.1.2.1, « LZ77 Compression Algorithm » (Algorithme de compression LZ77) de [Spécification du protocole au format câble](https://go.microsoft.com/fwlink/p/?linkid=179133). Ce type de compression est le même que celui qui est utilisé dans de nombreux protocoles Microsoft, en particulier le protocole MAPI RPC utilisé pour la compression entre Microsoft Outlook et Exchange.

Comme le chiffrement de réseau, la compression réseau est aussi une propriété du DAG, et non un réseau DAG. La configuration de la compression réseau DAG se fait à l’aide de la cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/fr-fr/library/dd297934\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell. Les paramètres de compression possibles pour les communications d’un réseau DAG figurent dans le tableau suivant.

### Paramètres de compression de communication de réseau DAG

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
<td><p>Désactivé</p></td>
<td><p>La compression réseau n’est pas utilisée.</p></td>
</tr>
<tr class="even">
<td><p>Activé</p></td>
<td><p>La compression réseau est utilisée sur tous les réseaux DAG pour la réplication et l’amorçage.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>La compression réseau est utilisée sur les réseaux DAG lors de la réplication entre différents sous-réseaux. Il s’agit du paramètre par défaut.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>La compression réseau est utilisée sur tous les réseaux DAG pour l’amorçage uniquement.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Réseaux DAG

Un réseau DAG est constitué d’un ou de plusieurs sous-réseaux utilisés pour le trafic de réplication ou le trafic MAPI. Chaque DAG contient au maximum un réseau MAPI et zéro, un ou plusieurs réseaux de réplication.

## Configurations de carte réseau unique

Dans des configurations de carte réseau unique, le même réseau est utilisé pour le trafic de réplication et le trafic MAPI. À des fins de simplification, une carte réseau unique est la configuration recommandée pour les serveurs Exchange. Il est donc possible d’avoir des trafics MAPI et de réplication sur le même réseau.

## Configurations de carte réseau double

En règle générale, vous n’avez besoin d’utiliser des cartes réseau doubles que lorsque l’augmentation du trafic réseau est susceptible de saturer une carte réseau unique.

Dans des configurations de carte réseau double, un réseau est généralement consacré au trafic de réplication et le second est principalement utilisé pour le trafic MAPI. Vous pouvez également ajouter des cartes réseau à chaque membre DAG et configurer des réseaux DAG supplémentaires en tant que réseaux de réplication.

> [!NOTE]
> En cas d’utilisation de plusieurs réseaux de réplication, il n’y a aucun moyen de spécifier un ordre de priorité pour l’utilisation des réseaux. sélectionne de manière aléatoire un réseau de réplication dans le groupe de réseaux de réplication à utiliser pour la copie des journaux de transaction.


Dans Exchange 2010, la configuration manuelle des réseaux DAG était nécessaire dans plusieurs scénarios. Dans Exchange 2013, par défaut, les réseaux DAG sont automatiquement configurés par le système. Pour pouvoir créer ou modifier des réseaux DAG, vous devez d’abord activer le contrôle de réseau DAG manuel en exécutant la commande suivante :

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

Après avoir activé la configuration manuelle du réseau DAG, vous pouvez utiliser la cmdlet **New-DatabaseAvailabilityGroupNetwork** dans l’environnement de ligne de commande Exchange Management Shell pour créer un réseau DAG. Pour obtenir la procédure détaillée de création d’un réseau DAG, voir [Création d’un réseau de groupe de disponibilité de la base de données](create-a-database-availability-group-network-exchange-2013-help.md).

Vous pouvez utiliser la cmdlet **Set-DatabaseAvailabilityGroupNetwork** dans l’environnement de ligne de commande Exchange Management Shell pour configurer les propriétés de réseau DAG. Pour obtenir la procédure détaillée sur la configuration des propriétés de réseau DAG, voir [Configuration des propriétés du réseau de groupe de disponibilité de la base de données](configure-database-availability-group-network-properties-exchange-2013-help.md). Chaque réseau DAG a des paramètres obligatoires et facultatifs qu’il faut configurer :

  - **Nom du réseau**   Un nom unique pour le réseau DAG pouvant contenir jusqu’à 128 caractères.

  - **Description du réseau**   Description facultative du réseau DAG pouvant contenir jusqu’à 256 caractères.

  - **Sous-réseaux de réseau**   Un ou plusieurs réseaux entrés à l’aide du format *IPAddress/Bitmask* (par exemple, 192.168.1.0/24 pour les sous-réseaux IPv4 (Internet Protocol version 4) ; 2001:DB8:0:C000::/64 pour les sous-réseaux IPv6 (Internet Protocol version 6).

  - **Activer la réplication**   Dans le Centre d’administration Exchange (EAC), cochez la case pour dédier le réseau DAG au trafic de réplication et bloquer le trafic MAPI. Cochez la case pour empêcher la réplication via le réseau DAG et pour activer le trafic MAPI. Dans l’environnement de ligne de commande Exchange Management Shell, utilisez le paramètre *ReplicationEnabled* de la cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298008\(v=exchg.150\)) pour activer ou désactiver la réplication.

> [!NOTE]
> La désactivation de la réplication sur votre réseau MAPI ne garantit pas que le système n’utilise pas ce réseau pour la réplication. Si tous les réseaux de réplication configurés sont hors connexion, en panne ou indisponibles pour une autre raison, et que seul reste le réseau MAPI (qui n’est pas activé pour la réplication), alors le système utilise le réseau MAPI pour la réplication.


Les réseaux DAG initiaux (par exemple, MapiDagNetwork et ReplicationDagNetwork01) créés par le système sont basés sur les sous-réseaux énumérés par le service de cluster. Chaque membre du groupe de disponibilité de base de données doit disposer du même nombre de cartes réseau et chaque carte réseau doit disposer d’une adresse IPv4 (et facultativement d’une adresse IPv6) sur un sous-réseau unique. Plusieurs membres du groupe de disponibilité de base de données peuvent disposer d’adresses IPv4 sur le même sous-réseau mais chaque carte réseau et chaque paire d’adresse IP d’un membre du groupe de disponibilité de base de données spécifique doivent se trouver sur un sous-réseau unique. En outre, uniquement la carte utilisée pour le réseau MAPI devrait être configurée avec une passerelle par défaut. Les réseaux de réplication ne devraient pas être configurés avec une passerelle par défaut.

Par exemple, imaginez DAG1, DAG à deux membres où chaque membre a deux cartes réseau (une dédiée pour le réseau MAPI et l’autre pour le réseau de réplication). Les paramètres de configuration de l’adresse IP sont affichés dans le tableau suivant.

### Exemple de paramètres de carte réseau

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Carte réseau-serveur</th>
<th>Adresse IP/masque de sous-réseau</th>
<th>Passerelle par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replication</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replication</p></td>
<td><p>10.0.0.16</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


Dans la configuration suivante, il existe deux sous-réseaux configurés dans le groupe de disponibilité de base de données : 192.168.1.0 et 10.0.0.0. Lorsque EX1 et EX2 sont ajoutés au groupe de disponibilité de base de données, deux sous-réseaux seront énumérés et deux réseaux DAG seront créés : MapiDagNetwork (192.168.1.0) et ReplicationDagNetwork01 (10.0.0.0). Ces réseaux seront configurés comme indiqué dans le tableau suivant.

### Paramètres de réseau DAG énumérés pour un DAG de sous-réseau unique

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>Sous-réseaux</th>
<th>Interfaces</th>
<th>Accès MAPI activé</th>
<th>Réplication activée</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Pour achever la configuration de ReplicationDagNetwork01 en tant que réseau de réplication dédié, désactivez la réplication pour MapiDagNetwork en exécutant la commande suivante.

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

Une fois la réplication désactivée pour MapiDagNetwork, le service de réplication Microsoft Exchange utilise ReplicationDagNetwork01 pour la réplication continue. Si ReplicationDagNetwork01 échoue, le service de réplication Microsoft Exchange utilise de nouveau MapiDagNetwork pour la réplication continue. Cette opération est effectuée intentionnellement par le système pour maintenir une disponibilité élevée.

## Déploiement de réseaux DAG et de plusieurs sous-réseaux

Dans l’exemple précédent, même si deux sous-réseaux différents sont en cours d’utilisation par le groupe de disponibilité de base de données (192.168.1.0 et 10.0.0.0), ce groupe est considéré comme DAG de sous-réseau unique car chaque membre utilise le même sous-réseau pour former le réseau MAPI. Lorsque les membres DAG utilisent différents sous-réseaux pour le réseau MAPI, ce DAG est appelé *DAG de sous-réseaux multiples*. Dans un DAG à plusieurs sous-réseaux, les sous-réseaux sont automatiquement associés au réseau DAG correspondant.

Par exemple, imaginez DAG2, un DAG à deux membres où chaque membre dispose de deux cartes réseau (une dédiée pour le réseau MAPI et l’autre pour le réseau de réplication). En outre, chaque membre DAG se trouve dans un site Active Directory distinct avec son réseau MAPI sur un sous-réseau différent. Les paramètres de configuration de l’adresse IP sont affichés dans le tableau suivant.

### Exemple de paramètres de carte réseau pour un DAG de sous-réseaux multiples

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Carte réseau-serveur</th>
<th>Adresse IP/masque de sous-réseau</th>
<th>Passerelle par défaut</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replication</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replication</p></td>
<td><p>10.0.1.15</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


Dans la configuration suivante, il existe quatre sous-réseaux configurés dans le groupe de disponibilité de base de données : 192.168.0.0, 192.168.1.0, 10.0.0.0 et 10.0.1.0. Lorsque EX1 et EX2 sont ajoutés au DAG, quatre sous-réseaux sont énumérés et seulement deux réseaux DAG sont créés : MapiDagNetwork (192.168.0.0, 192.168.1.0) et ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0). Ces réseaux seront configurés comme indiqué dans le tableau suivant.

### Paramètres de réseau DAG énumérés pour un DAG de sous-réseaux multiples

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>Sous-réseaux</th>
<th>Interfaces</th>
<th>Accès MAPI activé</th>
<th>Réplication activée</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## Réseaux DAG et réseaux iSCSI

Par défaut, les DAG effectuent une recherche de tous les réseaux détectés et configurés pour utilisation par le cluster sous-jacent. Cela inclut tout réseau iSCSI (Internet SCSI) en cours d’utilisation du fait de l’utilisation du stockage iSCSI pour un ou plusieurs membres du DAG. Il est recommandé que le stockage iSCSI utilise des réseaux dédiés et des cartes réseau. Ces réseaux ne devraient pas être gérés ni par le DAG ni par son cluster ni utilisés comme réseaux de DAG (MAPI ou réplication). Leur utilisation par le DAG devrait au contraire être désactivée manuellement, de manière à ce qu’ils soient dédiés au trafic du stockage iSCSI. Pour que les réseaux iSCSI ne soient plus détectés et utilisés comme réseaux DAG, configurez le DAG pour qu’il ignore tous les réseaux iSCSI détectés à l’aide de la cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298008\(v=exchg.150\)), comme indiqué dans cet exemple :

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

Cette commande désactive également le réseau pour une utilisation par le cluster. Même si les réseaux iSCSI continuent à apparaître en tant que réseaux DAG, ils ne sont pas utilisés pour le trafic MAPI ou de réplication une fois la commande ci-dessus exécutée.

Retour au début

## Configuration des membres du groupe de disponibilité de base de données (DAG)

Les serveurs de boîtes aux lettres qui sont membres d’un DAG ont certaines propriétés spécifiques de haute disponibilité qui doivent être configurées comme indiqué dans les sections suivantes :

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## Numérotation de montage automatique de base de données

Le paramètre *AutoDatabaseMountDial* spécifie le comportement du montage automatique de base de données après basculement d’une base de données. Vous pouvez utiliser la cmdlet [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\)) pour configurer le paramètre *AutoDatabaseMountDial* avec l’une des valeurs suivantes :

  - `BestAvailability`   Si vous spécifiez cette valeur, la base de données monte automatiquement immédiatement après un basculement si la longueur de file d’attente de copie est inférieure ou égale à 12. La longueur de la file d’attente de copie correspond au nombre de journaux reconnu par la copie passive devant être répliquée. Si la longueur de la file d’attente de copie est supérieure à 12, la base de données n’est pas montée automatiquement. Si la longueur de la file d’attente de copie est inférieure ou égale à 12, Exchange tente de répliquer les journaux restants sur la copie passive et monte la base de données.

  - `GoodAvailability`   Si vous spécifiez cette valeur, la base de données est montée immédiatement après un basculement si la longueur de la file d’attente de copie est inférieure ou égale à six. La longueur de la file d’attente de copie correspond au nombre de journaux à répliquer reconnus par la copie passive. Si la longueur de la file d’attente de copie est supérieure à six, la base de données n’est pas montée automatiquement. Si la longueur de la file d’attente de copie est inférieure ou égale à six, Exchange tente de répliquer les journaux restants sur la copie passive et monte la base de données.

  - `Lossless`   Si vous spécifiez cette valeur, la base de données n’est pas montée automatiquement tant que tous les journaux générés sur la copie active n’ont pas été copiés sur la copie passive. Ce paramètre permet également à l’algorithme de sélection de la meilleure copie par le Gestionnaire Active Manager de trier les candidats éventuels pour l’activation en fonction de la valeur de préférence d’activation de la copie de la base de données et non sur sa longueur de file d’attente.

La valeur par défaut est `GoodAvailability`. Si vous spécifiez `BestAvailability` ou `GoodAvailability`, et si les données sur la copie active ne peuvent pas toutes être répliquées sur la copie passive, vous risquez de perdre des données de boîte aux lettres. Toutefois, la fonctionnalité Safety Net (activée par défaut) forme une protection contre la plupart des cas de perte de données en renvoyant les messages qui se trouvent dans la file d’attente de Safety Net.

## Exemple : configuration de la numérotation de montage automatique de base de données

L’exemple suivant configure un serveur de boîtes aux lettres avec un paramètre *AutoDatabaseMountDial* de `GoodAvailability`.

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## Stratégie d’activation automatique de copie de base de données

Le paramètre *DatabaseCopyAutoActivationPolicy* spécifie le type d’activation automatique disponible pour les copies de base de données de boîtes aux lettres sur les serveurs de boîtes aux lettres sélectionnés. Vous pouvez utiliser la cmdlet [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\)) pour configurer le paramètre avec l’une des valeurs suivantes *DatabaseCopyAutoActivationPolicy* :

  - `Blocked`   Si vous spécifiez cette valeur, les bases de données ne peuvent pas être automatiquement activées sur les serveurs de boîtes aux lettres sélectionnées.

  - `IntrasiteOnly`   Si vous spécifiez cette valeur, la copie de la base de données est autorisée sur les serveurs appartenant au même site Active Directory. Cela empêche le basculement intersite ou l’activation. Cette propriété s’applique aux copies des bases de données des boîtes de réception (par exemple, une copie passive devenant une copie active). Il est impossible d’activer des bases de données sur ce serveur de boîtes aux lettres pour des copies de bases de données qui sont actives dans un autre site Active Directory.

  - `Unrestricted`   Si vous spécifiez cette valeur, il n’existe aucune restriction spéciale pour l’activation de copies de bases de données de boîtes aux lettres sur les serveurs de boîtes aux lettres sélectionnés.

## Exemple : configuration de la stratégie d’activation automatique de copie de base de données

L’exemple suivant configure un serveur de boîtes aux lettres avec un paramètre *DatabaseCopyAutoActivationPolicy* de `Blocked`.

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## Nombre maximal de bases de données actives

Le paramètre *MaximumActiveDatabases* (également utilisé avec la cmdlet [Set-MailboxServer](https://technet.microsoft.com/fr-fr/library/aa998651\(v=exchg.150\))) spécifie le nombre de bases de données qui peuvent être montées sur un serveur de boîtes aux lettres. Vous pouvez configurer des serveurs de boîtes aux lettres pour qu’ils correspondent aux exigences de déploiement en vous assurant qu’un serveur de boîtes aux lettres individuel ne devient pas surchargé.

Le paramètre *MaximumActiveDatabases* est configuré avec une valeur numérique de nombre entier. Lorsque le nombre maximal est atteint, les copies de la base de données sur le serveur ne sont pas activées si un basculement se produit. Si les copies sont déjà actives sur un serveur, le montage des bases de données ne sera pas autorisé par le serveur.

## Exemple : configuration du nombre maximal de bases de données actives

L’exemple suivant configure un serveur de boîtes aux lettres pour prendre en charge un nombre maximal de 20 bases de données actives.

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

Retour au début

## Exécution de la maintenance sur les membres du groupe de disponibilité de base de données (DAG)

Avant d’effectuer tout type de maintenance matérielle ou logicielle sur un membre du DAG, vous devez d’abord mettre le membre du DAG en mode maintenance. Cela implique de déplacer toutes les bases de données actives hors du serveur et de bloquer leur déplacement vers le serveur. Cela garantit également que la fonctionnalité de prise en charge du DAG qui peut se trouver sur le serveur (par exemple, le rôle PAM (Primary Active Manager)) est transférée sur un autre serveur et qu’elle est bloquée afin qu’elle ne puisse pas revenir sur le serveur précédent. Plus précisément, vous devez effectuer les tâches suivantes :

1.  Pour lancer le processus de drainage des files d’attente de transport, exécutez `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`

2.  Pour lancer le drainage des files d’attente de transport, exécutez `Restart-Service MSExchangeTransport`

3.  Pour lancer le processus de drainage de tous les appels de messagerie unifiée, exécutez `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`

4.  Pour rediriger les messages en attente de remise dans les files d’attente locales vers le serveur de boîtes aux lettres spécifié par le paramètre Target, exécutez `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`

5.  Pour interrompre le nœud de cluster, ce qui l’empêche d’être et de devenir le PAM (Primary Active Manager), exécutez `Suspend-ClusterNode <ServerName>`

6.  Pour déplacer toutes les bases de données actives actuellement hébergées sur le membre du DAG vers d’autres membres du DAG, exécutez `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`

7.  Pour empêcher le serveur d’héberger des copies de base de données active, exécutez `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`

8.  Pour mettre le serveur en mode maintenance, exécutez `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`

Pour vérifier que le serveur est prêt pour la maintenance, effectuez les tâches suivantes :

1.  Pour vérifier que le serveur a été mis en mode maintenance, exécutez `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

2.  Pour vérifier que le serveur n’héberge aucune copie de base de données active, exécutez `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`

3.  Pour vérifier que le nœud est interrompu, exécutez `Get-ClusterNode <ServerName> | fl`

4.  Pour vérifier que toutes les files d’attente de transport ont été drainées, exécutez `Get-Queue`

Une fois que la maintenance a été effectuée et que le membre du DAG est prêt à fonctionner de nouveau, vous pouvez enlever le membre du DAG du mode maintenance et le remettre en production en effectuant les tâches suivantes :

  - Pour indiquer que le serveur n’est pas en mode maintenance, exécutez `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`

  - Pour autoriser le serveur à accepter des appels de messagerie unifiée, exécutez `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`

  - Pour reprendre le nœud dans le cluster et activer la fonctionnalité de cluster complet pour le serveur, exécutez `Resume-ClusterNode <ServerName>`

  - Pour permettre aux bases de données de devenir actives sur le serveur, exécutez `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`

  - Pour supprimer les blocs d’activation automatique, exécutez `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`

  - Pour activer les files d’attente de transport et autoriser le serveur à accepter et à traiter les messages, exécutez `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`

  - Pour reprendre l’activité de transport, exécutez `Restart-Service MSExchangeTransport`

Pour vérifier qu’un serveur est prêt pour la production, effectuez les tâches suivantes :

1.  Pour vérifier que le serveur n’est pas en mode maintenance, exécutez `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

Si vous installez une mise à jour Exchange et que l’opération échoue, certains composants de serveur peuvent rester dans un état inactif, ce qui sera affiché dans les résultats de la cmdlet Get-ServerComponentState ci-dessus. Pour résoudre ce problème, exécutez les commandes suivantes :

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

Retour au début

## Arrêt des membres du DAG

La solution de haute disponibilité Exchange 2013 est intégrée au processus d’arrêt de Windows. Si un administrateur ou une application arrête un serveur Windows dans le DAG qui a une base de données montée répliquée sur un ou plusieurs membres du DAG, le système tentera d’activer une autre copie de la base de données montée avant de terminer le processus d’arrêt.

Toutefois, ce nouveau comportement ne garantit pas que toutes les bases de données sur le serveur en cours de fermeture vont bénéficier d’une activation `lossless`. C’est pourquoi il est préférable d’effectuer un basculement de serveur avant d’arrêter un serveur membre d’un DAG.

Retour au début

## Installation de mises à jour sur les membres du DAG

L’installation de mises à jour Microsoft Exchange Server 2013 sur un serveur membre d’un groupe de disponibilité de base de données (DAG) est un processus relativement simple. Plusieurs services sont arrêtés lorsque vous installez une mise à jour sur un serveur membre d’un DAG, notamment tous les services Exchange et le service de cluster. La procédure générale d’application de mises à jour à un membre de DAG est la suivante :

1.  Suivez les étapes décrites ci-dessus pour mettre le membre du DAG en mode maintenance.

2.  Installez la mise à jour.

3.  Suivez les étapes décrites ci-dessus pour enlever le membre du DAG du mode maintenance et le remettre en production.

4.  Vous pouvez également utiliser le script RedistributeActiveDatabases.ps1 pour rééquilibrer les copies de base de données actives dans le DAG.

Vous pouvez télécharger la dernière mise à jour pour Exchange 2013 à partir du [Centre de téléchargement Microsoft](http://www.microsoft.com/downloads/).

Retour au début

