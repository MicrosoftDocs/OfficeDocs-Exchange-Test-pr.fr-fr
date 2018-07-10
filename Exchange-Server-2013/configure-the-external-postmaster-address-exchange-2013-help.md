---
title: 'Configuration de l’adresse d’administrateur externe: Exchange 2013 Help'
TOCTitle: Configuration de l’adresse d’administrateur externe
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52062990
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l’adresse d’administrateur externe

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L'adresse d'administrateur externe est utilisée comme expéditeur des messages générés par le système et des notifications envoyées aux expéditeurs externes à votre organisation Microsoft Exchange Server 2013. Un expéditeur externe représente tout expéditeur disposant d'une adresse de messagerie dans un domaine qui n'est pas configuré comme un domaine accepté dans votre organisation.

Par défaut, la valeur du paramètre d'adresse de l'administrateur externe est vide. Cette valeur par défaut entraîne le comportement suivant au sein de votre organisation Exchange :

  - l'adresse d'administrateur externe est postmaster@\<*domaine accepté par défaut*\> pour tous les serveurs de boîtes aux lettres et serveurs de transport Edge abonnés.

  - Cette adresse d'administrateur externe est postmaster@\<*Edge Transport server FQDN*\> pour tous les serveurs de transport Edge non abonnés.

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Configuration du transport » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Quand vous configurez une adresse d'administrateur externe personnalisée, la valeur s'applique à tous les serveurs de boîtes aux lettres Exchange 2013 et à tous les serveurs de transport Hub Exchange 2010 dans votre organisation Exchange. Toutefois, cette valeur n'est pas répliquée sur les serveurs de transport Edge. Si vous spécifiez une valeur personnalisée pour l'adresse d'administrateur externe, vous devez configurer manuellement la valeur d'adresse d'administrateur externe sur les serveurs de transport Edge.

  - Si vous disposez de serveurs de transport Edge ou de serveurs de transport Hub Exchange 2007 dans votre organisation, vous devez configurer l'adresse d'administrateur externe personnalisée sur chacun de ces serveurs à l'aide de la cmdlet **Set-TransportServer**. Pour plus d'informations, consultez la rubrique [Gestion de l'adresse d'administrateur externe](https://go.microsoft.com/fwlink/?linkid=279922).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour configurer l'adresse d'administrateur externe

1.  Dans le CAE, accédez à l'onglet **Flux de messagerie** \> **Connecteurs de réception** \> **Autres options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Paramètres de transport de l'organisation** \> **Remise**.

2.  Dans le champ **Adresse d'administrateur externe**, entrez l'adresse de messagerie SMTP, par exemple, `postmaster@contoso.com`. Si vous souhaitez rétablir l'adresse d'administrateur externe par défaut, supprimez la valeur existante de manière à laisser le champ vierge.

3.  Lorsque vous avez terminé, cliquez sur **Enregistrer**.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer l'adresse d'administrateur externe

Pour configurer l'adresse d'administrateur externe, utilisez la syntaxe suivante.

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

Par exemple, pour définir l'adresse d'administrateur externe sur `postmaster@contoso.com`, exécutez la commande suivante :

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

Pour renvoyer l'adresse d'administrateur externe par défaut, exécutez la commande suivante :

    Set-TransportConfig -ExternalPostmasterAddress $null

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré l'adresse d'administrateur externe, procédez comme suit :

1.  Exécutez la commande suivante sur un serveur de boîtes aux lettres pour vérifier la valeur de l'adresse d'administrateur externe :
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  À partir d'un compte de messagerie externe, envoyez un message à votre organisation Exchange qui générera une notification d'état de remise. Par exemple, vous pouvez configurer une règle de transport chargée d'envoyer une notification d'échec de remise pour un message en provenance de cet expéditeur qui contient des mots clés spécifiques. Vérifiez que l'adresse de messagerie de l'expéditeur dans la notification d'état de remise correspond à la valeur que vous avez spécifiée.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

