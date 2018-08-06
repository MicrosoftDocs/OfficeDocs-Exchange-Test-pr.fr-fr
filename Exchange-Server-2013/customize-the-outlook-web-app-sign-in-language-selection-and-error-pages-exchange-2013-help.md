---
title: 'Personnaliser pages de connexion, de sélection de langue et d’erreur pr OWA | Microsoft Docs'
TOCTitle: Personnaliser les pages de connexion, de sélection de la langue et d’erreur pour Outlook Web App
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652778
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personnaliser les pages de connexion, de sélection de la langue et d’erreur pour Outlook Web App

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Cette rubrique explique comment personnaliser la couleur et les images des pages de connexion, de sélection de la langue et d'erreur pour Outlook Web App.

Signe dans Outlook Web App, sélection de la langue, les pages d’erreur sont créés en fonction des fichiers graphiques et .css dans le dossier de ressources de thèmes. Outlook Web App n'utilise qu’un seul ensemble de connexion, sélection de la langue et les pages d’erreur pour tous les thèmes. Les modifications apportées à ces pages seront afficheront par tous les utilisateurs. Vous pouvez trouver le dossier de ressources de thème dans le répertoire d’installation de Exchange à V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources. Vous aurez besoin d’un éditeur de texte pour modifier les couleurs par défaut et un éditeur graphique pour modifier les images. Si vous devez faire correspondre une couleur spécifique, et vous ne trouvez pas de correspondance pour elle à la [Table des couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679), vous pouvez utiliser une outil d’édition d’image pour échantillonner une couleur et déterminer sa valeur RVB de HTML.

Si vous disposez de plusieurs serveurs prenant en charge Outlook Web App et si vous souhaitez que tous utilisent les mêmes pages de connexion, de langue et d'erreur, vous devez copier les fichiers modifiés sur chaque serveur. Vous devez également créer une copie de sauvegarde de vos fichiers personnalisés. Si vous réinstallez ou mettez à niveau Exchange, tous les fichiers des dossiers de thèmes seront remplacés. Vous devrez recopier vos fichiers personnalisés dans le dossier approprié une fois la réinstallation ou la mise à niveau terminée

> [!NOTE]
> Avant de créer vos pages de connexion et de déconnexion personnalisées, conservez une copie des fichiers à modifier


Pour obtenir des informations sur la création d'un thème personnalisé, consultez la rubrique [Création d’un thème pour Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 45 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Éditeur graphique » sous « Autorisations Outlook Web App » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Personnaliser la couleur de la page de connexion

1.  Connectez-vous au serveur Exchange et utilisez l'Explorateur Windows pour accéder au répertoire d'installation du serveur Exchange et rechercher \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Utilisez le Bloc-notes ou un autre éditeur de texte pour ouvrir le fichier logon.css.

3.  Recherchez la valeur \#0072 par défaut de la couleur, c 6 et remplacez-le par la valeur HTML RVB de la couleur que vous souhaitez utiliser. Vous pouvez trouver HTML RVB valeurs ici : [Table de couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Enregistrez et fermez le fichier.

## Personnaliser la couleur de la page d'erreur

1.  Connectez-vous au serveur Exchange et utilisez l'Explorateur Windows pour accéder au répertoire d'installation du serveur Exchange et rechercher \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Utilisez le Bloc-notes ou un autre éditeur de texte pour ouvrir le fichier errorFE.css.

3.  Recherchez la valeur \#0072 par défaut de la couleur, c 6 et remplacez-le par la valeur HTML RVB de la couleur que vous souhaitez utiliser. Vous pouvez trouver HTML RVB valeurs ici : [Table de couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Enregistrez et fermez le fichier.

## Personnaliser la couleur de la page de sélection de la langue

1.  Connectez-vous au serveur Exchange et utilisez l'Explorateur Windows pour accéder au répertoire d'installation du serveur Exchange et rechercher \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles.

2.  Utilisez un éditeur de texte, tel que le bloc-notes, pour ouvrir le fichier LanguageSelection.css.

3.  Recherchez la valeur \#0072 par défaut de la couleur, c 6 et remplacez-le par la valeur HTML RVB de la couleur que vous souhaitez utiliser. Vous pouvez trouver HTML RVB valeurs ici : [Table de couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Enregistrez et fermez le fichier.

## Personnaliser les images des pages d'erreur et de connexion

Utilisez un outil d'édition d'images pour ouvrir et modifier les images utilisées pour créer les pages d'erreur et de connexion.

1.  Connectez-vous au serveur Exchange et utilisez l'Explorateur Windows pour accéder au répertoire d'installation du serveur Exchange et rechercher \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<version\>\\themes\\resources.

2.  Utilisez un éditeur graphique pour ouvrir et modifier les fichiers suivants :
    
      - owa\_text\_blue.png, pour modifier le logo de texte « Outlook Web App » ;
    
      - olk\_logo\_white.png, pour modifier le logo de l'application dans la barre latérale gauche ;
    
      - olk\_logo\_white\_cropped.png, pour modifier l'image située dans le volet gauche de la page d'erreur ;
    
      - sign\_in\_arrow.png, pour modifier l'icône gauche du bouton « Connexion » ;
    
      - olk\_exchange\_text\_blue.png, pour modifier le logo « Outlook Mobile » de la disposition tnarrow ;
    
      - olk\_logo\_white\_small.png est utilisé en disposition tnarrow ;
    
      - olk\_exchange\_text\_stacked\_white\_small.png est utilisé en disposition tnarrow.

3.  Recherchez la valeur \#0072 par défaut de la couleur, c 6 et remplacez-le par la valeur HTML RVB de la couleur que vous souhaitez utiliser. Vous pouvez trouver HTML RVB valeurs ici : [Table de couleurs](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Enregistrez et fermez le fichier.

## Comment savoir si cela a fonctionné ?

Ouvrez la page de connexion d'Outlook Web App dans Internet Explorer. Si vous testez les modifications apportées au site web par défaut sur le serveur hébergeant le répertoire virtuel Outlook Web App, ouvrez Internet Explorer et entrez l'URL https://localhost/owa.

Si vous ne voyez pas vos modifications, procédez comme suit :

1.  Dans la barre d'outils, sélectionnez **Paramètres** \> **Options Internet** \> **Général**.

2.  Sous **Historique de navigation**, sélectionnez **Supprimer**.

3.  Sélectionnez **Fichiers Internet temporaires et fichiers de site web**, puis **Supprimer**.

4.  Une fois la suppression terminée, sélectionnez **OK** pour fermer les **Options Internet**.

5.  Actualisez la fenêtre du navigateur.

> [!TIP]
> Pour voir les effets de vos modifications, vous pouvez garder ouvert le fichier .css que vous modifiez et actualiser la fenêtre du navigateur après avoir enregistré chaque modification.

