---
title: 'Modifier la configuration d’AD LDS: Exchange 2013 Help'
TOCTitle: Modifier la configuration d’AD LDS
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61180536
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modifier la configuration d’AD LDS

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Vous pouvez utiliser le script **ConfigureAdam.ps1** (situé dans $env:ExchangeInstallPath\\Scripts) pour modifier la configuration des services AD LDS (Active Directory Lightweight Directory Services) par défaut sur les serveurs de transport Edge avant d’abonner le serveur de transport Edge à votre organisation Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le script <strong>ConfigureAdam.ps1</strong> appelle la commande <strong>dsdbutil</strong> pour modifier les paramètres de registre pour AD LDS. La commande <strong>dsdbutil</strong> est un outil de gestion AD LDS destiné à être utilisé uniquement par des administrateurs expérimentés. Il est recommandé d’utiliser le script <strong>ConfigureAdam.ps1</strong> pour modifier la configuration AD LDS.</td>
</tr>
</tbody>
</table>


Les paramètres figurant dans le tableau suivant sont disponibles pour le script **ConfigureAdam.ps1**. Vous pouvez utiliser un, plusieurs ou une combinaison de ces paramètres pour modifier AD LDS.

### Paramètres disponibles pour le script ConfigureAdam.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>Modifie le port utilisé pour la communication LDAP. Par défaut, le serveur de transport Edge utilise le port 50389 non standard.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>Modifie le port utilisé pour la communication LDAP sécurisée. Par défaut, le serveur de transport Edge utilise le port 50636 non standard.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>Modifie l’emplacement du fichier journal. Par défaut, le serveur de transport Edge crée des fichiers journaux dans le dossier %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>Modifie l’emplacement du fichier de base de données d’annuaire. Par défaut, le serveur de transport Edge stocke la base de données d’annuaire dans le dossier %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
</tbody>
</table>


## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : cinq minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez la section « Serveurs de transport Edge » dans [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Si vous devez apporter des modifications à la configuration AD LDS du serveur de transport Edge, faites-le avant d’abonner le serveur de transport Edge à votre organisation Exchange. Si vous modifiez la configuration AD LDS d’un serveur de transport Edge abonné, vous devrez réabonner le serveur de transport Edge à l’organisation Exchange.

  - Utilisez toujours le script pour modifier les paramètres de registre. Il est possible que les modifications de registre manuelles apportées à la configuration AD LDS rendent l’instance AD LDS indisponible.

  - Si vous devez modifier le port LDAP ou SSL utilisé par AD LDS, vérifiez d’abord que le port sélectionné n’est pas utilisé par une autre application. Vous pouvez utiliser la commande **netstat** pour afficher les ports en cours d’utilisation sur le serveur de transport Edge.

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Modification de la configuration AD LDS sur un serveur de transport Edge

Cet exemple définit le port LDAP utilisé par AD LDS sur 5000. L’esperluette (&) fait partie de la syntaxe de la commande.

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

Cet exemple apporte les modifications suivantes à la configuration AD LDS. L’esperluette (&) fait partie de la syntaxe de la commande. Vous remarquerez que le signe deux-points (:) utilisé entre chaque paramètre et sa valeur :

  - Définit le port LDAP sur 5000

  - Définit le port SSL sur 500

  - Remplace le chemin d’accès au journal par D:\\Exchange Server\\Data\\ADLDS

  - Remplace le chemin d’accès aux données par D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

