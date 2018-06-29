---
title: 'Routage des messages entre les sites Active Directory: Exchange 2013 Help'
TOCTitle: Routage des messages entre les sites Active Directory
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52062975
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Routage des messages entre les sites Active Directory

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Un site Active Directory est un composant de configuration logique basé sur les aspects physiques du réseau. La création d'un site Active Directory permet essentiellement de définir les sous-réseaux connectés de façon à optimiser le contrôle du trafic de réplication Active Directory. Microsoft Exchange Server 2013 reconnaît les groupes de disponibilité de base de données (DAG) et les sites Active Directory comme limites de routage, et les serveurs Exchange 2013 prennent des décisions en matière de routage d'après la topologie de site Active Directory.

Par défaut, une forêt Active Directory contient un seul site Active Directory. Le nom par défaut de ce site Active Directory est `Default-First-Site-Name`. Si aucun autre site Active Directory n'est créé, tous les ordinateurs membres du domaine dans la forêt sont membres de `Default-First-Site-Name`. Vous n'avez pas besoin de configurer d'association de sous-réseau au site. Si d'autres sites Active Directory sont créés, vous devez spécifier les sous-réseaux associés à ce site Active Directory.

**Contenu de la rubrique**

Identification de l'appartenance au site

Liens de sites IP

Contrôle des coûts des liens de sites IP

Implémentation de sites hub

Découverte de la topologie

## Identification de l'appartenance au site

Chaque site Active Directory est associé à un ou plusieurs sous-réseaux IP. Un administrateur attribue l'appartenance à un site Active Directory aux ordinateurs configurés en tant que contrôleurs de domaine et serveurs de catalogue global. L'appartenance au site Active Directory est octroyée automatiquement aux autres ordinateurs membres du domaine, tels que des serveurs Exchange, lorsque ceux-ci sont configurés pour utiliser une adresse IP se trouvant dans un sous-réseau IP associé à un site Active Directory. Les ordinateurs avec la même appartenance au site Active Directory sont supposés avoir une bonne connectivité réseau. Un serveur est toujours membre d'un site Active Directory unique.

Les applications sensibles au site peuvent déterminer l'appartenance au site Active Directory de l'ordinateur sur lequel elles sont installées ainsi que celle d'autres ordinateurs de la forêt, puis utiliser ces informations pour contrôler le flux de communication. Quand les applications sensibles au site doivent utiliser les services d'un autre serveur, tel qu'un contrôleur de domaine ou un serveur de catalogue global, la priorité est donnée aux serveurs qui ont la même appartenance au site Active Directory que celle de l'ordinateur demandant ces services.

Exchange 2013 est une application sensible au site et utilise la topologie Active Directory pour acheminer les messages et pour communiquer avec les services exécutés sur d'autres ordinateurs Exchange 2013. Le site Active Directory n'est pas seulement une limite de routage. Il s'agit également de la limite de détection du service.

L'identification de l'appartenance au site pour un ordinateur membre d'un domaine dépend d'une série de requêtes DNS visant à comparer l'adresse IP locale aux sous-réseaux définis, puis de déterminer l'association d'appartenance au site appropriée. Pour réduire la charge associée aux requêtes DNS, les ajouts au schéma Active Directory Exchange 2013 incluent l'attribut **msExchServerSite** pour l'objet serveur Exchange. La valeur de cet attribut constitue le nom unique du site Active Directory d'un serveur Exchange. Cet attribut est une propriété de chaque objet serveur Exchange. Lorsque l'affinité d'appartenance au site est stockée en tant qu'attribut de l'objet serveur, la topologie actuelle peut être lue directement à partir d'Active Directory plutôt que d'utiliser des requêtes DNS et une association d'appartenance au site est activée pour un ordinateur ne faisant pas partie du domaine, tel qu'un serveur de transport Edge abonné.

