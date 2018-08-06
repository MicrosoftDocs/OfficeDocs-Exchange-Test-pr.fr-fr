---
title: 'Identifier mon problème à l’aide des vérif. automatiques - Active Directory | Microsoft Docs'
TOCTitle: Identifier mon problème à l’aide des vérifications automatiques - Active Directory
ms:assetid: af08e7a1-775a-4e56-a6fe-4ffc10460514
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn793979(v=EXCHG.150)
ms:contentKeyID: 62632400
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identifier mon problème à l’aide des vérifications automatiques - Active Directory

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les vérifications présentées sur cette page vous aideront à identifier certains des problèmes de configuration les plus courants. Vous pouvez utiliser les vérifications automatiques ci-dessous pour valider votre configuration et mettre à jour votre environnement.

Si vous possédez déjà un compte d’utilisateur Office 365, sélectionnez **Se connecter**. Vous n’avez pas besoin d’un compte Azure ID. Vous pouvez être invité à indiquer à nouveau un compte d’utilisateur lors de l’exécution des vérifications. Dans ce cas, vous devez indiquer votre compte d’utilisateur au format username@youroffice365login.domain et votre mot de passe.

## Conditions préalables

Nous allons vérifier que vous avez Assistant de connexion Azure Active Directory et installé la cmdlet Module Azure Active Directory pour Windows PowerShell.

Le Assistant de connexion Azure Active Directory est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

Le Module Azure Active Directory pour Windows PowerShell est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Vérifications Active Directory


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
<td><p>Version d’Exchange</p></td>
<td><p>Je ne sais pas si Exchange Server est installé en local ni quelle version j’utilise.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834879">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Informations d’identification</p></td>
<td><p>Je ne suis pas sûr d’avoir les bonnes informations d’identification pour accéder à Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834880">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Outils tiers</p></td>
<td><p>Je ne sais pas quelles intégrations/applications tierces sont installées dans mon environnement de messagerie.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834907">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Boîtes aux lettres partagées</p></td>
<td><p>J’aimerais déterminer qui gère des boîtes aux lettres pour d’autres personnes (délégués).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834917">Exécuter cette vérification</a></p></td>
</tr>
</tbody>
</table>

