---
title: 'Connexion à un srv dans l’Afficheur des files d’attente: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Se connecter à un serveur dans l’Afficheur des files d’attente
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 50478383
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Se connecter à un serveur dans l’Afficheur des files d’attente

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-03_

Lorsque vous utilisez l’Afficheur des files d’attente dans la Boîte à outils Exchange sur un serveur Microsoft Exchange Server 2013 situé dans l’organisation Exchange, vous pouvez vous connecter à d’autres serveurs de boîtes aux lettres. Par défaut, lorsque vous ouvrez l’Afficheur des files d’attente sur un serveur de boîtes aux lettres, l’Afficheur des files d’attente se connecte à la base de données de files d’attente sur le serveur local. Néanmoins, vous pouvez démarrer plusieurs instances de l’Afficheur des files d’attente afin que chaque instance cible un serveur distinct. Vous pouvez aussi afficher les fenêtres de l’Afficheur des files d’attente en mosaïque, afin de pouvoir surveiller facilement plusieurs serveurs de boîtes aux lettres à la fois.

Vous pouvez également indiquer le serveur que le PowerShell distant utilise pour effectuer les tâches spécifiées dans l’Afficheur des files d’attente. Ce serveur ne doit pas nécessairement correspondre au serveur distant que vous gérez dans l’Afficheur des files d’attente.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Files d’attente » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Les procédures décrites dans cette rubrique ne s’appliquent pas aux serveurs de transport Edge. Lorsque vous utilisez l’Afficheur des files d’attente sur un serveur de transport Edge, vous ne pouvez pas modifier le focus de l’outil.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser la Boîte à outils Exchange pour spécifier le serveur que vous souhaitez gérer dans l’Afficheur des files d’attente

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Microsoft Exchange Server 2013** \> **Boîte à outils Exchange**.

2.  Sous **Outils de flux de messagerie**, double-cliquez sur **Afficheur des files d’attente**.

3.  Dans le volet Actions, cliquez sur **Connecter au serveur**.

4.  Dans la fenêtre **Connecter au serveur**, cliquez sur **Parcourir** pour afficher la liste des serveurs de boîtes aux lettres disponibles.

5.  Dans la fenêtre **Sélectionner Exchange Server**, sélectionnez un serveur de boîtes aux lettres. Pour rechercher un serveur de boîtes aux lettres, utilisez l’une des procédures suivantes :
    
      - Dans le champ **Rechercher**, entrez le nom de serveur exact ou les premières lettres du nom de serveur, puis cliquez sur **Rechercher**. Dans le volet Résultats, sélectionnez un serveur.
    
      - Sélectionnez le menu **Affichage**, puis cliquez sur **Afficher le filtre**. Dans la colonne **Nom** ou la colonne **Version**, cliquez sur l’icône de filtre, puis sélectionnez l’opérateur de filtrage. Dans le champ **Entrez le texte ici**, tapez les critères de filtrage. Appuyez sur ENTRÉE. Dans le volet Résultats, sélectionnez un serveur.

6.  Cliquez sur **OK** pour fermer la fenêtre **Sélectionner Exchange Server**.

7.  Après avoir sélectionné un serveur, dans la fenêtre **Connecter au serveur**, activez la case à cocher **Définir comme serveur par défaut** si vous voulez que l’Afficheur des files d’attente se concentre prioritairement sur ce serveur à chaque ouverture.

8.  Dans la fenêtre **Connecter au serveur**, cliquez sur **Connecter**.

## Utiliser la Boîte à outils Exchange pour spécifier le serveur utilisé par l’Afficheur des files d’attente pour exécuter le PowerShell distant

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Microsoft Exchange Server 2013** \> **Boîte à outils Exchange**.

2.  Dans la **section des outils de flux de messagerie**, double-cliquez sur **Afficheur des files d’attente**.

3.  Dans le volet Actions, cliquez sur **Propriétés**.

4.  Dans la boîte de dialogue **Afficheur des files d’attente - \<nom serveur\> Propriétés**, sélectionnez l’une des options suivantes :
    
      - **Se connecter au serveur automatiquement sélectionné**   Sélectionnez cette option pour vous connecter automatiquement au serveur où vous gérez les files d’attente afin d’exécuter le PowerShell distant.
    
      - **Spécifier un serveur auquel se connecter**   Sélectionnez cette option pour spécifier un serveur devant exécuter le PowerShell distant. Si vous choisissez cette option, cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner Exchange Server**. Sélectionnez le serveur où vous souhaitez exécuter le PowerShell distant, puis cliquez sur **OK**.

## Comment savoir si cela a fonctionné ?

Vous devriez être capable de gérer les files d’attente sur le serveur de boîtes aux lettres que vous avez spécifié.

