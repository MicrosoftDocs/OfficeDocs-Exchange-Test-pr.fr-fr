---
title: 'Définir la langue par défaut sur un plan de numérotation: Exchange 2013 Help'
TOCTitle: Définir la langue par défaut sur un plan de numérotation
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50555417
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir la langue par défaut sur un plan de numérotation

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez définir la langue par défaut pour un plan de numérotation de messagerie unifiée. Chaque plan de numérotation que vous créez utilise initialement l'anglais (en-US) comme langue par défaut. Le module linguistique anglais (en-US) est installé sur toutes les versions de Microsoft Exchange Server 2013 et ne peut pas être supprimé.

Si vous souhaitez sélectionner une autre langue que la langue par défaut, par exemple, allemand (de-DE), vous devez tout d’abord télécharger l’allemand UM language pack fichier .exe à partir de [Modules linguistiques messagerie UNIFIÉE d’Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=266542) et installer le module linguistique sur le serveur de boîtes aux lettres en utilisant le fichier d’installation UMLanguagePack.de-de.exe. Après avoir installé le pack de langue, vous pouvez définir la langue par défaut pour une langue autre que l’anglais (en-US) sur vos plans de numérotation de messagerie UNIFIÉE.

Pour les tâches supplémentaires concernant les modules linguistiques de messagerie unifiée, consultez la rubrique [Procédures de langages, les invites et le message d'accueil de la messagerie unifiée](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour définir la langue par défaut dans un plan de numérotation de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis, dans la barre d'outils, cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans la page **Paramètres**, sous **Langue audio**, sélectionnez dans la liste déroulante la langue que vous souhaitez définir.

5.  Cliquez sur **Enregistrer** pour accepter les modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir la langue par défaut dans un plan de numérotation de messagerie unifiée

Cet exemple montre comment définir l'allemand comme langue par défaut dans un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

Cet exemple montre comment définir le japonais comme langue par défaut dans un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

Cet exemple montre comment définir l'anglais australien comme langue par défaut dans un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

