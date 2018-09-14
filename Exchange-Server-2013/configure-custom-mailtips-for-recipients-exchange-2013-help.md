---
title: 'Configuration des infos-courriers personnalisées: Exchange 2013 Help'
TOCTitle: Configurer les infos-courrier personnalisées pour les destinataires
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52057165
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer les infos-courrier personnalisées pour les destinataires

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-06-01_

Les *Infos-courrier* sont des messages informatifs à l'intention des utilisateurs, qui s'affichent dans la barre d'informations dans Outlook Web App et Microsoft Outlook 2010 ou version ultérieure quand un utilisateur effectue l'une des opérations suivantes en composant un message électronique :

  - Ajouter un destinataire

  - Ajouter une pièce jointe

  - Répondre ou Répondre à tous

  - Ouvrir un message présent dans le dossier Brouillons, déjà adressé à des destinataires

Outre les Infos-courrier intégrées disponibles, vous pouvez en créer des personnalisées pour tous types de destinataires. Pour plus d'informations sur les Infos-courrier intégrés, consultez la rubrique [MailTips](https://docs.microsoft.com/fr-fr/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 10 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Infos-courrier » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez configurer l'Info-courrier principale dans le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell. Cependant, vous ne pouvez configurer que des traductions d'Infos-courrier supplémentaires dans l'environnement de ligne de commande Exchange Management Shell.

  - L'ajout d'une Info-courrier à un destinataire a deux effets :
    
      - Des balises HTML sont automatiquement ajoutées au texte. Par exemple, si vous entrez le texte suivant : `This mailbox is not monitored`, l'Info-courrier devient automatiquement : `<html><body>This mailbox is not monitored</body></html>`. Les autres balises HTML dans les infos-courrier ne sont pas prises en charge.
    
      - Le texte est automatiquement ajouté à la propriété *MailTipTranslations* du destinataire comme valeur par défaut. Si vous modifiez le texte de l'Info-courrier, la valeur par défaut est automatiquement mise à jour dans la propriété *MailTipTranslations*.

  - Une Info-courrier ne doit pas comporter plus de 175 caractères affichés.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Configurer des Infos-courrier pour des destinataires

## Utiliser le CAE pour configurer des Infos-courrier pour des destinataires

1.  Dans le CAE, accédez à **Destinataires**.

2.  Sélectionnez l'un des onglets de destinataires suivants en fonction du type de destinataire :
    
      - **Boîtes aux lettres**
    
      - **Groupes**
    
      - **Ressources**
    
      - **Contacts**
    
      - **Partagés**

3.  Sous l'onglet Destinataire, sélectionnez le destinataire à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans la page des propriétés des destinataires qui s'ouvre, cliquez sur **Infos-courrier**.

5.  Entrez le texte de l'Info-courrier. Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des Infos-courrier pour des destinataires

Pour configurer une Info-courrier pour un destinataire, utilisez la syntaxe suivante.

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* peut être tout type de destinataire. Par exemple, `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup` ou `DynamicDistributionGroup`.

Supposons, par exemple, que vous disposiez d'une boîte aux lettres nommée « Help Desk », servant aux utilisateurs pour envoyer leurs demandes de support, et que le temps de réponse promis soit de deux heures. Pour configurer une Info-courrier personnalisée qui l'explique, exécutez la commande suivante :

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer des Infos-courrier supplémentaires dans différentes langues

Pour configurer des traductions d'Infos-courrier supplémentaires sans affecter le texte ou les traductions d'Infos-courrier existants, utilisez la syntaxe suivante :

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* est un code de culture ISO 639 à deux lettres valide associé à la langue.

Par exemple, imaginez que la boîte aux lettres Notifications possède actuellement l'Info-courrier : « Cette boîte aux lettres n'est pas surveillée. » Pour ajouter la traduction espagnole, exécutez les commandes suivantes :

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré un info-courrier pour un destinataire, procédez comme suit :

1.  Dans Outlook Web App ou Outlook 2010 ou version ultérieure, rédigez un message électronique adressé à un destinataire, mais sans l'envoyer.

2.  Vérifiez que l'Info-courrier apparaît dans la barre d'informations.

3.  Si vous configurez des traductions d’Info-courrier supplémentaires, rédigez le message dans Outlook Web App en vous assurant que le paramètre de langue correspond à la langue de la traduction de l’Info-courrier pour vérifier les résultats.

