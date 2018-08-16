---
title: 'Créer une boîte aux lettres de découverte: Exchange 2013 Help'
TOCTitle: Créer une boîte aux lettres de découverte
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50479074
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Créer une boîte aux lettres de découverte

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Le programme d’installation de Microsoft Exchange Server 2013 crée par défaut une boîte aux lettres de découverte. Dans Exchange Online, une boîte aux lettres de découverte est également créée par défaut. Les boîtes aux lettres de découverte servent de boîtes aux lettres cibles pour les recherches [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md) dans le Centre d’administration Exchange (CAE). Vous pouvez créer des boîtes aux lettres de découverte supplémentaires si nécessaire. Une fois que vous avez créé une boîte aux lettres de découverte, vous devez attribuer des autorisations d’accès total aux utilisateurs concernés afin qu’ils puissent accéder aux résultats de recherche eDiscovery (découverte électronique) qui sont copiés dans la boîte aux lettres de découverte.

> [!CAUTION]
> Une fois que le gestionnaire de découverte a copié les résultats d’une recherche eDiscovery dans une boîte aux lettres de découverte, la boîte aux lettres peut contenir des informations sensibles. Nous vous conseillons de contrôler l’accès aux boîtes aux lettres de découverte et de vous assurer que seuls des utilisateurs autorisés peuvent y accéder.


Pour plus d’informations, voir [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Création de boîtes aux lettres de découverte » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Les boîtes aux lettres de découverte présentent un quota de stockage de 50 gigaoctets (Go). Ce quota de stockage ne peut pas être augmenté.

  - Vous ne pouvez pas utiliser le CAE pour créer une boîte aux lettres de découverte ou attribuer des autorisations pour y accéder. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell. Dans Office 365, utilisez Remote PowerShell connecté à votre organisation Exchange Online.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Étape 1 (facultatif) : Connexion à Exchange Online à l’aide de Remote PowerShell

Vous devez uniquement effectuer cette étape si vous possédez une organisation Exchange Online ou Office 365. Si vous possédez une organisation Exchange Server 2013, passez à l’étape suivante et exécutez la commande dans Environnement de ligne de commande Exchange Management Shell.

1.  Sur votre ordinateur local, ouvrez Windows PowerShell et exécutez la commande suivante.
    
        $UserCredential = Get-Credential
    
    Dans la boîte de dialogue **Demande d’informations d’identification Windows PowerShell**, saisissez le nom d’utilisateur et le mot de passe d’un compte d’administrateur global Office 365, puis cliquez sur **OK**.

2.  Exécutez la commande suivante.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Exécutez la commande suivante.
    
        Import-PSSession $Session

4.  Pour vérifier que vous êtes connecté à votre organisation Exchange Online, exécutez la commande suivante pour obtenir la liste de toutes les boîtes aux lettres de votre organisation.
    
        Get-Mailbox

Pour plus d’informations ou si vous rencontrez des problèmes pour vous connecter à votre organisation Exchange Online, consultez la rubrique [Connexion à Exchange Online à l’aide de Remote PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Étape 2 : Créer une boîte aux lettres de découverte

Cet exemple de code permet de créer une boîte aux lettres de découverte nommée SearchResults.

    New-Mailbox -Name SearchResults -Discovery 

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [New-Mailbox](https://technet.microsoft.com/fr-fr/library/aa997663\(v=exchg.150\)).

Pour afficher la liste de toutes les boîtes aux lettres de découverte d’une organisation Exchange, exécutez la commande suivante :

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123685\(v=exchg.150\)).

## Étape 3 : Attribuer des autorisations d’accès à une boîte aux lettres de découverte

Vous devez attribuer explicitement les autorisations nécessaires aux utilisateurs ou aux groupes pour qu’ils puissent ouvrir une boîte aux lettres de découverte créée par vous. Utilisez la syntaxe suivante pour attribuer des autorisations à un utilisateur ou à un groupe afin qu’ils puissent ouvrir une boîte aux lettres de découverte et visualiser les résultats de la recherche :

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

Par exemple, la commande suivante attribue l’autorisation d’accès total au groupe Gestionnaires de litiges, afin que les membres du groupe puissent ouvrir la boîte aux lettres de découverte des litiges Fabrikam.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Add-MailboxPermission](https://technet.microsoft.com/fr-fr/library/bb124097\(v=exchg.150\)).

## Plus d’informations

  - Par défaut, seuls les membres du groupe de rôles Gestion de la découverte ont une autorisation d’accès total à la boîte aux lettres de recherche de découverte par défaut. Vous devrez attribuer explicitement l’autorisation d’accès total au groupe de rôles Gestion de la découverte si vous souhaitez que ses membres puissent ouvrir une boîte aux lettres de découverte que vous avez créée.

  - Bien que visibles dans les listes d’adresses Exchange, les utilisateurs ne peuvent pas envoyer de messages électroniques à une boîte aux lettres de découverte. La remise du courrier électronique aux boîtes aux lettres de découverte est bloquée par des restrictions de remise. Cela permet de préserver l’intégrité des résultats de recherche copiés dans une boîte aux lettres de découverte.

  - Une boîte aux lettres de découverte ne peut pas être utilisée pour d’autres tâches ou convertie en un autre type de boîte aux lettres.

  - Vous pouvez supprimer une boîte aux lettres de découverte comme tout autre type de boîte aux lettres.

