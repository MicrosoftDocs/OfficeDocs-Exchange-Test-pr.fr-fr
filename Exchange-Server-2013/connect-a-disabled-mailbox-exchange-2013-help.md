---
title: 'Connecter une boîte aux lettres déconnectée: Exchange 2013 Help'
TOCTitle: Connecter une boîte aux lettres déconnectée
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50555470
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connecter une boîte aux lettres déconnectée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-13_

Le Centre d’administration Exchange ou l’environnement de ligne de commande Exchange Management Shell vous permet de connecter une boîte aux lettres désactivée à un compte utilisateur Active Directory. Lorsque vous désactivez une boîte aux lettres, Exchange conserve celle-ci dans la base de données de boîtes aux lettres et change son état pour « désactivé ». Les attributs Exchange sont également supprimés du compte utilisateur Active Directory, mais le compte utilisateur est conservé. La boîte aux lettres est conservée tant que le délai de rétention des boîtes aux lettres supprimées n’a pas expiré. Ce délai est défini par défaut à 30 jours. Une fois ce délai passé, la boîte aux lettres est supprimée définitivement (ou *purgée*) de la base de données de boîtes aux lettres.

Tant qu’une boîte aux lettres désactivée n’a pas été supprimée définitivement de la base de données de boîtes aux lettres Exchange, vous pouvez la connecter à son compte utilisateur Active Directory d’origine à l’aide du Centre d’administration Exchange ou de l’environnement de ligne de commande Exchange Management Shell.

Pour plus d’informations sur les boîtes aux lettres déconnectées et sur l’exécution des autres tâches de gestion associées, consultez les rubriques suivantes :

  - [Boîtes aux lettres déconnectées](disconnected-mailboxes-exchange-2013-help.md)

  - [Désactiver ou supprimer une boîte aux lettres](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Connexion ou restauration d’une boîte aux lettres supprimée](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Supprimer définitivement une boîte aux lettres](permanently-delete-a-mailbox-exchange-2013-help.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Section « Autorisations de configuration des destinataires » dans la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la cmdlet **Get-User** pour vérifier que le compte utilisateur Active Directory auquel vous voulez connecter la boîte aux lettres désactivée existe et qu’il n’est pas déjà associé à une autre boîte aux lettres. Pour connecter une boîte aux lettres désactivée à un compte utilisateur, le compte doit exister et la valeur pour la propriété *RecipientType* doit être `User`, ce qui indique que le compte n’est pas à extension boîte aux lettres.
    
    S’agissant des organisations Exchange locales, vous pouvez également vérifier ces informations dans le composant Utilisateurs et ordinateurs Active Directory.

  - Exécutez la commande suivante pour vérifier que la boîte aux lettres désactivée à laquelle vous voulez connecter un compte utilisateur existe dans la base de données de boîtes aux lettres et qu’il ne s’agit pas d’une boîte aux lettres supprimées (récupérables).
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    Pour pouvoir connecter une boîte aux lettres désactivée, celle-ci doit exister dans la base de données des boîtes aux lettres et la valeur pour la propriété *DisconnectReason* doit être `Disabled`. Si la boîte aux lettres a été purgée de la base de données, la commande ne doit renvoyer aucun résultat.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d’administration Exchange (EAC) pour connecter une boîte aux lettres désactivée

La procédure suivante explique comment connecter une boîte aux lettres d’utilisateur désactivée. Vous pouvez également reconnecter des boîtes aux lettres liées désactivées et des boîtes aux lettres partagées désactivées au compte utilisateur correspondant.

1.  Dans le CAE, accédez à **Destinataires**  \> **Boîtes aux lettres**.

2.  Cliquez sur **Autre**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires"), puis cliquez sur **Se connecter à une boîte aux lettres**.
    
    La liste des boîtes aux lettres déconnectées sur le serveur Exchange sélectionné de votre organisation Exchange doit s’afficher.
    
    > [!NOTE]
    > Cette liste de boîtes aux lettres inclut des boîtes aux lettres désactivées, des boîtes aux lettres supprimées et des boîtes aux lettres supprimées (récupérables).


3.  Cliquez sur la boîte aux lettres désactivée à connecter, puis cliquez sur **Connecter**.

4.  Dans la fenêtre de demande de confirmation de reconnexion de la boîte aux lettres, cliquez sur **Oui**.
    
    Exchange va reconnecter la boîte aux lettres désactivée au compte utilisateur correspondant.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour connecter une boîte aux lettres désactivée

Dans l’environnement de ligne de commande Exchange Management Shell, utilisez la cmdlet **Connect-Mailbox** pour connecter un compte utilisateur à une boîte aux lettres désactivée. Vous devez spécifier le type de boîte aux lettres que vous connectez. L’exemple suivant présente la syntaxe pour la reconnexion de boîtes aux lettres utilisateur, liées et partagées.

Dans cet exemple, nous connectons une boîte aux lettres utilisateur. Le paramètre *Identity* spécifie la boîte aux lettres déconnectée dans la base de données Exchange. Le paramètre *User* indique le compte utilisateur Active Directory auquel la boîte aux lettres doit être reconnectée.

```powershell
Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"
```

Cet exemple connecte une boîte aux lettres liée. Le paramètre *Identity* spécifie la boîte aux lettres déconnectée dans la base de données Exchange. Le paramètre *LinkedMasterAccount* indique le compte utilisateur Active Directory dans la forêt de comptes auquel vous voulez reconnecter la boîte aux lettres. Le paramètre *Alias* spécifie l’alias, il s’agit de la partie de l’adresse de messagerie qui apparaît à gauche du symbole (@), for la boîte aux lettres reconnectée.

    Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia

Dans cet exemple, nous connectons une boîte aux lettres partagée.

    Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared

> [!NOTE]
> Si vous n’incluez pas la paramètre <em>Alias</em>, lorsque vous exécutez la cmdlet <strong>Connect-Mailbox</strong>, la valeur spécifiée dans le paramètre <em>User</em> ou <em>LinkedMasterAccount</em> est utilisée pour créer l’alias de l’adresse de messagerie pour la boîte aux lettre reconnectée.


Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Connect-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997878\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier qu’une boîte aux lettres désactivée a bien été connectée à compte utilisateur, exécutez l’une des actions suivantes :

  - Dans le Centre d’administration Exchange (EAC), cliquez sur **Destinataires**, accédez à la page appropriée au type de boîte aux lettres pour lequel vous avez effectué la reconnexion, cliquez sur **Actualiser**![Icône Actualiser](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icône Actualiser"), puis vérifiez que la boîte aux lettres est répertoriée.

  - Dans le composant Utilisateurs et ordinateurs Active Directory, cliquez avec le bouton droit sur le compte utilisateur pour lequel vous avez désactivé la boîte aux lettres, puis cliquez sur **Propriétés**. Sous l’onglet **Général**, notez que la zone **Courrier électronique** contient l’adresse de messagerie associée à la boîte aux lettres reconnectée.

  - Dans l’environnement de ligne de commande Exchange Management Shell, exécutez la commande suivante.
    
    ```powershell
Get-User <identity>
```
    
    La valeur **UserMailbox** pour la propriété *RecipientType* indique que le compte utilisateur et la boîte aux lettres sont connectés. Vous pouvez également exécuter la cmdlet **Get-Mailbox** pour vérifier que la boîte aux lettres existe.

