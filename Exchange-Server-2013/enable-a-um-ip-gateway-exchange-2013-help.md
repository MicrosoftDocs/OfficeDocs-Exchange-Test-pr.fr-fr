---
title: 'Activer une passerelle IP de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Activer une passerelle IP de messagerie unifiée
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50477686
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer une passerelle IP de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Par défaut, lorsqu’une passerelle IP de messagerie unifiée (MU) est créée, elle présente l’état Activé. Toutefois, vous devrez peut-être désactiver la passerelle IP de messagerie unifiée pour la mettre hors connexion et ne pas autoriser les appels entrants ou sortants. Après avoir créé une passerelle IP de messagerie unifiée, vous pouvez contrôler son exécution et sa fonctionnalité en définissant sa variable d’état sur Activé ou Désactivé.

Pour les autres tâches de gestion relatives aux passerelles IP de messagerie unifiée, voir [Procédures de passerelle IP de messagerie unifiée](um-ip-gateway-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Passerelles IP de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’une passerelle IP de messagerie unifiée a été créée et qu’elle a été désactivée. Pour obtenir la procédure détaillée, voir [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE pour activer une passerelle IP de messagerie unifiée

1.  Dans le CAE, accédez à \> **Messagerie unifiée** \> **Passerelles IP de messagerie unifiée**, sélectionnez la passerelle IP de messagerie unifiée à activer, puis cliquez sur la **flèche Haut**![Icône flèche vers le haut](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icône flèche vers le haut").

2.  Sur la page **Avertissement**, cliquez sur **Oui**.

## Utiliser le Shell pour activer une passerelle IP de messagerie unifiée

L’exemple de code suivant active une passerelle IP de messagerie unifiée nommée `MyUMIPGateway`.

    Enable-UMIPGateway -Identity MyUMIPGateway

