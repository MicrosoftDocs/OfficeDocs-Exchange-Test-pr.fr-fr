---
title: 'Recherche des URL interne et externe du Centre d’administration Exchange'
TOCTitle: Recherche des URL interne et externe du Centre d'administration Exchange
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50477978
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recherche des URL interne et externe du Centre d'administration Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-04_

Étant donné que le Centre d'administration Exchange (CAE) est une console de gestion basée sur le web dans Exchange Server 2013, vous y accédez en utilisant l'URL du répertoire virtuel du Panneau de configuration Exchange (ECP) dans un navigateur Internet. Cette rubrique vous montre comment trouver l'URL du répertoire virtuel du Panneau de configuration Exchange.

> [!NOTE]
> Le Panneau de configuration Exchange est l'interface utilisateur web développée pour Exchange Server 2010. Les cmdlets du CAE pour les répertoires virtuels utilisent toujours « ECP » dans le nom, et ces cmdlets peuvent être utilisées pour gérer les répertoires virtuels de l'ECP de Exchange 2010 et de Exchange 2013.


Pour en savoir plus sur le CAE, consultez la rubrique [Centre d’administration Exchange dans Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 5 minutes.

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange pour effectuer cette procédure. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Connectivité du centre d'administration Exchange» dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour trouver les URL internes et externes du répertoire virtuel de l'ECP

Cet exemple renvoie le nom du répertoire virtuel de l'ECP, une URL interne et une URL externe dans une liste mise en forme.

```powershell
Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL
```

Quand la commande a été exécutée, utilisez les valeurs *InternalURL* ou *ExternalURL* dans votre navigateur Internet pour lancer le CAE.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Get-EcpVirtualDirectory](https://technet.microsoft.com/fr-fr/library/dd351058\(v=exchg.150\)).

