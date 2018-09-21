---
title: 'Réécriture d’adresses sur les srv de transport Edge: Exchange 2013 Help'
TOCTitle: Gestion de la réécriture d’adresses sur les serveurs de transport Edge
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060520
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de la réécriture d’adresses sur les serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Pour toutes les tâches de gestion liées à la réécriture d’adresses et aux agents de réécriture d’adresses, utilisez l’environnement de ligne de commande Exchange Management Shell sur un serveur de transport Edge. Pour plus d’informations sur la réécriture d’adresses, consultez la rubrique [Réécriture d’adresses sur des serveurs de transport Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

Vous pouvez créer des entrées de réécriture d’adresses qui s’appliquent à un seul destinataire, à tous les destinataires dans un domaine ou sous-domaine spécifique, ou à tous les destinataires dans plusieurs sous-domaines. La réécriture d’adresses peut concerner uniquement les messages sortants ou les messages entrants et sortants (bidirectionnelle). Lorsque vous créez des entrées de réécriture d’adresses, gardez à l’esprit les points suivants :

  - Vérifiez que les adresses de messagerie obtenues sont uniques dans votre organisation.

  - Seules les chaînes littérales sont prises en charge dans les valeurs d’adresse de messagerie.

  - Le caractère générique (\*) est pris en charge uniquement dans l’adresse interne (les adresses à modifier). La syntaxe valide pour l’utilisation du caractère générique est **\*.contoso.com**. Les valeurs **\*contoso.com** ou **sales.\*.com** ne sont pas autorisées.

  - Lors de l’utilisation du caractère générique, vous devez configurer la réécriture d’adresses pour les messages sortants uniquement (vous devez définir le paramètre *OutboundOnly* sur la valeur `$true`).

  - Lors de la configuration de la réécriture d’adresses pour les messages sortants uniquement (en définissant le paramètre *OutboundOnly* sur la valeur `$true`), vous devez configurer les adresses proxy sur les destinataires concernés. Ainsi, les messages électroniques envoyés à l’adresse réécrite peuvent être distribués correctement.

  - Par défaut, la réécriture d’adresses est bidirectionnelle pour les destinataires uniques ou tous les destinataires dans un domaine ou sous-domaine spécifique (la valeur par défaut pour le paramètre *OutboundOnly* est `$false`).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Serveurs de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Soyez prudent lors de la configuration de la réécriture d’adresses. Toutes les modifications apportées sont appliquées dès l’exécution de la commande. Envisagez d’exécuter la commande avec le paramètre *WhatIf*. Pour plus d’informations sur le paramètre *WhatIf*, voir [Commutateurs WhatIf, Confirm et ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement Exchange Management Shell pour activer ou désactiver la réécriture d’adresses

Pour activer ou désactiver complètement la réécriture d’adresses, vous devez activer ou désactiver les agents de réécriture d’adresses. Par défaut, les agents de réécriture d’adresses sur un serveur de transport Edge sont activés.

Pour désactiver la réécriture d’adresses, exécutez les commandes suivantes :

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

Pour activer la réécriture d’adresses, exécutez les commandes suivantes :

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé la réécriture d’adresse, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-TransportAgent
```

2.  Vérifiez que les valeurs de la propriété **Enabled** pour l’agent de réécriture d’adresses pour les messages entrants et l’agent de réécriture d’adresses pour les messages sortants correspondent aux valeurs configurées.

## Utiliser l’environnement Exchange Management Shell pour afficher les entrées de réécriture d’adresses

Pour afficher la liste récapitulative de toutes les entrées de réécriture d’adresses, exécutez la commande suivante :

```powershell
Get-AddressRewriteEntry
```

Pour afficher les détails d’une entrée de réécriture d’adresses, utilisez la syntaxe suivante.

```powershell
Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List
```

L’exemple suivant affiche les détails de l’entrée de réécriture d’adresses nommée « Rewrite Contoso.com to Northwindtraders.com » (réécrire Contoso.com en Northwindtraders.com) :

```powershell
Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List
```

## Utiliser l’environnement Exchange Management Shell pour créer des entrées de réécriture d’adresses

## Réécriture d’adresses de messagerie de destinataires uniques

Pour réécrire l’adresse de messagerie pour un destinataire unique, utilisez la syntaxe suivante :

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

L’exemple suivant réécrit l’adresse de messagerie de tous les messages entrant et sortant de l’organisation Exchange pour le destinataire joe@contoso.com. Les messages sortants sont réécrits de sorte qu’ils semblent provenir de support@northwindtraders.com. L’adresse des messages entrants envoyés à support@northwindtraders.com est réécrite et remplacée par joe@contoso.com afin que ceux-ci soient remis à leur destinataire (le paramètre *OutboundOnly* est défini sur `$false` par défaut).

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## Réécriture d’adresses de messagerie de destinataires dans un domaine ou un sous-domaine unique

Pour réécrire les adresses de messagerie de destinataires dans un domaine ou sous-domaine unique, utilisez la syntaxe suivante :

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

L’exemple suivant réécrit les adresses de messagerie de tous les messages entrant et sortant de l’organisation Exchange pour les destinataires dans le domaine contoso.com. Les messages sortants sont réécrits de sorte qu’ils semblent provenir du domaine fabrikam.com. Lorsque des messages entrants sont envoyés à des adresses de messagerie dont le domaine est fabrikam.com, celui-ci est réécrit et remplacé par contoso.com pour être remis aux destinataires (le paramètre *OutboundOnly* est `$false` par défaut).

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

L’exemple suivant réécrit les adresses de messagerie de tous les messages sortant de l’organisation Exchange qui sont envoyés par les utilisateurs du sous-domaine sales.contoso.com. Les domaines des messages sortants sont réécrits de sorte que ces derniers semblent provenir du domaine contoso.com. Les messages entrants envoyés à des adresses de messagerie contoso.com ne sont pas réécrits.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## Réécriture d’adresses de messagerie de destinataires dans plusieurs sous-domaines

Pour réécrire les adresses de messagerie de destinataires dans un domaine et tous les sous-domaines, utilisez la syntaxe suivante :

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

L’exemple suivant réécrit les adresses de messagerie de tous les messages sortant de l’organisation Exchange qui sont envoyés par les utilisateurs du domaine contoso.com et de tous les sous-domaines. Les domaines des messages sortants sont réécrits de sorte que ces derniers semblent provenir du domaine contoso.com. Les domaines messages entrants envoyés à des destinataires contoso.com ne peuvent pas être réécrits car un caractère générique est utilisé dans le paramètre *InternalAddress*.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

L’exemple suivant est presque identique à l’exemple précédent, sauf qu’à présent les domaines des messages envoyés par les destinataires dans les sous-domaines legal.contoso.com et corp.contoso.com ne sont jamais réécrits :

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé des entrées de réécriture d’adresses, procédez comme suit :

1.  Exécutez la commande `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` et vérifiez que les paramètres affichés correspondent à ceux configurés.

2.  Envoyez un message de test à une boîte aux lettres externe à partir d’une boîte aux lettres concernée par une entrée de réécriture d’adresses. Vérifiez que le message de test semble provenir de l’adresse de messagerie réécrite.

3.  Répondez au message de test à partir de la boîte aux lettres externe. Vérifiez que la boîte aux lettres d’origine reçoit bien la réponse.

## Utiliser l’environnement Exchange Management Shell pour modifier des entrées de réécriture d’adresses

Les options de configuration disponibles lors de la modification d’une entrée de réécriture d’adresses existante sont identiques aux options de configuration disponibles lors de la création d’une entrée de réécriture d’adresses.

## Modification des entrées de réécriture d’adresses pour les destinataires uniques

Pour modifier une entrée de réécriture d’adresses qui réécrit l’adresse de messagerie d’un destinataire unique, utilisez la syntaxe suivante :

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

L’exemple suivant modifie les propriétés suivantes de l’entrée de réécriture d’adresses du destinataire unique nommée « joe@contoso.com to support@nortwindtraders.com » :

  - Remplace l’adresse externe par support@northwindtraders.net.

  - Remplace le nom de l’entrée de réécriture d’adresses par « joe@contoso.com to support@northwindtraders.net ».

  - Modifie la valeur de *OutboundOnly* et la remplace par `$true`. Notez que pour effectuer cette modification, vous devez configurer support@northwindtraders.net en tant qu’adresse proxy sur la boîte aux lettres de Joe.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## Modification d’entrées de réécriture d’adresses pour des destinataires dans des domaines ou sous-domaines uniques

Pour modifier une entrée de réécriture d’adresses qui réécrit les adresses de messagerie des destinataires dans un domaine ou sous-domaine unique, utilisez la syntaxe suivante.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

L’exemple suivant modifie la valeur d’adresse interne de l’entrée de réécriture d’adresses de domaine unique nommée « Northwind Traders to Contoso ».

```powershell
Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net
```

## Modification d’entrées de réécriture d’adresses pour des destinataires dans plusieurs sous-domaines

Pour modifier une entrée de réécriture d’adresses qui réécrit l’adresse de messagerie des destinataires dans un domaine et tous les sous-domaines, utilisez la syntaxe suivante.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

Pour remplacer les valeurs de la liste des exceptions existantes d’une entrée de réécriture d’adresses de plusieurs sous-domaines, utilisez la syntaxe suivante :

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

L’exemple suivant remplace la liste des exceptions existantes pour l’entrée de réécriture d’adresses de plusieurs sous-domaines nommée « Contoso to Northwind Traders » par les valeurs marketing.contoso.com et legal.contoso.com :

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

Pour ajouter ou supprimer de manière sélective des valeurs de la liste des exceptions d’une entrée de réécriture d’adresses de plusieurs sous-domaines sans modifier les valeurs de la liste des exceptions existantes, utilisez la syntaxe suivante :

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

L’exemple suivant ajoute finanace.contoso.com et supprime marketing.contoso.com de la liste des exceptions de l’entrée de réécriture d’adresses de plusieurs sous-domaines nommée « Contoso to Northwind Traders » :

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien modifié une entrée de réécriture d’adresses, procédez comme suit :

1.  Exécutez la commande `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` et vérifiez que les paramètres affichés correspondent à ceux configurés.

2.  Envoyez un message de test à une boîte aux lettres externe à partir d’une boîte aux lettres concernée par une entrée de réécriture d’adresses. Vérifiez que le message de test semble provenir de l’adresse de messagerie réécrite.

3.  Répondez au message de test à partir de la boîte aux lettres externe. Vérifiez que la boîte aux lettres d’origine reçoit bien la réponse.

## Utiliser l’environnement Exchange Management Shell pour supprimer des entrées de réécriture d’adresses

Pour supprimer une entrée de réécriture d’adresses unique, utilisez la syntaxe suivante :

```powershell
Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>
```

L’exemple suivant supprime l’entrée de réécriture d’adresses nommée « Contoso.com to Northwindtraders.com » :

```powershell
Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"
```

Pour modifier plusieurs entrées de réécriture d’adresses, utilisez la syntaxe suivante :

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

L’exemple suivant supprime toutes les entrées de réécriture d’adresses :

```powershell
Get-AddressRewriteEntry | Remove-AddressRewriteEntry
```

L’exemple suivant simule la suppression des entrées de réécriture d’adresses qui contiennent le texte « to contoso.com » dans leur nom. Le commutateur *WhatIf* vous permet d’afficher un aperçu du résultat en n’effectuant aucune modification.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

Si vous êtes satisfait du résultat, réexécutez la commande sans le commutateur *WhatIf* pour supprimer les entrées de réécriture d’adresses.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une entrée de réécriture d’adresses, procédez comme suit :

1.  Exécutez la commande `Get-AddressRewriteEntry` et vérifiez que les entrées de réécriture d’adresses que vous avez supprimées ne sont pas répertoriées.

2.  Envoyez un message de test à une boîte aux lettres externe à partir d’une boîte aux lettres concernée par une entrée de réécriture d’adresses. Vérifiez que le message de test n’est plus affecté par l’entrée de réécriture d’adresses supprimée.

3.  Répondez au message de test à partir de la boîte aux lettres externe. Vérifiez que la réponse est bien reçue dans la boîte aux lettres d’origine et que l’entrée de réécriture d’adresses supprimée n’a pas été appliquée au message.

