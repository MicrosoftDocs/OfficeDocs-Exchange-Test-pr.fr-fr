---
title: 'Banque gérée: Exchange 2013 Help'
TOCTitle: Banque gérée
ms:assetid: efdaf80b-335c-491c-8eb5-1fafd297e8a2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn792020(v=EXCHG.150)
ms:contentKeyID: 62607057
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Banque gérée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-07-14_

Toutes les versions antérieures d’Exchange Server, d’Exchange Server 4.0 à Exchange Server 2010, prennent en charge l’exécution d’une seule instance du processus de la banque d’informations (Store.exe) sur le rôle serveur de boîte aux lettres. Cette instance de banque unique héberge toutes les bases de données sur le serveur : actives, passives, retardées et de récupération. Dans les architectures Exchange précédentes, il y avait parfois une isolation minime, voire inexistante, entre les différentes bases de données hébergées sur un serveur de boîtes aux lettres. Un problème avec une seule base de données de boîtes aux lettres peut avoir un impact négatif sur toutes les autres bases de données, et les incidents résultant d’un endommagement de boîte aux lettres peuvent influer sur le service pour tous les utilisateurs dont les bases de données sont hébergées sur ce serveur.

L’autre défi avec une seule instance de banque dans les versions précédentes d’Exchange tient au fait que le moteur de stockage extensible (ESE) s’adapte bien de 8 à 12 cœurs de processeur. Au-delà, cependant, les problèmes de communication entre les processeurs et de synchronisation du cache entraînent un redimensionnement négatif. Étant donné que les serveurs actuels sont beaucoup plus importants, et qu’ils proposent plus de 16 systèmes centraux, cela compliquerait la gestion de l’affinité des 8 à 12 cœurs pour ESE, les autres cœurs servant pour les processus non liés à la banque (par exemple, les assistants, la tâche Rechercher la fondation, la disponibilité gérée, etc.). En outre, l’architecture précédente restreignait la mise à l’échelle pour le processus de banque.

Le processus Store.exe a considérablement évolué au fil des années, tout comme Exchange Server. Toutefois, en tant que processus unique, à terme, son évolutivité est limitée, et il représente un point de défaillance unique. En raison de ces limites, Store.exe a été abandonné dans Exchange 2013 et remplacé par la banque gérée.

## Banque gérée

La banque gérée est le nom des processus de la banque d’informations (c’est-à-dire la banque) dans Exchange Server 2013. Elle utilise un modèle de processus contrôleur/de travail qui permet d’isoler les processus de stockage et d’accélérer le basculement de base de données. La banque gérée comprend également un nouveau mécanisme de mise en cache de base de données statique qui remplace l’algorithme de tampon dynamique dans les versions précédentes d’Exchange Server. Le modèle multi-processus utilisé par la banque gérée compte un seul processus contrôleur de service de banque (dans ce cas, Microsoft.Exchange.Store.Service.exe aka MSExchangeIS) et un seul processus de travail (dans ce cas, Microsoft.Exchange.Store.Worker.exe) pour chaque base de données montée. Lorsqu’une base de données est montée, un nouveau processus de travail desservant uniquement cette base de données est instancié. Lorsqu’une base de données est démontée, le processus de travail de cette base de données est arrêté.

Par exemple, si 40 bases de données sont montées sur un serveur, il y aura 41 processus exécutés pour la banque gérée, un pour chaque base de données et un pour le contrôleur de processus de service de la banque.

Le processus contrôleur de service de banque est très fin et très fiable. Toutefois, s’il est désactivé ou arrêté, l’ensemble de ses processus de travail sont désactivés (ils détectent que le processus contrôleur de service est arrêté et le quittent). Le contrôleur de processus de banque surveille l’intégrité de tous les processus de travail de banque sur le serveur. Une fin forcée ou inattendue du processus Microsoft.Exchange.Store.Service.exe entraîne un basculement immédiat de toutes les copies de base de données actives. La banque gérée est aussi étroitement intégrée au service de réplication Microsoft Exchange (MSExchangeRepl.exe) et à Active Manager. Le processus contrôleur, les processus de travail et le service de réplication sont combinés pour vous fournir une disponibilité et une fiabilité accrues :

  - Processus du service de réplication Microsoft Exchange (MSExchangeRepl.exe)
    
      - Responsable de l’émission des opérations de montage et de démontage dans la banque
    
      - Lance une action de récupération en cas de défaillances de stockage ou de base de données signalées par la banque, le moteur de stockage extensible (ESE) et les répondeurs de disponibilité gérée.
    
      - Détecte les défaillances de base de données inattendues.
    
      - Fournit l’interface d’administration pour les tâches de gestion.

  - Contrôleur/processus de service de banque (Microsoft.Exchange.Store.Service.exe)
    
      - Gère la durée de vie de chaque processus de travail en fonction des opérations de montage et de démontage envoyées par le service de réplication.
    
      - Gère les demandes entrantes émanant du Gestionnaire de contrôle des services Windows.
    
      - Enregistre les éléments en échec lors de la détection de problèmes de processus de travail de banque (par exemple, blocage ou arrêt inattendu).
    
      - Met fin aux processus de travail de banque en cas d’événement de basculement de réponse.

  - Processus de travail de banque (Microsoft.Exchange.Store.Worker.exe)
    
      - Responsable de l’exécution des opérations RPC pour les boîtes aux lettres sur une base de données
    
      - L’instance de point de terminaison RPC au sein du processus de travail est le GUID de la base de données.
    
      - Fournit un cache de base de données.

## Algorithme de mise en cache de base de données statique

