---
title: 'Passwords and Security in Outlook for iOS and Android for Exchange Server: Exchange 2013 Help'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70087983
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**Sapplique à :**Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-04-01_

**Résumé** : Cet article explique comment fonctionnent les mots de passe et la sécurité dans Outlook pour iOS et Android avec Exchange Server.

La première fois que vous exécutez l’application Outlook pour iOS et Android dans un environnement local Exchange, Outlook génère une clé AES-128 aléatoire. Cette clé est appelée *clé de périphérique* et est stockée uniquement sur le périphérique de l’utilisateur.

## Création d’un compte et protection des mots de passe

Lorsqu’un utilisateur se connecte à Exchange, le nom d’utilisateur, le mot de passe et une clé de périphérique AES-128 unique sont envoyés du périphérique de l’utilisateur au service Outlook via une connexion TLS, où la clé de périphérique est conservée dans la mémoire de calcul d’exécution. Après avoir vérifié le mot de passe avec le serveur Exchange, le service Outlook utilise la clé de périphérique pour chiffrer le mot de passe, puis le mot de passe chiffré est stocké dans le service. Pendant ce temps, la clé de périphérique est effacée de la mémoire et n’est jamais stockée dans le service d’Outlook (la clé est stockée uniquement sur le périphérique de l’utilisateur).

Ensuite, lorsqu’un utilisateur tente de se connecter à Exchange pour récupérer des données de boîte aux lettres, la clé de périphérique est à nouveau transmise du périphérique au service Outlook via une connexion TLS sécurisée, où elle est utilisée pour déchiffrer le mot de passe dans la mémoire de calcul d’exécution. Une fois déchiffré, le mot de passe n’est jamais stocké dans le service ni écrit sur un disque de stockage local, et la clé de périphérique est à nouveau effacée de la mémoire.

Une fois que le service Outlook a déchiffré le mot de passe lors de l’exécution, le service peut se connecter au serveur Exchange pour synchroniser la messagerie, le calendrier et d’autres données de boîte aux lettres. Tant que l’utilisateur continue à ouvrir et à utiliser Outlook régulièrement, le service Outlook conserve une copie du mot de passe déchiffré de l’utilisateur en mémoire afin de garder la connexion au serveur Exchange active.

## Inactivité de compte et suppression des mots de passe de la mémoire

Au bout de trois jours d’inactivité, le service Outlook efface le mot de passe déchiffré de la mémoire. Une fois que le mot de passe déchiffré est effacé, le service Outlook ne peut plus accéder à la boîte aux lettres de l’utilisateur. Le mot de passe chiffré reste stocké dans le service Outlook, mais vous ne pouvez pas le déchiffrer à nouveau sans la clé de périphérique, qui est disponible uniquement à partir du périphérique de l’utilisateur.

Un compte d’utilisateur peut devenir inactif pour les trois raisons suivantes :

  - L’utilisateur désinstalle Outlook pour iOS et Android.

  - L’utilisateur désactive l’actualisation de l’application en arrière-plan dans les options de paramètres, puis force à quitter Outlook.

  - Aucune connexion Internet n’est disponible sur le périphérique, empêchant Outlook d’effectuer la synchronisation avec Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook ne devient pas inactif uniquement car l’utilisateur n’ouvre pas l’application pendant une certaine période de temps, comme un week-end ou pendant les vacances. Tant que l’actualisation de l’application en arrière-plan est activée (qui est le paramètre par défaut dans Outlook pour iOS et Android), les fonctions telles que les notifications push et la synchronisation en arrière-plan de la messagerie sont considérées comme activité.</td>
</tr>
</tbody>
</table>


**Effacement du mot de passe chiffré et du cache de message à partir du disque dur**

Le service Outlook vide ou supprime les comptes inactifs sur une base hebdomadaire. Une fois qu’un compte d’utilisateur est inactif, le service Outlook vide à la fois le mot de passe chiffré et l’ensemble du contenu de la boîte aux lettres mis en cache.

**Combinaison de sécurité de service et de périphérique**

Les clés de périphérique uniques d’utilisateur ne sont jamais stockées dans le service Outlook et le mot de passe Exchange d’un utilisateur n’est jamais stocké sur le périphérique. Cette architecture signifie que pour pouvoir accéder au mot de passe d’un utilisateur, un groupe malveillant doit disposer d’un accès non autorisé au service Outlook et d’un accès physique au périphérique de cet utilisateur.

En appliquant des stratégies de code confidentiel et un chiffrement sur les périphériques de votre organisation, le groupe malveillant se confronterait également au chiffrement d’un périphérique pour pouvoir accéder à la clé de périphérique. Le tout devant être fait avant que l’utilisateur ne remarque que le périphérique a été compromis et ne demande une réinitialisation à distance du périphérique.

