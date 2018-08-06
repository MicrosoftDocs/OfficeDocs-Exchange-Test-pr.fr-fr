---
title: 'Caract. non pris en charge pour noms d’obj. Exchange 2013: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Caractères non pris en charge pour les noms d’objets Exchange 2013
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652764
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Caractères non pris en charge pour les noms d’objets Exchange 2013

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Cet article décrit les caractères dont l’utilisation est interdite dans les noms d’objets ou de composants dans Exchange 2013. Lorsque vous créez des noms d’objets ou de composants dans Exchange 2013, ces noms ne peuvent pas contenir de caractères non pris en charge, même si vous pouvez créer un objet à l’aide d’un caractère non pris en charge. En outre, si vous tentez d'importer ou de vous connecter à des objets dont les noms incluent des caractères non pris en charge, un message d'erreur peut s'afficher ou un comportement inattendu peut se produire.

## Caractères non pris en charge

Le tableau suivant répertorie les caractères dont l’utilisation est interdite dans les noms d’objets ou de composants Exchange. Il présente également les circonstances au cours desquelles des problèmes peuvent survenir en cas d'utilisation de caractères non pris en charge. Notez la longueur maximale de 64 caractères pour chaque objet répertorié dans le tableau.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objet ou composant Exchange</th>
<th>Scénario Exchange</th>
<th>Caractères non pris en charge</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nom de domaine de messagerie</p></td>
<td><p>Connecteur SMTP (Simple Mail Transfer Protocol)</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nom d'hôte de l'espace d'adressage du connecteur</p></td>
<td><p>Flux de messagerie</p></td>
<td><p><code>..</code> (deux points)</p></td>
</tr>
<tr class="odd">
<td><p>Nom d'hôte des serveurs Exchange Server</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (caractère de soulignement)</p></td>
</tr>
<tr class="even">
<td><p>Nom du site ou de l'organisation</p></td>
<td><p>Exécution du programme d'installation ou déplacement de boîtes aux lettres</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nom du répertoire interne de l'organisation</p></td>
<td><p>Répertoire</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nom de l'arborescence de dossiers publics</p></td>
<td><p>Affichage et création de dossiers publics</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>Nom du destinataire</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>Adresse SMTP de la stratégie de destinataire</p></td>
<td><p>Affichage de la hiérarchie de dossiers publics</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nom d'hôte de l'adresse SMTP de la stratégie de destinataire</p></td>
<td><p>Flux de messagerie</p></td>
<td><p><code>..</code> (deux points)</p></td>
</tr>
<tr class="even">
<td><p>Nom du répertoire interne du site</p></td>
<td><p>Affichage de la hiérarchie de dossiers publics</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>Nom de l'hôte actif</p></td>
<td><p>SMTP</p></td>
<td><p>Espaces de début ou de fin</p></td>
</tr>
</tbody>
</table>

