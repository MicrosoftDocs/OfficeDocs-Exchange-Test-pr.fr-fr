﻿---
title: 'The World Wide Web Publishing Service is disabled or missing_ShouldReRunSetupForW3SVC: Exchange 2013 Help'
TOCTitle: The World Wide Web Publishing Service is disabled or missing_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 50479517
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# The World Wide Web Publishing Service is disabled or missing\_ShouldReRunSetupForW3SVC

 

_**Sapplique à :**Exchange Server_

_**Dernière rubrique modifiée :**2012-06-05_

Le contenu de cette rubrique n'a pas été mis à jour pour Microsoft Exchange Server 2013. Bien qu'il n'ait pas été encore mis à jour, il peut toujours être applicable pour Exchange 2013. Si vous avez toujours besoin d'aide, consultez les ressources de communauté ci-dessous.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 setup cannot continue because its attempt to install the Mailbox Server or Client Access role found that the World Wide Web Publishing Service is either disabled or not installed on this computer.

Exchange 2007 setup requires the computer that you are installing Microsoft Exchange to have the World Wide Web Publishing Service installed and set to something other than disabled.

To resolve this issue, verify that the World Wide Web Publishing service is installed and not disabled on the local computer, and then rerun Microsoft Exchange setup.

**To verify that the World Wide Web Publishing Service is installed and not disabled**

1.  Right-click **My Computer** on the desktop, and then click **Manage**.

2.  Expand the **Services and Applications** node, and then click the **Services** node.

3.  In the right pane, locate the **World Wide Web Publishing Service**.
    
    If the **World Wide Web Publishing Service** is not displayed in the list of services installed, follow the steps in the procedure below to install it.

4.  If the **World Wide Web Publishing Service** is displayed but has a status other than **Started**, continue with the steps below to start it.

5.  Right-click **World Wide Web Publishing Service**, and then click **Properties**.

6.  Verify the **Startup Type** is **Automatic** and the **Service status** is set to **Started**.

7.  Click **Apply**, and then click **OK**.

**To install the World Wide Web Publishing Service**

1.  On the **Start** menu, select **Settings**, **Control Panel**, and then click **Add or Remove Programs**

2.  Click **Add/Remove Windows Components**.

3.  In the **Components** list, select the **Application Server** check box, and then click **Details**.

4.  Select **Internet Information Services Manager**, and then click **Details**.

5.  Select **World Wide Web Service**, and then select the check box.

6.  Click **OK** two times to return to the **Components** list, and then click **Next**.

7.  Click **Finish** when the IIS service is installed.

