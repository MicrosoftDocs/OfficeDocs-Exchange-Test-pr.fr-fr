---
title: "Scénario : configuration d'Exchange pour prendre en charge les contrôleurs d'optimisation de réseau étendu: Exchange 2013 Help"
TOCTitle: "Scénario : configuration d'Exchange pour prendre en charge les contrôleurs d'optimisation de réseau étendu"
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 52062945
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Scénario : configuration d'Exchange pour prendre en charge les contrôleurs d'optimisation de réseau étendu

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-09-28_

Dans Microsoft Exchange Server 2013, le chiffrement TLS est obligatoire pour toutes les communications SMTP entre les serveurs de boîtes aux lettres dans le service de transport. Cela augmente la sécurité globale des communications du service de transport entre les serveurs de boîtes aux lettres. Toutefois, dans certaines topologies utilisant des contrôleurs d'optimisation de réseau étendu (WOC), le chiffrement TLS du trafic SMTP peut être indésirable. Dans ce genre de scénario, vous pouvez désactiver le chiffrement TLS pour les communications du service de transport entre serveurs de boîtes aux lettres.

Examinez la topologie présentée dans la figure suivante : Cette topologie comprenant quatre sites suppose que les deux sites du siège et le site de la filiale 2 sont bien connectés, tandis que la connexion entre le site du siège 1 et le site de la filiale 1 passe par un réseau étendu. L'organisation a installé des périphériques WOC sur cette liaison pour compresser et optimiser le trafic sur le réseau étendu.

**Exemple de topologie de réseau avec des périphériques WOC**

![Exemple de topologie avec optimiseurs WAN](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "Exemple de topologie avec optimiseurs WAN")

Cette topologie ne permet pas la compression du trafic SMTP sur le réseau étendu parce que Exchange 2013 utilise le chiffrement TLS pour la communication entre les serveurs de boîtes aux lettres. Dans l'idéal, l'ensemble du trafic SMTP sur le réseau étendu ne doit pas être chiffré, tout en conservant la sécurité TLS au sein des sites bien connectés. Exchange 2013 vous permet de désactiver le chiffrement TLS pour le trafic entre les sites en configurant les connecteurs de réception. En utilisant cette fonctionnalité dans Exchange 2013, vous pouvez configurer une exception pour le trafic SMTP entre le site du siège 1 et le site de la filiale 1, comme indiqué dans la figure suivante.

**Flux de messagerie logique préféré**

![Flux de message logique préféré](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "Flux de message logique préféré")

La configuration recommandée consiste à limiter le trafic SMTP non chiffré uniquement aux messages transitant sur le réseau étendu Par conséquent, la communication intra-site du service de transport entre serveurs de boîtes aux lettres dans tous les sites, et la la communication inter-sites du service de transport entre serveurs de boîtes aux lettres n'impliquant pas la filiale 1 doivent faire l'objet d'un chiffrement TLS.

Pour obtenir ce résultat final, vous devez effectuer les opérations suivantes, dans l'ordre indiqué, sur chaque serveur de boîtes aux lettres dans les sites contenant des périphériques WOC (site du siège 1 et site de la filiale 1 dans l'exemple de topologie) :

1.  Activez l'authentification de serveur Exchange rétrogradée.

2.  Créez un connecteur de réception dédié pour traiter le trafic sur la connexion équipée de périphériques WOC.
    
    1.  Configurez la propriété de plages d'adresses IP distantes du connecteur de réception dédié sur les pages d'adresses IP des serveurs de boîtes aux lettres dans le site Active Directory distant.
    
    2.  Désactivez le chiffrement TLS sur le connecteur de réception dédié.

