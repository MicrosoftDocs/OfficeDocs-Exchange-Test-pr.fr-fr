---
title: 'Désactivation ou activation du service de recherche Exchange: Exchange 2013 Help'
TOCTitle: Désactivation ou activation du service de recherche Exchange
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52062941
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Désactivation ou activation du service de recherche Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-05-07_

Par défaut, le service de recherche Exchange est activé pour toutes les nouvelles bases de données de boîtes aux lettres et ne requiert aucune configuration supplémentaire. Cependant, si vous souhaitez interrompre le service de recherche Exchange de l'indexation du contenu de la boîte aux lettres, vous pouvez le désactiver pour des bases de données de boîtes aux lettres individuelles ou un serveur de boîtes aux lettres entier.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La désactivation du service de recherche Exchange influe sur les fonctionnalités et performances des recherches de texte intégral effectuées par vos utilisateurs utilisant Outlook en mode en ligne ou des appareils Windows Mobile.<br />
La fonctionnalité <a href="in-place-ediscovery-exchange-2013-help.md">Découverte électronique locale</a> s'appuie également sur le service de recherche Exchange. Si vous désactivez le service de recherche Exchange pour une base de données ou un serveur de boîtes aux lettres, les recherches eDiscovery sur place ne retourneront pas de messages de la base de données ou du serveur.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives au service de recherche Exchange, consultez la rubrique [Procédures relatives au service de recherche Exchange](exchange-search-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 1 minute

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Vous pouvez activer ou désactiver le service de recherche Exchange pour les serveurs ou les bases de données de boîtes aux lettres, mais pas pour les utilisateurs de boîtes aux lettres individuelles.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Que souhaitez-vous faire ?

## Désactivation ou activation du service de recherche Exchange pour une base de données de boîtes aux lettres

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Service de recherche Exchange » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas utiliser le Centre d'administration Exchange (CAE) pour activer ou désactiver le service de recherche Exchange associé à une base de données de boîtes aux lettres.</td>
</tr>
</tbody>
</table>


Cette commande permet de désactiver le service de recherche Exchange pour une base de données de boîtes aux lettres appelée EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

Cette commande permet d’activer le service de recherche Exchange pour une base de données de boîtes aux lettres appelée EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb123971\(v=exchg.150\)).

## Désactivation ou activation du service de recherche Exchange pour un serveur de boîtes aux lettres

Pour désactiver le service de recherche Exchange pour un serveur de boîtes aux lettres, vous devez désactiver et arrêter le service Microsoft Exchange Search. De même, pour activer le service de recherche Exchange pour un serveur de boîtes aux lettres, vous devez activer et démarrer le service Microsoft Exchange Search. Utilisez la console Services ou le Shell pour effectuer cette opération.

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gérer le service de recherche Exchange sur un serveur de boîtes aux lettres » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

**Utilisation de la console Services**

1.  Accédez à **Démarrer** \> **Outils d’administration** \> **Services**.

2.  Dans le volet d'informations **Services**, cliquez avec le bouton droit sur le service **Microsoft Exchange Search**, puis sélectionnez **Propriétés**.

3.  Sous l'onglet **Général**, dans la liste **Type de démarrage**, sélectionnez **Désactivé** pour désactiver le service ou **Automatique** pour le démarrer automatiquement.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le type de démarrage affecte le service la prochaine fois qu'il est démarré, automatiquement après que le serveur est redémarré ou manuellement. À la prochaine étape, le service est arrêté ou démarré manuellement.</td>
    </tr>
    </tbody>
    </table>


4.  Cliquez sur **Arrêter** pour arrêter le service ou sur **Démarrer** pour le démarrer.

5.  Cliquez sur **OK** pour enregistrer les modifications.

**Utilisation du Shell**

Exécutez les commandes suivantes pour arrêter et désactiver le service Microsoft Exchange Search.

    Stop-Service MSExchangeFastSearch

    Set-Service MSExchangeFastSearch -StartupType Disabled

Exécutez les commandes suivantes pour configurer le service de recherche Exchange de sorte qu’il démarre automatiquement et démarrer ensuite le service.

    Set-Service MSExchangeFastSearch -StartupType Automatic

    Start-Service MSExchangeFastSearch

