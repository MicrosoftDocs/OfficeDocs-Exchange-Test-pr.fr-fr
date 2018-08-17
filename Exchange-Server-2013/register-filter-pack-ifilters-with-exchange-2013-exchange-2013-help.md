---
title: 'Inscrire les IFilters Filter Pack avec Exchange 2013: Exchange 2013 Help'
TOCTitle: Inscrire les IFilters Filter Pack avec Exchange 2013
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50555338
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Inscrire les IFilters Filter Pack avec Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les règles de transport comportant des conditions d’analyse de pièces jointes effectuent une extraction de texte lors de l’analyse du contenu des pièces jointes. Exchange 2013 peut analyser la plupart des types de pièces jointes les plus couramment utilisées en mode natif. Des types de pièces jointes supplémentaires peuvent être inclus en enregistrant des iFilters dans Exchange 2013. Cette rubrique vous explique comment enregistrer des iFilters publiés par Microsoft et des éditeurs tiers.

Après avoir enregistré un IFilter pour un type de fichier spécifique, les règles de transport dotées de conditions de traitement des pièces jointes pourront analyser ces pièces jointes. Par conséquent, ces types de fichiers ne déclencheront plus la condition *AttachmentIsUnsupported*.

> [!CAUTION]
> Les procédures répertoriées dans cette rubrique impliquent la modification du Registre sur vos serveurs Exchange. Une modification incorrecte du Registre peut être à l’origine de problèmes graves qui vous obligeront peut-être à réinstaller votre système d’exploitation. Il se peut que les problèmes résultant d’une modification incorrecte du Registre soient impossibles à résoudre. Avant de modifier le Registre, sauvegardez les données importantes.
> Ces procédures requièrent également l’interruption et le redémarrage du service de transport Microsoft Exchange sur vos serveurs de boîtes aux lettres.


Pour d’autres tâches de gestion relatives aux règles de transport, consultez la rubrique [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes par serveur.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Paramètres de configuration du serveur Exchange » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Vous devez exécuter les procédures suivantes sur les serveurs sur lesquels le rôle serveur de boîtes aux lettres Exchange 2013 est déjà installé. Si vous ajoutez d’autres serveurs de boîtes aux lettres après avoir suivi ces procédures, vous devez les réexécuter sur les nouveaux serveurs configurés.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Enregistrer le pack de filtres Microsoft Office 2010

Par défaut, les types de fichiers Office suivants ne sont pas pris en charge par les règles de transport Exchange :

  - Office OneNote

  - Office Publisher

Si vous souhaitez prendre en charge ces fichiers, vous devez déployer le pack de filtres Microsoft Office 2010. Ce pack de filtres n’est pas déployé pendant l’installation d’Exchange 2013 et n’est pas une condition préalable de déploiement.

## Déployer le pack de filtres Microsoft Office 2010

Le déploiement du pack de filtres Office 2010 s’articule en deux étapes principales :

  - Le téléchargement et l’installation du pack de filtres, qui enregistre les iFilters dans Windows (Rechercher).

  - La modification du Registre afin que les IFilters soient également homologués dans Exchange 2013. Cela permet à Exchange de prendre en charge l’analyse des pièces jointes pour les formats de fichier.

> [!IMPORTANT]
> Vous devez effectuer cette procédure sur tous les serveurs de boîtes aux lettres de votre organisation.


1.  Téléchargez et enregistrez le pack de filtres Microsoft Office 2010 (`FilterPack64bit.exe`) à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/?linkid=191548).

2.  Exécutez le fichier `FilterPack64bit.exe` sur votre serveur de boîtes aux lettres et suivez les instructions pour terminer l’installation.

3.  Démarrez l’Éditeur de Registre, puis localisez la sous-clé de Registre suivante :
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  Sous **CLSID**, ajoutez une sous-clé pour les fichiers OneNote comme suit :
    
    1.  Cliquez avec le bouton droit sur **CLSID**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur l’emplacement auquel vous avez installé le pack de filtres Office 2010. Par défaut, le pack de filtres est installé à l’emplacement suivant : `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`.
    
    4.  Cliquez avec le bouton droit sur **{B8D12492-CE0F-40AD-83EA-099A03D493F1}**, pointez sur **Suivant**, puis cliquez sur **Valeur de chaîne**.
    
    5.  Nommez la nouvelle valeur de chaîne `ThreadingModel` et définissez-la sur `Both`.

5.  Sous **CLSID**, ajoutez une sous-clé pour les fichiers Publisher comme suit :
    
    1.  Cliquez avec le bouton droit sur **CLSID**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur l’emplacement auquel vous avez installé le pack de filtres Office 2010. Par défaut, le pack de filtres est installé à l’emplacement suivant : `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`.
    
    4.  Cliquez avec le bouton droit sur **{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}**, pointez sur **Nouveau**, puis cliquez sur **Valeur de chaîne**.
    
    5.  Nommez la nouvelle valeur de chaîne `ThreadingModel` et définissez-la sur `Both`.

