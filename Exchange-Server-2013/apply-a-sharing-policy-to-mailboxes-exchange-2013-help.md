---
title: 'Appliquer une stratégie de partage aux boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Appliquer une stratégie de partage aux boîtes aux lettres
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50479348
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Appliquer une stratégie de partage aux boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-15_

Les stratégies de partage font partie intégrante du partage fédéré et permettent un partage établi par utilisateur, de personne à personne des informations de calendrier avec différents types d’utilisateurs externes. La stratégie de partage qu’un administrateur applique à la boîte aux lettres de l’utilisateur détermine le niveau d’accès que l’utilisateur peut partager et avec qui il peut le partager. Si vous ne changez rien, la stratégie de partage par défaut s’applique à tous les utilisateurs. Si vous créez une stratégie de partage, vous devez l’appliquer aux boîtes aux lettres pour qu’elle prenne effet. Une stratégie de partage peut être appliquée à une boîte aux lettres utilisateur spécifique ou à plusieurs boîtes aux lettres utilisateur simultanément. Un administrateur peut également désactiver une stratégie de partage d’un utilisateur pour empêcher l’accès externe aux calendriers.

Pour en savoir plus sur le partage fédéré, voir [Partage](sharing-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez*Recipient Provisioning Permissions* Entrée dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Une stratégie de partage doit exister. Pour plus d’informations, consultez la rubrique [Créer une stratégie de partage](create-a-sharing-policy-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utilisation du Centre d’administration Exchange pour appliquer une stratégie de partage à une seule boîte aux lettres

1.  Accédez à **destinataires** \> **boîtes aux lettres**.

2.  Dans la liste affichée, sélectionnez la boîte aux lettres souhaitée, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans **Boîte aux lettres de l’utilisateur**, cliquez sur **fonctionnalités de boîte aux lettres**.

4.  Dans la liste **Stratégie de partage**, sélectionnez la stratégie de partage que vous souhaitez appliquer à cette boîte aux lettres.

5.  Cliquez sur **enregistrer** pour appliquer la stratégie de partage.

## Utilisation du Centre d’administration Exchange pour appliquer une stratégie de partage à plusieurs boîtes aux lettres

1.  Accédez à **destinataires** \> **boîtes aux lettres**.

2.  Dans la vue Liste, maintenez la touche Ctrl enfoncée pour sélectionner plusieurs boîtes aux lettres.

3.  Dans le volet Détails, les propriétés de la boîte aux lettres sont configurées pour une modification en bloc. Cliquez sur **Autres options**.

4.  Sous **Stratégie de partage**, cliquez sur **Mettre à jour**.

5.  Dans **attribuer en bloc la stratégie de partage**, utilisez la liste **Sélectionner la stratégie de partage** pour sélectionner une stratégie de partage à affecter aux boîtes aux lettres.

6.  Cliquez sur **enregistrer** pour appliquer la stratégie de partage aux boîtes aux lettres sélectionnées.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour appliquer une stratégie de partage à une ou plusieurs boîtes aux lettres

Cet exemple applique la stratégie de partage Contoso à une boîte aux lettres unique pour l’utilisateur Barbara.

```powershell
Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"
```

Cet exemple indique que toutes les boîtes aux lettres utilisateur du service Marketing utilisent la stratégie de partage Contoso Marketing.

```powershell
Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"
```

Cet exemple renvoie toutes les boîtes aux lettres à laquelle la stratégie de partage Contoso est appliquée, et trie les utilisateurs dans un tableau qui affiche uniquement leur alias et leurs adresses de messagerie.

```powershell
Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses
```

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) et [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien appliqué la stratégie de partage à une boîte aux lettres utilisateur, effectuez l’une des opérations suivantes :

  - Dans le Centre d’administration Exchange, accédez à **Destinataires**\>**Boîtes aux lettres**, puis sélectionnez la boîte aux lettres à laquelle vous avez appliqué la stratégie de partage. Cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier"), cliquez sur **fonctionnalités de boîte aux lettres**, puis vérifiez que la stratégie de partage appropriée apparaît dans la liste **Stratégie de partage**.

  - Exécutez la commande suivante de l’environnement de ligne de commande Exchange Management Shell pour vérifier que la stratégie de partage a été affectée à une boîte aux lettres utilisateur. Vérifiez que la stratégie de partage appropriée est répertoriée dans le paramètre *SharingPolicy*.
    
    ```powershell
    Get-Mailbox <user name> | format-list
    ```

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

