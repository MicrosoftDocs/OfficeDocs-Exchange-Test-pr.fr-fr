---
title: 'Modifications de l’architecture vocale: Exchange 2013 Help'
TOCTitle: Modifications de l’architecture vocale
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50478223
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifications de l’architecture vocale

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

L'architecture Microsoft Exchange Server 2013 est différente de l'architecture dans Exchange Server 2007 et Exchange Server 2010. Dans Exchange 2007 et Exchange 2010, les types de serveurs étaient séparés en plusieurs rôles de serveurs : Accès client, boîte aux lettres, transport Hub et messagerie unifiée. Dans Exchange 2013, les rôles de serveurs sont combinés en deux types de serveurs et tous les composants ou services issus de ces rôles serveurs sont exécutés sur le même serveur physique ou sur deux serveurs nommés d'accès au client et de boîtes aux lettres. Dans le nouveau modèle, le serveur d'accès au client qui exécute le service routeur des appels de messagerie unifiée Microsoft Exchange redirige le trafic SIP généré depuis un appel entrant vers un serveur de boîtes aux lettres. Puis, un canal de support RTP (Realtime Transport Protocol) ou secure RTP (SRTP)) est établi depuis la passerelle VoIP ou PBX (Private Branch eXchange) IP vers le serveur de boîte aux lettres qui héberge la boîte aux lettres utilisateur. Dans Exchange 2013, le serveur de boîtes aux lettres a les mêmes processus que le rôle serveur de messagerie unifiée dans Exchange 2007 et Exchange 2010. Le serveur de boîtes aux lettres exécute à la fois le service de messagerie unifiée Microsoft Exchange et les processus de travail de messagerie unifiée. Le serveur d'accès au client exécute le service routeur des appels de messagerie unifiée Microsoft Exchange, qui reçoit un appel entrant et le transmet au serveur de boîtes aux lettres.

**Contenu de cette rubrique**

Support pour la nouvelle architecture d’Exchange

Ports de messagerie unifiée

Plans de numérotation de messagerie unifiée

Compteurs de performance pour le routeur des appels de messagerie unifiée

## Support pour la nouvelle architecture d’Exchange

Dans Exchange 2013, le serveur d'accès au client est responsable de la découverte automatique, du chiffrement SSL (Secure Sockets Layer), de l'authentification, de la redirection et du proxy. Le serveur d'accès au client est le point d'entrée de tout appel sortant ou demande SIP pour la messagerie unifiée. La logique de routage et SIP REDIRECT est mis en œuvre comme un service automatiquement inclus dans un serveur d'accès au client. Ce service est connu sous le nom de service de routeur des appels de messagerie unifiée Microsoft Exchange. Il est installé et s'exécute sur chaque serveur d'accès au Client dans votre organisation. Lorsqu'un serveur d'accès au client reçoit une IP INVITE pour un appel entrant, le service routeur des appels de messagerie unifiée Microsoft Exchange redirige l'appel entrant vers le serveur de boîtes aux lettres. Puis, un canal de support (RTP ou SRTP) est créé entre la passerelle VoIP, PBX IP ou le contrôleur de frontière de session (SBC) et le serveur de boîtes aux lettres. Bien que le serveur d'accès au client agisse comme un redirecteur SIP, il ne prend en charge que les demandes SIP des passerelles VoIP, des PBX IP ou des SBC. Il ne reçoit pas le trafic de n'importe quel support. le trafic de support qui utilise RTP ou SRTP est uniquement transmis entre le serveur de boîtes aux lettres et les homologues SIP tels que les passerelles VoIP, les PBX IP ou les SBC et non vers le serveur d'accès au client. Lorsque vous déployez Exchange 2013 et la messagerie unifiée, vous devez configurer vos passerelles VoIP, PBX IP ou SBC pour qu'ils pointent vers les serveurs d'accès au client installés, de sorte que les appels entrants soient acheminés correctement pour la messagerie unifiée.

Dans certains cas, le déploiement de plusieurs serveurs d'accès au client est obligatoire, et les serveurs d'accès au client sont déployés séparément sur différents matériels physiques depuis les serveurs de boîtes aux lettres. Les serveurs d'accès au client peuvent être groupés dans un tableau au moyen d'un matériel L4 ou L5 ou d'un équilibreur de chargement logiciel. Toutefois, il n'existe pas de tableau de serveurs d'accès au client basée sur les objets Active Directory Exchange. Il est possible d'utiliser un équilibreur de chargement matériel ou logiciel en face de serveurs d'accès au client dans des déploiements Exchange plus importants.

