---
title: 'Modifier le plan de numérotation de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Modifier le plan de numérotation de messagerie unifiée
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50478068
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier le plan de numérotation de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-05_

Dans certaines situations, vous pouvez avoir besoin de déplacer un utilisateur à extension messagerie unifiée vers un autre plan de numérotation de messagerie unifiée ou de modifier le plan de numérotation qui est associé à cet utilisateur. Vous pouvez, par exemple, vouloir déplacer un utilisateur à extension messagerie unifiée depuis un plan de numérotation des numéros de poste vers un plan de numérotation URI SIP.

Pour modifier le plan de numérotation de messagerie unifiée, il sera nécessaire de désactiver l'utilisateur pour la messagerie unifiée, puis d'activer le nouveau plan de numérotation de messagerie unifiée. Ceci est dû au fait que plusieurs plans de numérotation peuvent avoir des exigences et des paramètres différents, comme différentes longueurs de poste ou différents types d’URI. Par exemple, des plans de numérotation URI SIP exigent qu’un identificateur de ressources SIP soit attribué à chaque boîte aux lettres à extension messagerie unifiée, mais les plans de numérotation des numéros de poste ne l’exigent pas. De plus, chaque boîte aux lettres de messagerie unifiée contient des références à la fois vers le plan de numérotation de messagerie unifiée et la stratégie de boîtes aux lettres de messagerie unifiée. La stratégie de boîte aux lettres de messagerie unifiée contient à son tour des références vers le plan de numérotation de messagerie unifiée. Si vous modifiez l’adresse proxy principale d’un utilisateur à extension messagerie unifiée pour qu’elle pointe vers un autre plan de numérotation, la boîte aux lettres de messagerie unifiée est alors dans un état incohérent.

Pour d’autres tâches de gestion relatives aux utilisateurs activés pour la messagerie vocale, consultez la rubrique [Voix des procédures de l'utilisateur à extension messagerie](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Boîtes aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer cette procédure, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Avant d’effectuer ces procédures, vérifiez que le destinataire Exchange existant est à extension messagerie unifiée. Pour obtenir la procédure détaillée, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

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


## Comment procéder ?

## Étape 1 : Créer le nouveau plan de numérotation de messagerie unifiée

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous migrez les utilisateurs à extension messagerie unifiée vers Microsoft Office Communications Server 2007 R2 ou vers Microsoft Lync Server, vous devez d’abord créer un plan de numérotation URI SIP.</td>
</tr>
</tbody>
</table>


Pour plus d'informations, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

## Étape 2 : Désactiver l'utilisateur pour la messagerie unifiée

Pour plus d'informations, consultez la rubrique [Désactiver la messagerie vocale d'un utilisateur](disable-voice-mail-for-a-user-exchange-2013-help.md).

## Étape 3 : Activez l’utilisateur pour la messagerie unifiée sur le nouveau plan de numérotation de messagerie unifiée

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous déplacez des utilisateurs vers un environnement Office Communications Server 2007 R2 ou Lync Server, vous devez également préciser un identificateur de ressources SIP pour l’utilisateur en l'activant pour la messagerie unifiée. Vous devez aussi sélectionner la stratégie de boîte aux lettres de messagerie unifiée associée à un plan de numérotation SIP.</td>
</tr>
</tbody>
</table>


Pour plus d'informations, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md).

