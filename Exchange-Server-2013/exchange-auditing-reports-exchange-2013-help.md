---
title: 'Rapports d’audit Exchange: Exchange 2013 Help'
TOCTitle: Rapports d’audit Exchange
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50477225
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rapports d’audit Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Utilisez l’enregistrement d’audit pour résoudre des problèmes de configuration en suivant les modifications spécifiques effectuées par les administrateurs et vous aider à respecter les exigences réglementaires, de conformité et en matière de litiges. Microsoft Exchange fournit deux types d’enregistrements d’audit :

  - *Enregistrement d’audit d’administrateur* enregistre toute action, basée sur une cmdlet d’Exchange Management Shell, effectuée par un administrateur. Cela peut vous aider à résoudre des problèmes de configuration ou à identifier la cause de problèmes de sécurité ou de conformité. Dans Exchange Online, les actions effectuées par les administrateurs Microsoft et les administrateurs délégués sont également enregistrées.

  - *Enregistrement d’audit des boîtes aux lettres* enregistre chaque accès à une boîte aux lettres par un administrateur, un utilisateur délégué ou son propriétaire. Vous pouvez ainsi identifier les personnes ayant accédé à une boîte aux lettres et ce qu’elles y ont fait.

Cette rubrique présente les points suivants :

  - Exporter des journaux d’audit

  - Exécuter des rapports d’audit

  - Configurer l’enregistrement d’audit
    
      - Activer l’enregistrement d’audit de boîte aux lettres
    
      - Donner aux utilisateurs l’accès aux rapports d’audit
    
      - Configurer Outlook Web App pour autoriser les pièces jointes XML

## Exporter des journaux d’audit

