---
title: 'Fonctions pour les téléphones mobiles et les tablettes: Exchange 2013 Help'
TOCTitle: Fonctionnalités pour les téléphones mobiles et les tablettes
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50555457
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fonctionnalités pour les téléphones mobiles et les tablettes

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les utilisateurs peuvent accéder à leurs informations de messagerie électronique, de calendrier, de contacts et de tâches sur des téléphones mobiles, des tablettes et autres appareils portables via Microsoft Exchange ActiveSync. Vous pouvez également l’utiliser pour configurer leur signatures et réponses automatiques. Une grande variété de téléphones et appareils mobiles utilisent Exchange ActiveSync.

> [!NOTE]
> Même si nous faisons constamment référence à des appareils accédant à Exchange Server 2013 en tant que téléphones mobiles, il existe de nombreux appareils qui peuvent accéder à Exchange 2013 sans être dotés de la fonctionnalité de téléphone cellulaire. Le terme « téléphone mobile » utilisé dans cette documentation englobe également ces périphériques.


## Appareils compatibles Exchange ActiveSync

Les utilisateurs peuvent bénéficier de la richesse des fonctionnalités d’Exchange ActiveSync en sélectionnant des téléphones mobiles compatibles avec Exchange ActiveSync. Ces téléphones mobiles sont proposés par de nombreux fabricants et de nombreux opérateurs. Pour plus d’informations, voir la documentation spécifique du téléphone mobile.

Les téléphones mobiles compatibles avec Microsoft Exchange sont présentés ci-dessous :

  - **Apple** Les produis iPhone, iPod Touch et iPad d’Apple prennent en charge Exchange ActiveSync.

  - **Windows Phone** Windows Phone 8, Windows Phone 7 et les versions précédentes prennent toutes en charge Exchange ActiveSync.

  - **Android** De nombreux téléphones mobiles et tablettes dotés du système d’exploitation Android prennent en charge Exchange ActiveSync. Cependant, ces appareils mobiles peuvent ne pas prendre en charge toutes les stratégies de boîtes aux lettres des appareils mobiles. Pour plus d’informations, consultez la rubrique [Stratégies de boîte aux lettres d'appareil mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

## Fonctionnalités du logiciel Windows Phone

Les téléphones ayant une version du logiciel Windows comme système d’exploitation offrent les meilleures fonctionnalités lors de la synchronisation avec Exchange 2013. Le tableau suivant répertorie les stratégies de boîtes aux lettres des appareils mobiles qui sont accessibles sous Windows Phone 8 et Windows Phone 7.

### Fonctions de Windows Phone 7 et 8

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Système d’exploitation</th>
<th>Fonctionnalités</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 prend en charge les stratégies de boîtes aux lettres des appareils suivants :</p>
<ul>
<li><p>Autoriser un mot de passe d’appareil simple</p></li>
<li><p>Mot de passe alphanumérique requis</p></li>
<li><p>Mot de passe de l’appareil activé</p></li>
<li><p>Expiration du mot de passe de l’appareil</p></li>
<li><p>IRM activé</p></li>
<li><p>Nombre maximal de tentatives d’entrée du mot de passe de l’appareil ayant échoué</p></li>
<li><p>Verrouillage de temps maximal d’inactivité de l’appareil</p></li>
<li><p>Nombre minimal des caractères complexes du mot de passe</p></li>
<li><p>Longueur minimale du mot de passe de l’appareil</p></li>
<li><p>Exiger le chiffrement de l’appareil</p></li>
<li><p>Effacement à distance</p></li>
</ul>

> [!WARNING]
> Si votre organisation utilise d’autres paramètres de stratégies de boîtes aux lettres des appareils mobiles, vous devez définir la stratégie <strong>Autoriser les périphériques non configurables</strong> à vrai. Ceci peut avoir des incidences sur la sécurité dans votre organisation, en effet d’autres téléphones et appareils mobiles qui ne satisfont pas les exigences de vos paramètres de stratégies d’appareils mobiles seront autorisés à se synchroniser. Pour plus d’informations, consultez la rubrique <a href="mobile-device-mailbox-policies-exchange-2013-help.md">Stratégies de boîte aux lettres d'appareil mobile</a>.

</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Les téléphones mobiles Windows Phone 7 prennent en charge uniquement un sous-ensemble de tous les paramètres de la stratégie de boîtes aux lettres d’Exchange ActiveSync :</p>
<ul>
<li><p>Mot de passe obligatoire</p></li>
<li><p>Longueur minimale du mot de passe</p></li>
<li><p>Verrouillage de temps d’inactivité maximal</p></li>
<li><p>Nombre maximal de tentatives d’entrée du mot de passe de l’appareil ayant échoué</p></li>
<li><p>Autoriser mot de passe simple</p></li>
<li><p>Expiration du mot de passe</p></li>
<li><p>Historique du mot de passe</p></li>
<li><p>Désactiver le stockage amovible</p></li>
<li><p>Désactiver IrDA</p></li>
<li><p>Désactiver la synchronisation du bureau</p></li>
<li><p>Bloquer le bureau à distance</p></li>
<li><p>Bloquer le partage Internet</p></li>
</ul></td>
</tr>
</tbody>
</table>

