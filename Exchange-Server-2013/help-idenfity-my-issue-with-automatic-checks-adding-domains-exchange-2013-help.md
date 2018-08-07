---
title: 'Identifier mon problème à l’aide des vérif. automatiques (ajout de domaines)'
TOCTitle: Identifier mon problème à l’aide des vérifications automatiques (ajout de domaines)
ms:assetid: ea90a24b-7c9c-48d5-9475-0eb7777452f3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn793981(v=EXCHG.150)
ms:contentKeyID: 62632403
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identifier mon problème à l’aide des vérifications automatiques (ajout de domaines)

 

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
<td><p>Domaines</p></td>
<td><p>J’aimerais déterminer les domaines que je possède en local. Je ne sais pas quels domaines m’appartiennent.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834925">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Domaines</p></td>
<td><p>Je ne sais pas si j’ai ajouté et vérifié les bons domaines pour mon client.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Domaines</p></td>
<td><p>J’ai besoin d’aide afin de m’assurer que tous mes enregistrements DNS sont corrects pour Office 365.</p></td>
<td><ol>
<li><p><a href="https://portal.microsoftonline.com/">Connectez-vous à Office 365</a>.</p></li>
<li><p>Sélectionnez <a href="https://portal.microsoftonline.com/tools">Outils</a>.</p></li>
<li><p>Sélectionnez l’option <strong>Vérifier le PC local avec Office 365 Best Practices Analyzer</strong>.</p></li>
</ol></td>
</tr>
</tbody>
</table>