Dans la page **Gestion de la conformité** \> **Audit** du Centre d’administration Exchange (CAE), vous pouvez rechercher et exporter des entrées à partir du journal d’audit de l’administrateur et du journal d’audit de la boîte aux lettres.

  - **Exporter le journal d’audit de l’administrateur**   Toute action exécutée par un administrateur qui est basée sur une cmdlet de l’environnement de ligne de commande Exchange Management Shell et qui ne commence pas par les verbes **Get**, **Search** ou **Test** est enregistrée dans le journal d’audit de l’administrateur. Les entrées de journal d’audit incluent l’applet de commande exécutée, le paramètre et les valeurs utilisées avec l’applet de commande, et quand l’opération a réussi. Vous pouvez rechercher et exporter des entrées à partir du journal d’audit de l’administrateur. Lorsque vous exportez vos résultats de la recherche, Microsoft Exchange les enregistre dans un fichier XML et l’inclut en pièce jointe dans un message électronique. Pour plus d’informations, consultez :
    
      - [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [Afficher et exporter le journal d’audit de l’administrateur externe](https://technet.microsoft.com/fr-fr/library/dn505728\(v=exchg.150\))
    
    > [!NOTE]
    > Par défaut, les entrées du journal d’audit de l’administrateur sont conservées pendant 90 jours. Lorsqu’une entrée a dépassé le seuil de 90 jours, elle est supprimée. Ce paramètre ne peut pas être modifié dans une organisation informatique. Toutefois, il peut être modifié dans une organisation Exchange locale à l’aide de la cmdlet <strong>Set-AdminAuditLog</strong>.


  - **Exporter les journaux d’audit de boîte aux lettres**   Lorsque l’enregistrement d’audit des boîtes aux lettres est activé pour une boîte aux lettres, Microsoft Exchange stocke un enregistrement des actions effectuées sur les données de la boîte aux lettres par les non-propriétaires, dans le journal d’audit de la boîte aux lettres stocké dans un dossier caché dans la boîte aux lettres faisant l’objet de l’audit. L’enregistrement d’audit des boîtes aux lettres peut également être configuré pour enregistrer les actions du propriétaire. Les entrées de ce journal indiquent qui a accédé à la boîte aux lettres et quand, les actions effectuées et si l’action a réussi. Lorsque vous recherchez des entrées dans le journal d’audit de la boîte aux lettres et que vous les exportez, Microsoft Exchange enregistre les résultats de la recherche dans un fichier XML et l’inclut en pièce jointe dans un message électronique. Pour plus d’informations, consultez la rubrique [Exporter les journaux d’audit de boîte aux lettres](export-mailbox-audit-logs-exchange-2013-help.md).

## Exécuter des rapports d’audit

Lorsque vous exécutez l’un des rapports suivants sous l’onglet **Audit** du CAE, les résultats sont affichés dans le volet d’informations du rapport.

  - **Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires**   Utilisez ce rapport pour rechercher les boîtes aux lettres auxquelles une personne autre que le propriétaire de la boîte aux lettres a accédé. Pour plus d’informations, consultez la rubrique [Exécuter un rapport d’accès aux boîtes aux lettres par des non-propriétaires](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Exécuter un rapport de groupe de rôles d’administrateur**   Utilisez ce rapport pour rechercher des modifications apportées aux groupes de rôles d’administrateur. Pour plus d’informations, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Exécuter un rapport de découverte et de blocage sur place**   Utilisez ce rapport pour rechercher les boîtes aux lettres pour lesquelles un blocage sur place a été activé ou annulé. Pour plus d’informations, voir :
    
      - [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md)

  - **Rapport de mise en attente pour litige par boîte aux lettres**   Utilisez ce rapport pour rechercher les boîtes aux lettres pour lesquelles une mise en attente pour litige a été activée ou annulée. Pour plus d’informations, consultez :
    
      - [Exécuter un rapport de suspension pour litige par boîte aux lettres](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Placement d’une boîte aux lettres en conservation pour litige](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Exécuter le rapport du journal d’audit de l’administrateur**   Utilisez ce rapport pour afficher les entrées du journal d’audit de l’administrateur. Au lieu d’exporter le journal d’audit de l’administrateur, dont la réception par courrier électronique peut prendre jusqu’à 24 heures, vous pouvez exécuter ce rapport dans le CAE. Ce rapport enregistre les modifications de configuration apportées par les administrateurs de votre organisation. Jusqu’à 5 000 entrées peuvent s’afficher sur plusieurs pages. Pour affiner la recherche, vous pouvez spécifier une plage de dates. Pour plus d’informations, consultez :
    
      - [Consulter le journal d’audit de l’administrateur](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md)

  - **Exécuter le rapport du journal d’audit de l’administrateur externe**   Ce rapport est disponible uniquement dans Exchange Online et Exchange Online Protection. Les actions effectuées par les administrateurs Microsoft ou les administrateurs délégués sont enregistrées dans le journal d’audit de l’administrateur. Utilisez le rapport du journal d’audit de l’administrateur externe pour rechercher et afficher les actions que des administrateurs extérieurs à votre organisation ont effectuées sur la configuration de votre organisation Exchange Online. Pour plus d’informations, consultez la rubrique [Afficher et exporter le journal d’audit de l’administrateur externe](https://technet.microsoft.com/fr-fr/library/dn505728\(v=exchg.150\)).

## Configurer l’enregistrement d’audit

Avant de pouvoir exécuter des rapports d’audit et exporter des journaux d’audit, vous devez configurer l’enregistrement d’audit pour votre organisation.

## Activer l’enregistrement d’audit de boîte aux lettres

Vous devez activer l’enregistrement d’audit de boîte aux lettres pour chaque boîte aux lettres pour laquelle vous souhaitez exécuter un rapport d’accès aux boîtes aux lettres par un non-propriétaire. Si l’enregistrement d’audit de boîte aux lettres n’est pas activé pour une boîte aux lettres, vous n’obtiendrez pas de résultats lorsque vous exécuterez un rapport ou exporterez le journal d’audit de la boîte aux lettres.

Pour activer l’enregistrement d’audit de boîte aux lettres pour une boîte aux lettres unique, exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Pour activer l’audit de boîte aux lettres pour toutes les boîtes aux lettres des utilisateurs de votre organisation, exécutez les commandes suivantes.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

Pour plus d’informations sur la configuration des actions enregistrées, voir :

  - **Exchange 2013**   [Activer ou désactiver l’enregistrement d’audit pour une boîte aux lettres](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [Activer l’audit de boîte aux lettres dans Office 365](https://go.microsoft.com/fwlink/p/?linkid=626109)

## Donner aux utilisateurs l’accès aux rapports d’audit

Par défaut, les administrateurs peuvent accéder et exécuter tous les rapports dans la page Audit du CAE. Toutefois, les autres utilisateurs, tels qu’un gestionnaire d’enregistrements ou le personnel juridique, doivent avoir les autorisations nécessaires.

La façon la plus facile pour donner l’accès aux utilisateurs consiste à les ajouter au groupe de rôles Gestion des enregistrements. Vous pouvez également utiliser l’environnement de ligne de commande Exchange Management Shell pour donner à un utilisateur l’accès à la page **Audit** dans le CAE en lui attribuant le rôle Journaux d’audit.

## Ajouter un utilisateur au groupe de rôles Gestion des enregistrements

1.  Accédez à **Autorisations**\>**Rôles d’administrateur**.

2.  Dans la liste des groupes de rôles, cliquez sur **Gestion des enregistrements**, puis sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Sous **Membres**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans la boîte de dialogue **Sélectionner des membres**, sélectionnez l’utilisateur. Vous pouvez rechercher un utilisateur en tapant une partie ou la totalité d’un nom complet, puis en cliquant sur **Rechercher**![Icône Recherche](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Icône Recherche"). Vous pouvez également trier la liste en cliquant sur l’en-tête de colonne **Nom** ou **Nom complet**.

5.  Cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sur **OK** pour revenir à la page du groupe de rôles.

6.  Cliquez sur **Enregistrer** pour enregistrer la modification apportée au groupe de rôles.

Dans le volet d’informations, l’utilisateur est répertorié sous **Membres** et peut accéder à la page Audit dans le CAE, exécuter des rapports d’audit et exporter des journaux d’audit.

## Attribuer le rôle Journaux d’audit à un utilisateur

Exécutez la commande suivante pour attribuer le rôle Journaux d’audit à un utilisateur.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

Ceci permet à l’utilisateur de sélectionner **Gestion de la conformité** \>**Audit** dans le CAE pour exécuter l’un des rapports. L’utilisateur peut également exporter le journal d’audit de la boîte aux lettres, et exporter et afficher le journal d’audit de l’administrateur.

> [!NOTE]
> Pour permettre à un utilisateur d’exécuter des rapports d’audit mais pas d’exporter des journaux d’audit, utilisez la commande précédente pour attribuer le rôle Journaux d’audit en affichage seul.


## Configurer Outlook Web App pour autoriser les pièces jointes XML

Lorsque vous exportez le journal d’audit de la boîte aux lettres ou le journal d’audit de l’administrateur, Microsoft Exchange joint le journal d’audit, qui est un fichier XML à un message électronique. Cependant, Outlook Web App bloque les pièces jointes XML par défaut. Si vous voulez utiliser Outlook Web App pour accéder à ces journaux d’audit, vous devez configurer Outlook Web App pour autoriser les pièces jointes XML.

Exécutez la commande suivante pour autoriser les pièces jointes XML dans Outlook Web App.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

