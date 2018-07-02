---
title: 'Placement d’une boîte aux lettres en conservation pour litige: Exchange 2013 Help'
TOCTitle: Placement d’une boîte aux lettres en conservation pour litige
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62268984
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Placement d’une boîte aux lettres en conservation pour litige

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-10-18_

Vous pouvez placer une boîte aux lettres en conservation pour litige pour conserver tout le contenu de la boîte aux lettres, y compris les éléments supprimés et les versions originales des éléments modifiés. Lorsque vous placez une conservation pour litige sur la boîte aux lettres d’un utilisateur, le contenu de la boîte aux lettres d’archivage de l’utilisateur (si elle est activée) est également placé en conservation. Les éléments supprimés et modifiés sont conservés pendant une période déterminée, ou jusqu’à ce que vous supprimiez la boîte aux lettres de la conservation pour litige. Tous ces éléments de boîte aux lettres sont renvoyés dans une recherche de [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La conservation pour litige conserve les éléments dans le dossier Éléments récupérables de la boîte aux lettres de l’utilisateur. En fonction du nombre et de la taille des éléments supprimés ou modifiés, la taille du dossier Éléments récupérables de la boîte aux lettres peut augmenter rapidement. Le dossier Éléments récupérables est configuré avec un quota élevé par défaut. Dans Exchange Online, ce quota est automatiquement augmenté lorsque vous placez une boîte aux lettres en conservation pour litige. Dans Exchange Server 2013, nous vous recommandons de surveiller chaque semaine les boîtes aux lettres mises en conservation pour litige pour vous assurer qu’elles n’atteignent pas les limites de quotas du dossier Éléments récupérables.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes

  - Il se peut que vous deviez attendre 60 minutes avant que le paramètre Conservation pour litige ne soit actif.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Conservation inaltérable » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour placer une boîte aux lettres Exchange Online en conservation pour litige, elle doit disposer d’une licence Exchange Online (Plan 2). Si une boîte aux lettres dispose d’une licence Exchange Online (Plan 1), vous devez lui attribuer une licence Archivage Exchange Online distincte pour la placer en conservation inaltérable.

  - Comme expliqué précédemment, lorsque vous placez une conservation pour litige sur la boîte aux lettres d’un utilisateur, le contenu de la boîte aux lettres de l’utilisateur est également placé en conservation pour litige. Si vous placez une conservation pour litige sur une boîte aux lettres principale locale dans un déploiement hybride Exchange, la boîte aux lettres d’archivage en nuage (si activée) est également placée en conservation pour litige.

  - Dans Exchange Online, le quota du dossier Éléments récupérables est automatiquement augmenté jusqu’à 100 Go lorsque vous placez une boîte aux lettres en conservation pour litige. La taille par défaut de ce dossier est de 30 Go.

  - La conservation pour litige conserve les éléments supprimés, ainsi que les versions originales des éléments modifiés jusqu’à ce que la conservation soit supprimée. Vous pouvez éventuellement spécifier une durée d’attente, ce qui permet de conserver un élément de boîte aux lettres pendant la durée spécifiée. Si vous spécifiez une durée d’attente, cette dernière débute à partir de la date de réception d’un message ou de la date de création d’un élément de boîte aux lettres. Pour conserver les éléments qui répondent aux critères spécifiés, utilisez une conservation inaltérable pour créer une conservation *basée sur la requête*. Pour plus d’informations, consultez la rubrique [Créer ou supprimer une conservation inaltérable](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - Pour utiliser l’environnement de ligne de commande Shell pour placer une boîte aux lettres Exchange Online en conservation inaltérable, vous devez utiliser PowerShell Exchange Online. Pour plus d’informations, consultez la rubrique [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/fr-fr/library/jj984289\(v=exchg.150\)).

  - Le placement d’une boîte aux lettres de dossier public en conservation pour litige n’est pas pris en charge. Vous devez utiliser la conservation inaltérable pour placer des dossiers publics en conservation.

## Utilisation du Centre d’administration Exchange pour mettre une boîte aux lettres en conservation pour litige

1.  Accédez à **Destinataires**\>**Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateur, cliquez sur la boîte aux lettres pour laquelle vous souhaitez activer ou désactiver la conservation pour litige, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.

4.  Sous **Conservation pour litige : désactivée**, cliquez sur **Activer** pour mettre la boîte aux lettres en conservation pour litige.

5.  Sur la page **Conservation pour litige**, entrez les informations facultatives suivantes :
    
      - **Durée de conservation pour litige (en nombre de jours)**   Cette zone permet de spécifier la durée de conservation des éléments de boîte aux lettres lorsque la boîte aux lettres est conservée pour litige. La durée est calculée à compter de la date de réception ou de création de l’élément de boîte aux lettres. Si vous laissez cette zone vide, les éléments sont conservés indéfiniment ou jusqu’à ce que la conservation soit annulée. Indiquez la période en nombre de jours.
    
      - **Remarque**   Cette zone permet d’informer l’utilisateur de la conservation pour litige de sa boîte aux lettres. La notification apparaît dans la boîte aux lettres de l’utilisateur si ce dernier utilise Outlook 2010 ou une version ultérieure.
    
      - **URL**   Cette zone permet de diriger l’utilisateur vers un site web pour plus d’informations sur la conservation pour litige. Cette URL s’affiche dans la boîte aux lettres de l’utilisateur si ce dernier utilise Outlook 2010 ou une version ultérieure.

6.  Cliquez sur **Enregistrer** sur la page **Conservation pour litige**, puis cliquez sur **Enregistrer** sur la page des propriétés de boîte aux lettres.

Retour au début

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour mettre une boîte aux lettres en conservation pour litige indéfiniment

Dans cet exemple, la boîte aux lettres bsuneja@contoso.com est placée en conservation pour litige. Les éléments de la boîte aux lettres sont conservés indéfiniment ou jusqu’à ce que la conservation soit supprimée.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous placez une boîte aux lettres en conservation pour litige indéfiniment (en ne spécifiant aucune durée), la valeur de la propriété de boîte aux lettres <em>LitigationHoldDuration</em> est définie sur <code>Unlimited</code>.</td>
</tr>
</tbody>
</table>


## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour placer une boîte aux lettres en conservation pour litige et conserver les éléments pour une durée spécifiée

Dans cet exemple, la boîte aux lettres bsuneja@contoso.com est placée en conservation pour litige et les éléments sont conservés pendant 2 555 jours (environ 7 ans).

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour placer toutes les boîtes aux lettres en conservation pour litige pour une durée spécifiée

Votre organisation peut exiger que toutes les données de boîtes aux lettres soient conservées pendant une période spécifique. Avant de placer toutes les boîtes aux lettres d’une organisation en conservation pour litige, prenez en considération les points suivants :

Dans cet exemple, toutes les boîtes aux lettres d’utilisateurs de l’organisation sont placées en conservation pour litige pendant un an (365 jours).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

Dans cet exemple, la cmdlet [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)) est utilisée pour récupérer toutes les boîtes aux lettres de l’organisation, un filtre de destinataire est spécifié pour inclure toutes les boîtes aux lettres d’utilisateurs, puis la liste des boîtes aux lettres est dirigée vers la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) pour activer la conservation pour litige et la durée de conservation.

