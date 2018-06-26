---
title: 'IIS est en mode de compatibilité 32 bits_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS est en mode de compatibilité 32 bits_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50478461
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS est en mode de compatibilité 32 bits\_IIS32BitMode

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft® Exchange Server 2007 ne peut pas poursuivre son exécution car les services Internet (IIS) de Microsoft s’exécutent en mode 32 bits sur cet ordinateur 64 bits.

Exchange 2007 nécessite qu’IIS soit en mode 64 bits complet lorsqu’il s’exécute sur un ordinateur 64 bits.

Pour résoudre ce problème, faites basculer IIS en mode 64 bits, puis réexécutez le programme d’installation de Microsoft Exchange.

Pour faire basculer IIS en mode 64 bits

1.  Ouvrez une invite de commandes.

2.  Tapez ensuite :
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Appuyez sur Entrée.

