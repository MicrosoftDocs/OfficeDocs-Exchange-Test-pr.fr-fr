---
title: 'Carnets d’adresses en mode hors connexion: Exchange 2013 Help'
TOCTitle: Carnets d’adresses en mode hors connexion
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50478832
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Carnets d’adresses en mode hors connexion

 

_**Sapplique à :** Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-11-16_

Un carnet d’adresses en mode hors connexion est une copie d’un ensemble de listes d’adresses téléchargé pour permettre à un utilisateur de Microsoft Outlook d’accéder au carnet d’adresses, tout en étant déconnecté du serveur. Microsoft Exchange génère de nouveaux fichiers de carnet d’adresses en mode hors connexion, les compresse, puis les place dans un partage local. Vous pouvez déterminer quelles listes d’adresses sont rendues accessibles aux utilisateurs travaillant hors connexion et configurer également la manière dont les carnets d’adresses sont répartis.

Pour en savoir plus sur les listes d'adresses, consultez la rubrique [Listes d’adresses](https://docs.microsoft.com/fr-fr/exchange/address-books/address-lists/address-lists).

> [!IMPORTANT]
> Les données de carnet d'adresses en mode hors connexion dont produites par le service Microsoft Exchange OABGen, qui est un assistant de boîte aux lettres. Si vous utilisez le descripteur de sécurité pour empêcher les utilisateurs d’afficher certains destinataires dans Active Directory, les utilisateurs qui téléchargent le carnet d’adresses en mode hors connexion sont en mesure d’afficher ces destinataires masqués. En conséquence, pour masquer un destinataire dans une liste d’adresse, définissez le paramètre <em>HiddenFromAddressListsEnabled</em> sur les cmdlets <a href="https://technet.microsoft.com/fr-fr/library/aa998596(v=exchg.150)">Set-PublicFolder</a>, <a href="https://technet.microsoft.com/fr-fr/library/aa995950(v=exchg.150)">Set-MailContact</a>, <a href="https://technet.microsoft.com/fr-fr/library/aa995971(v=exchg.150)">Set-MailUser</a>, <a href="https://technet.microsoft.com/fr-fr/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</a>, <a href="https://technet.microsoft.com/fr-fr/library/bb123981(v=exchg.150)">Set-Mailbox</a> et <a href="https://technet.microsoft.com/fr-fr/library/bb124955(v=exchg.150)">Set-DistributionGroup</a>. Vous pouvez également créer un carnet d'adresses en mode hors connexion par défaut ne contenant pas les destinataires masqués. Pour plus d’informations sur l’ajout ou la suppression de listes d’adresses d’un carnet d’adresses en mode hors connexion, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/address-books/offline-address-books/add-or-remove-an-address-list">Ajout ou suppression d'une liste d'adresses à partir d'un carnet d'adresses en mode hors connexion</a>.


Souhaitez-vous rechercher les tâches de gestion relatives au carnet d'adresses en mode hors connexion ? Voir [Procédures des carnets d’adresses en mode hors connexion](https://docs.microsoft.com/fr-fr/exchange/address-books/offline-address-books/offline-address-book-procedures).

**Contenu de cette rubrique**

Déplacement de carnets d'adresses en mode hors connexion entre des versions d'Exchange

OAB version 4 et les clients Outlook

Distribution Web

Considérations relatives aux carnets d’adresses en mode hors connexion

## Déplacement de carnets d'adresses en mode hors connexion entre des versions d'Exchange

