---
title: 'Sélectionnez la langue pour une surveillance automatique: Exchange 2013 Help'
TOCTitle: Sélectionnez la langue pour une surveillance automatique
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50555373
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sélectionnez la langue pour une surveillance automatique

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez configurer le paramètre de langue d'invite par défaut sur un standard automatique de messagerie unifiée. Le paramètre de langue disponible sur un standard automatique de messagerie unifiée vous permet de configurer la langue d'invite par défaut sur le standard automatique. Lorsque vous utilisez les invites système par défaut pour le standard automatique, il s'agit de la langue que l'appelant entend lorsque le standard automatique répond à l'appel entrant. Ce paramètre de langue affecte seulement les invites système par défaut qui sont fournies après que vous avez installé le serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange. Ce paramètre est sans effet sur les invites personnalisées configurées sur un standard automatique. Les langues disponibles sont basées sur les modules linguistiques de messagerie unifiée installés sur le serveur de boîtes aux lettres.

Chaque surveillance automatique vous créez initialement utilisera anglais (en-US) comme la langue par défaut. Le pack de langue anglais (en-US) est installé par défaut sur toutes les versions de Microsoft Exchange 2013 et ne peut pas être supprimé. Si vous souhaitez sélectionner une autre langue, par exemple, allemand (de-DE), vous devez tout d’abord télécharger l’allemand UM language pack fichier .exe à partir de [Modules linguistiques messagerie UNIFIÉE d’Exchange Server 2013](https://go.microsoft.com/fwlink/?linkid=266542) et installer le module linguistique de messagerie UNIFIÉE sur le serveur de boîtes aux lettres en utilisant le fichier d’installation UMLanguagePack.de-de.exe. Après avoir installé le module linguistique de messagerie UNIFIÉE, vous pouvez définir la langue par défaut pour une langue autre que l’anglais (en-US) sur les surveillances automatiques de MU.

Pour les tâches supplémentaires concernant les modules linguistiques de messagerie unifiée, consultez la rubrique [Procédures de langages, les invites et le message d'accueil de la messagerie unifiée](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d’exécuter ces procédures, vérifiez qu’un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un standard automatique de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer le paramètre de langue par défaut

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans la page **Général**, sous **Langue de l'interface vocale automatisée**, sélectionnez la langue désirée dans la liste déroulante.

5.  Cliquez sur **Enregistrer** pour accepter les modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le paramètre de langue par défaut

Cet exemple montre comment définir l'anglais (Grande-Bretagne) comme langue par défaut sur un standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

Cet exemple montre comment définir l'allemand comme langue par défaut sur un standard automatique de messagerie unifiée `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

