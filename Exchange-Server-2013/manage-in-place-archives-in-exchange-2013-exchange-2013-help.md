---
title: 'Gestion des archives permanentes dans Exchange 2013: Exchange 2013 Help'
TOCTitle: Gestion des archives permanentes dans Exchange 2013
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50478064
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des archives permanentes dans Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-02-01_

L’archivage inaltérable vous permet de reprendre le contrôle des données de messagerie de votre organisation en supprimant le besoin de recourir aux fichiers de magasin personnel (.pst) et en vous autorisant à répondre au besoin de rétention de messages et aux exigences relatives à la découverte électronique de votre organisation. Lorsque l’archivage est activé, les utilisateurs peuvent stocker des messages dans une boîte aux lettres d’archivage, accessible à l’aide de MicrosoftOutlook et Outlook Web App.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Archivage inaltérable » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - L’hébergement de la boîte aux lettres principale d’un utilisateur sur une version plus ancienne d’Exchange que l’archive de l’utilisateur n’est pas pris en charge. Si la boîte aux lettres principale de l’utilisateur est toujours sur Exchange 2010, vous devez la déplacer vers Exchange 2013, en même temps que vous déplacez l’archive vers Exchange 2013.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Créer une boîte aux lettres et activer une archive locale

## Utiliser le CAE

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Cliquez sur **Nouveau** \> **Boîte aux lettres utilisateur**.

3.  Sur la page **Nouvelle boîte aux lettres utilisateur**, dans le champ **Alias**, saisissez l’alias de l’utilisateur.
    
    > [!NOTE]  
    > Si vous laissez ce champ vide, la valeur entrée dans la zone <strong>Nom de connexion utilisateur</strong> est utilisée comme alias.


4.  Sélectionnez l’une des options suivantes :
    
      - **Utilisateur existant**   Cliquez sur ce bouton, puis sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un utilisateur – Forêt entière**. Cette boîte de dialogue contient une liste des comptes d’utilisateur Active Directory de la forêt qui ne sont pas à extension messagerie ou qui n’ont pas de boîte aux lettres Exchange. Sélectionnez le compte d’utilisateur pour lequel vous souhaitez activer la messagerie, puis cliquez sur **OK**. Si vous sélectionnez cette option, il n’est pas nécessaire de fournir les informations du compte d’utilisateur puisque ces dernières existent déjà dans Active Directory.
    
      - **Nouvel utilisateur**   Cliquez sur ce bouton pour créer un compte d’utilisateur dans Active Directory et créer une boîte aux lettres pour l’utilisateur. Si vous sélectionnez cette option, vous devrez fournir les informations de compte d’utilisateur requises.
    
    > [!NOTE]  
    > Le compte Active Directory qui est associé aux boîtes aux lettres d’utilisateur doit résider dans la même forêt que le serveur Exchange. Pour créer une boîte aux lettres pour un compte d’utilisateur résidant dans une forêt approuvée, vous devez créer une boîte aux lettres liée. Pour plus d’informations, voir <a href="manage-linked-mailboxes-exchange-2013-help.md">Gérer les boîtes aux lettres liées</a>.


