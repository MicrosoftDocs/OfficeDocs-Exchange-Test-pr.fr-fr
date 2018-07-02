---
title: "Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires: Exchange 2013 Help"
TOCTitle: Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50479426
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-16_

Vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour créer une stratégie d'adresse de messagerie à l'aide de filtres des destinataires. Pour plus d'informations sur les stratégies d'adresse de messagerie, consultez la rubrique [Stratégies d'adresse de messagerie](email-address-policies-exchange-2013-help.md).

Pour d'autres tâches de gestion relatives aux stratégies d'adresse de courriel, voir [Procédures des stratégies d'adresse de messagerie](email-address-policy-procedures-exchange-2013-help.md).

## Que devez-vous savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Pour utiliser le paramètre *RecipientFilter* pour créer un filtre personnalisé, vous devez spécifier une chaîne pour le filtre. L'environnement de ligne de commande Exchange Management Shell utilise OPath pour la syntaxe de filtrage. OPath est un langage d'interrogation conçu pour rechercher les sources des données objet.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous utilisez un filtre des destinataires pour créer ou modifier une stratégie d'adresse de messagerie, vous ne pouvez pas utiliser le Centre d’administration Exchange (CAE) pour modifier la stratégie d'adresse de messagerie. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell. Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir <a href="https://technet.microsoft.com/fr-fr/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</a>.</td>
    </tr>
    </tbody>
    </table>


  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Stratégies d’adresses de messagerie électronique » dans la rubrique [Adresses de messagerie et carnets d’adresses](email-addresses-and-address-books-exchange-2013-help.md).

  - Avant de pouvoir utiliser un domaine d'adresse SMTP dans une stratégie d'adresse de messagerie, vous devez configurer un domaine accepté. Pour plus d'informations, voir [Domaines acceptés](accepted-domains-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Utilisez l’environnement de ligne de commande Exchange Management Shell pour créer une stratégie d’adresse de messagerie en utilisant des filtres de destinataires

Pour créer une stratégie d’adresse de messagerie à l’aide de filtres de destinataires, utilisez la syntaxe suivante.

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

Cet exemple montre la création d'une stratégie d'adresse de messagerie qui s'applique à tous les cadres et pour laquelle la partie locale de l'adresse de messagerie est constituée des deux premières lettres de leur prénom et de leur nom en entier.

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-EmailAddressPolicy](https://technet.microsoft.com/fr-fr/library/aa996800\(v=exchg.150\)).

