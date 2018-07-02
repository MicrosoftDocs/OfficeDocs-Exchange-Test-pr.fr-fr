---
title: 'Critère de diffusion d’échec de requête DNS: Exchange 2013 Help'
TOCTitle: Critère de diffusion d’échec de requête DNS
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52062987
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Critère de diffusion d’échec de requête DNS

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-02_

Dans Microsoft Exchange Server 2013, vous pouvez régler le critère de la requête DNS pour une remise des messages légèrement plus rapide lorsque le domaine de destination rencontre des erreurs DNS. Toutefois, selon les erreurs DNS, ce réglage peut provoquer des échecs de remise de message dans certaines circonstances.

## Requêtes DNS et remise de messages distante

Le serveur Exchange responsable de la remise des messages à des destinataires externes doit pouvoir trouver un serveur de messagerie de destination qui accepte les messages des destinataires externes. Selon la destination, les messages sont placés dans une ou plusieurs files d'attente distantes en attendant d'être remis aux destinataires distants. Pour plus d'informations sur les files d'attente de remise, consultez la rubrique [Files d'attente](queues-exchange-2013-help.md).

Le serveur Exchange interroge les serveurs DNS configurés pour trouver les enregistrements DNS requis pour remettre le message. Les serveurs DNS sont interrogés dans l'ordre dans lequel ils figurent dans la liste. Si l'un des serveurs DNS est indisponible, la requête va au serveur DNS suivant dans la liste. Les serveurs DNS sont interrogés pour les informations suivantes :

  - **Enregistrements MX (mail exchange) de la partie correspondant au domaine du destinataire externe**   L'enregistrement MX contient le nom de domaine complet (FQDN) du serveur de messagerie responsable de l'acceptation des messages pour le domaine, et une valeur de préférence pour ce serveur de messagerie. Une valeur de préférence inférieure indique un serveur de messagerie préféré. La valeur de préférence est importante si le domaine possède plusieurs enregistrements MX. Pour augmenter la tolérance aux pannes, la plupart des organisations utilisent plusieurs serveurs de messagerie et plusieurs enregistrements MX ayant différentes valeurs de préférence.

  - **Enregistrements d'adresse (A) des serveurs de messagerie de destination**   Chaque serveur de messagerie utilisé dans un enregistrement MX doit posséder un enregistrement A correspondant. L'enregistrement A est utilisé pour trouver l'adresse IP du serveur de messagerie de destination. Le serveur de transport Edge abonné utilise l'adresse IP pour ouvrir une connexion SMTP (Simple Mail Transfer Protocol) avec le serveur de messagerie de destination. Bien qu'il soit techniquement possible d'utiliser le nom de domaine complet (FQDN) dans un enregistrement CNAME d'un enregistrement MX, cette pratique ne respecte pas les RFC suivantes : RFC 974, RFC 1034, RFC 1912 et RFC 2181. Par conséquent, la plupart des serveurs de messagerie ne la prennent pas en charge.
    
    La combinaison requise des requêtes DNS itératives et récursives qui commencent avec un serveur DNS racine est utilisée pour résoudre le nom de domaine complet (FQDN) du serveur de messagerie trouvé dans l'enregistrement MX d'une adresse IP.

Dans Exchange 2013, il existe une limite de requête DNS non configurable de 5 secondes pour chaque serveur DNS et une limite d'une minute pour la requête DNS dans son intégralité.

## Problèmes DNS éventuels

Même lorsque les paramètres DNS sur le serveur Exchange sont configurés correctement, des problèmes concernant les enregistrements DNS pour un domaine spécifique ou des problèmes concernant l'un des serveurs DNS utilisés pour rechercher le serveur DNS faisant autorité pour un domaine spécifique peuvent toujours se produire. En général, ces problèmes échappent à votre contrôle. Ils doivent être résolus par les propriétaires de ces serveurs DNS. Ces erreurs liées au DNS peuvent être provoquées par une ou plusieurs des raisons suivantes :

  - Enregistrements DNS non valides pour le domaine de destination

  - Problèmes avec l'utilisation du serveur DNS

  - Problèmes avec la réplication du serveur DNS

Dans Exchange 2013, quand une requête DNS produit des erreurs, la requête est transférée au serveur DNS suivant seulement si ce serveur DNS n'a pas déjà renvoyé une erreur pour la requête en cours.

Vous pouvez contrôler le critère de diffusion d'échec de requête DNS en modifiant le fichier XML de configuration de l'application `%ExchangeInstallPath%bin\EdgeTransport.exe.config`. Ce fichier est associé au service de transport Microsoft Exchange. Les modifications enregistrées dans ce fichier sont appliquées une fois que vous redémarrez le service de transport Microsoft Exchange. Quand vous redémarrez ce service, le flux de messagerie sur le serveur est temporairement interrompu. Le critère de diffusion d'échec de requête DNS est contrôlé par la clé *DnsFaultTolerance* dans le fichier EdgeTransport.exe.config. Cette clé utilise les valeurs suivantes :

  - **Modéré**   Lorsque la requête DNS rencontre une combinaison d'enregistrements MX valides et non valides, la requête DNS continue jusqu'à ce que la valeur du délai d'attente de la requête DNS d'une minute soit atteinte. Les enregistrements MX non valides sont supprimés et l'enregistrement MX valide qui a la valeur de préférence la plus basse est utilisé pour remettre le message au serveur de messagerie de destination. Il s'agit de la valeur par défaut.

  - **Normal**   Lorsque la requête DNS rencontre un enregistrement MX non valide pour la première fois, tout enregistrement MX résolu qui a une valeur de préférence supérieure ou égale aux enregistrements MX non valides est immédiatement supprimé. L'enregistrement MX restant qui a la plus petite valeur de préférence est utilisé pour remettre le message au serveur de messagerie de destination sans attendre que la requête DNS entière n'expire. Bien que ce comportement puisse entraîner une remise des messages plus rapide, l'inconvénient potentiel de ce comportement est que la requête DNS ne possède pas d'enregistrements MX valides si les conditions suivantes sont vraies :
    
      - L'enregistrement MX non valide est le premier enregistrement MX pour le domaine de destination.
    
      - Les enregistrements MX valides ont la même valeur de priorité que les enregistrements MX non valides.

En mode `Normal` et `Lenient`, les résultats de la requête DNS pour une requête MX non valide ne sont jamais mis en cache. Lors de la prochaine exécution d'une requête DNS, celle-ci essaiera de résoudre les enregistrements MX pour le domaine de destination.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.</td>
</tr>
</tbody>
</table>

