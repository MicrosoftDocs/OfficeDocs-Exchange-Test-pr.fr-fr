---
title: 'Entrer votre clé de produit Exchange 2013: Exchange 2013 Help'
TOCTitle: Entrer votre clé de produit Exchange 2013
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51407240
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: HT
---

# Entrer votre clé de produit Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Une clé de produit indique à Exchange Server 2013 que vous avez acheté une licence Standard Edition ou Enterprise Edition. Si la clé de produit que vous avez achetée correspond à une licence Enterprise Edition, elle vous permet de monter plus de cinq bases de données par serveur et vous fournit toutes les options disponibles avec une licence Standard Edition. Pour en savoir plus sur la gestion des licences Exchange, voir [Exchange 2013 : éditions et versions](exchange-2013-editions-and-versions-exchange-2013-help.md).

Si vous n’entrez pas de clé de produit, votre serveur est automatiquement inscrit en tant que version d’évaluation. La version d’évaluation fonctionne comme un serveur Exchange Standard Edition et s’avère utile si vous voulez essayer Exchange avant de l’acheter, ou pour exécuter des tests dans un laboratoire. La seule différence est que vous pouvez utiliser le serveur Exchange sous licence de version d’évaluation pendant 180 jours maximum. Pour continuer à utiliser le serveur au-delà de 180 jours, vous devez entrer une clé de produit. À défaut, le Centre d’administration Exchange (CAE) commencera à afficher des rappels vous indiquant que vous devez acquérir le serveur sous licence.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous avons remarqué que certains visiteurs accédant à cette page sont à la recherche d’informations sur l’installation ou l’activation d’Office. Si c’est votre cas, consultez les pages suivantes :
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403360">Installer Office</a></p></li>
<li><p><a href="http://go.microsoft.com/fwlink/p/?linkid=403361">Besoin d’aide avec votre clé de produit Office ?</a></p></li>
</ul>
Si vous voulez entrer une clé de produit sur un serveur Exchange 2010, accédez à <a href="http://go.microsoft.com/fwlink/p/?linkid=403370">Entrer une clé de produit Exchange 2010</a>.<br />
Si vous voulez entrer une clé de produit sur un serveur Exchange 2013, vous êtes au bon endroit ! Poursuivons.</td>
</tr>
</tbody>
</table>


## Ce qu'il faut savoir avant de commencer

  - Durée estimée de la procédure : moins de 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Clé de produit » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Si vous possédez une licence pour un serveur Exchange qui exécute le rôle serveur de boîtes aux lettres, vous devez redémarrer le service de banque d’informations de Microsoft Exchange sur le serveur une fois la clé de produit saisie.

  - Si vous souhaitez mettre à niveau un serveur Exchange possédant une licence Standard Edition vers une licence Enterprise Edition, suivez les étapes de cette rubrique.

  - Si vous voulez déclasser un serveur Exchange possédant une licence Enterprise Edition vers une licence Standard Edition, vous devez réinstaller Exchange.

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

## Utiliser le Centre d'administration Exchange (CAE) pour entrer la clé de produit

1.  Ouvrez le CAE en accédant à la page https://\<*Client Access server name*\>/ecp.

2.  Entrez votre nom d'utilisateur et votre mot de passe dans **Domaine\\nom d'utilisateur** et **Mot de passe**, puis cliquez sur **Se connecter**.

3.  Accédez à **Serveurs** \> **Serveurs**. Sélectionnez le serveur pour lequel vous souhaiter obtenir une licence, puis cliquez sur **Modifier** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  (Facultatif) Si vous souhaitez mettre à niveau le serveur de la licence Standard Edition à la licence Enterprise Edition, dans la page **Général**, sélectionnez **Modifier la clé de produit**. Vous ne verrez cette option que si le serveur est déjà sous licence.

5.  Dans la page **Général**, entrez votre clé de produit dans la zone de texte **Entrez une clé de produit valide**.

6.  Cliquez sur **Enregistrer**.

7.  Si vous disposez d’une licence pour un serveur Exchange exécutant le rôle serveur de boîtes aux lettres, procédez comme suit pour redémarrer le service de banque d’informations de Microsoft Exchange :
    
    1.  Ouvrez le **Panneau de configuration**, accédez à **Outils d’administration**, puis ouvrez **Services**.
    
    2.  Cliquez avec le bouton droit sur **Banque d’informations Microsoft Exchange**, puis cliquez sur **Redémarrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour saisir la clé de produit

Cet exemple utilise la cmdlet **set-ExchangeServer** pour saisir la clé de produit.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous pouvez réexécuter cette commande sur le même serveur pour le mettre à niveau de la licence Standard Edition à la licence Enterprise Edition.</td>
</tr>
</tbody>
</table>


    Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-ExchangeServer](https://technet.microsoft.com/fr-fr/library/bb123716\(v=exchg.150\)).

Si vous disposez d’une licence pour un serveur Exchange exécutant le rôle serveur de boîtes aux lettres, procédez comme suit pour redémarrer le service de banque d’informations de Microsoft Exchange :

1.  Ouvrez le **Panneau de configuration**, accédez à **Outils d’administration**, puis ouvrez **Services**.

2.  Cliquez avec le bouton droit sur **Banque d’informations Microsoft Exchange**, puis cliquez sur **Redémarrer**.

## Comment savoir si cela a fonctionné ?

Pour vérifier via le Centre d’administration Exchange qu’une licence Standard Edition ou Enterprise Edition a bien été attribuée au serveur, procédez comme suit :

1.  Entrez votre nom d'utilisateur et votre mot de passe dans **Domaine\\nom d'utilisateur** et **Mot de passe**, puis cliquez sur **Se connecter**.

2.  Accédez à **Serveurs** \> **Serveurs**.

3.  Sélectionnez le serveur à afficher, puis consultez le volet d'informations du serveur. Si la clé de produit est acceptée, la mention **Avec licence** s'affiche en même temps que l'édition Exchange 2013.

Pour vérifier via l’environnement de ligne de commande Exchange Management Shell qu’une licence Standard Edition ou Enterprise Edition a bien été attribuée au serveur, procédez comme suit :

1.  Ouvrez l'environnement de ligne de commande Exchange Management Shell.

2.  Exécutez la commande suivante pour afficher l’état de la licence d’un serveur Exchange donné.
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  (Facultatif) Exécutez la commande suivante pour afficher l’état des licences de tous les serveurs Exchange de votre organisation.
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto

