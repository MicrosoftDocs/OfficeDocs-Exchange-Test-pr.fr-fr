---
title: 'Considérations sur le déploiement de dossiers publics: Exchange 2013 Help'
TOCTitle: Considérations relatives au déploiement de dossiers publics
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 64996428
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Considérations relatives au déploiement de dossiers publics

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-07-12_

Bien que l’utilisation de dossiers publics Exchange 2013 présente de nombreux avantages, il convient de prendre certains éléments en considération avant de les implémenter au sein de votre organisation.

## Considérations relatives au déploiement pour les dossiers publics

Cet article contient des facteurs à prendre en compte avant de déployer des dossiers publics dans votre organisation, notamment si vous envisagez d’avoir un grand nombre de dossiers publics. Exchange 2013 prend désormais en charge jusqu’à un million de dossiers publics.

  - L’activité au sein d’un dossier public influe directement sur la charge qui est placée sur la boîte aux lettres de dossiers publics dans laquelle se trouve le dossier. Pour éviter les problèmes de connectivité des clients, tels que la latence élevée ou l’impossibilité d’accéder à un dossier public, nous vous recommandons de procéder comme suit :
    
      - Les boîtes aux lettres de dossiers publics ne doivent pas dépasser 50 % de la limite de taille de la boîte aux lettres. Si cette limite est dépassée, envisagez d’utiliser le script `Split-PublicFolderMailbox.ps1` situé dans le dossier C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts sur le serveur Exchange 2013 pour déplacer des dossiers publics vers une nouvelle boîte aux lettres de dossiers publics.
    
      - Envisagez de déplacer les dossiers publics très utilisés vers une boîte aux lettres de dossiers publics dédiée.
    
      - Déplacez les dossiers publics très utilisés hors de la hiérarchie de dossiers publics de service. Vous pouvez effectuer cette action en définissant la propriété *IsExcludedFromServingHierarchy* sur la boîte aux lettres de dossiers publics à l’aide de la cmdlet **Set-Mailbox**.
    
      - Pour les grandes organisations disposant de nombreux dossiers publics, envisagez d’ajouter des boîtes aux lettres de dossiers publics supplémentaires pour répartir la charge des demandes de la hiérarchie de dossiers publics de service.

  - Placez la boîte aux lettres de dossiers publics principale dans un DAG pour améliorer la disponibilité de la boîte aux lettres. La boîte aux lettres de dossiers publics principale est l’exemplaire de la hiérarchie de dossiers publics faisant autorité.

  - Placez les boîtes aux lettres de dossiers publics secondaires dans un DAG ou sauvegardez régulièrement les boîtes aux lettres.

  - Placez les boîtes aux lettres de dossiers publics à l’emplacement le plus proche géographiquement des utilisateurs qui devront accéder au contenu du dossier public.

  - Réduisez les temps d’accès à la hiérarchie de dossiers publics en utilisant la propriété DefaultPublicFolderMailbox sur les boîtes aux lettres des utilisateurs pour spécifier une boîte aux lettres de dossiers publics située près d’eux. Ainsi, les utilisateurs n’auront pas à récupérer la hiérarchie de dossiers publics à partir d’une boîte aux lettres de dossiers publics située à d’autres emplacements géographiques.

  - Pour les déploiements de plus de 50 boîtes aux lettres secondaires de dossiers publics, nous vous recommandons de ne pas stocker le contenu du dossier public dans la boîte aux lettres principale de dossiers publics. Ainsi, la boîte aux lettres principale de dossiers publics est consacrée à la synchronisation de la hiérarchie avec les boîtes aux lettres secondaires de dossiers publics.

  - Exchange 2013 ne prend plus en charge les boîtes aux lettres de dossiers publics. Par conséquent, les utilisateurs d’Outlook Web App ayant des boîtes aux lettres Exchange 2013 ne seront pas en mesure d’accéder aux dossiers publics Exchange 2010 ou Exchange 2007. Les utilisateurs Exchange 2013 peuvent accéder aux dossiers publics Exchange 2010 ou Exchange 2007 avec Outlook ou Outlook pour Mac.

  - Outlook Web App est pris en charge, mais dans certaines limites. Vous pouvez ajouter et supprimer des dossiers publics favoris, ainsi qu’effectuer des opérations au niveau élément, telles que la création, la modification et la suppression de publications, et la réponse à des publications. En revanche, vous ne pouvez pas créer ni supprimer des dossiers publics dans Outlook Web App. De même, seuls des dossiers publics de messagerie, de publications, de calendriers et de contacts peuvent être ajoutés à la liste des favoris dans Outlook Web App.

  - Si la recherche en texte intégral de contenu de dossier public est disponible, il n’est pas possible de rechercher dans le contenu de plusieurs dossiers publics, et le contenu n’est pas indexé par Exchange Search.

  - Pour accéder à des dossiers publics sur des serveurs Exchange 2013, vous devez utiliser Outlook 2007 ou une version ultérieure.

  - Les stratégies de rétention ne sont pas prises en charge pour les boîtes aux lettres de dossiers publics.

