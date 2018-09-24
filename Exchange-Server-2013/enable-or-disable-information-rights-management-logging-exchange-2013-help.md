---
title: 'Activ./désactiv. connex. à la gestion des droits de l’infor.: Exchange 2013'
TOCTitle: Activer ou désactiver la connexion à la gestion des droits relatifs à l’information
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50478353
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activer ou désactiver la connexion à la gestion des droits relatifs à l’information

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-12_

Dans Exchange Server 2013, vous pouvez utiliser les journaux Information Rights Management (IRM) pour surveiller les opérations IRM et résoudre les problèmes liés à ces dernières. L’enregistrement des transactions IRM est activé par défaut.

Les journaux IRM utilisent les paramètres courants suivants :

  - *IrmLogEnabled*   Active ou désactive l’enregistrement des opérations IRM. Par défaut : `$true`.

  - *IrmLogMaxAge*   Spécifie l’âge maximal des fichiers journaux IRM. Les fichiers plus anciens que l’âge spécifié sont supprimés. Par défaut : 30 jours.

  - *IrmLogMaxDirectorySize*   Spécifie la taille maximale du répertoire qui contient les journaux IRM. Si un répertoire atteint sa taille maximale de fichier, le serveur supprime d’abord les fichiers journaux les plus anciens. Par défaut : 250 Mo.

  - *IrmLogMaxFileSize*   Spécifie la taille maximale de chaque fichier journal IRM. Lorsqu’un fichier journal atteint la taille spécifiée, un nouveau fichier journal est créé. Par défaut : 10 Mo.

  - *IrmLogPath*   Spécifie l’emplacement du répertoire des journaux IRM. Par défaut : `%ExchangeInstallPath%Logging\IRMLogs`.

Si vous souhaitez rechercher des tâches de gestion supplémentaires relatives à IRM, consultez [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 2 à 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez entrée « Configurer l’enregistrement IRM » de la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Vous ne pouvez pas utiliser le Centre d’administration Exchange (EAC) pour activer ou désactiver l’enregistrement IRM sur un serveur. Vous devez utiliser l’environnement de ligne de commande Exchange Management Shell

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer l’enregistrement IRM sur un serveur

Cet exemple active le journal IRM sur un serveur de boîtes aux lettres.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $true
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-TransportService](https://technet.microsoft.com/fr-fr/library/jj215682\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver l’enregistrement IRM sur un serveur

Cet exemple désactive l’enregistrement IRM sur un serveur de boîtes aux lettres.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $false
```

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Set-TransportService](https://technet.microsoft.com/fr-fr/library/jj215682\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé ou désactivé l’enregistrement IRM sur un serveur, exécutez la cmdlet [Get-TransportService](https://technet.microsoft.com/fr-fr/library/jj215746\(v=exchg.150\)) afin de récupérer les paramètres IRM.

Cet exemple récupère toutes les propriétés d’enregistrement IRM sur le serveur EXCH01.

```powershell
Get-TransportService -Identity EXCH01 | Format-List IRMLog*
```

