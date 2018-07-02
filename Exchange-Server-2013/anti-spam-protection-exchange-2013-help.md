---
title: 'Protection contre le courrier indésirable: Exchange 2013 Help'
TOCTitle: Protection contre le courrier indésirable
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 50478376
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protection contre le courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-06_

Les *expéditeurs de courrier indésirable*, ou expéditeurs malveillants, utilisent différentes techniques pour envoyer du courrier indésirable dans votre organisation. Aucun outil ou processus n'est capable d'éliminer la totalité du courrier indésirable. Néanmoins, Microsoft Exchange Server 2013 offre une méthode en couche, multi-niveaux et multi-facettes pour réduire le nombre de ces messages indésirables. Exchange utilise des agents de transport pour fournir une protection contre le courrier indésirable et les agents intégrés qui sont disponibles dans Exchange 2013 sont relativement identiques à ceux de Microsoft Exchange Server 2010.

Pour plus de fonctionnalités anti-courrier indésirable et une gestion plus facile, vous pouvez acheter Exchange Online Protection (EOP). Pour une comparaison des fonctionnalités d'EOP et d'Exchange 2013, consultez la rubrique [Avantages des fonctionnalités de blocage du courrier indésirable dans Exchange Online Protection sur Exchange Server 2013](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md). Pour en savoir plus sur la protection anti-courrier indésirable d’Office 365, consultez la rubrique [Protection contre le courrier indésirable pour Office 365](https://support.office.com/fr-fr/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us).

Pour obtenir des informations sur les fonctionnalités anti-programme malveillant intégrées dans Exchange 2013, consultez la rubrique [Détection anti-programmes malveillants](anti-malware-protection-exchange-2013-help.md).

**Contenu de cette rubrique**

Agents de blocage du courrier indésirable sur les serveurs de boîtes aux lettres

Agents de blocage du courrier indésirable sur les serveurs de transport Edge

Marquages de courrier indésirable

Stratégie anti-courrier indésirable

## Agents de blocage du courrier indésirable sur les serveurs de boîtes aux lettres

En général, vous activez les agents de blocage du courrier indésirable sur un serveur de boîtes aux lettres si votre organisation ne dispose pas d'un serveur de transport Edge ou n'effectue aucun filtrage du courrier indésirable préalable avant d'accepter les messages entrants. Pour plus d'informations, consultez la rubrique [Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Comme tous les agents de transport, une valeur de priorité est attribuée à chaque agent de blocage du courrier indésirable. Une valeur inférieure indique une priorité supérieure. Par conséquent, un agent de blocage du courrier indésirable qui a la priorité 1 agira sur un message avant un agent de blocage du courrier indésirable qui a la priorité 9. Cependant, l'événement SMTP où l'agent de blocage du courrier indésirable est enregistré est aussi très important pour déterminer l'ordre dans lequel les agents de blocage du courrier indésirable agissent sur les messages. Un agent de blocage du courrier indésirable de basse priorité qui est précocement enregistré sur un événement SMTP dans le pipeline de transport agira sur un message avant un agent de blocage du courrier indésirable de haute priorité qui est enregistré sur un événement SMTP plus tard dans le pipeline de transport.

Sur la base de la valeur de priorité par défaut de l'agent de blocage du courrier indésirable, mais aussi de l'événement SMTP dans le pipeline de transport où l'agent de blocage du courrier indésirable est enregistré, la liste suivante décrit les agents et l'ordre par défaut dans lequel ils sont appliqués aux messages sur un serveur de boîtes aux lettres :

1.  **Agent de filtrage des expéditeurs**   Le filtrage des expéditeurs compare l'expéditeur figurant sur la commande MAIL FROM: SMTP à une liste définie par l'administrateur d'expéditeurs ou de domaines expéditeurs qui ne sont pas autorisés à envoyer des messages à l'organisation afin de déterminer l'action éventuelle à appliquer à un message entrant. Pour plus d'informations, consultez la rubrique [Filtrage des expéditeurs](sender-filtering-exchange-2013-help.md).

2.  **Agent d'ID de l'expéditeur**   L'ID de l'expéditeur utilise l'adresse IP du serveur d'envoi et la PRA (Purported Responsible Address) de l'expéditeur pour déterminer si l'identité de l'expéditeur est falsifiée ou non. Pour plus d'informations, consultez la rubrique [ID de l'expéditeur](sender-id-exchange-2013-help.md).

3.  **Agent de filtrage du contenu**   Le filtrage du contenu évalue le contenu d'un message. Pour plus d'informations, consultez la rubrique [Filtrage du contenu](content-filtering-exchange-2013-help.md).
    
    La mise en quarantaine du courrier indésirable est une fonctionnalité de l'Agent de filtrage du contenu qui réduit le risque de perte de messages légitimes erronément classifiés comme du courrier indésirable. La mise en quarantaine du courrier indésirable fournit un emplacement de stockage temporaire pour les messages identifiés comme courrier indésirable, qui ne doivent pas être remis à une boîte aux lettres d'utilisateur au sein de l'organisation. Pour plus d'informations, consultez la rubrique [Mise en quarantaine du courrier indésirable](spam-quarantine-exchange-2013-help.md).
    
    Le filtrage de contenu agit également sur la fonction d'agrégation de listes fiables. L'agrégation de listes fiables collecte les données des listes fiables de blocage du courrier indésirable que les utilisateurs de Microsoft Outlook et Outlook Web App configurent, et met ces données à la disposition de l'agent de filtrage du contenu. Pour plus d'informations, consultez la rubrique [Agrégation de listes fiables](safelist-aggregation-exchange-2013-help.md).

4.  **Agent d'analyse de protocole**   L'agent d'analyse de protocole est l'agent sous-jacent qui implémente la fonctionnalité de réputation de l'expéditeur. La fonctionnalité de réputation de l'expéditeur s'appuie sur des données conservées relatives à l'adresse IP du serveur d'expédition pour déterminer l'action éventuelle à appliquer à un message entrant. Un niveau de réputation de l'expéditeur est calculé à partir de diverses caractéristiques de l'expéditeur dérivées de l'analyse du message et de tests externes. Pour plus d'informations, consultez la rubrique [Réputation de l’expéditeur et agent d’analyse de protocole](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

Retour au début

## Agents de blocage du courrier indésirable sur les serveurs de transport Edge

Dans votre organisation, si un serveur de transport Edge est installé dans le réseau de périmètre, tous les agents de blocage du courrier indésirable qui sont disponibles sur un serveur de boîtes aux lettres sont installés et activés par défaut sur le serveur de transport Edge. Toutefois, les agents de blocage du courrier indésirable suivants sont uniquement disponibles sur un serveur de transport Edge :

  - **Agent de filtrage des connexions**   Le filtrage des connexions inspecte l'adresse IP du serveur distant qui tente d'envoyer des messages pour déterminer l'action éventuelle à exécuter sur un message entrant. Le filtrage des connexions utilise une liste d’adresses IP bloquées, une liste d’adresses IP autorisées, des services de fournisseurs de listes d’adresses IP bloquées et des services de fournisseurs de listes d’adresses IP autorisées pour déterminer si l’adresse IP de connexion doit être bloquée ou autorisée. Pour plus d’informations, voir [Filtrage des connexions sur des serveurs de transport Edge](connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

  - **Agent de filtrage des destinataires**   Le filtrage des destinataires compare les destinataires du message figurant sur la commande RCPT TO: SMTP à une liste rouge de destinataires définie par l'administrateur. En cas de correspondance, le message ne peut pas pénétrer dans l'organisation. Le filtre des destinataires compare également les destinataires des messages entrants au répertoire des destinataires local pour déterminer le message est adressé à des destinataires valides. Quand un message n'est pas adressé à des destinataires valides, le message est rejeté. Pour plus d'informations, consultez la rubrique [Filtrage des destinataires sur les serveurs de transport Edge](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Bien que l’agent de filtrage des destinataires soit disponible sur les serveurs de boîtes aux lettres, vous ne devez pas le configurer. Lorsque le filtrage des destinataires sur un serveur de boîte aux lettres détecte un destinataire non valide ou bloqué dans un message qui contient d’autres destinataires valides, le message est rejeté. Si vous installez les agents de filtrage du courrier indésirable sur un serveur de boîte aux lettres, l’agent de filtrage des destinataires est activé par défaut. Cependant, il n’est configuré pour bloquer aucun destinataire.</td>
    </tr>
    </tbody>
    </table>


  - **Agent de filtrage des pièces jointes**   Le filtrage des pièces jointes bloque les messages en fonction du nom du fichier en pièce jointe, de l’extension du nom de fichier, ou du type de contenu MIME du fichier. Vous pouvez configurer un filtrage des pièces jointes pour bloquer un message et ses pièces jointes, pour écarter les pièces jointes et autoriser le passage du message ou supprimer silencieusement le message et ses pièces jointes. Pour plus d’informations, voir [Filtrage des pièces jointes sur les serveurs de transport Edge](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

Sur la base de la valeur de priorité par défaut de l'agent de blocage du courrier indésirable, mais aussi de l'événement SMTP dans le pipeline de transport où l'agent de blocage du courrier indésirable est enregistré, voici l'ordre par défaut dans lequel les agents de blocage du courrier indésirable sont appliqués sur un serveur de transport Edge :

1.  Agent de filtrage des connexions

2.  Agent de filtrage des expéditeurs

3.  Agent de filtrage des destinataires

4.  Agent d'ID de l'expéditeur

5.  Agent de filtrage du contenu

6.  Agent d'analyse de protocole pour la réputation de l'expéditeur

7.  Agent de filtrage des pièces jointes

Retour au début

## Marquages de courrier indésirable

Les marquages de courrier indésirable vous aident à diagnostiquer les problèmes de courrier indésirable en appliquant des métadonnées de diagnostic, ou « marquages », telles que des informations spécifiques à un expéditeur, des résultats de validation du puzzle et des résultats de filtrage du contenu, aux messages à mesure qu'ils sont soumis aux fonctionnalités de blocage du courrier indésirable qui filtrent les messages entrants en provenance d'Internet. Pour plus d'informations, consultez la rubrique [Marquages de courrier indésirable](anti-spam-stamps-exchange-2013-help.md).

Retour au début

## Stratégie anti-courrier indésirable

Votre stratégie de configuration des fonctionnalités de blocage du courrier indésirable et d'établissement de l'agressivité de vos paramètres d'agent de blocage du courrier indésirable requiert une planification et un calcul soigneux. Si vous définissez tous les filtres de blocage du courrier indésirable sur les niveaux les plus agressifs et configurez toutes les fonctions de blocage du courrier indésirable afin de rejeter tous les messages suspects, il y a plus de chances que vous rejetiez également des messages qui ne sont pas du courrier indésirable. En revanche, si vous ne définissez pas les filtres de blocage du courrier indésirable sur un niveau suffisamment agressif et que vous ne définissez pas un seuil de probabilité de courrier indésirable (SCL) suffisamment bas, vous n'observerez probablement pas de réduction de la quantité de courrier indésirable entrant dans votre organisation.

Nous vous recommandons de rejeter un message quand Exchange détecte un message suspect via l'agent de filtrage des connexions, l'agent de filtrage des destinataires ou l'agent de filtrage des expéditeurs. Cette approche est préférable à la mise en quarantaine de tels messages ou à l'affectation de métadonnées, tels des marquages de courrier indésirable, à de tels messages. L'agent de filtrage des connexions et l'agent de filtrage des destinataires bloquent automatiquement les messages identifiés par les filtres concernés. L'agent de filtrage des expéditeurs est configurable.

Cette pratique est recommandée car le seuil de probabilité de courrier indésirable (SCL) en relation avec le filtrage des connexions, le filtrage des destinataires ou le filtrage des expéditeurs, est relativement élevé. Par exemple, avec le filtrage des expéditeurs où l'administrateur a configuré des expéditeurs spécifiques à bloquer, il n'y a aucune raison d'affecter les données de filtrage des expéditeurs à de tels messages et de continuer à les traiter. Dans la plupart des organisations, les messages bloqués doivent être rejetés. (Si vous ne souhaitez pas que les messages soient rejetés, vous ne devez pas les placer dans la liste des expéditeurs bloqués.)

La même logique s'applique aux services de liste rouge en temps réel et au filtrage des destinataires, bien que la confiance sous-jacente ne soit pas aussi élevée que la liste rouge IP. Il faut savoir que plus le message avance dans le chemin du flux des messages, plus la probabilité de faux positifs est élevée du fait que les fonctions de blocage du courrier indésirable évaluent plus de variables. Par conséquent, il se peut que vous constatiez que, lors de la configuration des premières fonctions de blocage du courrier indésirable de façon plus agressive dans la chaîne de blocage du courrier indésirable, vous pouvez réduire le volume de courrier indésirable. Ainsi, vous économiserez les ressources de traitement, de la bande passante et des disques afin de traiter des messages plus ambigus.

En définitive, vous devez prévoir de surveiller l'efficacité globale des fonctions de blocage du courrier indésirable. Moyennant une surveillance étroite, vous pouvez continuer à ajuster les fonctions de blocage du courrier indésirable pour qu'elles fonctionnent bien avec votre environnement. En vertu de cette approche, nous vous recommandons de commencer par tabler sur une configuration plutôt non agressive des fonctions de blocage du courrier indésirable. Cette approche permet de lire le nombre de faux positifs. En surveillant et ajustant les fonctions de blocage du courrier indésirable, vous deviendrez peut-être plus agressif concernant les types de courrier indésirable et d'attaque auxquels votre organisation est confrontée.

Retour au début

## Voir aussi


[Protection contre le courrier indésirable pour Office 365](https://support.office.com/fr-fr/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)

