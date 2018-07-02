---
title: 'Restaurer un modèle de détails sur la configuration par défaut: Exchange 2013 Help'
TOCTitle: Restaurer un modèle de détails sur la configuration par défaut
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50478593
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurer un modèle de détails sur la configuration par défaut

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-12_

L’Éditeur de modèles de détails ne contient pas de bouton **Annuler** ; vous ne pouvez pas non plus utiliser de raccourci clavier pour annuler une action. Pour annuler un ajout apporté au modèle, vous devez utiliser la touche SUPPR. Pour annuler une suppression, vous devez appliquer de nouveau le paramètre. Vous pouvez également rétablir les paramètres originaux en quittant l’Éditeur de modèles de détails sans enregistrer les modifications. Pour annuler des modifications après les avoir enregistrées, vous pouvez restaurer le modèle. Lorsque vous restaurez un modèle, toute la personnalisation est perdue et la configuration originale du modèle est restaurée.

Cette rubrique décrit l’utilisation de la boîte à outils Exchange 2013 ou de l’environnement Exchange Management Shell pour restaurer la configuration par défaut d’un modèle de détails.

Pour plus d’informations sur les modèles de détails, consultez la rubrique [Modèles de détails](details-templates-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Modèles de détails » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

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


## Utiliser la boîte à outils Exchange pour restaurer la configuration par défaut d’un modèle de détails

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Microsoft Exchange Server 2013** \> **Boîte à outils Exchange**.

2.  Dans **Boîte à outils Exchange**, cliquez sur **Éditeur de modèles de détails**, puis sur le volet d’action, cliquez sur **Ouvrir l’outil**.

3.  Dans l’**Éditeur de modèles de détails** du volet d’informations, sélectionnez le modèle à restaurer, puis dans le volet d’action, cliquez sur **Restaurer**.

4.  Cliquez sur **Oui** pour confirmer la restauration du modèle à son état d’origine. Tous les éléments personnalisés seront perdus.

## Utiliser l’environnement Shell pour restaurer la configuration par défaut d’un modèle de détails

Dans cet exemple, nous montrons comment restaurer le modèle de détails United States English contacts (contacts anglais États-Unis).

    Restore-DetailsTemplate -Identity "en-US\Contact"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Restore-DetailsTemplate](https://technet.microsoft.com/fr-fr/library/bb125188\(v=exchg.150\)).

