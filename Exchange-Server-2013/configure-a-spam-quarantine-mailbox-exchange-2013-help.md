---
title: 'Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable: Exchange 2013 Help'
TOCTitle: Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50478686
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2013-02-19_

Les messages identifiés comme courrier indésirable par l'agent de filtrage du contenu peuvent être dirigés vers une boîte aux lettres de mise en quarantaine du courrier indésirable. Si le seuil de quarantaine du seuil de probabilité de courrier indésirable (SCL) est activé, tous les messages mis en quarantaine sont inclus dans des rapports de non-remise (NDR) et envoyés à l'adresse SMTP que vous avez indiquée comme boîte aux lettres de mise en quarantaine de courrier indésirable. Vous pouvez examiner les messages mis en quarantaine et les libérer à l'aide de la fonction Envoyer à nouveau de Microsoft Outlook.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 45 minutes.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Le responsable de la boîte aux lettres de mise en quarantaine du courrier indésirable peut afficher des messages potentiellement privés et sensibles et envoyer des messages pour le compte de toute personne au sein de l'organisation Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Vérifier que le filtrage de contenu est activé

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Fonctionnalités de blocage du courrier indésirable » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

1.  Exécutez la commande suivante pour vérifier que l'agent de contenu est installé et activé sur le serveur Exchange :
    
        Get-TransportAgent "Content Filter Agent"

2.  Exécutez la commande suivante pour vérifier que le filtrage de contenu est activé :
    
        Get-ContentFilterConfig | Format-List Enabled

Pour plus d'informations, consultez la rubrique [Gérer le filtrage du contenu](manage-content-filtering-exchange-2013-help.md).

## Étape 2 : Créer une boîte aux lettres de mise en quarantaine du courrier indésirable

