---
title: 'Compteurs de performance Exchange 2013: Exchange 2013 Help'
TOCTitle: Compteurs de performance Exchange 2013
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63913013
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Compteurs de performance Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-02-06_

## Compteurs de performance Exchange 2013

Les sections suivantes répertorient les compteurs de performance que vous pouvez utiliser lors de la résolution de problèmes de performances Exchange 2013.

## Compteurs de connectivité de contrôleur de domaine Exchange

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs de connectivité de contrôleur de domaine Exchange.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Compteur</th>
<th>Description</th>
<th>Seuil</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contrôleurs de domaine MSExchange ADAccess(*)\Durée de lecture LDAP</p></td>
<td><p>Indique le temps en millisecondes (ms) pour envoyer une demande de lecture LDAP au contrôleur de domaine spécifié et recevoir une réponse.</p></td>
<td><p>Cette valeur doit être de 50 ms en moyenne. Les pics (valeurs maximales) ne doivent pas être supérieurs à 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Contrôleurs de domaine MSExchange ADAccess(*)\Durée de recherche LDAP</p></td>
<td><p>Indique la durée (en ms) pour envoyer une demande de recherche LDAP et recevoir une réponse.</p></td>
<td><p>Cette valeur doit être de 50 ms en moyenne. Les pics (valeurs maximales) ne doivent pas être supérieurs à 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Processus MSExchange ADAccess(*)\Durée de lecture LDAP</p></td>
<td><p>Indique la durée (en ms) pour envoyer une demande de lecture LDAP au contrôleur de domaine spécifié et recevoir une réponse.</p></td>
<td><p>Cette valeur doit être de 50 ms en moyenne. Les pics (valeurs maximales) ne doivent pas être supérieurs à 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Processus MSExchange ADAccess(*)\Durée de recherche LDAP</p></td>
<td><p>Indique la durée (en ms) pour envoyer une demande de recherche LDAP et recevoir une réponse.</p></td>
<td><p>Cette valeur doit être de 50 ms en moyenne. Les pics (valeurs maximales) ne doivent pas être supérieurs à 100 ms.</p></td>
</tr>
</tbody>
</table>


## Processeur et compteurs de processus

Le tableau suivant affiche les seuils acceptables et des informations sur les processeurs et les compteurs de processus.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Compteur</th>
<th>Description</th>
<th>Seuil</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processeur(_Total)\% temps processeur</p></td>
<td><p>Indique le pourcentage de temps pendant lequel le processeur exécute une application ou utilise des processus système. Ceci est lorsque le processeur est actif.</p></td>
<td><p>Cette valeur doit être inférieure à 75 % en moyenne.</p></td>
</tr>
<tr class="even">
<td><p>Processeur(_Total)\% temps utilisateur</p></td>
<td><p>Indique le pourcentage de temps processeur passé en mode utilisateur. Le mode utilisateur est un mode de traitement restreint conçu pour les applications, les sous-systèmes d'environnement et les sous-systèmes intégraux.</p></td>
<td><p>Cette valeur doit être inférieure à 75 % en moyenne.</p></td>
</tr>
<tr class="odd">
<td><p>Processeur(_Total)\% temps privilégié</p></td>
<td><p>Indique le pourcentage de temps processeur passé en mode privilégié. Le mode privilégié est un mode de traitement conçu pour les composants de système d'exploitation et les pilotes de matériel. Il permet un accès direct au matériel et à toute la mémoire.</p></td>
<td><p>Cette valeur doit être inférieure à 75 % en moyenne.</p></td>
</tr>
<tr class="even">
<td><p>Système\Longueur de la file du processeur (toutes les instances)</p></td>
<td><p>Indique le nombre de threads servis par chaque processeur. La longueur de la file du processeur peut servir à identifier si la contention du processeur ou l'utilisation élevée du processeur est due à la capacité insuffisante du processeur pour gérer les charges de travail qui lui sont assignées. La longueur de la file du processeur indique le nombre de threads qui sont retardés dans la file de disponibilité du processeur et attendent d'être planifiés pour l'exécution. La valeur indiquée est la dernière valeur observée au moment de la prise de la mesure.</p></td>
<td><p>Elle ne doit pas être supérieure à 5 par processeur.</p></td>
</tr>
<tr class="odd">
<td><p>Processus(*)\% temps processeur</p></td>
<td><p>Permet d'identifier les processus spécifiques qui utilisent le processeur.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs de mémoire

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs de mémoire.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>Mémoire\Mégaoctets disponibles</p></td>
<td><p>Indique la quantité de mémoire physique, en mégaoctets (Mo), immédiatement disponible pour une allocation à un processus ou pour une utilisation système. Elle est égale à la somme de mémoire attribuée aux listes de page zéro, en attente (mises en cache) et disponibles. Pour une explication complète du gestionnaire de mémoire, référez-vous à MSDN ou au chapitre Performance du système et résolution de problèmes dans le guide du Kit de ressources Windows Server 2003.</p></td>
<td><p>Elle doit rester supérieure à 5 % de la mémoire RAM totale.</p></td>
</tr>
<tr class="odd">
<td><p>Mémoire\% octets dédiés utilisés</p></td>
<td><p>Indique le rapport entre la mémoire\octets dédiés et la mémoire\limite de mémoire dédiée. La mémoire dédiée est la mémoire physique utilisée pour laquelle un espace a été réservé dans le fichier de pagination s'il doit être écrit sur le disque. La limite de mémoire dédiée est déterminée par la taille du fichier de pagination. Si le fichier de pagination est agrandi, la limite de mémoire dédiée augmente et le rapport diminue. Ce compteur affiche la valeur de pourcentage actuel uniquement et non une moyenne.</p></td>
<td><p>Si cette valeur est supérieure à 80 %, c'est que le système est probablement sous contrainte pour fournir davantage de mémoire.</p></td>
</tr>
</tbody>
</table>