Vous devez également effectuer les opérations suivantes pour garantir que l'ensemble du trafic STMP sur le réseau étendu est traité par les connecteurs de réception dédiés que vous avez créés :

  - Configurez les sites Active Directory qui participeront à la communication non-TLS comme des sites hub pour forcer la totalité du flux de messagerie à passer par les connecteurs de réception dédiés (site du siège 1 et site de la filiale 1 dans l'exemple de topologie).

  - Vérifiez que les coûts de liaison IP Active Directory sont configurés pour garantir que l'itinéraire de routage le moins coûteux jusqu'à votre site distant (filiale 1 dans l'exemple de topologie) passe par la liaison réseau équipée des périphériques WOC. Attribuez un coût spécifique d'Exchange aux liens de sites Active Directory si nécessaire.

Les sections suivantes fournissent un aperçu de cette procédure. Pour des instructions détaillées sur la configuration de votre organisation dans ce scénario, consultez la rubrique [Désactivation du chiffrement TLS entre des sites Active Directory](disable-tls-between-active-directory-sites-exchange-2013-help.md).

**Contenu de cette rubrique**

Rétrogradation de l'authentification sur les connexions où le chiffrement TLS est désactivé

Création et configuration des connecteurs de réception dédiés

Configuration de sites hub

Configuration des coûts de lien de sites Active Directory spécifiques d'Exchange

## Rétrogradation de l'authentification sur les connexions où le chiffrement TLS est désactivé

L'authentification Kerberos est utilisée avec le chiffrement TLS dans Exchange. Lorsque vous désactivez le chiffrement TLS sur les communications du service de transport entre serveurs de boîtes aux lettres, vous devez effectuer une autre forme d'authentification. Lorsque Exchange 2013 communique avec d'autres serveurs exécutant Exchange  et ne prenant pas en charge le chiffrement **X-ANONYMOUSTLS**, il recourt à une authentification GSSAPI (Generic Security Services Application Programming Interface). Toutes les communications du service de transport entre les serveurs de boîtes aux lettres Exchange 2013 utilisent le chiffrement **X-ANONYMOUSTLS**. Lorsque vous configurez le service de transport sur votre serveur de boîtes aux lettres pour utiliser l'authentification de serveur Exchange rétrogradée, vous activez l'authentification GSSAPI pour les communications du service de transport avec d'autres serveurs de boîtes aux lettres Exchange 2013.

Retour au début

## Création et configuration des connecteurs de réception dédiés

Vous devez créer des connecteurs de réception qui seront les seuls responsables du traitement du trafic non chiffré TLS. L'utilisation de connecteurs de réception séparés dédiés garantit que l'ensemble du trafic ne transitant par le réseau étendu reste protégé par le chiffrement TLS.

Pour limiter les connecteurs de réception dédiés au trafic transitant sur le réseau étendu, vous devez configurer la propriété de plage d'adresses IP distantes. Exchange utilise toujours le connecteur avec la plage d'adresses IP distantes la plus spécifique. Par conséquent, ces nouveaux connecteurs sont préférés au connecteur de réception par défaut configuré pour recevoir des messages de toutes provenances.

En revenant à la l'exemple de topologie, supposons que le sous-réseau de classe C 10.0.1.0/24 soit utilisé pour le site du siège 1, et le sous-réseau 10.0.2.0/24 pour le site de la filiale 1. Pour préparer la désactivation du chiffrement TLS entre ces deux sites, vous devez procéder comme suit :

1.  Créez un connecteur de réception (appelé WAN) sur chaque serveur de boîtes aux lettres dans le site du siège 1 et le site de la filiale 1.

2.  Configurez la plage d'adresses IP distantes 10.0.2.0/24 sur chaque connecteur de réception dédié dans le site du siège 1.

3.  Configurez la plage d'adresses IP distantes 10.0.1.0/24 sur chaque connecteur de réception dédié dans le site de la filiale 1.

4.  Désactivez le chiffrement TLS sur tous les connecteurs de réception dédiés.

Le résultat final est présenté dans la figure suivante (la propriété de plages d'adresses IP distantes des connecteurs de réception nommés « WAN » est affichée entre parenthèses). Un seul serveur de boîtes aux lettres est affiché pour le site de la filiale 1, et celui de la filiale 2 est omis par souci de clarté.

**Configuration de connecteur de réception**

![Configuration des connecteurs de réception](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "Configuration des connecteurs de réception")

Retour au début

## Configuration de sites hub

Par défaut, un serveur de boîtes aux lettres Exchange 2013 tente d'établir une connexion directe avec le serveur de boîtes aux lettres le plus proche de la destination finale d'un message spécifique. Dans l'exemple de topologie, si un utilisateur du site de la filiale 2 envoie un message à un utilisateur du site de la filiale 1, le serveur de boîtes aux lettres du site de la filiale 2 se connecte directement au serveur de boîtes aux lettres du site de la filiale 1 pour remettre ce message. Cette connexion est chiffrée, et donc indésirable dans cette topologie. Pour que ces messages passent par les serveurs de boîtes aux lettres sur le site du siège 1, garantissant ainsi qu'ils ne sont pas chiffrés pendant leur transit sur le réseau étendu, le site du siège 1 et celui de la filiale 1 doivent être configurés comme sites hub. En bref, tout site disposant d'un serveur de boîtes aux lettres avec un connecteur de réception où le chiffrement TLS est désactivé doit être configuré comme site hub pour forcer les serveurs des autres sites à router le trafic via ce site. Pour plus d'informations, consultez la rubrique [Configurer les paramètres de routage de messagerie Exchange dans Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Retour au début

## Configuration des coûts de lien de sites Active Directory spécifiques d'Exchange

Il ne suffit pas de configurer des sites hub pour garantir que l'ensemble du trafic ne soit pas chiffré sur le réseau étendu. En effet, Exchange route les messages via les sites hub uniquement si ces derniers se trouvent sur l'itinéraire de routage le moins coûteux. Supposons que les coûts de liaison IP pour notre exemple de topologie soient configurés dans Active Directory comme illustré dans la figure suivante (le site du siège 2 est omis par souci de clarté).

**Coûts de liaison IP pour l'exemple de topologie**

![Coûts de lien de sites IP pour un exemple de topologie](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "Coûts de lien de sites IP pour un exemple de topologie")

Dans ce cas, l'itinéraire du site de la filiale 2 à celui de la filiale 1 via le site hub représente un coût total de 12 (6+6), tandis que le coût du trajet direct est de 10. Par conséquent, aucun des messages du site de la filiale 2 à celui de la filiale 1 ne passe par le site du siège 1 et l'ensemble de ce trafic reste protégé par le chiffrement TLS.

Pour éviter ce problème, vous devez désigner un coût spécifique d'Exchange qui soit supérieur à 12 pour la liaison IP entre le site de la filiale 2 et celui de la filiale 1, comme illustré dans la figure suivante. Cela garantit que tous les messages passent par le canal non chiffré entre le site du siège 1 et celui de la filiale 1.

**Exemple de topologie configurée avec des coûts de liaison IP spécifiques d'Exchange**

![Exemple de topologie avec coûts Exchange](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "Exemple de topologie avec coûts Exchange")

Pour plus d'informations, consultez la rubrique [Configurer les paramètres de routage de messagerie Exchange dans Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Retour au début

