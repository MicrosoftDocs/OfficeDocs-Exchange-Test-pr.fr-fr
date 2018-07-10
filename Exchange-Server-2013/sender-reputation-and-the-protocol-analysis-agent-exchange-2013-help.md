---
title: 'Réputation de l’expéditeur et agent d’analyse de protocole: Exchange 2013 Help'
TOCTitle: Réputation de l’expéditeur et agent d’analyse de protocole
ms:assetid: c4c34235-d545-41e7-ac2f-1dd43aaa3708
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124512(v=EXCHG.150)
ms:contentKeyID: 50479127
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Réputation de l’expéditeur et agent d’analyse de protocole

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Le niveau de réputation de l’expéditeur fait partie de la fonctionnalité de blocage du courrier indésirable Exchange qui bloque les messages en fonction des nombreuses caractéristiques de l’expéditeur. La fonctionnalité de réputation de l’expéditeur s’appuie sur des données conservées relatives à l’expéditeur pour déterminer, le cas échéant, l’action à appliquer à un message entrant. L’agent d’analyse de protocole est l’agent sous-jacent pour la fonctionnalité de réputation de l’expéditeur.

Lorsque vous configurez des agents de blocage du courrier indésirable sur un serveur Exchange, les agents agissent de façon cumulative sur les messages pour réduire le nombre de messages non sollicités entrant dans l’organisation.

**Contenu de cette rubrique**

Calculation of the sender reputation level

Use of the SRL

Enabling and configuring the detection of open proxy servers

Setting the SRL block threshold

## Calcul du niveau de réputation de l’expéditeur

Le niveau de réputation de l’expéditeur (SRL) est calculé à partir des statistiques suivantes :

  - **Analyse HELO/EHLO**   Les commandes SMTP HELO et EHLO sont destinées à fournir un nom de domaine, tel que Contoso.com, ou une adresse IP du serveur SMTP de l’expéditeur au serveur SMTP du destinataire. Les utilisateurs malveillants, ou *expéditeurs de courrier indésirable*, usurpent fréquemment les instructions HELO/EHLO de différentes manières. Par exemple, ils tapent une adresse IP qui ne correspond pas à l’adresse IP de la provenance de la connexion. Les expéditeurs de courrier indésirable insèrent également des domaines connus pour être localement pris en charge sur le serveur destinataire dans une instruction HELO pour tenter de faire apparaître les domaines comme s’ils faisaient partie de l’organisation. Dans d’autres cas, les expéditeurs de courrier indésirable modifient le domaine transmis dans l’instruction HELO. Le comportement typique d’un utilisateur légitime peut être d’utiliser un ensemble relativement constant de plusieurs domaines dans ses instructions HELO.
    
    Par conséquent, l’analyse de l’instruction HELO/EHLO sur une base expéditeur peut indiquer que l’expéditeur est vraisemblablement un expéditeur de courrier indésirable. Par exemple, il y a de grandes chances pour qu’un expéditeur qui fournit de nombreuses instructions HELO/EHLO uniques dans une période spécifique soit un expéditeur de courrier indésirable. Les expéditeurs qui fournissent constamment une adresse IP dans l’instruction HELO qui ne correspond pas à l’adresse IP d’origine déterminée par l’agent de filtrage des connexions sont également davantage susceptibles d’être des expéditeurs de courrier indésirable. Les expéditeurs distants qui fournissent constamment un nom de domaine local dans l’instruction HELO qui se trouve dans la même organisation que le serveur Exchange sont également davantage susceptibles d’être des expéditeurs de courrier indésirable.

  - **Recherche DNS inverse**   La fonction de réputation de l’expéditeur vérifie également que l’adresse IP d’origine à partir de laquelle l’expéditeur transmet le message correspond au nom de domaine enregistré soumis par l’expéditeur dans la commande HELO ou EHLO.
    
    La fonction de réputation de l’expéditeur effectue une requête DNS inverse en soumettant l’adresse IP d’origine au DNS. Le résultat renvoyé par le DNS est le nom de domaine enregistré en utilisant l’autorité de dénomination de domaine pour cette adresse IP. La fonction de réputation de l’expéditeur compare le nom de domaine qui est renvoyé par le DNS au nom de domaine que l’expéditeur a soumis dans la commande SMTP HELO/EHLO. Si les noms de domaine ne correspondent pas, il est probable que l’expéditeur soit un expéditeur de courrier indésirable et le seuil SRL global pour l’expéditeur est augmenté.
    
    L’agent d’ID de l’expéditeur effectue une tâche similaire, mais la réussite de celle-ci repose sur les expéditeurs légitimes pour mettre à jour l’infrastructure DNS afin d’identifier tous les serveurs SMTP expéditeurs de messages électroniques dans l’organisation. En effectuant une recherche DNS inverse, vous contribuez à l’identification d’expéditeurs potentiels de courrier indésirable.

  - **Analyse de contrôle d’accès SCL sur les messages d’un expéditeur particulier**   Lorsque l’agent de filtrage du contenu traite un message, il affecte des contrôles d’accès SCL au message. Le seuil de probabilité de courrier indésirable est un nombre compris entre 0 et 9. Une valeur élevée indique qu’un message est probablement un courrier indésirable. Les données sur chaque expéditeur et valeurs SCL que leurs messages génèrent sont conservées pour analyse par la fonction de réputation de l’expéditeur. La fonction de réputation de l’expéditeur calcule les statistiques sur un expéditeur en fonction du ratio entre tous les messages en provenance de cet expéditeur qui avaient une valeur de contrôle d’accès SCL faible dans le passé et tous les messages en provenance de cet expéditeur qui avaient une valeur de contrôle d’accès SCL élevée dans le passé. En outre, le nombre de messages ayant une valeur de contrôle d’accès SCL élevée que l’expéditeur a envoyé durant la dernière journée est appliqué au SRL général.

  - **Test de proxy expéditeur ouvert**   Un *proxy ouvert* est un serveur proxy qui accepte les demandes de connexion de n’importe qui, n’importe où et transmet le trafic comme s’il était en provenance des hôtes locaux. Les serveurs proxy relaient le trafic TCP à travers les hôtes du pare-feu pour fournir à l’utilisateur un accès transparent aux applications via le pare-feu. Comme les protocoles proxy sont indépendants des protocoles d’application utilisateur, les proxy peuvent être utilisés par de nombreux services différents. Les proxy peuvent également être utilisés pour partager une connexion Internet unique entre plusieurs hôtes. Les proxy sont généralement définis de telle sorte que seuls les hôtes fiables au niveau du pare-feu peuvent utiliser les proxy. Il se peut qu’un expéditeur légitime soit un proxy ouvert en raison d’une mauvaise configuration involontaire ou d’un programme malveillant.
    
    Les proxy ouverts fournissent aux utilisateurs malveillants une solution idéale pour masquer leur réelle identité et lancer des attaques par déni de service ou envoyer du courrier indésirable. Comme de plus en plus de serveurs proxy sont configurés pour être « ouverts par défaut », les proxy ouverts sont de plus en plus courants. En outre, les utilisateurs malveillants peuvent utiliser plusieurs proxy ouverts pour masquer l’adresse IP d’origine de l’expéditeur.
    
    Lorsque la fonction de réputation de l’expéditeur effectue un test de proxy ouvert, elle le fait en mettant en forme une demande SMTP lors d’une tentative de reconnexion au serveur Exchange à partir du proxy ouvert. Si une demande SMTP est reçue du proxy, la fonction de réputation de l’expéditeur vérifie que le proxy est ouvert et met à jour les statistiques de test de proxy ouvert pour cet expéditeur.

