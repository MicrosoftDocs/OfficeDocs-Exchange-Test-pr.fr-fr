---
title: 'Récupérer un serveur Exchange: Exchange 2013 Help'
TOCTitle: Récupérer un serveur Exchange
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50478058
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Récupérer un serveur Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez récupérer un serveur perdu à l’aide de la commande **Setup /m:RecoverServer** dans Microsoft Exchange Server 2013. La plupart des paramètres pour un ordinateur exécutant Exchange 2013 sont stockés dans Active Directory. La commande */m:RecoverServer* récupère un serveur Exchange portant le même nom à l’aide des paramètres et autres informations enregistrés dans Active Directory.

La récupération d’un serveur Exchange perdu s’effectue souvent à l’aide d’un nouveau matériel. Toutefois, vous pouvez également utiliser un serveur existant.

Cette rubrique vous explique comment récupérer un serveur Exchange 2013 perdu qui n’est pas membre d’un groupe de disponibilité de base de données (DAG). Pour obtenir des instructions détaillées sur la récupération d’un serveur qui était membre d’un groupe de disponibilité de base de données, voir [Récupérer un serveur membre de groupe de disponibilité de la base de données](recover-a-database-availability-group-member-server-exchange-2013-help.md).

> [!NOTE]
> Si Exchange est installé à un autre emplacement que celui défini par défaut, vous devez utiliser le commutateur <em>/TargetDir</em> afin de spécifier l’emplacement des fichiers binaires Exchange. Si vous n’utilisez pas le commutateur <em>/TargetDir</em>, les fichiers Exchange sont installés à l’emplacement par défaut (%programfiles%\Microsoft\Exchange Server\V15).<br />
Pour déterminer l’emplacement d’installation, procédez comme suit :
> <ol>
> <li><p>Ouvrez ADSIEDIT.MSC ou LDP.EXE.</p></li>
> <li><p>Accédez à l’emplacement suivant : <strong>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</strong></p></li>
> <li><p>Cliquez avec le bouton droit sur l’objet serveur Exchange, puis cliquez sur <strong>Propriétés</strong>.</p></li>
> <li><p>Recherchez l’attribut <strong>msExchInstallPath</strong>. Cet attribut contient le chemin d’installation actuel.</p></li></ol>

Souhaitez-vous rechercher d’autres tâches de gestion relatives à la sauvegarde et la restauration des données ? Consultez la rubrique [Sauvegarde, restauration et récupération d’urgence](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 20 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Autorisations d’infrastructure Exchange » dans la rubrique [Autorisations d’infrastructure Exchange et Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Le serveur sur lequel la récupération s’effectue doit exécuter le même système d’exploitation que celui du serveur perdu. Par exemple, vous ne pouvez pas récupérer un serveur qui exécutait Exchange 2013 et Windows Server 2008 R2 sur un serveur exécutant Windows Server 2012, ou vice versa. Par exemple, vous ne pouvez pas récupérer un serveur qui exécutait Exchange 2013 et Windows Server 2012 sur un serveur exécutant Windows Server 2012, ou inversement.

  - Les mêmes lettres de lecteur de disque sur le serveur défaillant pour des bases de données montées doivent exister sur le serveur sur lequel vous exécutez la récupération.

  - Le serveur sur lequel la récupération s’effectue doit présenter les mêmes caractéristiques en termes de performances et la même configuration matérielle que le serveur perdu.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Récupérer un serveur Exchange perdu

1.  Réinitialisez le compte d’ordinateur pour le serveur perdu. Pour obtenir la procédure détaillée, consultez la page [Réinitialiser un compte d’ordinateur](https://go.microsoft.com/fwlink/p/?linkid=165388).

2.  Installez le système d’exploitation qui convient et donnez au nouveau serveur le même nom que celui du serveur perdu. La récupération échouera si le serveur sur lequel cette récupération s’effectue ne porte pas le même nom que celui du serveur perdu.

3.  Connectez le serveur au même domaine que celui du serveur perdu.

4.  Installez les conditions préalables requises et les composants du système d‘exploitation. Pour plus de détails, consultez les rubriques [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) et [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

5.  Connectez-vous au serveur en cours de récupération et ouvrez une invite de commande.

6.  Accédez aux fichiers d’installation d’Exchange 2013, puis exécutez la commande suivante :
    
    ```powershell
Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms
```

7.  Une fois la configuration terminée, mais avant que le serveur récupéré ne soit utilisé, reconfigurez les paramètres personnalisés précédemment présents sur le serveur, puis redémarrez le serveur.

## Comment savoir si cela a fonctionné ?

La bonne exécution du programme d’installation est le principal indicateur de réussite de la récupération. Pour vérifier que vous avez correctement récupéré un serveur perdu, procédez comme suit :

  - Ouvrez l’outil Services Windows (services.msc) et vérifiez que les services Microsoft Exchange ont bien été installés et qu’ils sont exécutés.

