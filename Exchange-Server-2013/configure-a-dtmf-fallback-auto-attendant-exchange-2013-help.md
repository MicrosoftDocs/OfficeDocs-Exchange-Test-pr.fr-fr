---
title: 'Configurer un standard de standard automatique de secours DTMF: Exchange 2013 Help'
TOCTitle: Configurer un standard de standard automatique de secours DTMF
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50478969
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer un standard de standard automatique de secours DTMF

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-30_

Vous pouvez configurer un standard automatique de messagerie unifiée à reconnaissance vocale doté d'un standard automatique de secours DTMF (numérotation en fréquences vocales). Un standard automatique de secours DTMF est utilisé lorsque le standard automatique de messagerie unifiée à reconnaissance vocale ne comprend pas ou ne reconnaît pas les entrées vocales de l'appelant. En cas d'utilisation d'un standard automatique de secours DTMF, l'appelant doit utiliser des entrées DTMF, également appelées entrées à tonalité, pour naviguer dans le système de menus du standard automatique, épeler un nom d'utilisateur ou utiliser un message de menu personnalisé. Si aucun standard automatique de secours DTMF n'a été configuré et si le nombre maximal d'entrées vocales est dépassé parce que le système n'a pas compris ce que disait l'appelant, le système répond par le message d'assistance vocale suivant : « Désolé de n'avoir pu vous aider. Veuillez rappeler plus tard. »

Par défaut, un standard automatique n'est pas à reconnaissance vocale lorsque vous le créez. Après que vous avez activé la reconnaissance vocale pour le standard automatique, les appelants ne peuvent plus utiliser que des commandes vocales pour naviguer dans le système de menus du standard automatique car les entrées à tonalité n’opèrent plus. Il est recommandé de configurer un standard automatique de secours DTMF pour chaque standard automatique à reconnaissance vocale, de sorte que les appelants puissent utiliser des entrées à tonalité si le standard automatique à reconnaissance vocale ne reconnaît ou ne comprend pas les mots qu'ils prononcent. Par ailleurs, il est déconseillé d'activer la reconnaissance vocale sur un standard automatique de secours DTMF.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : Moins d’une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE (Centre d’administration Exchange) pour configurer un standard automatique à reconnaissance vocale avec un standard automatique de secours DTMF

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans la liste, sélectionnez le plan de numérotation de MU que vous voulez modifier et cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Sur la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée pour lequel créer un standard automatique de secours DTMF. Dans la barre d’outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sur la page **Standard automatique de messagerie unifiée** \> **Général**, cochez la case en regard de l'option **Utilisez ce standard automatique lorsque les commandes vocales ne fonctionnent pas correctement**, puis cliquez sur **Parcourir**.

4.  Sur la page **Sélectionner un standard automatique de messagerie unifiée**, sélectionnez le standard automatique que vous voulez utiliser comme standard automatique de secours DTMF, puis cliquez sur **Enregistrer**.

> [!NOTE]
> Vous devez commencer par activer la reconnaissance vocale du standard automatique avant de rechercher un standard automatique de secours DTMF que vous avez configuré.


## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer un standard automatique à reconnaissance vocale avec un standard automatique de secours DTMF

Cet exemple configure un standard automatique de messagerie unifiée nommé `MySpeechEnabledAA` pour qu'il utilise un standard automatique de secours DTMF nommé `MyDTMFAA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

