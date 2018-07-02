---
title: 'Modifier les stratégies d’archivage: Exchange 2013 Help'
TOCTitle: Modifier les stratégies d’archivage
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50477738
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier les stratégies d’archivage

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-02-01_

Dans Exchange Server 2013 et Exchange Online, vous pouvez utiliser des stratégies d’archivage pour déplacer automatiquement des éléments de boîte aux lettres vers des archives personnelles (locales) ou des archives en nuage. Les stratégies d’archivage sont des balises de rétention qui utilisent l’action de rétention **Déplacer vers l’archive**.

Le programme d’installation d’Exchange crée une stratégie de rétention appelée **stratégie MRM par défaut**. Une balise de stratégie par défaut qui déplace les éléments vers la boîte aux lettres d’archivage au bout de deux ans est affectée à cette stratégie. La stratégie inclut également de nombreuses balises personnelles que les utilisateurs peuvent appliquer à des dossiers ou des éléments de boîte aux lettres pour déplacer ou supprimer automatiquement des messages. Si aucune stratégie de rétention n’est affectée à une boîte aux lettres dont l’archivage est activé, Exchange lui applique automatiquement la **stratégie MRM par défaut**. Vous pouvez également créer vos propres stratégies d’archivage et de rétention et les appliquer aux utilisateurs de boîtes aux lettres. Pour en savoir plus, consultez la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

Vous pouvez modifier les balises de rétention incluses dans la stratégie par défaut pour répondre aux besoins de votre entreprise. Par exemple, vous pouvez modifier la balise de stratégie d’archivage par défaut pour déplacer les éléments vers l’archive au bout de trois ans au lieu de deux. Vous pouvez également créer des balises personnelles supplémentaires pour les ajouter à une stratégie de rétention, notamment la **stratégie MRM par défaut** ou autoriser les utilisateurs à ajouter des balises personnelles à leurs boîtes aux lettres à partir des options d’Outlook Web App.

Pour découvrir d’autres tâches de gestion associées aux archives, consultez :

  - **Exchange Server 2013:** [Gestion des archives permanentes dans Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [Activer ou désactiver une boîte aux lettres d’archivage dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj984357\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans un déploiement hybride Exchange, vous pouvez activer une boîte aux lettres d’archivage en nuage pour une boîte aux lettres principale locale. Si vous attribuez une stratégie d’archivage à une boîte aux lettres locale, les éléments sont déplacés vers l’archive en nuage. Si un élément est déplacé vers la boîte aux lettres d’archivage, une copie n’est pas conservée dans la boîte aux lettres locale. Si la boîte aux lettres locale est placée en conservation, une stratégie d’archivage déplacera les éléments vers la boîte aux lettres d’archivage en nuage dans laquelle ils sont conservés pendant la durée spécifiée par la conservation.</td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Gestion des enregistrements de messagerie » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange pour modifier la stratégie d’archivage par défaut

1.  Accédez à **Gestion de la conformité** \> **Balises de rétention**.

2.  Dans l’affichage Liste, sélectionnez la balise **Déplacement vers l’archive après 2 ans - Par défaut**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous pouvez cliquer sur la colonne <strong>TYPE</strong> pour trier les balises de rétention par type. La stratégie d’archivage par défaut indique le type <strong>Par défaut</strong> et l’action de rétention <strong>Archive</strong>. Vous pouvez également cliquer sur <strong>NOM</strong> pour trier les balises de rétention par nom.</td>
    </tr>
    </tbody>
    </table>


3.  
    
    Dans **Balise de rétention**, affichez ou modifiez les paramètres suivants, puis cliquez sur **Enregistrer** :
    
      - **Nom**   Ce champ situé en haut de la page permet d’afficher ou de modifier le nom de la balise.
    
      - **Type de balise de rétention**   Ce champ en lecture seule affiche le type de balise.
    
      - **Action de rétention**   Ne modifiez pas ce champ pour les stratégies d’archivage.
    
      - **Période de rétention** Sélectionnez l’une des options suivantes :
        
          - **Jamais**   Cliquez sur ce bouton pour désactiver la balise. Si la balise de stratégie par défaut est désactivée, elle ne s’applique plus à la boîte aux lettres.
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Les éléments ayant une balise de rétention désactivée ne sont pas traités par l’Assistant de boîte aux lettres. Pour empêcher l’application d’une balise aux éléments, nous vous recommandons de désactiver la balise plutôt que de la supprimer. Lorsque vous supprimez une balise, la configuration de la balise est supprimée d’Active Directory et l’Assistant de boîte aux lettres traite tous les messages pour enlever la balise supprimée.</td>
            </tr>
            </tbody>
            </table>
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>Si un utilisateur applique une balise à un élément en pensant que cet élément ne sera jamais déplacé, son activation ultérieure peut entraîner le déplacement d’éléments que l’utilisateur souhaitait conserver dans la boîte aux lettres principale.</td>
            </tr>
            </tbody>
            </table>
        
          - **Lorsque l'élément atteint l'âge suivant (en jours)**   Cliquez sur ce bouton pour indiquer que les éléments doivent être déplacés au bout d’un certain temps. Par défaut, ce paramètre est configuré pour déplacer les éléments vers l’archive après un délai de deux ans (730 jours). Pour modifier ce paramètre, dans la zone de texte correspondante, tapez le nombre de jours de la période de rétention. La valeur peut être comprise entre 1 et 24 855 jours.
    
      - **Commentaire**   Cette zone permet d'entrer un commentaire à l'attention des utilisateurs d'Outlook et d'Outlook Web App.

## Utilisation de l’environnement de ligne de commande Exchange Management Shell pour modifier les stratégies d’archivage

Cet exemple illustre la modification de la balise `Default 2 year move to archive` pour déplacer des éléments au bout de 1 095 jours (3 ans).

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

Cet exemple illustre la désactivation de la balise `Default 2 year move to archive`.

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

Cet exemple illustre la récupération de toutes les balises de stratégie d’archivage par défaut et les balises personnelles, ainsi que leur désactivation.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298042\(v=exchg.150\)) et [Get-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298009\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Utilisez la cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/fr-fr/library/dd298009\(v=exchg.150\)) pour récupérer les paramètres de la balise de rétention.

Cette commande permet de récupérer les propriétés de la balise de rétention `Default 2 year move to archive` et de transférer la sortie vers la cmdlet **Format-List** pour afficher toutes les propriétés sous forme de liste.

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