Lorsqu'un serveur d'accès au client est installé, le service routeur des appels de la messagerie unifiée Microsoft Exchange est en cours d'exécution. Le service effectue ce qui suit :

  - Une fois initialisé, il lit un fichier de configuration local nommé msexchangeumcallrouter.config.

  - Exécute une génération de grammaires vocales à l'aide de la boîte aux lettres d'arbitrage pour une organisation.

  - Prend en charge les connexions TCP (Transmission Control Protocol) et/ou TLS (Transport Layer Security). Ce paramètre est configurable.

  - Ne s'arrête qu'en cas d'erreur de configuration ou si les ports requis ne peuvent pas être enregistrés.

Dans Exchange 2013, le serveur de boîtes aux lettres n'est pas chargé de répondre aux demandes SIP des appels entrants. Il n'est responsable que de la réception du trafic SIP d'un serveur d'accès au client et établit alors une connexion RTP ou SRTP vers la passerelle VoIP, le PBX IP ou le SBC.

Une fois qu'un serveur d'accès au client a redirigé un appel entrant vers un serveur de boîtes aux lettres, un canal de support est établi entre la passerelle VoIP, le PBX IP ou le SBC et le serveur de boîtes aux lettres. Une fois le canal de support établi, le service de messagerie unifiée Microsoft Exchange sur le serveur de boîte aux lettres lit le message d'accueil de la messagerie vocale de l'utilisateur, traite les règles de réponse aux appels de l'utilisateur et invite l'appelant à laisser un message vocal. Le serveur de boîtes aux lettres enregistre alors le message vocal, crée une transcription du message et le dépose dans la boîte aux lettres de l'utilisateur. néanmoins, si vous intégrez Exchange à Office Communications Server 2007 R2 ou Lync Server, les canaux de support SIP et RTP ou SRTP pour les appels entrants sont pris en charge par les serveurs Lync et le serveur de boîtes aux lettres. Dans un environnement Lync intégré, vous ne disposez pas de passerelles VoIP, de PBX IP ni de SBC. Pour Lync, le serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange est identique à un serveur de messagerie unifiée Exchange 2010. Le serveur de boîtes aux lettres et le serveur d'accès au client qui exécutent le service routeur des appels de messagerie unifiée Microsoft Exchange sont considérés comme des homologues approuvés car les deux serveurs doivent être ajoutés à un plan de numérotation SIP. Lync achemine l'appel entrant au moyen du composant Routage des entrées qui utilise SIP pour communiquer avec le serveur d'accès au client, puis achemine l'appel vers un serveur de boîtes aux lettres.

Les administrateurs de messagerie unifiée Exchange 2010 peuvent configurer un jeu de propriétés pour la messagerie unifiée sur chaque serveur de messagerie unifiée. Dans Exchange 2013, les composants de messagerie unifiée et les paramètres de configuration pour la messagerie unifiée se trouvent sur les serveurs d'accès au client et de boîtes aux lettres. Tous les paramètres de messagerie unifiée appliqués à un seul ordinateur exécutant le rôle de serveur de messagerie unifiée dans Exchange 2010 sont encore disponibles. Cependant, certaines de ces propriétés et paramètres de configuration sont définis sur un serveur d'accès au client exécutant le service routeur des appels de messagerie unifiée Microsoft Exchange, et d'autres sont disponibles sur un serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange. Dans certains cas, le même paramètre est disponible pour les deux. La liste suivante contient les cmdlets et les paramètres qui sont disponibles sur les serveurs d’accès au client et les serveurs de boîtes aux lettres, et chaque fois que des modifications ont été apportées à une cmdlet pour prendre en charge des scénarios de déploiement avec des versions précédentes de la messagerie unifiée.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Disponible sur les serveurs de boîtes aux lettres Exchange 2013. Fonctionne également sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Disponible sur les serveurs d’accès au client Exchange 2013, mais non disponible sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Disponible sur les serveurs de boîtes aux lettres Exchange 2013. Fonctionne également sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Non disponible sur les serveurs d’accès au client Exchange 2013 et sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    Non disponible sur les serveurs de boîtes aux lettres Exchange 2013, mais fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   Ne peut pas être configuré sur les serveurs de boîtes aux lettres Exchange 2013, mais fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**    Disponible sur les serveurs d’accès au client Exchange 2013, mais ne fonctionne pas sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   Disponible sur les serveurs d’accès au client Exchange 2013, mais ne fonctionne pas sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   Non disponible sur les serveurs de boîtes aux lettres Exchange 2013, mais fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**    Non disponible sur les serveurs d’accès au client Exchange 2013, mais ne fonctionne pas sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   Disponible sur les serveurs de boîtes aux lettres Exchange 2013 et fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**    Disponible sur les serveurs d’accès au client Exchange 2013, mais ne fonctionne pas sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Enable-UMService**    Non disponible sur les serveurs de boîtes aux lettres Exchange 2013, mais fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

  - **Disable-UMService**    Non disponible sur les serveurs de boîtes aux lettres Exchange 2013, mais fonctionne sur les serveurs de messagerie unifiée Exchange 2007 et Exchange 2010.

