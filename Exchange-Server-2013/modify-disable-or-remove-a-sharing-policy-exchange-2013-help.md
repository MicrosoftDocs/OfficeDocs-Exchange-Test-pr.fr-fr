---
title: 'Modifier, désactiver ou supprimer une stratégie de partage: Exchange 2013 Help'
TOCTitle: Modifier, désactiver ou supprimer une stratégie de partage
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50478424
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier, désactiver ou supprimer une stratégie de partage

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-15_

Les stratégies de partage permettent à des utilisateurs individuels de votre organisation Exchange de partager des informations de disponibilité de calendrier avec d’autres organisations Exchange fédérées, des organisations Exchange non fédérées et des utilisateurs Internet individuels. Au cours des opérations normales, vous pouvez changer des propriétés de stratégie de partage. Vous pouvez par exemple modifier des règles de partage, modifier le niveau d’accès de disponibilité, désactiver temporairement une stratégie de partage ou supprimer intégralement une stratégie de partage.

Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md)

Pour plus d’informations sur la création d’une stratégie de partage, voir [Créer une stratégie de partage](create-a-sharing-policy-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Autorisations de calendrier et de partage » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour modifier une stratégie de partage

1.  Accédez à **organisation** \> **partage**.

2.  Sous **Partage individuel**, sélectionnez une stratégie de partage et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **stratégie de partage**, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans **règle de partage**, modifiez les règles de partage en conséquence. Vous pouvez modifier les paramètres, tels que le domaine avec lequel vous voulez partager des informations et le niveau de partage pour les rendez-vous du calendrier. Lorsque vous avez terminé, cliquez sur **enregistrer** pour fermer la boîte de dialogue **règles de partage**.

5.  Dans **stratégie de partage**, cliquez sur **enregistrer** pour mettre à jour la règle de partage.

## Utiliser le Centre d’administration Exchange (EAC) pour définir une stratégie de partage comme stratégie de partage par défaut

1.  Accédez à **organisation** \> **partage**.

2.  Sous **Partage individuel**, sélectionnez une stratégie de partage et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **stratégie de partage**, cochez la case **Définir cette stratégie comme ma stratégie de partage par défaut**.

4.  Cliquez sur **enregistrer** pour mettre à jour la stratégie de partage.

## Utiliser le Centre d’administration Exchange (EAC) pour désactiver une stratégie de partage

1.  Accédez à **Organisation**\>**Partage**.

2.  Sous **Partage individuel**, sélectionnez une stratégie de partage.

3.  Dans la colonne **Activé**, désactivez la case à cocher correspondant à la stratégie de partage que vous souhaitez désactiver.

## Utiliser le Centre d’administration Exchange (EAC) pour supprimer une stratégie de partage

> [!IMPORTANT]
> Avant de supprimer une stratégie de partage, celle-ci doit être supprimée de toutes les boîtes aux lettres utilisateur.


1.  Accédez à **organisation** \> **partage**.

2.  Sous **Partage individuel**, sélectionnez une stratégie de partage et cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

3.  Dans le message d’avertissement, cliquez sur **oui** pour supprimer la stratégie de partage.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier, désactiver ou supprimer une stratégie de partage

  - Cet exemple modifie la stratégie de partage Contoso pour contoso.com, qui est un domaine extérieur à votre organisation. Cette stratégie permet aux utilisateurs dans le domaine Contoso de voir de simples informations de disponibilité.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'
    ```

  - Cet exemple ajoute un second domaine à la stratégie de partage Contoso. Lorsque vous ajoutez un domaine à une stratégie existante, vous devez inclure tous les domaines précédemment inclus.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'
    ```

  - Cet exemple définit la stratégie de partage Contoso comme stratégie de partage par défaut.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Default $True
    ```

  - Cet exemple désactive la stratégie de partage Contoso.
    
    ```powershell
    Set-SharingPolicy -Identity "Contoso" -Enabled $False
    ```

  - Le premier exemple supprime la stratégie de partage Contoso. Le second exemple supprime la stratégie de partage Contoso et supprime la confirmation de suppression de la stratégie.
    
    
    ```powershell
    Remove-SharingPolicy -Identity Contoso
    ```
    
    ```powershell
    Remove-SharingPolicy -Identity Contoso -Confirm
    ```    

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd297931\(v=exchg.150\)) et [Remove-SharingPolicy](https://technet.microsoft.com/fr-fr/library/dd351071\(v=exchg.150\)).