Dans Exchange 2007 et Exchange 2010, utilisez la cmdlet **Move-OfflineAddressBook** pour déplacer la génération de carnet d’adresses en mode hors connexion vers un autre serveur de messagerie. Exchange 2013 ne prend en charge que le carnet d’adresses en mode hors connexion (version 4). Il s’agit de la même version de carnet d’adresses en mode hors connexion qui était la valeur par défaut dans Exchange 2010. Vous ne pouvez pas configurer Exchange 2013 pour générer d’autres versions de carnet d’adresses en mode hors connexion et la génération de carnet d’adresses en mode hors connexion intervient sur ​​le serveur de boîtes aux lettres dans lequel réside la boîte aux lettres de l’organisation. En conséquence, pour déplacer la génération de carnet d’adresses en mode hors connexion dans Exchange 2013, vous devez déplacer la boîte aux lettres de l’organisation. Vous ne pouvez déplacer la génération de carnet d'adresses en mode hors connexion vers une autre base de données de boîte aux lettres Exchange 2013. Vous ne pouvez déplacer la génération de carnet d'adresses en mode hors connexion vers une version antérieure d'Exchange. Pour trouver la boîte aux lettres de l’organisation du carnet d’adresses en mode hors connexion Exchange 2013, exécutez la commande suivante de l’environnement de ligne de commande Exchange Management Shell :

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

Vous pouvez ensuite utiliser les cmdlets **MoveRequest** pour déplacer la boîte aux lettres.

## OAB version 4 et les clients Outlook

Exchange 2013 prend en charge uniquement OAB version 4. OAB version 4 a été introduit dans le Exchange 2003 Service Pack 2 (SP2) et est pris en charge par Outlook 2007, Outlook 2010 et Outlook 2013. Ce carnet d'adresses en mode hors connexion Unicode permet aux ordinateurs clients de recevoir des mises à jour différentielles plutôt que des téléchargements de carnet d'adresses en mode hors connexion et une taille de fichier réduite.

## Clients Outlook qui utilisent un carnet d'adresses en mode hors connexion version 4

Pour Outlook 2013, Outlook 2010, Outlook 2007 et les clients qui utilisent un carnet d’adresses en mode hors connexion version 4, si la taille des fichiers « changes.oab » correspond à la moitié (ou plus) de la taille des fichiers de carnet d’adresses en mode hors connexion, Outlook lance un téléchargement complet de carnet d’adresses en mode hors connexion.

## Distribution Web

*La distribution Web* est la méthode de distribution par laquelle les clients Outlook 2013, Outlook 2010, ou Outlook 2007 qui sont en mode hors connexion peuvent accéder au carnet d'adresses en mode hors connexion.

L'utilisation d'une distribution Web offre plusieurs avantages, notamment :

  - Prise en charge simultanée d'un plus grand nombre d'ordinateurs clients.

  - Réduction de l'utilisation de la bande passante.

  - Contrôle accru des points de distribution de carnet d'adresses en mode hors connexion. Avec une distribution Web, le point de distribution est l’adresse Web HTTPS dans laquelle des ordinateurs clients peuvent télécharger le carnet d’adresses en mode hors connexion.

Pour bénéficier au mieux de la distribution Web, les ordinateurs client doivent exécuter Outlook 2013, Outlook 2010 ou Outlook 2007.