Pour conserver toutes les boîtes aux lettres d’utilisateurs pour une durée indéterminée, exécutez la commande précédente, mais n’incluez pas le paramètre *LitigationHoldDuration*.

Consultez la section Plus d’informations pour obtenir des exemples d’utilisation d’autres propriétés de destinataire dans un filtre pour inclure ou exclure une ou plusieurs boîtes aux lettres.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour supprimer la conservation pour litige d’une boîte aux lettres

Dans cet exemple, la conservation pour litige de la boîte aux lettres bsuneja@contoso.com est supprimée.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false

Retour au début

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement placé une boîte aux lettres en conservation pour litige, effectuez l’une des opérations suivantes :

  - Dans le CAE, procédez comme suit :
    
    1.  Accédez à **Destinataires**\>**Boîtes aux lettres**.
    
    2.  Dans la liste des boîtes aux lettres d’utilisateurs, cliquez sur la boîte aux lettres pour laquelle vous souhaitez vérifier les paramètres de conservation pour litige, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Fonctionnalités de boîte aux lettres**.
    
    4.  Sous **Conservation pour litige**, vérifiez que la conservation est activée.
    
    5.  Cliquez sur **Afficher les détails** pour vérifier la date et l’auteur de la conservation pour litige de la boîte aux lettres. Vous pouvez également vérifier ou modifier les valeurs dans les zones facultatives **Durée de conservation pour litige (en nombre de jours)**, **Remarque** et **URL**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez l’une des commandes suivantes :
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    ou
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    Si une boîte aux lettres est placée en conservation pour litige indéfiniment, la valeur de la propriété de boîte aux lettres *LitigationHoldDuration* est définie sur `Unlimited`.

