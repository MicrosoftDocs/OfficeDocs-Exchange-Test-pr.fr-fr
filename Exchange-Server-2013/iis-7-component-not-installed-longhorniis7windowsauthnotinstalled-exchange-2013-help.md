---
title: 'Composant IIS 7 non installé_LonghornIIS7WindowsAuthNotInstalled: Exchange 2013 Help'
TOCTitle: Composant IIS 7 non installé_LonghornIIS7WindowsAuthNotInstalled
ms:assetid: f0e75196-5d0d-4e6d-8931-e6c576f55caa
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.longhorniis7windowsauthnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50479540
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Composant IIS 7 non installé\_LonghornIIS7WindowsAuthNotInstalled

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2015-03-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2010 ou le programme d’installation de Microsoft Exchange Server 2007 ne peut pas installer le rôle serveur d’accès au Client (CAS) ou le rôle serveur de boîtes aux lettres sur un ordinateur Microsoft Windows Server 2008 ou sur un ordinateur Windows Server 2008 R2 car les composants IIS 7 requis ne sont pas installés.

Le programme d’installation d’Exchange 2010 et le programme d’installation d’Exchange 2007 exigent que les composants IIS 7 suivants soient déjà installés sur l’ordinateur Windows Server 2008 ou l’ordinateur Windows Server 2008 R2 sur lequel vous installez le rôle CAS.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Composants IIS 7 requis pour le rôle serveur CAS</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compression du contenu dynamique</p></td>
</tr>
<tr class="even">
<td><p>Compression du contenu statique</p></td>
</tr>
<tr class="odd">
<td><p>Authentification de base</p></td>
</tr>
<tr class="even">
<td><p>Authentification Windows</p></td>
</tr>
<tr class="odd">
<td><p>Authentification Digest IIS 7</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Mappage de certificat client</p></td>
</tr>
<tr class="even">
<td><p>Exploration des répertoires</p></td>
</tr>
<tr class="odd">
<td><p>Erreurs HTTP</p></td>
</tr>
<tr class="even">
<td><p>Journalisation HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Redirection HTTP</p></td>
</tr>
<tr class="even">
<td><p>Traçage</p></td>
</tr>
<tr class="odd">
<td><p>Filtres ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Observateur de demandes</p></td>
</tr>
<tr class="odd">
<td><p>Contenu statique</p></td>
</tr>
</tbody>
</table>


Le programme d’installation d’Exchange 2010 et le programme d’installation d’Exchange 2007 exigent que les composants IIS 7 suivants soient déjà installés sur l’ordinateur Windows Server 2008 ou l’ordinateur Windows Server 2008 R2 sur lequel vous installez le rôle serveur de boîte aux lettres.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Composants IIS 7 requis pour le rôle serveur de boîtes aux lettres</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authentification de base</p></td>
</tr>
<tr class="even">
<td><p>Authentification Windows</p></td>
</tr>
</tbody>
</table>


Pour résoudre ce problème, suivez les étapes appropriées pour installer les composants IIS 7 requis sur l’ordinateur de destination, puis exécutez de nouveau le programme d’installation de Microsoft Exchange.

Installez les composants IIS 7 pour le rôle serveur CAS à l’aide du Gestionnaire de serveur Windows Server 2008

1.  Cliquez sur **Démarrer**, cliquez sur **Outils d’administration**, puis cliquez sur **Gestionnaire de serveur**.

2.  Dans le volet de navigation, développez **Rôles**, cliquez avec le bouton droit de la souris sur **Serveur Web (IIS)**, puis sur **Ajouter des services de rôle**.

3.  Dans le volet **Sélectionner des services de rôle**, faites défiler jusqu’à **IIS**.

4.  Dans la zone **Sécurité**, activez les cases à cocher suivantes :
    
      - **Authentification de base**
    
      - **Authentification Digest**
    
      - **Authentification Windows**

5.  Dans la zone **Performances**, activez les cases à cocher suivantes :
    
      - **Compression statique**
    
      - **Compression dynamique**

6.  Dans le volet **Sélectionner les services de rôle**, cliquez sur **Suivant**, puis cliquez sur **Installer** dans le volet **Confirmer les sélections d’installation**.

7.  Cliquez sur **Fermer** pour quitter l’Assistant Ajouter des services de rôle.

Installer les composants IIS 7 pour le rôle serveur de boîtes aux lettres à l’aide du Gestionnaire de serveur Windows Server 2008

1.  Cliquez sur **Démarrer**, cliquez sur **Outils d’administration**, puis cliquez sur **Gestionnaire de serveur**.

2.  Dans le volet de navigation, développez **Rôles**, cliquez avec le bouton droit de la souris sur **Serveur Web (IIS)**, puis sur **Ajouter des services de rôle**.

3.  Dans le volet **Sélectionner des services de rôle**, faites défiler jusqu’à **IIS**.

4.  Dans la zone **Sécurité**, activez les cases à cocher suivantes :
    
      - **Authentification de base**
    
      - **Authentification Windows**

5.  Dans le volet **Sélectionner les services de rôle**, cliquez sur **Suivant**, puis cliquez sur **Installer** dans le volet **Confirmer les sélections d’installation**.

6.  Cliquez sur **Fermer** pour quitter l’Assistant Ajouter des services de rôle.

