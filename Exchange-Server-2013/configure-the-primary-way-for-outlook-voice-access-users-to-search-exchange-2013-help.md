---
title: 'Configurer le principal moyen pour les utilisateurs Outlook Voice Access pour la recherche: Exchange 2013 Help'
TOCTitle: Configurer le principal moyen pour les utilisateurs Outlook Voice Access pour la recherche
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 50477945
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le principal moyen pour les utilisateurs Outlook Voice Access pour la recherche

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-02-21_

Lors de la création d'un plan de numérotation de messagerie unifiée, vous pouvez configurer les méthodes principale et secondaire que les appelants vont utiliser pour rechercher des noms et retrouver un utilisateur quand ils appellent un numéro Outlook Voice Access ou un standard automatique de messagerie unifiée associé au plan de numérotation. Les appelants peuvent utiliser des entrées à tonalité pour retrouver un utilisateur à extension messagerie unifiée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'option <strong>Aucune</strong> n'est pas disponible comme méthode principale utilisée par des appelants pour rechercher des noms. Lorsque l'option <strong>Aucune</strong> est sélectionnée pour la méthode secondaire de recherche de noms, seule la méthode principale est proposée aux appelants. Si vous configurez les deux méthodes de recherche de noms par les appelants, ils seront invités à choisir l'une des deux méthodes.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

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

## Utiliser le CAE pour modifier la méthode principale de numérotation selon le nom

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Méthode principale pour rechercher des noms**, utilisez la liste déroulante pour sélectionner l'option que vous souhaitez :
    
      - **Nom Prénom** (par défaut)
    
      - **Prénom Nom**
    
      - **Adresse SMTP**

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour modifier la numérotation primaire par nom de méthode

Cet exemple permet de définir la numérotation principale par nom à `FirstLast`. Cette action permet aux appelants qui contactent le numéro Outlook ou un standard automatique de messagerie unifiée associé au plan de numérotation de rechercher un utilisateur à extension messagerie unifiée en fonction de son prénom et de son nom.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

Cet exemple permet de définir la numérotation principale par nom à `LastFirst`. Cette action permet aux appelants qui contactent le numéro Outlook Voice Access ou un standard automatique de messagerie unifiée associé au plan de numérotation de rechercher un utilisateur à extension messagerie unifiée en fonction de son nom et de son prénom.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

Cet exemple permet de définir la numérotation principale par nom à `SMTP address`. Cette action permet aux appelants qui contactent le numéro Outlook Voice Access ou un standard automatique de messagerie unifiée associé au plan de numérotation de rechercher un utilisateur à extension messagerie unifiée en fonction de son adresse SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress

