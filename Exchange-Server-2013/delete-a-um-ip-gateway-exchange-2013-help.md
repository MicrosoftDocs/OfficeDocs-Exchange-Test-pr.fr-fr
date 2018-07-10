---
title: 'Supprimer une passerelle IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Supprimer une passerelle IP de messagerie unifiée
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50478232
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supprimer une passerelle IP de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-21_

Quand vous supprimez une passerelle IP de messagerie unifiée, les serveurs Exchange ne peuvent plus accepter d'appels entrants de la passerelle VoIP, du protocole SIP à extension PBX, du PBX IP ou du contrôleur de frontière de session (SBC) associés à la passerelle IP de messagerie unifiée.

> [!NOTE]
> Vous ne devez supprimer une passerelle IP de messagerie unifiée que lorsque vous avez pleinement compris les implications issues de la désactivation d'une passerelle VoIP, un PBX IP ou un SBC.


Pour les autres tâches relatives aux passerelles IP de messagerie unifiée, consultez la rubrique [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour supprimer une passerelle IP de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à supprimer, puis cliquez sur **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer").

2.  dans la page **Avertissement**, cliquez sur **Oui**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer une passerelle IP de messagerie unifiée

Cet exemple permet de supprimer la passerelle IP de messagerie unifiée intitulée `MyUMIPGateway`.

    Remove-UMIPGateway -Identity MyUMIPGateway

