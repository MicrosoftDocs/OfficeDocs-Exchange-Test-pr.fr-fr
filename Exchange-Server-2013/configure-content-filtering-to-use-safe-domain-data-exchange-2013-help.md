---
title: 'Config. filtrage de cont. pr données de domaine autorisé: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurer le filtrage de contenu pour utiliser les données de domaine autorisé
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59634335
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le filtrage de contenu pour utiliser les données de domaine autorisé

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-12-16_

Les données de domaine autorisé correspondent à un domaine entier (par exemple, @contoso.com) stocké dans la liste des expéditeurs autorisés d’un utilisateur. Par défaut, l’agent de filtrage du contenu n’utilise pas les données de domaine autorisé pour identifier les expéditeurs autorisés à contourner le filtrage de contenu.

Ce paramètre par défaut permet de réduire la quantité de courrier indésirable remis à votre organisation. Par exemple, un utilisateur peut ajouter le domaine d’un grand fournisseur de messagerie à sa liste d’expéditeurs autorisés. Si ce domaine est souvent employé ou usurpé par des expéditeurs de courrier indésirable, et si le filtrage de contenu est configuré afin d’utiliser les données de domaine autorisé pour marquer le message comme autorisé, les messages de tous les expéditeurs de ce domaine seront remis aux destinataires dans votre organisation.

Dans la plupart des cas, nous vous recommandons de ne pas modifier le paramètre par défaut. Toutefois, vous pouvez configurer le stockage des données de domaine autorisé des utilisateurs dans Active Directory et leur emploi par le filtre de contenu afin de marquer les messages comme autorisés. Pour ce faire, vous devez modifier le fichier de configuration de l’application XML MSExchangeMailboxAssistants.exe.config associé au service Assistants de boîte aux lettres Microsoft Exchange, comme décrit plus loin dans cette rubrique. Lorsque vous modifiez cette configuration, les données de domaine autorisé sont hachées et stockées dans l’attribut d’objet **msExchSafeSenderHash** de chaque utilisateur dans Active Directory, dans le cadre d’une agrégation de liste fiable. L’agent de filtrage de contenu peut ensuite utiliser les données de domaine autorisé pour marquer les messages provenant d’expéditeurs de ces domaines comme sûrs. Pour plus d’informations sur l’agrégation de liste fiable, voir [Agrégation de listes fiables](safelist-aggregation-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 10 minutes

  - Les autorisations Exchange ne s’appliquent pas aux procédures de cette rubrique. Ces procédures sont exécutées dans le système d’exploitation du serveur Exchange.

  - Les modifications que vous enregistrez dans le fichier MSExchangeMailboxAssistants.exe.config sont appliquées après le redémarrage du service Assistants de boîte aux lettres de Microsoft Exchange.

  - Les paramètres par serveur personnalisés de vos fichiers de configuration d’application XML Exchange, par exemple les fichiers web.config sur les serveurs d’accès au client ou le fichier EdgeTransport.exe.config sur les serveurs de boîtes aux lettres, seront remplacés lors de l’installation d’une mise à jour cumulative Exchange. Veuillez enregistrer ces informations pour configurer à nouveau votre serveur après l’installation. Vous devez reconfigurer ces paramètres après avoir installé une mise à jour cumulative Exchange.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Servez-vous d’une invite de commandes pour configurer le filtrage de contenu de manière à utiliser des données de domaine autorisé.

1.  Dans la fenêtre d’invite de commandes, ouvrez le fichier MSExchangeMailboxAssistants.exe.config dans le Bloc-notes en exécutant la commande suivante :
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  Localisez la clé *\</appsettings\>* à la fin du fichier et collez la clé suivante avant la clé *\</appsettings\>* :
    
        <add key="IncludeSafeDomains" value="true" />

3.  Quand vous avez terminé, enregistrez et fermez le fichier MSExchangeMailboxAssistants.exe.config.

4.  Redémarrez le service Assistants de boîte aux lettres de Microsoft Exchange en exécutant la commande suivante :
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré le filtrage de contenu de manière à utiliser des données de domaine autorisé, procédez comme suit :

1.  Vérifiez que l’ajout d’un domaine à la liste des expéditeurs autorisés d’un utilisateur dans Outlook met à jour l’attribut **msExchSafeSenderHash** de l’utilisateur dans Active Directory. Pour ce faire, consultez l’attribut dans ADSIEdit.exe ou LDP.exe, ouvrez la boîte aux lettres de l’utilisateur dans Outlook, ajoutez un domaine à la liste des expéditeurs autorisés, exécutez la commande `Update-Safelist <username>` et vérifiez que la valeur d’origine et la valeur actuelle de l’attribut **msExchSafeSenderHash** sont différentes.

2.  Après avoir vérifié que les données de domaine autorisé sont stockées dans Active Directory, envoyez un message de test à partir d’un expéditeur externe de ce domaine à un utilisateur de votre organisation. Vérifiez que le message est marqué comme autorisé en examinant les champs d’en-tête anti-programme malveillant dans l’en-tête du message.

