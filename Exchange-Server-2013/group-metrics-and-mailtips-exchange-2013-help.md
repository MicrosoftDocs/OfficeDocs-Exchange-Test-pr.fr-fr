---
title: 'Mesures de groupe et les infos-courrier: Exchange 2013 Help'
TOCTitle: Mesures de groupe et les infos-courrier
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50478466
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mesures de groupe et les infos-courrier

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Les données suivantes sur les groupes de distribution et les groupes de distribution dynamique de votre organisation constituent les mesures de groupe :

  - Nombre de membres

  - Nombre de membres qui sont externes à votre organisation

Les données de mesures de groupe sont utilisées pour prendre en charge les infos-courrier dans Microsoft Exchange Server 2013. Les infos-courrier sont des messages informatifs que les expéditeurs visualisent pendant qu’ils rédigent leurs messages. Pour plus d’informations sur les infos-courrier, notamment la liste complète des infos-courrier disponibles dans Exchange 2013, voir [MailTips](https://docs.microsoft.com/fr-fr/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips).

Les données de mesures de groupe sont utilisées par les infos-courrier suivantes :

  - **Large public**   Cette info-courrier s’affiche lorsqu’un expéditeur ajoute un groupe de distribution dont le nombre de membres est considéré comme un large public, tel que cela est configuré dans votre organisation. Par défaut, tout message adressé à plus de 25 destinataires est considéré comme message destiné à un large public.

  - **Destinataires externes**   Cette info-courrier s’affiche lorsqu’un expéditeur ajoute un groupe de distribution dont les membres sont externes à votre organisation.

Les infos-courrier sont évaluées à chaque fois qu’un expéditeur ajoute un destinataire à un message. Pour fournir ces informations, Exchange calcule les données de mesures de groupe dans un processus d’arrière-plan pouvant être programmé pour s’exécuter en dehors des heures d’ouverture normales de votre organisation. Lors de l’évaluation des destinataires pour les infos-courrier, Exchange lit les données de mesures de groupe.

## Génération de mesures de groupe

Dans Exchange 2013, les données de mesures de groupe sont stockées dans les attributs **msExchGroupMemberCount** et **msExchGroupExternalMemberCount** sur l’objet de groupe d’Active Directory. Les fichiers suivants, contenus dans le dossier %ExchangeInstallPath%GroupMetrics, sont également associés à des mesures de groupe :

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   Ce fichier texte contient des informations sur le serveur de boîtes aux lettres qui est configuré pour générer des données de mesures de groupe, ainsi que l’heure de la dernière génération de mesures de groupe ayant abouti. Cela permet aux mesures de groupe de générer des données pour les groupes qui ont été modifiés depuis la dernière génération de mesures de groupe.

  - **ChangedGroups.txt**   Ce fichier contient la liste des groupes qui ont été mis à jour la dernière fois que les données de mesures de groupe ont été générées.

La génération de mesures de groupe est réalisée par une boîte aux lettres d’arbitrage, également appelée boîte aux lettres d’organisation. Lorsque le paramètre *GMGen* d’une boîte aux lettres d’arbitrage est défini sur `$true`, la boîte aux lettres d’arbitrage est responsable de la génération des données de mesures de groupe.

Le serveur de boîtes aux lettres génère des données de mesures de groupe complètes pour tous les groupes de distribution et groupes de distribution dynamique lors de la première exécution de l’assistant de boîte aux lettres Mesures de groupe, ainsi que des mises à jour incrémentielles pour les groupes qui ont été modifiés depuis la dernière génération complète. Par défaut, les données de mesures de groupe sont générées quotidiennement à l’heure aléatoire à laquelle la charge de travail du serveur Exchange est faible. Si la charge de travail est constamment élevée, la génération de mesures de groupe ne sera pas effectuée.

Pour configurer la génération de mesures de groupe, voir [Configuration des mesures de groupe](configure-group-metrics-exchange-2013-help.md).

