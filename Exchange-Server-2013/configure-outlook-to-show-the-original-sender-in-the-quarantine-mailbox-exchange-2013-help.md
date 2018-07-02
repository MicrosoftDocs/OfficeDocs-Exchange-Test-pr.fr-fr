---
title: 'Configurer Outlook pour afficher l’expéditeur d’origine dans la boîte aux lettres de mise en quarantaine: Exchange 2013 Help'
TOCTitle: Configurer Outlook pour afficher l’expéditeur d’origine dans la boîte aux lettres de mise en quarantaine
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50478696
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer Outlook pour afficher l’expéditeur d’origine dans la boîte aux lettres de mise en quarantaine

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

La mise en quarantaine du courrier indésirable est une fonctionnalité de l’agent de filtrage du contenu qui réduit le risque de perte de messages légitimes. La mise en quarantaine du courrier indésirable fournit un emplacement de stockage temporaire pour les messages identifiés comme courrier indésirable, qui ne doivent pas être remis à une boîte aux lettres d’utilisateur au sein de l’organisation.

Lorsqu’un message atteint le seuil de quarantaine du courrier indésirable, il est consigné dans une notification d’échec de remise et déposé dans la boîte aux lettres de mise en quarantaine du courrier indésirable. Les messages mis en quarantaine étant stockés sous forme de notifications d’échec de remise dans la boîte aux lettres de mise en quarantaine, l’adresse d’administrateur de votre organisation s’affiche comme l’adresse De: pour tous les messages. Toutefois, avec l’adresse de l’expéditeur initial, l’adresse du destinataire initial et le seuil de probabilité de courrier indésirable (SCL) initial figurant dans la liste des champs, il devient plus facile de localiser le message que vous souhaitez récupérer.

Par défaut, vous ne pouvez pas sélectionner ces champs dans Microsoft Outlook. Avant de pouvoir ajouter des champs dans la vue du message, vous devez commencer par créer un formulaire Outlook qui ajoute l’expéditeur initial, le destinataire initial et le seuil de probabilité de courrier indésirable (SCL) initial comme champs facultatifs que vous pouvez sélectionner. Après avoir créé ce formulaire personnalisé, vous pouvez configurer Outlook pour afficher ces champs dans la vue du message.

