---
title: 'Création d’un thème pour Outlook Web App: Exchange 2013 Help'
TOCTitle: Création d’un thème pour Outlook Web App
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652762
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’un thème pour Outlook Web App

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Un *thème* définit la couleur d’arrière-plan, les polices, les couleurs de surbrillance, les icônes et l’en-tête utilisés par MicrosoftOutlook Web App. Chaque thème est un ensemble de fichiers multimédia et de feuilles de style en cascade (fichiers .css) stockés sur le serveur MicrosoftExchange dans le répertoire d’installation dans \\Client Access\\OWA\\prem\\*version*\\resources\\themes. Chaque thème est stocké dans son propre sous-répertoire \\themes.

Le thème par défaut figure dans \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base. Chaque dossier de thème contient tous les fichiers nécessaires pour définir un thème. Il s’agit des fichiers .css, des graphiques et du fichier .xml qui définit le nom du thème. Pour créer des thèmes supplémentaires, copiez tous les fichiers d’un thème dans un nouveau dossier, puis modifiez-les à votre guise.

Par défaut, lorsque vous installez Exchange Server 2013, plusieurs thèmes sont installés comme suit :

  - Les fichiers CSS (.css) définissent les couleurs, les dégradés et les polices.

  - Les fichiers d'image (.png) fournissent les icônes et autres éléments graphiques. Si vous éditez des icônes, ne modifiez pas leur taille. Si vous modifiez la taille d'un élément graphique, testez vos changements pour vérifier que les éléments s'assemblent toujours correctement.

Ces fichiers sont stockés sur le serveur d’accès au client, dans le répertoire d’installation \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes. Chaque thème est stocké dans un sous-répertoire de thèmes. Vous pouvez créer des thèmes supplémentaires en copiant un thème existant et en modifiant la copie.

Après avoir créé un thème, vous pouvez également [Personnaliser les pages de connexion, de sélection de la langue et d’erreur pour Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La version allégée d'Outlook Web App ne prend pas en charge les thèmes.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous avez plusieurs serveurs prenant en charge Outlook Web App, vous devez copier votre thème personnalisé sur chaque serveur. Vous devez également créer une copie de sauvegarde de votre thème personnalisé. Si vous réinstallez ou mettez à niveau Exchange, tous les fichiers des dossiers de thèmes sont remplacés. Une fois la réinstallation ou la mise à niveau terminée, vous devez recopier votre thème dans le dossier approprié.<br />
Avant de commencer à créer votre thème personnalisé, créez des copies de sauvegarde de tous les fichiers que vous allez modifier.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 60 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Répertoires virtuels Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour exécuter ces procédures, vous devez disposer d'un accès administrateur de serveur local.

  - Vous aurez besoin d’un éditeur de texte pour modifier les couleurs par défaut et un éditeur graphique pour modifier les images. Si vous devez faire correspondre une couleur spécifique, et vous ne trouvez pas de correspondance pour elle à la [Table des couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679), vous pouvez utiliser une outil d’édition d’image pour échantillonner une couleur et déterminer sa valeur RVB de HTML.

  - Lorsque vous modifiez ou créez un thème Outlook Web App, nous vous recommandons de suivre les indications suivantes :
    
      - Si vous décidez de modifier un thème, faites préalablement des copies de sauvegarde des fichiers d'origine.
    
      - Ne supprimez pas le dossier \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base ou les fichiers qu’il contient.

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


## Comment procéder ?

## Étape 1 : Création d'un thème Outlook Web App

Pour commencer, vous allez créez un dossier pour un nouveau thème, puis copier les fichiers d'un thème existant dans ce nouveau dossier.

1.  Connectez-vous au serveur Exchange hébergeant le répertoire virtuel Outlook Web App à l'aide d'un compte auquel a été déléguée l'appartenance au groupe Administrateurs local.

2.  Ouvrez Windows Explorer, puis recherchez le répertoire d'installation du serveur Exchange.

3.  Dans \\Client Access\\OWA\\prem\\*version*\\resources\\themes, créez un dossier, puis nommez-le (par exemple Fourth Coffee).

4.  Copiez tous les fichiers d'un autre thème dans le nouveau dossier.

## Étape 2 : Dénomination du nouveau thème

Pour définir le nom complet du nouveau thème, procédez comme suit :

1.  Ouvrez la copie de themeinfo.xml figurant dans le dossier de thème personnalisé que vous venez de créer.

2.  Recherchez la valeur `displayname` du thème, puis remplacez-la par le nom que vous voulez utiliser. Par exemple, `displayname = "Fourth Coffee Theme"`.

3.  Enregistrez et fermez le fichier theminfo.xml.

## Étape 3 : Modification de l'ordre de tri du nouveau thème (facultatif)

Si vous le souhaitez, vous pouvez modifier l'ordre de tri du nouveau thème en éditant le fichier themeinfo.xml. L'ordre de tri détermine la position du thème dans le volet **Modifier le thème** du menu Paramètres.

Pour modifier l'ordre de tri du nouveau thème à l'aide du fichier themeinfo.xml file, procédez comme suit :

1.  Ouvrez la copie de themeinfo.xml figurant dans le dossier du thème personnalisé.

2.  Recherchez la valeur `sortorder` du thème, puis modifiez-la pour indiquer la position souhaitée du nouveau thème dans la liste. Les thèmes sont triés dans l'ordre croissant de leur valeur numérique. Par défaut, le thème de base est le premier dans la liste, et sa valeur `sortorder` est « 0 ». Par exemple, `sortorder="<number>"`.

3.  Enregistrez et fermez le fichier theminfo.xml.

## Étape 4 : Modification du nouveau thème

À présent que vous avez recopié les fichiers et nommé votre thème, vous pouvez le personnaliser. Dans un thème Outlook Web App, vous pouvez personnaliser les éléments suivants :

  - Les fichiers Image qui définissent la zone d'en-tête et les icônes.

  - Les fichiers CSS qui définissent les polices et les couleurs.

## Fichiers image

Ces images sont enregistrées dans deux dossiers dans \\themes*\\\<nom du thème\>*\\images\\. Le dossier \\images\\0 contient les images utilisées pour les langues qui se lisent de gauche à droite (comme le français), et le dossier \\images\\rtl les images utilisées pour les langues qui se lisent de droite à gauche.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Certaines des images du dossier \images\rtl sont identiques à celles du dossier \images\0, mais en miroir.</td>
</tr>
</tbody>
</table>


Pour personnaliser le thème, vous pouvez utiliser un outil d'édition d'image afin d'ouvrir et de modifier les images suivantes :

  - Headerbgmain.png
    
      - Il s'agit de l'image de l'en-tête principal. Nous vous recommandons d'utiliser une image dont la hauteur ne dépasse pas celle de l'en-tête, à savoir 30 pixels. Le thème par défaut n'utilisant pas d'image d'arrière-plan, cette image est transparente. Pour un exemple de thème utilisant une image d'arrière-plan personnalisée, consultez l'image figurant dans le dossier de thème **Blueprint**.

  - Headerbgright.png
    
      - Il s'agit de l'image utilisée en mosaïque derrière l'en-tête. Le thème par défaut n'utilisant pas d'image d'arrière-plan en mosaïque, cette image est transparente. Pour un exemple de thème utilisant une image d'arrière-plan en mosaïque personnalisée, consultez l'image figurant dans le dossier de thème **Blueprint**.

  - sprite1.mouse.png
    
      - Ici figurent la plupart des images utilisées dans un thème. Vous pouvez modifier la couleur des images en fonction de votre thème, ainsi que le logo textuel Outlook Web App par défaut.
    
      - Pour éviter tout problème, ne modifiez pas la taille des icônes dans le sprite, et veillez à ce qu'il soit enregistré comme fichier .png transparent.

  - themepreview.png
    
      - Cette image est utilisée pour représenter le thème dans le volet **Modifier le thème** du menu Paramètres dans Outlook Web App.

## Couleurs et polices

Les fichiers de feuille de style en cascade (.css) définissant les couleurs et polices utilisées dans un thème sont stockés dans plusieurs dossiers sous \\themes\\*\<nom du thème\>*. Le dossier \\*\<nom du thème\>*\\0 contient les fichiers .css utilisés pour les langues qui se lisent de gauche à droite (comme le français), et le dossier \\*\<nom du thème\>*\\rtl les fichiers .css utilisés pour les langues qui se lisent de droite à gauche. Il existe également des dossiers spécifiques aux langues, (par exemple, \\ja, \\ko, \\zhs et \\zht) contenant des fichiers .css à utiliser avec ces dernières.

Commencez par modifier le dossier \\*\<theme name\>*\\images\\0. Chaque thème utilise quatre couleurs que vous pouvez personnaliser.

  - BrandColor: \#0072C6

  - NavBarHoverColor: \#4C9CD7

  - UnreadColor: \#2A8DD4

  - FocusColor: \#DFEDFA

Vous pouvez utiliser un éditeur de texte tel que Bloc-notes pour rechercher toutes les instances de ces valeurs et les remplacer par les couleurs de votre thème dans les deux fichiers suivants : owa2styles.mouseCSS et owa2styles2.mouseCSS. Vous devez effectuer cette opération dans chaque dossier de votre nouveau thème contenant ces fichiers .css.

## Étape 5 : Définition du thème Outlook Web App par défaut

La définition d’un nouveau thème par défaut affecte uniquement les utilisateurs qui n’ont pas modifié leur thème via le menu Paramètres dans Outlook Web App.

Pour forcer tous les utilisateurs à utiliser le thème par défaut, outre la configuration de ce dernier, vous devez désactiver la sélection de thème.

## Utilisation de l'environnement de ligne de commande pour définir le thème par défaut pour Outlook Web App

Cet exemple montre comment définir le thème par défaut pour Outlook Web App, où le nom de serveur est `fourthcoffee`, le nom de répertoire virtuel `owa`, le nom de site web `default web site`, et où le thème figure dans le dossier nommé `Custom`.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)).

## Utilisation de l'environnement de ligne de commande pour désactiver la sélection de thème pour Outlook Web App

Cet exemple montre comment désactiver la sélection de thème dans Outlook Web App, où le nom de serveur est `fourthcoffee`, le nom de répertoire virtuel `owa`, et le nom de site web `default web site`.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

Vous pouvez exécuter les deux commandes simultanément comme l'illustre l'exemple suivant :

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Set-OwaVirtualDirectory](https://technet.microsoft.com/fr-fr/library/bb123515\(v=exchg.150\)).

## Étape 6 : Exécution de iisreset/noforce pour enregistrer vos modifications

Si vous ajoutez ou modifiez un thème, modifiez son nom ou son ordre de tri, vous devez arrêter puis redémarrer les services IIS pour que les modifications prennent effet. Pour ce faire, ouvrez une fenêtre d'invite de commandes sur le serveur où vous avez créé votre nouveau thème, puis exécutez la commande **iisresest /nforce**.

## Comment savoir si cette tâche a fonctionné ?

1.  Connectez-vous à Outlook Web App en utilisant le répertoire virtuel sur le serveur où vous avez créé votre nouveau thème. Si vous testez les modifications apportées au site web par défaut sur le serveur Exchange hébergeant le répertoire virtuel Outlook Web App, vous pouvez tester votre thème en ouvrant Internet Explorer, puis en entrant l'URL https://localhost/owa.

2.  Accédez à votre thème personnalisé en sélectionnant le menu Paramètres \> **Modifier le thème**, puis en sélectionnant le thème.

## Non-affichage des dernières modifications après exécution de la commande iisreset/noforce

1.  Dans la barre d'outils Internet Explorer, sélectionnez le menu Paramètres \> **Options Internet**.

2.  Sous l'onglet **Général**, sous **Historique de navigation**, cliquez sur **Supprimer**, puis vérifiez si l'option **Fichiers Internet et fichiers de site Web temporaires** est activée. Cliquez ensuite sur **Supprimer** pour supprimer ces fichiers.

3.  Cliquez sur **OK** pour fermer la fenêtre **Options Internet**.

4.  Cliquez sur **Actualiser** pour afficher vos modifications.

Il se peut que vous deviez répéter ces étapes pour afficher vos modifications chaque fois que vous en apportez aux fichiers de thème. Si vous apportez plusieurs modifications, vous pouvez laisser Outlook Web App ouvert et répéter l'exécution de la commande **iisreset/noforce** sur le serveur ainsi que l'effacement des fichiers temporaires d'Internet Explorer si nécessaire.

