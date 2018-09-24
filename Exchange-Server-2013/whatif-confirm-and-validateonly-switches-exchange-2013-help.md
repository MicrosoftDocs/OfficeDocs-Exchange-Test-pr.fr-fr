---
title: 'Commutateurs WhatIf, Confirm et ValidateOnly: Exchange 2013 Help'
TOCTitle: Commutateurs WhatIf, Confirm et ValidateOnly
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 50478841
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Commutateurs WhatIf, Confirm et ValidateOnly

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-04_

Les administrateurs et les auteurs de scripts expérimentés, de même que les administrateurs qui débutent avec Exchange et les scripts, peuvent tirer parti de l'utilisation des commutateurs *WhatIf*, *Confirm* et *ValidateOnly*. Les commutateurs suivants vous aident à contrôler comment sont exécutées vos commandes et à indiquer exactement ce que fera une commande avant d’affecter les données. Cette fonctionnalité est surtout importante lorsque vous opérez une transition de votre environnement de test à votre environnement de production et pendant que vous transférez de nouveaux scripts ou commandes.

Les commutateurs *WhatIf*, *Confirm* et *ValidateOnly* sont particulièrement utiles lorsque vous les utilisez avec des commandes qui modifient les objets retournés à l'aide d'un filtre ou d'une commande **Get** d'un pipeline. Cette rubrique décrit chaque commutateur et fournit également une commande en exemple.

> [!IMPORTANT]
> Si vous voulez utiliser les commutateurs <em>WhatIf</em>, <em>Confirm</em> et <em>ValidateOnly</em> avec des commandes dans un script, vous devez ajouter le commutateur approprié à chaque commande dans le script, et non dans la ligne de commande qui appelle le script.


> [!NOTE]
> <em>WhatIf</em>, <em>Confirm</em> et <em>ValidateOnly</em> sont des paramètres de commutateur. Pour plus d’informations sur les paramètres de commutateurs, voir <a href="https://technet.microsoft.com/fr-fr/library/bb124388(v=exchg.150)">Paramètres</a>.


## Commutateur WhatIf

Lorsque le commutateur *WhatIf* est appliqué à une commande, la commande s'exécute, mais uniquement pour afficher les objets qui seraient affectés par son exécution, ainsi que les modifications qui seraient apportées à ces objets. Le commutateur ne change vraiment aucun de ces objets. Lorsque vous utilisez le commutateur *WhatIf*, vous pouvez déterminer si les modifications qui seraient apportées à ces objets correspondent à vos attentes, tout en sachant que ces objets ne sont pas modifiés.

Lorsque vous exécutez une commande avec le commutateur *WhatIf*, vous placez le commutateur *WhatIf* à la fin de la commande, comme dans l’exemple suivant :

```powershell
New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 
```

Lorsque vous exécutez cet exemple de commande, le texte suivant est retourné par le Shell :

```powershell
What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".
```

## Commutateur Confirm

Lorsque le commutateur *Confirm* est appliqué à une commande, le traitement de la commande est arrêté avant que des modifications ne soient effectuées. La commande vous incite ensuite à accepter chaque action avant qu’elle ne continue. Lorsque vous utilisez le commutateur *Confirm*, vous pouvez vérifier individuellement les modifications apportées aux objets pour vous assurer qu'elles s'appliquent uniquement aux objets que vous voulez modifier. Cette fonctionnalité est utile lorsque vous appliquez les changements à plusieurs objets et que vous voulez un contrôle précis sur l’opération du Shell. Une boîte de dialogue de confirmation est affichée pour chaque objet avant que le Shell ne modifie l’objet.

Par défaut, l'environnement de ligne de commande Exchange Management Shell applique automatiquement le commutateur *Confirm* aux cmdlets qui contiennent les verbes suivants :

  - **Clear**

  - **Disable**

  - **Dismount**

  - **Move**

  - **Remove**

  - **Stop**

  - **Suspend**

  - **Uninstall**

Lorsqu’une cmdlet qui n’a aucun de ces verbes est exécutée, le Shell arrête automatiquement la commande et attend votre acceptation avant de continuer le processus.

Lorsque vous appliquez manuellement le commutateur *Confirm* à une commande, incluez-le à la fin de la commande, comme dans l'exemple suivant :

```powershell
Get-JournalRule | Enable-JournalRule -Confirm
```

Lorsque vous exécutez cet exemple de commande, la boîte de dialogue suivante est retournée par le Shell :

```powershell
Confirm
Are you sure you want to perform this action?
Enabling journal rule "Litigation Journal Rule".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

La boîte de dialogue de confirmation fournit les options suivantes:

  - **\[Y\] Yes**   Tapez **Y** pour que la commande poursuive l'opération. L’opération suivante présentera une autre boîte de dialogue de confirmation. `[Y] Yes` est la sélection par défaut.

  - **\[A\] Yes to All**   Tapez **A** pour que la commande poursuive l'opération ainsi que toutes les opérations suivantes. Vous ne recevrez pas d’autres boîtes de dialogue de confirmation pendant la durée de cette commande.

  - **\[N\] No**   Tapez **N** pour que la commande ignore cette opération et passe à l'opération suivante. L’opération suivante présentera une autre boîte de dialogue de confirmation.

  - **\[L\] No to All**   Tapez **L** pour que la commande ignore cette opération ainsi que toutes les opérations suivantes.

  - **\[S\] Suspend**   Tapez **S** pour interrompre le pipeline en cours et revenir à la ligne de commande. Tapez **Exit** pour reprendre le pipeline.

  - **\[?\] Help**   Tapez **?** pour afficher l'aide de la demande de confirmation sur la ligne de commande.

Si vous souhaitez annuler le comportement par défaut de l'environnement Exchange Management Shell et supprimer la demande de confirmation pour les cmdlets auxquelles elle est automatiquement appliquée, vous pouvez inclure le commutateur *Confirm* avec la valeur `$False`, comme dans l'exemple suivant :

```powershell
Get-JournalRule | Disable-JournalRule -Confirm:$False
```

Dans ce cas, aucune boîte de dialogue de confirmation n’est affichée.

> [!CAUTION]
> La valeur par défaut du commutateur <em>Confirm</em> est <code>$True</code>. Le comportement par défaut du Shell est d’afficher automatiquement une boîte de dialogue de confirmation. Si vous supprimez ce comportement par défaut, vous ordonnez à la commande de supprimer toutes les boîtes de dialogue de confirmation pendant la durée d’exécution de la commande. La commande traitera tous les objets qui satisfont aux critères pour la commande sans confirmation.


## Commutateur ValidateOnly

Lorsque le commutateur *ValidateOnly* est appliqué à une commande, la commande évalue toutes les conditions et exigences nécessaires pour exécuter l'opération avant d'appliquer des modifications. Le commutateur *ValidateOnly* est disponible pour les cmdlets dont l'exécution peut être longue, qui possèdent plusieurs dépendances sur différents systèmes ou qui affectent des données essentielles telles que les boîtes aux lettres.

Lorsque vous appliquez le commutateur *ValidateOnly* à une commande, toutes les étapes sont exécutées. La commande exécute chaque action comme elle le ferait sans le commutateur *ValidateOnly*. La commande ne modifie cependant aucun objet. Lorsque la commande termine son processus, elle affiche un résumé avec les résultats de la validation. Si la validation indique que la commande a réussi, vous pouvez réexécuter la commande sans le commutateur *ValidateOnly*.

Lorsque vous exécutez une commande avec le commutateur *ValidateOnly*, vous placez le commutateur *ValidateOnly* à la fin de la commande.

