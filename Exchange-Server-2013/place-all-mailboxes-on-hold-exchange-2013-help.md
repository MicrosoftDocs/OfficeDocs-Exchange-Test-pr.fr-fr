---
title: 'Placement de toutes les boîtes aux lettres en conservation: Exchange 2013 Help'
TOCTitle: Placement de toutes les boîtes aux lettres en conservation
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486284
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Placement de toutes les boîtes aux lettres en conservation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-01-18_

> [!NOTE]
> Nous avons différé la date d’échéance du 1er juillet 2017 pour créer des conservations inaltérables dans Exchange Online (dans les plans autonomes Office 365 et Exchange Online). Mais plus tard cette année ou au début de l’année prochaine, vous ne pourrez pas créer des conservations inaltérables dans Exchange Online. Au lieu d’utiliser des conservations inaltérables, vous pouvez avoir recours à des <a href="https://go.microsoft.com/fwlink/?linkid=780738">cas de découverte électronique</a> ou des <a href="https://go.microsoft.com/fwlink/?linkid=827811">stratégies de rétention</a> dans le centre de sécurité et conformité Office 365. Lorsque nous aurons désactivé les nouvelles conservations inaltérables, vous pourrez toujours modifier les conservations inaltérables existantes. La création de conservations inaltérables sera toujours prise en charge dans les déploiements hybrides Exchange Server 2013 et Exchange . Vous serez également toujours en mesure de mettre des boîtes aux lettres en conservation pour litige.


Votre organisation peut exiger que toutes les données de boîtes aux lettres soient conservées pendant une période spécifique. Vous pouvez utiliser la conservation pour litige et la conservation inaltérable pour satisfaire cette exigence. Après avoir placé une boîte aux lettres en conservation pour litige ou en conservation inaltérable, les éléments de boîte aux lettres qui sont modifiés ou supprimés définitivement sont conservés dans le dossier Éléments récupérables. Pour plus d’informations, voir [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md).