L’algorithme de mise en cache de base de données, également connu sous le nom « allocation de mémoire tampon dynamique », qui a été introduit dans Exchange Server 5.5 et qui était également utilisé par la banque d’informations dans Exchange 2000 Server, Exchange Server 2003, Exchange Server 2007 et Exchange Server 2010, a été supprimé d’Exchange 2013. Exchange 2013 utilise un algorithme très simple et direct pour la détermination du cache de base de données. La banque gérée ne réalloue plus dynamiquement le cache entre les bases de données en cas de basculement, ce qui simplifie fortement la gestion du cache interne. À la place, la mémoire allouée pour chaque cache de base de données (par exemple, chaque processus de travail de banque) est calculée en fonction du nombre de copies de base de données locales et de la valeur du paramètre *MaximumActiveDatabases*, si celui-ci est configuré. Si la valeur du paramètre *MaximumActiveDatabases* est supérieure au nombre actuel de copies de base de données, le calcul du cache est basé sur le nombre de copies de base de données.

L’algorithme statique utilisé par Exchange 2013 alloue de la mémoire pour le cache ESE de chaque processus de travail de banque en fonction de la mémoire vive physique. Cela correspond à la *cible de cache maximale* d’une base de données. Le quart de la mémoire totale du serveur est alloué au cache ESE. Cela correspond à la *taille cible de cache de serveur*.

> [!NOTE]
> La taille cible de cache de serveur et, par conséquent, la quantité de mémoire allouée à la banque pour le cache ESE peuvent être remplacées à l’aide de l’attribut <em>msExchESEParamCacheSizeMax</em> de l’objet <em>InformationStore</em> dans Active Directory (la valeur configurée correspond au nombre de pages de 32 Ko à allouer dans tous les processus de banque).


Une quantité statique de ce cache est allouée aux copies actives et passives. La cible de cache maximale sera allouée au processus de travail de banque uniquement lors du traitement d’une copie de base de données active. Les copies de bases de données passives bénéficient de 20 % de la cible de cache maximale. Le reste est conservé par la banque et alloué au processus de travail si la base de données passive devient active.

La cible de cache maximale est calculée uniquement au démarrage de la banque. Par conséquent, si vous ajoutez ou supprimez des bases de données ou des copies de bases de données, vous devez redémarrer le service de contrôleur de banque (MSExchangeIS) afin que le cache puisse être ajusté. Si vous ne redémarrez pas le service, les bases de données récemment créées auront une taille cible de cache inférieure à celle des bases de données créées avant le démarrage du service. Dans ce cas, la somme des tailles cible de cache de base de données dépassera probablement la taille cible de cache du serveur avant le redémarrage de MSExchangeIS.

## Exemples de calculs de cache de base de données

Voici des exemples de calculs de mise en cache de base de données effectués selon la configuration de la mémoire et de la base de données d’un serveur de boîtes aux lettres.

**Exemple 1**

Dans cet exemple, le serveur de boîtes aux lettres possède une mémoire de 48 Go et il héberge deux bases de données actives et deux bases de données passives. Par ailleurs, le paramètre *MaximumActiveDatabases* n’est pas configuré. Dans cette configuration, la quantité de cache de base de données est de 3 Go pour chaque processus de travail de copie de base de données active et de 0,6 Go pour chaque processus de travail de copie de base de données passive. Voici comment ces valeurs ont été obtenues.

Pour obtenir la taille cible de cache de serveur, multipliez la quantité de mémoire par 25 % :

48 Go X 25 % = 12 Go

Pour obtenir la cible de cache maximale de base de données, divisez la taille cible de cache de serveur par le nombre total de bases de données actives et passives :

12 Go/4 bases de données = 3 Go

Pour déterminer la quantité de mémoire utilisée pour les copies de bases de données passives, multipliez la cible de cache maximale de base de données par 20 % :

3 Go X 20 % = 0,6 Go

Sur les 12 Go de mémoire alloués à la taille cible de cache de serveur, 7,2 Go seront utilisés par les processus de travail de base de données, et 4,8 Go seront réservés par la banque d’informations pour les deux copies de bases de données passives, au cas où elles deviendraient des copies actives. Dans ce cas, elles utiliseront leur cible de cache maximale de 3 Go.

**Exemple 2**

Dans cet exemple, le serveur de boîtes aux lettres possède également 48 Go de mémoire et héberge deux bases de données actives et deux bases de données passives. Cependant, le paramètre *MaximumActiveDatabases* est configuré avec une valeur de 2. Dans cette configuration, la quantité de cache de base de données est de 5 Go pour chaque processus de travail de copie de base de données active et de 0,2 Go pour chaque processus de travail de copie de base de données passive. Voici comment ces valeurs ont été obtenues.

Pour obtenir la taille cible de cache de serveur, multipliez la quantité de mémoire par 25 % :

48 Go X 25 % = 12 Go

Pour obtenir la cible de cache maximale de base de données, divisez la taille cible de cache de serveur par le nombre total de bases de données actives, plus le nombre total de bases de données passives multiplié par 20 % :

12 Go/(2A + (2P X 20 %)) = 5 Go

Pour déterminer la quantité de mémoire utilisée pour les copies de bases de données passives, multipliez la cible de cache maximale de base de données par 20 % :

5 Go X 20 % = 1 Go

Sur les 12 Go de mémoire alloués à la taille cible de cache de serveur, la totalité sera utilisée par les processus de travail de base de données, et la banque d’informations ne réservera aucune quantité de mémoire pour les deux copies de bases de données passives, car elles ne peuvent pas devenir des copies actives dans cette configuration (parce que le paramètre *MaximumActiveDatabases* est configuré avec une valeur de 2, et qu’il existe déjà deux copies de bases de données actives sur le serveur).

