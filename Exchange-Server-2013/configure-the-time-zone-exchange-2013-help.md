---
title: 'Configurer le fuseau horaire: Exchange 2013 Help'
TOCTitle: Configurer le fuseau horaire
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50555366
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer le fuseau horaire

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-17_

Par défaut, le standard automatique de messagerie unifiée utilise le fuseau horaire du serveur de boîtes aux lettres sur lequel il est créé. Toutefois, dans certains cas, vous pouvez être amené à changer de fuseau horaire pour un standard automatique de messagerie unifiée. Par exemple, si vous disposez de deux plans de numérotation de messagerie unifiée et que chaque plan représente un fuseau horaire différent, vous devez configurer un standard automatique de messagerie unifiée afin que le fuseau horaire soit identique à celui du serveur de boîtes aux lettres et que l’autre standard automatique de messagerie unifiée ait un fuseau horaire différent de celui du serveur de boîtes aux lettres.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, voir [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Configuration du fuseau horaire à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans la liste affichée, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel vous souhaitez définir le fuseau horaire, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Standard automatique de messagerie unifiée**, cliquez sur **Heures d’ouverture**, puis sous **Fuseau horaire**, sélectionnez le fuseau horaire dans la liste déroulante.

4.  Pour enregistrer vos modifications, cliquez sur **OK**, puis sur **Enregistrer**.

## Utiliser l’environnement Shell pour configurer le fuseau horaire

Cet exemple montre comment définir le fuseau horaire sur la zone Pacifique pour un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

