---
title: 'Azure : identifier un problème par des vérifications auto. (enregist. DNS)'
TOCTitle: 'Azure : identifier mon problème à l’aide des vérifications automatiques (enregistrements DNS)'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62629989
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure : identifier mon problème à l’aide des vérifications automatiques (enregistrements DNS)

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

L’un des problèmes les plus courants concerne la configuration incorrecte des enregistrements DNS. Vous pouvez utiliser les vérifications automatiques répertoriées ci-dessous pour valider votre configuration et mettre à jour votre environnement.

Si vous disposez déjà d’un compte d’utilisateur Office 365, sélectionnez Se connecter. Vous n’avez pas besoin d’un compte Azure ID. Vous pouvez être invité à indiquer à nouveau un compte d’utilisateur lors de l’exécution des vérifications. Dans ce cas, vous devez indiquer votre compte d’utilisateur au format username@youroffice365login.domain et votre mot de passe.

## Conditions préalables

Nous allons vérifier que vous avez Assistant de connexion Azure Active Directory et installé la cmdlet Module Azure Active Directory pour Windows PowerShell.

Le Assistant de connexion Azure Active Directory est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

Le Module Azure Active Directory pour Windows PowerShell est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Vérifications d’enregistrements DNS


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
<td><p>Mon domaine personnalisé (par exemple, contoso.com) ne semble pas être configuré avec Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Domaines</p></td>
<td><p>Mon domaine personnalisé (par exemple, contoso.com) ne semble pas être configuré avec Office 365 (j’ai utilisé un enregistrement CNAME).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Domaines</p></td>
<td><p>Mon domaine personnalisé (par exemple, contoso.com) ne semble pas être configuré avec Office 365 (j’ai utilisé un enregistrement TXT).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Messagerie instantanée</p></td>
<td><p>Mes utilisateurs rencontrent des difficultés lorsqu’ils tentent de faire fonctionner leur client Lync.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Messagerie instantanée</p></td>
<td><p>Mes utilisateurs rencontrent des difficultés lorsqu’ils tentent de faire fonctionner leur client Lync avec d’autres organisations.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Courrier</p></td>
<td><p>Je ne parviens pas à faire en sorte qu’Outlook soit automatiquement configuré avec Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Courrier</p></td>
<td><p>Ma messagerie ne semble pas effectuer de routage vers Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Courrier</p></td>
<td><p>Mon organisation reçoit une grande quantité de courrier indésirable.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Courrier</p></td>
<td><p>Je ne parviens pas à faire fonctionner Exchange hybride.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">Exécuter cette vérification</a></p></td>
</tr>
</tbody>
</table>

