---
title: 'Réinitialisation à distance: Exchange 2013 Help'
TOCTitle: Réinitialisation à distance
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 50479253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réinitialisation à distance

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-09-19_

Les téléphones mobiles, les tablettes et les autres périphériques peuvent stocker des données d’entreprise sensibles et fournir un accès à de nombreuses ressources d’entreprise. Si un périphérique mobile est perdu ou volé, ces données peuvent être compromises. Grâce aux stratégies de boîte aux lettres de périphérique mobile Microsoft Exchange, vous pouvez ajouter un mot de passe obligatoire sur vos périphériques mobiles. Si tel est le cas, les utilisateurs doivent entrer un mot de passe pour accéder à leur périphérique mobile. Outre l’activation d’un mot de passe d’appareil, il est recommandé de configurer vos périphériques mobiles pour qu’un mot de passe soit automatiquement demandé après une période d’inactivité. La combinaison d’un mot de passe de l’appareil et du verrouillage d’inactivité améliore la sécurité de l’accès à vos données d’entreprise.

En plus de ces fonctionnalités, Exchange Server 2013 fournit un service de réinitialisation à distance. Vous pouvez émettre une commande de réinitialisation à distance à partir de l’environnement de ligne de commande Exchange Management Shell ou à partir du Centre d’administration Exchange (CAE). Les utilisateurs peuvent émettre leurs propres commandes de réinitialisation à distance à partir de l’interface utilisateur d’MicrosoftOutlook Web App.

La fonctionnalité de réinitialisation à distance inclut également une fonction de confirmation qui inscrit un cachet horodateur dans les données de l’état de synchronisation de la boîte aux lettres de l’utilisateur. Cet horodatage s’affiche dans Outlook Web App et dans la boîte de dialogue des propriétés du périphérique mobile de l’utilisateur dans le CAE.

> [!NOTE]
> La réinitialisation à distance permet de restaurer les valeurs par défaut des paramètres d’usine d’un téléphone mobile. Bien que le protocole de réinitialisation à distance tel qu’il est implémenté dans Exchange 2013 nécessite uniquement la suppression de données d’entreprise personnelles, tous les fabricants de périphériques mobiles actuels interprètent la commande comme étant une commande supprimant l’ensemble des données contenues dans le téléphone. De nombreux systèmes d’exploitation de périphériques mobiles suppriment aussi toutes les données contenues sur n’importe quelle carte de stockage insérée dans le périphérique mobile. Si vous réalisez une réinitialisation à distance sur un téléphone mobile en votre possession et que vous voulez conserver les données présentes sur la carte de stockage, il est recommandé de retirer cette dernière avant de commencer la réinitialisation à distance.


<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une fois l’opération effectuée, il est très difficile de récupérer les données. Toutefois, aucun processus de suppression des données ne supprime totalement les données résiduelles. Seuls des outils sophistiqués permettent de récupérer les données d’un périphérique mobile.</td>
</tr>
</tbody>
</table>


## Réinitialisation à distance ou réinitialisation locale

La réinitialisation locale est un mécanisme par lequel un périphérique mobile efface les données sans demande de la part du serveur. Si votre organisation a mis en œuvre des stratégies de boîte aux lettres de périphériques mobiles qui spécifient un nombre maximal de tentatives de saisie du mot de passe et que ce nombre maximal est atteint, le périphérique mobile effectue une réinitialisation locale. Le résultat d’une réinitialisation locale est le même que celui d’une réinitialisation à distance. Les paramètres par défaut de l’appareil sont rétablis. Lorsqu’un périphérique effectue une réinitialisation locale, aucune confirmation n’est envoyée au serveur Exchange.

