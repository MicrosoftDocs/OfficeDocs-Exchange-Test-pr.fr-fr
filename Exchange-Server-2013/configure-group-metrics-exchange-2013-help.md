---
title: 'Configuration des mesures de groupe: Exchange 2013 Help'
TOCTitle: Configuration des mesures de groupe
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50478490
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration des mesures de groupe

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Les infos-courrier qui fournissent des informations sur la taille des groupes de distribution et des groupes de distribution dynamique s'appuient sur des données de mesures de groupe. Les données de mesures de groupe sont générées sur les serveurs de boîtes aux lettres désignés. Pour plus d'informations sur les mesures de groupe, consultez la rubrique [Mesures de groupe et les infos-courrier](group-metrics-and-mailtips-exchange-2013-help.md).

Vous pouvez activer ou désactiver la génération des mesures de groupe sur un serveur de boîtes aux lettres.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de chaque procédure : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Mesures de groupe » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Les données de mesures de groupe sont utilisées uniquement pour les infos-courrier. Assurez-vous que les infos-courrier de mesures de groupe sont activées dans votre organisation. Pour obtenir la procédure détaillée, consultez la rubrique [Gérer les infos-courrier pour les relations de l’organisation](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

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


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la génération des mesures de groupe

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Par défaut, les données de mesures de groupe sont générées sur un serveur responsable de la génération du carnet d'adresses en mode hors connexion. Ces exemples sont uniquement nécessaires aux organisations qui n'utilisent pas les carnets d'adresses en mode hors connexion.</td>
</tr>
</tbody>
</table>


Pour activer ou désactiver la génération des mesures de groupe sur un serveur de boîtes aux lettres, exécutez la commande suivante :

    Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>

Cet exemple active la génération des mesures de groupe sur le serveur de boîtes aux lettres MBX1.

    Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé ou désactivé la génération des mesures de groupe dans une organisation qui n'utilise pas les carnets d'adresses en mode hors connexion, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration

2.  Vérifiez que le paramètre affiché est le paramètre que vous avez configuré.