Pour le serveur de boîtes aux lettres, vous devrez utiliser les cmdlets **Set/Get/Enable/Disable-UMService** pour afficher ou configurer les propriétés de messagerie unifiée pour le service de messagerie unifiée Microsoft Exchange sur les serveurs de boîtes aux lettres Exchange 2013 ou les serveurs de messagerie unifiée Exchange 2007 ou Exchange 2010. Un jeu de cmdlets différent, **Set/Get-UMCallRouterSettings**, est utilisé pour afficher ou configurer les propriétés du service routeur des appels de la messagerie unifiée Microsoft Exchange sur un serveur d'accès au client. Ceci garantit que les cmdlets **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** et **Disable-UMServer** de Exchange 2007 et Exchange 2010 fonctionnent dans un déploiement de coexistence avec les serveurs de boîtes aux lettres Exchange 2013. Cela garantit également que les cmdlets fonctionnent lorsque les serveurs de boîtes aux lettres et d'accès au client sont installés sur le même serveur ou des serveurs différents.

Support pour la nouvelle architecture d’Exchange

## Ports de messagerie unifiée

Le service routeur des appels de la messagerie unifiée Microsoft Exchange qui se trouve sur un serveur d'accès client utilise SIP sur le protocole TCP (Transmission Control Protocol) ou le protocole mutuel TLS (Transport Layer Security) pour communiquer avec les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange. Afin d'éviter tout conflit de port TCP/UDP (User Datagram Protocol), le service routeur des appels de messagerie unifiée Microsoft Exchange et le service de messagerie unifiée Microsoft Exchange sélectionnent et écoutent différents ports TCP par défaut. Ils peuvent accepter à la fois des connexions sécurisées et non sécurisées, en fonction de l'utilisation du protocole mutuel TLS avec le trafic SIP ou RTP. Par défaut, un serveur d'accès au client écoute les demandes SIP sur le port 5060 TCP en mode non sécurisé et le port 5061 TCP en mode SIP sécurisé lorsque le protocole mutuel TLS est utilisé. Ces ports sont configurables au moyen de la cmdlet **Set-UMCallRouterSettings**. Le service routeur des appels de la messagerie unifiée Microsoft Exchange sur le serveur d'accès au client ne prend pas en charge le trafic de support (RTP ou SRTP). Ainsi, seuls les ports TCP et non les ports UDP sont utilisés. Par défaut, un serveur de boîtes aux lettres écoute les demandes SIP sur le port 5062 TCP en mode non sécurisé et le port 5063 TCP en mode SIP sécurisé lorsque le protocole mutuel TLS est utilisé. Ces ports ne sont pas configurables à l'aide des cmdlets Exchange Management Shell. Dans le serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange, les ports TCP ne peuvent pas être configurés sur le serveur Exchange soit en utilisant le Shell soit en configurant les paramètres dans le registre. Le service de messagerie unifiée Microsoft Exchange sur le serveur de boîtes aux lettres acceptera les connexions d'un serveur d'accès au client sur les ports 5062 et 5063 SIP. Une fois que le serveur d'accès au client a redirigé la demande SIP vers un serveur de boîtes aux lettres, un canal de support RTP ou SRTP est créé à l'aide d'une passerelle VoIP, d'un PBX IP ou d'un SBC, et la messagerie unifiée Microsoft Exchange fonctionne sur le serveur de boîtes aux lettres.

Le tableau suivant résume les ports et protocoles de Exchange 2013 et indique si les ports peuvent être modifiés.