Pour créer une boîte aux lettres dédiée à la mise en quarantaine du courrier indésirable, procédez comme suit :

  - **Créer une base de données Exchange dédiée**   nous vous recommandons de créer une base de données dédiée pour la boîte aux lettres de mise en quarantaine du courrier indésirable. La boîte aux lettres de mise en quarantaine du courrier indésirable doit disposer d'une base de données importante car si la limite du quota de stockage est atteinte, des messages seront perdus. Pour plus d'informations, consultez la rubrique [Gestion des bases de données de boîtes aux lettres dans Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

  - **Créer une boîte aux lettres et un compte d'utilisateur dédiés**   Nous vous recommandons de créer une boîte aux lettres et un compte d'utilisateur Active Directory dédiés pour la boîte aux lettres de mise en quarantaine du courrier indésirable. Pour plus d'informations, consultez la rubrique [Création de boîtes aux lettres utilisateur](create-user-mailboxes-exchange-2013-help.md).
    
    Vous pouvez appliquer des stratégies de destinataire, comme la gestion des enregistrements de messagerie, des quotas de boîte aux lettres et des droits de délégation, en fonction des stratégies de conformité et des besoins de votre organisation. Pour plus d'informations, consultez la rubrique [Gestion des enregistrements de messagerie](messaging-records-management-exchange-2013-help.md).
    
    > [!NOTE]
    > Si un message mis en quarantaine est rejeté à cause d'un quota de stockage, ce message est perdu. Exchange ne génère pas de notifications d'échec de remise pour les messages mis en quarantaine, car ceux-ci sont inclus dans des rapports d'échec de remise.


  - **Configurer Outlook**   Vous devez configurer les droits d'accès de délégué d'Outlook en fonction des besoins de votre organisation. En outre, nous vous recommandons de configurer le profil d'Outlook pour afficher les champs `Sender[#0x0069001E]`, `Recipient[#0x0E04001E]` et `Bcc[#0x0E02001E]` d'origine dans la vue **Message**. Pour plus d'informations, consultez la rubrique [Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

## Étape 3 : Spécifier la boîte aux lettres de mise en quarantaine du courrier indésirable

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

Exécutez la commande suivante :

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

Cet exemple envoie tous les messages qui dépassent le seuil de mise en quarantaine du courrier indésirable à spamQ@contoso.com.

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement spécifié la boîte aux lettres de mise en quarantaine du courrier indésirable, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Étape 4 : Définir le seuil de mise en quarantaine SCL

Le seuil de mise en quarantaine SCL est la valeur à laquelle un message particulier identifié comme courrier indésirable potentiel est déposé dans la boîte aux lettres de mise en quarantaine du courrier indésirable. Vous pouvez définir le seuil SCL de mise en quarantaine sur une valeur comprise entre 0 et 9, avec 0 pour les messages les moins susceptibles d'être du courrier indésirable et 9 pour les messages les plus susceptibles d'être du courrier indésirable.

Pour plus d'informations sur la manière d'ajuster des seuils SCL en fonction des besoins de votre organisation et la manière d'ajuster les seuils SCL pour chaque destinataire, consultez la rubrique [Gérer le filtrage du contenu](manage-content-filtering-exchange-2013-help.md).

## Étape 5 : Gérer la boîte aux lettres de mise en quarantaine du courrier indésirable

Lorsque vous gérez votre boîte aux lettres de mise en quarantaine du courrier indésirable, procédez comme suit :

  - Libérez les éléments qui ont été envoyés à la boîte aux lettres de mise en quarantaine du courrier indésirable à l'aide de la fonction Envoyer à nouveau d'Outlook pour renvoyer le message d'origine.
    
    Pour plus d'informations, consultez la rubrique [Récupération des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

  - Surveillez la boîte aux lettres de mise en quarantaine du courrier indésirable de façon à ce que sa taille demeure dans une plage acceptable. Le volume des messages électroniques peut varier en raison d'un ensemble plus large de destinataires, de la tendance naturelle des messages plus volumineux ou du seuil de l'action de mise en quarantaine SCL.

  - Surveillez la boîte aux lettres de mise en quarantaine des messages indésirables afin de détecter les faux positifs. Si votre boîte aux lettres de mise en quarantaine du courrier indésirable contient de nombreux faux positifs, ajustez votre seuil de mise en quarantaine SCL. Pour plus d'informations sur la manière de déterminer pourquoi les faux positifs sont délivrés à la boîte aux lettres de mise en quarantaine du courrier indésirable, consultez la rubrique [Marquages de courrier indésirable](anti-spam-stamps-exchange-2013-help.md).

  - Utilisez le même profil Outlook pour la récupération des messages mis en quarantaine à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable. L'application d'autorisations à un profil Outlook différent pour la récupération des messages n'est pas prise en charge. Vous ne pouvez pas utiliser un profil Outlook différent pour la récupération ou la diffusion des messages à partir de la boîte aux lettres de mise en quarantaine du courrier indésirable.

> [!NOTE]
> Les NDR qui sont identifiés comme courrier indésirable sont supprimés, même si leur valeur SCL indique qu'ils devraient être mis en quarantaine. Les notifications d'échec de remise ne sont pas remises à la boîte aux lettres de mise en quarantaine du courrier indésirable. Pour détecter de tels messages, utilisez l'enregistrement de l'agent ou le journal de suivi des messages. Pour plus d'informations, consultez la rubrique <a href="anti-spam-agent-logging-exchange-2013-help.md">Journalisation de l’agent anti-courrier indésirable</a>.


## Étape 6 : Configurer le seuil de mise en quarantaine SCL

Après avoir configuré le seuil de mise en quarantaine SCL, vous devez surveiller périodiquement ces paramètres et les ajuster sur la base des besoins de votre organisation. Par exemple, si un trop grand nombre de faux positifs sont filtrés dans la boîte aux lettres de mise en quarantaine du courrier indésirable, augmentez la valeur du seuil de mise en quarantaine SCL. Pour plus d'informations sur l'ajustement du seuil de mise en quarantaine SCL, consultez la rubrique [Niveau de confiance du courrier indésirable](spam-confidence-level-threshold-exchange-2013-help.md).

