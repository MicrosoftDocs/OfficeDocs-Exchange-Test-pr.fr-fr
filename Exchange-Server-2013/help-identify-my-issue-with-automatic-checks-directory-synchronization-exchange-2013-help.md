---
title: 'Identifier mon problème à l’aide des vérifications automatiques - Synchronisation d’annuaires: Exchange 2013 Help'
TOCTitle: Identifier mon problème à l’aide des vérifications automatiques - Synchronisation d’annuaires
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62632404
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identifier mon problème à l’aide des vérifications automatiques - Synchronisation d’annuaires

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez utiliser les vérifications automatiques répertoriées ci-dessous pour valider votre configuration et mettre à jour votre environnement.

Si vous disposez déjà d’un compte d’utilisateur Office 365, sélectionnez Se connecter. Vous n’avez pas besoin d’un compte Azure ID. Vous pouvez être invité à indiquer à nouveau un compte d’utilisateur lors de l’exécution des vérifications. Dans ce cas, vous devez indiquer votre compte d’utilisateur au format username@youroffice365login.domain et votre mot de passe.

> [!NOTE]
> Si vous recevez des messages d’avertissement de synchronisation dans le portail Office 365, les erreurs dans les journaux d’événements serveur, ou les e-mails de notification de synchronisation de répertoire incorrect à partir de Microsoft Online Services, vous pouvez avoir un type de problème de synchronisation d’annuaire. La <a href="https://aka.ms/dsup">Résolution des problèmes de synchronisation de répertoire</a> est un outil de diagnostic basé sur le Web conçu pour aider à identifier les types courants d’échecs de synchronisation et de prescrire des solutions ciblées pour les problèmes éventuellement rencontrés. La résolution des problèmes de synchronisation de répertoire doit être exécuté sur le serveur de synchronisation d’annuaire.


## Conditions préalables

Nous allons vérifier que vous avez Assistant de connexion Azure Active Directory et installé la cmdlet Module Azure Active Directory pour Windows PowerShell.

Le Assistant de connexion Azure Active Directory est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

Le Module Azure Active Directory pour Windows PowerShell est disponible en deux versions : [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) et [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Vérifications de synchronisation d’annuaires


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
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si tous mes comptes d’utilisateur Active Directory satisfont aux exigences pour la synchronisation d’annuaires.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si les niveaux fonctionnels de mon domaine Active Directory sont configurés correctement pour Windows Server 2003 ou une version supérieure.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si la synchronisation d’annuaires a été effectuée au cours des trois dernières heures.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si mon annuaire Active Directory contient des attributs utilisateur en double qui vont bloquer la synchronisation d’annuaires.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si la synchronisation d’annuaires est activée dans Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si je peux déployer des limitations de devis Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si je peux déployer Office 365 et utiliser les paramètres de synchronisation d’annuaires par défaut.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Exécuter cette vérification</a></p></td>
</tr>
<tr class="odd">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne suis pas sûr d’utiliser Active Directory ou que la synchronisation d’annuaires soit prise en charge.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">Exécuter cette vérification</a></p></td>
</tr>
<tr class="even">
<td><p>Synchronisation d’annuaires</p></td>
<td><p>Je ne sais pas si tous mes groupes Active Directory satisfont aux exigences pour la synchronisation d’annuaires.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">Exécuter cette vérification</a></p></td>
</tr>
</tbody>
</table>

