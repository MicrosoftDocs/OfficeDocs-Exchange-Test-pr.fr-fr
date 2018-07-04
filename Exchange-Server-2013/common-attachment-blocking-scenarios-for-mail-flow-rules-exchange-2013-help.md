---
title: 'Scénarios courants de blocage de pièce jointe: Exchange 2013 Help'
TOCTitle: Scénarios courants de blocage de pièce jointe
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65207677
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scénarios courants de blocage de pièce jointe

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-02-23_

Votre organisation peut exiger le blocage ou le rejet de certains types de messages afin de répondre aux exigences juridiques ou de conformité, ou pour répondre à des besoins spécifiques de l’entreprise. Voici quelques exemples de scénarios courants permettant de bloquer toutes les pièces jointes que vous pouvez configurer à l’aide des règles de transport dans Exchange :

  -  
    Example 1: Block messages with attachments, and notify the sender

  -  
    Example 2: Notify intended recipients when an inbound message is blocked

  -  
    Example 3: Modify the subject line for notifications

  -  
    Example 4: Apply a rule with a time limit

Pour obtenir des exemples supplémentaires illustrant la procédure de blocage des pièces jointes spécifiques, voir :

  - [Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

Le filtre anti-programme malveillant inclut un filtre de types de pièces jointes courants. Dans le Centre d’administration Exchange (CAE), accédez à **Protection**, puis cliquez sur **Nouveau** (![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")) pour ajouter des filtres. Sur le portail Exchange Online, accédez à **Protection**, puis sélectionnez **Filtre anti-programme malveillant**.

Pour commencer à mettre en place un de ces scénarios afin de bloquer certains types de message, procédez comme suit :

1.  Connectez-vous au Centre d’administration Exchange.

2.  Accédez à **Flux de messagerie** \>**Règles**.

3.  Cliquez sur **Nouveau** (![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")), puis sélectionnez **Créer une règle**.

4.  Dans la zone **Nom**, spécifiez un nom pour la règle, puis cliquez sur **Autres options**.

5.  Sélectionnez les conditions et les actions souhaitées.

**Remarque** : dans le CAE, la plus petite taille de pièce jointe que vous pouvez entrer est 1 kilo-octet, qui doit détecter la plupart des pièces jointes. Toutefois, si vous souhaitez détecter toutes les pièces jointes possibles quelle que soit leur taille, vous devez utiliser PowerShell pour régler la taille de pièce jointe sur 1 octet après avoir créé la règle dans le CAE. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).Pour apprendre à utiliser Windows PowerShell afin de vous connecter à Exchange Online Protection, consultez la rubrique [Connexion à Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=627290).

Remplacez *\<Rule Name\>* par le nom de la règle existante et exécutez la commande suivante pour définir la taille de pièce jointe sur 1 octet :

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

Une fois que vous avez réglé la taille de pièce jointe sur 1 octet, la valeur affichée pour la règle dans le CAE est **0,00 Ko**.

## Exemple 1 : Bloquez les messages contenant des pièces jointes et informez-en l’expéditeur

Si vous ne voulez pas que les membres de votre organisation envoient ou reçoivent des pièces jointes, vous pouvez configurer une règle de transport pour bloquer tous les messages en contenant.

Dans cet exemple, tous les messages contenant des pièces jointes envoyés vers ou à partir de l’organisation sont bloqués.

![Règle qui bloque toutes les pièces jointes](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "Règle qui bloque toutes les pièces jointes")

Si vous souhaitez simplement bloquer le message, vous pouvez arrêter le traitement des règles une fois que cette règle est mise en correspondance. Faites défiler la boîte de dialogue vers le bas, puis cochez la case **Ne plus traiter de règles**.

## Exemple 2 : Prévenez les destinataires lorsqu’un message entrant est bloqué

Si vous souhaitez rejeter un message et informer le destinataire de ce qu’il s’est passé, vous pouvez utiliser l’action **Avertir le destinataire par message**.

Vous pouvez inclure des espaces réservés dans le message de notification afin qu’il comprenne des informations sur le message d’origine. Vous devez placer les espaces réservés entre deux symboles de pourcentage (%%) ; ainsi, lors de l’envoi du message de notification, les espaces réservés sont remplacés par les informations du message d’origine. Vous pouvez également utiliser la mise en forme HTML simple, comme \<br\>, \<b\>, \<i\> et \<img\> dans le message.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Type d’information</strong></p></td>
<td><p><strong>Espace réservé</strong></p></td>
</tr>
<tr class="even">
<td><p>Expéditeur du message.</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>Destinataires indiqués sur la ligne « À ».</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>Destinataires indiqués sur la ligne « Cc ».</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>Objet du message d’origine</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>En-têtes du message d’origine. Ceci est semblable à la liste des en-têtes dans une notification d’état de remise (DSN) générée pour le message d’origine.</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>Date d’envoi du message d’origine.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


Dans cet exemple, tous les messages contenant des pièces jointes et envoyés à des membres de votre organisation sont bloqués, et le destinataire en est informé.

![Règle qui avertit les destinataires lorsqu’un message entrant est bloqué](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Règle qui avertit les destinataires lorsqu’un message entrant est bloqué")

## Exemple 3 : Modifier la ligne d’objet pour les notifications

Lorsqu’une notification est envoyée au destinataire, la ligne d’objet est l’objet du message d’origine. Si vous souhaitez modifier l’objet afin qu’il soit plus clair pour le destinataire, vous devez utiliser deux règles de transport :

  - La première règle ajoute le mot « non remis » au début de l’objet des messages contenant des pièces jointes.

  - La deuxième règle bloque le message et envoie un message de notification à l’expéditeur à l’aide du nouvel objet du message d’origine.

> [!NOTE]
> Les deux règles doivent avoir des conditions identiques. Les règles sont traitées dans l’ordre, afin que la première règle ajoute le mot « non remis » et que la deuxième bloque le message et informe le destinataire.


Voici ce que la première règle donnera si vous souhaitez ajouter « non remis » à l’objet :

![Règle qui ajoute Undeliverable aux messages contenant des pièces jointes](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "Règle qui ajoute Undeliverable aux messages contenant des pièces jointes")

La deuxième règle, quant à elle, effectue le blocage et envoie la notification (même règle que dans l’exemple 2) :

![Règle qui avertit les destinataires lorsqu’un message entrant est bloqué](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Règle qui avertit les destinataires lorsqu’un message entrant est bloqué")

## Exemple 4 : Appliquer une règle avec une limite de temps

Si un programme malveillant apparaît, vous devez appliquer une règle avec une limite de temps pour bloquer temporairement les pièces jointes. Par exemple, la règle suivante a un jour et une heure de début et de fin :

![Règle avec une limite de temps](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "Règle avec une limite de temps")

## Voir aussi


[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))  
[Règles de flux de messagerie (règles de transport) dans Exchange Online Protection](https://technet.microsoft.com/fr-fr/library/dn271424\(v=exchg.150\))