## FAQ sur la sécurité des mots de passe

Vous trouverez ci-dessous les questions fréquemment posées concernant la conception et les paramètres de sécurité d’Outlook pour iOS et Android.

## Les informations d’identification d’utilisateur sont-elles stockées dans le service Outlook si j’empêche Outlook d’accéder à mon instance Exchange Server ?

Si vous avez choisi d’empêcher Outlook pour iOS et Android d’accéder à vos serveurs Exchange locaux, la connexion initiale sera refusée par Exchange. Les informations d’identification de l’utilisateur ne sont pas stockées par le service Outlook, et les informations d’identification présentées dans l’échec de la tentative de connexion sont immédiatement supprimées de la mémoire.

## Comment sont chiffrés le mot de passe clé et la clé de périphérique unique lors de la transition vers le service Outlook ?

Toutes les communications entre l’application Outlook et le service Outlook sont effectuées via une connexion TLS chiffrée. Outlook pour iOS et Android peut se connecter uniquement au service Outlook.

## Comment supprimer du service Outlook les informations d’identification et les informations de boîte aux lettres d’un utilisateur ?

Il existe trois manières de supprimer les informations du service Outlook, comme indiqué ci-dessous :

  - Option 1 : lancer une réinitialisation à distance pour chaque utilisateur ayant utilisé l’application afin de se connecter à Exchange.

  - Option 2 : tous les utilisateurs doivent supprimer Outlook pour iOS et Android. Toutes les données seront supprimées du service Outlook au bout d’une période de 3 à 7 jours.

  - Option 3 : tous les utilisateurs doivent supprimer leurs comptes de l’application Outlook, puis supprimer l’application de leurs périphériques. Dans l’application, demandez aux utilisateurs d’accéder à **Paramètres**, d’appuyer sur **Paramètres du compte**, **Sélectionner un compte**, puis sur **Supprimer le compte**.

## L’application est fermée ou désinstallée, mais elle s’affiche encore comme connectée à mon serveur Exchange. Que se passe-t-il ?

Le service Outlook déchiffre les mots de passe utilisateur dans la mémoire de calcul d’exécution, puis utilise les mots de passe déchiffrés pour se connecter à Exchange. Étant donné que le service Outlook se connecte à Exchange à la place du périphérique afin d’extraire et de mettre en cache les données de la boîte aux lettres, il reste connecté pendant une courte période, jusqu’à ce que le service détecte qu’Outlook ne demande plus de données.

Si un utilisateur désinstalle l’application de son périphérique sans passer d’abord par l’option **Supprimer le compte**, le service Outlook reste connecté à votre serveur Exchange jusqu’à ce que le compte devienne inactif, comme indiqué plus haut dans la section « Inactivité de compte et suppression des mots de passe de la mémoire ». Pour arrêter cette activité, il suffit de suivre l’Option 1 ou l’Option 3 indiquées dans le FAQ ci-dessus, ou de bloquer l’application comme décrit dans [Blocage d’Outlook pour iOS et Android](https://technet.microsoft.com/fr-fr/library/mt759239\(v=exchg.150\)).

## Le mot de passe utilisateur est-il moins sécurisé dans Outlook pour iOS et Android que dans d’autres clients Exchange ActiveSync ?

Non. Les clients EAS enregistrent généralement les informations d’identification de l’utilisateur localement sur le périphérique de l’utilisateur. Cela signifie qu’un périphérique volé ou compromis risque de permettre à un groupe malveillant d’accéder au mot de passe de l’utilisateur. Avec la conception de sécurité d’Outlook pour iOS et Android, un groupe malveillant a besoin de disposer d’un accès non autorisé au service cloud Outlook **et** d’un accès physique au périphérique de l’utilisateur.

## Que se passe-t-il si un utilisateur tente d’utiliser Outlook pour iOS et Android une fois que ses données ont été supprimées du service Outlook ?

Si un compte d’utilisateur devient inactif (par exemple, si l’actualisation de l’application en arrière-plan est désactivée sur le périphérique ou si le périphérique se déconnecte d’Internet pendant un certain temps), l’application Outlook se reconnecte au service Outlook lors du prochain lancement de l’application, et le processus de chiffrement de mot de passe et de mise en cache des messages redémarre. Ce processus est transparent pour l’utilisateur.

## Comment sont sécurisées les données de boîte aux lettres temporairement mises en cache pendant qu’elles sont stockées dans le service d’Outlook ?

Vous pouvez découvrir comment nos données sont protégées dans le [Centre de confiance Azure](https://azure.microsoft.com/support/trust-center/). Comme mentionné précédemment, nous progressions dans Azure et Office 365. La sécurité de ces services est couvert dans [Le centre de confiance Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