La réputation de l’expéditeur pondère chacune de ces statistiques et calcule le SRL pour chaque expéditeur. Le SRL est un nombre compris entre 0 et 9 qui indique la probabilité qu’un expéditeur spécifique soit un expéditeur de courrier indésirable ou un utilisateur malveillant. La valeur 0 indique que l’expéditeur n’est probablement pas un expéditeur de courrier indésirable et la valeur 9 indique l’expéditeur est probablement un expéditeur de courrier indésirable.

Vous pouvez configurer un seuil de blocage compris entre 0 et 9 à partir duquel la fonction de réputation de l’expéditeur envoie une demande à l’agent de filtrage des expéditeurs et, par conséquent, empêche l’expéditeur d’envoyer un message à l’organisation. Quand un expéditeur est bloqué, il est ajouté à la liste des expéditeurs proscrits pour une période configurable. Le mode de gestion des messages bloqués dépend de la configuration de l’agent de filtrage des expéditeurs. Les actions suivantes sont les options de gestion des messages bloqués :

  - Rejeter

  - Supprimer et archiver

  - Accepter et marquer comme expéditeur proscrit

Si un expéditeur est inclus dans la liste d’adresses IP bloquées ou le service de réputation d’IP de Microsoft, la fonctionnalité de réputation de l’expéditeur envoie une demande immédiate à l’agent de filtrage des expéditeurs pour bloquer l’expéditeur. Pour tirer parti de cette fonctionnalité, vous devez activer et configurer le service de mise à jour antispam de Microsoft Exchange.

Par défaut, la réputation de l’expéditeur définit un contrôle d’accès de 0 pour les expéditeurs qui n’ont pas été analysés. Quand un expéditeur a envoyé 20 messages ou plus, la fonctionnalité de réputation de l’expéditeur calcule un SRL à partir des statistiques précédemment décrites dans cette rubrique.

Retour au début

## Utilisation du SRL

