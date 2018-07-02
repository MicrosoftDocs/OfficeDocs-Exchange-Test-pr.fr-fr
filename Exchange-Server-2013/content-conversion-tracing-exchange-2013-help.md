---
title: 'Suivi de la conversion de contenu: Exchange 2013 Help'
TOCTitle: Suivi de la conversion de contenu
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 50479467
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suivi de la conversion de contenu

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-09-25_

Le suivi de la conversion de contenu capture les erreurs dans la conversion de contenu MAPI réalisées par le service de transport de boîtes aux lettres sur les messages entrants et sortants dans un serveur de boîtes aux lettres Microsoft Exchange Server 2013.

Le service de transport de boîtes aux lettres sur un serveur de boîte aux lettres est responsable de la conversion du contenu des messages en provenance et à destination des destinataires de boîtes aux lettres. Plus particulièrement, le service Dépôt de transport de boîtes aux lettres convertit les messages sortants en provenance d'utilisateurs de boîtes aux lettres, de MAPI en MIME. Le service Remise de transport de boîtes aux lettres convertit les messages entrants pour des utilisateurs de boîtes aux lettres, de MAPI en MIME. Le suivi de la conversion de contenu est chargé de la capture de ces échecs de conversion MAPI.

Le catégoriseur du service de transport sur un serveur de boîtes aux lettres est responsable de la conversion du contenu de tous les messages envoyés à des destinataires externes. Le suivi de conversion de contenu ne capture aucune erreur de conversion de contenu que le catégoriseur du service de transport rencontre lors de la conversion des messages envoyés à des destinataires externes.

**Contenu de cette rubrique**

Configurer le suivi de conversion de contenu

Fonctionnement du suivi de conversion de contenu

Considérations sur le suivi de conversion de contenu

## Configurer le suivi de conversion de contenu

