---
title: 'Activer les appels sortants sur les passerelles IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Activer les appels sortants sur les passerelles IP de messagerie unifiée
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 50479145
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer les appels sortants sur les passerelles IP de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-13_

Si les appels sortants ont été désactivés, vous pouvez activer les appels sortants sur une passerelle IP de messagerie unifiée. En activant l’option **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée** dans les propriétés de la passerelle IP de messagerie unifiée, vous configurez celle-ci pour qu’elle accepte et envoie des appels sortants à une passerelle VoIP (Voice over IP), un PBX (Private Branch eXchange) compatible SIP (Session Initiation Protocol), un PBX IP ou un contrôleur de frontière de session (SBC). Bien que le paramètre **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée** détermine si la passerelle IP de messagerie unifiée peut établir des appels sortants pour les utilisateurs, il n’affecte pas les transferts d’appels ou les appels entrants provenant d’une passerelle VoIP, PBX activé pour SIP, IP PBX ou SBC.

L’*automate d’appels* est le terme utilisé pour décrire une situation dans laquelle un utilisateur appartenant à un plan de numérotation de messagerie unifiée établit un appel vers un utilisateur à extension messagerie unifiée faisant partie d’un plan de numérotation différent, ou vers un numéro de téléphone externe.

Pour autoriser l’automate d’appels pour les utilisateurs à extension messagerie unifiée, vous devez :

  - vérifier que la passerelle IP de messagerie unifiée autorise les appels sortants.

  - créer des groupes de règles de numérotation en créant des entrées de règle de numérotation dans le plan de numérotation de messagerie unifiée associé à la passerelle IP de messagerie unifiée.

  - ajouter les groupes de règles de numérotation appropriés à la liste des restrictions de numérotation sous **Autorisation de numérotation** dans le plan de numérotation de messagerie unifiée, un standard automatique ou une stratégie de boîte aux lettres de messagerie unifiée.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, voir [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer les appels sortants sur une passerelle IP de messagerie unifiée

1.  Dans la CCE, accédez à **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Passerelle IP de la messagerie unifiée**, activez la case à cocher en regard de **Autoriser les appels sortants via cette passerelle IP de messagerie unifiée**.

3.  Cliquez sur **Enregistrer**.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer les appels sortants sur une passerelle IP de messagerie unifiée

Cet exemple active les appels sortants sur une passerelle IP de messagerie unifiée nommée `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true

