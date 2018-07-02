---
title: 'Activer ou désactiver la messagerie pour un utilisateur de messagerie: Exchange 2013 Help'
TOCTitle: Activer ou désactiver la messagerie pour un utilisateur de messagerie
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50555358
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver la messagerie pour un utilisateur de messagerie

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-14_

Vous pouvez désactiver la messagerie pour un utilisateur de messagerie existant dans votre organisation Exchange. Lorsque vous désactivez la messagerie pour un utilisateur de messagerie, elle est supprimée d’Exchange et du carnet d’adresses de votre organisation. Si l’utilisateur de messagerie est membre d’un groupe de distribution, l’utilisateur ne reçoit plus la messagerie envoyée au groupe. De plus, les attributs d’Exchange sont supprimés de l’objet utilisateur dans Active Directory. Toutefois, cet objet et ses attributs non Exchange (tels que les coordonnées et les informations sur l’organisation) sont conservés dans Active Directory.

Après avoir désactivé la messagerie pour un utilisateur de messagerie, vous pouvez réactiver la messagerie de l’utilisateur à l’aide de la cmdlet **Enable-MailUser** dans l’environnement de ligne de commande Exchange Management Shell. Vous pouvez également utiliser cette cmdlet pour activer la messagerie de tout utilisateur Active Directory.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les utilisateurs de messagerie (également appelés <em>utilisateurs à extension messagerie</em>) diffèrent des utilisateurs disposant d’une boîte aux lettres dans votre organisation. La principale différence est que les utilisateurs de messagerie sont ceux qui possèdent une adresse de messagerie externe à votre organisation Exchange. Ils ne possèdent pas de boîte aux lettres dans votre organisation. Pour de plus amples informations sur les différences entre les utilisateurs disposant de boîtes aux lettres dans votre organisation et les utilisateurs de messagerie, consultez la rubrique <a href="recipients-exchange-2013-help.md">Recipients</a>.</td>
</tr>
</tbody>
</table>


