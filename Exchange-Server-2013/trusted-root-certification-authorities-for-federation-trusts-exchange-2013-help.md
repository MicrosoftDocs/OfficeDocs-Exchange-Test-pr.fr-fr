---
title: 'Autorités de certification racine de confiance pour les approbations de fédération: Exchange 2013 Help'
TOCTitle: Autorités de certification racine de confiance pour les approbations de fédération
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50479305
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorités de certification racine de confiance pour les approbations de fédération

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2017-07-26_

Pour établir une approbation de fédération entre votre organisation Exchange Server 2013 de Microsoft et le [système d’authentification Azure Active Directory](https://go.microsoft.com/fwlink/p/?linkid=135986), vous avez besoin d’un certificat numérique installé sur le serveur Exchange utilisé pour créer l’approbation. Nous recommandons vivement à l’aide d’un certificat auto-signé. Un certificat auto-signé est créé et installé automatiquement lors de l’utilisation de l’Assistant **Activer l’approbation de fédération** dans le Centre d’administration Exchange (FAC).

Si vous souhaitez passer outre le certificat auto-signé recommandé, vous devez demander et installer un certificat SSL (Secure Sockets Layer) X.509 à partir d’une autorité de certification approuvée par Microsoft. Bien que certains certificats émis par d’autres autorités de certification puissent être utilisés pour établir une approbation de fédération avec le système d’authentification Azure AD, elles ne sont pour l’heure pas certifiées par Microsoft.

Le tableau suivant répertorie les autorités de certification actuellement approuvées par Microsoft. Ces autorités de certification ont été testées en vue d’une utilisation avec Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom convivial de l’autorité de certification</th>
<th>Émis par</th>
<th>Rôles prévus</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Brasileira de Raiz de Certificadora de Autoridade</p></td>
<td><p>Brasileira de Raiz de Certificadora de Autoridade</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Autorité de certification Comodo</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Autorité de certification Baltimore CyberTrust Root</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Autorité de certification racine globale Digicert</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV</p></td>
<td><p>Autorité de certification racine globale Digicert</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Autorité de certification sécurisée Equifax</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>Autorité de Certification GlobalSign</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Autorité de certification de classe 2 Go Daddy</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Autorité de certification Network Solutions</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Autorité de certification Comodo</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>Autorité de certification SECOM Trust Systems</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Autorité de certification Comodo</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Autorité de certification publique principale de classe 3</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network (VTN)</p></td>
<td><p>Authentification serveur, authentification client</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les exigences en matière de certificats pour la fédération, consultez la rubrique [Fédération](federation-exchange-2013-help.md).

