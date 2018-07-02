---
title: "Créer une règle de protection d'Outlook: Exchange 2013 Help"
TOCTitle: Créer une règle de protection d'Outlook
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50479326
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une règle de protection d'Outlook

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

À l'aide des règles de protection de Microsoft Outlook, vous pouvez protéger des messages avec la Gestion des droits relatifs à l'information, en appliquant un modèle de services Active Directory RMS (Rights Management Services) dans Outlook 2010, avant l'envoi des messages.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 1 minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Protection des droits » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un serveur [AD RMS](https://technet.microsoft.com/fr-fr/library/hh831364.aspx) doit avoir été déployé dans la même forêt Active Directory que celle sur laquelle votre serveur exécute Microsoft Exchange Server 2013.

  - Si vous configurez des règles de protection Outlook avec des messages protégés par la gestion des droits relatifs à l'information, pensez à activer le déchiffrement de transport pour permettre aux agents de transport, y compris à l'agent Règles de transport, de déchiffrer et d'accéder au message. Si vous utilisez la journalisation, vous pouvez aussi envisager l'activation du déchiffrement du rapport de journal pour permettre à l'agent de journalisation d'enregistrer une copie non chiffrée du message dans le rapport du journal. Pour plus d'informations, consultez la rubrique [Déchiffrement de l'état de journal](journal-report-decryption-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour créer des règles de protection Outlook. Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell.

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


## Utiliser le shell pour créer une règle de protection Outlook

Cet exemple crée la règle de protection Outlook Projet Contoso. La règle protège des messages envoyés au groupe de distribution ContosoPMs avec le modèle AD RMS Business Critical.

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous utilisez le prédicat <code>SentTo</code> pour une règle de protection Outlook et spécifiez un groupe de distribution, seuls les messages destinés au groupe de distribution dans les champs À, Cc ou Cci sont protégés par IRM. La protection de la gestion des droits relatifs à l'information n'est pas appliquée à tous les messages adressés à des membres individuels du groupe de distribution.</td>
</tr>
</tbody>
</table>


Vous pouvez aussi utiliser les prédicats `FromDepartment` et `SentToScope` pour appliquer une protection de la gestion des droits relatifs à l'information aux messages envoyés par des utilisateurs dans le service spécifié ou les messages envoyés vers l'étendue indiquée (`InOrganization` pour des messages internes, `All` pour tous les destinataires).

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd298182\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien créé une règle de protection Outlook, procédez comme suit :

  - Exécutez la cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd298004\(v=exchg.150\)) pour vous assurer que la règle a bien été créée et afficher ses propriétés. Pour obtenir un exemple de récupération d’une règle de protection Outlook, reportez-vous à la section [Examples](https://technet.microsoft.com/fr-fr/dd298004\(exchg.150\)#examples) de la rubrique **Get-OutlookProtectionRule**.

  - Utilisez Outlook 2010 pour créer un message de test répondant à la condition de la règle et vous assurer que la règle est déclenchée sur le client.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous devrez éventuellement patienter quelques minutes avant qu’une règle de protection Outlook ne soit disponible dans Outlook.</td>
    </tr>
    </tbody>
    </table>

