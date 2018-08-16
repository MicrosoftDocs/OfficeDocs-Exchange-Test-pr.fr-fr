---
title: "ID de l'expéditeur: Exchange 2013 Help"
TOCTitle: ID de l'expéditeur
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50477564
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ID de l'expéditeur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L’agent ID de l’expéditeur est un agent anti-spam disponible dans Microsoft Exchange Server 2013. Cet agent ID de l’expéditeur se base sur l’en-tête SMTP RECEIVED et une requête au service DNS du système d’envoi pour déterminer l’action éventuelle à appliquer à un message entrant.

L’ID de l’expéditeur est destiné à lutter contre l’usurpation d’identité d’un expéditeur et d’un domaine, pratique fréquemment appelée *falsification*. Un *message électronique falsifié* est un message électronique dont l’adresse de l’expéditeur a été modifiée pour qu’il semble provenir d’un expéditeur autre que l’expéditeur réel du message.

Les messages falsifiés contiennent généralement une adresse De : qui prétend être celle d’une certaine organisation. Par le passé, il était relativement simple de falsifier l’adresse De : tant au niveau de la session SMTP, par exemple comme l’en-tête MAIL FROM : que dans les données du message RFC 2822, telles que De : "Masato Kawai" masato@contoso.com, parce que les en-têtes n’étaient pas validés.

**Contenu de cette rubrique**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## Utilisation de l’ID de l’expéditeur pour combattre les falsifications

L’ID de l’expéditeur complique la falsification. Si vous activez un ID de l’expéditeur, les métadonnées de chaque message contiennent un état de l’ID de l’expéditeur. Lors de la réception d’un message électronique, le serveur Exchange interroge le serveur DNS de l’expéditeur pour vérifier si l’adresse IP qui émet le message est autorisée à envoyer des messages pour le domaine spécifié dans les en-têtes de message. L’adresse IP du serveur d’envoi autorisé est indiquée comme adresse prétendue responsable (PRA).

