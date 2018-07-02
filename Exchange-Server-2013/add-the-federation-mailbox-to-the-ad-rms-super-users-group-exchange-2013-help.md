---
title: 'Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS: Exchange 2013 Help'
TOCTitle: Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50478039
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Pour les fonctionnalités suivantes de Microsoft Exchange Server 2013 gestion des droits relatifs à l’Information (IRM) est activée, vous devez ajouter la boîte aux lettres de fédération (une boîte aux lettres système créé par Exchange 2013 le programme d’installation) pour le groupe de super utilisateurs sur un cluster des [Services AD RMS (Active Directory Rights Management Services) (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) de votre organisation :

  - IRM dans Microsoft Office Outlook Web App

  - IRM dans Exchange ActiveSync

  - Déchiffrement du rapport de journal

  - Déchiffrement du transport

Vous pouvez configurer un groupe de distribution à extension messagerie en tant que groupe de super utilisateurs dans AD RMS. Une licence d’utilisation de propriétaire est accordée aux membres du groupe de distribution lorsque ces derniers en font la demande à partir du cluster AD RMS. Cela leur permet de déchiffrer tout le contenu protégé par RMS qui a été publié par ce cluster. Que vous utilisiez un groupe de distribution existant ou que vous en créiez un et le configuriez en tant que groupe de super utilisateurs dans AD RMS, il est conseillé de le dédier à cette fin et de configurer les paramètres appropriés pour l’approbation, l’audit et le contrôle des modifications apportées à l’appartenance au groupe.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Configuration d’un groupe de super utilisateurs dans AD RMS permet de décrypter le contenu protégé par IRM, les membres de groupe. Nous vous conseillons prenez les mesures appropriées pour contrôler et surveiller l’appartenance de groupe et activez l’audit suivre les modifications d’appartenance. Vous pouvez également limiter les modifications indésirables dans l’appartenance au groupe en configurant le groupe comme un groupe restreint à l’aide de la stratégie de groupe. Pour plus d’informations, voir <a href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">Paramètres de stratégie de groupes restreints</a>.</td>
</tr>
</tbody>
</table>


Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Groupes de distribution » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Un cluster AD RMS doit être déployé dans la forêt Active Directory.

  - Si un groupe de super utilisateurs est déjà configuré sur un cluster AD RMS, toute modification apportée à l’appartenance au groupe de distribution peut prendre jusqu’à 24 heures pour être actualisée par le cluster AD RMS. C’est le résultat de la mise en cache de l’appartenance au groupe sur le cluster.

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

## Étape 1 : Utilisez l’environnement Shell pour ajouter la boîte aux lettres de fédération à un groupe de distribution

Si un groupe de distribution a été créé et configuré comme groupe de super utilisateurs dans le cluster AD RMS, vous pouvez ajouter la boîte aux lettres de fédération Exchange 2013 comme membre de ce groupe. Si aucun groupe de super utilisateurs n’est configuré, vous devez créer un groupe de distribution et ajouter la boîte aux lettres de fédération comme membre.

1.  Créez un groupe de distribution dédié à une utilisation en tant que groupe de super utilisateurs AD RMS. Pour plus d’informations, voir [Création et gestion de groupes de distribution](create-and-manage-distribution-groups-exchange-2013-help.md).

2.  Ajoutez l’utilisateur **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** au nouveau groupe de distribution. La boîte aux lettres de fédération est de type système. Par conséquent, elle n’est pas visible dans le CAE. Pour l’ajouter à un groupe de distribution, vous devez utiliser la cmdlet [Add-DistributionGroupMember](https://technet.microsoft.com/fr-fr/library/bb124340\(v=exchg.150\)) de l’environnement de ligne de commande Exchange Management Shell.
    
    Cet exemple montre comment ajouter la boîte aux lettres de fédération au groupe de distribution ADRMSSuperUsers.
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Add-DistributionGroupMember](https://technet.microsoft.com/fr-fr/library/bb124340\(v=exchg.150\)).

## Étape 2 : Utilisation d’AD RMS pour configurer un groupe de super utilisateurs

Effectuez la procédure suivante sur un cluster AD RMS. Le compte utilisé pour effectuer cette procédure doit être membre du groupe local Administrateurs d’entreprise AD RMS sur le serveur AD RMS.

1.  Ouvrez la console AD RMS (Active Directory Rights Management Services) et développez le cluster AD RMS.

2.  Dans l’arborescence de la console, développez **Stratégies de sécurité**, puis cliquez sur **Super utilisateurs**.

3.  Dans le volet Actions, cliquez sur **Activer les super utilisateurs**.

4.  Dans le volet Résultats, cliquez sur **Modifier le groupe des super utilisateurs** pour ouvrir la feuille de propriétés **Super utilisateurs**.

5.  Dans le champ **Groupe de super utilisateurs**, entrez l’adresse de messagerie du groupe de distribution que vous avez créé dans la procédure précédente ou cliquez sur **Parcourir** pour sélectionner un groupe de distribution.

## Comment savoir si cela a fonctionné ?

Après avoir ajouté la boîte aux lettres de fédération à un groupe de distribution nouveau ou existant, utilisez la cmdlet [Get-DistributionGroupMember](https://technet.microsoft.com/fr-fr/library/aa996367\(v=exchg.150\)) pour vérifier l’appartenance au groupe.

Pour un exemple sur la manière de vérifier l’appartenance au groupe de distributions, voir l’[Examples](https://technet.microsoft.com/fr-fr/aa996367\(exchg.150\)#examples) dans **Get-DistributionGroupMember**.

Après avoir utilisé AD RMS pour mettre en place un groupe de super utilisateurs, vous pouvez utiliser les méthodes suivantes pour vérifier que le groupe de super utilisateurs est configuré correctement. En outre, vous pouvez utiliser la cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979798\(v=exchg.150\)) pour vérifier la fonctionnalité IRM.

  - Utilisez la console AD RMS pour vérifier que le groupe correct a été configuré comme groupe de super utilisateurs.

  - Exécutez la commande PowerShell suivante sur un serveur AD RMS pour récupérer le groupe de super utilisateurs :
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le module ADRMSAdmin PowerShell est disponible dans Windows Server 2008 R2 et version ultérieure.</td>
    </tr>
    </tbody>
    </table>
    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser

