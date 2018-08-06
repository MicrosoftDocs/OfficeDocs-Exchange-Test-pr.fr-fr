---
title: 'Événements et erreurs de gestion des enregist. de messag.: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Événements et erreurs de gestion des enregistrements de messagerie
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51407210
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Événements et erreurs de gestion des enregistrements de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La gestion des enregistrements de messagerie (MRM) génère des événements que vous pouvez consulter dans l'Observateur d'événements. Cela vous permet de dépanner et de vérifier les performances de l'Assistant Dossier géré. L'Observateur d'événements suit les types d'événements suivants, dans l'ordre d'importance ci-après :

1.  erreurs ;

2.  avertissements ;

3.  événements d'information.

## Erreurs et événements de MRM

Le tableau suivant présente la liste des événements que vous pouvez utiliser pour dépanner la MRM. Les types d'enregistrements sont les suivants :

  - Les événements étiquetés comme **LogAlways** sont toujours enregistrés individuellement.

  - Les événements étiquetés comme **LogPeriodic** ne sont enregistrés qu'une seule fois dans une période de cinq minutes et non à chaque fois qu'ils se produisent. Cela aide à éviter un nombre excessif d'entrées dans le journal.

### Événements de MRM dans la catégorie Assistant Dossier géré

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>ID d'événement</strong></th>
<th><strong>Catégorie</strong></th>
<th><strong>Type d'événement</strong></th>
<th><strong>Enregistrement</strong></th>
<th><strong>Valeur ou description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Impossible d'obtenir l'objet configuration du serveur à partir d'Active Directory. &lt;<em>Exception details</em>&gt;. Vérifiez s'il y a des problèmes de connectivité réseau au niveau du contrôleur de domaine ou une configuration DNS incorrecte.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>La stratégie de rétention pour le dossier &lt;<em>folder</em>&gt; dans la boîte aux lettres &lt;<em>mailbox</em>&gt; ne sera pas appliquée. L’Assistant Dossier géré ne peut pas traiter le paramètre de contenu géré &lt;<em>content setting</em>&gt; pour le dossier géré &lt;<em>managed folder</em>&gt;. RetentionAction est défini sur MoveToFolder mais aucun dossier de destination n'a été spécifié. Spécifiez un dossier de destination.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>La stratégie de rétention ne sera pas appliquée au dossier &lt;<em>folder</em>&gt; dans la boîte aux lettres &lt;<em>mailbox</em>&gt;. Impossible de traiter le paramètre de contenu géré &lt;<em>content setting</em>&gt; pour le dossier géré &lt;<em>managed folder</em>&gt;. RetentionAction est défini sur MoveToFolder mais le dossier de destination &lt;<em>folder</em>&gt; est le même que le dossier source &lt;<em>folder</em>&gt;. Spécifiez un dossier de destination différent du dossier source.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>L’Assistant Dossier géré a ignoré le traitement de toutes les bases de données sur le serveur local car il n’a pas pu lire les paramètres du fichier journal d’audit depuis Active Directory. Il réessaiera plus tard dans la fenêtre de planification. Base de données en cours : &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>L’Assistant Dossier géré a ignoré le traitement de toutes les bases de données sur le serveur local car le fichier journal d’audit est activé, mais son chemin d’accès est manquant dans Active Directory. Il réessaiera plus tard dans la fenêtre de planification. Base de données en cours : &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>L’Assistant Dossier géré n’a pas pu configurer le journal d’audit. Il va arrêter le traitement de la base de données en cours : ’%1’. Il réessaiera plus tard dans la fenêtre de planification. Détails de l'exception : &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>Échec d’écriture dans le journal d’audit par l’Assistant Dossier géré. Il va arrêter le traitement de la base de données en cours : &lt;<em>database</em>&gt;. Il réessaiera plus tard d'écrire dans le journal d'audit dans la fenêtre de planification. Détails de l'exception : &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>Assistant Dossier géré</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>Une exception s'est produite dans l'Assistant Dossier géré lors du traitement de la boîte aux lettres : Dossier &lt;<em>mailbox</em>&gt; : Nom : Id &lt;<em>folder name</em>&gt; : Élément &lt;<em>folder ID</em>&gt; : Id : &lt;<em>IDs</em>&gt;. Exception : &lt;<em>exception</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### Événements MRM dans la catégorie d'Assistants

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>ID d'événement</strong></th>
<th><strong>Catégorie</strong></th>
<th><strong>Type d'événement</strong></th>
<th><strong>Enregistrement</strong></th>
<th><strong>Valeur ou description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; n'a pas pu traiter la boîte aux lettres &lt;<em>mailbox</em>&gt;. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. Impossible de traiter les modifications du planning. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; pour la base de données &lt;<em>database</em>&gt; entre une fenêtre de temps programmée. Il existe &lt;<em>number</em>&gt; boîtes aux lettres à traiter.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; pour la base de données &lt;<em>mailbox</em>&gt; quitte une fenêtre de temps programmée. &lt;<em>number</em>&gt; boîtes aux lettres sur &lt;<em>number</em>&gt; ont été traitées. &lt;<em>number</em>&gt; boîtes aux lettres ont été ignorées en raison d'erreurs. &lt;<em>number</em>&gt; boîtes aux lettres ont été traitées séparément. &lt;<em>number</em>&gt; boîtes aux lettres n'ont pas été traitées par manque de temps.</p>
> [!NOTE]
> L'Assistant Dossier géré reprendra là où il en était lors de sa prochaine exécution.

</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Service &lt;<em>service</em>&gt;. Impossible d'enregistrer l'avancement de &lt;<em>service</em>&gt; pour la base de données &lt;<em>database</em>&gt;. (L’Assistant n’a pas pu enregistrer là où il s’est arrêté de manière à pouvoir reprendre au même endroit au redémarrage.) L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; n’a pas pu démarrer pour la base de données &lt;<em>database</em>&gt;. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; pour la base de données &lt;<em>database</em>&gt; traite une requête sur demande. Il existe &lt;<em>number</em>&gt; boîtes aux lettres à traiter.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; pour la base de données &lt;<em>database</em>&gt; a terminé une requête sur demande. &lt;<em>number</em>&gt; boîtes aux lettres sur &lt;<em>number</em>&gt; ont été traitées. &lt;<em>number</em>&gt; boîtes aux lettres ont été ignorées en raison d'erreurs.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; n'a pas pu démarrer le traitement de la fenêtre de temps sur la base de données &lt;<em>database</em>&gt;. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; a ignoré &lt;<em>number</em>&gt; boîtes aux lettres sur la base de données &lt;<em>database</em>&gt;. Boîtes aux lettres : &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; n'a pas pu démarrer le traitement à la demande sur la base de données &lt;<em>database</em>&gt;. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>Assistants</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; a interrompu le processus &lt;<em>number</em>&gt; fois lors du traitement de la boîte aux lettres &lt;<em>mailbox</em>&gt; sur la base de données &lt;<em>database</em>&gt;. Cette boîte aux lettres ne sera plus traitée dans la fenêtre de temps requise ou la requête sur demande. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; a interrompu le processus &lt;<em>number</em>&gt; fois lors du traitement de la boîte aux lettres &lt;<em>mailbox</em>&gt; sur la base de données &lt;<em>database</em>&gt;. L'exception suivante a provoqué l'erreur : &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; pour la base de données &lt;<em>database</em>&gt; a reçu une requête sur demande. Toutefois, il n'existe aucune boîte aux lettres à traiter.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>Assistants</p></td>
<td><p>Informations</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt; a arrêté les opérations basées sur l’heure pour l’Assistant Dossier géré sur la base de données &lt;<em>database</em>&gt;.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>Assistants</p></td>
<td><p>Avertissement</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; n’a pas pu traiter &lt;<em>number</em>&gt; boîtes aux lettres par manque de temps.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>Assistants</p></td>
<td><p>Erreur</p></td>
<td><p>LogAlways</p></td>
<td><p>Service &lt;<em>service</em>&gt;. Une exception s'est produite lors du traitement d'un appel RPC. Méthode : &lt;<em>method</em>&gt;, Exception: &lt;<em>exception</em>&gt;</p></td>
</tr>
</tbody>
</table>

