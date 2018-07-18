---
title: Utilisation du pack d'administration Exchange Server 2013 à des fins de dépannage
TOCTitle: Utilisation du pack d'administration Exchange Server 2013 à des fins de dépannage
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53275526
ms.date: 01/09/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation du pack d'administration Exchange Server 2013 à des fins de dépannage

 

_**Dernière rubrique modifiée :**  2013-04-09_

La rubrique [Mise en route avec le pack d'administration Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) offre une vue d'ensemble du tableau de bord du pack d'administration. Elle vous décrit comment ce dernier peut vous aider à résoudre un problème. L'exemple suivant vous permettra de mieux appréhender le processus. Prenons l'exemple du scénario suivant :

Rob Fielder est un administrateur Exchange chez Contoso. Il ouvre la console SCOM et clique sur **Intégrité du serveur** dans le tableau de bord Exchange Server 2013 pour vérifier l'état des serveurs Exchange. Il remarque un état critique des **composants du service** sur l'un des serveurs d'accès au client.

![Serveur CAS défaillant](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "Serveur CAS défaillant")

Rob double-clique sur le serveur, ce qui ouvre la fenêtre **Explorateur d'intégrité**. Dans cette fenêtre, il constate que le composant de service présentant un état défectueux est OWA.Proxy. Il clique sur ce dernier pour afficher les informations d'intégrité pertinentes de cet ensemble.

![Détails de l'intégrité du serveur CAS défaillant](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "Détails de l'intégrité du serveur CAS défaillant")

Le lien fourni sous Sources d'information externes dirige Rob vers la rubrique [Dépannage de l'indicateur d'intégrité OWA.Proxy](https://technet.microsoft.com/fr-fr/library/jj737712\(v=exchg.150\)). Dans cet article, Rob découvre que la première action à entreprendre est de vérifier que le problème est encore présent. Conformément aux instructions, il exécute la commande suivante dans l'environnement de ligne de commande Exchange Management Shell pour vérifier l'état actuel des informations d'intégrité OWA.Proxy :

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

L'exécution de la commande lui renvoie la sortie suivante :

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Rob constate que le problème réside dans le pool d'applications OWA. L'étape suivante consiste à réexécuter la sonde associée pour le moniteur dont l'état n'est pas intègre. À l'aide du tableau de la rubrique « Résolution des problèmes liés aux informations d'intégrité d'OWA.Proxy », il établit que la sonde à réexécuter est OWAProxyTestProbe. Il exécute la commande suivante :

```Powershell
    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List
```

Il analyse la sortie associée à la valeur ResultType et constate que la sonde a échoué :

```Powershell
    ResultType : Failed
```

Il poursuit la lecture avec la section « Actions de récupération OWAProxyTestMonitor » dans l'article. Il se connecte à Server1 via le Gestionnaire des services Internet (IIS) pour vérifier si MSExchangeOWAAppPool est en cours d'exécution sur le serveur IIS. Après avoir confirmé que ce dernier est en cours d'exécution, il passe à l'étape suivante et recycle le pool d'applications MSExchangeOWAAppPool :

```Powershell
    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
```

Après avoir constaté que MSExchangeOWAAppPool a bien été recyclé, il revient pour vérifier si le problème est encore présent en réexécutant la sonde à l'aide de la cmdlet Invoke-MonitoringProbe. Cette fois, il observe que le résultat est probant. Il réexécute la commande suivante pour vérifier que les informations d'intégrité affiche de nouveau l'état **Intègre** :

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

Cette fois, il constate que le problème est résolu.

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Il revient à la console SCOM et contrôle que le problème est résolu.

![Intégrité du serveur](images/Dn195913.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Intégrité du serveur")

Le scénario présenté ci-dessus est une simple démonstration du flux de travail de résolution des problèmes quand vous apercevez une alerte dans la console SCOM. Même si les détails sont différents, vous suivrez généralement un flux de travail de résolution des problèmes similaire pour chaque problème signalé dans la console.

