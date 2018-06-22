---
title: 'Création d’une archive informatique pour une boîte aux lettres principale locale dans un déploiement hybride Exchange: Exchange Online Help'
TOCTitle: Création d’une archive informatique pour une boîte aux lettres principale locale dans un déploiement hybride
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253081
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Création d’une archive informatique pour une boîte aux lettres principale locale dans un déploiement hybride Exchange

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2017-01-20_

Dans un déploiement hybride Exchange, vous pouvez configurer une boîte aux lettres principale locale avec une boîte aux lettres d’archivage informatique dans Exchange Online.

Étape 1 : activer une boîte aux lettres d'archivage informatique pour une boîte aux lettres principale locale

Étape 2 : vérifier que la boîte aux lettres d'archivage informatique est créée

(Facultatif) Effectuez une synchronisation d'annuaires

## Avant de commencer

  - L’utilisateur ayant la boîte aux lettres principale locale doit avoir un compte d’utilisateur dans votre organisation Office 365.

  - Le compte d’utilisateur Office 365 doit être attribué à un archivage Exchange Online pour la licence Exchange Server. Les étapes d’attribution d’une licence sont incluses dans les procédures indiquées à l’étape 1.

  - Après avoir activé la boîte aux lettres d’archivage informatique à l’étape 1, la configuration de la boîte aux lettres d’archivage informatique peut prendre jusqu’à 30 minutes. La boîte aux lettres d’archivage informatique est créée par le processus de synchronisation d’annuaires, où Active Directory en local est synchronisé avec Azure Active Directory (Azure AD) dans Office 365. Par défaut, la synchronisation d’annuaires est exécutée toutes les 30 minutes.

## Étape 1 : activer une boîte aux lettres d’archivage informatique pour une boîte aux lettres principale locale

Utilisez une des procédures suivantes pour activer une boîte aux lettres d’archivage informatique pour une boîte aux lettres principale locale. Effectuez ces étapes dans le Centre d’administration Exchange dans votre organisation Exchange locale et dans le Centre d’administration Office 365.

Création d'une boîte aux lettres d'archivage informatique pour un nouvel utilisateur

Création d'une boîte aux lettres d'archivage informatique pour un utilisateur existant

## Création d’une boîte aux lettres d’archivage informatique pour un nouvel utilisateur

