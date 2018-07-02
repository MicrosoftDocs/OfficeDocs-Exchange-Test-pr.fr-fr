---
title: 'Installer l’outil de dépannage de la messagerie unifiée Exchange: Exchange 2013 Help'
TOCTitle: Installer l’outil de dépannage de la messagerie unifiée Exchange
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56269369
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installer l’outil de dépannage de la messagerie unifiée Exchange

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

L’outil de dépannage de la messagerie unifiée de Microsoft Exchange 2010 est une cmdlet de l’environnement de ligne de commande Exchange Management Shell nommée **Test-ExchangeUMCallFlow**. Vous pouvez utiliser cette cmdlet pour diagnostiquer des erreurs de configuration inhérentes à des scénarios de répondeur automatique et pour tester si la messagerie vocale fonctionne correctement pour les déploiements de messagerie unifiée Microsoft Exchange Server 2010 Service Pack 1 (SP1) (ou ultérieur) locaux et entre différents locaux à la fois. Vous pouvez vous servir de cette cmdlet pour des déploiements avec Microsoft Office Lync Server 2010 (ou ultérieur) ou pour des déploiements de messagerie unifiée avec des passerelles VoIP, des PBX IP ou des contrôleurs de frontière de session.

L’outil de dépannage de la messagerie unifiée peut être installé sur un serveur de messagerie unifiée local, un serveur de boîtes aux lettres Exchange 2013 ou sur un autre ordinateur 64 bits.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 3 minutes

  - Avant d’installer l’outil de dépannage de la messagerie unifiée, les composants suivants doivent être installés sur un ordinateur exécutant Windows Vista, Windows 7, Windows 8 ou l’édition 64 bits de Windows Server 2008 ou Windows Server 2012 ou version ultérieure :
    
      - Reportez-vous à Microsoft .NET Framework 3.5 Service Pack 1 (SP1) [Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Si l’outil est exécutée sur un ordinateur Windows Vista ou Windows Server 2008, consultez le [Microsoft.NET Framework 3.5 Family Update pour les x64, de Windows Vista et Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Gestion à distance de Windows(WinRM) 2.0 et Windows PowerShell V2 (Windows6.0-KB968930.msu). Consultez l’article 968930 de la base de connaissances Microsoft, [Package central de Framework de gestion Windows (Windows PowerShell 2.0 et 2.0 de WinRM)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).
    
      - Microsoft Unified Communications API managée Core 2.0 Runtime (UcmaRuntimeWebDownloadX64.msi). Consultez [Unified Communications Managed API 2.0 Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Installer l’outil de dépannage de la messagerie unifiée

1.  Télécharger l’outil unifiée de messagerie la résolution des problèmes à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625), puis double-cliquez sur le dossier d’installation de MicrosoftExchange2010UMTroubleshootingTool.msi.

2.  Sur la page d’accueil de l’**Assistant Installation de l’outil de dépannage de messagerie unifiée Microsoft Exchange 2010**, cliquez sur **Suivant**.

3.  Sur la page **Contrat de licence utilisateur final**, lisez les termes du contrat de licence et, si vous les acceptez, cliquez sur **J’accepte les termes du contrat de licence**. Cliquez ensuite sur **Suivant**.

4.  Sur la page **Sélectionner le dossier d’installation**, vérifiez le chemin d’accès au dossier d’installation, puis cliquez sur **Suivant**.

5.  Sur la page **Confirmer l’installation**, cliquez sur **Suivant** pour démarrer l’installation.

6.  Dans la page **Installation terminée**, cliquez sur **Fermer**.

