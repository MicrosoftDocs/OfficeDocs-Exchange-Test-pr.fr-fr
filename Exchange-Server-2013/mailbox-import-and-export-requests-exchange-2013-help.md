---
title: 'Demandes d’exportation et d’importation de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Demandes d’exportation et d’importation de boîtes aux lettres
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50477553
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Demandes d’exportation et d’importation de boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Grâce aux jeux de cmdlets **MailboxImportRequest** ou **MailboxExportRequest** de l’environnement de ligne de commande Exchange Management Shell, vous pouvez importer ou exporter des données en provenance et à destination de fichiers .pst. Après avoir lancé une demande d’importation ou d’exportation de boîte aux lettres, le service de réplication de boîtes aux lettres Microsoft Exchange va achever le traitement de manière asynchrone. Le service de réplication de boîtes aux lettres réside sur tous les serveurs d’accès au client Exchange 2010 et il permet de déplacer des boîtes aux lettres et d’importer, puis d’exporter des fichiers .pst.

**Contenu de cette rubrique**

Motifs pour importer ou exporter des données de boîtes aux lettres

Avantages associés à l’utilisation des demandes d’importation et d’exportation

Considérations

Importation de données de boîtes aux lettres

Exportation de données de boîtes aux lettres

## Motifs pour importer ou exporter des données de boîtes aux lettres

