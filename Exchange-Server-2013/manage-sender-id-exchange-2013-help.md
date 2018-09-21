---
title: 'Gérer les ID des expéditeurs: Exchange 2013 Help'
TOCTitle: Gérer les ID des expéditeurs
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50477823
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer les ID des expéditeurs

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-08_

La fonctionnalité d’ID de l’expéditeur est fournie par l’agent d’ID de l’expéditeur. L’ID de l’expéditeur valide l’origine des messages électroniques en vérifiant l’adresse IP de l’expéditeur par rapport à celle du prétendu propriétaire du domaine de l’expéditeur. Le filtrage de l’ID de l’expéditeur est effectué sur les messages entrants en provenance d’Internet mais qui ne sont pas authentifiés. Ces messages sont traités comme des messages externes.

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de chaque procédure : 5 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Par défaut, les fonctionnalités de courrier indésirable ne sont pas activées dans le service Transport du serveur de boîtes aux lettres. En général, vous activez uniquement les fonctionnalités de courrier indésirable sur un serveur de boîtes aux lettres si votre organisation Exchange n'effectue aucun filtrage de courrier indésirable avant d'accepter les messages entrants. Pour plus d'informations, voir Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres[Activer la fonctionnalité de blocage du courrier indésirable sur un serveur de boîtes aux lettres](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver l’ID de l’expéditeur

Pour désactiver l'ID de l'expéditeur, exécutez la commande suivante :

```powershell
Set-SenderIDConfig -Enabled $false
```

Pour activer l'ID de l'expéditeur, exécutez la commande suivante :

```powershell
Set-SenderIDConfig -Enabled $true
```

> [!NOTE]
> Lorsque vous désactivez l’ID de l’expéditeur, l’agent d’ID de l’expéditeur sous-jacent est toujours activé. Pour désactiver l’agent d’ID de l’expéditeur, exécutez la commande : <code>Disable-TransportAgent &quot;Sender ID Agent&quot;</code>.


## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement activé ou désactivé l’ID de l’expéditeur, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-SenderIDConfig | Format-List Enabled
```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer une action d’ID de l’expéditeur pour les messages usurpés

Pour configurer l’action d’ID de l’expéditeur pour les messages usurpés, exécutez la commande suivante :

```powershell
Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>
```

Cet exemple configure l’agent d’ID de l’expéditeur pour rejeter tous les messages dont l’adresse IP du serveur d’envoi n’est pas répertoriée comme serveur d’envoi SMTP faisant autorité dans l’enregistrement Sender Policy Framework (SPF) DNS pour le domaine d’envoi.

```powershell
Set-SenderIDConfig -SpoofedDomainAction Reject
```

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez configuré l’action de l’ID de l’expéditeur pour les messages usurpés, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-SenderIDConfig | Format-List SpoofedDomainAction
```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer une action d’ID de l’expéditeur pour les erreurs temporaires

Pour configurer l’action d’ID de l’expéditeur pour les erreurs temporaires, exécutez la commande suivante :

```powershell
Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>
```

Dans cet exemple, l’agent d’ID de l’expéditeur est configuré afin de marquer les messages dans le cas où l’état d’ID de l’expéditeur ne peut pas être déterminé, en raison d’une erreur temporaire du serveur DNS. Le message sera traité par d'autres agents de blocage du courrier indésirable, tandis que l'agent de filtrage de contenu utilisera la marque lors de la détermination de la valeur de seuil de probabilité de courrier indésirable pour le message.

```powershell
Set-SenderIDConfig -TempErrorAction StampStatus
```

Notez bien que `StampStatus` est la valeur par défaut pour le paramètre *TempErrorAction*.

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez configuré l’action de l’ID de l’expéditeur pour les erreurs temporaires, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-SenderIDConfig | Format-List TempErrorAction
```

2.  Vérifiez que la valeur affichée est la valeur que vous avez configurée.

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les exceptions de domaine de destinataire et expéditeur

Pour remplacer les valeurs existantes, exécutez la commande suivante :

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

Cet exemple configure l’agent d’ID de l’expéditeur pour ignorer la vérification de l’ID de l’expéditeur pour les messages envoyés à kim@contoso.com et john@contoso.com et contourner la vérification de l’ID de l’expéditeur pour les messages envoyés à partir du domaine fabrikam.com.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

Pour ajouter ou supprimer des entrées sans modifier une valeur existante, exécutez la commande suivante :

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Cet exemple configure l’agent d’ID de l’expéditeur avec les informations suivantes :

  - Ajoutez chris@contoso.com et michelle@contoso.com à la liste des destinataires existants qui ignorent la vérification de l’ID de l’expéditeur.

  - Retirez tailspintoys.com de la liste des domaines existants qui ignorent la vérification de l’ID de l’expéditeur.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez correctement configuré les exceptions de domaine de destinataire et d’expéditeur, procédez comme suit :

1.  Exécutez la commande suivante :
    
    ```powershell
Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains
```

2.  Vérifiez que les valeurs affichées sont les valeurs que vous avez configurées.

