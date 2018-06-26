---
title: 'Configuration des propriétés du réseau de groupe de disponibilité de la base de données: Exchange 2013 Help'
TOCTitle: Configuration des propriétés du réseau de groupe de disponibilité de la base de données
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50477974
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration des propriétés du réseau de groupe de disponibilité de la base de données

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-10-31_

Chaque réseau de groupes de disponibilité de la base de données (DAG) présente plusieurs propriétés que vous pouvez configurer, parmi lesquelles le nom du réseau DAG, un champ de description du réseau DAG, une liste des sous-réseaux utilisés par le réseau DAG et l’activation ou non du réseau DAG pour la réplication.

Souhaitez-vous rechercher les autres tâches de gestion relatives aux groupes de disponibilité de bases de données ? Consultez la rubrique [Gestion de groupes de disponibilité de base de données](managing-database-availability-groups-exchange-2013-help.md).

## Ce que vous devez savoir avant de commencer

  - Durée d’exécution estimée : 1 minute

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de disponibilité de la base de données » dans la rubrique [Autorisations de haute disponibilité et de résilience des sites](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Vous pouvez configurer un réseau DAG seulement si la configuration automatique du réseau a été désactivée pour un DAG. Pour obtenir la procédure détaillée de désactivation d’une configuration de réseau automatique pour un groupe de disponibilité de base de données, consultez la rubrique [Configuration des propriétés du groupe de disponibilité de base de données](configure-database-availability-group-properties-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le CAE pour configurer les propriétés du réseau de groupes de disponibilité de la base de données

1.  Dans le CAE, accédez à **Serveurs** \> **Groupes de disponibilité de base de données**.

2.  Sélectionnez le DAG que vous voulez configurer, puis dans le volet d’informations, sous le réseau DAG que vous voulez configurer, choisissez :
    
      - **Désactiver la réplication** ou **Activer la réplication** Configure les paramètres de réplication du réseau DAG.
    
      - **Supprimer** Supprime un réseau DAG. Avant de pouvoir supprimer un réseau DAG, vous devez d’abord supprimer tous les sous-réseaux associés du réseau DAG.
    
      - **Afficher les détails**   Configure les propriétés du réseau DAG, telles que le nom, la description et les sous-réseaux associés du réseau DAG. Vous pouvez également afficher les interfaces réseau associées à ces sous-réseaux, et activer ou désactiver la réplication du réseau DAG.

## Utilisation de l’environnement Shell pour configurer les propriétés du réseau de groupes de disponibilité de la base de données

Cet exemple montre comment ajouter le sous-réseau 10.0.0.0 et le masque de sous-réseau 255.0.0.0 au réseau DAG MapiDagNetwork dans le groupe de disponibilité de base de données DAG1.

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré le réseau DAG, procédez comme suit :

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les paramètres de configuration du réseau DAG et vérifiez que ce dernier a été correctement configuré :
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Pour plus d'informations

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/fr-fr/library/dd298131\(v=exchg.150\))

