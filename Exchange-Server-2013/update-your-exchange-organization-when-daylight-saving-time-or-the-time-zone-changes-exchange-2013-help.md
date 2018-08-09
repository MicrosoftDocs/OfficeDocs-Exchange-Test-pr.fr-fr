---
title: 'Màj de l’org. Exchange lorsque l’heure d’été ou le fuseau horaire change'
TOCTitle: Mise à jour de l’organisation Exchange lorsque l’heure d’été ou le fuseau horaire change
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 70087267
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mise à jour de l’organisation Exchange lorsque l’heure d’été ou le fuseau horaire change

 

_**Sapplique à :** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Si le pays de résidence de votre organisation ou de certains de vos utilisateurs a modifié sa stratégie de reconnaissance de l'heure d’été, ou a modifié le décalage horaire local par rapport au temps universel coordonné (UTC), vous devez peut-être mettre à jour Microsoft Windows, Microsoft Exchange, Microsoft Outlook ou d’autres programmes pour intégrer ces modifications.

Pour plus d’informations sur les modifications de l’heure d’été, consultez la page [Aide et support relatifs à l’heure d’été](https://go.microsoft.com/fwlink/p/?linkid=99640). Accédez également aux sites d’aide de vos autres fournisseurs logiciels pour vérifier s’ils exigent des mises à jour supplémentaires.

Même si votre fuseau horaire n’a pas changé, votre ordinateur doit être capable d’effectuer des calculs corrects d’heure et de date concernant les événements que vous organisez avec d’autres utilisateurs de par le monde.

Il vous faut donc installer au plus vite les mises à jour de fuseau horaire afin de réduire le nombre d’événements organisés (rendez-vous et réunions) pendant la transition du changement d’heure.

## Comment procéder ?

## Étape 1 : Installez la mise à jour Windows de passage à l'heure d’été sur tous les ordinateurs

Du fait que le système d’authentification Office 365 est mis à jour lors du passage à l'heure d’été ou d’un changement de fuseau horaire, tous les ordinateurs clients Office 365 doivent être mis à jour pour ne pas rencontrer de problèmes de connexion.

  - Assurez-vous que tous les ordinateurs clients et de bureau ont installé la mise à jour Windows de passage à l’heure d’été. Pour plus d’informations, consultez la rubrique relative à la [procédure de configuration de l’heure d’été pour les systèmes d’exploitation Microsoft Windows](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=914387).

## Étape 2 : Installez la mise à jour Windows de passage à l'heure d’eté sur tous les serveurs

1.  Mettez à jour tous vos serveurs locaux avec la mise à jour Windows de passage à l'heure d’été.

2.  Si vous utilisez Office 365, mettez à jour tous les serveurs interagissant avec le système d’authentification Office 365 (tels que les serveurs DirSync ou AD FS). Ces serveurs doivent être mis à jour tout en assurant un temps de disponibilité.

**Remarque**   Si vous mettez à jour des clusters de serveur, assurez-vous de suivre le processus habituel de mise à jour des clusters. Mettez d’abord à jour le serveur passif, basculez ensuite vers le serveur passif (qui devient actif), puis mettez à jour le serveur précédemment actif (devenu passif). Pour plus d’informations sur la mise à jour des clusters de serveur et des clusters de service à haute disponibilité, consultez la page Update Exchange Server Clusters and High Availability Servers et la rubrique relative à la [mise à jour des clusters de basculement Windows Server](https://support.microsoft.com/fr-fr/kb/174799).

## Étape 3 : Mettez à jour Exchange et Outlook, si nécessaire, sur les ordinateurs clients et de bureau

1.  Si vos utilisateurs utilisent Outlook 2007 ou des clients plus anciens, choisissez les outils de fuseau horaire Exchange ou Outlook à exécuter, à l’aide du tableau ci-dessous.

2.  Envoyez un message à tous vos utilisateurs devant mettre à jour leurs ordinateurs en leur fournissant un lien vers l’outil approprié.

Le tableau suivant indique à quel moment les utilisateurs doivent exécuter l’[outil de mise à jour de calendrier Exchange](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879) ou l’[outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667). Déterminez la version des serveurs que votre organisation utilise, puis les programmes clients que vos utilisateurs utilisent.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Version du client</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>Version de l’organisation</strong></p></td>
<td><p><strong>Outlook 2003 ou Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Organisation locale Exchange 2003</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Outil de calendrier Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="even">
<td><p><strong>Organisation locale Exchange 2007</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Outil de calendrier Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="odd">
<td><p><strong>Organisation locale Exchange 2010</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Outil de calendrier Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="even">
<td><p><strong>Organisation locale Exchange 2013</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-S (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a></p></td>
<td><p>Aucune action n'est requise</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a> (non pris en charge par Outlook 2003)</p></td>
<td><p>Aucune action requise</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Outil de mise à jour des données de fuseau horaire pour Microsoft Office Outlook</a> (non pris en charge par Outlook 2003)</p></td>
<td><p>Aucune action requise</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

