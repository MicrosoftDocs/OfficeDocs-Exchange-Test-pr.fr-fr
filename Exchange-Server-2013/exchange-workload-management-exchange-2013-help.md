---
title: 'Gestion de la charge de travail Exchange: Exchange 2013 Help'
TOCTitle: Gestion de la charge de travail Exchange
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50477691
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion de la charge de travail Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-11-16_

Une charge de travail Exchange est une fonctionnalité, un protocole ou un service de serveur Exchange explicitement défini à des fins de gestion des ressources système Exchange. Chaque charge de travail Exchange consomme des ressources système telles que le processeur, des opérations de base de données de boîtes aux lettres ou des requêtes Active Directory pour exécuter les demandes des utilisateurs ou des tâches en arrière-plan. Des exemples de charge de travail Exchange sont Outlook Web App, Exchange ActiveSync, la migration de boîte aux lettres et les Assistants de boîtes aux lettres.

Vous gérez les charges de travail en contrôlant la manière dont les ressources sont consommées par des utilisateurs individuels (cette approche est parfois appelée « limitation utilisateur » dans Exchange 2010). Il était déjà possible de contrôler la façon dont les ressources système Exchange étaient consommées par des utilisateurs individuels dans Exchange Server 2010. Cette fonctionnalité a été étendue pour Exchange Server 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La gestion des charges de travail via le contrôle de l’état des ressources système sur les serveurs Exchange de votre organisation ne doit s’effectuer que sous la direction du Support technique et Service clientèle Microsoft.</td>
</tr>
</tbody>
</table>


## Gestion des charges de travail en contrôlant la manière dont les ressources sont consommées par des utilisateurs individuels

Dans Exchange 2013, la fonctionnalité de limitation a été améliorée. La fonctionnalité améliorée permet d’assurer qu’une consommation excessive de ressources par des utilisateurs individuels ne va réduire pas les performances du serveur ou l’expérience utilisateur.

Par défaut, la limitation utilisateur dans Exchange 2013 permet aux utilisateurs d'augmenter la consommation de ressources pendant de courtes périodes sans subir de réduction de bande passante. En outre, le verrouillage complet des utilisateurs qui utilisent une très grande quantité de ressources ne survient jamais ou presque. Au lieu de bloquer complètement l’exécution des opérations d’un utilisateur, la limitation intervient, et les processus sont retardés pendant de courtes périodes (comme des « microretards ») avant d’affecter sensiblement un serveur.

**Principales fonctionnalités**

Voici quelques particularités de la façon dont Exchange contrôle la consommation des ressources par des utilisateurs individuels dans Exchange 2013 :

  - **Autorisations en rafales**   Les autorisations en rafales permettent aux utilisateurs de consommer des ressources accrues pendant de courtes périodes sans percevoir de limitation.

  - **Vitesse de recharge**   La vitesse de recharge gère la consommation des ressources par vos utilisateurs à l’aide d’un système de budgétisation des ressources. Vous pouvez définir la vitesse à laquelle les budgets de ressources des utilisateurs sont rechargés. Par exemple, une valeur de 600 000 (en millisecondes) signifie que les budgets des utilisateurs sont rechargés à raison de dix minutes d’utilisation par heure.

  - **Mise en forme de trafic**   Lorsque l’utilisation des ressources par un utilisateur atteint la limite configurée sur une certaine période, cet utilisateur est retardé pendant de très courtes périodes bien avant d’affecter sensiblement un serveur. Généralement, les utilisateurs ne remarquent pas ces « microretards ». Ce processus permet à Exchange 2013 de mettre en forme le trafic efficacement sans bloquer la productivité des utilisateurs. La mise en forme du trafic a moins d'impact sur vos utilisateurs que le verrouillage anticipé, et elle réduit sensiblement les risques de blocage.

  - **Utilisation maximale**   Dans de rares circonstances, un utilisateur peut consommer une quantité très élevée de ressources sur une courte période. Par mesure de précaution, un utilisateur qui atteint un seuil maximal d'utilisation peut voir son utilisation des ressources temporairement bloquée. Les utilisateurs temporairement empêchés d'utiliser des ressources sont débloqués dès que les budgets de leur utilisation sont rechargés.

Pour obtenir la liste des cmdlets permettant de contrôler la manière dont les ressources sont consommées par des utilisateurs individuels, consultez la section « Cmdlets pour contrôler la manière dont les ressources sont utilisées par des utilisateurs individuels », plus loin dans cette rubrique.

**Considérations relatives à la fonctionnalité de limitation et au déploiement d'Exchange 2013**