Avant de placer toutes les boîtes aux lettres d’une organisation en conservation pour litige ou en conservation inaltérable, prenez en compte les points suivants :

  - Lorsque vous placez des boîtes aux lettres en conservation, le contenu de la boîte aux lettres d’archivage de l’utilisateur (si elle est activée) est également placé en conservation.

  - Le fait de placer toutes les boîtes aux lettres d’une organisation en conservation peut avoir un impact significatif sur la taille des boîtes aux lettres. Dans un déploiement Exchange Server 2013, prévoyez suffisamment d’espace de stockage pour répondre aux exigences de conservation de votre organisation. Dans Exchange Online, les [limites de stockage des boîtes aux lettres](https://go.microsoft.com/fwlink/?linkid=403645) pour vos utilisateurs dépendent de la licence d’abonnement de chaque utilisateur.

  - La conservation prolongée dans le temps des données de boîtes aux lettres entraîne l’augmentation de la taille du dossier Éléments récupérables des boîtes aux lettres principale et d’archivage de l’utilisateur. Le dossier Éléments récupérables possède sa propre limite de stockage. Par conséquent, les éléments de ce dossier ne sont pas pris en compte dans la limite de stockage de la boîte aux lettres. Dans Exchange Server 2013 et Exchange Online, la limite de stockage par défaut pour le dossier Éléments récupérables est de 30 Go.
    
      - Dans Exchange Online, le quota pour le dossier Éléments récupérables est automatiquement augmenté jusqu’à 100 Go lorsque vous placez une boîte aux lettres en conservation.
    
      - Dans Exchange Server 2013, nous vous recommandons de surveiller régulièrement la taille de ce dossier pour vous assurer qu’elle n’atteint pas la limite. Pour plus d'informations, voir [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

## Choix entre conservation pour litige et conservation inaltérable

Voici quelques facteurs à prendre en compte lorsque vous décidez de la fonctionnalité de conservation à utiliser pour placer toutes les boîtes aux lettres de votre organisation en attente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Vous souhaitez...</th>
<th>Utiliser la conservation pour litige</th>
<th>Utiliser la conservation inaltérable</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utiliser le CAE</p></td>
<td><p>Oui</p>
<p>Pour définir la conservation pour litige, le CAE est l’outil le mieux adapté pour effectuer des actions ponctuelles rapides sur quelques boîtes aux lettres. Nous recommandons d’utiliser l’environnement de ligne de commande Exchange Management Shell pour définir la conservation pour litige pour tous les utilisateurs de votre organisation.</p></td>
<td><p>Oui</p>
<p>Toutefois, vous ne pouvez pas sélectionner plus de 500 boîtes aux lettres sources dans le CAE.</p></td>
</tr>
<tr class="even">
<td><p>Utilisation de l’environnement de ligne de commande Exchange Management Shell</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Placer plus de 10 000 boîtes aux lettres en conservation</p></td>
<td><p>Oui</p>
<p>La conservation pour litige est une propriété de boîte aux lettres. Vous pouvez placer toutes les boîtes aux lettres d’une organisation en conservation à l’aide de la cmdlet <strong>Set-Mailbox</strong>.</p></td>
<td><p>Oui, utilisez plusieurs conservations inaltérables.</p>
<p>Vous pouvez utiliser des groupes de distribution pour spécifier au maximum 10 000 boîtes aux lettres dans une seule conservation inaltérable. Pour placer des boîtes aux lettres supplémentaires en conservation, vous devez créer des conservations inaltérables supplémentaires. Cela entraînera des frais de gestion supplémentaires. Il est plus simple d’utiliser la conservation pour litige pour placer un grand nombre de boîtes aux lettres en attente.</p></td>
</tr>
<tr class="even">
<td><p>Placer un grand nombre de boîtes aux lettres en conservation pendant des périodes différentes</p></td>
<td><p>Oui</p>
<p>La conservation pour litige est une propriété de boîte aux lettres. Vous pouvez placer chaque boîte aux lettres (ou des ensembles de boîtes aux lettres) en conservation pour une durée différente.</p>
<p>Consultez la section Plus d’informations pour obtenir des exemples d’utilisation des propriétés de destinataires dans un filtre afin de pouvoir placer une conservation pour litige sur un sous-ensemble de boîtes aux lettres.</p></td>
<td><p>Oui</p>
<p>Si vous devez placer en conservation des milliers de boîtes aux lettres individuelles, nous vous recommandons d’utiliser la conservation pour litige. Si vous créez des conservations pour des événements spécifiques qui impliquent plusieurs utilisateurs, utilisez une conservation inaltérable unique pour le groupe d’utilisateurs en question.</p>
<p>Il n’est pas recommandé de créer des conservations inaltérables distinctes pour chaque boîte aux lettres, car de nombreuses requêtes de conservation inaltérable, plus difficiles à gérer que les conservations pour litige, seront créées. Un grand nombre d’objets en conservation inaltérable peut également entraîner un ralentissement des performances du CAE lors de l’actualisation, la création ou la modification d’objets en conservation.</p></td>
</tr>
<tr class="odd">
<td><p>Placer automatiquement les nouvelles boîtes aux lettres en conservation</p></td>
<td><p>Non</p>
<p>Vous devez placer les nouvelles boîtes aux lettres en conservation pour litige dès leur création. Vous pouvez programmer la commande ou le script à exécuter aussi souvent que nécessaire, pour obtenir le même résultat.</p></td>
<td><p>Non</p>
<p>Vous devez ajouter une nouvelle boîte aux lettres en conservation inaltérable, même si vous avez spécifié un groupe de distribution lorsque vous avez créé cette conservation inaltérable. Vous pouvez également programmer la commande ou le script à exécuter aussi souvent que nécessaire, pour obtenir le même résultat. Nous vous recommandons de configurer le script afin qu’il vérifie si une conservation inaltérable existante a déjà atteint la limite des 10 000 boîtes aux lettres et pour qu’une conservation permanente soit créée, le cas échéant.</p></td>
</tr>
<tr class="even">
<td><p>Placer tous les dossiers publics en conservation</p></td>
<td><p>Non</p>
<p>Dans Exchange Online, le placement des boîtes aux lettres de dossier public en conservation pour litige n’est pas pris en charge. Vous devez utiliser la conservation inaltérable.</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


## Placer toutes les boîtes aux lettres en conservation pour litige

Vous pouvez facilement et rapidement placer toutes les boîtes aux lettres en conservation indéfiniment ou pour une durée déterminée à l’aide de l’environnement de ligne de commande Exchange Management Shell. Cette commande place toutes les boîtes aux lettres en conservation pendant 2 555 jours (environ 7 ans).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

L’exemple utilise la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) et un filtre de destinataires pour récupérer toutes les boîtes aux lettres utilisateur de l’organisation, puis redirige la liste de boîtes aux lettres vers la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) afin d’activer la conservation pour litige et spécifier une durée de conservation. Pour plus d’informations, voir [Placement d’une boîte aux lettres en conservation pour litige](place-a-mailbox-on-litigation-hold-exchange-2013-help.md).