Pour d’autres tâches de gestion relatives aux utilisateurs de messagerie, consultez la rubrique [Gérer les utilisateurs de messagerie](manage-mail-users-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Utilisateurs de messagerie » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

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


## Que souhaitez-vous faire ?

## Désactivation de la messagerie pour un utilisateur de messagerie

Comme indiqué précédemment, lorsque vous désactivez la messagerie électronique pour un utilisateur de messagerie, les attributs d’Exchange sont supprimés de l’objet utilisateur de messagerie Active Directory correspondant, mais l’utilisateur est conservé. L’utilisateur de messagerie est supprimé de la liste d’utilisateurs de messagerie du CAE. Toutefois, vous pouvez afficher et gérer l’objet de contact Active Directory correspondant à l’aide du composant Utilisateurs et ordinateurs Active Directory ou des cmdlets **Get-MailUser** et **Set-Set-MailUser** de l’environnement de ligne de commande Exchange Management Shell.

## Désactivation de la messagerie pour un utilisateur de messagerie à l’aide du Centre d’administration Exchange (CAE)

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste de contacts, cliquez sur l’utilisateur de messagerie pour lequel vous souhaitez désactiver la messagerie.

3.  Cliquez sur **Plus**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis sur **Désactiver**.

4.  Un message d’avertissement vous demande de confirmer la désactivation de l’utilisateur de messagerie sélectionné. Cliquez sur **Oui** pour le désactiver.

L’utilisateur de messagerie est supprimé de la liste de contacts.

## Désactivation de la messagerie pour un utilisateur de messagerie à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment désactiver la messagerie pour l’utilisateur de messagerie Yan Li.

    Disable-MailUser -Identity "Yan Li"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Disable-MailUser](https://technet.microsoft.com/fr-fr/library/aa998578\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien désactivé la messagerie pour un utilisateur de messagerie, suivez l’une des procédures ci-dessous :

1.  Dans le CAE, accédez à **Destinataires** \> **Contacts** et vérifiez que l’utilisateur de messagerie ne figure plus dans la liste.

2.  Dans Utilisateurs et ordinateurs Active Directory, cliquez avec le bouton droit sur l’utilisateur, puis cliquez sur **Propriétés**. Dans l’onglet **Général**, remarquez que le champ **Courrier électronique** est vide. Cela indique que l’utilisateur n’est pas activé pour la messagerie.

3.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-MailUser
    
    L’utilisateur de messagerie pour lequel vous avez désactivé la messagerie électronique ne sera pas renvoyé dans les résultats car cette cmdlet ne renvoie que les utilisateurs à extension messagerie.

4.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-User
    
    L’utilisateur de messagerie pour lequel vous avez désactivé la messagerie est renvoyé dans les résultats car cette cmdlet renvoie tous les objets utilisateur Active Directory.

## Activation des utilisateurs à extension messagerie à l’aide de l’environnement de ligne de commande Exchange Management Shell

La cmdlet **Enable-MailUser** permet d’activer la messagerie des utilisateurs Active Directory existants. Vous pouvez activer la messagerie d’un seul utilisateur ou utiliser un fichier CSV pour activer la messagerie de plusieurs utilisateurs.

## Activation de la messagerie pour un seul utilisateur à l’aide de l’environnement de ligne de commande Exchange Management Shell

Cet exemple montre comment activer la messagerie pour l’utilisateur Sanjay Shah. Vous devez saisir une adresse de messagerie externe.

    Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com

## Activation de la messagerie pour plusieurs utilisateurs à l’aide de l’environnement de ligne de commande Exchange Management Shell et d’un fichier CSV

Lorsque vous activez la messagerie pour un groupe d’utilisateurs, vous exportez d’abord la liste des utilisateurs qui ne sont pas activés pour la messagerie vers un fichier CSV (valeurs séparées par une virgule), puis ajoutez les adresses de messagerie externes au fichier CSV à l’aide d’un éditeur de texte, tel que le Bloc-notes ou un tableur tel que Microsoft Excel. Vous utilisez ensuite le fichier CSV mis à jour dans la commande de l’environnement de ligne de commande Exchange Management Shell pour activer la messagerie des utilisateurs répertoriés dans le fichier CSV.

1.  Exécutez la commande suivante pour exporter une liste des utilisateurs existants qui ne sont pas activés pour la messagerie ou ne disposant pas d’une boîte aux lettres dans votre organisation vers un fichier du Bureau de l’administrateur appelé UsersToMailEnable.csv :
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    Le fichier obtenu ressemble à celui-ci :
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  Apportez les modifications suivantes au fichier CSV :
    
      - Supprimez du fichier CSV tous les utilisateurs pour lesquels vous ne souhaitez pas activer la messagerie. Par exemple, vous pouvez supprimer les trois premières entrées dans l’exemple précédent car il s’agit de comptes système par défaut.
    
      - Supprimez la colonne **RecipientType** et toutes les instances de `User`.
    
      - Ajoutez un en-tête de colonne appelé **EmailAddress**, puis ajoutez une adresse de messagerie pour chaque utilisateur dans le fichier. Le nom et l’adresse de messagerie externe de chaque utilisateur doivent être séparés par une virgule.
    
    Le fichier CSV mis à jour doit ressembler à celui-ci :
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  Exécutez la commande suivante pour utiliser les données du fichier CSV afin d’activer la messagerie des utilisateurs répertoriés dans le fichier :
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    Les résultats de la commande affichent des informations sur les nouveaux utilisateurs à extension messagerie.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé la messagerie des utilisateurs Active Directory, procédez comme suit :

  - Dans le CAE, accédez à **Destinataires**  \> **Contacts**. Les nouveaux utilisateurs de messagerie sont affichés dans la liste de contacts. Sous **Type de contact**, le type est **Utilisateur de messagerie**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous devrez éventuellement cliquer sur <strong>Actualiser</strong><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Icône Actualiser" alt="Icône Actualiser" /> pour afficher les nouveaux utilisateurs de messagerie.</td>
    </tr>
    </tbody>
    </table>


  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher des informations sur les nouveaux utilisateurs de messagerie :
    
        Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

