---
title: 'Désactiver les appels sortants sur les passerelles IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Désactiver les appels sortants sur les passerelles IP de messagerie unifiée
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 50478819
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Désactiver les appels sortants sur les passerelles IP de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-13_

Vous pouvez activer ou désactiver les appels sortants sur une passerelle IP de messagerie unifiée. Quand vous désactivez l'option **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée** dans les propriétés de la passerelle IP de messagerie unifiée, vous configurez cette passerelle IP pour qu'elle n'accepte pas les appels sortants et ne les envoie pas sur une passerelle VoIP, un PBX IP ou un contrôleur de frontière de session (SBC). Bien que le paramètre **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée** détermine si la passerelle IP de messagerie unifiée peut établir des appels sortants pour les utilisateurs, il n'affecte pas les transferts d'appels ou les appels entrants provenant d'une passerelle VoIP, d'un PBX IP ou d'un SBC.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange pour désactiver les appels sortants pour une passerelle IP de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Passerelle IP de messagerie unifiée**, décochez la case en regard de **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée**.

3.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour désactiver les appels sortants pour une passerelle IP de messagerie unifiée

Cet exemple désactive les appels sortants sur une passerelle IP de messagerie unifiée nommée `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