Vous pouvez importer et exporter les données d’une boîte aux lettres pour les motifs suivants :

  - **Satisfaire aux exigences de conformité**   Vous pouvez exporter le contenu d’une boîte aux lettres vers un fichier .pst pour satisfaire à des exigences de découverte légale. Après avoir terminé l’exportation, vous pouvez importer le contenu vers une boîte aux lettres utilisée spécifiquement à des fins de conformité.

  - **Créer un cliché instantané ponctuel de boîte aux lettres**   En créant un cliché instantané de boîtes aux lettres spécifiques, vous n’avez plus à conserver le jeu de sauvegarde complet pour une base de données de boîtes aux lettres.

  - **Transférer le fichier .pst d’un utilisateur vers sa boîte aux lettres ou son archive personnelle**   Les utilisateurs de Microsoft Outlook peuvent sauvegarder leurs courriers électroniques localement sous la forme de fichiers .pst. La cmdlet [New-MailboxImportRequest](https://technet.microsoft.com/fr-fr/library/ff607310\(v=exchg.150\)) permet de déplacer les données du fichier .pst d’un utilisateur vers sa boîte aux lettres ou son archive personnelle. C’est une méthode simple pour transférer des messages électroniques de l’ordinateur local d’un utilisateur vers des serveurs Exchange.

## Avantages associés à l’utilisation des demandes d’importation et d’exportation

Les avantages liés à l'utilisation de demandes d'importation et d'exportation dans Exchange 2013 sont les suivants :

  - Un fournisseur de .pst, capable de lire et d’écrire des fichiers .pst, est inclus dans Exchange 2013.

  - Les demandes d’importation et d’exportation sont asynchrones. Le traitement est géré par le service de réplication de boîte aux lettres Microsoft (MRS) qui tire parti des structures de limitation et de file d’attente.

  - Les fichiers .pst peuvent être directement importés dans l’archive personnelle d’un utilisateur.

  - Plusieurs fichiers .pst peuvent être importés ou exportés en même temps.

  - Les fichiers .pst peuvent résider sur n’importe quel lecteur réseau partagé accessible par vos serveurs Exchange.

  - Exchange 2013 prend en charge ces fichiers .pst : Fichiers Unicode créés par Office Outlook 2007 et Outlook 2010

## Considérations

Avant d’importer ou d’exporter des données de boîtes aux lettres, prenez en compte les éléments suivants :

  - Pour importer ou exporter des données de boîtes aux lettres, vous devez configurer un dossier partagé sur le réseau qui soit accessible par vos serveurs Exchange. Vous devez également accorder des autorisations d’accès en lecture/écriture au groupe du sous-système approuvé Exchange pour qu’il puisse accéder au partage réseau dans lequel vous importez ou exportez les données de boîtes aux lettres. Si vous n’accordez pas cette autorisation, vous recevrez un message d’erreur signalant que Microsoft Exchange ne parvient pas à établir de connexion avec la boîte aux lettres cible.

  - La taille maximale du fichier .pst prise en charge par Outlook est de 50 Go. Par conséquent, nous vous recommandons de ne pas importer de fichiers .pst supérieurs à 50 Go. Vous pouvez créer plusieurs fichiers .pst pour des boîtes aux lettres dépassant 50 Go en indiquant des dossiers spécifiques à inclure ou exclure ou bien en utilisant un filtre de contenu.

  - Les demandes d’importation ou d’exportation sont exécutées par le service de réplication de boîte aux lettres. Ce dernier traite également les demandes de déplacement et de restauration de boîtes aux lettres. Toutes les demandes sont mises en attente et limitées par MRS.

  - L’importation et l’exportation de données de boîtes aux lettres peut prendre plusieurs heures selon la taille du fichier, la bande passante réseau et la limitation du service de réplication de boîte aux lettres.

  - Vous ne pouvez pas importer de données dans un dossier public ou dans une base de données de dossiers publics.

## Importation de données de boîtes aux lettres

Utilisez le jeu de cmdlets **MailboxImportRequest** pour importer des données d’un fichier .pst dans une boîte aux lettres ou une archive personnelle. Voici la liste des options que vous pouvez utiliser lorsque vous importez des données de boîtes aux lettres à partir d’un fichier .pst :

> [!NOTE]
> La boîte aux lettres dans laquelle vous importez des données doit exister. Vous ne pouvez pas importer des données dans un compte d’utilisateur qui ne dispose pas d’une boîte aux lettres.


  - Vous pouvez importer des données dans un compte d’utilisateur différent de celui à partir duquel l’exportation a été effectuée. Par exemple, vous pouvez exporter des données de john@contoso.com et les importer dans legaldiscovery@contoso.com.

  - Vous pouvez importer des éléments dans l’archive personnelle de l’utilisateur uniquement en indiquant le paramètre *IsArchive*.

  - Si les messages de dossier associés existent dans le fichier .pst, vous pouvez les importer en utilisant le paramètre *AssociatedMessagesCopyOption*. Des messages associés contiennent des données masquées avec des informations sur les règles, les écrans et les formulaires. S’ils existent dans le fichier .pst, tous les messages du dispositif de sécurité sont importés.

  - Vous pouvez inclure ou exclure des dossiers spécifiques à l’aide du paramètre *IncludeFolders* ou *ExcludeFolders*.

  - Vous pouvez exclure le dossier Éléments récupérables à l’aide du paramètre *ExcludeDumpster*. Par défaut, une demande d’importation inclut le dossier Éléments récupérables de l’utilisateur si celui-ci est présent dans le fichier .pst.

## Cmdlets de demande d'importation de boîte aux lettres

Utilisez les cmdlets suivants pour les demandes d’importation de boîtes aux lettres.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>Lance le processus d’importation d’un fichier .pst dans une boîte aux lettres ou une archive personnelle. Vous pouvez créer plus d’une demande d’importation par boîte aux lettres. Chaque demande doit avoir un nom unique.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>Permet de modifier les options de demande d’importation après la création de la demande ou assure une reprise après l'échec de demandes d’importation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>Suspend une demande d’importation à n’importe quel moment une fois que la demande a été créée, mais avant que la demande n’ait atteint l’état Traitée.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>Reprend une demande d’importation interrompue ou ayant échoué.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>Supprime les demandes d’importation entièrement ou partiellement terminées. Les demandes d’importation terminées ne sont pas automatiquement effacées. Pour les supprimer, utilisez cette cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>Affiche des informations générales relatives à une demande d’importation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>Affiche des informations détaillées relatives à une demande d’importation.</p></td>
</tr>
</tbody>
</table>


## Exportation de données de boîtes aux lettres

Utilisez le jeu de cmdlets **MailboxExportRequest** pour exporter des données de boîtes aux lettres vers un fichier .pst. Vous pouvez exporter une ou plusieurs boîtes aux lettres mais une seule demande à la fois est écrite dans chaque fichier .pst. Voici la liste des options que vous pouvez utiliser lorsque vous exportez des données de boîtes aux lettres vers un fichier .pst :

  - Vous pouvez exporter des données d’archives personnelles à l’aide du paramètre *IsArchive*.

  - Vous pouvez filtrer les messages exportés à l’aide du paramètre *ContentFilter*. Vous pouvez filtrer par contenu de message, pièce jointe, expéditeurs, destinataires, catégorie de boîte de réception, importance, type de message, taille de message ainsi que par date d’envoi, de réception ou d’expiration du message.

  - Vous pouvez spécifier des dossiers à inclure ou exclure à l’aide du paramètre *IncludeFolders* ou *ExcludeFolders*. Si vous exportez des données à partir d’une boîte aux lettres Exchange 2013, vous pouvez également exclure le dossier Éléments récupérables à l’aide du paramètre *ExcludeDumpster*.

  - Vous pouvez exporter des messages associés à l’aide du paramètre *AssociatedMessagesCopyOption*. Des messages associés contiennent des données masquées avec des informations sur les règles, les écrans et les formulaires. Les éléments associés ne sont, par défaut, pas copiés dans le fichier .pst.

## Cmdlets de demande d'exportation de boîte aux lettres

Utilisez les cmdlets suivants pour les demandes d’exportation de boîtes aux lettres.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>Démarre le processus d’exportation de données vers un fichier .pst à partir d’une boîte aux lettres principale ou d’une archive personnelle. Vous pouvez créer plus d’une demande d’exportation par boîte aux lettres. Chaque demande doit avoir un nom unique.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>Permet de modifier les options de demande d’exportation après la création de la demande ou assure une reprise après l'échec d'une demande d’exportation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>Suspend une demande d’exportation à n’importe quel moment une fois que la demande a été créée, mais avant que la demande n’ait atteint l’état Traitée.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>Reprend une demande d’exportation interrompue ou ayant échoué.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>Supprime les demandes d’exportation entièrement ou partiellement terminées. Les demandes d’exportation terminées ne sont pas automatiquement effacées. Pour les supprimer, utilisez cette cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>Affiche des informations générales relatives à une demande d’exportation.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/fr-fr/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>Affiche des informations détaillées relatives à une demande d’exportation.</p></td>
</tr>
</tbody>
</table>

