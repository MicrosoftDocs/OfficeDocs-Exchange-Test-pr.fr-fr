---
title: 'Config. des param. de blocage du courr. ind. sur les BAL: Exchange 2013 Help'
TOCTitle: Configurer les paramètres de blocage du courrier indésirable sur les boîtes aux lettres
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50478617
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer les paramètres de blocage du courrier indésirable sur les boîtes aux lettres

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-11-17_

Vous pouvez configurer des paramètres anti-courrier indésirable spécifiques sur des boîtes aux lettres individuelles qui diffèrent de ceux qui sont appliqués aux autres boîtes aux lettres de votre organisation Exchange. Lorsque vous configurez un paramètre anti-courrier indésirable sur une boîte aux lettres, ce paramètre remplace le paramètre correspondant de filtre du contenu dans l’ensemble de l’organisation ou d’anti-courrier indésirable de configuration de l’organisation.

> [!NOTE]
> Le 1er novembre 2016, Microsoft a cessé de produire des mises à jour des définitions de courrier indésirable pour les filtres SmartScreen dans Exchange et Outlook. Les définitions de courrier indésirable SmartScreen existantes restent en place, mais leur efficacité se dégradera probablement au cours du temps. Pour plus d’informations, voir l’article relatif à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=835894">arrêt de la prise en charge de SmartScreen dans Outlook et Exchange</a>.


## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée de chaque procédure : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Fonctionnalités anti-courrier indésirable » de la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) et entrée « Anti-courrier indésirable » de la rubrique [Autorisations des destinataires](recipients-permissions-exchange-2013-help.md).

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Le comportement de la valeur du seuil SCL du dossier de courrier indésirable diffère de celui des valeurs SCL de suppression, de rejet et de mise en quarantaine. Pour plus d’informations, consultez la rubrique [Niveau de confiance du courrier indésirable](spam-confidence-level-threshold-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utilisation du Shell pour configurer les fonctionnalités de blocage du courrier indésirable sur une seule boîte aux lettres

Utilisez la syntaxe suivante pour configurer les paramètres anti-courrier indésirable pour une boîte aux lettres unique.

```powershell
Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>
```

Dans cet exemple, nous configurons la boîte aux lettres de Jeff Phillips afin qu’elle contourne tous les filtres anti-courrier indésirable et obtienne des messages correspondant ou excédant un seuil SCL de dossier courrier indésirable de 5 indiqué pour son dossier courrier indésirable dans Microsoft Outlook.

```powershell
Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré les fonctionnalités anti-courrier indésirable sur une boîte aux lettres unique, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*
    ```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utilisation de l’environnement Shell pour configurer les fonctionnalités anti-courrier indésirable sur plusieurs boîtes aux lettres

Utilisez la syntaxe suivante pour configurer tous les paramètres anti-courrier indésirable pour plusieurs boîtes aux lettres.

```powershell
Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>
```

Cet exemple indique comment activer le seuil de mise en quarantaine SCL avec une valeur de 7 sur toutes les boîtes aux lettres du conteneur d’utilisateurs dans le domaine Contoso.com.

```powershell
Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré les fonctionnalités anti-courrier indésirable sur plusieurs boîtes aux lettres, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*
    ```

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

## Utilisez l’environnement Shell pour configurer le seuil de courrier indésirable pour toutes les boîtes aux lettres de votre organisation

Exécutez la commande suivante :

```powershell
Set-OrganizationConfig -SCLJunkThreshold <Integer>
```

Dans cet exemple, nous indiquons comment définir le seuil de courrier indésirable de l’organisation à 5.

```powershell
Set-OrganizationConfig -SCLJunkThreshold 5
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré le seuil de courrier indésirable pour toutes les boîtes aux lettres de votre organisation, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-OrganizationConfig | Format-List SCLJunkThreshold
    ```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

