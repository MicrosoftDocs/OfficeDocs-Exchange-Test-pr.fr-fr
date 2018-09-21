---
title: 'Gérer le filtrage du contenu: Exchange 2013 Help'
TOCTitle: Gérer le filtrage du contenu
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50477455
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer le filtrage du contenu

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

L’agent de filtrage du contenu permet de filtrer du contenu. Il filtre tous les messages en provenance de tous les connecteurs de réception sur le serveur Exchange. Seuls les messages provenant de sources non authentifiées sont filtrés.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage du contenu

Pour désactiver le filtrage du contenu, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -Enabled $false
```

Pour activer le filtrage du contenu, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -Enabled $true
```

> [!NOTE]
> Lorsque vous désactivez le filtrage du contenu, l’agent de filtrage du contenu sous-jacent est toujours activé. Pour désactiver l’agent de filtrage du contenu, exécutez la commande suivante : <code>Disable-TransportAgent &quot;Content Filter Agent&quot;</code>.


## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à activer ou désactiver le filtrage du contenu, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

2.  Vérifiez la valeur de la propriété *Enabled* affichée.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage du contenu dans les messages externes

Par défaut, la fonctionnalité de filtrage du contenu est activée pour les messages externes.

Pour désactiver le filtrage du contenu dans les messages externes, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $false
```

Pour activer le filtrage du contenu dans les messages externes, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $true
```

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à activer ou désactiver le filtrage du contenu dans les messages externes, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterConfig | Format-List ExternalMailEnabled
```

2.  Vérifiez la valeur de la propriété *ExternalMailEnabled* affichée.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage du contenu dans les messages internes

Il est conseillé de ne pas filtrer les messages provenant de partenaires approuvés ou de l’intérieur de l’organisation. Lorsque vous exécutez des filtres anti-spam, il est toujours possible que les filtres détectent des faux positifs. Pour éviter autant que possible de filtrer des messages électroniques légitimes, vous devez permettre aux agents anti-spam de ne s’exécuter que sur les messages en provenance de sources potentiellement non approuvées et inconnues.

Pour activer le filtrage du contenu dans les messages internes, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -InternalMailEnabled $true
```

Pour désactiver le filtrage du contenu dans les messages internes, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -InternalMailEnabled $false
```

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à activer ou désactiver le filtrage du contenu dans les messages internes, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterConfig | Format-List InternalMailEnabled
```

2.  Vérifiez la valeur de la propriété *InternalMailEnabled* affichée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des exceptions de destinataire et d'expéditeur

Pour remplacer les valeurs existantes, exécutez la commande suivante :

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

Cet exemple permet de configurer les exceptions suivantes dans le filtrage du contenu :

  - Le filtrage du contenu ne vérifie pas les destinataires laura@contoso.com et julia@contoso.com.

  - Le filtrage du contenu ne vérifie pas les expéditeurs steve@fabrikam.com et cindy@fabrikam.com.

  - Le filtrage du contenu ne vérifie aucun expéditeur du domaine nwtraders.com ni aucun sous-domaine.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

Pour ajouter ou supprimer des entrées sans modifier une valeur existante, exécutez la commande suivante :

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Cet exemple permet de configurer les exceptions suivantes dans le filtrage du contenu :

  - Ajoutez tiffany@contoso.com et chris@contoso.com à la liste des destinataires qui ne sont pas vérifiés par le filtrage du contenu.

  - Ajoutez joe@fabrikam.com et michelle@fabrikam.com à la liste des expéditeurs qui ne sont pas vérifiés par le filtrage du contenu.

  - Ajoutez blueyonderairlines.com à la liste des domaines dont les expéditeurs ne sont pas vérifiés par le filtrage du contenu.

  - Supprimez le domaine woodgrovebank.com et tous les sous-domaines de la liste des domaines dont les expéditeurs ne sont pas vérifiés par le filtrage du contenu.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à configurer les exceptions de destinataires et d’expéditeurs, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  Vérifiez si les valeurs affichées correspondent aux paramètres spécifiés.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des expressions autorisées et bloquées

Pour ajouter des expressions et des mots autorisés et bloqués, exécutez la commande suivante :

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

Dans cet exemple, tous les messages contenant l’expression « customer feedback » sont autorisés.

```powershell
Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"
```

Dans cet exemple, tous les messages contenant l’expression « stock tip » sont bloqués.

```powershell
Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"
```

Pour supprimer les expressions autorisées ou bloquées, exécutez la commande suivante :

```powershell
Remove-ContentFilterPhrase -Phrase <Phrase>
```

Dans cet exemple, l’expression « stock tip » est supprimée :

```powershell
Remove-ContentFilterPhrase -Phrase "stock tip"
```

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à configurer les expressions autorisées et bloquées, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterPhrase | Format-List Influence,Phrase
```

2.  Vérifiez si les valeurs affichées correspondent aux paramètres spécifiés.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des seuils de probabilité de courrier indésirable

Pour configurer les seuils de probabilité de courrier indésirable (SCL) et les actions, exécutez la commande suivante :

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>

> [!NOTE]
> L’action de suppression prévaut sur l’action de rejet, laquelle prévaut sur l’action de mise en quarantaine. Ainsi, le seuil SCL de l’action de suppression doit être supérieur au seuil SCL de l’action de rejet, lequel doit être supérieur au seuil SCL de l’action de mise en quarantaine. Seule l’action de rejet est activée par défaut. Son seuil SCL a la valeur 7.


Cet exemple permet de configurer les valeurs de seuil SCL suivantes :

  - L’action de suppression est activée et le seuil SCL correspondant est défini sur 9.

  - L’action de rejet est activée et le seuil SCL correspondant est défini sur 8.

  - L’action de mise en quarantaine est activée et le seuil SCL correspondant est défini sur 7.

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à configurer les seuils SCL, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-ContentFilterConfig | Format-List SCL*

2.  Vérifiez si les valeurs affichées correspondent aux paramètres spécifiés.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la réponse de rejet

Lorsque l’action de rejet est activée, vous pouvez personnaliser la réponse de rejet envoyée à l’expéditeur du message. La réponse de rejet ne peut pas dépasser 240 caractères.

Pour configurer une réponse de rejet personnalisée, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -RejectionResponse "<Custom Text>"
```

L’exemple suivant permet de configurer l’agent de filtrage du contenu afin qu’il envoie une réponse de rejet personnalisée.

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à configurer la réponse de rejet, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  Vérifiez si les valeurs affichées correspondent aux paramètres spécifiés.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le cachet électronique Outlook

La validation du *cachet électronique Outlook* est une preuve de calcul que Microsoft Outlook applique aux messages sortants pour permettre aux systèmes de messagerie destinataires de différencier les messages électroniques légitimes du courrier indésirable. Cette fonction de cachet électronique est disponible dans Outlook 2007 ou dans les versions ultérieures. Elle contribue à réduire les faux positifs. Le cachet électronique Outlook est activé par défaut.

Pour désactiver le cachet électronique Outlook, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false
```

Pour activer le cachet électronique Outlook, exécutez la commande suivante :

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true
```

## Comment savoir si cela a fonctionné ?

Pour savoir si vous avez réussi à configurer le cachet électronique Outlook, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled
```

2.  Vérifiez si la valeur affichée correspond au paramètre spécifié.

