---
title: 'Mécanismes d’authentification du connecteur de réception: Exchange 2013 Help'
TOCTitle: Mécanismes d’authentification du connecteur de réception
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50478724
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mécanismes d’authentification du connecteur de réception

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_


Les mécanismes d’authentification du connecteur de réception sont les suivants :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mécanisme d’authentification</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aucun</p></td>
<td><p>Pas d’authentification.</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>Annoncer STARTTLS. Requiert de disposer d’un certificat de serveur pour offrir TLS.</p></td>
</tr>
<tr class="odd">
<td><p>Intégré</p></td>
<td><p>NTLM et Kerberos (authentification Windows intégrée).</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>Authentification de base. Requiert une ouverture de session authentifiée.</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>Authentification de base sur TLS. Requiert un certificat de serveur.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Authentification Exchange Server (interface GSSAPI et interface GSSAPI mutuelle).</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>La connexion est considérée comme sécurisée de l’extérieur à l’aide d’un mécanisme de sécurité externe à Exchange. La connexion peut être une association IPSec (Internet Protocol Security) ou un réseau privé virtuel (VPN). De la même façon, les serveurs peuvent résider dans un réseau contrôlé physiquement approuvé. La méthode d’authentification <code>ExternalAuthoritative</code> requiert le groupe d’autorisations <code>ExchangeServers</code>. Cette combinaison de méthode d’authentification et de groupe de sécurité permet de résoudre des adresses de messagerie d’expéditeur anonymes pour des messages reçus via ce connecteur.</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les mécanismes d’authentification du connecteur de réception, consultez la rubrique [New-ReceiveConnector](https://technet.microsoft.com/fr-fr/library/bb125139\(v=exchg.150\)).

