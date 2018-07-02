---
title: 'Désactiver une passerelle IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Désactiver une passerelle IP de messagerie unifiée
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50479648
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver une passerelle IP de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-13_

Par défaut, lorsque vous créez une passerelle IP de messagerie unifiée, cette passerelle est activée. Lorsque cette passerelle est créée, pour désactiver le fonctionnement de la passerelle définissez sont état à « désactivé ». Après avoir désactivé cette passerelle, la passerelle VoIP, le PBX (Private Branch eXchange) IP ou le contrôleur de frontière de session (SBC) configuré pour l’utilisation ne peut plus traiter les appels entrants de messagerie unifiée.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, voir [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée et qu’elle est activée. Pour obtenir la procédure détaillée, voir [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md) et [Activer une passerelle IP de messagerie unifiée](enable-a-um-ip-gateway-exchange-2013-help.md).

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

## Utiliser le Centre d’administration Exchange (CAE) pour désactiver une passerelle IP de messagerie unifiée

1.  Dans le Centre d’administration Exchange (CAE), accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à désactiver, puis cliquez sur la flèche **Bas**![Icône de flèche vers le bas](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icône de flèche vers le bas").

2.  Sur la page **Avertissement**, cliquez sur **Oui**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver une passerelle IP de messagerie unifiée

Cet exemple désactive une passerelle IP de messagerie unifiée appelée `MyUMIPGateway` et l’empêche d’accepter les appels entrants provenant d’une passerelle VoIP, d’un autocommutateur IP ou d’un contrôleur de frontière de session (SBC).

    Disable-UMIPGateway -Identity MyUMIPGateway

Cet exemple désactive une passerelle IP de messagerie unifiée appelée `MyUMIPGateway` et déconnecte immédiatement tous les appels en cours.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

