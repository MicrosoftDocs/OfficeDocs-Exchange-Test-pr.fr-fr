---
title: 'Ajouter ou supprimer des adresses de messagerie pour une boîte aux lettres: Exchange 2013 Help'
TOCTitle: Ajouter ou supprimer des adresses de messagerie pour une boîte aux lettres
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50555441
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ajouter ou supprimer des adresses de messagerie pour une boîte aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez configurer plusieurs adresses de messagerie pour une même boîte aux lettres. Les adresses supplémentaires sont appelées *adresses proxy*. Une adresse proxy permet à un utilisateur de recevoir un e-mail envoyé à une adresse de messagerie différente. Tous les e-mails envoyés à l’adresse proxy de l’utilisateur sont réceptionnés à son adresse de messagerie principale, également appelée *adresse SMTP principale* ou *adresse de réponse par défaut*.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous utilisez Office 365 pour les entreprises, vous devez ajouter ou supprimer des adresses de messagerie pour les boîtes aux lettres utilisateur dans le <a href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Centre d’administration Office 365 : Ajouter d’autres alias de messagerie à un utilisateur dans Office 365</a></td>
</tr>
</tbody>
</table>


Pour d’autres tâches de gestion relatives à la gestion des destinataires, consultez le tableau « Documentation des destinataires » dans [Recipients](recipients-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Les procédures de cette rubrique expliquent comment ajouter ou supprimer une adresse de messagerie pour une boîte aux lettres d’utilisateur. Vous pouvez utilisez des procédures similaires pour ajouter ou supprimer des adresses de messagerie pour d’autres type de destinataires.

## Que souhaitez-vous faire ?

## Ajouter une adresse de messagerie à une boîte aux lettres d’utilisateur

## Utiliser le Centre d’administration Exchange (EAC) pour ajouter une adresse de messagerie

1.  Dans le Centre d’administration Exchange, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres de votre choix pour y ajouter une adresse de messagerie, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Adresse e-mail**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Sur la page <strong>Adresse e-mail</strong>, l’adresse SMTP principale apparaît en caractères gras dans la liste des adresses, avec la valeur <strong>SMTP</strong> en majuscules dans la colonne <strong>Type</strong>.</td>
    </tr>
    </tbody>
    </table>


4.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis cliquez sur **SMTP** pour ajouter une adresse de messagerie SMTP à cette boîte aux lettres.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>SMTP est le type d’adresse de messagerie par défaut. Vous pouvez également ajouter des adresses de messagerie unifiée ou des adresses personnalisées à une boîte aux lettres. Pour plus d’informations, voir la section « Modifier les propriétés de boîte aux lettres d’utilisateur » de la rubrique <a href="manage-user-mailboxes-exchange-2013-help.md">Gestion des boîtes aux lettres utilisateur</a>.</td>
    </tr>
    </tbody>
    </table>


5.  Entrez la nouvelle adresse SMTP dans la zone **Adresse e-mail**, puis cliquez sur **OK**.
    
    La nouvelle adresse apparaît dans la liste des adresses de messagerie pour la boîte aux lettres sélectionnée.

6.  Cliquez sur **Enregistrer** pour enregistrer la modification.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter une adresse de messagerie

Les adresses de messagerie associées à une boîte aux lettres sont contenues dans la propriétés *EmailAddresses* de la boîte aux lettres. Parce qu’elle contient plusieurs adresses de messagerie, la propriété *EmailAddresses* est appelée « propriété *à valeurs multiples* ». Les exemples suivants présentent différentes manières de modifier une propriété à valeurs multiples.

Cet exemple décrit comment ajouter une adresse SMTP à la boîte aux lettres de Dan Jump.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

Cet exemple décrit comment ajouter plusieurs adresses SMTP à une boîte aux lettres.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

Pour plus d’informations sur l’utilisation de cette méthode d’ajout ou de suppression de valeurs pour des propriétés à valeurs multiples, consultez la rubrique [Modification de propriétés à valeurs multiples](modifying-multivalued-properties-exchange-2013-help.md).

Cet exemple décrit un autre moyen d’ajouter des adresses de messagerie à une boîte aux lettres en spécifiant toutes les adresses associées à la boîte aux lettres. Dans cette exemple, danj@tailspintoys.com est l’adresse de messagerie que vous souhaitez ajouter. Les deux autres adresses de messagerie sont des adresses existantes. L’adresse avec le qualificateur `SMTP` avec respect de la casse est l’adresse SMTP principale. Vous devez inclure toutes les adresses de messagerie pour la boîte aux lettres si vous utilisez cette syntaxe de commande. Si vous ne précédez pas ainsi, les adresses spécifiées dans la commande viennent écraser les adresses existantes.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une adresse de messagerie pour une boîte aux lettres, procédez de l’une des manières suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Adresse e-mail**.

  - Dans la liste des adresses de messagerie pour la boîte aux lettres, vérifiez que la nouvelle adresse de messagerie est incluse.

Ou

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Vérifiez que la nouvelle adresse de messagerie figure dans les résultats.

## Supprimer une adresse de messagerie d’une boîte aux lettres d’utilisateur

## Utiliser le Centre d’administration Exchange (EAC) pour supprimer une adresse de messagerie

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Dans la liste des boîtes aux lettres utilisateurs, cliquez sur la boîte aux lettres de votre choix pour y supprimer une adresse de messagerie, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page de propriétés de boîte aux lettres, cliquez sur **Adresse e-mail**.

4.  Dans la liste des adresses de messagerie, sélectionnez l’adresse que vous souhaitez supprimer, puis cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

5.  Cliquez sur **Enregistrer** pour enregistrer la modification.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer une adresse de messagerie

Cet exemple décrit comment supprimer une adresse de messagerie de la boîte aux lettres de Janet Schorr.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

Cet exemple décrit comment supprimer plusieurs adresses d’une boîte aux lettres.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

Pour plus d’informations sur l’utilisation de cette méthode d’ajout ou de suppression de valeurs pour des propriétés à valeurs multiples, consultez la rubrique [Modification de propriétés à valeurs multiples](modifying-multivalued-properties-exchange-2013-help.md).

Vous pouvez également supprimer une adresse de messagerie en l’omettant de la commande permettant de définir des adresses de messagerie pour une boîte aux lettres. Par exemple, supposons que la boîte aux lettres de Janet Schorr possède trois adresses de messagerie : janets@contoso.com (l’adresse SMTP principale), janets@corp.contoso.com et janets@tailspintoys.com. Pour supprimer l’adresse janets@corp.contoso.com, vous devez exécuter la commande suivante.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

Parce qu’elle a été omise de la commande précédente, l’adresse janets@corp.contoso.com est supprimée de la boîte aux lettres.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une adresse de messagerie a bien été supprimée d’une boîte aux lettres, procédez de l’une des manières suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Adresse e-mail**.

  - Dans la liste des adresses de messagerie pour la boîte aux lettres, vérifiez que l’adresse de messagerie en est absente.

Ou

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Vérifiez que l’adresse de messagerie est absente des résultats.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter des adresses de messagerie à plusieurs boîtes aux lettres

Vous pouvez ajouter une nouvelle adresse de messagerie à plusieurs boîtes aux lettres à l’aide de l’environnement de ligne de commande Exchange Management Shell et d’un fichier à valeurs séparées par des virgules (CSV).

Dans cet exemple, nous importons des données de C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv, dont le format est le suivant.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

Exécutez la commande suivante pour utiliser les données du fichier CSV pour ajouter l’adresse de messagerie électronique à chacune des boîtes aux lettres spécifiées dans le fichier CSV.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les noms de colonne de la première ligne de ce fichier CSV (<code>Mailbox,NewEmailAddress</code>) sont arbitraires. Quels que soient les noms de colonne utilisés, veillez à employer les mêmes noms dans la commande de l’environnement de ligne de commande Exchange Management Shell.</td>
</tr>
</tbody>
</table>


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement créé une adresse de messagerie pour plusieurs boîtes aux lettres, procédez de l’une des manières suivantes :

  - Dans le Centre d’administration Exchange (EAC), accédez à **Destinataires** \> **Boîtes aux lettres**, cliquez sur la boîte aux lettres pour laquelle vous ajoutez l’adresse, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

  - Dans la page de propriétés de boîte aux lettres, cliquez sur **Adresse e-mail**.

  - Dans la liste des adresses de messagerie pour la boîte aux lettres, vérifiez que la nouvelle adresse de messagerie est incluse.

Ou

  - Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell, en utilisant le même fichier CSV que vous avez utilisé pour ajouter la nouvelle adresse de messagerie.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - Vérifiez que la nouvelle adresse de messagerie figure dans les résultats de chaque boîte aux lettres.

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

