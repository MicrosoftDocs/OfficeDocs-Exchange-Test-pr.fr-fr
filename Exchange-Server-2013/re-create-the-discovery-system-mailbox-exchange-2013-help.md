---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50478265
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Re-create the Discovery system mailbox

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-01-17_

La découverte électronique sur place utilise une boîte aux lettres système pour stocker les métadonnées de recherche de la découverte électronique sur place. Le nom affiché de cette boîte aux lettres système de découverte est **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**. Les boîtes aux lettres système n’étant pas visibles dans le centre d'administration Exchange (EAC) ni dans les listes d’adresses Exchange, elles sont rarement supprimées par inadvertance.

Toutefois, si la boîte aux lettres système de découverte est supprimée accidentellement, les gestionnaires de recherche ne seront pas en mesure d’effectuer des recherches dans la découverte électronique sur place ni de gérer les recherches existantes. Dans ce cas, pour activer la fonctionnalité de découverte électronique, vous devez recréer la boîte aux lettres système de découverte.

## Ce que vous devez savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utiliser l’environnement de ligne de commande pour recréer la boîte aux lettres système de détection

1.  Supprimez le compte utilisateur SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} à partir d’Active Directory, s’il existe. Par défaut, le programme d’installation Exchange Server 2013 crée la boîte aux lettres dans le conteneur Utilisateurs d’Active Directory. Pour plus de détails sur la suppression d’un compte utilisateur à partir d’Active Directory, voir [Supprimer un compte d’utilisateur](https://go.microsoft.com/fwlink/p/?linkid=215850).

2.  Utilisez le Shell pour activer la boîte aux lettres système de découverte.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous ne pouvez pas utiliser le centre d'administration Exchange (EAC) pour activer la boîte aux lettres système de découverte.<br />
    La commande suivante doit être exécutée dans le même répertoire où vous avez extrait le support d’installation Exchange.</td>
    </tr>
    </tbody>
    </table>
    
    Pour recréer la boîte aux lettres système de découverte, exécutez la commande suivante :
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez recréé la boîte aux lettres système de découverte avec succès, utilisez la cmdlet **Get-Mailbox** avec le commutateur *Arbitration* pour récupérer les boîtes aux lettres système. Affichez les résultats de la commande pour vérifier que la boîte aux lettres système `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` a été recréée.

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