1.  Dans le Centre d’administration Exchange de votre organisation locale, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Cliquez sur **Nouveau**![Icône Ajouter](images/Mt791517.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") \> **Boîte aux lettres utilisateur**.

3.  Sur la page **Nouvelle boîte aux lettres utilisateur**, créez une boîte aux lettres pour un utilisateur nouveau ou existant. Pour plus d'informations sur la création d'une boîte aux lettres utilisateur, consultez la rubrique [Création de boîtes aux lettres utilisateur](https://technet.microsoft.com/fr-fr/library/jj991919\(v=exchg.150\)).

4.  Cliquez sur **Plus d’options** pour activer une boîte aux lettres d’archivage informatique.

5.  Sous **Archive**, cliquez sur la case à cocher **Créer une archive sur site pour cet utilisateur**, puis cliquez sur **Archive informatique**. Le nom du domaine qui sera configuré par la boîte aux lettres d’archivage apparaît.
    
    ![Sous Archive, cliquez sur la case à cocher, puis sur Archive en nuage](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "Sous Archive, cliquez sur la case à cocher, puis sur Archive en nuage")  

6.  Cliquez sur **Enregistrer** pour créer la boîte aux lettres et l’archive informatique.
    
    Sur la page **Boîtes aux lettres**, la valeur **Utilisateur (archiver)** est affichée dans la colonne **Type de boîte aux lettres** pour la boîte aux lettres sélectionnée.

7.  La création d’un compte d’utilisateur correspondant dans Office 365 par la synchronisation d’annuaires peut prendre jusqu’à 30 minutes.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Mt589761.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dans le Centre d’administration Office 365, accédez à <strong>Intégrité</strong> &gt; <strong>État de la synchronisation d’annuaires</strong> pour savoir quand la synchronisation d’annuaires s’est produite pour la dernière fois.</td>
    </tr>
    </tbody>
    </table>


8.  Après avoir vérifié que la synchronisation d’annuaires a été réalisée après que vous avez créé la boîte aux lettres locale, dans le Centre d’administration Office 365, accédez à **Utilisateurs** \> **Utilisateurs actifs**, puis sélectionnez le nouveau compte d’utilisateur Office 365 créé pour la nouvelle boîte aux lettres locale.

9.  Sur la page de propriétés utilisateur qui s’affiche, cliquez sur **Modifier** dans la section **Licences des produits**.
    
    ![Cliquez sur Modifier dans le volet d’informations pour attribuer une licence à l’utilisateur sélectionné](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Cliquez sur Modifier dans le volet d’informations pour attribuer une licence à l’utilisateur sélectionné")  

10. Sous le menu déroulant **Emplacement**, sélectionnez un emplacement pour l’utilisateur.

11. Développez la liste des licences Office 365 Entreprise, assignez la licence **Archivage Exchange Online pour Exchange Server**, puis enregistrez les modifications.
    
    Dans la colonne **État** de la liste des utilisateurs, la licence est désormais affectée à l’utilisateur.

12. Une fois encore, patientez jusqu'à 30 minutes le temps que la synchronisation d’annuaires configure une boîte aux lettres d’archivage informatique. Passez à l’étape 2 pour savoir comment vérifier que la boîte aux lettres d’archivage informatique a été créée. Une fois la boîte aux lettres d’archivage créée, l’utilisateur peut y accéder à l’aide d’Outlook ou d’Outlook sur le web.

Retour au début

## Création d’une boîte aux lettres d’archivage informatique pour un utilisateur existant

1.  Dans le Centre d’administration Office 365, accédez à **Utilisateurs** \> **Utilisateurs actifs**, puis sélectionnez le compte d’utilisateur pour lequel créer une boîte aux lettres d’archivage informatique.

2.  Sur la page de propriétés utilisateur qui s’affiche, cliquez sur **Modifier** dans la section **Licences des produits**.
    
    ![Cliquez sur Modifier dans le volet d’informations pour attribuer une licence à l’utilisateur sélectionné](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Cliquez sur Modifier dans le volet d’informations pour attribuer une licence à l’utilisateur sélectionné")  

3.  Sous le menu déroulant **Emplacement**, sélectionnez un emplacement pour l’utilisateur.

4.  Développez la liste des licences Office 365 Entreprise, assignez la licence **Archivage Exchange Online pour Exchange Server**, puis enregistrez les modifications.
    
    Dans la colonne **État** de la liste des utilisateurs, la licence est désormais affectée à l’utilisateur.

5.  Dans le Centre d’administration Exchange de votre organisation locale, accédez à **Destinataires** \> **Boîtes aux lettres**.

6.  Dans la liste des boîtes aux lettres, sélectionnez l’utilisateur auquel vous venez d’attribuer la licence.

7.  Dans le volet d'informations, sous **Archive locale**, cliquez sur **Activer**
    
    ![Cliquez sur Activer dans le volet d’informations pour activer la boîte aux lettres d’archivage de l’utilisateur sélectionné](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "Cliquez sur Activer dans le volet d’informations pour activer la boîte aux lettres d’archivage de l’utilisateur sélectionné")  

8.  Sur la page **Créer une archive sur place**, cliquez sur **Archive informatique**, puis sur **OK**. Le nom du domaine qui sera configuré par la boîte aux lettres d’archivage apparaît.
    
    ![Sur la page Créer une boîte aux lettres d’archivage, cliquez sur Archive en nuage](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "Sur la page Créer une boîte aux lettres d’archivage, cliquez sur Archive en nuage")  
    
    Sur la page **Boîtes aux lettres**, la valeur **Utilisateur (archiver)** est affichée dans la colonne **Type de boîte aux lettres** pour la boîte aux lettres sélectionnée.

9.  La création de la boîte aux lettres d’archivage informatique par la synchronisation d’annuaires peut prendre jusqu’à 30 minutes. Passez à l’étape 2 pour savoir comment vérifier que la boîte aux lettres d’archivage informatique a été créée. Une fois la boîte aux lettres d’archivage créée, l’utilisateur peut y accéder à l’aide d’Outlook ou d’Outlook sur le web.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Mt589761.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dans le Centre d’administration Office 365, accédez à <strong>Intégrité</strong> &gt; <strong>État de la synchronisation d’annuaires</strong> pour savoir quand la synchronisation d’annuaires s’est produite pour la dernière fois.</td>
    </tr>
    </tbody>
    </table>


Retour au début

## Étape 2 : Vérifiez que la boîte aux lettres d’archivage informatique est créée.

Comme indiqué précédemment, il peut y avoir une différence entre le moment où vous activez une boîte aux lettres d’archivage informatique et celui de sa création effective. Cela est dû au fait que la synchronisation d’annuaires doit être exécutée pour créer la boîte aux lettres d’archivage informatique. Voici quelques méthodes permettant de vérifier que la boîte aux lettres d’archivage informatique a été créée.

Dans votre organisation Exchange Online, exécutée la commande PowerShell suivante pour afficher les propriétés associées à la boîte aux lettres de l’utilisateur archive. Pour vous connecter à Exchange Online à l’aide du PowerShell distant, voir [se connecter à Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554).

    Get-MailUser <cloud mail user> | FL *archive*

Les captures d’écran ci-après montrent les propriétés renvoyées lorsque la configuration de la boîte aux lettres d’archivage informatique est en attente et après que la boîte aux lettres d’archivage a été créée.

**Propriétés de l’utilisateur de messagerie avant la configuration de la boîte aux lettres d’archivage informatique par la synchronisation d’annuaires**

![Propriétés de l’utilisateur de la boîte aux lettres en nuage avant la configuration de l’archive informatique](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "Propriétés de l’utilisateur de la boîte aux lettres en nuage avant la configuration de l’archive informatique")

Avant que la synchronisation d’annuaires configure l’archive informatique, la propriété *ArchiveStatus* est définie sur `None`. Notez également que les propriétés *ArchiveGuid* et *ArchiveName* sont vides.

**Propriétés de l’utilisateur de messagerie après la configuration de la boîte aux lettres d’archivage informatique par la synchronisation d’annuaires**

![Propriétés de l’utilisateur de la boîte aux lettres en nuage une fois que l’archive informatique est configurée](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "Propriétés de l’utilisateur de la boîte aux lettres en nuage une fois que l’archive informatique est configurée")

Après que la synchronisation d’annuaires a configuré l’archive informatique, la propriété *ArchiveStatus* est définie sur `Active` et les propriétés *ArchiveGuid* et *ArchiveName* sont remplies. À ce stade, l’utilisateur est en mesure d’accéder à sa boîte aux lettres d’archivage informatique dans Outlook ou Outlook sur le web.

![Les utilisateurs peuvent accéder à leur boîte aux lettres d’archivage en nuage dans Outlook ou Outlook sur le web](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "Les utilisateurs peuvent accéder à leur boîte aux lettres d’archivage en nuage dans Outlook ou Outlook sur le web")

Vous pouvez également exécuter la commande PowerShell suivante dans votre organisation Exchange locale pour afficher les propriétés associées à la boîte aux lettres d’archivage informatique d’un utilisateur.

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**Propriétés de boîte aux lettres locale avant la configuration de la boîte aux lettres d’archivage informatique par la synchronisation d’annuaires**

![Propriétés de la boîte aux lettres avant la configuration de l’archive informatique](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "Propriétés de la boîte aux lettres avant la configuration de l’archive informatique")

Avant que la synchronisation d’annuaires configure l’archive informatique, la propriété *ArchiveStatus* est définie sur `None` et la propriété *ArchiveState* est définie sur `HostedPending`.

**Propriétés de boîte aux lettres locale après la configuration de la boîte aux lettres d’archivage informatique par la synchronisation d’annuaires**

![Propriétés de la boîte aux lettres une fois que l’archive informatique est configurée](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "Propriétés de la boîte aux lettres une fois que l’archive informatique est configurée")

Après que la synchronisation d’annuaires a configuré l’archive informatique, la propriété *ArchiveStatus* est définie sur `Active` et la propriété *ArchiveState* est définie sur `HostedProvisioned`. À ce stade, l’utilisateur est en mesure d’accéder à sa boîte aux lettres d’archivage informatique dans Outlook ou Outlook sur le web.

Retour au début

## (Facultatif) Effectuez une synchronisation d’annuaires

Comme indiqué précédemment, la boîte aux lettres d’archivage informatique est créée par le biais du processus de synchronisation d’annuaires. Par défaut, Active Directory en local est synchronisé avec Azure AD dans Office 365 toutes les 30 minutes. Vous pouvez savoir quand la synchronisation d’annuaires s’est produite pour la dernière fois en accédant à **Intégrité** \> **État de la synchronisation d’annuaires** dans le Centre d’administration Office 365.

Dans certains cas, vous pouvez souhaiter démarrer la synchronisation d’annuaires pour configurer la boîte aux lettres d’archivage informatique avant la prochaine synchronisation planifiée. Vous pouvez effectuer cette opération en exécutant la commande PowerShell suivante sur le serveur où Azure AD Connect est installé.

    Start-ADSyncSyncCycle -PolicyType Delta

Pour plus d’informations, reportez-vous à la rubrique [Planificateur Azure AD Connect Sync](https://go.microsoft.com/fwlink/p/?linkid=836813).

Retour au début