## Placement de toutes les boîtes aux lettres en conservation inaltérable

Vous pouvez utiliser le CAE pour sélectionner jusqu’à 500 boîtes aux lettres et les placer en conservation. Pour plus d’informations, consultez la rubrique [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md).

> [!TIP]
> Pour placer plus de 500 utilisateurs en conservation inaltérable, utilisez l’environnement de ligne de commande Exchange Management Shell. Consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/dd298064(v=exchg.150)">New-MailboxSearch</a>.


## Plus d’informations

  - Lorsque vous placez toutes les boîtes aux lettres de votre organisation en attente, seules les boîtes aux lettres qui existent au moment de l’exécution de la commande sont placées en attente. Si vous créez des boîtes aux lettres par la suite, exécutez à nouveau la commande pour les placer en attente. Si vous créez fréquemment des boîtes aux lettres, vous pouvez exécuter la commande en tant que tâche planifiée aussi souvent que nécessaire.

  - Le fait de mettre les boîtes aux lettres en conservation permet de préserver les données en empêchant leur suppression avant la période spécifiée et en enregistrant la version d’origine d’un message avant qu’il ne soit modifié. Cette opération ne supprime pas automatiquement les messages après la période spécifiée. Combinez la conservation pour litige ou la conservation inaltérable avec une stratégie de rétention, qui peut supprimer automatiquement les messages après la période spécifiée pour répondre aux exigences de votre organisation en matière de rétention des messages électroniques. Pour plus d’informations, voir [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

  - La commande PowerShell utilisée dans cette rubrique pour placer une conservation pour litige sur toutes les boîtes aux lettres utilise un filtre de destinataires qui renvoie toutes les boîtes aux lettres utilisateur. Vous pouvez utiliser d’autres propriétés de destinataire pour renvoyer une liste de boîtes aux lettres spécifiques que vous pouvez ensuite rediriger vers la cmdlet **Set-Mailbox** pour placer une conservation pour litige sur ces boîtes aux lettres.
    
    Voici quelques exemples d’utilisation des cmdlets **Get-Mailbox** et **Get-Recipient** pour renvoyer un sous-ensemble de boîtes aux lettres sur la base de propriétés de boîte aux lettres ou d’utilisateur courantes. Ces exemples supposent que les propriétés de boîte aux lettres appropriées (telles que *CustomAttributeN* ou *Department*) aient été renseignées.
    
       ```
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
       ```

       ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
       ```

       ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
       ```

       ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
       ```

       ```
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
       ```

    
    Vous pouvez utiliser d’autres propriétés de boîte aux lettres utilisateur dans un filtre pour inclure ou exclure des boîtes aux lettres. Pour plus d’informations, voir [Propriétés filtrables pour le paramètre -Filter](https://technet.microsoft.com/fr-fr/library/bb738155\(v=exchg.150\)).

