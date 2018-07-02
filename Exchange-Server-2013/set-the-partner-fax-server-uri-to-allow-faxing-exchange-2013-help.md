---
title: 'Définir le partenaire de serveur de télécopie URI pour permettre l’envoi de télécopies: Exchange 2013 Help'
TOCTitle: Définir le partenaire de serveur de télécopie URI pour permettre l’envoi de télécopies
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52057099
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Définir le partenaire de serveur de télécopie URI pour permettre l’envoi de télécopies

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Vous pouvez activer ou désactiver les télécopies entrantes pour les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée. Par défaut, quand vous activez la messagerie unifiée pour des utilisateurs, ces derniers ne peuvent recevoir de messages de télécopie que si vous activez les télécopies entrantes dans la stratégie de boîte aux lettres de messagerie unifiée et spécifiez l'URI du serveur de télécopie partenaire. Si les URI sont configurés dans la stratégie de boîte aux lettres de messagerie unifiée, mais que l'option autorisant les télécopies entrantes est désactivée dans le plan de numérotation de messagerie unifiée, les utilisateurs à extension messagerie unifiée ne pourront toujours pas recevoir de télécopies.

Pour plus d’informations sur les partenaires de télécopie, consultez [Microsoft PinPoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

Pour découvrir d'autres tâches de gestion relatives à la télécopie, consultez la rubrique [Procédures d'envoi de télécopie](faxing-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies de boîte aux lettres de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).

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

## Utiliser le Centre d'administration Exchange (CAE) pour définir l'URI de partenaire de télécopie

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Stratégies de boîte aux lettres de messagerie unifiée**, sélectionnez la stratégie à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Stratégie de boîte aux lettres de messagerie unifiée** \> **Général**, dans la zone **URI de serveur de télécopie partenaire**, entrez l'URI TCP ou TLS. Par exemple : *sip:faxserver1.contoso.com:5060;transport=tcp* ou *sip:faxserver2.contoso.com:5061;transport=tls*
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Bien que vous puissiez entrer plusieurs URI de serveurs de télécopie, un seul sera utilisé. Si vous entrez deux URI, seul le premier sera utilisé.</td>
    </tr>
    </tbody>
    </table>


4.  Cliquez sur **Enregistrer** pour enregistrer vos modifications.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour définir l'URI de partenaire de télécopie

Cet exemple permet aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `UMDialPlan Default Policy` d'utiliser TCP avec le port 5060 pour le serveur de télécopie partenaire`faxserver1`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

Cet exemple permet aux utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée `UMDialPlan Default Policy` d'utiliser TLS avec le port 5061 pour le serveur de télécopie partenaire`faxserver2`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