La valeur de l'attribut **msExchServerSite** est renseignée et mise à jour par le service de topologie Active Directory de Microsoft Exchange. Au démarrage d'un ordinateur Windows, le service Net Logon détermine l'appartenance au site pour l'ordinateur. Le service Net Logon utilise ces informations pour rechercher les contrôleurs de domaine se trouvant dans le même site Active Directory que l'ordinateur local, puis dirige les demandes d'autorisation et d'authentification vers ces serveurs. Le service de topologie Active Directory de Microsoft Exchange utilise l'appel d'API **DsGetSiteName** pour récupérer la valeur de l'appartenance au site à partir du service Net Logon et écrit le nom unique du site Active Directory sur l'attribut **msExchServerSite** pour l'objet serveur Exchange dans Active Directory.

Le tableau suivant montre la manière dont une organisation peut définir les sites Active Directory. Dans cet exemple, trois sites Active Directory sont définis et chaque site Active Directory est associé à plusieurs sous-réseaux IP.

**Exemple d'association de sous-réseau au site Active Directory**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du site Active Directory</th>
<th>Sous-réseaux IP associés</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>Site B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>Site C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


Si l'adresse IP d'un serveur nommé Mailbox01 est 192.168.1.1, le serveur est membre du site A. En modifiant l'adresse IP d'un serveur, vous modifiez son appartenance au site. Si vous modifiez l'adresse IP du serveur Mailbox01 en 192.168.2.1, cela ne modifie par l'appartenance au site Active Directory du serveur, car ce sous-réseau est également associé au site A. Toutefois, si vous déplacez le serveur et que l'adresse IP devient 192.168.3.1, le serveur sera considéré comme membre du site B.

La modification de l'appartenance au site peut également se produire si vous changez l'association de sous-réseaux sur des sites Active Directory. Par exemple, si vous supprimez le sous-réseau 192.168.3.0 de l'association avec le site B et que vous l'associez au site A, l'appartenance au site d'un serveur doté de l'adresse IP 192.168.3.1 est également modifiée avec le site A. À chaque modification de l'appartenance au site, Exchange doit mettre à jour ses données de configuration afin que la modification soit prise en compte lorsqu'Exchange prend les décisions de routage. Une latence survient au moment où une modification est apportée à une appartenance au site Active Directory et la modification de la topologie est entièrement répercutée.

Retour au début

## Liens de sites IP

Les liens de sites sont des chemins d'accès logiques entre des sites Active Directory. Un objet de lien de sites représente un ensemble de sites qui peuvent communiquer à un coût uniforme. Les liens de sites ne correspondent pas au chemin d'accès utilisé par les paquets réseau sur le réseau physique. Toutefois, le coût affecté au lien de sites par l'administrateur se base généralement sur la fiabilité, la vitesse et la bande passante disponible du réseau sous-jacent. Par exemple, l'administrateur Active Directory affecte un coût inférieur à une connexion réseau dont la vitesse est 100 Mbits/s qu'à une connexion réseau dont la vitesse est 10 Mbits/s.

Par défaut, tous les liens de sites sont transitifs. En d'autres termes, si le site A est lié au site B et que le site B est lié au site C, le site A est lié de manière transitive au site C. La liaison transitive entre le site A et le site C est également appelée *pont lien de sites*

Exchange utilise uniquement des liens de sites IP pour déterminer sa topologie de routage du site Active Directory. Lors du calcul d'une table de routage, le composant de routage d'Exchange tient compte du coût affecté au lien de sites IP. Ces coûts entrent dans le calcul du chemin de routage le moins coûteux vers la destination finale d'un message.

Chaque site Active Directory doit être associé à un lien de sites IP au minimum. Il existe un lien de sites IP unique par défaut intitulé `DEFAULTIPSITELINK`. Quand vous créez un site Active Directory, vous devez l'associer à un lien de sites IP. Vous pouvez créer des liens de sites IP supplémentaires pour implémenter la topologie souhaitée ou associer chaque site Active Directory à la liaison `DEFAULTIPSITELINK`. Chaque site Active Directory faisant partie d'un lien de sites IP peut communiquer directement avec les autres sites de ce lien à un coût uniforme.