## Compteurs .NET Framework

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs .NET Framework.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>Mémoire CLR .NET(*)\% temps dans le GC</p></td>
<td><p>Indique le moment où a eu lieu le nettoyage de la mémoire. Lorsque le compteur dépasse le seuil, cela indique que le processeur est en cours de nettoyage et qu'il n'est pas utilisé de manière efficace pour la charge. Ajoutez de la mémoire au serveur pour améliorer cette situation.</p></td>
<td><p>Elle doit être inférieure à 10 % en moyenne.</p></td>
</tr>
<tr class="odd">
<td><p>Exceptions CLR .NET(*)\Nombre d'exceptions envoyées par seconde</p></td>
<td><p>Affiche le nombre d'exceptions envoyées par seconde. Elles comprennent les exceptions .NET Framework et les exceptions non gérées qui sont converties en exceptions .NET Framework. Par exemple, l'exception de référence de pointeur null dans du code non géré est renvoyée dans du code géré en tant qu'exception .NET Framework System.NullReferenceException. Ce compteur inclut les exceptions gérées et non gérées.</p></td>
<td><p>Elle doit être inférieure à 5 % du nombre total de demandes par seconde (RPS) (serveur web(_Total)\Tentatives de connexion/sec * ,05).</p></td>
</tr>
<tr class="even">
<td><p>Mémoire CLR .NET(*)\Nombre d'octets dans tous les tas</p></td>
<td><p>Affiche la somme des quatre autres compteurs : Taille tas génération 0, Taille tas génération 1, Taille tas génération 2 et Taille tas grand objet. Ce compteur indique la mémoire actuellement allouée en octets sur les tas GC.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs de réseau

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs de réseau courants.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>Interface réseau(*)\Erreurs de paquets sortants</p></td>
<td><p>Indique le nombre de paquets sortants qui n'ont pas pu être transmis en raison d'erreurs.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Échecs de connexion</p></td>
<td><p>Indique le nombre de connexions TCP dont l'état actuel est ESTABLISHED ou CLOSE-WAIT. Le nombre de connexions TCP qui peuvent être établies est limité par la taille de la réserve non paginée. Lorsque la réserve non paginée est épuisée, aucune nouvelle connexion ne peut être établie.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Réinitialisation des connexions</p></td>
<td><p>Indique le nombre de fois que les connexions TCP ont effectué une transition directe vers l'état CLOSED à partir de l'état ESTABLISHED ou de l'état CLOSE-WAIT.</p></td>
<td><p>Un nombre croissant de réinitialisations ou un augmentation constante du taux de réinitialisations peut indiquer une bande passante insuffisante.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Réinitialisation des connexions</p></td>
<td><p>Indique le nombre de fois que les connexions TCP ont effectué une transition directe vers l'état CLOSED à partir de l'état ESTABLISHED ou de l'état CLOSE-WAIT.</p></td>
<td><p>Un nombre croissant de réinitialisations ou un augmentation constante du taux de réinitialisations peut indiquer une bande passante insuffisante.</p></td>
</tr>
</tbody>
</table>