Les administrateurs de domaine publient les enregistrements de framework (SPF) de stratégie de l’expéditeur sur leurs serveurs DNS. Enregistrements SPF identifient les serveurs de messages autorisés. Si un enregistrement SPF est configuré sur le serveur DNS de l’expéditeur, le serveur Exchange analyse l’enregistrement SPF et détermine si l’adresse IP à partir de laquelle le message a été reçu est autorisé à envoyer du courrier électronique pour le compte de domaine qui est spécifié dans le message. Pour plus d’informations sur la création d’un enregistrement SPF et de ce que contient un enregistrement SPF, consultez [ID de l’expéditeur](https://go.microsoft.com/fwlink/p/?linkid=50977).

Le serveur Exchange met à jour les métadonnées du message en indiquant l’état de l’ID de l’expéditeur en fonction de l’enregistrement SPF. Lorsque le serveur Exchange a mis à jour les métadonnées du message, le message est transmis comme il convient.

## Valeurs d’état d’ID de l’expéditeur

Le processus d’évaluation de l’ID de l’expéditeur génère un état d’ID de l’expéditeur pour le message. L’état de l’ID de l’expéditeur permet d’évaluer le contrôle d’accès SCL (Spam Confidence Level) du message. Cet état peut avoir l’une des valeurs suivantes :

  - **Pass** L’adresse IP et la PRA (Purported Responsible Address, adresse prétendue responsable) ont toutes les deux passé le contrôle de vérification de l’ID de l’expéditeur.

  - **Neutral** Les données de l’ID de l’expéditeur publiées sont peu concluantes.

  - **Soft fail**   L’adresse IP de la PRA figure peut-être parmi les adresses non autorisées.

  - **Fail** L’adresse IP n’est pas autorisée ; aucune PRA ne figure dans le courrier entrant ou le domaine d’envoi n’existe pas.

  - **None**   Il n’existe aucune donnée SPF publiée dans le DNS de l’expéditeur.

  - **TempError**   Une erreur DNS temporaire s’est produite. Un serveur DNS peut être indisponible, par exemple.

  - **PermError**   L’enregistrement DNS n’est pas valide. Il présente peut-être une erreur de format d’enregistrement.

L’état de l’ID de l’expéditeur est ajouté aux métadonnées du message, puis est converti en une propriété MAPI. Dans Microsoft Outlook, le filtre de courrier indésirable utilise la propriété MAPI pendant la génération de la valeur SCL.

Outlook n’affiche pas l’état de l’ID de l’expéditeur et ne marque pas nécessairement un message comme étant indésirable en présence de certaines valeurs d’ID de l’expéditeur. Outlook utilise la valeur de l’état de l’ID de l’expéditeur uniquement durant le calcul de la valeur SCL.

Outre les sept scénarios qui génèrent les états de l’ID de l’expéditeur, le processus d’évaluation de l’ID de l’expéditeur est parfois confronté à des cas où l’adresse IP De : est manquante. Si l’adresse IP De : est manquante, il n’est pas possible de définir l’état de l’ID de l’expéditeur. S’il n’est pas possible de définir l’état de l’ID de l’expéditeur, Exchange continue à traiter le message sans inclure d’état d’ID de l’expéditeur dans le message. Le message n’est pas écarté ni rejeté. Dans ce scénario, l’état de l’ID de l’expéditeur n’est pas défini et un événement Application est journalisé.

Pour plus d’informations sur la manière dont l’état de l’ID de l’expéditeur s’affiche dans les messages, consultez la rubrique [Marquages de courrier indésirable](anti-spam-stamps-exchange-2013-help.md).

## Options d’ID de l’expéditeur pour la gestion de messages électroniques falsifiés et de serveurs DNS inaccessibles

Vous pouvez également définir la manière dont le serveur Exchange gère les messages électroniques identifiés comme falsifiés et la manière dont il gère les messages si un serveur DNS est inaccessible. Les options relatives à la manière dont le serveur Exchange gère les messages électroniques falsifiés et les serveurs DNS inaccessibles incluent les actions suivantes :

  - **Stamp the status**   Cette option est l’action par défaut. Les métadonnées de tous les messages entrant dans votre organisation contiennent l’état d’ID de l’expéditeur.

  - **Reject**   Cette option rejette le message et envoie une réponse d’erreur SMTP au serveur d’envoi. La réponse d’erreur SMTP est une réponse de protocole de niveau 5*xx* contenant un texte correspondant à l’état d’ID de l’expéditeur.

  - **Delete**   Cette option supprime le message sans informer le système émetteur de la suppression. En fait, le serveur Exchange envoie une commande SMTP OK factice au serveur d’envoi, puis supprime le message. Comme le serveur d’envoi suppose que le message a été envoyé, il ne réessaie pas d’envoyer le message au cours de la même session.

Pour plus d’informations sur la configuration de l’agent d’ID de l’expéditeur, consultez la rubrique [Gérer les ID des expéditeurs](manage-sender-id-exchange-2013-help.md).

Retour au début

## Mise à jour du DNS connecté à Internet de votre organisation pour la prise en charge de l’ID de l’expéditeur

L’efficacité de l’ID de l’expéditeur varie en fonction de données DNS spécifiques. Plus les organisations mettent à jour leurs serveurs DNS connectés à Internet avec un enregistrement SPF, plus l’ID de l’expéditeur est efficace pour identifier les messages électroniques falsifiés.

Pour prendre en charge l’infrastructure de l’ID de l’expéditeur, vous devez mettre à jour vos données DNS connecté à Internet par la création d’un enregistrement SPF et hébergeant l’enregistrement SPF sur vos serveurs DNS publics. Pour plus d’informations sur la façon de créer et de déployer des enregistrements SPF, consultez [ID de l’expéditeur](https://go.microsoft.com/fwlink/p/?linkid=50977).

Retour au début

## Spécification des destinataires et des domaines d’expéditeurs à exclure du filtrage de l’ID de l’expéditeur

Parfois, il se peut que vous vouliez exclure des destinataires et des domaines d’expéditeurs spécifiques du filtrage des ID d’expéditeur. Pour ce faire, indiquez les destinataires et les domaines d’expéditeurs via la cmdlet **Set-SenderIdConfig** de l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations, consultez la rubrique [Set-SenderIdConfig](https://technet.microsoft.com/fr-fr/library/aa998859\(v=exchg.150\)).

Retour au début