La fonction de réputation de l’expéditeur agit sur les messages durant deux phases de la session SMTP :

  - **À la commande SMTP MAIL FROM:**    La fonction de réputation de l’expéditeur agit uniquement sur les messages qui ont été bloqués ou traités par l’agent de filtrage des connexions, l’agent de filtrage des expéditeurs, l’agent de filtrage des destinataires ou l’agent d’ID de l’expéditeur. Dans ce cas, la fonction de réputation de l’expéditeur récupère la valeur de contrôle d’accès SRL actuelle de l’expéditeur à partir du profil expéditeur conservé sur le serveur Exchange. Lorsque cette valeur de contrôle d’accès est récupérée et évaluée, la configuration du serveur Exchange impose le comportement d’une connexion particulière en fonction du seuil de blocage.

  - **Après la commande SMTP « fin des données »**   La commande SMTP de fin du transfert de données (**EOD**) est donnée lorsque toutes les données de messages réelles sont envoyées. À ce point de la session SMTP, de nombreux agents de blocage du courrier indésirable ont traité le message. En tant que sous-produit du traitement de blocage du courrier indésirable, les statistiques sur lesquelles la fonctionnalité de réputation de l’expéditeur se base sont mises à jour. Par conséquent, la fonctionnalité de réputation de l’expéditeur dispose des données nécessaires au calcul ou au nouveau calcul d’une valeur de contrôle d’accès pour l’expéditeur.

Pour plus d’informations, voir [Gérer la réputation de l’expéditeur](manage-sender-reputation-exchange-2013-help.md).

Retour au début

## Activation et configuration de la détection des serveurs proxy ouverts

La réputation de l’expéditeur évalue plusieurs caractéristiques de l’expéditeur pour calculer un SRL. Parmi celles-ci, figurent les résultats d’un test pour les serveurs de proxy ouverts. Souvent, les expéditeurs de courrier indésirable routent des messages via des serveurs proxy ouverts sur Internet. En ce faisant, les expéditeurs de courrier indésirable peuvent envoyer des messages qui semblent provenir d’un serveur autre que le leur.

Lorsque la réputation de l’expéditeur calcule une valeur SRL, elle tente de se connecter à l’adresse IP d’origine de l’expéditeur en utilisant une série de protocoles proxy ordinaires, tels que SOCKS4, SOCKS5, HTTP, Telnet, Cisco et Wingate. La réputation de l’expéditeur met en forme une demande spécifique au protocole en tentant de se reconnecter au serveur de transport Edge depuis le serveur proxy ouvert à l’aide d’une demande SMTP (Simple Mail Transfer Protocol). Si une demande SMTP est reçue du serveur proxy, la réputation de l’expéditeur vérifie que le serveur proxy est un serveur ouvert et ajuste le niveau de réputation de l’expéditeur en fonction de ce résultat. Par défaut, la détection de serveurs proxy ouverts est activée par la réputation de l’expéditeur.

Pour plus d’informations sur l’activation et la configuration de la détection des serveurs proxy ouverts, voir [Gérer la réputation de l’expéditeur](manage-sender-reputation-exchange-2013-help.md).

Retour au début

## Définition du seuil de blocage SRL

Le SRL est un nombre compris entre 0 et 9 qui indique la probabilité qu’un expéditeur spécifique soit un expéditeur de courrier indésirable ou un utilisateur malveillant. Vous devez définir un seuil auquel SRL doit bloquer les expéditeurs. Ce seuil de blocage SRL définit la valeur SRL qui doit être dépassée pour que l’agent de réputation de l’expéditeur bloque un expéditeur. Par défaut, le SRL est défini sur 7. Il est recommandé de contrôler l’efficacité de l’agent au niveau par défaut. Vous pouvez ajuster la valeur pour satisfaire les besoins de votre organisation. Si vous définissez d’autres agents de blocage du courrier indésirable de façon agressive, il se peut que vous soyez en mesure de définir un seuil SRL plus élevé pour la réputation de l’expéditeur que vous ne le feriez si les autres agents de blocage du courrier indésirable n’étaient pas définis de façon agressive. Pour plus d’informations sur l’ajustement des configurations de blocage du courrier indésirable de façon à réduire le courrier indésirable, voir [Protection contre le courrier indésirable](anti-spam-protection-exchange-2013-help.md).

Sur un serveur de transport Edge, en cas de dépassement du seuil de blocage SRL pour un expéditeur particulier, la réputation de l’expéditeur ajoute l’expéditeur à la liste rouge des expéditeurs de l’agent de filtrage des connexions. Parfois, des expéditeurs de courrier indésirable envoient des lots de courrier indésirable à partir d’un expéditeur unique. Dans ce scénario, si la réputation de l’expéditeur calcule qu’une valeur de SRL dépasse le seuil de blocage SRL, l’expéditeur est ajouté à la liste rouge des expéditeurs pendant une durée configurable. La durée par défaut est de 24 heures. Après 24 heures, l’expéditeur est supprimé de la liste de blocage des expéditeurs et peut de nouveau envoyer des messages.

Lorsqu’un expéditeur est ajouté à la liste rouge d’IP, la réputation de l’expéditeur supprime le profil de l’expéditeur. La réputation de l’expéditeur supprime le profil parce que le profil bloqué de l’expéditeur existant indique que le SRL de l’expéditeur excède le seuil de blocage SRL. Ceci engendre un nouvel ajout de l’expéditeur bloqué dans la liste d’interdiction d’IP une fois le blocage d’expéditeur terminé.

Pour plus d’informations, voir [Gérer la réputation de l’expéditeur](manage-sender-reputation-exchange-2013-help.md).

Retour au début