## Ce qu’il faut savoir avant de commencer ?

  - Durée estimée de la procédure : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Accès à la boîte aux lettres » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Cette procédure nécessite d’avoir configuré la boîte aux lettres de mise en quarantaine antispam. Pour plus d’informations, consultez la rubrique [Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Pour accéder à la boîte aux lettres de mise en quarantaine, vous devez lui configurer un profil Outlook, puis l’ouvrir dans Outlook. Pour plus d’informations sur la configuration et l’utilisation de plusieurs profils Outlook, consultez l’article [Créer un profil Outlook](https://go.microsoft.com/fwlink/p/?linkid=178975).

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

## Étape 1 : Utilisez le bloc-notes pour créer un formulaire Outlook personnalisé

1.  Ouvrez le bloc-notes et copiez le code suivant dans le document.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  Enregistrez le fichier dans votre dossier Office Forms en utilisant les valeurs suivantes :
    
      - **Chemin d’accès**   *\<Chemin d’installation Office\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Chemin d’installation Office\>*   Pour des versions 32 bits de Microsoft Office sur des versions 32 bits de Microsoft Windows ou des versions 64 bits Microsoft Office sur des versions 64 bits de Microsoft Windows, le chemin d’accès par défaut est `C:\Program Files\Microsoft Office`. Pour des versions 32 bits de Microsoft Office sur des versions 64 bits de Microsoft Windows, le chemin d’accès par défaut est `C:\Program Files (x86)\Microsoft Office`.
        
          - *\<OfficeVersion\>*   Pour Outlook 2007, la valeur est `Office12`. Pour Outlook 2010, la valeur par défaut est généralement `Office14`. Pour Outlook 2013, la valeur est `Office15`.
        
          - *\<LCID\>*   Il s’agit de la valeur de votre identificateur de paramètre régional (LCID). Par exemple, le LCID pour l’anglais américain est 1033. Pour plus d’informations, consultez l’article [KB221435 : Liste des identificateurs de paramètres régionaux pris en charge dans Word](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=221435).
    
      - **Nom**   Pour le reste de cette procédure, supposons que le fichier se nomme `QTNE.cfg`. Le nom du fichier n’est pas important, mais veillez à mettre la valeur entre guillemets (") pour que le fichier soit enregistré de la forme QTNE.cfg et non QTNE.cfg.txt.
    
    Par exemple, pour une version 32 bits en anglais américain de Outlook 2013 installée sur une version 64 bits de Windows, enregistrez le fichier comme suit :
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si Windows User Access Control (UAC) vous empêche d'enregistrer le fichier à l'emplacement correct, enregistrez-le tout d'abord dans un emplacement temporaire, et copiez-le.</td>
    </tr>
    </tbody>
    </table>


## Étape 2 : Configurez Outlook pour utiliser le formulaire Outlook personnalisé

Utilisez l’une des procédures suivantes selon la version de Microsoft Outlook installée sur votre ordinateur.

## Configurer Outlook 2010 ou Outlook 2013

1.  Dans Outlook 2010 ou Outlook 2013, cliquez sur **Fichier** \> **Options** \> **Avancé**.

2.  Dans la section **Développeurs**, cliquez sur **Formulaires personnalisés**.

3.  Dans la boîte de dialogue **Options**, cliquez sur **Gérer les formulaires**.

4.  Dans la boîte de dialogue **Gestionnaire de formulaires**, cliquez sur **Installer**. Naviguez jusqu'à l'emplacement du fichier `QTNE.cfg`, sélectionnez-le, puis cliquez sur **Ouvrir**. Dans la boîte de dialogue **Propriétés du formulaire**, vérifiez les informations, puis cliquez sur **OK** pour installer le Formulaire d'extension de quarantaine dans votre bibliothèque de formulaires personnels.

5.  Dans la boîte de dialogue **Gestionnaire de formulaires**, cliquez sur **Fermer**. Cliquez sur **OK** deux fois pour fermer les boîtes de dialogue restantes et retourner sur l’interface Outlook principale.

6.  Sur l’onglet **Accueil** dans la vue **Courrier** de la boîte de réception, cliquez avec le bouton droit sur la ligne des en-têtes des colonnes (vous devez peut-être augmenter la largeur de la liste des messages pour voir les colonnes), puis sélectionnez **Paramètres d’affichage**.

7.  Dans la boîte de dialogue **Paramètres d’affichage avancés**, cliquez sur **Colonnes**.

8.  Dans la boîte de dialogue **Afficher les colonnes**, dans la liste déroulante **Sélectionner les colonnes disponibles dans**, accédez à la fin de la liste et sélectionnez **Formulaires**.

9.  Dans la boîte de dialogue **Sélectionner les formulaires d’entreprise pour ce dossier**, dans le champ **Formulaires sélectionnés**, sélectionnez **Message**, puis cliquez sur **Supprimer**. Dans le champ **Formulaires personnels**, sélectionnez **Formulaire d’extension de mise en quarantaine**, puis cliquez sur **Ajouter**. Lorsque vous avez terminé, cliquez sur **Fermer**.

10. Dans la boîte de dialogue **Afficher les colonnes**, dans la section **Colonnes disponibles**, sélectionnez un ou plusieurs champs parmi les suivants et cliquez sur **Ajouter** pour chaque champ sélectionné.
    
      - **ReceivedRepresentingEmailAddress**   Expéditeur d’origine
    
      - **DisplayTo**   Destinataire d'origine (notez qu'il apparaît sous la forme **À** une fois que vous l'avez ajouté)
    
      - **OriginalScl**   SCL d’origine
    
    Utilisez les boutons **Monter** ou **Descendre** pour positionner les colonnes dans l’affichage. Pour obtenir des résultats optimaux, placez les trois nouveaux champs après le champ **Pièce jointe**, et avant le champ **De**. Lorsque vous avez terminé, cliquez sur **OK** deux fois pour retourner sur l’interface Outlook principale.

## Configurer Outlook 2007

1.  Dans Outlook 2007, cliquez sur **Outils** \> **Options**.

2.  Dans la boîte de dialogue **Options**, cliquez sur l’onglet **Autre**, puis sous **Général**, cliquez sur **Options avancées**.

3.  Dans la boîte de dialogue **Options avancées**, cliquez sur **Formulaires personnalisés**, puis dans la boîte de dialogue **Formulaires personnalisés**, cliquez sur **Gérer les formulaires**.

4.  Dans la boîte de dialogue **Gestionnaire de formulaires**, cliquez sur **Installer**. Naviguez jusqu'à l'emplacement du fichier `QTNE.cfg`, sélectionnez-le, puis cliquez sur **Ouvrir**. Dans la boîte de dialogue **Propriétés du formulaire**, vérifiez les informations, puis cliquez sur **OK** pour installer le Formulaire d'extension de quarantaine dans votre bibliothèque de formulaires personnels.

5.  Fermez la boîte de dialogue **Gestionnaire des formulaires**, puis cliquez trois fois sur **OK** pour fermer les autres boîtes de dialogue et revenir à l’interface Outlook 2007 principale.

6.  Dans la vue **Messagerie** de la boîte de réception, cliquez avec le bouton droit sur la ligne d'en-tête de colonne (vous devez peut-être augmenter la largeur de la liste des messages pour voir les colonnes), puis sélectionnez **Personnaliser l'affichage actuel**.

7.  Dans la boîte de dialogue **Personnalisation de l'affichage : Messages**, cliquez sur **Afficher les champs**.

8.  Dans la boîte de dialogue **Afficher les champs**, dans la liste déroulante **Sélectionner les champs disponibles dans :**, accédez à la fin de la liste et sélectionnez **Formulaires**.

9.  Dans la boîte de dialogue **Sélectionner les formulaires d’entreprise pour ce dossier**, dans le champ **Formulaires sélectionnés**, sélectionnez **Message**, puis cliquez sur **Supprimer**. Dans le champ **Formulaires personnels**, sélectionnez **Formulaire d’extension de mise en quarantaine**, puis cliquez sur **Ajouter**. Lorsque vous avez terminé, cliquez sur **Fermer**.

10. Dans la boîte de dialogue **Afficher les champs**, dans la section **Champs disponibles**, sélectionnez un ou plusieurs champs parmi les suivants et cliquez sur **Ajouter** pour chaque champ sélectionné.
    
      - **ReceivedRepresentingEmailAddress**   Expéditeur d’origine
    
      - **DisplayTo**   Destinataire d'origine (notez qu'il apparaît sous la forme **À** une fois que vous l'avez ajouté)
    
      - **OriginalScl**   SCL d’origine
    
    Utilisez les boutons **Monter** ou **Descendre** pour positionner les colonnes dans l’affichage. Pour obtenir des résultats optimaux, placez les trois nouveaux champs après le champ **Pièce jointe**, et avant le champ **De**. Lorsque vous avez terminé, cliquez sur **OK** deux fois pour retourner sur l’interface Outlook 2007 principale.

## Comment savoir si cela a fonctionné ?

Vous savez si cette procédure a fonctionné si vous pouvez voir les valeurs expéditeur initial, destinataire initial ou SCL initial pour des messages mis en quarantaine dans la boîte aux lettres de mise en quarantaine du courrier indésirable à l’aide de Microsoft Outlook.

