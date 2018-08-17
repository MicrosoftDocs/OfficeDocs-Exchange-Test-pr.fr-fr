---
title: 'Le remplacement de contrôleur de domaine est défini dans le Registre'
TOCTitle: Le remplacement de contrôleur de domaine est défini dans le Registre_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50477917
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Le remplacement de contrôleur de domaine est défini dans le Registre\_ConfigDCHostNameMismatch

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2016-12-15_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Le programme d’installation de Microsoft Exchange Server 2007 ne peut pas poursuivre son exécution car sa tentative d’utiliser le contrôleur de domaine spécifié a échoué. Un contrôleur de domaine a été statiquement mappé dans le Registre.

L’installation d’Exchange 2007 nécessite que le contrôleur de domaine spécifié dans la commande d’installation corresponde au contrôleur de domaine mappé statiquement à l’aide d’un écrasement du Registre.

Pour résoudre ce problème, réexécutez le programme d’installation, en spécifiant le contrôleur de domaine mappé statiquement pour le paramètre **/DomainController: \<***FQDN of thestatically mapped domain controller***\>** .

Pour plus d’informations sur DSAccess et la détection de services d’annuaire, consultez l’article 250570 de la Base de connaissances Microsoft « Directory Service Server Detection et utilisation de DSAccess » ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052&kbid=250570)).