## Plus d’informations

  - Si votre organisation exige la conservation de toutes les données de boîtes aux lettres pendant une période spécifique, réfléchissez aux éléments suivants avant de placer toutes les boîtes aux lettres de l’organisation en conservation pour litige.
    
      - Lorsque vous utilisez la commande précédente pour mettre en conservation toutes les boîtes aux lettres d’une organisation (ou un sous-ensemble de boîtes aux lettres correspondant à un filtre de destinataire spécifié), seules les boîtes aux lettres existantes au moment de l’exécution de la commande sont placées en conservation. Si vous créez des boîtes aux lettres par la suite, vous devrez exécuter à nouveau la commande pour les placer en conservation. Si vous créez fréquemment des boîtes aux lettres, vous pouvez exécuter la commande en tant que tâche planifiée aussi souvent que nécessaire.
    
      - Le placement de toutes les boîtes aux lettres en conservation pour litige peut avoir une incidence considérable sur la taille des boîtes aux lettres. Dans une organisation Exchange Server 2013, prévoyez un espace de stockage suffisant pour répondre aux exigences de conservation de votre organisation.
    
      - Le dossier Éléments récupérables possède sa propre limite de stockage. Par conséquent, les éléments de ce dossier ne sont pas pris en compte dans la limite de stockage de la boîte aux lettres. Comme expliqué précédemment, si la conservation des données de boîtes aux lettres se prolonge dans le temps, la taille du dossier Éléments récupérables de la boîte aux lettres et de l’archive de l’utilisateur sera de plus en plus élevée. Pour prendre en charge cette augmentation dans Exchange Online, le quota du dossier Éléments récupérables est automatiquement augmenté, passant de 30 Go à 100 Go lorsque vous placez une boîte aux lettres en conservation pour litige.
        
        Dans Exchange Server 2013, la limite de stockage par défaut pour le dossier Éléments récupérables est également de 30 Go. Nous vous recommandons de surveiller la taille du dossier régulièrement afin de vous assurer qu’elle n’atteint pas la limite. Pour plus d'informations, voir [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

  - La commande précédente permettant de placer en conservation toutes les boîtes aux lettres utilise un filtre de destinataire qui renvoie toutes les boîtes aux lettres d’utilisateurs. Vous pouvez utiliser d’autres propriétés de destinataire pour renvoyer une liste de boîtes aux lettres spécifiques que vous pouvez ensuite rediriger vers la cmdlet **Set-Mailbox** pour placer une conservation pour litige sur ces boîtes aux lettres.
    
    Voici quelques exemples d’utilisation des cmdlets **Get-Mailbox** et **Get-Recipient** pour renvoyer un sous-ensemble de boîtes aux lettres sur la base de propriétés de boîte aux lettres ou d’utilisateur courantes. Ces exemples supposent que les propriétés de boîte aux lettres appropriées (telles que *CustomAttributeN* ou *Department*) aient été renseignées.
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    Vous pouvez utiliser d’autres propriétés de boîte aux lettres utilisateur dans un filtre pour inclure ou exclure des boîtes aux lettres. Pour plus d’informations, voir [Propriétés filtrables pour le paramètre -Filter](https://technet.microsoft.com/fr-fr/library/bb738155\(v=exchg.150\)).

Retour au début

