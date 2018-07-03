---
title: 'Nouveautés de la messagerie unifiée Exchange 2013: Exchange 2013 Help'
TOCTitle: Nouveautés de la messagerie unifiée Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50478939
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Nouveautés de la messagerie unifiée Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans Microsoft Exchange Server 2013, nous améliorons les versions antérieures d'Exchange, en introduisant de nouvelles fonctionnalités et des changements architecturaux. La messagerie unifiée (UM) dans Exchange 2013 comprend les mêmes fonctionnalités que Exchange 2010 et Exchange 2007, cependant la messagerie unifiée n'est plus un rôle de serveur distinct. Il s'agit désormais d'un composant des fonctionnalités liées à la voix offertes dans Exchange 2013.

## Modifications dans l'architecture de voix

L'architecture de Exchange 2013 est différente de ce qu'elle était dans Exchange 2010 et Exchange 2007. Dans les versions précédentes de la messagerie unifiée Exchange, tous les composants de la messagerie unifiée étaient inclus dans un serveur dans le lequel était installé le rôle de serveur de messagerie unifiée. Dans Exchange 2013, tous les composants de messagerie unifiée sont répartis entre un serveur d'accès au client exécutant le service Microsoft Exchange Unified Messaging Call Router et un serveur de boîtes aux lettres exécutant le service Microsoft Exchange Unified Messaging. Toutes les fonctionnalités, y compris les services et les processus de travail pour la messagerie unifiée, sont situées sur chaque serveur de boîte aux lettres, à l'exception du serveur d'accès au client exécutant le service Microsoft Exchange Unified Messaging Call Router, qui proxy les appels entrants vers le serveur de boîtes aux lettres. Pour plus d’informations, consultez la rubrique [Modifications de l’architecture vocale](voice-architecture-changes-exchange-2013-help.md).

## prise en charge du protocole IPv6