Pour fonctionner correctement, la distribution Web dépend des composants suivants :

  - **Processus de génération de carnet d'adresses en mode hors connexion**   Il s'agit du processus par lequel Exchange crée et met à jour le carnet d'adresses en mode hors connexion. Pour créer et mettre à jour le carnet d’adresses en mode hors connexion, le service OABGen s’exécute sur le serveur de boîtes aux lettres ou se trouve la boîte aux lettres de l’organisation. Pour supporter la distribution de carnet d'adresses en mode hors connexion, ce serveur doit être un serveur de boîte aux lettres Exchange.

  - **Distribution de carnets d’adresses en mode hors connexion**   Si un client initie la demande de distribution de carnet d’adresses en mode hors connexion, la demande est dirigée par le biais d’un serveur d’accès au client. Le serveur d’accès au client achemine ensuite la demande au serveur de boîtes aux lettres qui héberge les fichiers de carnet d’adresses en mode hors connexion. Les fichiers de carnet d’adresses en mode hors connexion sont alors distribués directement à partir du serveur de boîtes aux lettres vers le client.

  - **Répertoire virtuel de carnet d'adresses en mode hors connexion**   Le répertoire virtuel de carnet d'adresses en mode hors connexion est le point de distribution utilisé par la méthode de distribution Web. Par défaut, lors de l’installation d’Exchange, un nouveau répertoire virtuel nommé **OAB** est créé dans le site Web interne par défaut des Services Internet (IIS). Si vous avez des utilisateurs côté client qui se connectent à Outlook depuis l’extérieur du pare-feu de votre organisation, vous pouvez ajouter un site Web externe. De la même manière, lorsque vous exécutez la cmdlet **New-OABVirtualDirectory** dans l’environnement de ligne de commande Exchange Management Shell, un répertoire virtuel nommé OAB est créé sur le site Web par défaut des services Internet (IIS) sur le serveur d’accès au client Exchange local. Pour plus d'informations, consultez la rubrique [Créer un répertoire virtuel du carnet d’adresses en mode hors connexion](https://docs.microsoft.com/fr-fr/exchange/address-books/offline-address-books/create-virtual-directory).

  - **Service de découverte automatique**   Cette fonction est disponible dans Outlook 2013, Outlook 2010, Outlook 2007 et sur certains périphériques mobiles qui configurent automatiquement les clients pour l’accès à Exchange. Le service s'exécute sur un serveur d'accès au client et renvoie l'adresse URL de carnet d'adresses en mode hors connexion correcte pour la connexion d'un client spécifique.

## Considérations relatives aux carnets d’adresses en mode hors connexion

Il est recommandé, si vous utilisez un seul ou plusieurs carnets d’adresses en mode hors connexion, que vous considériez les facteurs suivants à mesure que vous planifiez et mettez en œuvre votre stratégie de carnet d’adresses en mode hors connexion :

  - Taille de chaque carnet d'adresses en mode hors connexion dans votre organisation. Pour plus d’informations, consultez la section Considérations relatives à la taille des carnets d’adresses en mode hors connexion plus loin dans cette rubrique.

  - Nombre de téléchargements de carnets d'adresses en mode hors connexion.

  - Nombre et fréquence de changements de nom unique de parent.

  - Incompatibilités d'adresses SMTP.

  - Nombre global de modifications apportées à l'annuaire.

## Considérations relatives à la taille des carnets d’adresses en mode hors connexion

Pour certaines organisations, le Carnet d'adresses en mode hors connexion est un petit fichier que les utilisateurs distants téléchargent occasionnellement. Pour ces organisations, le téléchargement du Carnet d'adresses en mode hors connexion n'est généralement pas une préoccupation. Cependant, pour certaines grandes organisations qui possèdent des répertoires volumineux ou pour des organisations qui ont déployé Outlook 2003 en mode Exchange mis en cache, ceci peut être problématique, notamment si les organisations ont consolidé des serveurs Exchange dans un centre de données régional.

Tailles de carnet d'adresses en mode hors connexion peuvent varier de quelques mégaoctets à quelques centaines de mégaoctets. Les facteurs suivants peuvent affecter la taille du carnet d'adresses en mode hors connexion :

  - L'utilisation de certificats dans une société. Plus il y a de certificats d'infrastructure à clé publique (PKI), plus le Carnet d'adresses en mode hors connexion est volumineux. Certificat PKI de plage de 1 kilo-octet (Ko) à 3 KO. Les certificats constituent le plus grand collaborateur à la taille du carnet d'adresses en mode hors connexion.

  - Nombre de destinataires de messages dans Active Directory.

  - Nombre de groupes de destination dans Active Directory.

  - Les informations qu'une société ajoute à Active Directory pour chacun objet à extension boîte aux lettres ou messagerie. Par exemple certaines organisations remplissent les propriétés d'adresse sur chaque utilisateur, d'autres ne le font pas.

