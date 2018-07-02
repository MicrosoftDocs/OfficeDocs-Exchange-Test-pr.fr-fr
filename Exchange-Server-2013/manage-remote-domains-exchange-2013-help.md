---
title: 'Gestion des domaines distants: Exchange 2013 Help'
TOCTitle: Gestion des domaines distants
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52057062
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: HT
---

# Gestion des domaines distants

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-13_

Les domaines distants sont des domaines SMTP externes à votre organisation Microsoft Exchange. Vous pouvez créer des entrées de domaine distant pour définir les paramètres des messages transférés entre votre organisation Exchange et des domaines externes spécifiques. Les paramètres de l'entrée de domaine distant pour un domaine externe spécifique remplacent les paramètres du domaine distant par défaut qui s'appliquent normalement à tous les destinataires externes. Les paramètres du domaine distant s'appliquent à l'ensemble de l'organisation Exchange.

Si vous supprimez une entrée de domaine distant, les paramètres de transfert de message ne s'appliquent plus aux messages envoyés au domaine distant. La suppression d'une entrée de domaine distant ne désactive pas le flux de messagerie vers le domaine distant. Suite à la suppression d'une entrée de domaine distant, les paramètres de configuration définis pour le domaine distant par défaut s'appliquent aux nouveaux messages envoyés à ce domaine. Vous ne pouvez pas supprimer le domaine distant par défaut.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Domaines distants » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Vous ne pouvez pas créer un domaine distant pour un espace d'adresse configuré comme un domaine accepté dans votre organisation. Par exemple, si votre organisation accepte du courrier provenant de fabrikam.com, vous ne pouvez pas créer un domaine distant pour fabrikam.com.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que voulez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un domaine distant

Pour créer une nouvelle entrée de domaine distant, utilisez la syntaxe suivante.

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

Cet exemple crée une entrée de domaine distant pour les messages envoyés au domaine contoso.com.

    New-RemoteDomain -Name Contoso -DomainName contoso.com

Cet exemple crée une entrée de domaine distant pour les messages envoyés au domaine fabrikam.com et à tous les sous-domaines.

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez créé correctement un domaine distant, procédez comme suit :

1.  Exécutez la commande **Get-RemoteDomain** et vérifiez que le domaine distant est répertorié.

2.  Exécutez la commande `Get-RemoteDomain <Remote Domain Name> | Format-List` pour vérifier les paramètres de votre nouveau domaine distant. Envoyez un message de test à un destinataire de l'espace d'adresse spécifié dans la nouvelle entrée de domaine distant. Vérifiez également que les paramètres de message correspondent à ceux spécifiés par la nouvelle entrée de domaine distant.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer un domaine distant

Configurez les paramètres de l'entrée do domaine distant à l'aide de la cmdlet **Set-RemoteDomain**. De nombreux paramètres de messages sont disponibles, notamment ceux relatifs aux réponses automatiques ou au format et au codage des messages Pour plus d'informations, consultez la rubrique [Set-RemoteDomain](https://technet.microsoft.com/fr-fr/library/aa997857\(v=exchg.150\)).

Pour configurer les domaines distants pour des scénarios spécifiques, consultez les rubriques suivantes :

  - [Configurer des réponses d’absence du bureau de domaine distant](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [Configurer des réponses automatiques de domaine distant](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [Configuration du rapport de message de domaine distant](configure-remote-domain-message-reporting-exchange-2013-help.md)

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un domaine distant

Pour supprimer une entrée de domaine distant, utilisez la syntaxe suivante.

    Remove-RemoteDomain <RemoteDomainName>

Cet exemple supprime l'entrée de domaine distant appelée Contoso.

    Remove-RemoteDomain Contoso

## Comment savoir si cela a fonctionné ?

Pour vérifier que le domaine distant a bien été supprimé, procédez comme suit :

1.  Exécutez la commande **Get-RemoteDomain** et vérifiez que le domaine distant n'est pas répertorié.

2.  Exécutez la commande `Get-RemoteDomain Default | Format-List` pour vérifier les paramètres du domaine distant par défaut. Envoyez un message de test à un destinataire de l'espace d'adresse spécifié dans le domaine distant supprimé. Vérifiez également que les paramètres de message correspondent à ceux spécifiés par le domaine distant par défaut.

