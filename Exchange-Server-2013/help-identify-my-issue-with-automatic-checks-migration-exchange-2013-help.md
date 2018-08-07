---
title: 'Identifier problème par vérifications auto. (migration): Exchange 2013 Help'
TOCTitle: Identifier mon problème à l’aide des vérifications automatiques (migration)
ms:assetid: c1cd235d-8e8b-44a8-862d-9d36dc3a44c3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn793980(v=EXCHG.150)
ms:contentKeyID: 62632401
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identifier mon problème à l’aide des vérifications automatiques (migration)

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les vérifications présentées sur cette page vous aideront à identifier certains des problèmes de configuration les plus courants. Vous pouvez utiliser les vérifications automatiques ci-dessous pour valider votre configuration et mettre à jour votre environnement.

Si vous possédez déjà un compte d’utilisateur Office 365, sélectionnez **Se connecter**. Vous n’avez pas besoin d’un compte Azure ID. Vous pouvez être invité à indiquer à nouveau un compte d’utilisateur lors de l’exécution des vérifications. Dans ce cas, vous devez indiquer votre compte d’utilisateur au format username@youroffice365login.domain et votre mot de passe.

## Conditions préalables

Nous allons vérifier que vous avez Assistant de connexion Azure Active Directory et installé la cmdlet Module Azure Active Directory pour Windows PowerShell.

Le Assistant de connexion Azure Active Directory est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

Le Module Azure Active Directory pour Windows PowerShell est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Vérifications d’ajout de domaines


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Application</p></td>
<td><p>Symptôme</p></td>
<td><p>Vérification</p></td>
</tr>
<tr class="even">
<td><p>Tailles de boîtes aux lettres</p></td>
<td><p>Je voudrais déterminer si les utilisateurs respectent les tailles de boîtes aux lettres par défaut de mon organisation de manière à pouvoir planifier au mieux ma migration.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834877">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Forêt unique</p></td>
<td><p>Je tente de déterminer si je peux migrer les comptes d’utilisateurs à l’aide de la synchronisation d’annuaires.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834875">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Mode fonctionnel de domaine</p></td>
<td><p>Je ne sais pas si je suis prêt à intégrer ADFS 2.0 et/ou l’authentification unique.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Dossiers publics</p></td>
<td><p>Je ne sais pas si je dispose de dossiers publics à migrer vers Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834896">Exécuter cette vérification</a></p></td>
</tr>
</tbody>
</table>