6.  Localisez la clé de Registre suivante :
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  Sous **Filtres**, ajoutez une sous-clé pour les extensions .one comme suit :
    
    1.  Cliquez avec le bouton droit sur **filtres**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `.one`.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.

8.  Sous **Filtres**, ajoutez une sous-clé pour les extensions .pub comme suit :
    
    1.  Cliquez avec le bouton droit sur **Filtres**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `.pub`.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.

9.  Fermez l'Éditeur du registre.

10. Sur votre serveur de boîtes aux lettres, arrêtez puis redémarrez les services suivants dans l’ordre spécifié :
    
    1.  Arrêtez le service de transport Microsoft Exchange.
    
    2.  Arrêtez le service de gestion de filtrage de Microsoft.
    
    3.  Démarrez le service de gestion de filtrage de Microsoft.
    
    4.  Démarrez le service de transport Microsoft Exchange.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien enregistré les iFilters du pack de filtres Microsoft Office 2010, effectuez l’opération suivante :

1.  Créez une règle de transport avec les propriétés suivantes : Pour des instructions détaillées sur la procédure de création de règles de transport, consultez la rubrique [Gestion de règles de flux de messagerie](manage-mail-flow-rules-exchange-2013-help.md).
    
      - L’expéditeur est votre boîte aux lettres.
    
      - Tout contenu de pièce jointe inclut « Test des iFilters ».
    
      - Générez un rapport d’incidents et envoyez-le à votre boîte aux lettres.

2.  Créez un fichier OneNote contenant la phrase « Test des iFilters », joignez-le à un nouveau message électronique, et envoyez-le à votre propre adresse de messagerie.

3.  Vérifiez que vous avez bien reçu un rapport d’incidents de règles de transport pour la règle que vous venez de créer. Cela permet de confirmer que le moteur de règles a pu analyser le contenu du fichier OneNote.

4.  Répétez les étapes 2 et 3 avec un fichier Publisher.

## Enregistrement d’iFilters tiers pour prendre en charge des formats de fichiers supplémentaires

Vous pouvez étendre la capacité d’analyse des pièces joints à d’autres types de fichiers en enregistrant des iFilters tiers supplémentaires. La prise en charge de fichiers supplémentaires peut être ajoutée en installant et en enregistrant l’iFilter du type de fichier sur chacun de vos serveurs de boîtes aux lettres.

> [!IMPORTANT]
> Microsoft n’a pas testé d’IFilters tiers avec des règles de transport. Par conséquent, il est recommandé de déployer et de tester tous les IFilters tiers dans un environnement de test avant de déployer votre environnement de production.


## Déploiement de l’iFilter Adobe PDF

Cette procédure explique comment déployer l’[IFilter Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) pour prendre en charge le traitement de pièces jointes PDF dans les règles de transport.

> [!NOTE]
> Par défaut, Exchange 2013 prend en charge l’analyse des fichiers PDF dans les règles de transport. Le fichier PDF fourni ici à titre d’exemple permet simplement d’illustrer l’extension de la prise en charge d’autres types de fichiers à l’aide d’iFilters tiers.


1.  Téléchargez l’[iFilter Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025), puis suivez les instructions d’installation.

2.  Démarrez l’Éditeur de Registre, puis localisez la sous-clé suivante :
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  Sous **CLSID**, ajoutez une sous-clé pour les fichiers PDF comme suit :
    
    1.  Cliquez avec le bouton droit sur **CLSID**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.
        
        > [!NOTE]
        > Chaque iFilter est associé à un ID de classe unique (CLSID). Vous trouverez le CLSID dans la documentation d’installation de l’iFilter que vous enregistrez ou en recherchant l’extension de fichier sous la clé <code>HKEY_CLASSES_ROOT\CLSID</code> du Registre.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur l’emplacement auquel vous avez installé l’iFilter PDF. Par défaut, l’iFilter PDF est installé à l’emplacement suivant : `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`.

4.  Localisez la clé de Registre suivante :
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  Sous **Filtres**, ajoutez une sous-clé pour les extensions .pdf comme suit :
    
    1.  Cliquez avec le bouton droit sur **Filtres**, pointez sur **Nouveau**, puis cliquez sur **Clé**.
    
    2.  Modifiez le nom de la nouvelle clé à `.pdf`.
    
    3.  Cliquez sur la clé que vous venez de créer et définissez la valeur **(Par défaut)** sur `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.

6.  Fermez l'Éditeur du registre.

7.  Sur votre serveur de boîtes aux lettres, arrêtez et redémarrez les services suivants dans l’ordre spécifié :
    
    1.  Arrêtez le service de transport Microsoft Exchange.
    
    2.  Arrêtez le service de gestion de filtrage de Microsoft.
    
    3.  Démarrez le service de gestion de filtrage de Microsoft.
    
    4.  Démarrez le service de transport Microsoft Exchange.

## Comment savoir si cela a fonctionné ?

Suivez la même procédure que celle décrite dans la section Comment savoir si cela a fonctionné ? décrite précédemment dans cette rubrique, en remplaçant les fichiers Publisher par des fichiers Adobe PDF.

## Pour plus d'informations

[Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Actions de règle de transport](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