5.  Cliquez sur **Plus d’options** pour configurer les paramètres suivants.
    
      - **Base de données de boîtes aux lettres**   Cliquez sur **Parcourir** pour sélectionner une base de données de boîtes aux lettres dans laquelle stocker la boîte aux lettres. Si vous ne sélectionnez pas de base de données, Exchange en attribue une automatiquement.
    
      - **Archive**   Cochez cette case pour créer une boîte aux lettres d’archivage pour la boîte aux lettres. Si vous créez une boîte aux lettres d’archivage, les éléments de la boîte aux lettres seront automatiquement déplacés de la boîte aux lettres principale vers l’archive, selon les paramètres de stratégie de rétention par défaut ou ceux que vous définissez.
        
        Cliquez sur **Parcourir** pour sélectionner une base de données résidant dans la forêt locale pour stocker la boîte aux lettres d’archivage.
        
        Pour en savoir plus, voir [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Stratégie de carnet d’adresses**   Sélectionnez dans cette liste une stratégie de carnet d’adresses pour la boîte aux lettres. Les stratégies de carnet d’adresses contiennent une liste d’adresses globale, un carnet d’adresses en mode hors connexion, une liste de salles et un ensemble de listes d’adresses. Lors de l’affectation aux utilisateurs de boîtes aux lettres, une stratégie de carnet d’adresses leur fournit l’accès à une liste d’adresses globale personnalisée dans Outlook et Outlook Web App. Pour en savoir plus, voir [Stratégies de carnet d’adresses](address-book-policies-exchange-2013-help.md).

6.  Lorsque vous avez terminé, cliquez sur **Enregistrer** pour créer la boîte aux lettres.

## Utiliser l’environnement de ligne de commande Exchange Management Shell

Cet exemple crée l’utilisateur Chris Ashton dans Active Directory, ainsi que la boîte aux lettres dans la base de données de boîtes aux lettres DB01, et active une archive. Le mot de passe doit être réinitialisé à la prochaine ouverture de session. Pour définir la valeur initiale du mot de passe, cet exemple crée une variable ($password), vous invite à entrer un mot de passe et affecte ce mot de passe à la variable en tant qu’objet SecureString.

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

## Comment savoir si l’opération a fonctionné ?

Pour vérifier que vous avez créé avec succès une boîte aux lettres utilisateur avec une archive locale, réalisez l’une des tâches suivantes :

  - Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez la nouvelle boîte aux lettres utilisateur dans la liste. Dans le volet d’informations, sous **Archive locale**, vérifiez que l’option est définie sur **Activé**. Cliquez sur **Afficher les détails** pour afficher les propriétés d’archivage, notamment l’état des archives et la base de données de boîtes aux lettres dans laquelle elles ont été créées.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher les informations relatives à la nouvelle boîte aux lettres utilisateur et à l’archive.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - Dans l’environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Test-ArchiveConnectivity** pour tester la connectivité à l’archive. Pour obtenir un exemple de test de la connectivité à l’archive, consultez la section Exemples de la rubrique [Test-ArchiveConnectivity](https://technet.microsoft.com/fr-fr/library/hh529914\(v=exchg.150\)).

## Activer une archive locale pour une boîte aux lettres existante

Vous pouvez également créer des archives pour les utilisateurs existants qui ont une boîte aux lettres mais dont l’archivage n’est pas activé. Cette opération est appelée l’*activation d’une archive* pour une boîte aux lettres existante.

## Utiliser le CAE

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez une boîte aux lettres.

3.  Dans le volet d’informations, sous **Archive locale**, cliquez sur **Activer**.
    
    > [!TIP]  
    > Vous pouvez également activer des archives en bloc en sélectionnant plusieurs boîtes aux lettres (à l’aide de la touche Maj ou Ctrl). Une fois les boîtes aux lettres sélectionnées, cliquez sur <strong>Plus d’options</strong> dans le volet d’informations. Sous <strong>Archive</strong>, cliquez sur <strong>Activer</strong>.


4.  Sur la page **Créer une archive locale**, cliquez sur **OK** pour qu’Exchange sélectionne automatiquement une base de données de boîtes aux lettres pour l’archive ou cliquez sur **Parcourir** pour en indiquer une.

## Utiliser l’environnement de ligne de commande Exchange Management Shell

Cet exemple active l’archive de la boîte aux lettres de Tony Smith.

    Enable-Mailbox "Tony Smith" -Archive

Cet exemple récupère les boîtes aux lettres de la base de données DB01 qui n’ont pas d’archive locale ou en nuage activée ou dont le nom ne commence pas par DiscoverySearchMailbox. Il redirige le résultat vers la cmdlet **Enable-Mailbox** afin d’activer l’archive pour toutes les boîtes aux lettres sur la base de données de boîtes aux lettres DB01.

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Enable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa998251\(v=exchg.150\)) et [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

## Comment savoir si l’opération a fonctionné ?

Pour vérifier que vous avez activé une archive locale pour une boîte aux lettres existante, exécutez l’une des actions suivantes :

  - Dans le CAE, accédez à **Destinataires** \> **Boîtes aux lettres**, puis sélectionnez la boîte aux lettres dans la liste. Dans le volet d’informations, sous **Archive locale**, vérifiez que l’option est définie sur **Activé**. Cliquez sur **Afficher les détails** pour afficher les propriétés d’archivage, notamment l’état des archives et la base de données de boîtes aux lettres dans laquelle elles ont été créées.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour afficher des informations sur la nouvelle archive.
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - Dans l’environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Test-ArchiveConnectivity** pour tester la connectivité à l’archive. Pour obtenir un exemple de test de la connectivité à l’archive, consultez la section Exemples de la rubrique [Test-ArchiveConnectivity](https://technet.microsoft.com/fr-fr/library/hh529914\(v=exchg.150\)).

## Désactiver une archive locale

Vous voulez peut-être désactiver l’archive d’utilisateur pour résoudre des problèmes ou pour déplacer la boîte aux lettres vers une version d’Exchange qui ne prend pas en charge l’archivage inaltérable. Si vous désactivez une archive locale, toutes les informations qu’elle contient seront conservées dans la base de données de boîtes aux lettres jusqu’à ce que le délai de rétention de cette dernière ait expiré et que l’archive soit définitivement supprimée. (Par défaut, Exchange conserve les boîtes aux lettres déconnectées, y compris les boîtes aux lettres d’archivage, pendant trente jours.)

> [!IMPORTANT]  
> La désactivation des archives entraîne leur suppression de la boîte aux lettres et leur marquage pour suppression dans la base de données de boîtes aux lettres.


Pour reconnecter l’archive locale à cette boîte aux lettres, vous pouvez utiliser la cmdlet [Connect-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997878\(v=exchg.150\)) avec le paramètre *Archive*.

## Utiliser le CAE

1.  Accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez une boîte aux lettres.

3.  Dans le volet d’informations, sous **Archive locale**, cliquez sur **Désactiver**.
    
    > [!TIP]  
    > Vous pouvez également désactiver des archives en bloc en sélectionnant plusieurs boîtes aux lettres (à l’aide de la touche Maj ou Ctrl). Une fois les boîtes aux lettres sélectionnées, cliquez sur <strong>Plus d’options</strong> dans le volet d’informations. Sous <strong>Archive</strong>, cliquez sur <strong>Désactiver</strong>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell

Cet exemple illustre la désactivation de l’archive pour la boîte aux lettres de Chris Ashton. Il n’indique pas comment désactiver la boîte aux lettres.

    Disable-Mailbox -Identity "Chris Ashton" -Archive

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Disable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997210\(v=exchg.150\)).

## Comment savoir si l’opération a fonctionné ?

Pour vérifier qu’une archive a bien été désactivée, procédez comme suit :

  - Dans le CAE, sélectionnez la boîte aux lettres. Ensuite, dans le volet d’informations, vérifiez l’état de son archive sous **Archive locale**.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante pour vérifier les propriétés de l’archive de l’utilisateur de la boîte aux lettres.
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    Si l’archive est désactivée, les valeurs suivantes sont retournées pour les propriétés associées à l’archive.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Propriété</th>
    <th>Valeur</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (pour les archives locales)</p></td>
    <td><p>&lt;vide&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (pour les archives locales)</p></td>
    <td><p>&lt;nom de la base de données de boîtes aux lettres&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;GUID de l’archive désactivée&gt;</p></td>
    </tr>
    </tbody>
    </table>


## Connecter une archive locale

Lorsque vous désactivez une boîte aux lettres d’archivage, elle est déconnectée. Une boîte aux lettres dont l’archive est déconnectée est conservée dans la base de données de boîtes aux lettres pendant une durée spécifiée. Par défaut, Exchange conserve les archives déconnectées pendant 30 jours. Pendant cette période, vous pouvez récupérer l’archive en l’associant à une boîte aux lettres existante. Vous pouvez modifier la période de rétention des boîtes aux lettres supprimées si vous souhaitez conserver une boîte aux lettres ou une archive supprimée pendant une période plus longue ou plus courte.

> [!CAUTION]
> Si vous désactivez une archive pour un utilisateur, puis activez une archive pour le même utilisateur, une nouvelle archive lui est octroyée. La nouvelle archive ne contient pas les données présentes dans l’archive déconnectée de l’utilisateur. Si vous souhaitez reconnecter un utilisateur à son archive déconnectée, vous devez appliquer cette procédure.


> [!NOTE]  
> Vous ne pouvez pas utiliser le CAE pour connecter une archive déconnectée à un utilisateur de boîte aux lettres.


## Utiliser l’environnement de ligne de commande Exchange Management Shell

1.  Si vous ne connaissez pas le nom de l’archive, vous pouvez l’afficher dans l’environnement de ligne de commande Exchange Management Shell en exécutant la commande suivante. Cet exemple récupère la base de données de boîtes aux lettres DB01, la transmet à la cmdlet **Get-MailboxStatistics** pour récupérer les statistiques de toutes les boîtes aux lettres de la base de données, puis utilise la cmdlet **Where-Object** pour filtrer les résultats et récupérer la liste des archives déconnectées. La commande affiche des informations supplémentaires sur chaque archive, notamment le GUID et le nombre d’éléments.
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  Connectez l’archive à la boîte aux lettres principale. Cet exemple montre comment connecter l’archive de Chris Ashton à sa boîte aux lettres principale et utilise le GUID comme identité de l’archive.
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques suivantes :

  - [Get-MailboxDatabase](https://technet.microsoft.com/fr-fr/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/fr-fr/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/fr-fr/library/aa998251\(v=exchg.150\))

## Comment savoir si l’opération a fonctionné ?

Pour vérifier que vous avez connecté une archive déconnectée à un utilisateur de boîte aux lettres, exécutez la commande Shell suivante pour récupérer les propriétés d’archivage de l’utilisateur de la boîte aux lettres et vérifier les valeurs retournées pour les propriétés *ArchiveGuid* et *ArchiveDatabase* :

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