## Compteurs d'accès réseau

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs courants pour le suivi des problèmes d'authentification NTLM et des problèmes MaxConcurrentAPI. Pour plus d’informations, consultez l’article 2688798 de la Base de connaissances Microsoft [Comment effectuer le réglage des performances pour l’authentification NTLM en utilisant le paramètre MaxConcurrentApi](https://go.microsoft.com/fwlink/p/?linkid=389728).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Attentes de sémaphore</p></td>
<td><p>Le nombre de threads en attente pour obtenir le sémaphore.</p></td>
<td><p>Consultez l’article 2688798 de la Base de connaissances Microsoft <a href="https://go.microsoft.com/fwlink/p/?linkid=389728">Comment effectuer le réglage des performances pour l’authentification NTLM en utilisant le paramètre MaxConcurrentApi</a>.</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Détenteurs de sémaphore</p></td>
<td><p>Le numéro du thread qui détient le sémaphore.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Acquisitions de sémaphore</p></td>
<td><p>Le nombre total de fois où le sémaphore a été obtenu sur la durée de vie de la connexion de canal de sécurité, ou depuis le démarrage du système pour _Total.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Délais dépassés d'attente de sémaphore</p></td>
<td><p>Le nombre total de fois où le délai d'attente d'un sémaphore a été dépassé pour un thread sur la durée de vie de la connexion de canal de sécurité, ou depuis le démarrage du système pour _Total.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Temps moyen de retenue du sémaphore</p></td>
<td><p>Le temps moyen (en secondes) pendant lequel le sémaphore est retenu sur le dernier exemple.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs de la base de données

Le tableau suivant indique les compteurs des besoins de latence des E/S du journal actif. Le dépassement des seuils altère l’expérience client. Par exemple, les utilisateurs risquent de subir un ralentissement des performances du système et des retards dans la remise des messages.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les instructions relatives à la latence de stockage normale dans Exchange 2013 sont très semblables à celles d’Exchange 2010. Des compteurs de bases de données supplémentaires sont disponibles dans <a href="https://go.microsoft.com/fwlink/p/?linkid=525622">Compteurs de serveurs de boîtes aux lettres</a>.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des lectures de base de données E/S (associées)</p></td>
<td><p>Indique le temps moyen, exprimé en ms, par opération de lecture dans la base de données.</p></td>
<td><p>Cette valeur doit être inférieure à 20 ms en moyenne.</p></td>
</tr>
<tr class="odd">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des écritures de base de données E/S (associées)</p></td>
<td><p>Indique le temps moyen, exprimé en ms, par opération d’écriture dans la base de données.</p></td>
<td><p>Cette valeur doit être inférieure à 50 ms en moyenne.</p></td>
</tr>
<tr class="even">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des écritures de journal E/S</p></td>
<td><p>Indique le temps moyen, exprimé en ms, par opération d’écriture dans le journal.</p></td>
<td><p>Cette valeur doit être inférieure à 10 ms en moyenne.</p></td>
</tr>
<tr class="odd">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des lectures de base de données E/S (récupération)</p></td>
<td><p>Indique le temps moyen, exprimé en ms, par opération de lecture dans la base de données passive.</p></td>
<td><p>Cette valeur doit être inférieure à 200 ms en moyenne.</p></td>
</tr>
<tr class="even">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des écritures de base de données E/S (récupération)</p></td>
<td><p>Indique le temps moyen, exprimé en ms, par opération d’écriture dans la base de données passive.</p></td>
<td><p>Cette valeur doit être inférieure à la latence de lecture pour la même instance, telle que mesurée par le compteur Base de données MSExchange ==&gt; Instances(*)\Latence moyenne des lectures de base de données E/S (récupération).</p></td>
</tr>
<tr class="odd">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Lectures de base de données E/S (associées)/s</p></td>
<td><p>Indique le nombre d'opérations de lectures de base de données par seconde pour chaque instance de base de données associée.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Écritures de base de données E/S (associées)/s</p></td>
<td><p>Indique le nombre d'opérations d'écritures de base de données par seconde pour chaque instance de base de données associée.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>Base de données MSExchange ==&gt; Instances(*)\Écritures E/S de journal/s</p></td>
<td><p>Indique le nombre d'écritures de journal par seconde pour chaque instance de base de données.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Active Manager(_total)\Base de données montée</p></td>
<td><p>Indique le nombre de copies de base de données actives sur le serveur.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## ASP.NET

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs ASP.NET.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Redémarrages de l’application</p></td>
<td><p>Indique le nombre de fois que l’application a été redémarrée durant la durée de vie du serveur web.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Redémarrages du processus de travail</p></td>
<td><p>Ce compteur indique le nombre de fois qu’un processus de travail a redémarré sur l’ordinateur.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Durée d'attente de la demande</p></td>
<td><p>Indique le nombre de millisecondes pendant lequel la demande la plus récente a attendu dans la file d’attente.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="odd">
<td><p>Applications ASP.NET(*)\Demandes dans la file d’attente d’application</p></td>
<td><p>Indique le nombre de demandes dans la file d’attente de demande d’application.</p></td>
<td><p>Cette valeur doit être égale à 0 en permanence.</p></td>
</tr>
<tr class="even">
<td><p>Applications ASP.NET(*) \Demandes en cours d'exécution</p></td>
<td><p>Indique le nombre de demandes en cours d'exécution.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>Applications ASP.NET(*)\Demandes/s</p></td>
<td><p>Indique le nombre de demandes exécutées par seconde.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs d’accès au client RPC

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs d'accès au client RPC.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Latence RPC moyenne</p></td>
<td><p>Indique la latence moyenne, en millisecondes, pour les 1 024 derniers paquets.</p></td>
<td><p>Elle doit être inférieure à 250 ms.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Demandes RPC</p></td>
<td><p>Affiche le nombre de demandes client actuellement traitées par le service d’accès au client RPC.</p></td>
<td><p>Ce nombre ne doit pas être supérieur à 40.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Nombre d’utilisateurs actifs</p></td>
<td><p>Affiche le nombre d’utilisateurs uniques qui ont indiqué une activité au cours des deux dernières minutes.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Nombre de connexions</p></td>
<td><p>Affiche le nombre total de connexions client maintenues.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Opérations RPC/s</p></td>
<td><p>Affiche la vitesse à laquelle les opérations RPC ont lieu par seconde.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Nombre d’utilisateurs</p></td>
<td><p>Indique le nombre d’utilisateurs connectés au service.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs de proxy HTTP

