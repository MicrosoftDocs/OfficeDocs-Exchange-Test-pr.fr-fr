---
title: 'Supprimer une approbation de fédération: Exchange 2013 Help'
TOCTitle: Supprimer une approbation de fédération
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50479343
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une approbation de fédération

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-01-04_

Une approbation de fédération établit une relation d’approbation entre une organisation Microsoft Exchange 2013 et le système d’authentification Azure Active Directory, et prend en charge le partage avec d’autres organisations Exchange fédérées. La suppression d’une approbation de fédération de votre organisation Exchange locale entraîne la désactivation du partage fédéré avec d’autres organisations Exchange fédérées et avec des organisations Office 365 connectées à votre organisation dans le cadre d’un déploiement hybride. Vous devriez réfléchir attentivement aux répercussions globales d’une suppression d’approbation de fédération sur votre organisation.

Pour les autres tâches de gestion relatives aux approbations de fédération, consultez la rubrique [Procédures de fédération](federation-procedures-exchange-2013-help.md).

> [!IMPORTANT]
> Cette fonctionnalité d’Exchange Server 2013 n’est pas entièrement compatible avec les systèmes Office 365 exécutés par 21Vianet en Chine et certaines limitations de fonctionnalités peuvent s’appliquer. Pour plus d’informations, voir <a href="https://go.microsoft.com/fwlink/?linkid=313640">En savoir plus sur Office 365 exécuté par 21Vianet</a>.


## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée d’autorisations de « Fédération et certificats » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Après avoir supprimé l’approbation de fédération, vous pouvez supprimer les enregistrements TXT de votre serveur DNS public pour chaque domaine fédéré. Passez en revue les exigences de suppression d’un enregistrement TXT avec l’organisation qui héberge vos enregistrements DNS publics.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utilisation du Centre d’administration Exchange pour supprimer une approbation de fédération

1.  Sur un serveur Exchange 2013 de votre organisation sur site, accédez à **organisation** \> **partage**.

2.  Dans la section **Approbation de fédération**, cliquez sur **Supprimer**.

3.  Dans l’avertissement, cliquez sur **oui** pour confirmer la suppression de l’approbation de fédération.

4.  Une fois l’approbation de fédération supprimée, cliquez sur **Fermer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer une approbation de fédération

Cet exemple illustre la suppression de l’approbation de fédération.

```powershell
Remove-FederationTrust
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Remove-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd351153\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé l’approbation de fédération, effectuez l’une des opérations suivantes :

  - Dans le CAE, accédez à **organisation** \> **partage**. Si vous avez correctement supprimé l’approbation de fédération, seul le bouton **Activer** sera disponible sous **Approbation de fédération**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier que les informations relatives à l’approbation de fédération ne sont pas renvoyées pour votre organisation Exchange.
    
    ```powershell
Get-FederationTrust
```
    
    Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-FederationTrust](https://technet.microsoft.com/fr-fr/library/dd351262\(v=exchg.150\)).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

