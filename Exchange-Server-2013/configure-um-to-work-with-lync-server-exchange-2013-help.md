---
title: 'Configurer la messagerie unifiée pour qu’elle fonctionne avec Lync Server: Exchange 2013 Help'
TOCTitle: Configurer la messagerie unifiée pour qu’elle fonctionne avec Lync Server
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52062948
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer la messagerie unifiée pour qu’elle fonctionne avec Lync Server

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-06-11_

Lorsque vous intégrez Microsoft Lync Server à la messagerie unifiée Exchange, vous devez exécuter le script ExchUcUtil.ps1 dans l’environnement Shell. Le script ExchUcUtil.ps1 effectue les opérations suivantes :

  - Il crée une passerelle IP de messagerie unifiée pour chaque pool Lync Server.
    
    > [!NOTE]
    > Le script ExchUcUtil.ps1 crée une ou plusieurs passerelles IP de messagerie unifiée. Vous devez désactiver les appels sortants sur toutes les passerelles IP de messagerie unifiée à l’exception de celle que le script a créée. Ceci inclut la désactivation des appels sortants sur les passerelles IP de messagerie unifiée qui ont été créées avant l’exécution du script. Pour désactiver les appels sortants sur une passerelle IP de messagerie unifiée, consultez la rubrique <a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Désactiver les appels sortants sur les passerelles IP de messagerie unifiée</a>.


  - Il crée un groupement de postes de messagerie unifiée pour chaque passerelle IP de messagerie unifiée. L’identificateur de pilote de chaque groupement de postes spécifie le plan de numérotation avec un URI SIP de messagerie unifiée utilisé par le pool frontal Lync Server ou le serveur Standard Edition qui est associé à la passerelle IP de messagerie unifiée.

  - Il donne l’autorisation à Lync Server de lire les objets conteneurs de messagerie unifiée Active Directory, tels que les plans de numérotation de messagerie unifiée, les standards automatiques, les passerelles IP de messagerie unifiée et les groupements de postes de messagerie unifiée.

> [!NOTE]
> Chaque forêt de messagerie unifiée doit être configurée pour approuver la forêt dans laquelle Lync Server 2013 est déployé, et vice versa. Si la messagerie unifiée Exchange est installée dans plusieurs forêts, les étapes d’intégration d’Exchange Server doivent être effectuées pour chaque forêt de messagerie unifiée ou vous devrez spécifier le domaine Lync Server. Par exemple, <em>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</em>.


Pour découvrir des tâches de gestion supplémentaires liées à l’intégration de Lync Server et de la messagerie unifiée, consultez la rubrique [Présentation du déploiement de la messagerie unifiée Exchange 2013 et de Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 2 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Cmdlets d’autorisations » dans la rubrique [Cmdlets Exchange 2013](https://technet.microsoft.com/fr-fr/library/bb124413\(v=exchg.150\)).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Utiliser l’environnement Shell pour exécuter le script ExchUcUtil.ps1

Exécutez le script ExchUcUtil.ps1 sur n’importe quel serveur Exchange de votre organisation qui est dans la même topologie que Microsoft Lync Server. Vous pouvez exécuter le script à partir d’un serveur de boîtes aux lettres en utilisant l’environnement Shell ou vous pouvez l’exécuter à l’aide de Remote Windows PowerShell sur un serveur d’accès au client. Si vous exécutez le script sur un serveur d’accès au client de votre organisation, le serveur d’accès au client redirigera via proxy la session Remote Windows PowerShell vers un serveur de boîtes aux lettres dans l’organisation.

> [!NOTE]
> Le script ExchUcUtil.ps1 crée une ou plusieurs passerelles IP de messagerie unifiée. Vous devez désactiver les appels sortants sur toutes les passerelles IP de messagerie unifiée à l’exception de celle que le script a créée. Ceci inclut la désactivation des appels sortants sur les passerelles IP de messagerie unifiée qui ont été créées avant l’exécution du script. Pour désactiver les appels sortants sur une passerelle IP de messagerie unifiée, consultez la rubrique <a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Désactiver les appels sortants sur les passerelles IP de messagerie unifiée</a>.


> [!NOTE]
> Vous devez avoir les autorisations du rôle Gestion de l’organisation Exchange ou être membre du groupe de sécurité Administrateurs d’organisation Exchange pour exécuter le script.


1.  Ouvrez l’environnement de ligne de commande Exchange Management Shell.

2.  À l’invite `C:\Windows\System32`, tapez **cd “\<lettre de lecteur\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1”**, puis appuyez sur Entrée.

## Comment savoir si cela a fonctionné ?

Pour vérifier que le script ExchUcUtul.ps1 a été exécuté correctement, procédez comme suit :

  - Utilisez la cmdlet **Get-UMIPGateway** ou le CAE pour voir la nouvelle passerelle IP de messagerie unifiée ou des passerelles qui ont été créées.

  - Utilisez la cmdlet **Get-UMHuntGroup** ou le CAE pour voir le nouveau groupement de postes de messagerie unifiée ou des groupes qui ont été créés.

