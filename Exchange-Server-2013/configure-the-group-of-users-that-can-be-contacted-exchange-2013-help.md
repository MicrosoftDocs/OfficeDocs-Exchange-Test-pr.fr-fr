---
title: "Configurer le groupe d'utilisateurs qui peuvent être contactés: Exchange 2013 Help"
TOCTitle: Configurer le groupe d'utilisateurs qui peuvent être contactés
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52057070
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le groupe d'utilisateurs qui peuvent être contactés

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2012-12-09_

Vous pouvez indiquer le groupe d'utilisateurs que les appelants peuvent contacter sur un standard automatique de messagerie unifiée. Par défaut, les appelants peuvent contacter les utilisateurs appartenant au même plan de numérotation associé au standard automatique de messagerie unifiée. Toutefois, vous pouvez modifier le regroupement d'utilisateurs afin de permettre aux appelants de transférer des appels ou d'envoyer des messages vocaux à des utilisateurs présents dans le carnet d'adresses d'une organisation ou à un ensemble spécifique d'utilisateurs.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Gérer un standard automatique de messagerie unifiée](manage-a-um-auto-attendant-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

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

## Utiliser le CAE pour configurer le groupe d'utilisateurs que les appelants peuvent contacter

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**. Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, sélectionnez le standard automatique de messagerie unifiée à configurer, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Standard automatique de messagerie unifiée** \> **Accès au carnet d'adresses et à l'opérateur**, sous **Options de recherche dans le carnet d'adresses**, activez l'une des options suivantes :
    
      - **Dans ce plan de numérotation seulement**   Activez cette option pour permettre aux appelants qui se connectent au standard automatique de messagerie unifiée de localiser et de contacter des utilisateurs se trouvant dans le même plan de numérotation associé à ce standard automatique de messagerie unifiée.
    
      - **Dans toute l'organisation**   Activez cette option pour permettre aux appelants qui se connectent au standard automatique de messagerie unifiée de localiser et de contacter toute personne répertoriée dans le carnet d'adresses de l'organisation. Cela inclut tous les utilisateurs à extension boîte aux lettres.

4.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande pour configurer le groupe d'utilisateurs que les appelants peuvent contacter

Cet exemple définit l'étendue des utilisateurs que les appelants peuvent contacter sur tous les utilisateurs du carnet d'adresses de l'organisation via un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

