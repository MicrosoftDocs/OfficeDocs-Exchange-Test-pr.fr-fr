---
title: 'Nouvelles fonctionnalités de messagerie vocale: Exchange 2013 Help'
TOCTitle: Nouvelles fonctionnalités de messagerie vocale
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 50478637
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nouvelles fonctionnalités de messagerie vocale

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

La messagerie unifiée dans Microsoft Exchange Server 2013 inclut le même ensemble de fonctionnalités que dans Microsoft Exchange 2010 et Microsoft Exchange 2007, avec cependant quelques améliorations et modifications architecturales. Notez que la messagerie unifiée n’est plus un rôle serveur distinct. Il s'agit désormais d'un composant des fonctionnalités liées à la voix offertes dans Exchange 2013.

## Modifications dans l'architecture de voix

L’architecture voix de Microsoft Exchange 2013 est différente de celle de Microsoft Exchange 2010 et de Microsoft Exchange 2007. Dans les versions précédentes de la messagerie unifiée Exchange, tous les composants de la messagerie unifiée étaient inclus dans un serveur dans le lequel était installé le rôle de serveur de messagerie unifiée. Dans Exchange 2013, les composants de la messagerie unifiée sont partagés entre un serveur d’accès au client qui exécute le service Routeur d’appel de messagerie unifiée Microsoft Exchange et un serveur de boîtes aux lettres qui exécute un service de messagerie unifiée Microsoft Exchange. La plupart des fonctionnalités, notamment les services et processus de travail associés à la messagerie unifiée, se trouvent sur chacun des serveurs de boîtes aux lettres. Le serveur d’accès au client qui exécute le service Routeur d’appel de messagerie unifiée Microsoft Exchange, redirige via un proxy des appels entrants pour le serveur de boîtes aux lettres. Pour plus d’informations, consultez la rubrique [Modifications de l’architecture vocale](voice-architecture-changes-exchange-2013-help.md).

## prise en charge du protocole IPv6

Le protocole IPv6 (Internet Protocol Version 6) est la version la plus récente du protocole Internet (IP). IPv6 est conçu pour corriger un grand nombre d’insuffisances d’IPv4, la précédente version du protocole Internet. A l'instar de Microsoft Exchange 2010, les serveurs d’accès au client et de boîtes aux lettres de Microsoft Exchange 2013 sont entièrement compatibles avec les réseaux IPv6. Pour plus d’informations, consultez la rubrique [Prise en charge d’IPv6 dans la messagerie unifiée](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Prise en charge pour les API UCMA 4.0

A partir de Microsoft Exchange 2010 Service Pack 1 (SP1), le rôle de messagerie unifiée s’est reposé sur Unified Communications Managed API v2.0 (UCMA) pour la signalisation et le support. En conséquence, UCMA 2.0 était un prérequis pour la configuration de la messagerie unifiée de Microsoft Exchange 2010. Les administrateurs peuvent télécharger UCMA 2.0 séparément et le déployer manuellement sur des serveurs de messagerie unifiée qui exécutent Microsoft Exchange 2010 SP1 ou une version ultérieure.

Notez cependant que UCMA 2.0 présente plusieurs limitations. Nombre de ces insuffisances sont corrigées par UCMA 4.0, qui est obligatoire pour Microsoft Exchange 2013. Puisque le serveur de messagerie unifiée n’est plus un rôle serveur distinct, ce sont maintenant les serveurs d’accès au client et de boîtes aux lettres qui nécessitent UCMA 4.0.

UCMA 4.0 prend en charge de nouvelles fonctionnalités dans la messagerie unifiée, notamment l'utilisation de la même version du moteur de reconnaissance vocale à la fois pour Conversion de texte par synthèse vocale (TTS) et la reconnaissance vocale (ASR). La plateforme utilisée pour Exchange 2013, .NET 4.0, contient un fichier d'installation unique qui permet la compatibilité descendante avec les serveurs de messagerie unifiée Exchange 2010 et Exchange 2007.

Dans Exchange 2010 SP2 et SP1, l'installation d'UCMA 2.0 est requise avant l'installation du service pack sur un serveur de messagerie unifiée.

L'utilisation d’UCMA 4.0 offre plusieurs avantages :

  - Il intègre des correctifs.

  - Il prend en charge IPv6.

  - Le déploiement d’UCMA 4.0 a été automatisé et simplifié.

  - L'installation d'UCMA 4.0 comprend tous les composants requis pour Exchange 2013.

  - UCMA 4.0 autorise des traductions plus précises grâce au moteur de reconnaissance vocale et une prise en charge plus évolutive de la plate-forme vocale sur de nombreux produits.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UCMA 4.0 est installé lorsque vous installez Exchange 2013. Pour plus d'informations sur UCMA 4.0 et les conditions d'installation, voir <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>. Pour mettre à niveau la version la plus récente d'UCMA, vous devez avant tout désinstaller les versions d'UCMA installées au moyen de l'option Ajouter/supprimer des programmes.</td>
</tr>
</tbody>
</table>


## Améliorations de l'aperçu de messagerie vocale

