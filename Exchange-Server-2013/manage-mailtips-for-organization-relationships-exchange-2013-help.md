---
title: 'Gérer les infos-courrier pour les relations de l’org.: Exchange 2013 Help'
TOCTitle: Gérer les infos-courrier pour les relations de l’organisation
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50478404
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer les infos-courrier pour les relations de l’organisation

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour définir les paramètres personnalisés de MailTips entre différentes organisations.

Les relations organisationnelles permettent d’améliorer l’expérience utilisateur des deux organisations, grâce au partage des données de disponibilité, à la configuration du flux de messagerie sécurisé et à l’activation du suivi des messages. Pour plus d’informations sur les relations organisationnelles, voir [Infos-courrier sur les relations de l’organisation](mailtips-over-organization-relationships-exchange-2013-help.md).

Vous disposez de différents paramètres pour contrôler la façon dont les infos-courrier sont utilisées entre deux organisations ayant établi une relation organisationnelle. Les procédures décrites dans cette section illustrent les différents paramètres de contrôle. Dans tous les exemples, contoso.com représente l’organisation locale, alors que online.contoso.com désigne l’organisation distante ; la relation organisationnelle est appelée Contoso Online.

La cmdlet **Set-OrganizationRelationship** permet de configurer ces paramètres.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Infos-courrier » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement Shell pour activer ou désactiver les infos-courrier entre deux organisations

Cet exemple configure la relation organisationnelle de façon à ce que les infos-courrier soient renvoyées aux expéditeurs de l’organisation distante lors de la composition de messages à des destinataires de votre organisation.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

Cet exemple configure la relation organisationnelle de façon à interdire que les infos-courrier soient renvoyées aux expéditeurs de l’organisation distante lors de la composition de messages à des destinataires de votre organisation.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332326\(v=exchg.150\)).

## Utiliser l’environnement Shell pour configurer le renvoi des infos-courrier à l’organisation distante

Pour chaque relation organisationnelle, vous pouvez déterminer l’ensemble d’infos-courrier à renvoyer aux expéditeurs dans l’autre organisation. Cet exemple configure la relation organisationnelle afin que tous les infos-courrier soient renvoyées.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

Cet exemple configure la relation organisationnelle pour renvoyer uniquement les réponses automatiques, les messages dépassant la taille limite, les destinataires restreints et les infos-courrier de boîte aux lettres saturée.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

Cet exemple configure la relation organisationnelle pour qu’aucune info-courrier ne soit renvoyée.

> [!NOTE]
> N’utilisez pas cette méthode pour désactiver les infos-courrier de cette relation. Pour les désactiver, définissez le paramètre <em>MailTipsAccessEnabled</em> sur <code>$false</code>.


    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332326\(v=exchg.150\)).

## Utiliser l’environnement Shell pour configurer un groupe d’utilisateurs spécifique auxquels sont renvoyées des infos-courrier spécifiques

Vous pouvez restreindre le renvoi d’infos-courrier spécifiques à des destinataires à un groupe d’utilisateurs spécifique. Par défaut, lorsque vous activez les infos-courrier pour une relation organisationnelle, les infos-courrier spécifiques à des destinataires suivantes sont renvoyées à tous les utilisateurs :

  - Réponses automatiques

  - Boîte aux lettres saturée

  - Info-courrier personnalisée

Vous pouvez spécifier un groupe d’accès aux infos-courrier pour la relation organisationnelle. Après avoir spécifié un groupe, les infos-courrier spécifiques aux destinataires sont renvoyées uniquement pour les boîtes aux lettres, les contacts de messagerie et les utilisateurs de messagerie appartenant à ce groupe. Cet exemple configure la relation organisationnelle pour renvoyer les infos-courrier spécifiques aux destinataires uniquement pour les membres du groupe ShareMailTips@contoso.com.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-OrganizationRelationship](https://technet.microsoft.com/fr-fr/library/ee332326\(v=exchg.150\)).

