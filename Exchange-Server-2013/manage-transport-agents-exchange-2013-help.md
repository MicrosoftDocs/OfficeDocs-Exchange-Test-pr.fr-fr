---
title: 'Gérer les agents de transport: Exchange 2013 Help'
TOCTitle: Gérer les agents de transport
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50479541
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gérer les agents de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Les agents de transport utilisent les événements SMTP pour agir sur les messages lorsque ceux-ci sont déplacés dans le pipeline de transport. La plupart des agents de transport intégrés inclus dans Microsoft Exchange Server 2013 sont invisibles et ne sont pas administrables. Cependant, vous pouvez installer et configurer des agents de transport tiers sur les serveurs Exchange de votre organisation. Pour plus d’informations sur les agents de transport, consultez la rubrique [Agents de transport](transport-agents-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - La prise en charge des anciens agents de transport n'est pas activée par défaut, mais vous pouvez l'activer. Pour plus d'informations, consultez la rubrique [Activer la prise en charge des agents de transport hérités](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## A propos des procédures des agents de transport dans le service de transport frontal sur des serveurs d'accès au client

Vous ne pouvez pas utiliser l'environnement de ligne de commande Exchange Management pour gérer l'agent de transport dans le service de transport frontal sur un serveur d'accès au client. A la place, vous devez ouvrir Windows PowerShell sur le serveur d'accès au client et importer ensuite les cmdlets Exchange dans la session Windows PowerShell.

> [!CAUTION]
> L'exécution des cmdlets Exchange dans Windows PowerShell pour les autres tâches que les agents de transport dans le service de transport frontal n'est pas prise en charge. Les conséquences sont graves si vous n'utilisez pas l'environnement de ligne de commande Exchange Management et le contrôle d’accès basé sur les rôles (RBAC) en exécutant des cmdlets Exchange dans Windows PowerShell. Vous devez toujours exécuter les cmdlets Exchange dans l'environnement de ligne de commande Exchange Management. Pour plus d'informations, voir <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notes de publication relatives à Exchange 2013</a>.


Pour exécuter les procédures de l'agent de transport décrites dans cette rubrique dans le service de transport frontal, vous devez procéder comme suit :

1.  Sur le serveur d’accès au client, ouvrez Windows PowerShell et exécutez la commande suivante :
    
    ```powershell
    Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    ```

2.  Exécutez la commande comme cela est indiqué, mais ajoutez-lui la valeur suivante : `-TransportService FrontEnd`.
    
    Par exemple, pour afficher les agents de transport dans le service de transport frontal sur un serveur d'accès au client, exécutez la commande suivante :
    
    ```powershell
    Get-TransportAgent -TransportService FrontEnd
    ```

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour installer un agent de transport

Lorsque vous installez un agent de transport, Exchange enregistre uniquement les DLL associées à cet agent de transport. Vous devez vérifier que les fichiers, les clés de Registre et les autres objets dont dépend l'agent de transport sont installés et configurés correctement. Après avoir chargé les DLL, Exchange continue à les référencer lorsque l'exécution de la commande est terminée.

Les agents de transport ont un accès illimité aux messages électroniques qu'ils rencontrent. Exchange n'impose pas de restrictions au comportement d'un agent de transport. Les agents de transport instables ou qui contiennent des failles de sécurité peuvent affecter la stabilité et la sécurité d'Exchange. C’est pourquoi vous devez installer uniquement des agents de transport totalement approuvés et entièrement testés dans un environnement approprié.

Les agents de transport sont installés dans un état désactivé pour éviter que des agents de transport qui ne sont pas encore configurés nuisent au fonctionnement du flux de messagerie. Par conséquent, lorsqu'un agent de transport est correctement configuré, vous devez l'activer.

Utilisez la syntaxe suivante pour installer un agent de transport.

```powershell
Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">
```

Cet exemple installe une application fictive appelée « Agent de transport Contoso » dans le service de transport sur un serveur de boîtes aux lettres.

```powershell
Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement installé l'agent de transport, exécutez la commande `Get-TransportAgent` et vérifiez la présence de l'agent.

## Utiliser l'environnement de ligne de commande Exchange Management pour activer un agent de transport

Utilisez la syntaxe suivante pour activer un agent de transport.

```powershell
Enable-TransportAgent <TransportAgentIdentity>
```

Cet exemple active l'agent de transport « Agent de transport Contoso » dans le service de transport sur un serveur de boîtes aux lettres.

```powershell
Enable-TransportAgent "Contoso Transport Agent"
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé un agent de transport, exécutez la commande `Get-TransportAgent | Format-List Name,Enabled` et vérifiez que l'agent est activé.

## Utiliser l'environnement de ligne de commande pour désactiver un agent de transport

Utilisez la syntaxe suivante pour désactiver un agent de transport :

```powershell
Disable-TransportAgent <TransportAgentIdentity>
```

Cet exemple désactive l'agent de transport « Agent de transport Fabirkam » dans le service de transport sur un serveur de boîtes aux lettres.

```powershell
Disable-TransportAgent "Fabrikam Transport Agent"
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement désactivé un agent de transport, exécutez la commande `Get-TransportAgent | Format-List Name,Enabled` et vérifiez que l'agent est désactivé.

## Utiliser l'environnement de ligne de commande pour afficher les agents de transport

Pour afficher une liste récapitulative de tous les agents de transport, exécutez la commande suivante :

```powershell
Get-TransportAgent
```

Pour afficher la configuration détaillée d'un agent de transport particulier, exécutez la commande suivante :

```powershell
Get-TransportAgent <TransportAgentIdentity> | Format-List
```

Cet exemple fournit la configuration détaillée de l'agent de transport appelé « Agent de règles de transport ».

```powershell
Get-TransportAgent "Transport Rule Agent" | Format-List
```

## Utiliser l’environnement de ligne de commande pour configurer la priorité d'un agent de transport

Les agents de transport dont la priorité est la plus proche de 0 traitent d’abord les messages électroniques. Cependant, l'événement SMTP dans le pipeline de transport où l'agent de transport est inscrit peut entraîner qu'un agent de priorité inférieure agisse sur le message avant un agent de priorité supérieure.

Pour modifier la priorité d’un agent de transport existant, exécutez la commande suivante :

```powershell
Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>
```

Cet exemple définit la priorité de l'agent de transport « Agent de transport Contoso » avec la valeur 3 dans le service de transport sur un serveur de boîtes aux lettres.

```powershell
Set-TransportAgent "Contoso Transport Agent" -Priority 3
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré la priorité d'un agent de transport, exécutez la commande `Get-TransportAgent | Format-List Name,Priority` et vérifiez sa valeur.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour désinstaller un agent de transport

Lorsque l'agent de transport est désinstallé, Exchange annule l'enregistrement des fichiers DLL utilisés avec l'agent. Exchange ne supprime pas de fichiers, de clés de registre ou tout autre objet ajouté par l'installation de l'agent de transport.

Pour désinstaller un agent de transport, exécutez la commande suivante :

```powershell
Uninstall-TransportAgent <TransportAgentIdentity>
```

Cet exemple désinstalle l'agent de transport « Agent de transport Fabrikam » du service de transport sur un serveur de boîtes aux lettres.

```powershell
Uninstall-TransportAgent "Fabrikam Transport Agent"
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement désinstallé l'agent de transport, exécutez la commande `Get-TransportAgent` et vérifiez l'absence de l'agent.