Certaines améliorations destinées aux services associés à la reconnaissance vocale ont été incluses dans la messagerie unifiée de Microsoft Exchange Server 2013 via le moteur de reconnaissance vocale Speech Engine 11.0 et UCMA 4.0. Des améliorations ont été apportées en matière de génération de grammaire, de services vocaux principaux et de prise en charge de plusieurs langues. La messagerie unifiée Microsoft Exchange Server 2013 inclut également plusieurs améliorations qui concernent les services de transcription fournis aux utilisateurs finaux et qui accroissent la confiance et la précision de l’aperçu de messagerie vocale. Pour plus d’informations, consultez la rubrique [Améliorations d'aperçu de messagerie vocale](voice-mail-preview-enhancements-exchange-2013-help.md).

## Prise en charge de l'ID d'appelant améliorée

Dans les versions précédentes de la messagerie unifiée d’Exchange, un serveur de messagerie unifiée qui recevait un appel utilisait l’ID d’appelant pour rechercher l'identité eventuelle de l’appelant. Cette recherche s’étendait à Active Directory et aux contacts personnels de l’utilisateur de la messagerie unifiée enregistrés dans sa boîte aux lettres.

Par le passé, les utilisateurs se sentaient parfois frustrés parce que le système de messagerie vocale n’arrivait pas à identifier des contacts Exchange ou personnels à partir de leur ID d’appelant. Jusqu’à présent, la recherche se limitait au seul dossier des contacts par défaut de la boîte aux lettres Exchange de l’utilisateur. En revanche, des utilisateurs de Microsoft Exchange Server 2013 doivent probablement disposer de contacts agrégés issus de réseaux sociaux ou de contacts externes qu’ils ont ajoutés à des dossiers uniques lors de l’organisation de leurs contacts. Dans Microsoft Exchange 2013, la messagerie unifiée étend la portée de la recherche pour inclure les autres dossiers de contacts Exchange et personnels de l’utilisateur qui ont été créés manuellement. Exchange 2013 prend en charge également l’agrégation des contacts issus de réseaux sociaux externes, offre l’intelligence de pouvoir relier plusieurs contacts qui se réfèrent à la même personne et utilise ces données pour présenter des vues centrées sur les personnes et non sur des contacts. En d’autres termes, des contacts qui ont été agrégés à partir de réseaux sociaux externes peuvent être placés dans le dossier des contacts enregistré dans la boîte aux lettres de l’utilisateur dans Outlook Web App et Outlook. Ces contacts peuvent maintenant être également ajoutés dans des dossiers de contacts supplémentaires créés par l’utilisateur.

La recherche de l'ID d'appelant est intégrée à l'agrégation de contacts, de sorte que la recherche s'effectue dans les contacts externes. La propriété **PersonID**, présente et définie à une valeur autre que Null, améliore l’expérience utilisateur pour la résolution de l’ID d’appelant en supprimant des correspondances en double dans les contacts associés à la même personne. Puisque la propriété PersonID est la même pour les deux résultats, la messagerie unifiée la traite comme une correspondance à un contact unique.

## Améliorations apportées à la plateforme de reconnaissance vocale et à la reconnaissance vocale

La messagerie unifiée Exchange Server 2013 introduit certaines améliorations à la plateforme de reconnaissance vocale et à la reconnaissance vocale, notamment les suivantes :

  - Améliorations et précision accrue pour l'aperçu de messagerie vocale.

  - Prise en charge pour la [plateforme de reconnaissance vocale de Microsoft – Runtime (Version 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Génération de grammaires vocales à l'aide de la boîte aux lettres système pour une organisation.

La messagerie unifiée d’Exchange utilise des grammaires dynamiques de reconnaissance vocale pour identifier des commandes, des noms de contacts figurant dans la liste d’adresses globale (LAG) et des noms de contacts personnels de la boîte aux lettres de l'utilisateur. Aujourd'hui, dans Exchange Server 2013, chaque serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange génère des grammaires pour toutes les langues de messagerie unifiée installées et les stocke dans des répertoires. Chaque serveur de boîte aux lettres stocke toutes les grammaires possibles, qu'il génère à partir du nombre de plans de numérotation, de standards automatiques et de langues de messagerie unifiée installés.

La messagerie unifiée utilise les fichiers de grammaire pour permettre à des appelants d’utiliser la reconnaissance vocale pour rechercher des utilisateurs au sein de votre organisation. L’Assistant de boîte aux lettres met à jour les fichiers toutes les 24 heures. La commande GGG.exe de Microsoft Exchange 2007 et Microsoft Exchange 2010 permet de mettre à jour manuellement les fichiers de grammaire sans attendre la mise à jour planifiée. Dans Microsoft Exchange Server 2013, pour résoudre des problèmes d’évolutivité de génération de la grammaire de reconnaissance vocale (ASR) relatifs à la messagerie unifiée, la génération de grammaire vocale dans la liste d’adresses globales (LAG) ne s’effectue plus sur le serveur ayant le rôle serveur de messagerie unifiée installé. À la place, cela se produit généralement en utilisant l'Assistant de boîtes aux lettres, sur le serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange qui héberge la boîte aux lettres d'arbitrage de l'organisation. Le fichier de grammaire vocale est enregistré dans la boîte aux lettres d’arbitrage pour une organisation et téléchargé ensuite sur tous les serveurs de boîtes aux lettres de l’organisation Exchange. Par défaut, l'Assistant de boîte aux lettres s'exécute toutes les 24 heures. Vous pouvez régler la fréquence en utilisant la cmdlet **Set-MailboxServer**.

## Mises à jour de la cmdlet

Pour Microsoft Exchange 2013, plusieurs cmdlets de messagerie unifiée ont été récupérés dans Microsoft Exchange 2010. Notez cependant que certains de ces cmdlets ont subi quelques changements, et que de nouveaux cmdlets ont été ajoutés pour de nouvelles fonctionnalités. Pour plus d’informations, consultez la rubrique [Mises à jour des cmdlets de messagerie unifiée](unified-messaging-cmdlet-updates-exchange-2013-help.md).