Le suivi de conversion de contenu est contrôlé par les paramètres suivants des cmdlets **Set-TransportService** et **Set-MailboxTransportService** dans l'environnement de ligne de commande Exchange Management Shell:

  - *ContentConversionTracingEnabled*   Ce paramètre active ou désactive le suivi de la conversion de contenu dans le service de transport sur le serveur de boîtes aux lettres ou dans le service de transport de boîtes aux lettres sur le serveur de boîtes aux lettres. Les valeurs valides pour ce paramètre sont `$true` et `$false`. La valeur par défaut est `$false`. Si votre organisation Exchange contient plusieurs serveurs de boîtes aux lettres, vous devez activer le suivi de la conversion de contenu sur chacun d'eux.

  - *PipelineTracingPath*   Bien que ce paramètre soit associé au suivi de pipeline, il spécifie également l'emplacement racine des fichiers de suivi de conversion de contenu. L'emplacement par défaut dans le service de transport est `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. L'emplacement par défaut dans le service de transport de boîtes aux lettres est `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`.Le chemin d'accès vers l'ordinateur Exchange doit être local.

La conversion de contenu crée un dossier appelé `ContentConversionTracing` dans le chemin d'accès spécifié par le paramètre *PipelineTracingPath*. Dans le dossier `ContentConversionTracing`, la conversion de contenu crée deux sous-dossiers : `InboundFailures` et `OutboundFailures`. Le dossier `InboundFailures` contient les informations des échecs de conversion du contenu des messages entrants. Le dossier `OutboundFailures` contient les informations des échecs de conversion du contenu des messages sortants.

La taille maximale pour tous les fichiers du dossier `InboundFailures` ou du dossier `OutboundFailures` est fixée à 128 mégaoctets (Mo). Le suivi de conversion de contenu n'utilise pas d'enregistrement circulaire pour supprimer les anciens fichiers en fonction de l'âge ou de la taille des fichiers. Dès que la taille maximale d'un dossier est atteinte, le suivi de la conversion de contenu arrête d'écrire des données dans le dossier. Si vous souhaitez vérifier si la limite de taille maximale des dossiers n'est pas dépassée, vous pouvez créer une tâche planifiée qui déplace périodiquement les fichiers de suivi de la conversion de contenu vers un emplacement différent.

Les autorisations requises sur les dossiers et sous-dossiers utilisés dans le suivi de la conversion de contenu sont les suivantes :

  - Administrateurs : Contrôle total

  - Service réseau : Contrôle total

  - Système : Contrôle total

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le suivi de conversion de contenu copie le contenu complet des messages électroniques. Pour éviter une diffusion indésirable des données confidentielles, vous devez définir des autorisations de sécurité appropriées pour l'emplacement des fichiers de suivi de conversion de contenu.</td>
</tr>
</tbody>
</table>


Retour au début

## Fonctionnement du suivi de conversion de contenu

Lorsque la conversion de contenu d'un message entrant échoue, une notification d'état de remise affichant le code d'état 5.6.0 est envoyée à l'expéditeur du message. Si le suivi de la conversion de contenu est activé, les informations relatives à l'échec sont enregistrées au moment où le message DSN 5.6.0 est généré. Chaque erreur de la conversion de contenu génère deux fichiers distincts.

Une erreur de la conversion de contenu qui a lieu lors de la conversion d''un message entrant de MIME en MAPI génère les deux fichiers suivants dans le dossier InboundFailures :

  - **\<GUID\>.eml**   Ce fichier contient le message qui a échoué au format texte.

  - **\<GUID\>.txt**   Ce fichier contient la description de l'exception, les résultats de la conversion, les options de conversion et la taille limite imposée à tous les messages par le service de transport de boîtes aux lettres.

Une erreur de la conversion de contenu qui a lieu lors de la conversion d'un message sortant de MAPI en MIME génère les deux fichiers suivants dans le dossier OutboundFailures :

  - **\<GUID\>.msg**   Ce fichier contient le message qui a échoué au format Microsoft Outlook.

  - **\<GUID\>.txt**   Ce fichier contient la description de l'exception, les résultats de la conversion, les options de conversion et la taille limite des messages imposée pour tous les messages par le pilote de banque d'informations.

L'espace réservé \<*GUID*\> est identique dans les deux noms de fichier. Chaque erreur de conversion de contenu génère un GUID différent utilisé dans les noms de fichier des messages et des fichiers texte correspondants. Un exemple de GUID utilisé dans les noms de fichier est `038b930e-61fd-4bfd-b9b4-0374c18b73f7`.

Retour au début

## Considérations sur le suivi de conversion de contenu

Vous pouvez laisser le suivi de la conversion de contenu activé pour une surveillance proactive. Vous pouvez également activer le suivi de la conversion de contenu pour dépanner un événement d'échec particulier. Vous pouvez généralement reproduire des échecs de conversion de contenu entrant en demandant au destinataire du message DSN 5.6.0 de renvoyer le message d'origine.

Les échecs de conversion entrant sont les plus courants. Parmi les raisons entraînant des erreurs de conversion de contenu figurent les suivantes :

  - **Violations des tailles limites des messages**   Ces tailles limites des messages sont imposées par le service de transport de boîtes aux lettres pour prévenir des attaques par déni de service (DoS). Ces tailles limites des messages figurent dans le fichier \<*GUID*\>.txt. Ces tailles limites des messages sont les suivantes :
    
      - **MaxMimeTextHeaderLength**   Cette limite spécifie le nombre maximal de caractères de texte que peut contenir un en-tête MIME. La valeur est 2000.
    
      - **MaxMimeSubjectLength**   Cette limite spécifie le nombre maximal de caractères de texte que peut contenir la ligne d'objet. La valeur est 255.
    
      - **MSize**   Cette limite spécifie la taille maximale d'un message. La valeur est  2 147 483 647 octets.
    
      - **MaxMimeRecipients**   Cette limite spécifie le nombre total de destinataires autorisés dans les champs À :, Cc :, et Cci :. La valeur est 12 288.
    
      - **MaxRecipientPropertyLength**   Cette limite spécifie le nombre maximal de caractères de texte que peut contenir une description de destinataire. La valeur est 1000.
    
      - **MaxBodyPartsTotal**   Cette limite spécifie le nombre maximal de parties de messages pouvant figurer dans un message MIME multipart. La valeur est 250.
    
      - **MaxEmbeddedMessageDepth**   Cette limite spécifie le nombre maximal de messages transférés qui peuvent figurer dans un message. La valeur est 30.
    
    Pour plus d'informations sur les tailles limites configurables des messages utilisées dans le service de transport sur les serveurs de boîtes aux lettres ou sur les serveurs de transport Edge, voir [Tailles limites des messages](message-size-limits-exchange-2013-help.md).

  - **Échec de conversion dans un message iCalendar entrant pour une demande de réunion**   RFC 2445 définit iCalendar comme standard pour l'échange de données de calendrier. Les causes spécifiques de l'échec de conversion sont les suivantes :
    
      - Usage incorrect d'iCalendar par l'agent d'envoi.
    
      - Constructions d'iCalendar qui ne peuvent pas être prises en charge par le schéma de calendrier Exchange ou Outlook.
    
    Les échecs de conversion d'iCalendar n'ont pas pour effet d'envoyer un message DSN 5.6.0 à l'expéditeur. Au lieu de cela, le message est remis avec un fichier .ics en pièce jointe, contenant le corps du message iCalendar.

  - **Échecs provoqués par une mauvaise mise en forme des messages MIME**   Les messages électroniques commerciaux non sollicités ou les messages de courrier indésirable peuvent contenir des erreurs de mise en forme dans l'en-tête, telles qu'un guillemet manquant dans les descriptions de destinataire. Un nombre sensiblement inférieur d'échecs provoqués par une mauvaise mise en forme des messages MIME sont considérés comme des bogues.

Les échecs de conversion de contenu sortant sont beaucoup moins fréquents que les échecs de conversion de contenu entrant. Lorsque des échecs sortants se produisent, ils sont généralement provoqués par des bogues de code Exchange ou un contenu de message endommagé.

Retour au début

