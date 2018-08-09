---
title: 'Le nom de domaine complet de l’ordinateur correspond à une strat. de dest.'
TOCTitle: Le nom de domaine complet de l’ordinateur correspond à une stratégie de destinataire_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50479538
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Le nom de domaine complet de l’ordinateur correspond à une stratégie de destinataire\_ServerFQDNMatchesSMTPPolicy

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d'installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car le nom de domaine complet de l'ordinateur local correspond à l'adresse SMTP (Simple Mail Transfer Protocol) d'une stratégie de destinataire.

Le programme d'installation de Microsoft Exchange nécessite que les noms de domaine complets des serveurs d'une organisation Exchange ne correspondent à aucune adresse SMTP des stratégies de destinataire dans la même organisation Exchange.

Si le nom de domaine complet d'un ordinateur correspond à l'adresse SMTP d'une stratégie de destinataire, le courrier ne bascule pas en SMTP et est bloqué dans les files d'attente MTA.

Pour résoudre ce problème, renommez l'ordinateur local. Vous pouvez également supprimer ou renommer la stratégie de destinataire, puis recommencer l'installation de Microsoft Exchange

**Pour renommer l'ordinateur local**

1.  Ouvrez **Système** dans **Panneau de configuration**.

2.  Sous l’onglet **Nom de l’ordinateur**, cliquez sur **Modifier**.

3.  Sous **Nom de l’ordinateur**, entrez un nouveau nom pour l’ordinateur, puis cliquez sur **OK**. Vous êtes invité à fournir un nom d'utilisateur et un mot de passe pour renommer l'ordinateur dans le domaine.

4.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés système**. Vous êtes invité à redémarrer votre ordinateur pour appliquer les modifications.

> [!NOTE]
> Si l’ordinateur que vous souhaitez renommer est un contrôleur de domaine, consultez la rubrique sur la modification du nom d’un contrôleur de domaine (<a href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</a>).


**Pour modifier l'adresse SMTP d'une stratégie de destinataire**

1.  Démarrez le Gestionnaire système Exchange.

2.  Cliquez sur **Organisation**, sur **Destinataires**, puis sur **Stratégies de destinataire**.

3.  Double-cliquez sur la stratégie que vous souhaitez modifier.

4.  Cliquez sur l’onglet **Adresses de messagerie**, puis modifiez l’adresse SMTP appropriée

Pour plus d'informations sur les problèmes de nom de stratégie de destinataire, voir l'article 288175 de la Base de connaissances Microsoft sur La stratégie du destinataire ne parvient à trouver le FQDN d’aucun serveur dans l’organisation, notifications d’échec de remise 5.4.8 » ([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052&kbid=288175)).

