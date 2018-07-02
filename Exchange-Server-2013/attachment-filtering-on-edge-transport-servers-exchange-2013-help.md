---
title: 'Filtrage des pièces jointes sur les serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Filtrage des pièces jointes sur les serveurs de transport Edge
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60829198
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Filtrage des pièces jointes sur les serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-02-10_

Dans Microsoft Exchange Server 2013, vous pouvez utiliser le filtrage des pièces jointes sur les serveurs de transport Edge pour contrôler les pièces jointes que les utilisateurs reçoivent dans des messages électroniques. Le filtrage des pièces jointes est effectué par l’Agent de filtrage des pièces jointes, qui n’est disponible que sur les serveurs de transport Edge.

## Types de filtrage des pièces jointes

Vous pouvez utiliser les types de filtrage des pièces jointes suivants pour contrôler les pièces jointes entrant ou sortant de votre organisation via un serveur de transport Edge :

  - **Filtrage sur le nom de fichier ou l’extension de nom de fichier**   Vous indiquez le nom de fichier ou l’extension de nom de fichier exact à filtrer. `BadFileName.exe` est un exemple de filtre de nom de fichier. `*.exe` est un exemple de filtre d’extension de nom de fichier.

  - **Filtrage sur le type de contenu MIME de fichier**   Vous spécifiez la valeur du type de contenu MIME à filtrer. La valeur du type de contenu MIME indique la nature de la pièce jointe (par exemple, une image JPEG, un fichier exécutable ou un fichier Microsoft Excel). Les types de contenu sont exprimés comme `type/subtype`. Par exemple, un fichier image JPEG est exprimé comme `image/jpeg`.
    
    Pour afficher la liste complète des extensions de nom de fichier et des types de contenu que le filtrage des pièces jointes peut détecter, exécutez la commande suivante sur le serveur de transport Edge :
    
        Get-AttachmentFilterEntry | Format-List

Après avoir défini les fichiers à rechercher, vous pouvez configurer l’action à effectuer sur les messages qui contiennent ces pièces jointes. Vous ne pouvez pas spécifier différentes actions pour différents types de pièces jointes. Vous configurez l’une des actions suivantes pour tous les messages qui correspondent à l’un des filtres de pièces jointes :

  - **Rejeter (bloquer) le message**   Le message est bloqué. L’expéditeur reçoit une notification d’échec de remise qui explique que le message n’a pas été remis car il contenait une pièce jointe inacceptable. Vous pouvez personnaliser le texte de la notification d’échec de remise. Le texte par défaut est le suivant : `Message rejected due to unacceptable attachments`.

  - **Supprimer les pièces jointes, mais autoriser le message**   La pièce jointe est supprimée du message. Cependant, le message lui-même et les éventuelles pièces jointes qui ne correspondent pas au filtre sont autorisés. Si une pièce jointe est supprimée, elle est remplacée par un fichier texte expliquant le motif de sa suppression. Il s’agit de l’action par défaut.

  - **Supprimer silencieusement le message**   Le message est supprimé. Ni l’expéditeur ni le destinataire ne reçoit de notification.

Pour plus d'informations, consultez la rubrique [Gestion du filtrage des pièces jointes sur les serveurs de transport Edge](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous ne pouvez pas récupérer les messages qui ont été bloqués, ni les pièces jointes qui ont été supprimées. Lorsque vous configurez des filtres de pièces jointes, examinez attentivement toutes les correspondances de noms de fichier possibles et vérifiez que les pièces jointes légitimes ne seront pas affectées par le filtre.<br />
De plus, ne supprimez pas les pièces jointes des messages électroniques signés numériquement, chiffrés ou protégés par des droits. Si vous supprimez les pièces jointes de ces messages, vous invalidez les messages signés numériquement et vous rendez les messages chiffrés et protégés illisibles.</td>
</tr>
</tbody>
</table>

