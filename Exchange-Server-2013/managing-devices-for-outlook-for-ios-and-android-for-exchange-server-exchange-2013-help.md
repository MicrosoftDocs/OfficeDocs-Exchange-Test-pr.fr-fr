---
title: 'Gestion d’appareils pour Outlook pour iOS et Android dans Exchange Server: Exchange 2013 Help'
TOCTitle: Gestion d’appareils pour Outlook pour iOS et Android dans Exchange Server
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70086937
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion d’appareils pour Outlook pour iOS et Android dans Exchange Server

 

_**Sapplique à :**Exchange Server 2010, Exchange Server 2013_

_**Dernière rubrique modifiée :**2018-04-01_

**Résumé** : Cet article décrit comment Exchange ActiveSync vous permet de gérer des appareils mobiles avec Outlook pour iOS et Android dans votre organisation Exchange locale.

Microsoft recommande l’utilisation d’Exchange ActiveSync pour gérer les appareils mobiles utilisés pour accéder aux boîtes aux lettres Exchange dans votre environnement local. Exchange ActiveSync est un protocole de synchronisation de Microsoft Exchange qui autorise les téléphones mobiles à accéder aux informations d’une organisation situées sur un serveur exécutant Microsoft Exchange.

Cet article décrit certaines fonctionnalités d’Exchange ActiveSync et des scénarios pour les appareils mobiles exécutant Outlook pour iOS et Android. Des informations complètes sur le protocole de synchronisation de Microsoft Exchange sont disponibles dans [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md). Vous trouverez également des informations sur [le blog Office](https://go.microsoft.com/fwlink/p/?linkid=62392) concernant l’application de mots de passe et d’autres avantages liés à l’utilisation d’Exchange ActiveSync sur des appareils exécutant Outlook pour iOS et Android.

## Code confidentiel et chiffrement de l’appareil

Si la stratégie Exchange ActiveSync de votre organisation exige que les utilisateurs entrent un mot de passe sur leur appareil mobile pour synchroniser des e-mails, Outlook applique cette stratégie au niveau de l’appareil. Cela fonctionne différemment sur les appareils iOS et Android, selon les contrôles fournis par Apple et Google.

Sur les appareils iOS, Outlook vérifie qu’un code secret ou un code confidentiel est correctement défini. Si aucun code secret n’est défini, Outlook invite les utilisateurs à créer un code secret dans les paramètres d’iOS. Tant que le code secret n’est pas défini, l’utilisateur ne peut pas accéder à Outlook pour iOS.

Outlook pour iOS fonctionne uniquement sur iOS 8.0 ou version ultérieure. Le chiffrement est intégré dans les appareils. Outlook l’utilise dès que le code secret est activé pour chiffrer toutes les données qu’Outlook stocke localement sur l’appareil iOS. Par conséquent, les appareils iOS protégés par un code confidentiel seront chiffrés, qu’une stratégie ActiveSync l’exige ou non.

Sur les appareils Android, Outlook doit appliquer les règles de verrouillage de l’écran. De plus, Google fournit des contrôles qui permettent à Outlook pour Android de respecter les stratégies d’Exchange concernant la longueur et la complexité des mots de passe, ainsi que le nombre de tentatives de déverrouillage de l’écran autorisé avant de réinitialiser le téléphone. Outlook pour Android encourage également le chiffrement du stockage s’il n’est pas activé. Des instructions détaillées sont proposées aux utilisateurs pour l’activer.

Les appareils iOS et Android qui ne prennent pas en charge ces paramètres de sécurité des mots de passe ne pourront pas se connecter à une boîte aux lettres Exchange.

## Réinitialisation à distance avec Exchange ActiveSync

Exchange ActiveSync permet aux administrateurs de réinitialiser des appareils à distance, par exemple s’ils ne sont plus sécurisés. Avec Outlook pour iOS et Android, seule l’application Outlook est réinitialisée à distance, et non tout l’appareil.

Lorsque l’administrateur lance une réinitialisation à distance, celle-ci se produit lors de la prochaine connexion de l’application Outlook à Exchange, dans les secondes suivant la connexion. L’application Outlook se réinitialise et l’ensemble des e-mails, calendriers, contacts et données de fichiers Outlook est supprimé de l’appareil, ainsi que du service Outlook. La réinitialisation n’affecte pas les applications et les informations personnelles de l’utilisateur qui se trouvent en dehors d’Outlook.

Étant donné qu’Outlook pour iOS et Android s’affiche dans Exchange en tant qu’association d’appareil mobile unique dans la liste des appareils mobiles de l’utilisateur, une demande de réinitialisation à distance supprime les données et les relations de synchronisation de tous les appareils exécutant Outlook (iPhone, iPad, Android) associés à cet utilisateur.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>En raison de l’architecture informatique qui supporte Outlook pour iOS et Android, le résultat de la réinitialisation à distance n’est pas envoyé à Exchange. Même lorsque la réinitialisation à distance est réussie, le statut affiché est <strong>En attente</strong>. Il s’agit d’un problème connu ; une solution est en cours de développement.</td>
</tr>
</tbody>
</table>


## Identificateurs d’appareils et contrôle d’accès

En raison de l’architecture informatique d’Outlook pour iOS et Android, les connexions Outlook apparaissent dans Exchange sous la forme d’un identificateur (ID) unique associé à l’appareil mobile de chaque utilisateur. Ainsi, les contrôles d’accès de l’appareil mobile de l’utilisateur s’appliquent à tous les appareils associés à l’ID de cet appareil. Cette implémentation crée deux conditions qui diffèrent du fonctionnement classique des contrôles d’accès des appareils dans Exchange ActiveSync.

  - **Bloquer** : une règle de blocage bloque Outlook sur tous les appareils et tous les systèmes d’exploitation pris en charge. Vous ne pouvez pas bloquer des appareils ou des systèmes d’exploitation individuels.

  - **Mise en quarantaine** : le processus de mise en quarantaine dépend de l’utilisateur, et non de l’appareil. Lorsque l’appareil d’un utilisateur est libéré de quarantaine, Outlook peut être installé et configuré sur autant d’appareils que vous le souhaitez. Dans la mesure où l’utilisateur a été libéré de quarantaine, tous les nouveaux appareils associés à cet utilisateur ne seront pas mis en quarantaine.

Dès leur mise en place, les stratégies de boîte aux lettres d’appareil mobile s’appliquent à tous les appareils associés. Par conséquent, si vous appliquez un code confidentiel pour une boîte aux lettres spécifique, tous les appareils qui se connecteront à cette boîte aux lettres nécessiteront un code confidentiel.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Étant donné que les ID d’appareil ne sont pas régis par n’importe quel ID d’<em>appareil physique</em>, ils peuvent changer sans préavis. Lorsqu’une modification se produit, elle peut entraîner des conséquences inattendues si les ID d’appareil sont utilisés pour gérer les appareils des utilisateurs, car les appareils « autorisés » existants peuvent être inopinément bloqués ou mis en quarantaine par Exchange. Par conséquent, nous recommandons aux administrateurs de définir uniquement des stratégies d’appareil mobile qui autorisent/bloquent les appareils en fonction du type d’appareil ou du modèle d’appareil.</td>
</tr>
</tbody>
</table>


## FAQ sur la gestion des appareils dans Exchange ActiveSync

Vous trouverez ci-dessous les questions fréquemment posées concernant les mots de passe, les codes confidentiels et les stratégies de chiffrement pour les appareils exécutant Outlook pour iOS et Android.

## L’application de messagerie native d’iOS applique les stratégies d’Exchange ActiveSync concernant les obligations de longueur et de complexité des mots de passe. Pourquoi Outlook ne les applique-t-il pas ?

Outlook utilise les contrôles du développeur d’applications tiers destinés à Microsoft. Nous continuerons d’améliorer cette fonctionnalité dans la mesure où Apple met de plus en plus de contrôles à la disposition des développeurs.

## Pourquoi Outlook pour iOS et Android exige des codes confidentiels au niveau de l’appareil, et non au niveau de l’application ?

Après avoir évalué les fonctionnalités disponibles dans iOS et Android, Microsoft estime que l’application d’un code confidentiel au niveau de l’appareil offre la meilleure expérience aux clients, que ce soit au niveau du confort d’utilisation que de la sécurité. En mettant en place un code confidentiel au niveau de l’application, les utilisateurs devraient entrer deux codes confidentiels différents pour accéder à leurs e-mails, ce qui pourrait nuire à l’expérience de l’utilisateur. Par ailleurs, en mettant en place un code confidentiel au niveau de l’appareil, nous pouvons utiliser des fonctionnalités telles que le chiffrement natif de l’appareil, TouchID sur iOS et Smart Lock sur Android. La réinitialisation à distance est toujours activée au niveau de l’application, ce qui signifie que les applications et les données personnelles des utilisateurs ne sont pas affectées lors de la réinitialisation d’Outlook.

## Fait Outlook pour le chiffrement du périphérique Android de prise en charge ?

Oui, Outlook pour Android prend en charge le cryptage de périphérique via les stratégies de boîte aux lettres Exchange appareil mobile. Toutefois, antérieures à 7.0 Android, la disponibilité et la mise en oeuvre de ce processus varie en fonction du fabricant de matériel et du système d’exploitation Android, qui permettent à l’utilisateur d’annuler pendant le processus de cryptage. Avec les modifications introduite par Google Android 7.0, Outlook pour Android est désormais en mesure de renforcer le cryptage sur les appareils exécutant Android 7.0 ou version ultérieure. Les utilisateurs dont les périphériques exécutent ces systèmes d’exploitation ne sera pas en mesure d’annuler le processus de cryptage.

Même si l’appareil Android n’est pas crypté et un pirate est en possession du périphérique, comme un code confidentiel du périphérique est activé, la base de données Outlook reste inaccessible. Cela est vrai même avec le débogage USB est activé et le SDK Android installé. Si un attaquant tente de la racine de l’appareil pour ignorer le code confidentiel pour accéder à ces informations, le processus racine permet d’effacer tout le stockage périphérique et supprime toutes les données d’Outlook. Si le périphérique est décrypté et associé à une racine par l’utilisateur avant le vol, il est possible pour un intrus d’accéder à la base de données Outlook par l’interface USB de débogage sur le périphérique et connecter le périphérique à un ordinateur avec le SDK Android installé.

