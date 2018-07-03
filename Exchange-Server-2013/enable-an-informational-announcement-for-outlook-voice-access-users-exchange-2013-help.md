---
title: 'Activer une annonce d’information pour les utilisateurs d’Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Activer une annonce d’information pour les utilisateurs d’Outlook Voice Access
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50555483
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer une annonce d’information pour les utilisateurs d’Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez activer une annonce ayant valeur d’informations sur un plan de numérotation de messagerie unifiée. Les annonces ayant valeur d’informations sont utilisées pour des annonces générales qui changent plus fréquemment que le message de bienvenue ou pour des annonces requises par des stratégies de conformité d’entreprise.

Par défaut, les appelants, y compris les utilisateurs d’Outlook Voice Access qui se connectent à un numéro Outlook Voice Access qui a été configuré, n’entendent pas une annonce ayant valeur d’informations. Pour qu’une annonce soit lue, vous devez créer un fichier .wav ou .wma à utiliser pour l’annonce ayant valeur d’informations après avoir créé un plan de numérotation de messagerie unifiée, et activer ensuite l’annonce ayant valeur d’informations sur le plan de numérotation.

S’il est important que les appelants entendent l’annonce ayant valeur d’informations dans son intégralité, vous pouvez configurer l’annonce comme ne pouvant pas être interrompue. Ainsi les appelants ne peuvent ni appuyer sur une touche ni énoncer une commande risquant d’interrompre et de mettre fin à l’annonce ayant valeur d’informations.

Pour plus d’informations sur les options de menu qui sont disponibles pour les utilisateurs de Outlook Voice Access, consultez le Guide de référence rapide pour Outlook Voice Access, qui est disponible à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour activer une annonce ayant valeur d’informations

1.  Dans le Centre d’administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l’affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Outlook Voice Access**, sous **Annonce ayant valeur d’informations**, cliquez sur **Modifier**, puis cliquez sur **Parcourir** pour rechercher le fichier d’annonces.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le fichier que vous utilisez pour l’annonce ayant valeur d’informations doit être un fichier .wav ou .wma.</td>
    </tr>
    </tbody>
    </table>


5.  Après avoir localisé le fichier, cliquez sur **Ouvrir**, puis sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer une annonce ayant valeur d'informations

Dans cet exemple, nous activons une annonce ayant valeur d’informations qui utilise le fichier d’annonce « informational.wav » sur le plan de numérotation de messagerie unifiée intitulé `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav

