---
title: 'Gérer le filtrage des expéditeurs: Exchange 2013 Help'
TOCTitle: Gérer le filtrage des expéditeurs
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50478838
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer le filtrage des expéditeurs

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Le filtrage des expéditeurs est fourni par l'agent de filtrage des expéditeurs. L'agent de filtrage des expéditeurs s'appuie sur l'en-tête SMTP **MAIL FROM:**  pour déterminer l’action à effectuer (le cas échéant) pour un message entrant.

Lorsque la fonctionnalité de filtrage des expéditeurs est activée sur un serveur Exchange, elle filtre tous les messages transmis via l'ensemble des connecteurs de réception présents.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage des expéditeurs

Pour désactiver le filtrage des expéditeurs, exécutez la commande suivante :

```powershell
Set-SenderFilterConfig -Enabled $false
```

Pour activer le filtrage des expéditeurs, exécutez la commande suivante :

```powershell
Set-SenderFilterConfig -Enabled $true
```

> [!NOTE]
> Quand vous désactivez le filtrage des expéditeurs, l'agent de filtrage des expéditeurs sous-jacent reste activé. Pour désactiver l'agent de filtrage des expéditeurs, exécutez la commande suivante : <code>Disable-TransportAgent &quot;Sender Filter Agent&quot;</code>.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé le filtrage des expéditeurs, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderFilterConfig | Format-List Enabled
    ```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des domaines et expéditeurs bloqués

Pour remplacer les valeurs existantes, exécutez la commande suivante :

```powershell
Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>
```

Dans cet exemple, l'agent de filtrage des expéditeurs est configuré de manière à bloquer les messages de kim@contoso.com et john@contoso.com, ceux provenant du domaine fabrikam.com et ceux provenant du domaine northwindtraders.com et de tous ses sous-domaines.

```powershell
Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com
```

Pour ajouter ou supprimer des entrées sans modifier une valeur existante, exécutez la commande suivante :

```powershell
Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}
```

Dans cet exemple, l'agent de filtrage des expéditeurs est configuré avec les informations suivantes :

  - Ajouter chris@contoso.com et michelle@contoso.com à la liste des expéditeurs existants qui sont bloqués.

  - Supprimer tailspintoys.com de la liste des domaines existants d'expéditeurs qui sont bloqués.

  - Ajouter blueyonderairlines.com à la liste des domaines et sous-domaines existants d'expéditeurs qui sont bloqués.

<!-- end list -->

```powershell
Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré le blocage des expéditeurs, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains
    ```

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le blocage des messages à expéditeurs vierges

Pour activer ou désactiver le blocage des messages à expéditeurs vierges, exécutez la commande suivante :

```powershell
Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>
```

Dans cet exemple, l'agent de filtrage des expéditeurs est configuré de manière à bloquer les messages qui n'indiquent pas d'expéditeur dans l'en-tête de commande SMTP MAIL FROM:

```powershell
Set-SenderFilterConfig -BlankSenderBlockingEnabled $true
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé le blocage des messages à expéditeurs vierges, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled
    ```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