Dans la figure suivante, quatre sites Active Directory sont configurés dans la forêt. Chaque site a été associé à la liaison `DEFAULTIPSITELINK`. Par conséquent, chaque site Active Directory communique directement avec tous les autres sites en utilisant la même mesure de coût. Plusieurs chemins d'accès de communication sont indiqués, mais un seul lien de sites IP est défini.

**Topologie à maille pleine avec un lien de sites IP unique**

![Topologie à maille pleine avec un lien de sites IP unique](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "Topologie à maille pleine avec un lien de sites IP unique")

Dans la figure suivante, quatre sites Active Directory sont configurés dans la forêt. Dans cette topologie, l'administrateur a configuré les liens de sites IP de manière a créer une *topologie « hub-and-spoke »* de sites Active Directory. Chaque site spoke peut communiquer directement avec le site central. Les sites Spoke peuvent communiquer entre eux via les liens de sites IP transitifs.

**Topologie « hub-and-spoke » de liens de sites IP Active Directory**

![Topologie « Hub and Spoke » des liens de sites IP](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "Topologie « Hub and Spoke » des liens de sites IP")

Il est important de noter qu'Exchange utilise des liens de sites pour identifier le chemin le moins coûteux et essaie toujours de remettre les messages directement au serveur Exchange de destination. Par exemple, si un utilisateur du site B dans la topologie présentée dans la figure précédente envoie un message à un autre utilisateur du site C, le serveur de boîtes aux lettres du site B se connectera directement au serveur de boîtes aux lettres du site C. Si vous voulez obliger les messages à transiter par le site A, celui-ci doit être activé comme site hub. Pour plus d'informations sur les sites hub, consultez la section « Implémentation de sites hub » plus loin dans cette rubrique.

Un administrateur Active Directory met en œuvre la topologie qui représente le mieux les exigences de connectivité et de communication de la forêt. Comme la même topologie est utilisée par Exchange, vous devez vérifier que la topologie actuelle prend en charge une communication de messagerie efficace.

Le coût par défaut pour un lien de sites est 100. Un coût de lien de sites valide est un chiffre compris entre 1 et 99 999. Si vous spécifiez des liens redondants, le lien présentant l'affectation de coût la plus faible est toujours préféré. Un administrateur d'organisation Exchange peut affecter un coût spécifique d'Exchange à un lien de sites IP. Si un coût Exchange est affecté à un lien de sites IP, ce dernier sera utilisé par Exchange. Autrement, le coût Active Directory est utilisé. Pour plus d'informations sur la définition d'un coût Exchange sur un lien de sites IP, consultez la section « Contrôle des coûts des liens de sites IP » plus loin dans cette rubrique. Un administrateur doté de l'appartenance au groupe Administrateurs de l'entreprise peut créer d'autres liens de sites IP.

Pour plus d'informations sur la configuration du site Active Directory, consultez la rubrique [Conception de la topologie de site](https://go.microsoft.com/fwlink/p/?linkid=33551).

Retour au début

## Contrôle des coûts des liens de sites IP

