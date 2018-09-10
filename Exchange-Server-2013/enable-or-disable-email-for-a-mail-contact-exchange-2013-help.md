---
title: 'Activer ou désactiver la messagerie pour un contact: Exchange 2013 Help'
TOCTitle: Activer ou désactiver la messagerie pour un contact de messagerie
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50555492
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer ou désactiver la messagerie pour un contact de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-12-05_

Vous pouvez désactiver la messagerie électronique pour un contact de messagerie existant dans votre organisation Exchange. Lorsque vous désactivez la messagerie électronique pour un contact de messagerie, la suppression s'effectue dans Exchange et dans le carnet d’adresse de votre organisation. Si le contact de messagerie est membre d’un groupe de distribution, le contact ne reçoit plus les messages envoyés au groupe. En outre, les attributs Exchange sont supprimés de l’objet de contact a extension messagerie dans Active Directory, mais le contact et ses attributs non Exchange (comme des informations relatives aux contacts et à l’organisation) sont conservés dans Active Directory.

Après avoir désactivé la messagerie électronique d’un contact de messagerie, vous avez toujours utiliser la cmdlet **Enable-MailContact** dans l’environnement de ligne de commande Exchange Management Shell pour réactiver le contact pour la messagerie. Vous pouvez également utiliser cette cmdlet pour activer la messagerie pour tout contact Active Directory.

Pour connaître les tâches de gestion supplémentaires relatives aux contacts de messagerie, consultez la rubrique [Gérer les contacts de messagerie](https://docs.microsoft.com/fr-fr/exchange/recipients-in-exchange-online/manage-mail-contacts).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Contacts de messagerie » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Désactiver la messagerie électronique pour un contact de messagerie

Comme précédemment mentionné, lorsque vous désactivez la messagerie électronique pour un contact de messagerie, les attributs Exchange sont supprimés de l’objet de contact Active Directory correspondant, mais le contact est conservé. Le contact de messagerie est supprimé de la liste des contacts de messagerie dans le Centre d’administration Exchange (EAC), mais vous pouvez afficher et gérer l’objet de contact Active Directory correspondant à l’aide du composant Utilisateurs et ordinateurs Active Directory ou à l’aide des cmdlets **Get-Contact** et **Set-Contact** dans l’environnement de ligne de commande Exchange Management Shell.

## Utiliser le Centre d’administration Exchange (EAC) pour désactiver la messagerie électronique pour un contact de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Contacts**.

2.  Dans la liste des contacts, cliquez sur le contact de messagerie pour lequel vous voulez désactiver la messagerie électronique.

3.  Cliquez sur **Autre**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Désactiver**.

4.  Le message d’avertissement qui s’affiche vous demande de confirmer la désactivation du contact de messagerie sélectionné. Cliquez sur **Oui** pour le désactiver.

Le contact de messagerie est supprimé de la liste de contacts.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver la messagerie électronique pour un contact de messagerie

Dans cet exemple, nous désactivons la messagerie électronique pour le contact de messagerie Neil Black.

    Disable-MailContact -Identity "Neil Black"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Disable-MailContact](https://technet.microsoft.com/fr-fr/library/aa997465\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que la messagerie électronique a bien été désactivée pour un contact de messagerie, procédez selon l’une des manières suivantes :

1.  Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Contacts**, puis vérifiez que le contact de messagerie n’est plus répertorié.

2.  Dans le composant Utilisateurs et ordinateurs Active Directory, cliquez avec le bouton droit sur le contact, puis cliquez sur **Propriétés**. Sous l’onglet **Général**, notez que la zone **Courrier électronique** est vide. Ceci permet de vérifier que le contact n’est pas à extension messagerie.

3.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-MailContact
    
    Le contact pour lequel vous avez désactivé la messagerie électronique est absent des résultats parce que cette cmdlet ne renvoie que les contacts à extension messagerie.

4.  Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-Contact
    
    Le contact pour lequel vous avez désactivé la messagerie électronique figure dans les résultats parce que cette cmdlet renvoie tous les objets de contact Active Directory.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer des contacts à extension messagerie

La cmdlet **Enable-MailContact** permet d’activer la messagerie pour des contacts Active Directory. Vous pouvez activer la messagerie pour un contact unique ou utiliser un fichier CSV pour activer la messagerie de plusieurs contacts.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer la messagerie d’un contact unique

Dans cet exemple, nous activons la messagerie pour le contact Rene Valdes. Vous devez fournir une adresse de messagerie externe.

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## Utiliser l’environnement de ligne de commande Exchange Management Shell et un fichier CSV pour activer la messagerie pour plusieurs contacts

Lors de l’activation de la messagerie de contacts en bloc, vous devez commencer par exporter la liste des contacts qui ne sont pas à extension messagerie dans un fichier CSV (valeurs séparées par des virgules), et ajouter ensuite les adresses de messagerie électronique externes au fichier CSV à l’aide d’un éditeur de texte comme le Bloc-notes ou une application avec feuille de calcul comme Microsoft Excel. Ensuite, utilisez le fichier CSV mis à jour dans la commande de l’environnement de ligne de commande Exchange Management Shell pour activer la messagerie des contacts répertoriés dans le fichier CSV.

1.  Exécutez la commande suivante pour exporter la liste des contacts existants qui ne sont pas à extension messagerie dans un fichier du bureau de l’administrateur intitulé Contacts.csv.
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    Le fichier résultat doit ressembler au fichier suivant :
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  Ajoutez un en-tête de colonne intitulé **EmailAddress**, puis ajoutez une adresse de messagerie électronique pour chaque contact figurant dans le fichier. Le nom et l’adresse de messagerie électronique externe associés à chaque contact doivent être séparés par une virgule. Le fichier CSV mis à jour doit ressembler au fichier suivant.
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  Exécutez la commande suivante pour utiliser les données du fichier CSV pour activer la messagerie des contacts répertoriés dans le fichier.
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    Les résultats de la commande affichent les informations relatives aux nouveaux contacts à extension messagerie.

## Comment savoir si cela a fonctionné ?

Pour vérifier l’activation de la messagerie des contacts Active Directory s’est correctement effectuée, procédez selon l’une des manières suivantes :

  - Dans le CAE, accédez à **Destinataires**  \> **Contacts**. Les nouveaux contacts de messagerie sont affichés dans la liste des contacts. Sous **Type de contact**, le type est **Contact de messagerie**.
    
    > [!NOTE]
    > Vous devez peut-être cliquer sur <strong>Actualiser</strong><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Icône Actualiser" alt="Icône Actualiser" /> pour afficher les nouveaux contacts de messagerie.


  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations relatives aux nouveaux contacts de messagerie.
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

