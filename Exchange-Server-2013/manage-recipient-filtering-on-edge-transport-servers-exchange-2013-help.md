---
title: 'Gérer le filtrage des destinataires sur les serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Gérer le filtrage des destinataires sur les serveurs de transport Edge
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50479523
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer le filtrage des destinataires sur les serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

L'agent de filtrage des destinataires assure le filtrage des destinataires. Lorsque le filtrage des destinataires est activé sur un serveur Exchange, il filtre les messages entrants provenant d'Internet mais ne sont pas authentifiés. Ces messages sont traités comme des messages externes.

> [!NOTE]
> Bien que l’agent de filtrage des destinataires soit disponible sur les serveurs de boîtes aux lettres, vous ne devez pas le configurer. Lorsque le filtrage des destinataires sur un serveur de boîte aux lettres détecte un destinataire non valide ou bloqué dans un message qui contient d’autres destinataires valides, le message est rejeté. Si vous installez les agents de filtrage du courrier indésirable sur un serveur de boîte aux lettres, l’agent de filtrage des destinataires est activé par défaut. Cependant, il n’est configuré pour bloquer aucun destinataire. Pour plus d’informations, voir <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres</a>.


## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Le paramètre *AddressBookEnabled* de la cmdlet **Set-AcceptedDomain** active ou désactive le filtrage des destinataires dans un domaine accepté. Par défaut, le filtrage est activé pour les domaines faisant autorité et désactivé pour les domaines de relais internes et externes. Pour afficher l'état du paramètre *AddressBookEnabled* pour les domaines acceptés dans votre organisation, exécutez la commande suivante :
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - Si vous désactivez le filtrage des destinataires en utilisant la procédure de cette rubrique, le filtrage est désactivé, mais l'agent sous-jacent de filtrage des destinataires reste activé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage des destinataires

Pour désactiver le filtrage des destinataires, exécutez la commande suivante :

    Set-RecipientFilterConfig -Enabled $false

Pour activer le filtrage des destinataires, exécutez la commande suivante :

    Set-RecipientFilterConfig -Enabled $true

> [!NOTE]
> Lorsque vous désactivez le filtrage des destinataires, l'agent sous-jacent de filtrage des destinataires reste activé. Pour désactiver l'agent de filtrage des destinataires, exécutez la commande suivante : <code>Disable-TransportAgent &quot;Recipient Filter Agent&quot;</code>.


## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez bien activé ou désactivé le filtrage des destinataires :

1.  Exécutez la commande suivante :
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la liste des destinataires bloqués

Exécutez la commande suivante :

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

Cet exemple montre comment activer la liste des destinataires bloqués :

    Set-RecipientFilterConfig -BlockListEnabled $true

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez bien activé ou désactivé la liste des destinataires bloqués :

1.  Exécutez la commande suivante :
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer la liste des destinataires bloqués

Pour remplacer les valeurs existantes, exécutez la commande suivante :

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

Cet exemple montre comment configurer la liste des destinataires bloqués pour valuesmark@contoso.com et kim@contoso.com :

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

Pour ajouter ou supprimer des entrées sans modifier une valeur existante, exécutez la commande suivante :

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

Cet exemple montre comment ajouter chris@contoso.com à la liste des destinataires et supprime michelle@contoso.com de la liste des destinataires bloqués :

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que la liste des destinataires bloqués est correctement configurée :

1.  Exécutez la commande suivante :
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la recherche de destinataire

Exécutez la commande suivante :

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

Pour bloquer les messages envoyés aux destinataires qui n'existent pas dans votre organisation, exécutez la commande suivante :

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## Comment savoir si cela a fonctionné ?

Voici comment vérifier que vous avez bien activé ou désactivé la recherche de destinataire :

1.  Exécutez la commande suivante :
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