Si vous effectuez une nouvelle installation d'Exchange 2013 ou si vous installez Exchange 2013 dans un environnement de coexistence comprenant des ordinateurs Exchange 2010, tous les utilisateurs ayant des boîtes aux lettres sur des ordinateurs exécutant Exchange 2013 sont limités à l'aide de la nouvelle fonctionnalité de limitation d'Exchange 2013. Toutefois, les utilisateurs d'Exchange 2010 demeurent limités par la fonctionnalité de limitation d'Exchange 2010 lorsqu'ils accèdent à leurs boîtes aux lettres via des serveurs d'accès au client Exchange 2010.

Quand Exchange 2013 est installé dans un environnement de coexistence, le processus d'installation d'Exchange 2013 peut tenter de transposer certains des paramètres de limitation définis dans votre configuration d'Exchange 2010. Toutefois, la fonctionnalité de limitation d'Exchange 2013 est si différente que les paramètres de limitation hérités n'affectent généralement pas le fonctionnement de la limitation dans Exchange 2013.

**Gestion des stratégies de limitation à l'aide d'étendues**

Comme dans Exchange 2010, il n’y a qu’une stratégie de limitation par défaut dans Exchange 2013. Dans Exchange 2013, la stratégie de limitation par défaut est appelée **GlobalThrottlingPolicy**. Cette stratégie a l'étendue **Global**. Les autres étendues de limitation utilisateur disponibles sont **Organization** et **Regular**. En raison de l'introduction de l'affectation de l'étendue pour les stratégies de limitation utilisateur pour Exchange 2013, vous gérez les stratégies de limitation différemment par rapport à Exchange 2010. La stratégie **GlobalThrottlingPolicy** définit les paramètres de limitation par défaut de départ pour tous les utilisateurs nouveaux et existants dans votre organisation, sauf si vous avez personnalisé des stratégies de limitation pour votre organisation. Dans de nombreux scénarios classiques de déploiement d'Exchange, la stratégie **GlobalThrottlingPolicy** convient pour gérer vos utilisateurs.

Nous recommandons vivement de ne pas personnaliser les paramètres de limitation en modifiant la stratégie **GlobalThrottlingPolicy**. Au lieu de cela, vous devez créer des stratégies de limitation supplémentaires. La création de stratégies de limitation supplémentaires vous aide à mieux gérer vos charges de travail. Elle évite également le remplacement de modifications de paramètres de stratégie de limitation par des mises à jour Exchange 2013 ultérieures.

Pour personnaliser les paramètres de limitation qui s'appliquent à tous les utilisateurs de votre organisation, créez une nouvelle stratégie de limitation avec l'affectation de l'étendue **Organization**. Dans les nouvelles stratégies ayant une étendue Organisationnelle, vous devez définir uniquement les paramètres de limitation qui diffèrent de ceux de la stratégie **GlobalThrottlingPolicy**. Pour personnaliser les paramètres de limitation qui s'appliquent uniquement à des utilisateurs spécifiques au sein de votre organisation, créez une nouvelle stratégie de limitation avec l'affectation de l'étendue **Regular**. Dans les nouvelles stratégies ayant une étendue Ordinaire, vous devez définir uniquement les paramètres de limitation qui diffèrent de ceux de la stratégie **GlobalThrottlingPolicy** et de toute autre stratégie organisationnelle. Cela vous permet d'hériter du reste des paramètres de la stratégie **GlobalThrottlingPolicy** et de bénéficier des mises à jour des stratégies de limitation ajoutées aux mises à jour Exchange ultérieures.

## Gestion des paramètres de limitation de la charge de travail

Vous gérez les paramètres de limitation de la charge de travail Exchange à l'aide de l'environnement de ligne de commande Exchange Management Shell.

**Cmdlets pour contrôler la manière dont les ressources sont utilisées par des utilisateurs individuels**

Vous gérez les paramètres de limitation avec les cmdlets suivantes introduites dans Exchange 2010 :

Gérer des stratégies de limitation

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/fr-fr/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/fr-fr/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/fr-fr/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/fr-fr/library/dd298094\(v=exchg.150\))

Affecter des stratégies de limitation

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/fr-fr/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/fr-fr/library/ff459231\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les cmdlets de gestion de la charge de travail système <strong>*-ResourcePolicy</strong>, <strong>*-WorkloadManagementPolicy</strong> et <strong>*-WorkloadPolicy</strong> sont déconseillées. Les paramètres de gestion de la charge de travail système ne doivent être personnalisés que sous la direction du Support technique et Service clientèle Microsoft.</td>
</tr>
</tbody>
</table>

