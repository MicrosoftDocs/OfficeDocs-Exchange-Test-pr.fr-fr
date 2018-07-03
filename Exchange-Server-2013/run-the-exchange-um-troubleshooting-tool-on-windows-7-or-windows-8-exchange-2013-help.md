---
title: 'Exécuter l’outil de dépannage de la messagerie unifiée Exchange sur Windows 7 ou Windows 8: Exchange 2013 Help'
TOCTitle: Exécuter l’outil de dépannage de la messagerie unifiée Exchange sur Windows 7 ou Windows 8
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56269368
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exécuter l’outil de dépannage de la messagerie unifiée Exchange sur Windows 7 ou Windows 8

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

L’outil de dépannage de la messagerie unifiée de Microsoft Exchange 2010 est une cmdlet de l’environnement de ligne de commande Exchange Management Shell nommée **Test-ExchangeUMCallFlow**. Vous pouvez utiliser cette cmdlet pour diagnostiquer des erreurs de configuration inhérentes à des scénarios de répondeur automatique et pour tester si la messagerie vocale fonctionne correctement pour les déploiements de messagerie unifiée Microsoft Exchange Server 2010 Service Pack 1 (SP1) (ou ultérieur) locaux et entre différents locaux à la fois. Vous pouvez vous servir de cette cmdlet pour des déploiements avec Microsoft Office Lync Server 2010 (ou ultérieur) ou pour des déploiements de messagerie unifiée avec des passerelles VoIP, des PBX IP ou des contrôleurs de frontière de session.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Serveur de messagerie unifiée » ou « Services de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Assurez-vous que votre organisation Exchange 2010 ou Exchange 2013 remplit les conditions suivantes :
    
      - Un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, voir [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).
    
      - Une stratégie de boîte aux lettres de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, voir [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md).
    
      - Une passerelle IP de messagerie unifiée a été créée. Pour obtenir la procédure détaillée, voir [Créer une passerelle IP de messagerie unifiée](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Un serveur de messagerie unifiée Exchange 2010 a été ajouté au plan de numérotation de messagerie unifiée. Si vous utilisez Exchange 2013 avec Lync Server, ajoutez tous les serveurs d’accès au client et de boîtes aux lettres aux plans de numérotation URI SIP. Pour obtenir la procédure détaillée, consultez la rubrique [Ajouter un serveur de messagerie unifiée au plan de numérotation](https://go.microsoft.com/fwlink/p/?linkid=313051) ou [Ajouter des serveurs de boîtes aux lettres et accès au Client à un plan de numérotation URI SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Si vous utilisez l’outil de dépannage de la messagerie unifiée sur un serveur local de messagerie unifiée avec Exchange 2010 SP1 ou version supérieure, ou sur un serveur de boîtes aux lettres Exchange 2013, vous n’avez peut-être pas besoin de procéder à toutes les installations préalables répertoriées ci-dessous. Il se peut qu’elles aient été effectuées avec le rôle serveur de messagerie unifiée. Cependant, si vous installez l’outil de dépannage de messagerie unifiée sur un ordinateur 64 bits autre qu’un serveur exécutant le rôle serveur de messagerie unifiée, vous devez installer les composants suivants :
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Consultez la rubrique [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Si l’outil est destiné à être utilisé sur un ordinateur Windows Vista ou Windows Server 2008, consultez la rubrique [Mises à jour Microsoft .NET Framework 3.5 (Family Update) pour Windows Vista x64 et Windows Server 2008 x64](https://go.microsoft.com/fwlink/?linkid=178998).
    
      - Gestion à distance de Windows(WinRM) 2.0 et Windows PowerShell V2 (Windows6.0-KB968930.msu). Consultez l’article 968930 de la base de connaissances Microsoft, [Package central de Framework de gestion Windows (Windows PowerShell 2.0 et 2.0 de WinRM)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi). Consultez la rubrique [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Téléchargez et installez l’outil de dépannage de messagerie unifiée.
    
      - Téléchargez l’[outil de dépannage de la messagerie unifiée](https://go.microsoft.com/fwlink/p/?linkid=182625) à partir du centre de téléchargement Microsoft.
    
      - Installez l’outil. Pour plus d’informations, voir [Installer l’outil de dépannage de la messagerie unifiée Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Si vous envisagez d’utiliser l’outil de dépannage de la messagerie unifiée en mode <code>SIPClient</code>, plusieurs autres conditions doivent être satisfaites concernant Office Communications Server 2007 R2 ou Microsoft Lync Server. Pour plus d’informations, consultez les rubriques <a href="https://go.microsoft.com/fwlink/p/?linkid=311961">Liste de vérification : Déploiement d’Office Communications Server 2007 R2 et d’une messagerie unifiée Exchange 2010</a>.</td>
        </tr>
        </tbody>
        </table>


  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Exécuter l’outil de dépannage de la messagerie unifiée sur Windows Vista, Windows 7 ou Windows 8

1.  Cliquez sur **Démarrer** \> **Tous les programmes** \> **Accessoires** \> **Windows PowerShell**.

2.  Cliquez avec le bouton droit sur **Windows PowerShell**, puis dans le menu contextuel, sélectionnez **Exécuter en tant qu’administrateur**.

3.  À l’invite de commandes Windows PowerShell, accédez au dossier dans lequel vous avez installé l’outil de dépannage de la messagerie unifiée et exécutez la commande ci-après.
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  Si vous exécutez l’outil de dépannage de la messagerie unifiée sous Windows Vista, Windows 7 ou Windows 8, à l’invite de commandes Windows PowerShell, exécutez la commande ci-après.
    
        Set-ExecutionPolicy RemoteSigned

5.  À partir du menu **Démarrer**, ouvrez l’**outil de dépannage de la messagerie unifiée Microsoft Exchange 2010**.

6.  À l’invite de la fenêtre **Microsoft Exchange 2010 UM Troubleshooting Tool**, saisissez ce qui suit, puis appuyez sur la touche Entrée.
    
        $cred=Get-Credential

7.  Dans la fenêtre **Demande d’informations d’identification Windows PowerShell**, saisissez un nom d’utilisateur/de domaine et un mot de passe, puis cliquez sur **OK**.

8.  Dans la fenêtre **Microsoft Exchange 2010 UM Troubleshooting Tool**, indiquez les paramètres de cmdlet nécessaires pour tester le flux d’appels. Par exemple :
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

