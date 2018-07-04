---
title: 'Test et dépannage à l’aide de l’outil de dépannage de la messagerie unifiée: Exchange 2013 Help'
TOCTitle: Test et dépannage à l’aide de l’outil de dépannage de la messagerie unifiée
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56269363
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Test et dépannage à l’aide de l’outil de dépannage de la messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

L’outil de dépannage de la messagerie unifiée de Microsoft Exchange 2010 est une cmdlet de l’environnement de ligne de commande Exchange Management Shell nommée **Test-ExchangeUMCallFlow**. Vous pouvez utiliser cette cmdlet pour diagnostiquer des erreurs de configuration inhérentes à des scénarios de répondeur automatique et pour tester si la messagerie vocale fonctionne correctement pour les déploiements de messagerie unifiée Microsoft Exchange Server 2010 Service Pack 1 (SP1) (ou ultérieur) locaux et entre différents locaux à la fois. Vous pouvez vous servir de cette cmdlet pour des déploiements avec Microsoft Office Lync Server 2010 (ou ultérieur) ou pour des déploiements de messagerie unifiée avec des passerelles VoIP, des PBX IP ou des contrôleurs de frontière de session.

## Vue d’ensemble

Cette cmdlet émule les appels et exécute un ensemble de tests de diagnostic pour aider les administrateurs locaux à identifier les erreurs de configuration des équipements téléphoniques, les paramètres de messagerie unifiée Exchange 2010 SP1 ou version supérieure, et les problèmes de connectivité entre les déploiements locaux et intersites de la messagerie unifiée Exchange 2010 SP1 ou version supérieure.

Lorsque vous exécutez la cmdlet, elle indique l’origine et les possibles solutions des problèmes détectés. Elle génère également des mesures générales de qualité audio pour diagnostiquer les problèmes dans ce domaine, en relation avec la connectivité réseau (gigue et perte moyenne de paquets). La cmdlet **Test-ExchangeUMCallFlow** prend en charge les tests des composants de messagerie unifiée dans les appels `Secured`, `SIP Secured` et `Unsecured`, et peut être exécutée en mode `Gateway` ou en mode `SIPClient`.

Par défaut, lorsque vous exécutez le service de messagerie UNIFIÉE outil de dépannage, il utilise les informations d’identification qui sont utilisées lorsque vous ouvrez une session sur l’ordinateur. Les informations d’identification utilisées sont celles qui sont spécifiées pour la partie appelante. Vous devez définir ou spécifiez les informations d’identification à utiliser lorsque vous exécutez l’outil Résolution des problèmes de messagerie UNIFIÉE en mode de `SIPClient` . Toutefois, vous n’avez pas besoin de définir les informations d’identification lors de l’exécution de l’outil Résolution des problèmes de messagerie UNIFIÉE en mode de `Gateway` . Si vous utilisez l’outil Résolution des problèmes de messagerie UNIFIÉE en mode de `SIPClient` , les besoins de plusieurs autres Office Communications Server 2007 R2 ou Lync Server et les conditions préalables doivent être remplies. Pour plus d’informations, consultez [liste de vérification : déploiement Office Communications Server 2007 R2 et la messagerie unifiée Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=311961) ou [Liste de contrôle : intégration de la messagerie unifiée d'Exchange 2013 à Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

> [!NOTE]
> La cmdlet <strong>Test-ExchangeUMCallFlow</strong> doit uniquement être utilisée pour tester la fonctionnalité de messagerie vocale d’un serveur de messagerie unifiée Microsoft Exchange Server 2010, sur lequel Exchange 2010 Service Pack 1 (SP1) ou Microsoft Exchange 2013 est installé.


La cmdlet **Test-ExchangeUMCallFlow** peut être installée sur un serveur de messagerie unifiée Exchange 2010 local, sur un serveur de boîtes aux lettres Exchange 2013 ou sur un autre ordinateur 64 bits sur lequel sont exécutés :

  - le système d’exploitation Windows 7 ou Windows 8 ;

  - le système d’exploitation Windows Server 2008 ou Windows Server 2008 R2 ;

  - le système d’exploitation Windows Server 2012 ou Windows Server 2012 R2.

La cmdlet **Test-ExchangeUMCallFlow** nécessite l’installation des composants suivants sur un ordinateur Windows 7, Windows 8, Windows Server 2008 ou Windows Server 2012 64 bits avant son installation :

  - .NET Framework 3.5 Service Pack 1 (SP1) Microsoft. Pour télécharger le service pack, consultez [Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).

  - Microsoft .NET Framework 3.5 Family Update pour les Windows Vista x64 et Windows Server 2008 x64 met à jour si l’outil est exécutée sur un ordinateur Windows Vista ou Windows Server 2008. Pour télécharger la mise à jour, consultez [Microsoft.NET Framework 3.5 Family Update pour les x64, de Windows Vista et Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).

  - Windows Remote Management (WinRM) 2.0 et Windows PowerShell V2 (Windows6.0-KB968930.msu). Pour plus d’informations, consultez l’article 968930 de la Base de connaissances Microsoft, [Package central de Framework de gestion Windows (Windows PowerShell 2.0 et WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Communications unifiées géré des points d’accès 1 2.0, le Runtime de cœur (64 bits). Pour télécharger le fichier UcmaRuntimeWebDownloadX64.msi, consultez [Unified Communications Managed API 2.0, le Runtime de cœur (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

L’applet de commande **Test-ExchangeUMCallFlow** n’est pas inclus sur le DVD de SP1 Exchange 2010, le téléchargement du Service Pack 1 uniquement Exchange 2010 ou le support d’installation Exchange 2013 ; Toutefois, vous pouvez télécharger l’applet de commande à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Pour plus d’informations sur la syntaxe et les paramètres, consultez la rubrique [Test-ExchangeUMCallFlow](https://technet.microsoft.com/fr-fr/library/ff630913\(v=exchg.150\)).

