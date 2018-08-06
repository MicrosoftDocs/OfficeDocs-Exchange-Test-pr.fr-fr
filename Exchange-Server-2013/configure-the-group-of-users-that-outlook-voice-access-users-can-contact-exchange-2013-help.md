---
title: "Config. du groupe d’utilisateurs que les utilisateurs OVA peuvent contacter | Microsoft Docs"
TOCTitle: Configurer le groupe d'utilisateurs que les utilisateurs Outlook Voice Access peuvent contacter
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50478843
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer le groupe d'utilisateurs que les utilisateurs Outlook Voice Access peuvent contacter

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-11-09_

Vous pouvez préciser les utilisateurs pouvant recevoir des appels transférés ou des messages vocaux parmi les utilisateurs de Outlook Voice Access. Par défaut, l’option **Dans ce plan de commutation seulement** est sélectionnée. Vous pouvez modifier ce paramètre pour permettre aux utilisateurs de Outlook Voice Access de transférer des appels ou d'envoyer des messages vocaux aux utilisateurs de toute l'organisation, à un standard automatique de messagerie unifiée ou à un numéro d'extension spécifique.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, voir [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'effectuer ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le CAE (Centre d’administration Exchange) pour configurer le groupe d'utilisateurs que les utilisateurs de Outlook Voice Access peuvent contacter

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage de liste, sélectionnez le plan de numérotation de messagerie unifiée que vous souhaitez modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Transférer et rechercher**, sous **Autoriser les appelants à rechercher des utilisateurs par leur nom ou leur alias**, sélectionnez l'une des options suivantes :
    
      - **Dans ce plan de numérotation uniquement**   Utilisez cette option pour permettre aux utilisateurs de Outlook Voice Access qui appellent un numéro Outlook Voice Access de localiser et contacter des utilisateurs appartenant au même plan de numérotation.
    
      - **Dans toute l'organisation**   Utilisez cette option pour permettre aux utilisateurs de Outlook Voice Access qui appellent un numéro Outlook Voice Access de localiser et contacter toute personne au sein de l'organisation. Cela inclut tous les utilisateurs à extension boîte aux lettres.
    
      - **Uniquement sur ce standard automatique**   Utilisez cette option pour permettre aux utilisateurs de Outlook Voice Access qui appellent un numéro Outlook Voice Access de se connecter à un standard automatique spécifique. Vous devez créer le standard automatique avant de le spécifier ici. Ainsi, les utilisateurs de Outlook Voice Access peuvent être transférés vers un autre standard automatique. Le standard automatique que vous choisissez ici peut être un standard automatique à reconnaissance vocale ou non.
    
      - **Uniquement pour cette extension**   Utilisez cette option pour permettre aux utilisateurs de Outlook Voice Access de se connecter à un numéro d'extension que vous indiquez. L'extension ne peut comporter que des caractères numériques. Le nombre de chiffres que vous définissez dans ce champ doit correspondre au nombre de chiffres présents dans les numéros de poste qui sont configurés sur le plan de numérotation de messagerie unifiée.

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer le groupe d'utilisateurs que les utilisateurs de Outlook Voice Access peuvent contacter

Dans cet exemple, le groupe d'utilisateurs que les utilisateurs de Outlook Voice Access peuvent contacter pour un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` est configuré pour toute l'organisation.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

Dans cet exemple, le groupe d'utilisateurs que les utilisateurs de Outlook Voice Access peuvent contacter pour un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` est configuré pour le `DialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