Les coûts des liens de sites IP Active Directory sont basés sur la vitesse relative du réseau comparée à toutes les connexions réseau du réseau étendu WAN et sont conçues pour produire une topologie de réplication fiable et efficace. Par conséquent, dans la plupart des cas, les coûts du lien de sites IP existant doivent fonctionner correctement pour le routage des messages Exchange. Cependant, si après avoir documenté le site Active Directory et la topologie de lien de sites IP existants, vous constatez que les coûts propres aux liens de sites IP et les schémas de flux de trafic Active Directory ne sont pas optimaux pour Exchange, vous pouvez apporter des ajustements aux coûts évalués par Exchange. La modification du coût affecté au lien de sites IP à l'aide des outils Active Directory aurait un impact sur l'ensemble de l'environnement. Utilisez plutôt la cmdlet **Set-AdSiteLink** de l'environnement de ligne de commande Exchange Management Shell pour affecter un coût spécifique à Exchange à un lien de sites IP. Par exemple, pour configurer la valeur de coût 25 spécifique d'Exchange sur le lien de sites IP SITELINKAB, exécutez la commande suivante dans l'environnement de ligne de commande Exchange Management Shell. `Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

Quand un coût spécifique d'Exchange est affecté à un lien de sites IP, celui-ci remplace le coût Active Directory à des fins de routage des messages. Par ailleurs, le routage ne tient compte du coût Exchange que lorsqu'il détermine le chemin de routage le moins coûteux.

L'ajustement des coûts de lien de sites IP peut être utile lorsque la topologie de routage des messages doit être différente de la topologie de réplication Active Directory. Les coûts Exchange peuvent être utilisés pour forcer tous les itinéraires de messages à utiliser un site hub. Les coûts Exchange permettent également de contrôler l'emplacement de mise en file d'attente des messages lorsque la communication vers un site Active Directory échoue. La figure suivante illustre une topologie Active Directory à quatre sites.

**Topologie avec les coûts Exchange configurés sur des liens de sites IP**

![Topologie avec les coûts Exchange sur les liens de sites IP](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "Topologie avec les coûts Exchange sur les liens de sites IP")

Dans la figure précédente, la connexion réseau entre le site C et le site D est une connexion à bande passante faible utilisée uniquement pour la réplication Active Directory et ne doit par conséquent pas être utilisée à des fins de routage des messages. Toutefois, les coûts des liens de sites IP Active Directory entraînent l'inclusion de cette liaison dans le chemin de routage le moins coûteux à partir de tout autre site Active Directory vers le site D. Par conséquent, les messages sont remis à la file d'attente du site D dans le site C. L'administrateur Exchange préfère que le chemin de routage le moins coûteux inclue le site B de sorte que si le site D est inaccessible, les messages sont placés en file d'attente sur le site B. La configuration d'un coût Exchange élevé sur le lien de sites IP entre le site C et le site D empêche ce lien de sites IP d'être inclus dans le chemin de routage le moins coûteux vers le site D.

Exchange prend en charge la configuration d'une limite de taille de message maximale sur un lien de sites IP Active Directory. Par défaut, Exchange n'impose pas de limite de taille de message maximale pour les messages relayés entre des serveurs Exchange dans différents sites Active Directory. Si vous utilisez la cmdlet **Set-AdSiteLink** pour configurer une taille de message maximale sur un lien de sites IP Active Directory, le routage génère une notification d'échec de remise pour tout message dont la taille est supérieure à la taille de message maximale configurée sur tout lien de sites Active Directory dans le chemin de routage le moins coûteux. Cette configuration est utile pour restreindre la taille des messages envoyés à des sites Active Directory distants qui doivent communiquer via des connexions à bande passante faible. Pour plus d'informations, consultez la rubrique [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

Retour au début

## Implémentation de sites hub

Dans votre organisation Exchange, vous souhaitez peut-être que la remise de tous les messages s'effectue via un site Active Directory en particulier. Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour désigner un site Active Directory en tant que site hub. Lors de cette opération, vous entraînez une surcharge générale supplémentaire, car plus de serveurs sont impliqués dans la remise des messages. Par exemple, un message est envoyé du site A au site E. Si le chemin de routage le moins coûteux est Site A-Site B-Site C-Site D-Site E et que vous désignez le site C comme site hub, le message est relayé du site A au site C, puis du site C au site E.

La cmdlet **Set-AdSite** vous permet de spécifier un site Active Directory comme site hub. Lorsqu'un site hub est présent sur le chemin de routage le moins coûteux pour la remise des messages, les messages sont placés en file d'attente et traités par le service de transport sur des serveurs de boîtes aux lettres dans le site hub avant d'être relayés vers leur destination finale.

Après avoir choisi le chemin de routage le moins coûteux, le routage détermine s'il existe un site hub dans le chemin parcouru. Si un site hub est configuré, les messages s'arrêtent sur un serveur de boîtes aux lettres dans le site hub avant d'être relayés vers leur destination finale. S'il existe plusieurs sites hub sur le chemin de routage le moins coûteux, les messages s'arrêtent à chaque site hub jalonnant le chemin de routage.

Cette variante au routage de relais direct uniquement prend effet lorsque le site hub est situé sur le chemin de routage le moins coûteux. La figure suivante illustre l'utilisation correcte d'un site hub. Dans ce schéma, le site B est configuré comme site hub. Les messages relayés du site A au site D sont relayés via le site B avant d'être remis au site D.

**Remise de messages avec un site hub**

![Remise de messages avec un site concentrateur](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "Remise de messages avec un site concentrateur")

La figure suivante illustre la mesure dans laquelle les coûts du lien de sites IP affectent le routage vers un site hub. Dans ce scénario, le site B est désigné comme site hub. Toutefois, le site B n'existe pas sur le chemin de routage le moins coûteux entre les autres sites. Par conséquent, les messages relayés du site A au site D ne sont jamais relayés via le site B. Aucun site Active Directory n'est utilisé comme site hub s'il ne se trouve pas sur le chemin de routage le moins coûteux entre deux autres sites.

**Site hub mal configuré**

![Site concentrateur mal configuré](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "Site concentrateur mal configuré")

Vous pouvez configurer un site Active Directory comme site hub. Cependant, pour que cette configuration fonctionne correctement, vous devez disposer d'au moins un serveur de boîtes aux lettres dans le site hub.

Retour au début

## Découverte de la topologie

Exchange peut accéder à la topologie Active Directory via les éléments obligatoires suivants :

  - Service de topologie Active Directory de Microsoft Exchange

  - Module de découverte de topologie au sein du service de transport Microsoft Exchange

Le service de topologie Active Directory de Microsoft Exchange est exécuté sur tous les serveurs d'accès au client Exchange 2013 et sur tous les serveurs de boîtes aux lettres. Ces serveurs utilisent le service de topologie Active Directory de Microsoft Exchange pour découvrir les contrôleurs de domaine et les serveurs de catalogue global qui peuvent être utilisés par les serveurs Exchange de manière à lire et écrire des données Active Directory. Exchange 2013 est lié aux serveurs d'annuaire identifiés quand Exchange doit lire à partir d'Active Directory ou écrire vers Active Directory.

Le module de découverte de topologie est inclus dans le service de transport Microsoft Exchange et fournit des informations concernant la topologie Active Directory aux serveurs Exchange. Cette API détecte les serveurs et rôles Exchange dans l'organisation et identifie leur relation avec les objets de configuration Active Directory. Les données de configuration sont extraites d'Active Directory, puis elles sont mises en cache de sorte que les services Exchange en cours d'exécution sur l'ordinateur puissent y accéder.

Le module de découverte de topologie procède comme suit pour générer une topologie de routage Exchange :

1.  Les données sont lues à partir d'Active Directory. Tous les objets suivants sont récupérés :
    
      - Sites Active Directory
    
      - Liens de sites IP
    
      - Tous les serveurs Exchange

2.  Les données récupérées lors de l'étape 1 sont utilisées pour créer la topologie initiale et démarrer la liaison et le mappage des objets de configuration concernés.

3.  Les serveurs Exchange sont mis en correspondance avec des sites Active Directory en récupérant la valeur d'attribut de site à partir de l'objet serveur Exchange stocké dans Active Directory.

4.  Les tables de routage sont mises à jour avec l'ensemble des informations récupérées.

Ce processus permet de révéler l'existence de chaque serveur Exchange 2013 aux autres serveurs Exchange dans l'organisation ainsi que le degré de proximité entre tous les serveurs Exchange.

Retour au début

