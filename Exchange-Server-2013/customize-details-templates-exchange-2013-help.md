---
title: 'Personnaliser les modèles de détails: Exchange 2013 Help'
TOCTitle: Personnaliser les modèles de détails
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 50478904
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Personnaliser les modèles de détails

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-09-25_

L’éditeur de modèles de détails permet de personnaliser la présentation d’interface utilisateur graphique (GUI) côté client des propriétés d’objet accessibles à l’aide de listes d’adresses dans MicrosoftOutlook. Par exemple, quand un utilisateur ouvre une liste d'adresses dans Outlook, les propriétés d'un objet particulier sont présentées telles que définies par le modèle de détails dans l'organisation Exchange. Vous pouvez personnaliser les objets en modifiant les tailles de champ, en ajoutant ou supprimant des champs ou des onglets, ainsi qu'en réorganisant les champs. La disposition de ces modèles peut varier en fonction de la langue.

## Ce qu’il faut savoir avant de commencer ?

  - Il n'y a aucune option d'annulation dans l'éditeur de modèles de détails. Si vous faites une erreur, vous devez revenir à la version précédente. Pour plus d’informations, voir [Restaurer un modèle de détails sur la configuration par défaut](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md).

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Modèles de détails » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Personnaliser le modèle de détails

1.  Dans la **Boîte à outils Exchange**, cliquez sur **Éditeur de modèles de détails**, puis dans le volet d'actions, cliquez sur **Ouvrir l’outil**.

2.  Dans l'arborescence de l'éditeur de modèles de détails, cliquez sur **Modèles de détails**.
    
    Dans le volet d'informations, les colonnes suivantes sont affichées :
    
      - **Langue**   Cette colonne indique la langue dans laquelle le modèle a été créé.
    
      - **Type de modèle**   Cette colonne indique le type de modèle que vous pouvez personnaliser.
    
      - **Identité**   Cette colonne indique l'identité unique du modèle.
    
      - **Créé**   Cette colonne indique la date et l'heure de création du modèle.
    
      - **Modifié**   Cette colonne indique la date et l'heure de la dernière modification du modèle.

3.  Pour modifier un modèle, cliquez dessus, puis dans le volet Actions, cliquez sur **Modifier**. Par exemple, le modèle de détails des contacts **Anglais (États-Unis)** est illustré dans la figure suivante.
    
    **Modèle de détails par défaut tel que présenté dans Outlook 2013**
    
    ![Modèle de détails par défaut dans Outlook 2007](images/JJ556601.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Modèle de détails par défaut dans Outlook 2007")  

4.  Après avoir cliqué sur **Modifier**, vous pouvez exécuter plusieurs tâches pour personnaliser un modèle de détails :
    
      - Pour déplacer un objet dans le volet de conception, sélectionnez l'objet, puis faites-le glisser vers le nouvel emplacement dans le modèle. Lors du déplacement de l'objet, les lignes d'alignement s'affichent.
    
      - Pour modifier le texte d'une étiquette, sélectionnez-la dans le volet de conception. Dans le volet des propriétés, tapez le nouveau texte dans la zone **Texte**. Pour créer des raccourcis clavier, vous pouvez utiliser le symbole esperluette (&). Insérez l'esperluette (&) devant la lettre que vous voulez utiliser comme raccourci.
    
      - Pour modifier la taille d'un objet, sélectionnez-le, puis faites glisser les poignées de redimensionnement jusqu'à ce que l'objet ait la forme et la taille souhaitées.
    
      - Pour supprimer un objet, sélectionnez-le et appuyez sur la touche SUPPR.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>L’Éditeur de modèles de détails ne contient pas de bouton <strong>Annuler</strong> ; vous ne pouvez pas non plus utiliser de raccourci clavier pour annuler une action. Pour annuler un ajout apporté au modèle, vous devez utiliser la touche SUPPR. Pour annuler une suppression, vous devez appliquer de nouveau le paramètre. Vous pouvez également rétablir les paramètres originaux en quittant l'éditeur de modèles de détails sans enregistrer les modifications. Pour annuler des modifications après les avoir enregistrées, vous pouvez restaurer le modèle. Lorsque vous restaurez un modèle, toute la personnalisation est perdue et la configuration originale du modèle est restaurée. Pour plus d'informations sur la procédure de restauration du modèle de détails, voir <a href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">Restaurer un modèle de détails sur la configuration par défaut</a>.</td>
        </tr>
        </tbody>
        </table>
    
      - Pour ajouter des zones de texte « Modifier », des zones de liste, des zones déroulantes à plusieurs valeurs ou des zones de liste à plusieurs valeurs, faites glisser l'objet depuis le volet de la boîte à outils vers le volet de conception. Définissez l'attribut de l'objet en cliquant sur la zone déroulante de l'attribut dans le volet des propriétés, puis sélectionnez l'attribut qui sera utilisé par Exchange.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Vous devez lier un objet à un attribut pour qu'il soit utilisé par Exchange. L'attribut détermine également le contenu affiché à l'utilisateur final dans Outlook. Si vous ne sélectionnez pas d'attribut, un attribut est automatiquement sélectionné de façon aléatoire.</td>
        </tr>
        </tbody>
        </table>
    
      - Pour ajouter une zone de groupe, faites glisser l'objet dans le volet de conception. Ensuite, dans le volet des propriétés, saisissez un nom dans la zone **Texte**. Utilisez des zones de groupe pour regrouper les objets similaires.
    
      - Pour ajouter un onglet au modèle, cliquez avec le bouton droit de la souris sur un onglet existant, puis cliquez sur **Ajouter un onglet**. Un onglet vide s'affiche. Pour nommer l'onglet, saisissez son nom dans la zone **Texte** du volet des propriétés.
    
      - Pour supprimer un onglet du modèle, cliquez avec le bouton droit de la souris sur l'onglet, puis cliquez sur **Supprimer l'onglet**. Un message d'avertissement s'affiche. Cliquez sur **OK** pour confirmer la suppression de l'onglet.
    
      - Pour modifier l'ordre des objets dans un onglet afin que les utilisateurs utilisent la touche TAB pour parcourir les objets dans l'ordre que vous définissez, sélectionnez l'objet dans le volet de conception. Ensuite, dans le volet des propriétés, utilisez la zone **TabIndex** pour modifier l'ordre.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Pour vous assurer que les utilisateurs ne pourront pas utiliser la touche TAB pour accéder aux étiquettes d'un objet (par exemple, <strong>Nom</strong> ou <strong>Alias</strong>), modifiez l'ordre des étiquettes afin qu'elles figurent en dernière position dans l'ordre des tabulations.</td>
        </tr>
        </tbody>
        </table>


5.  Pour enregistrer les modifications apportées au modèle de détails, dans le menu **Fichier**, cliquez sur **Enregistrer**.

6.  Pour fermer le modèle, dans le menu **Fichier**, cliquez sur **Quitter**.