Le tableau suivant affiche des informations sur les compteurs de proxy HTTP.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Latence moyenne MailboxServerLocator</p></td>
<td><p>Indique la latence moyenne (ms) des appels de service web MailboxServerLocator.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Latence d'authentification moyenne</p></td>
<td><p>Affiche le temps moyen passé à authentifier des demandes CAS sur les 200 derniers exemples.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Latence de traitement moyenne du serveur ClientAccess</p></td>
<td><p>Indique la latence moyenne (ms) de traitement CAS (n'inclut pas le temps consacré à la transmission par proxy) sur les 200 dernières demandes.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Taux d'échec de proxy de serveur de boîte aux lettres</p></td>
<td><p>Indique le pourcentage d'échecs liés à la connectivité entre ce serveur d'accès au client et les serveurs MBX sur les 200 derniers exemples.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Demandes de proxy en attente</p></td>
<td><p>Indique le nombre de demandes simultanées de proxy en attente.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Demandes de proxy/s</p></td>
<td><p>Indique le nombre de demandes de proxy traitées par seconde.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Demandes/s</p></td>
<td><p>Indique le nombre de demandes traitées par seconde.</p></td>
</tr>
</tbody>
</table>


## Compteurs de banque d’informations

Le tableau suivant affiche les seuils acceptables et des informations sur les compteurs de banque d'informations.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les instructions relatives à la latence de stockage normale dans Exchange 2013 sont très semblables à celles d’Exchange 2010. Des compteurs de banques d’informations supplémentaires sont disponibles dans <a href="https://go.microsoft.com/fwlink/p/?linkid=525622">Compteurs de serveurs de boîtes aux lettres</a>.</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
<td><p>Seuil</p></td>
</tr>
<tr class="even">
<td><p>Demandes \RPC de banque d’informations MSExchangeIS (*)</p></td>
<td><p>Indique les demandes RPC globales actuellement en cours d’exécution dans le processus de banque d’informations.</p></td>
<td><p>Cette valeur doit être inférieure à 70 en permanence.</p></td>
</tr>
<tr class="odd">
<td><p>Type de client MSExchangeIS(*)\Latence RPC moyenne</p></td>
<td><p>Indique la latence RPC du serveur, exprimée en ms, des 1 024 derniers paquets pour un protocole client particulier.</p></td>
<td><p>Cette valeur doit être inférieure à 50 ms en moyenne pour chaque client.</p></td>
</tr>
<tr class="even">
<td><p>Banque MSExchangeIS(*)\Latence RPC moyenne</p></td>
<td><p>La moyenne de la latence RPC (ms) est la latence moyenne en millisecondes des demandes RPC par base de données. La moyenne est calculée sur l’ensemble des RPC depuis le chargement d’exrpc32.</p></td>
<td><p>Cette valeur doit être inférieure à 50 ms en permanence, avec des pics inférieurs à 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Banque MSExchangeIS(*)\Opérations RPC/s</p></td>
<td><p>Indique le nombre d'opérations RPC par seconde pour chaque instance de base de données.</p></td>
<td><p>Non applicable</p></td>
</tr>
<tr class="even">
<td><p>Type de client MSExchangeIS(*)\Opérations RPC/s</p></td>
<td><p>Indique le nombre d'opérations RPC par seconde pour chaque type de connexion client.</p></td>
<td><p>Non applicable</p></td>
</tr>
</tbody>
</table>


## Compteurs du serveur d’accès au client

Le tableau suivant affiche des informations sur les compteurs de connexion du client et les compteurs Internet Information Services (IIS).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Demandes/s</p></td>
<td><p>Indique le nombre de demandes HTTP reçues par seconde du client via ASP.NET. Détermine la fréquence des demandes Exchange ActiveSync actuelle. Permet uniquement de déterminer la charge utilisateur actuelle.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Commandes Ping en attente</p></td>
<td><p>Affiche le nombre de commandes ping actuellement en file d’attente.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Commandes Sync/s</p></td>
<td><p>Indique le nombre de commandes sync traitées par seconde. Les clients utilisent cette commande pour synchroniser des éléments à l’intérieur d’un dossier.</p></td>
</tr>
<tr class="odd">
<td><p>Service de disponibilité MSExchange\Demandes de disponibilité (sec)</p></td>
<td><p>Indique le nombre de demandes traitées par seconde. La demande peut uniquement servir pour avoir des informations de disponibilité ou pour inclure des suggestions. Une demande peut contenir plusieurs boîtes aux lettres. Détermine la fréquence à laquelle les demandes de service de disponibilité surviennent.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Utilisateurs uniques actuels</p></td>
<td><p>Indique le nombre d’utilisateurs uniques actuellement connectés à Outlook Web App. Cette valeur suit le nombre de sessions utilisateur actives uniques, de sorte que des utilisateurs ne sont supprimés de ce compteur uniquement après qu'ils se sont déconnectés ou que leur session a expiré. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Demandes/s</p></td>
<td><p>Indique le nombre de demandes traitées par Outlook Web App par seconde. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Demandes/s</p></td>
<td><p>Indique le nombre de demandes de service de découverte automatique traitées par seconde. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Demandes/s</p></td>
<td><p>Indique le nombre de demandes traitées par seconde. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="even">
<td><p>Service Web(_Total)\Connexions actuelles</p></td>
<td><p>Indique le nombre de connexions actuelles établies avec le service web. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="odd">
<td><p>Service Web(site web par défaut)\Connexions actuelles</p></td>
<td><p>Indique le nombre actuel de connexions établies sur le site web par défaut qui correspond au nombre de connexions en appuyant sur le rôle de serveur CAS frontal. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="even">
<td><p>WebService(_Total)\Tentatives de connexion/s</p></td>
<td><p>Indique la fréquence des tentatives de connexion au service web. Détermine la charge utilisateur actuelle.</p></td>
</tr>
<tr class="odd">
<td><p>Service Web(_Total)\Autres méthodes de demande/s</p></td>
<td><p>Indique la fréquence de demandes HTTP qui n’utilisent pas les méthodes OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, MOVE, COPY, MKCOL, PROPFIND, PROPPATCH, SEARCH, LOCK ou UNLOCK. Détermine la charge utilisateur actuelle.</p></td>
</tr>
</tbody>
</table>


## Compteurs de gestion de la charge de travail

Le tableau suivant affiche des informations sur les compteurs de gestion de la charge de travail Exchange. Ces compteurs sont importants à surveiller car la gestion de la charge de travail peut exécuter des tâches en arrière-plan pendant les heures creuses.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compteur</p></td>
<td><p>Description</p></td>
</tr>
<tr class="even">
<td><p>Charges de travail WorkloadManagement MSExchange(*)\ActiveTasks</p></td>
<td><p>Indique le nombre de tâches actives en cours d'exécution en arrière-plan pour la gestion de la charge de travail.</p></td>
</tr>
<tr class="odd">
<td><p>Charges de travail WorkloadManagement MSExchange(*)\CompletedTasks</p></td>
<td><p>Indique le nombre de tâches de gestion de la charge de travail qui ont été effectuées.</p></td>
</tr>
<tr class="even">
<td><p>Charges de travail WorkloadManagement MSExchange(*) \QueuedTasks</p></td>
<td><p>Indique le nombre de tâches de gestion de la charge de travail qui sont actuellement en file d'attente pour être traitées.</p></td>
</tr>
</tbody>
</table>

