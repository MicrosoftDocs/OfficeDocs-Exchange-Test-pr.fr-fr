---
title: 'Activer l’enregistrement des invites personnalisées à l’aide de l’interface utilisateur de téléphonie: Exchange 2013 Help'
TOCTitle: Activer l’enregistrement des invites personnalisées à l’aide de l’interface utilisateur de téléphonie
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54652775
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer l’enregistrement des invites personnalisées à l’aide de l’interface utilisateur de téléphonie

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2014-09-17_

Vous pouvez utiliser l'environnement de ligne de commande pour activer l'enregistrement des invites et des messages d'accueil personnalisés pour les plans de numérotation et les standards automatiques de messagerie unifiée à l'aide de l'interface utilisateur de téléphonie (TUI). Cela peut être utile si vous voulez modifier une annonce ou un message d'accueil personnalisés à l'aide du CAE ou de l'environnement de ligne de commande, ou en cas d'urgence telle que la fermeture d'une organisation pour des raisons météorologiques. Lorsque vous modifiez une annonce ou un message d’accueil personnalisé sur un standard automatique de messagerie unifiée, vous devez modifier l’enregistrement d’invite de la TUI sur le plan de numérotation auquel le standard automatique de messagerie unifiée est lié.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez les entrées « Plans de numérotation de messagerie unifiée » et « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

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

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour enregistrer une invite ou un message d'accueil personnalisé à l'aide de l'interface utilisateur de téléphonie

Pour enregistrer des invites et messages d'accueil personnalisés à l'aide de la TUI, procédez comme suit :

1.  Créez un compte d'utilisateur de domaine qui ne peut pas se connecter de façon interactive.

2.  Déléguez le rôle Administrateur d'organisation Exchange au compte d'utilisateur de domaine.

3.  Créez une boîte aux lettres pour l'utilisateur du domaine.

4.  Activez la boîte aux lettres de l'utilisateur du domaine pour la messagerie unifiée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Autorisez uniquement les administrateurs qui gèrent les invites et les messages d'accueil à accéder au numéro de poste et au code confidentiel du compte d'utilisateur. Utilisez ce compte d'utilisateur uniquement pour la gestion des invites par téléphone.</td>
    </tr>
    </tbody>
    </table>


5.  Créez un fichier .wav ou .wma à utiliser pour le message d'accueil personnalisé du plan de numérotation ou du standard automatique de messagerie unifiée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous ne pouvez pas utiliser des fichiers MP3 pour les invites personnalisées.</td>
    </tr>
    </tbody>
    </table>


6.  Utilisez le CAE ou l'environnement de ligne de commande pour configurer le plan de numérotation afin d'utiliser le message d'accueil personnalisé ou de configurer le standard automatique pour utiliser le message d'accueil des heures d'ouverture ou de fermeture. Pour plus d'informations sur la configuration d'un plan de numérotation, consultez la rubrique [Activation d’un message d’accueil personnalisé pour les utilisateurs d’Outlook Voice Access](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md). Pour plus de détails sur la configuration d'un standard automatique, consultez la rubrique [Activer un accueil pendant les heures personnalisé](enable-a-customized-business-hours-greeting-exchange-2013-help.md) ou [Activer un message d’accueil en dehors des heures d’ouverture personnalisé](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md).

7.  Exécutez la cmdlet suivante :
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Pour pouvoir activer l’enregistrement d’une invite ou d’un message d’accueil personnalisé, vous devez vous connecter à la boîte aux lettres configurée pour l’enregistrement des invites. Après avoir enregistré la nouvelle invite ou le nouveau message d'accueil, vous devez vous déconnecter, puis vous reconnecter pour pouvoir les entendre en utilisant la TUI.</td>
</tr>
</tbody>
</table>


## Enregistrer des invites de la TUI sur un standard automatique de messagerie unifiée

1.  Vérifiez que le standard automatique est lié au plan de numérotation que vous avez activé pour l’enregistrement d’invite de la TUI.

2.  Appelez le numéro de téléphone configuré sur le standard automatique de messagerie unifiée.

3.  Lors de la lecture des messages d'accueil des heures d'ouverture ou de fermeture du standard automatique, appuyez sur la touche dièse (\#), puis sur la touche étoile (\*).

4.  Vous êtes invité à entrer le numéro de poste de l'utilisateur. Entrez le numéro de poste de l'utilisateur à extension messagerie unifiée qui est autorisé à procéder à l'enregistrement d'invites de la TUI.

5.  Vous êtes invité à entrer un code confidentiel. Entrez le code confidentiel de l’utilisateur.

6.  Suivez les invites du système pour modifier ou mettre à jour le message d'accueil ou le message d'information automatique pour le standard automatique.

## Enregistrer l'invite de la TUI sur un plan de numérotation de messagerie unifiée

1.  Appelez un numéro Outlook Voice Access que vous utilisez pour vous connecter à Outlook Voice Access.

2.  Pendant la lecture du message d'accueil du standard automatique, appuyez sur la touche dièse (\#), puis sur la touche étoile (\*).

3.  Si vous appelez à partir d'un téléphone utilisé par un utilisateur à extension messagerie unifiée, vous êtes invité à entrer un code confidentiel. Au lieu d'entrer le code confidentiel, appuyez sur la touche étoile (\*). Vous êtes invité à entrer un numéro de poste. Entrez le numéro de poste de l'utilisateur à extension messagerie unifiée qui est autorisé à procéder à l'enregistrement d'invites de la TUI.

4.  Si vous appelez à partir d'un téléphone qui n'est pas utilisé par un utilisateur à extension messagerie unifiée, un numéro de poste vous est automatiquement demandé. Entrez le numéro de poste de l'utilisateur à extension messagerie unifiée qui est autorisé à procéder à l'enregistrement d'invites de la TUI.

5.  Vous êtes invité à entrer un code confidentiel. Entrez le code confidentiel de l’utilisateur.

6.  Suivez les invites du système pour modifier ou mettre à jour le message d'accueil pour le plan de numérotation ou le message d'information automatique.

