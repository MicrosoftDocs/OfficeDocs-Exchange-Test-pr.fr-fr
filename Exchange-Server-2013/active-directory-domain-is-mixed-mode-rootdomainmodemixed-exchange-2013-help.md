---
title: 'Active Directory domain is mixed mode_RootDomainModeMixed: Exchange 2013 Help'
TOCTitle: Active Directory domain is mixed mode_RootDomainModeMixed
ms:assetid: 9f60096e-3eaa-40d8-bde5-13ada5855702
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.rootdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50478900
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory domain is mixed mode\_RootDomainModeMixed

 

_**Sapplique à :** Exchange Server_

_**Dernière rubrique modifiée :** 2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because an existing Active Directory domain is not set to Microsoft Windows®°2000 Server native mode or better.

Exchange 2007 setup will create Universal Security Groups that can only exist in Windows 2000 Server native mode, or better, domains.

To resolve this issue, follow these steps to raise the domain functional level to at least the Windows 2000 Server native level, and then rerun Exchange 2007 setup.

**To raise the domain functional level**

1.  Open Active Directory Domains and Trusts.

2.  In the console tree, right-click the domain for which you want to raise functionality, and then click **Raise Domain Functional Level**.

3.  In **Select an available domain functional level**, use one of the following procedures:
    
      - To raise the domain functional level to Windows 2000 Server native, click **Windows 2000 native**, and then click **Raise**.
    
      - To raise domain functional level to Windows Server® 2003, click **Windows Server 2003**, and then click **Raise.**

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><br />
If you have or will have any domain controllers running Windows NT® 4.0 and earlier, do not raise the domain functional level to Windows 2000 Server native. After the domain functional level is set to Windows 2000 Server native, it cannot be changed back to Windows 2000 Server mixed.<br />
If you have or will have any domain controllers running Windows NT 4.0 and earlier or Windows 2000 Server, do not raise the domain functional level to Windows Server 2003. After the domain functional level is set to Windows Server 2003, it cannot be changed back to Windows 2000 Server mixed or Windows 2000 Server native.</td>
</tr>
</tbody>
</table>



