---
title: 'Consulter le journal d’audit de l’administrateur: Exchange 2013 Help'
TOCTitle: Consulter le journal d’audit de l’administrateur
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56269201
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consulter le journal d’audit de l’administrateur

 

_**Sapplique à :** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-05-03_

Dans Microsoft Exchange Online Protection (EOP), Microsoft Exchange Online et Microsoft Exchange 2013, vous pouvez utiliser le Centre d’administration Exchange (CAE) pour rechercher et afficher des entrées dans le *journal d’audit de l’administrateur*. Le journal d’audit de l’administrateur enregistre des actions spécifiques, basées sur la cmdlet Environnement de ligne de commande Exchange Management Shell, effectuées par les administrateurs et les utilisateurs disposant de privilèges d’administration. Les entrées du journal d’audit de l’administrateur vous fournissent des informations sur la cmdlet qui a été exécutée, les paramètres utilisés, l’utilisateur qui a exécuté la cmdlet et les objets concernés.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>La journalisation d’audit de l’administrateur est activée par défaut.</p></li>
<li><p>Le journal d’audit de l’administrateur n’enregistre aucune action basée sur une cmdlet Environnement de ligne de commande Exchange Management Shell qui commence avec le verbe <strong>Get</strong>, <strong>Search</strong> ou <strong>Test</strong>.</p></li>
<li><p>Les entrées du journal d’audit sont conservées pendant 90 jours. Lorsqu’une entrée remonte à plus de 90 jours, elle est supprimée.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Afficher les rapports » dans la rubrique [Feature permissions in EOP](https://technet.microsoft.com/fr-fr/library/jj723125\(v=exchg.150\)).

  - Comme indiqué précédemment, la journalisation d’audit de l’administrateur est activée par défaut. Pour vérifier qu’elle a été activée, vous pouvez exécuter la commande suivante :
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    Dans Exchange 2013, vous pouvez activer la journalisation d’audit de l’administrateur si elle est désactivée en exécutant la commande suivante.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    Dans Exchange Online Protection et Exchange Online, la journalisation d’audit de l’administrateur est toujours activée. Elle ne peut pas être désactivée.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser le Centre d’administration Exchange (CAE) pour consulter le journal d’audit de l’administrateur

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Audit**, puis sélectionnez **Exécuter le rapport du journal d’audit de l’administrateur**.

2.  Choisissez une **date de début** et une **date de fin**, puis choisissez **Rechercher**. Toutes les modifications de configuration effectuées pendant la période spécifiée sont affichées et peuvent être triées, avec les informations suivantes :
    
      - **Date**   Date et heure auxquelles la modification de configuration a été effectuée. La date et l’heure sont enregistrées au format temps universel coordonné (UTC).
    
      - **Cmdlet**   Nom de la cmdlet qui a été utilisée pour la modification de configuration.
    
      - **Utilisateur**   Nom du compte de l’utilisateur qui a effectué la modification de configuration.
    
    Jusqu’à 5 000 entrées s’affichent sur plusieurs pages. Si vous devez affiner vos résultats, spécifiez une plage de dates plus courte. Si vous sélectionnez un seul résultat de recherche, l’information supplémentaire suivante s’affiche dans le volet de détails :
    
      - **Objet modifié**   Objet qui a été modifié par la cmdlet.
    
      - **Paramètres (Parameter:Value)**   Paramètres de cmdlet qui ont été utilisés et valeurs indiquées avec ces paramètres.

3.  Si vous souhaitez imprimer une entrée du journal d’audit spécifique, choisissez le bouton **Imprimer** dans le volet de détails.

## Comment savoir si cela a fonctionné ?

Si vous avez exécuté avec succès un rapport de journal d’audit de l’administrateur, les modifications de configuration effectuées dans la plage de dates indiquée sont affichées dans le volet des résultats de la recherche. Si aucun résultat n’apparaît, modifiez la plage de dates et réexécutez le rapport.

> [!NOTE]
> Lorsqu’une modification est apportée à votre organisation, cela peut prendre jusqu’à 15 minutes avant qu’elle n’apparaisse dans les résultats de recherche du journal d’audit. Si une modification n’apparaît pas dans le journal d’audit de l’administrateur, patientez quelques minutes, puis réeffectuez la recherche.

