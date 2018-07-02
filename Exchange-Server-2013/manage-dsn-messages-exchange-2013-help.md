---
title: "Gestion des messages de notification d'état de remise (DSN): Exchange 2013 Help"
TOCTitle: Gestion des messages de notification d'état de remise (DSN)
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50477660
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- modification du message de notification d'échec de remise
- modification du message de quota
- modification du message de rejet
- modification du message système
ms.translationtype: HT
---

# Gestion des messages de notification d'état de remise (DSN)

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-02-20_

Microsoft Exchange Server 2013 utilise des notifications d'état de remise (DSN) pour fournir des notifications d'échec de remise et d'autres messages d'état aux expéditeurs de messages. Vous pouvez utiliser les DSN intégrés ou créer des messages DSN personnalisés pour répondre aux exigences de votre organisation.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « DSN » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas supprimer un message DSN intégré inclus dans Exchange. Pour modifier un message DSN intégré, vous devez créer un message DSN personnalisé pour le code DSN approprié que vous souhaitez personnaliser. Quand vous supprimez un message DSN personnalisé, le code DSN associé au message rétablit le message DSN intégré inclus dans Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour afficher les messages DSN intégrés et personnalisés

Pour afficher un résumé de tous les messages DSN intégrés inclus avec Exchange 2013, exécutez la commande suivante :

    Get-SystemMessage -Original

Pour afficher une liste récapitulative de tous les messages DSN personnalisés dans votre organisation, exécutez la commande suivante :

    Get-SystemMessage

Pour afficher des informations détaillées pour le message DSN personnalisé correspondant au code DSN 5.1.2 envoyé aux expéditeurs internes en anglais, exécutez la commande suivante :

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour créer un message DSN personnalisé

Exécutez la commande suivante :

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

Cet exemple montre comment créer un message DSN personnalisé en texte brut pour le code DSN 5.1.2 qui est envoyé aux expéditeurs internes en anglais.

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

Cet exemple montre comment créer un message DSN personnalisé en texte brut correspondant au code DSN 5.1.2 qui est envoyé aux expéditeurs externes en anglais.

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

Cet exemple montre comment créer un message DSN personnalisé au format HTML pour le code DSN 5.1.2 qui est envoyé aux expéditeurs internes en anglais.

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé un message DSN personnalisé, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  Vérifiez que les valeurs affichées sont celles que vous avez configurées.

3.  Envoyez un message de test qui va générer le DSN personnalisé que vous avez configuré.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier le texte d'un message DSN personnalisé

Pour modifier le texte d'un message DSN personnalisé, utilisez la commande suivante :

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

Cet exemple montre comment modifier le texte affecté au message DSN personnalisé correspondant au code DSN 5.1.2 qui est envoyé aux expéditeurs internes en anglais.

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez modifié le texte d'un message DSN personnalisé, procédez comme suit :

1.  Exécutez la commande suivante : `Get-SystemMessage`.
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour supprimer un message DSN personnalisé

Exécutez la commande suivante :

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

Cet exemple montre comment supprimer le message DSN personnalisé correspondant au code DSN 5.1.2 qui est envoyé aux expéditeurs internes en anglais.

    Remove-SystemMessage En\Internal\5.1.2

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez supprimé un message DSN personnalisé, procédez comme suit :

1.  Exécutez la commande suivante : `Get-SystemMessage`.

2.  Vérifiez qu'il n'existe aucun message de notification d'état de remise pour les paramètres régionaux, les destinataires internes ou externes et le code DSN que vous avez supprimés.

## Transmettre des copies des messages DSN à la boîte aux lettres du destinataire Exchange

Vous pouvez spécifier une liste de codes DSN que vous souhaitez contrôler en copiant les messages DSN dans la boîte aux lettres du destinataire Exchange. Toutefois, par défaut, aucune boîte aux lettres n'est attribuée au destinataire Exchange. Ainsi, les messages envoyés au destinataire Exchange sont supprimés. Pour envoyer des copies de messages DSN à la boîte aux lettres du destinataire Exchange, vous devez attribuer une boîte aux lettres au destinataire Exchange, puis spécifier les codes DSN à surveiller. Par défaut, les codes DSN suivants sont surveillés : `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0` et `5.1.4`.

## Étape 1 : utiliser l'environnement de ligne de commande Exchange Management Shell pour attribuer une boîte aux lettres au destinataire Exchange

Pour attribuer une boîte aux lettres au destinataire Exchange, procédez comme suit :

1.  Vu les volumes probablement élevés de courriers électroniques, envisagez la création d'une boîte aux lettres dédiée et d'un compte d'utilisateur Active Directory pour le destinataire Exchange. Pour plus d'informations, consultez la rubrique [Création de boîtes aux lettres utilisateur](create-user-mailboxes-exchange-2013-help.md). Sinon, identifiez la boîte aux lettres existante que vous souhaitez associer au destinataire Exchange.

2.  Exécutez la commande suivante :
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    Par exemple, pour attribuer la boîte aux lettres existante nommée « Boîte aux lettres système de Contoso » au destinataire Exchange, exécutez la commande suivante :
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## Étape 2 : spécifier les codes DSN à surveiller

## Utiliser le Centre d'administration Exchange (CAE) pour spécifier les codes DSN

1.  Dans le CAE, accédez à **Flux de messagerie** \> **Connecteurs de réception** \> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Paramètres de transport de l'organisation** \> **Remise**.

2.  Dans la section **Codes DSN**, indiquez les codes à surveiller à l'aide du format *\<x.y.z\>*, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Sélectionnez une entrée existante, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour la modifier, ou sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression") pour la supprimer. Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour spécifier les codes DSN

Pour remplacer les valeurs existantes, exécutez la commande suivante :

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

Cet exemple montre comment configurer l'organisation Exchange de sorte que tous les messages DSN associés aux codes DSN 5.7.1, 5.7.2 et 5.7.3 sont transférés au destinataire Exchange.

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

Pour ajouter ou supprimer des entrées sans modifier une valeur existante, exécutez la commande suivante :

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

Cet exemple montre comment ajouter le code DSN 5.7.5 et supprime le code DSN 5.7.1 de la liste existante des messages DSN transmis au destinataire Exchange.

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## Comment savoir si cela a fonctionné ?

Pour vous assurer que vous avez bien configuré des copies de messages DSN à envoyer à la boîte aux lettres du destinataire Exchange, surveillez la boîte aux lettres associée au destinataire Exchange, puis vérifiez que les messages DSN contiennent bien les codes DSN spécifiés.

