---
title: 'Connecter ou restaurer une boîte aux lettres supprimée: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Connexion ou restauration d’une boîte aux lettres supprimée
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50555453
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connexion ou restauration d’une boîte aux lettres supprimée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-05-04_

Le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande vous permet de connecter une boîte aux lettres supprimée à un compte d'utilisateur Active Directory. Lorsque vous supprimez une boîte aux lettres, Exchange conserve celle-ci dans la base de données de boîtes aux lettres et change son état en « désactivé ». Le compte d'utilisateur Active Directory associé est également supprimé. La boîte aux lettres est conservée tant que le délai de rétention des boîtes aux lettres supprimées n’a pas expiré. Ce délai est défini par défaut à 30 jours. Une fois ce délai passé, la boîte aux lettres est supprimée définitivement (ou *purgée*) de la base de données de boîtes aux lettres.

Tant qu'une boîte aux lettres supprimée n'a pas été supprimée définitivement de la base de données de boîtes aux lettres Exchange, vous pouvez la connecter à un compte d'utilisateur Active Directory à l'aide du CAE ou de l'environnement de ligne de commande. L'environnement de ligne de commande vous permet également de restaurer le contenu de la boîte aux lettres supprimée dans une boîte aux lettres existante.

Pour plus d'informations sur les boîtes aux lettres déconnectées et sur l'exécution d'autres tâches de gestion associées, consultez les rubriques suivantes :

  - [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md)

  - [Désactiver ou supprimer une boîte aux lettres](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Connecter une boîte aux lettres déconnectée](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

## Ce qu'il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Créez un compte d'utilisateur dans Active Directory pour vous connecter à la boîte aux lettres supprimée. Ou dans l’environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Get-User** pour vérifier que le compte utilisateur Active Directory auquel vous voulez connecter la boîte aux lettres supprimée existe et qu’il n’est pas déjà associé à une autre boîte aux lettres. Pour connecter une boîte aux lettres supprimée à un compte utilisateur, le compte doit exister et la valeur pour la propriété *RecipientType* doit être `User`, ce qui indique que le compte n’est pas à extension boîte aux lettres.
    
    S'agissant des organisations Exchange locales, vous pouvez également vérifier ces informations dans le composant Utilisateurs et ordinateurs Active Directory.
    
    > [!NOTE]
    > Lorsque vous connectez des boîtes aux lettres liées, des boîtes aux lettres de ressources ou des boîtes aux lettres partagées supprimées, le compte d’utilisateur auquel vous connectez la boîte aux lettres doit être désactivé.


  - Pour vérifier que la boîte aux lettres supprimée à laquelle vous voulez connecter un compte utilisateur existe dans la base de données des boîtes aux lettres et qu’elle n’est pas une boîte aux lettres supprimée (récupérable), exécutez la commande suivante.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    La boîte aux lettres supprimée doit exister dans la base de données des boîtes aux lettres et la valeur de la propriété *DisconnectReason* doit être `Disabled`. Si la boîte aux lettres a été purgée de la base de données, la commande ne renvoie aucun résultat.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Que souhaitez-vous faire ?

## Connecter une boîte aux lettres supprimée

Lorsque vous connectez une boîte aux lettres supprimée, vous associez celle-ci à un compte utilisateur qui n’est pas à extension messagerie, en d’autres termes, il ne possède pas de boîte aux lettres existante. Pour connecter une boîte aux lettres supprimée à un compte d'utilisateur possédant une boîte aux lettres, vous devez restaurer la boîte aux lettres supprimée. Pour plus d'informations, consultez la section Restaurer une boîte aux lettres supprimée plus loin dans cette rubrique.

## Utiliser le CAE pour connecter une boîte aux lettres supprimée

La procédure suivante montre comment connecter une boîte aux lettres utilisateur supprimée à un compte d'utilisateur. Cette procédure permet également de connecter à un compte d'utilisateur des boîtes aux lettres liées, des boîtes aux lettres de ressources et des boîtes aux lettres partagées qui ont été supprimées.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Cliquez sur **Autres** ![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis sur **Se connecter à une boîte aux lettres**.
    
    La liste des boîtes aux lettres déconnectées sur le serveur Exchange sélectionné de votre organisation Exchange s'affiche.
    
    > [!NOTE]
    > Cette liste de boîtes aux lettres déconnectées inclut des boîtes aux lettres désactivées, des boîtes aux lettres supprimées et des boîtes aux lettres supprimées (récupérables).


3.  Cliquez sur la boîte aux lettres à laquelle vous voulez connecter un utilisateur, puis sur **Connecter**.

4.  Dans la fenêtre de demande de confirmation de connexion de la boîte aux lettres, cliquez sur **Oui**.
    
    La liste de comptes utilisateurs qui ne sont pas à extension messagerie s’affiche.

5.  Cliquez sur l'utilisateur auquel vous voulez connecter la boîte aux lettres supprimée, puis sur **Connecter**.
    
    Exchange connecte la boîte aux lettres supprimée au compte d'utilisateur que vous avez sélectionné.

## Utiliser l'environnement de ligne de commande pour connecter une boîte aux lettres supprimée

Dans l’environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Connect-Mailbox** pour connecter une boîte aux lettres supprimée à un compte utilisateur qui n’est pas à extension messagerie. Vous devez spécifier le type de boîte aux lettres que vous connectez. Les exemples suivantes montrent la syntaxe pour la reconnexion de boîtes aux lettres utilisateur, liées, de salle, d'équipement et partagées. Dans tous les exemples, nous utilisons le paramètre *Alias* facultatif pour spécifier l'alias de courrier électronique. Il s'agit de la partie de l'adresse de messagerie qui est située à gauche du symbole @. Si vous n’utilisez pas le paramètre *Alias*, la valeur spécifiée dans le paramètre *User* ou *LinkedMasterAccount* est utilisée pour créer l’alias pour l’adresse de messagerie associée à la boîte aux lettres reconnectée.

> [!NOTE]
> Comme indiqué précédemment, lorsque vous connectez des boîtes aux lettres liées, de ressources ou partagées, le compte d’utilisateur Active Directory auquel vous liez la boîte aux lettres doit être désactivé.


Cet exemple montre comment connecter une boîte aux lettres utilisateur. Le paramètre *Identity* indique le nom complet de la boîte aux lettres supprimée qui est conservée dans la base de données de boîtes aux lettres MBXDB01. Le paramètre *User* indique le compte d'utilisateur Active Directory auquel connecter la boîte aux lettres.

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw

> [!NOTE]
> Vous pouvez également utiliser les valeurs des propriétés <code>LegacyDN</code> ou <code>MailboxGuid</code> pour identifier la boîte aux lettres supprimée.


Cet exemple montre comment connecter une boîte aux lettres liée. Le paramètre *Identity* indique la boîte aux lettres supprimée dans la base de données de boîtes aux lettres MBXDB02. Le paramètre *LinkedMasterAccount* indique le compte d'utilisateur Active Directory dans la forêt de comptes, auquel vous voulez connecter la boîte aux lettres. Le paramètre *LinkedDomainController* indique un contrôleur de domaine dans la forêt de comptes.

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

Cet exemple montre comment connecter une boîte aux lettres de salle.

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

Cet exemple montre comment connecter une boîte aux lettres de ressource.

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

Cet exemple montre comment connecter une boîte aux lettres partagée.

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared

> [!NOTE]
> Vous pouvez également utiliser les valeurs <code>LegacyDN</code> ou <code>MailboxGuid</code> pour identifier la boîte aux lettres supprimée.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [Connect-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997878\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une boîte aux lettres supprimée a bien été connectée à un compte utilisateur, exécutez l’une des actions suivantes :

  - Dans le CAE, cliquez sur **Destinataires**, accédez à la page appropriée pour le type de boîte aux lettres pour lequel vous avez effectué la connexion, cliquez sur **Actualiser** ![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser"), puis vérifiez que la boîte aux lettres est répertoriée.

  - Dans le composant Utilisateurs et ordinateurs Active Directory, cliquez avec le bouton droit sur le compte d'utilisateur auquel vous connectez la boîte aux lettres, puis cliquez sur **Propriétés**. Sous l'onglet **Général**, notez que la zone **Courrier électronique** contient l'adresse de messagerie associée à la boîte aux lettres connectée.

  - Dans l'environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
        Get-User <identity>
    
    La valeur **UserMailbox** de la propriété *RecipientType* indique que le compte d'utilisateur et la boîte aux lettres sont connectés. Vous pouvez également exécuter la commande **Get-Mailbox \<identité\>** pour vérifier que la boîte aux lettres a été connectée.

## Restaurer une boîte aux lettres supprimée

L'environnement de ligne de commande permet de restaurer une boîte aux lettres supprimée dans une boîte aux lettres existante à l'aide de la cmdlet **New-MailboxRestoreRequest**. Lorsque vous restaurez une boîte aux lettres supprimée, son contenu est copié dans une boîte aux lettres existante, appelée *boîte aux lettres cible*. Après la restauration de la boîte aux lettres supprimée, celle-ci est conservée dans la base de données de boîtes aux lettres tant qu’un administrateur ne l’a pas supprimée définitivement ou qu’elle n’a pas été purgée après l’expiration du délai de rétention des boîtes aux lettres supprimées.

Après qu'une demande de restauration de boîte aux lettres a été correctement exécutée, la boîte aux lettres est conservée pendant 30 jours avant d'être supprimée. Vous pouvez la supprimer plus tôt à l'aide de la cmdlet **Remove-StoreMailbox**.

> [!NOTE]
> Le CAE ne permet pas de restaurer une boîte aux lettres supprimée.


## Utiliser l'environnement de ligne de commande pour restaurer une boîte aux lettres supprimée

Pour créer une demande de restauration de boîte aux lettres, vous devez utiliser le nom complet, le nom unique hérité ou le GUID de la boîte aux lettres supprimée. Utilisez la cmdlet **Get-MailboxStatistics** pour afficher les valeurs des propriétés `DisplayName`, `MailboxGuid` et `LegacyDN` pour la boîte aux lettres supprimée à restaurer. Par exemple, exécutez la commande suivante pour renvoyer ces informations pour toutes les boîtes aux lettres désactivées et supprimées au sein de votre organisation.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

Cet exemple montre comment restaurer dans la boîte aux lettres cible de Debra Garcia, la boîte aux lettres supprimée identifiée par le paramètre *SourceStoreMailbox* , qui se trouve dans la base de données de boîtes aux lettres MBXDB01. Le paramètre *AllowLegacyDNMismatch* est utilisé de façon à ce que la boîte aux lettres source puisse être restaurée dans une autre boîte aux lettres dont la valeur de nom unique hérité diffère.

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

Dans cet exemple, nous restaurons la boîte aux lettres d’archive supprimée de Pilar Pinilla dans sa boîte aux lettres d’archive. Le paramètre *AllowLegacyDNMismatch* n’est pas nécessaire, car une boîte aux lettres principale et sa boîte aux lettres d’archivage correspondante comportent le même nom unique hérité.

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, consultez la rubrique [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour restaurer une boîte aux lettres de dossier public supprimée

Si vous avez supprimé définitivement une boîte aux lettres de dossiers publics que vous voulez à présent restaurer et que la boîte aux lettres n’a pas dépassé la limite Rétention des éléments supprimés (voir [Configurer la rétention des éléments supprimés et les quotas d’éléments récupérables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)) que vous pouvez utiliser la cmdlet `Connect-Mailbox`, suivie par la cmdlet `Update-StoreMailboxState`. Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Connect-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997878\(v=exchg.150\)) et [Update-StoreMailboxState](https://technet.microsoft.com/fr-fr/library/jj860462\(v=exchg.150\)).

Vous aurez besoin du GUID de la boîte aux lettres de dossiers publics supprimée, ainsi que du GUID ou du nom de la base de données de boîtes aux lettres qui contenait la boîte aux lettres de dossiers publics. Si vous ne disposez pas de ces informations, vous pouvez prendre les mesures suivantes :

1.  Obtenir le nom de domaine complet (FQDN) du contrôleur de domaine et de forêt Active Directory en exécutant la cmdlet suivante :
    
        Get-OrganizationConfig | fl OriginatingServer

2.  Avec les informations renvoyées par l’étape 1, recherchez dans le conteneur Objets supprimés dans Active Directory le GUID de la boîte aux lettres de dossiers publics et le GUID ou le nom de la base de données de boîtes aux lettres dans laquelle la boîte aux lettres de dossiers publics supprimée était contenue.
    
    > [!TIP]
    > Vous pouvez rechercher des objets supprimés à l’aide d’un script personnalisé ou à l’aide de l’utilitaire Ldp, qui peut être ouvert en saisissant <strong>ldp.exe</strong> à l’invite Powershell.


Si vous connaissez le GUID de la boîte aux lettres de dossiers publics supprimée et le nom ou le GUID de la base de données de boîtes aux lettres qui contenait la boîte aux lettres de dossiers publics, exécutez les commandes suivantes pour restaurer la boîte aux lettres de dossiers publics.

1.  Créer un nouvel objet Active Directory en exécutant les commandes suivantes (vous pouvez être invité à fournir des informations d’identification appropriées) :
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    Où `<mailUserName>`, `<emailAddress>` et `<mailUserName>` sont des valeurs que vous choisissez. Vous devez utiliser la même valeur `<mailUserName>` à l’étape suivante.

2.  Connectez la boîte aux lettres de dossiers publics supprimée à l’objet Active Directory que vous venez de créer en exécutant la commande suivante :
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    
    > [!NOTE]
    > Le paramètre <code>Identity</code> spécifie l’objet de boîte aux lettres dans la base de données Exchange à connecter à un objet utilisateur Active Directory. L’exemple ci-dessus spécifie le GUID pour la boîte aux lettres de dossiers publics, mais vous pouvez également utiliser la valeur de nom d’affichage ou la valeur LegacyExchangeDN.


3.  Exécutez `Update-StoreMailboxState` sur la boîte aux lettres de dossiers publics, en fonction de l’exemple suivant :
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    Comme à l’étape 2, le paramètre `Identity` acceptera les valeurs GUID, nom d’affichage ou LegacyExchangeDN pour la boîte aux lettres de dossiers publics.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien restauré une boîte aux lettres de dossiers publics supprimée, exécutez la cmdlet **Get-PublicFolder -GetChildren -\<GUID de la boîte aux lettres de dossiers publics\>**. Si la restauration a réussi, cette cmdlet fonctionne.

Pour plus d'informations, consultez les rubriques suivantes :

  - [Connect-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/fr-fr/library/jj860462\(v=exchg.150\))

