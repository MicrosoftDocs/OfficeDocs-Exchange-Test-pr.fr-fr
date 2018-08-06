---
title: 'Param. par défaut pour les répertoires virtuels Exchange: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Paramètres par défaut pour les répertoires virtuels Exchange
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52063020
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Paramètres par défaut pour les répertoires virtuels Exchange

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-07_

Exchange Server 2013 configure automatiquement plusieurs répertoires virtuels IIS (Internet Information Services) au cours de l'installation. Cette rubrique contient des informations sur les paramètres SSL (Secure Sockets Layer) et d'authentification IIS par défaut pour les serveurs d'accès au client et de boîtes aux lettres.

## Serveur d'accès au client

Le tableau suivant récapitule les paramètres par défaut sur un serveur d'accès au client Exchange 2013 autonome.

### Paramètres SSL et d'authentification IIS par défaut du serveur d'accès au client

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Répertoire virtuel</th>
<th>Méthode d'authentification</th>
<th>Paramètres SSL</th>
<th>Méthode de gestion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site web par défaut</p></td>
<td><ul>
<li><p>Anonyme</p></li>
</ul></td>
<td><ul>
<li><p>Obligatoire</p></li>
</ul></td>
<td><p>Console de gestion IIS</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Console de gestion IIS</p></td>
</tr>
<tr class="odd">
<td><p>Découverte automatique</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
<li><p>Authentification de base</p></li>
<li><p>Authentification Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
<li><p>Authentification de base</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Centre d'administration Exchange (CAE) ou environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
<li><p>Authentification Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>Authentification de base</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>CAE ou environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Authentification Windows</p></li>
</ul></td>
<td><ul>
<li><p>Non obligatoire</p></li>
</ul></td>
<td><p>CAE ou environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>Authentification de base</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>CAE ou environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
</ul></td>
<td><ul>
<li><p>Non obligatoire</p></li>
</ul></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="even">
<td><p>RPC</p></td>
<td><ul>
<li><p>Authentification de base</p></li>
<li><p>Authentification Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>Par défaut, toutes les méthodes d'authentification sont désactivées.</p></td>
<td><ul>
<li><p>Obligatoire</p></li>
</ul></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Serveur de boîtes aux lettres

Le tableau suivant récapitule les paramètres par défaut sur un serveur de boîtes aux lettres Exchange 2013 autonome.

### Paramètres SSL et d'authentification IIS par défaut du serveur de boîtes aux lettres

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Répertoire virtuel</th>
<th>Méthode d’authentification</th>
<th>Paramètres SSL</th>
<th>Méthode de gestion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site web par défaut</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
</ul></td>
<td><ul>
<li><p>SSL requis</p></li>
<li><p>Nécessite un chiffrement 128 bits</p></li>
</ul></td>
<td><p>Ce répertoire virtuel ne peut pas être configuré par l’utilisateur.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Authentification anonyme</p></li>
</ul></td>
<td><ul>
<li><p>Non obligatoire</p></li>
</ul></td>
<td><p>Environnement de ligne de commande Exchange Management Shell</p></td>
</tr>
</tbody>
</table>

