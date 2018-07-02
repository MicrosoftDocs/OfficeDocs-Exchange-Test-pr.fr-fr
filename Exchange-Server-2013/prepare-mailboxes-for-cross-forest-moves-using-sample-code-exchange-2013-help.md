---
title: 'Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code: Exchange 2013 Help'
TOCTitle: Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50479560
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Préparer les boîtes aux lettres pour les déplacements inter-forêts à l’aide d’un exemple de code

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Microsoft Exchange 2013 prend en charge les migrations et les déplacements de boîtes aux lettres à l'aide des cmdlets **New-MoveRequest** et **New-MigrationBatch**. Vous pouvez également déplacer la boîte aux lettres via le Centre d'administration Exchange (CAE). Vous pouvez déplacer une boîte aux lettres depuis une forêt Exchange source vers une forêt Exchange 2010 cible.

Pour exécuter **New-MoveRequest**, un utilisateur de messagerie doit exister dans la forêt Exchange cible et disposer d'un ensemble d'attributs Active Directory obligatoires minimum. Vous pouvez créer l'utilisateur de messagerie voulu dans la forêt Exchange cible en personnalisant votre déploiement de Microsoft Identity Lifecycle Manager (ILM) 2007. L'exemple de code d'extension des règles ILM décrit dans cette rubrique illustre la personnalisation de votre déploiement ILM actuel pour créer les utilisateurs de messagerie voulus dans la forêt Exchange 2013 cible.

