---
title: 'Form. d’adress. SMTP non pris en charge_SMTPAddressLiteral: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Format d’adressage SMTP non pris en charge_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50478925
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Format d’adressage SMTP non pris en charge\_SMTPAddressLiteral

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-09_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 et Exchange Server 2010 ne peut pas poursuivre son exécution car la stratégie de destinataire spécifiée utilise un format d’adresse SMTP (Simple Mail Transfer Protocol) non pris en charge.

Pour installer Exchange 2007 et Exchange 2010, aucune adresse SMTP utilisée pour les stratégies d’adresses électroniques ne doit contenir de littéral d’adresse IP, par exemple : *user@\[10.10.1.1\]*.

Pour résoudre ce problème, modifiez la valeur de l'adresse SMTP dans la stratégie de destinataire afin qu'elle ne contienne pas de litéral d'adresse IP. Remplacez les crochets (\[\]) et les chiffres (10.10.1.1) du littéral de l’adresse IP par le format DNS (Domain Name System), par exemple : *user@contoso.com*, puis recommencez la procédure d’installation d’Exchange.

Pour plus d’informations sur la gestion des stratégies de destinataire dans Exchange Server 2007, voir la rubrique sur la gestion des stratégies d’adresse de messagerie ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653)).

Pour plus d’informations sur la gestion des stratégies de destinataire dans Exchange Server 2010, consultez la rubrique sur la gestion des stratégies d’adresse de messagerie ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519)).

