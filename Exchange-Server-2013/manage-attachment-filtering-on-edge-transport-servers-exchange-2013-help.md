---
title: 'Gestion du filtrage des pièces jointes sur les serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Gestion du filtrage des pièces jointes sur les serveurs de transport Edge
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60828958
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion du filtrage des pièces jointes sur les serveurs de transport Edge

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Le filtrage des pièces jointes est effectué par l’agent de filtrage des pièces jointes, uniquement disponible sur les serveurs de transport Edge. Le filtrage des pièces jointes peut permettre d’empêcher les fichiers joints aux messages électroniques d’entrer dans votre organisation. Vous pouvez configurer une ou plusieurs entrées de filtre de pièce jointe pour filtrer les pièces jointes soit par type de contenu, soit par nom de fichier.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 10 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) et l’entrée « Agents de transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Les modifications de configuration que vous apportez au filtrage des pièces jointes sur un serveur de transport Edge sont appliquées uniquement à l’ordinateur local. Si vous disposez de plusieurs serveurs de transport Edge dans votre réseau de périmètre, vous devez configurer le filtrage des pièces jointes sur chaque serveur de transport Edge séparément.

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Lorsque vous désactivez le filtrage des pièces jointes et redémarrez le service de transport Microsoft Exchange, toutes les fonctionnalités de filtrage des pièces jointes cessent de fonctionner.

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

## Utiliser l’environnement Exchange Management Shell pour activer ou désactiver le filtrage des pièces jointes

Lorsque vous activez ou désactivez l’agent de filtrage des pièces jointes, la modification prend effet après le redémarrage du service de transport Microsoft Exchange. Lorsque vous redémarrez le service de transport Microsoft Exchange sur un serveur de transport Edge, le flux de messagerie sur le serveur est temporairement interrompu.

Pour désactiver le filtrage des pièces jointes, exécutez la commande suivante :

    Disable-TransportAgent "Attachment Filtering Agent"

Pour activer le filtrage des pièces jointes, exécutez la commande suivante :

    Enable-TransportAgent "Attachment Filtering Agent"

Après avoir activé ou désactivé le filtrage des pièces jointes, redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :

    Restart-Service MSExchangeTransport

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé le filtrage des pièces jointes, procédez comme suit :

1.  Exécutez la commande suivante :
    
        Get-TransportAgent "Attachment Filtering Agent"

2.  Si la valeur de **Enabled** est `True`, le filtrage des pièces jointes est activé. Si la valeur est `False`, le filtrage des pièces jointes est désactivé.

## Utiliser l’environnement Exchange Management Shell pour afficher les entrées de filtrage des pièces jointes

Les entrées de filtrage des pièces jointes définissent les pièces jointes de messages que vous voulez empêcher d’entrer dans votre organisation. Pour afficher les entrées de filtrage des pièces jointes utilisées par l’agent de filtrage des pièces jointes, exécutez la commande suivante :

    Get-AttachmentFilterEntry | Format-Table

Pour afficher une entrée de type de contenu MIME spécifique, utilisez la syntaxe suivante :

    Get-AttachmentFilteringEntry ContentType:<MIMEContentType>

Par exemple, pour afficher l’entrée de type de contenu pour les images JPEG, exécutez la commande suivante :

    Get-AttachmentFilteringEntry ContentType:image/jpeg

Pour afficher une entrée de nom de fichier ou d’extension de nom de fichier spécifique, utilisez la syntaxe suivante :

    Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>

Par exemple, pour afficher l’entrée d’extension de nom de fichier pour les pièces jointes au format JPEG, exécutez la commande suivante :

    Get-AttachmentFilteringEntry FileName:*.jpg

## Utiliser l’environnement Exchange Management Shell pour ajouter des entrées de filtrage des pièces jointes

Pour ajouter une entrée de filtrage des pièces jointes qui filtre les pièces jointes par type de contenu MIME, utilisez la syntaxe suivante :

    Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType

L’exemple suivant ajoute une entrée de type de contenu MIME qui permet de filtrer les images JPEG.

    Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType

Pour ajouter une entrée de filtrage des pièces jointes qui filtre les pièces jointes par nom de fichier ou extension de nom de fichier, utilisez la syntaxe suivante :

    Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName

L’exemple suivant filtre les pièces jointes portant l’extension de nom de fichier .jpg.

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté une entrée de filtrage des pièces jointes, procédez comme suit :

1.  Exécutez la commande suivante pour vérifier que l’entrée de filtrage existe.
    
        Get-AttachmentFilterEntry | Format-Table

2.  Envoyez un message de test contenant une pièce jointe interdite à un destinataire interne à partir d’une boîte aux lettres externe et vérifiez que le message a bien été rejeté ou supprimé.

## Utiliser l’environnement Exchange Management Shell pour supprimer des entrées de filtrage des pièces jointes

Pour supprimer une entrée de filtrage des pièces jointes qui filtre les pièces jointes par type de contenu MIME, utilisez la syntaxe suivante :

    Remove-AttachmentFilterEntry ContentType:<ContentType>

L’exemple suivant supprime l’entrée de type de contenu MIME pour les images JPEG.

    Remove-AttachmentFilterEntry ContentType:image/jpeg

Pour supprimer une entrée de filtrage des pièces jointes qui filtre les pièces jointes par nom de fichier ou extension de nom de fichier, utilisez la syntaxe suivante :

    Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>

L’exemple suivant supprime l’entrée de nom de fichier pour l’extension de nom de fichier .jpg.

    Remove-AttachmentFilterEntry FileName:*.jpg

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé une entrée de filtrage des pièces jointes, procédez comme suit :

1.  Exécutez la commande suivante pour vérifier que l’entrée de filtrage a bien été supprimée.
    
        Get-AttachmentFilterEntry | Format-Table

2.  Envoyez un message de test contenant une pièce jointe autorisée à un destinataire interne à partir d’une boîte aux lettres externe et vérifiez que le message a bien été reçu avec la pièce jointe.

## Utiliser l’environnement Exchange Management Shell pour afficher l’action de filtrage des pièces jointes

Pour afficher l’action de filtrage des pièces jointes utilisée lors de la détection d’une pièce jointe interdite dans un message, exécutez la commande suivante :

    Get-AttachmentFilterListConfig

## Utiliser l’environnement Exchange Management Shell pour configurer l’action de filtrage des pièces jointes

Pour configurer l’action de filtrage des pièces jointes à appliquer lors de la détection d’une pièce jointe interdite dans un message, utilisez la syntaxe suivante :

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

Cet exemple apporte les modifications suivantes à la configuration du filtrage des pièces jointes :

  - Le rejet (blocage) des messages qui contiennent des pièces jointes interdites.

  - L’utilisation d’une réponse personnalisée pour les messages rejetés.

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

Pour plus d’informations, consultez la rubrique [Set-AttachmentFilterListConfig](https://technet.microsoft.com/fr-fr/library/bb123483\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré l’action de filtrage des pièces jointes, envoyez un message de test contenant une pièce jointe interdite à un destinataire interne à partir d’une boîte aux lettres externe et vérifiez que le message et la pièce jointe sont traités comme prévu.