Pour plus d'informations sur la préparation de déplacements inter-forêts, y compris les descriptions des attributs Active Directory obligatoires, consultez la rubrique [Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Téléchargez l'exemple de code dans la page [Préparer un déplacement de boîtes aux lettres en ligne](https://go.microsoft.com/fwlink/p/?linkid=177882) dans le Centre de téléchargement Microsoft.

  - Pour exécuter l'exemple de code, ILM 2007 Feature Pack 1 Service Pack 1 (SP1) est requis. Pour télécharger le Feature Pack, consultez l'article de la Base de connaissances Microsoft 977791, [Service Pack 1 (build 3.3.1139.2) est disponible pour Identity Lifecycle Manager 2007 Feature Pack 1](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=977791).

  - Vous devez également disposer des éléments suivants :
    
      - Une forêt source exécutant Exchange 2013 à l’endroit où la boîte aux lettres réside actuellement.
    
      - Une forêt cible dans laquelle Exchange 2013 est installé, à l'endroit où la boîte aux lettres sera déplacée.

  - Pour vous connecter à la forêt Exchange 2013 cible, vous devez disposer de l'autorisation pour appeler la cmdlet **UpdateRecipient**. Pour afficher les autorisations nécessaires, consultez la section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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


## Comment procéder ?

## Étape 1 : Installer l'exemple de code ILM

1.  Dans Microsoft Visual Studio 2008, ouvrez Microsoft.Exchange.Sample.OneWayGALSync.sln pour afficher l'exemple de code. Cet exemple comprend les éléments suivants :
    
      - Microsoft.MetadirectoryServicesEx.dll est le fichier binaire expédié avec ILM 2007 FP1 SP1 sous « \\Program Files\\Microsoft Identity Integration Server\\Bin\\Assemblies ». Il est référencé par l'exemple de code.
    
      - OneWaySync.xml est référencé par l'exemple de code.
    
      - Le dossier ILMServerConfig contient les fichier de configuration ILM pour l'agent de gestion source, l'agent de gestion cible et l'objet Metaverse ILM.
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll et Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (générés à partir de l’exemple de code) sont sous « \\obj\\Debug »

2.  Sur le serveur ILM, copiez les fichiers suivants sur \\Program Files\\Microsoft Identity Integration Server\\Extensions :
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  Modifiez le fichier OneWaySync.xml copié dans le dossier d'extensions ILM à l'étape 1 pour spécifier le nom unique (DN) du conteneur de l'unité d'organisation cible dans la forêt Exchange cible dans laquelle vous souhaitez créer les utilisateurs de messagerie. Vous pouvez utiliser LDP.exe ou ADSIEdit.exe pour rechercher le conteneur de l’unité d’organisation cible si vous ne connaissez pas son nom.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous utilisez cet exemple avec ILM GalSync 2007, pensez à exclure ce conteneur de la liste des conteneurs gérés par GalSync 2007.</td>
    </tr>
    </tbody>
    </table>


4.  Sur la console Gestionnaire d'identités ILM, allez sur **Fichier**\>**Importer la configuration du serveur** pour importer la configuration du serveur ILM du dossier ILMServerConfig. Cette action va importer deux agents de gestion Active Directory ainsi que le schéma Metaverse et la règle d'approvisionnement.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pendant l'importation, vous devez fournir le nom de la forêt et les informations d'identification, et mettre en correspondance les partitions de l'agent ADMA importé (agent de gestion Active Directory) avec le nom de la partition dans votre configuration pour les agents ADMA source et cible.</td>
    </tr>
    </tbody>
    </table>


5.  Pour que l’agent ADMA prenne en charge la forêt cible Exchange 2013, sur la page **Création de l’agent de gestion**, dans le volet **Configurer les extensions**, sélectionnez **Exchange 2013** dans la liste déroulante **Configurer pour** et entrez l’URI Windows PowerShell distant d’un serveur d’accès au client Exchange 2010 dans l’**URI Exchange 2013 RPS**.
    
    **Page Création de l'agent de gestion**
    
    ![Approvisionnement de l’Agent de gestion d’Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Approvisionnement de l’Agent de gestion d’Exchange 2010")  

6.  Sur la console Gestionnaire d'identités ILM sur le volet **Création de l'agent de gestion**, ouvrez les **Propriétés** pour l'Agent de gestion de la forêt source. Sélectionnez l'Assistant **Configuration des partitions d'annuaire**, puis cliquez sur **Conteneurs** pour sélectionner le conteneur qui contiendra les boîtes aux lettres que vous déplacerez sur la forêt cible. Effacez les sélections de tous les autres conteneurs, autrement dit, faites en sorte que l'agent de gestion porte uniquement sur la gestion d'un seul conteneur. De même, pour l'Agent de gestion de la forêt cible, sélectionnez le conteneur sur lequel seront configurés les utilisateurs à extension messagerie, à savoir l'unité d'organisation cible spécifiée à l'étape 2.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si vous utilisez cet exemple avec ILM GalSync 2007, pensez à exclure ces deux conteneurs de la liste des conteneurs gérés par GalSync 2007.</td>
    </tr>
    </tbody>
    </table>


7.  Exécutez une importation complète (test uniquement) sur les Agents de gestion cibles afin qu'ILM puisse détecter l'organisation cible spécifiée à l'étape 2.

## Étape 2 : Créer un utilisateur de messagerie dans la forêt Exchange cible

Maintenant que vous avez installé l'exemple de code, utilisez la procédure suivante pour créer l'utilisateur de messagerie nécessaire dans la forêt Exchange cible afin que la cmdlet **New-MoveRequest** puisse être exécutée pour effectuer un déplacement de boîte aux lettres en ligne.

1.  Dans la forêt source, utilisez le Centre d'administration Exchange pour créer des utilisateurs de boîtes aux lettres dans le conteneur sélectionné à l'étape 4 de la section « Installer l'exemple de code ILM ». Vous pouvez également utiliser les Utilisateurs et ordinateurs Active Directory pour déplacer des utilisateurs de messagerie existants dans le conteneur.

2.  Exécutez une importation delta et une synchronisation delta sur l'Agent de gestion source pour détecter les boîtes aux lettres ajoutées au conteneur source et configurer les utilisateurs de boîte aux lettres sur l'Agent de gestion cible.

3.  Exécutez une exportation sur l'Agent de gestion cible pour exporter les utilisateurs de boîte aux lettres configurés à l'étape 1 sur l'Active Directory cible.

4.  Exécutez une importation delta sur l'Agent de gestion cible pour confirmer les modifications exportées à l'étape 2.

5.  Dans la forêt cible, ouvrez l'environnement de ligne de commande Exchange Management Shell et utilisez la cmdlet **New-MoveRequest** pour déplacer les boîtes aux lettres à partir de la forêt source.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez terminé avec succès le migration, procédez comme suit :

  - Dans la forêt cible, vérifiez la présence des utilisateurs déplacés à partir de la forêt source.

