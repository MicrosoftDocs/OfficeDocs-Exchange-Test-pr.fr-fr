---
title: 'Afficheur des files d’attente: Exchange 2013 Help'
TOCTitle: Afficheur des files d’attente
ms:assetid: db892f88-5c13-4607-a38c-8845b35ab8b2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124789(v=EXCHG.150)
ms:contentKeyID: 50479367
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Afficheur des files d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-09-25_

L’Afficheur des files d’attente est un composant logiciel enfichable Microsoft Management Console qui est installé sur un serveur de boîtes aux lettres ou le serveur de transport Edge. Il se trouve dans la section **Outils de flux de messagerie** de la console Boîte à outils Exchange. Cet outil vous permet d'afficher des informations concernant les files d'attente sur un serveur de transport et les messages se trouvant dans ces files d'attente. En outre, il vous permet d'effectuer des actions de gestion sur les files d'attente et les éléments de courrier. L'Afficheur des files d'attente est utile pour résoudre les problèmes de flux de messagerie et identifier le courrier indésirable.

Lorsque vous utilisez l'Afficheur des files d'attente pour gérer les files d'attente, tenez compte de ce qui suit :

  - Vous devez vous connecter à un serveur de transport. Par défaut, l’Afficheur des files d’attente ouvre la base de données de file d’attente sur le serveur où vous l’avez activé. Cependant, vous pouvez également vous connecter à d’autres serveurs. Pour plus d’informations, consultez la rubrique [Se connecter à un serveur dans l’Afficheur des files d’attente](connect-to-a-server-in-queue-viewer-exchange-2013-help.md).

  - La liste des files d'attente et des messages peut être volumineuse, selon le flux de messagerie, et sa taille varie à mesure que des messages se présentent sur le serveur et le quittent. Vous pouvez configurer les options de l'Afficheur des files d'attente pour déterminer la fréquence à laquelle la liste des files d'attente et des messages est actualisée et le nombre d'éléments affichés sur chaque page. Pour plus d’informations, consultez la rubrique [Définir les options de l’Afficheur des files d’attente](set-queue-viewer-options-exchange-2013-help.md).

  - Vous pouvez créer un filtre pour afficher le jeu de files d'attente ou de messages spécifique que vous voulez surveiller. Après avoir localisé les files d'attente et les messages à surveiller, vous pouvez afficher les informations de propriété relatives à ces files d'attente et ces messages. Ces informations sont utiles lorsque vous recherchez la cause des problèmes de flux de messagerie. Pour plus d’informations, consultez les rubriques [Filtres de file d’attente](queue-filters-exchange-2013-help.md) et [Filtres de messages](message-filters-exchange-2013-help.md).

  - Utilisez le lien **Exporter la liste** dans le volet Actions pour exporter la liste des files d'attente ou une liste des messages. Pour plus d'informations, voir [Exporter des listes à partir de l’Afficheur des files d’attente](export-lists-from-queue-viewer-exchange-2013-help.md).

