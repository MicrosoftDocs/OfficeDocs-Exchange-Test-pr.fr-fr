---
title: 'Convertir une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Convertir une boîte aux lettres
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50479374
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Convertir une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-04-26_

La conversion d’une boîte aux lettres en une boîte aux lettres de type différent est très semblable à la procédure dans Exchange 2010. Vous devez toujours utiliser la cmdlet Set-Mailbox dans l’interpréteur de commandes pour réaliser la conversion.

Voici les conversions de boîtes aux lettres qui sont possibles :

  - boîte aux lettres d’utilisateur en boîte aux lettres de ressources (salle ou équipement) ;

  - boîte aux lettres partagée en boîte aux lettres d'utilisateur ;

  - boîte aux lettres partagée en boîte aux lettres de ressources ;

  - boîte aux lettres de ressources en boîte aux lettres d'utilisateur ;

  - boîte aux lettres de ressources en boîte aux lettres partagée.

Si votre organisation utilise un environnement Exchange hybride, vous devez gérer vos boîtes aux lettres à l’aide des outils locaux de gestion Exchange. Pour convertir une boîte aux lettres dans un environnement hybride, vous devrez peut-être déplacer la boîte aux lettres vers l’instance Exchange locale, convertir le type de boîte aux lettres, puis la redéplacer vers Office 365.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous convertissez une boîte aux lettres d’utilisateur en boîte aux lettres partagée, vous devez soit supprimer les appareils mobiles de la boîte aux lettres avant la conversion, soit bloquer l’accès mobile à la boîte aux lettres après la conversion. En effet, une fois la boîte aux lettres convertie en boîte aux lettres partagée, les fonctionnalités mobiles ne fonctionnent plus correctement. Pour savoir comment bloquer l’accès mobile, consultez l’article <a href="https://go.microsoft.com/fwlink/p/?linkid=847873">Supprimer un ancien employé d’Office 365</a>.</td>
</tr>
</tbody>
</table>


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour convertir une boîte aux lettres

Durée d'exécution estimée : 5 minutes.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

Dans cet exemple, la boîte aux lettres partagée, MarketingDept1, est convertie en boîte aux lettres d’utilisateur.

    Set-Mailbox MarketingDept1 -Type Regular

Vous pouvez utiliser les valeurs suivantes pour le paramètre *Type* :

  - Regular

  - Salle

  - Équipements

  - Shared

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien converti la boîte aux lettres, exécutez la commande suivante de l’environnement de ligne de commande Exchange Management Shell :

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

La valeur de *RecipientTypeDetails* doit être *UserMailbox*.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

