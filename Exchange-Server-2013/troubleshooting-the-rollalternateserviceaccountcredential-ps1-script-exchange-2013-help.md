---
title: 'Dépannage des problèmes liés au script RollAlternateServiceAccountCredential.ps1: Exchange 2013 Help'
TOCTitle: Dépannage des problèmes liés au script RollAlternateServiceAccountCredential.ps1
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63918666
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dépannage des problèmes liés au script RollAlternateServiceAccountCredential.ps1

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-01-14_

Cette rubrique fournit des solutions et des informations à propos des erreurs courantes qui peuvent se produire lorsque vous utilisez le script RollAlternateServiceAccountPassword.ps1.

## Au moins un serveur d’accès au client ne peut pas être mis à jour avec le mot de passe

## Problème

Lorsque vous utilisez les paramètres *ToEntireForest* ou *ToArrayMembers* avec le script, dans certains cas, au moins un des serveurs d’accès au client risque de ne pas être mis à jour.

## Solution

Vérifiez que les serveurs que le script ciblera sont bien tous les serveurs requis à l’aide de la cmdlet **Get-ClientAccessArray**, comme dans l’exemple suivant.

    Get-ClientAccessArray | fl members

Si le serveur dont la mise à jour échoue est membre du groupe d'accès au client et qu'il n'est toujours pas mis à jour correctement, exécutez de nouveau le programme d'installation Exchange et ajoutez de nouveau le rôle de serveur d'accès au client au serveur. Vous pouvez également spécifier des serveurs individuels à cibler à l'aide du paramètre *ToSpecificServers*.

## Certains serveurs ne répondent pas au script

## Problème

Dans certains cas, les serveurs peuvent ne pas se mettre à jour à cause d’erreurs temporaires telles qu’une mauvaise connexion réseau.

## Solution

Vérifiez que les serveurs en question ont une connectivité réseau et Active Directory, puis réexécutez le script.

## Certains membres de groupe sont hors service pendant un certain temps

## Problème

Si un serveur est hors service pendant plus longtemps, mais qu'il est toujours membre du groupe, tel que déterminé par la cmdlet **Get-ClientAccessArray**, la fonctionnalité du script peut être affectée lors de l'utilisation des paramètres *ToArrayMembers* et *ToEntireForest*. Le même problème se produira si un serveur a rencontré un échec permanent mais qu’il n’a pas été supprimé correctement de votre déploiement.

## Solution

Pour résoudre ce problème, supprimez le serveur de votre déploiement à l'aide du programme d'installation Exchange ou exécutez le script en mode avec assistance jusqu'à ce que le serveur puisse être supprimé.

Si le serveur est hors service pendant une courte durée seulement et que vous ne souhaitez pas supprimer définitivement Exchange, vous pouvez ajuster le script pour qu'il soit exécuté sur des serveurs spécifiques à l'aide du paramètre *ToSpecificServers* afin que seuls les serveurs actifs soient ciblés. Vous pouvez supprimer le service d'accès au client RPC à partir de l'objet Active Directory du serveur qui ne répond pas à l'aide de la cmdlet **Remove-ClientAccessArray**, comme indiqué dans l'exemple suivant.

    Remove-RPCClientAccess -Server Server.Contoso.com

Après la suppression du service d’accès au client RPC, le serveur se sera pas renvoyé comme membre du groupe par [Get-ClientAccessArray](https://technet.microsoft.com/fr-fr/library/dd297976\(v=exchg.150\)) et le script ne le ciblera pas. Dès que le serveur est à nouveau fonctionnel, vous pouvez rajouter le service d’accès au client RPC à l’aide de la cmdlet **New-RpcClientAccess**. Lorsque vous aurez rajouté le service d’accès au client RPC, assurez-vous de redémarrer le service Carnet d’adresses Microsoft Exchange sur le serveur concerné.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Avant de supprimer le service d’accès au client RPC d’un serveur, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</a>.</td>
</tr>
</tbody>
</table>


## Pour plus d’informations

Pour plus d’informations sur l’utilisation de l’authentification Kerberos avec un groupe de serveurs d’accès au client ou une solution d’équilibrage de charge, consultez les rubriques suivantes :

  - [Configuration de l’authentification Kerberos pour les serveurs d’accès au client avec équilibrage de charge](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [Utilisation du script RollAlternateserviceAccountCredential.ps1 dans l’environnement de ligne de commande Exchange Management Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

