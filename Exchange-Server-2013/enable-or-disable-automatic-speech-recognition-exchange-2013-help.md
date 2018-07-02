---
title: 'Activation ou désactivation de la reconnaissance vocale automatique: Exchange 2013 Help'
TOCTitle: Activation ou désactivation de la reconnaissance vocale automatique
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52057120
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation ou désactivation de la reconnaissance vocale automatique

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-12-12_

Vous pouvez activer votre standard automatique de messagerie unifiée pour la reconnaissance vocale automatique. Une fois la reconnaissance vocale activée, les appelants peuvent répondre oralement aux messages du standard automatique et se déplacer dans le système de menus. Par défaut, un standard automatique n'est pas à reconnaissance vocale lorsque vous le créez. Après que vous avez activé la reconnaissance vocale pour le standard automatique, les appelants ne peuvent plus utiliser que des commandes vocales pour naviguer dans le système de menus du standard automatique car les entrées à tonalité n'opèrent plus.

Même si ce n'est pas obligatoire, nous vous recommandons de configurer un standard automatique de secours DTMF (numérotation en fréquences vocales) pour chaque standard automatique à reconnaissance vocale, de façon à ce que les appelants puissent utiliser des entrées à tonalité si le standard automatique à reconnaissance vocale ne reconnaît ou ne comprend pas les mots qu'ils prononcent. Si un standard automatique de secours DTMF est configuré, l'appelant peut utiliser des entrées DTMF, également appelées entrées à tonalité, pour naviguer dans le système de menus du standard automatique, épeler un nom d'utilisateur ou utiliser un message d'assistance vocale de menu personnalisé. Il est déconseillé d'activer la reconnaissance vocale pour un standard automatique de secours DTMF.

Pour découvrir d'autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour activer la reconnaissance vocale sur un standard automatique de messagerie unifiée

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Général**, cochez la case en regard de l'option **Définir le standard automatique pour répondre aux commandes vocales** pour activer la reconnaissance vocale. Pour la désactiver, décochez la case.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer la reconnaissance vocale sur un standard automatique de messagerie unifiée

Cet exemple active la reconnaissance vocale sur le standard automatique de messagerie unifiée `MySpeechEnabled AA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

