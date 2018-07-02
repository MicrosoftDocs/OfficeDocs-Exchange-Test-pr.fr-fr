---
title: "Modification d'une stratégie d'adresse de messagerie: Exchange 2013 Help"
TOCTitle: Modification d'une stratégie d'adresse de messagerie
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50479250
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: HT
---

# Modification d'une stratégie d'adresse de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-12-10_

Les stratégies d'adresse de messagerie génèrent des adresses de messagerie principales et secondaires pour vos destinataires (utilisateurs, contacts et groupes), afin qu'ils puissent recevoir et envoyer des messages.

Pour d'autres tâches de gestion relatives aux stratégies d'adresse de messagerie, consultez la rubrique [Procédures des stratégies d'adresse de messagerie](email-address-policy-procedures-exchange-2013-help.md).

## Que devez-vous savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour modifier une stratégie d'adresse de messagerie si cette stratégie a été créée à l'aide de l'environnement de ligne de commande Exchange Management Shell.

  - Si la stratégie d'adresse de messagerie a été créée à l'aide d'un filtre de destinataires, vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour la modifier. Pour plus d'informations, consultez la rubrique [Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies d'adresse de messagerie » dans la rubrique [Adresses de messagerie et carnets d’adresses](email-addresses-and-address-books-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le CAE pour modifier les destinataires auxquels la stratégie s'applique

1.  Accédez à **Flux de messagerie** \> **Stratégies d'adresse de messagerie**.

2.  Dans l'affichage Liste, sélectionnez la stratégie d'adresse de messagerie à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  
    
    Dans **Stratégie d'adresse de messagerie**, cliquez sur **Appliquer à** et modifiez les paramètres.

## Utiliser le CAE pour modifier la priorité de la stratégie d'adresse de messagerie

Un utilisateur peut avoir plusieurs adresses de messagerie proxy pour le même compte de messagerie (par exemple, ayla@exchange.mail.contoso.com ou ayla@contoso.com). Ces adresses électroniques peuvent ensuite être appliquées en fonction de leur priorité. Imaginons, par exemple, le scénario suivant : vous avez deux stratégies d'adresse de messagerie et vous leur attribuez les priorités 1 et 2. Si vous créez une autre stratégie, la priorité 3 lui sera automatiquement attribuée. Toutefois, imaginons que vous avez deux stratégies et que vous spécifiez l'une d'entre elles comme étant la priorité 1, mais que l'autre stratégie avait, par défaut, une priorité 2 lors de sa création. Dans ce cas, la prochaine stratégie que vous créerez deviendra, par défaut, la stratégie de priorité 2. La stratégie qui avait précédemment la priorité 2 recevra une priorité de 3.

1.  Accédez à **Flux de messagerie** \> **Stratégies d'adresse de messagerie**.

2.  Sélectionnez la stratégie d'adresse de messagerie pour laquelle vous souhaitez modifier la priorité, puis cliquez sur **Augmenter la priorité**![Icône flèche vers le haut](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icône flèche vers le haut") ou sur **Diminuer la priorité**![Icône de flèche vers le bas](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icône de flèche vers le bas").

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une stratégie d'adresse de messagerie

Cet exemple modifie la stratégie d'adresse de messagerie des bureaux de la région Sud-est qui inclut les destinataires basés en Géorgie, en Alabama et en Louisiane afin d'y ajouter également les destinataires basés au Texas.

    Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Bien que la stratégie d'adresse de messagerie soit déjà appliquée aux destinataires basés en Géorgie, en Alabama et en Louisiane, vous devez les inclure au paramètre, car celui-ci remplace les valeurs. En effet, il n'ajoute pas de valeurs à celles existantes.</td>
</tr>
</tbody>
</table>


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-EmailAddressPolicy](https://technet.microsoft.com/fr-fr/library/bb124517\(v=exchg.150\)).

