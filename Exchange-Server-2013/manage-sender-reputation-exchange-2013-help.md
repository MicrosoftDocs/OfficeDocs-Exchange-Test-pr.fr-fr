---
title: 'Gérer la réputation de l’expéditeur: Exchange 2013 Help'
TOCTitle: Gérer la réputation de l’expéditeur
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50479550
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer la réputation de l’expéditeur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

L’Agent d’analyse de protocole fournit la réputation de l'expéditeur. La réputation de l'expéditeur bloque les messages en fonction de diverses caractéristiques de l'expéditeur. La fonctionnalité de réputation de l'expéditeur s'appuie sur des données conservées relatives à l'expéditeur pour déterminer, le cas échéant, l'action à appliquer à un message entrant.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - L'agent d'analyse de protocole est l'agent sous-jacent pour la fonctionnalité de réputation de l'expéditeur. Lorsque vous désactivez la réputation de l'expéditeur, l'agent d'analyse de protocole est toujours activé.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne Exchange Management Shell pour activer ou désactiver la réputation de l'expéditeur

Cet exemple désactive la réputation de l'expéditeur.

```powershell
Set-SenderReputationConfig -Enabled $false
```

Cet exemple active la réputation de l'expéditeur.

```powershell
Set-SenderReputationConfig -Enabled $true
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que la réputation de l'expéditeur est activée ou désactivée, procédez comme suit :

1.  Exécutez la commande suivante pour vérifier que l'agent d’analyse de protocole est installé et activé :
    
    ```powershell
    Get-TransportAgent
    ```

2.  Exécutez la commande suivante pour vérifier les valeurs de réputation de l'expéditeur que vous configurées :
    
    ```powershell
    Get-SenderReputationConfig | Format-List Enabled,*MailEnabled
    ```

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la réputation de l'expéditeur pour les messages internes ou externes

Par défaut, la réputation de l'expéditeur est activée pour les messages externes et désactivée pour les messages internes. Un message est considéré comme externe s'il provient d'une connexion non authentifiée extérieure à votre organisation Exchange. Un message est considéré comme interne s'il provient d'une connexion authentifiée et si le domaine de l'expéditeur est configuré en tant que domaine faisant autorité dans votre organisation Exchange.

Pour désactiver la fonctionnalité de réputation de l'expéditeur pour des messages externes, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $false
```

Pour activer la fonctionnalité de réputation de l'expéditeur pour des messages externes, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $true
```

Pour désactiver la fonctionnalité de réputation de l'expéditeur pour des messages internes, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -InternalMailEnabled $false
```

Pour activer la fonctionnalité de réputation de l'expéditeur pour des messages internes, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -InternalMailEnabled $true
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que la réputation de l'expéditeur est activée ou désactivée pour les messages internes et externes, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderReputationConfig | Format-List Enabled,*MailEnabled
    ```

2.  Vérifiez que les valeurs affichées correspondent aux valeurs que vous avez configurées.

## Utiliser l’environnement pour configurer les propriétés de la réputation de l’expéditeur

Pour configurer les propriétés de la réputation de l'expéditeur, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>
```

Cet exemple définit le seuil de blocage de niveau de réputation de l’expéditeur (SRL) avec la valeur 6 et configure la réputation de l’expéditeur pour ajouter des expéditeurs incriminés à la liste rouge IP pendant 36 heures :

```powershell
Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que les propriétés de la réputation de l'expéditeur sont correctement configurées, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderReputationConfig
    ```

2.  Vérifiez que les valeurs affichées correspondent aux valeurs que vous avez configurées.

## Utiliser l'environnement de ligne de commande pour configurer l'accès sortant pour la détection de serveurs proxy ouverts

Vous devez effectuer des opérations supplémentaires pour permettre à la réputation de l'expéditeur de traverser les pare-feu entre Internet et le serveur Exchange qui exécute l'agent d’analyse de protocole. Le tableau suivant répertorie les ports sortants indispensables pour la réputation de l’expéditeur.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocoles</th>
<th>Ports</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4, SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate, Telnet, Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT, HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


Pour configurer l’accès sortant pour la détection de serveurs proxy ouverts, exécutez la commande suivante :

```powershell
Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>
```

Cet exemple configure la réputation de l'expéditeur pour utiliser le serveur proxy ouvert nommé SERVER01 qui utilise le protocole HTTP CONNECT sur le port 80.

```powershell
Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que l’accès sortant est correctement configuré pour la détection des serveurs proxy ouverts, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
    Get-SenderReputationConfig | Format-List ProxyServer*
    ```

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