Le protocole version 6 (IPv6) est la version la plus récente du protocole Internet. IPv6 est conçu pour corriger un grand nombre d’insuffisances d’IPv4, la précédente version du protocole Internet. Comme dans Exchange 2010, Exchange 2013 Client Access et les serveurs de boîtes aux soutiennent pleinement les réseaux IPv6. Pour plus d’informations, consultez la rubrique [Prise en charge d’IPv6 dans la messagerie unifiée](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Prise en charge pour les API UCMA 4.0

Depuis Service Pack 1 pour Exchange 2010, le rôle de la messagerie unifiée a misé sur Unified Communications Managed API v2.0 (UCMA) pour la signalisation et les médias. Par conséquent, UCMA 2.0 est une condition requise pour la configuration de la messagerie unifiée de Exchange 2010. UCMA 2.0 est téléchargé séparément et déployé manuellement par les administrateurs sur les serveurs de messagerie unifiée exécutant Exchange 2010 SP1 ou une version ultérieure. Pour Exchange 2013, UCMA 4.0 est nécessaire. Toutefois, étant donné que le serveur de messagerie unifiée n'est plus un rôle de serveur distinct Exchange 2013, maintenant l'accès au client et le serveur de boîtes aux lettres qui nécessitent UCMA 4.0.

UCMA 4.0 prend en charge de nouvelles fonctionnalités dans la messagerie unifiée, notamment l'utilisation de la même version du moteur de reconnaissance vocale à la fois pour Conversion de texte par synthèse vocale (TTS) et la reconnaissance vocale (ASR). La plateforme utilisée pour Exchange 2013, .NET 4.0, contient un fichier d'installation unique qui permet la compatibilité descendante avec les serveurs de messagerie unifiée Exchange 2010 et Exchange 2007.

Dans Exchange 2010 SP2 et SP1, l'installation d'UCMA 2.0 est requise avant l'installation du service pack sur un serveur de messagerie unifiée. Cependant, UCMA 2.0 avait plusieurs limites. UCMA 4.0 corrige bon nombre des lacunes. Dans Exchange Server 2013, UM continue d'utiliser UCMA. Toutefois, le passage à la version la plus récente d'UCMA propose les avantages suivants :

  - La plus récente génération d'UCMA intègre les correctifs.

  - UCMA requiert .NET 4.0, qui est de la plate-forme utilisée par Exchange Server 2013. (UCMA 2.0 ne prend en charge .NET 4.0.)

  - UCMA 4.0 prend en charge IPv6.

  - Déploiement simplifié et automatisé de UCMA 4.0. Exchange 2013Le programme d'installation effectue une vérification unique pour UCMA 4.0.

  - L'installation d'UCMA 4.0 comprend tous les composants requis pour Exchange 2013.

> [!NOTE]
> UCMA 4.0 est installé lorsque vous installez Exchange 2013. Pour plus d'informations sur UCMA 4.0 et les conditions d'installation, voir <a href="exchange-2013-prerequisites-exchange-2013-help.md">Conditions préalables pour Exchange 2013</a>. Pour mettre à niveau la version la plus récente d'UCMA, vous devez avant tout désinstaller les versions d'UCMA installées au moyen de l'option Ajouter/supprimer des programmes.


## Améliorations de l'aperçu de messagerie vocale

Certaines améliorations aux services liés à la parole sont offerts pour Exchange Server 2013 UM via Speech Engine 11.0 et UCMA 4.0. Améliorations de génération et de la langue grammaire sont incluses. De plus, Exchange Server 2013 UM comprend plusieurs améliorations à l'interface utilisateur et des améliorations pour la confiance et la précision de l'aperçu de messagerie vocale. Pour plus d’informations, consultez la rubrique [Améliorations d'aperçu de messagerie vocale](voice-mail-preview-enhancements-exchange-2013-help.md).

## Prise en charge de l'ID d'appelant améliorée

Dans les versions précédentes d'Exchange Unified Messaging, un serveur de messagerie unifiée qui a reçu un appel a utilisé l'identification de l'appelant pour essayer de rechercher l'identité de l'appelant. Cette recherche s'est étendue dans Active Directory et aux contacts personnels de l'utilisateur UM stockés dans leur boîte aux lettres.

Les utilisateurs Exchange sont souvent ennuyés par l'incapacité d'identifier Exchange ou les contacts personnels à partir de leur identifiant de l'appelant. Jusqu'à présent, seul le dossier de contacts par défaut dans la messagerie unifiée Exchange a été utilisé pour cette recherche. Mais les utilisateurs Exchange Server 2013 sont susceptibles d'avoir des contacts externes agrégés à partir des réseaux sociaux ou des contacts dans des dossiers spécifiques que les utilisateurs ont créés manuellement. Exchange 2013 prend en charge l'agrégation de contact à partir des réseaux sociaux externes, fournit des renseignements pour lier des contacts multiples se rapportant à la même personne, et utilise ces données pour présenter une vue de la personne (plutôt que le contact). Les contacts qui sont agrégées à partir de réseaux externes sont placés dans des dossiers de contacts ainsi que tous les dossiers de contacts supplémentaires que les utilisateurs créés. Les caractéristiques de la messagerie unifiée Exchange 2013 étendent le champ de la recherche pour inclure d'autres Échange de l'utilisateur et dossiers de contacts personnels qui ont été créés manuellement.

La recherche de l'ID d'appelant est intégrée à l'agrégation de contacts, de sorte que la recherche s'effectue dans les contacts externes. La propriété RéfPersonne, où présent et avec une valeur non nulle, améliore l'expérience utilisateur pour la résolution de l'appelant en supprimant les doubles contacts qui sont associés à la même personne. Puisque la propriété PersonID est la même pour les deux résultats, la messagerie unifiée la traite comme une correspondance à un contact unique.

## Améliorations apportées à la plateforme de reconnaissance vocale et à la reconnaissance vocale

La messagerie unifiée Exchange Server 2013 introduit certaines améliorations à la plateforme de reconnaissance vocale et à la reconnaissance vocale, notamment les suivantes :

  - Améliorations et précision accrue pour l'aperçu de messagerie vocale.

  - Prise en charge de la [Microsoft Speech Platform – Runtime (Version 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Génération de grammaires vocales à l'aide de la boîte aux lettres système pour une organisation.

La messagerie unifiée Exchange utilise des grammaires vocales statiques et dynamiques pour reconnaître les commandes, les noms des contacts dans la liste d'adresses globale, et les noms des contacts personnels dans la boîte aux lettres de l'utilisateur. Aujourd'hui, dans Exchange Server 2013, chaque serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange génère des grammaires pour toutes les langues de messagerie unifiée installées et les stocke dans des répertoires. Chaque serveur de boîte aux lettres stocke toutes les grammaires possibles, qu'il génère à partir du nombre de plans de numérotation, de standards automatiques et de langues de messagerie unifiée installés.

Les fichiers de grammaire sont utilisés comme intrants dans le processus de reconnaissance de la parole et sont générés sur une base périodique. La commande GGG.exe dans Exchange 2007 et Exchange 2010 vous a permis de mettre à jour manuellement les fichiers de grammaire sans attendre la mise à jour planifiée. Dans Exchange Server 2013, pour résoudre les problèmes d'évolutivité ASR de génération de grammaire pour la messagerie unifiée, la génération de grammaire vocale GAL ne se fait plus sur le serveur avec le rôle serveur de messagerie unifiée installé. À la place, cela se produit généralement en utilisant l'Assistant de boîtes aux lettres, sur le serveur de boîtes aux lettres exécutant le service de messagerie unifiée Microsoft Exchange qui héberge la boîte aux lettres d'arbitrage de l'organisation. Le fichier de grammaire vocale GAL est stocké dans la boîte aux lettres d'arbitrage pour une organisation, puis ensuite téléchargé à tous les serveurs de boîtes aux lettres dans cette organisation Exchange. Par défaut, l'Assistant de boîte aux lettres s'exécute toutes les 24 heures. Vous pouvez régler la fréquence en utilisant la cmdlet **Set-MailboxServer**.

## Mises à jour de la cmdlet

Pour Exchange 2013, de nombreuses cmdlets de messagerie unifiée ont été ramenés de Exchange 2010, mais il y a eu des changements dans certains de ces cmdlets et de nouvelles cmdlets ont été ajoutées pour de nouvelles fonctionnalités. Pour plus d’informations, consultez la rubrique [Mises à jour des cmdlets de messagerie unifiée](unified-messaging-cmdlet-updates-exchange-2013-help.md).