### Ports d'écoute de messagerie unifiée

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocole</th>
<th>Port TCP</th>
<th>Port UDP</th>
<th>Est-il possible de modifier des ports ?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (serveur d'accès au Client – service routeur des appels de messagerie unifiée Microsoft Exchange)</p></td>
<td><p>5060 (non sécurisé), 5061 (sécurisé). Le service écoute sur les deux ports.</p></td>
<td><p>Non applicable</p></td>
<td><p>Oui, à l’aide de la cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (serveur de boîtes aux lettres – service de messagerie unifiée Microsoft Exchange)</p></td>
<td><p>5062 (non sécurisé), 5063 (sécurisé). Le service écoute sur les deux ports.</p></td>
<td><p>Non applicable</p></td>
<td><p>Les ports ne peuvent pas être modifiés.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (Serveur de boîtes aux lettres - processus de travail de messagerie unifiée)</p></td>
<td><p>5065 et 5067 pour TCP (non sécurisé). 5066 et 5068 pour une authentification TLS mutuelle (sécurisé). C'est le cas lors lorsque <em>UMStartupMode</em> est défini sur <em>Dual</em>. Si <em>UMStartUpMode</em> est défini sur <em>TCP</em> ou <em>TLS</em>, les ports 5065 et 5066 sont utilisés. La valeur par défaut de <em>UMStartupMode</em> est <em>TCP</em>.</p></td>
<td><p>Non applicable</p></td>
<td><p>Les ports ne peuvent pas être modifiés.</p></td>
</tr>
<tr class="even">
<td><p>RTP (serveur de boîtes aux lettres - processus de travail de messagerie unifiée)</p></td>
<td><p>Non applicable</p></td>
<td><p>Ports entre 1024 et 65535.</p></td>
<td><p>La plage de ports peut être modifiée via le registre (toutefois, ceci n'est pas une configuration prise en charge) :</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


Support pour la nouvelle architecture d’Exchange

## Plans de numérotation de messagerie unifiée

Le mappage ou l'association des plans de numérotation de messagerie unifiée n'est pas requis dans Exchange 2013 comme dans Exchange 2007 et Exchange 2010. Les serveurs d'accès au client ou de boîtes aux lettres exécutant les services de messagerie unifiée n'ont pas besoin d'être reliés à un plan de numérotation de messagerie unifiée car tous les serveurs d'accès au client et de boîtes aux lettres doivent recevoir tous les messages entrants des passerelles VoIP, PBX IP et SBC. L'exception est que les plans de numérotation SIP utilisés avec Lync 2013, Lync Server 2010 et Office Communications Server 2007 R2 doivent être associés aux serveurs d'accès au client et de boîtes aux lettres déployés. Les deux types de serveurs Exchange doivent être ajoutés à chaque plan de numérotation SIP pour être inclus comme des homologues approuvés depuis Communications Server 2007 R2 ou Lync Server. Sinon, Communications Server 2007 R2 ou Lync Server refuseront les appels sortants provenant des utilisateurs.

Le tableau suivant résume la relation entre les serveurs d'accès au client et de boîtes aux lettres et les plans de numérotation de messagerie unifiée.

### Relier les plan de numérotation de messagerie unifiée

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologie</th>
<th>Plan de numérotation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accès au client et boîtes aux lettres sur le même serveur (sans les plans de numérotation non SIP Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Il n'est plus obligatoire d'associer les plans de numérotation au serveur d'accès au client ou de boîtes aux lettres. Vous n'êtes pas autorisé à ajouter les serveurs d'accès au client ou de boîtes aux lettres à un plan de numérotation. Si vous exécutez la cmdlet <strong>Set-UMService</strong>, elle génèrera une erreur si vous essayez d’associer un serveur de boîtes aux lettres à un plan de numérotation non SIP.</p></td>
</tr>
<tr class="even">
<td><p>Accès au client et boîtes aux lettres sur des serveurs différents (sans les plans de numérotation non SIP Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Il n'est plus obligatoire d'associer les plans de numérotation aux serveurs d'accès au client ou de boîtes aux lettres. Vous n'êtes pas autorisé à ajouter des serveurs d'accès au client ou de boîtes aux lettres à un plan de numérotation. Si vous exécutez la cmdlet <strong>Set-UMService</strong>, elle génèrera une erreur si vous essayez d’associer un serveur de boîtes aux lettres à un plan de numérotation non SIP.</p></td>
</tr>
<tr class="odd">
<td><p>Serveur d'accès au client et de boîtes aux lettres sur le même serveur physique (avec les plans de numérotation SIP Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Dans le cas d’un plan de numérotation SIP unique, ajoutez tous les serveurs d’accès au client et de boîtes aux lettres au plan de numérotation SIP. Dans le cas de plans de numérotation SIP multiples, ajoutez tous les serveurs d’accès au client et de boîtes aux lettres à chaque plan de numérotation SIP. Les deux serveurs deviendront alors des homologues approuvés d’Office Communications Server 2007 R2 ou de Lync Server. Vous devez utiliser le même certificat dans votre déploiement Office Communications Server 2007 R2 ou Lync Server, comme vous le faites sur chaque serveur d'accès au client et de boîtes aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Serveur d'accès au client et de boîtes aux lettres sur des serveurs physiques différents (avec les plans de numérotation SIP Communications Server 2007 R2 ou Lync Server 2010)</p></td>
<td><p>Dans le cas d’un plan de numérotation SIP unique, ajoutez tous les serveurs d’accès au client et de boîtes aux lettres au plan de numérotation SIP. Dans le cas de plans de numérotation SIP multiples, ajoutez tous les serveurs d’accès au client et de boîtes aux lettres à chaque plan de numérotation SIP. Les deux serveurs deviendront alors des homologues approuvés d’Office Communications Server 2007 R2 ou de Lync Server. Si les certificats utilisés sur les serveurs d'accès au client et de boîtes aux lettres sont différents, vous devez utiliser le même certificat dans votre déploiement Office Communications Server 2007 R2 ou Lync Server comme vous le faites sur chaque serveur d'accès au client ou de boîtes aux lettres dans votre organisation.</p></td>
</tr>
</tbody>
</table>


Support pour la nouvelle architecture d’Exchange

## Compteurs de performance pour le routeur des appels de messagerie unifiée

Les précédentes versions d'Exchange contenaient le rôle serveur de messagerie unifiée, qui exécutait le service de messagerie unifiée Microsoft Exchange. Dû à un changement de l'architecture dans Exchange 2013, le serveur d’accès au client exécute le service routeur des appels de messagerie unifiée Microsoft Exchange et le serveur de boîtes aux lettres exécute le service de messagerie unifiée Microsoft Exchange. Les mêmes compteurs de performances pour le service de messagerie unifiée Microsoft Exchange sont disponibles pour les administrateurs comme dans les versions précédentes de la messagerie unifiée Exchange. Cependant, vous pouvez utiliser des compteurs de performances supplémentaires sur le serveur d’accès au client pour vérifier l’état du service routeur des appels de messagerie unifiée Microsoft Exchange et résoudre des problèmes.

Pour prendre en charge le service routeur des appels de messagerie unifiée dans Exchange 2013, les compteurs de performances suivants ne sont pas disponibles.

### Compteurs de performances

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Catégorie de compteurs de performances</th>
<th>Nom du compteur</th>
<th>Description</th>
<th>Seuil</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Pourcentage des appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange au cours de la dernière heure</p></td>
<td><p>Ce compteur indique le pourcentage d’appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange au cours de la dernière heure.</p></td>
<td><p>Ce pourcentage doit toujours être inférieur à 5 %, mais peut être à 0 à tout moment.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Appels déconnectés sur une erreur interne irrécupérable pour le service routeur des appels de messagerie unifiée Microsoft Exchange</p></td>
<td><p>Ce compteur indique le nombre d’appels déconnectés suite à une erreur système interne.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total des appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange</p></td>
<td><p>Ce compteur indique le nombre total d’appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange depuis le démarrage du service.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Nombre total des appels reçus par le service routeur des appels de messagerie unifiée Microsoft Exchange</p></td>
<td><p>Ce compteur indique le nombre total d’appels entrants reçus par le service routeur des appels de messagerie unifiée Microsoft Exchange depuis le démarrage du service.</p></td>
<td><p>Doit être égal ou supérieur à 0.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Pourcentage des appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange au cours de la dernière heure</p></td>
<td><p>Ce compteur indique le pourcentage d’appels entrants refusés par le service routeur des appels de messagerie unifiée Microsoft Exchange au cours de la dernière heure.</p></td>
<td><p>La valeur doit être inférieure à 5 %.</p></td>
</tr>
</tbody>
</table>


Support pour la nouvelle architecture d’Exchange

