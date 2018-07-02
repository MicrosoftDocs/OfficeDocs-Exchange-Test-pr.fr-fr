---
title: "Suppression d'un module linguistique de messagerie unifiée: Exchange 2013 Help"
TOCTitle: Suppression d'un module linguistique de messagerie unifiée
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50478930
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suppression d'un module linguistique de messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-14_

Vous pouvez utiliser le Centre d'administration Exchange ou l'environnement de ligne de commande pour gérer les langues de la messagerie unifiée sur les serveurs de boîtes aux lettres qui exécutent le service de messagerie unifiée Microsoft Exchange. Toutefois, pour supprimer une langue de la liste d'un plan de numérotation de messagerie unifiée, vous devez supprimer le module linguistique de messagerie unifiée approprié du serveur de boîtes aux lettres en utilisant la commande **Setup.exe /RemoveUmLanguagePack**. Une fois que vous avez supprimé le module linguistique de messagerie unifiée du serveur de boîtes aux lettres, la langue n'est plus disponible lorsque vous configurez un plan de numérotation de messagerie unifiée ou un standard automatique de messagerie unifiée. Pour afficher les modules linguistiques de messagerie unifiée installés, vous devez afficher les propriétés du serveur de boîtes aux lettres ou utiliser la cmdlet **Get-UMService**.

Pour les tâches supplémentaires concernant les modules linguistiques de messagerie unifiée, consultez la rubrique [Procédures de langages, les invites et le message d'accueil de la messagerie unifiée](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Serveur de boîtes aux lettres (service de messagerie unifiée) » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifier qu'un module linguistique de messagerie unifiée autre que le module en-US est installé.

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


## Utilisation de Setup.exe pour supprimer un module linguistique de messagerie unifiée.

Depuis une invite de commandes, exécutez la commande suivante.

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

Dans la commande précédente, *\<UmLanguagePackName\>* est le nom du module linguistique de messagerie unifiée ; par exemple, fr-FR.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dès lors que vous avez installé des mises à jour, vous ne pouvez plus utiliser le fichier Setup.exe situé dans le dossier \Bin pour supprimer un module linguistique de messagerie unifiée. Vous devez utiliser le fichier Setup.exe à partir du DVD Exchange 2013 ou des fichiers source téléchargés. Si vous ne le faites pas, l'erreur suivante s'affiche : Il existe une incohérence de version entre l'application en cours d'exécution et l'application installée.</td>
</tr>
</tbody>
</table>

