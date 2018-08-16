---
title: "Stratégies de boîte aux lettres d'appareil mobile: Exchange 2013 Help"
TOCTitle: Stratégies de boîte aux lettres d'appareil mobile
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50478713
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Stratégies de boîte aux lettres d'appareil mobile

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-06-16_

Dans MicrosoftExchange Server 2013, vous pouvez créer des stratégies de boîte aux lettres d’appareil mobile pour appliquer un ensemble commun de stratégies ou de paramètres de sécurité à un ensemble d’utilisateurs. Après avoir déployé Exchange ActiveSync dans votre organisation Exchange 2013, vous pouvez créer des stratégies de boîte aux lettres d'appareil mobile ou modifier des stratégies existantes. Une stratégie de boîte aux lettres d'appareil mobile par défaut est créée lors de l'installation d'Exchange 2013. Cette stratégie de boîte aux lettres d'appareil mobile par défaut est automatiquement attribuée à tous les utilisateurs.

> [!NOTE]
> Les téléphones mobiles Windows Phone 7 ne prennent en charge qu'un sous-ensemble de tous les paramètres de stratégie de boîte aux lettres Exchange ActiveSync. Pour une liste complète, consultez la rubrique Synchronisation de Windows Phone 7.


> [!WARNING]
> Le lecteur d’empreintes digitales d’iOS7 n’est pas pris en charge comme mot de passe d’appareil. Si vous activez le lecteur d’empreintes digitales pour sécuriser votre appareil iOS7, vous devrez tout de même créer et entrer un mot de passe si les stratégies de boîte aux lettres de votre appareil mobile en exigent un.


## Présentation des stratégies de boîte aux lettres d'appareil mobile

Vous pouvez utiliser les stratégies de boîte aux lettres d'appareil mobile pour gérer différents paramètres. Ces algorithmes sont les suivants :

  - exiger un mot de passe

  - spécifier la longueur minimale du mot de passe

  - exiger l'utilisation d'un nombre ou d'un caractère spécial dans le mot de passe

  - déterminer la durée maximale d'inactivité d'un appareil avant d'obliger l'utilisateur à entrer une nouvelle fois son mot de passe

  - nettoyer un appareil après un nombre spécifique de saisies de mot de passe infructueuses

Pour plus d'informations sur tous les paramètres que vous pouvez configurer, consultez la rubrique Paramètres de stratégies d'appareil mobile.

## Gestion des stratégies de boîte aux lettres Exchange ActiveSync

Vous pouvez créer des stratégies de boîte aux lettres d'appareil mobile dans le Centre d'administration Exchange (CAE) ou dans l'environnement de ligne de commande Exchange Management Shell. Si vous créez une stratégie dans le CAE, vous ne pouvez configurer qu'un sous-ensemble des paramètres disponibles. Vous pouvez configurer le reste des paramètres à l'aide de l'environnement de ligne de commande Exchange Management Shell.

## Synchronisation de Windows Phone 7

Si votre organisation utilise des téléphones mobiles Windows Phone 7, des problèmes de synchronisation se produiront si certaines propriétés de la stratégie de boîte aux lettres Exchange ActiveSync sont configurées. Pour permettre la synchronisation des téléphones mobiles Windows Phone 7 avec une boîte aux lettres Exchange, définissez la propriété **AllowNonProvisionableDevices** sur True ou configurez uniquement les propriétés de stratégie de boîte aux lettres Exchange ActiveSync suivantes :

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

## Paramètres de stratégie de boîte aux lettres d'appareil mobile

Le tableau suivant résume les paramètres que vous pouvez spécifier à l'aide de stratégies de boîte aux lettres d'appareil mobile.

### Paramètres de stratégie de boîte aux lettres d'appareil mobile

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoriser Bluetooth</p></td>
<td><p>Ce paramètre indique si un appareil mobile accepte les connexions Bluetooth. Les options disponibles sont Désactiver, Mains libres uniquement et Autoriser. La valeur par défaut est Autoriser. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser le navigateur</p></td>
<td><p>Ce paramètre indique si Pocket Internet Explorer est autorisé sur l'appareil mobile. Ce paramètre n'affecte pas les navigateurs tiers installés sur l'appareil mobile. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser l'appareil photo</p></td>
<td><p>Ce paramètre indique s'il est possible d'utiliser l'appareil photo de l'appareil mobile. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser la messagerie client</p></td>
<td><p>Ce paramètre indique si l'utilisateur de l'appareil mobile peut configurer un compte de messagerie électronique personnel (POP3 ou IMAP4) sur l'appareil mobile. La valeur par défaut est <code>$true</code>. Ce paramètre ne contrôle pas l’accès aux comptes de messagerie électronique utilisant des programmes tiers de messagerie électronique d’appareil mobile. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser la synchronisation du bureau</p></td>
<td><p>Ce paramètre indique si l'appareil mobile peut être synchronisé avec un ordinateur par l'intermédiaire d'un câble, de la technologie Bluetooth ou d'une connexion IrDA. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser la gestion de périphériques externes</p></td>
<td><p>Ce paramètre spécifie si un programme de gestion de périphériques externes est autorisé à gérer l'appareil mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser la messagerie HTML</p></td>
<td><p>Ce paramètre spécifie si la messagerie électronique synchronisée avec l'appareil mobile peut être au format HTML. Si ce paramètre est défini sur <code>$false</code>, tous les messages électroniques sont convertis en texte brut.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser le partage Internet</p></td>
<td><p>Ce paramètre indique si l'appareil mobile peut être utilisé comme modem pour un bureau ou un ordinateur portable. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>Ce paramètre spécifie si les connexions infrarouges vers l'appareil mobile sont autorisées. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser une mise à jour Mobile OTA</p></td>
<td><p>Ce paramètre indique s'il est possible d'envoyer les paramètres de stratégie de boîte aux lettres d'appareil mobile sur l'appareil mobile via une connexion de données cellulaire. La valeur par défaut est <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser les périphériques non configurables</p></td>
<td><p>Ce paramètre indique si des appareils mobiles qui ne prennent pas en charge l'application de tous les paramètres de stratégie sont autorisés à se connecter à Exchange 2013 via Exchange ActiveSync. Autoriser les appareils mobiles non configurables peut avoir des conséquences sur la sécurité. Par exemple, certains appareils non configurables peuvent ne pas être en mesure de mettre en œuvre les exigences de l’organisation en matière de mots de passe.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser les messages au format POP/IMAP</p></td>
<td><p>Ce paramètre spécifie si l'utilisateur peut configurer un compte de messagerie électronique POP3 ou IMAP4 sur l'appareil mobile. La valeur par défaut est <code>$true</code>. Ce paramètre ne régit pas l’accès via des programmes de messagerie tiers.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser le bureau à distance</p></td>
<td><p>Ce paramètre spécifie si l'appareil mobile peut initier une connexion Bureau à distance. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser mot de passe simple</p></td>
<td><p>Ce paramètre active ou désactive la possibilité d'utiliser un mot de passe simple, comme 1111 ou 1234. La valeur par défaut est <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser la négociation d'algorithme de chiffrement S/MIME</p></td>
<td><p>Le paramètre spécifie si l’application de messagerie sur l’appareil mobile peut négocier l’algorithme de chiffrement au cas où le certificat d’un destinataire ne prendrait pas en charge l’algorithme de chiffrement spécifié.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser les certificats logiciels S/MIME</p></td>
<td><p>Ce paramètre spécifie si les certificats logiciels S/MIME sont autorisés sur l'appareil mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser les cartes de stockage</p></td>
<td><p>Ce paramètre spécifie si l'appareil mobile peut accéder aux informations stockées sur une carte de stockage. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser la messagerie texte</p></td>
<td><p>Ce paramètre indique si l'utilisation de la messagerie texte de l'appareil mobile est autorisée. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser les applications non signées</p></td>
<td><p>Ce paramètre indique si des applications non signées peuvent être installées sur l'appareil mobile. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Autoriser les packages d'installation non signés</p></td>
<td><p>Ce paramètre indique si des packages d'installation non signés peuvent être exécutés sur l'appareil mobile. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="odd">
<td><p>Autoriser Wi-Fi</p></td>
<td><p>Ce paramètre indique si l'accès Internet sans fil est autorisé sur l'appareil mobile. La valeur par défaut est <code>$true</code>. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Mot de passe alphanumérique requis</p></td>
<td><p>Ce paramètre requiert qu'un mot de passe contienne des caractères numériques et non numériques. La valeur par défaut est <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Liste d'applications approuvées</p></td>
<td><p>Ce paramètre indique si une liste d'applications approuvées peut être exécutée sur l'appareil mobile. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p>Pièces jointes activées</p></td>
<td><p>Ce paramètre permet le téléchargement de pièces jointes sur l'appareil mobile. La valeur par défaut est <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Chiffrement de périphérique activé</p></td>
<td><p>Ce paramètre active le chiffrement sur l'appareil mobile. Tous les appareils mobiles ne peuvent pas appliquer le chiffrement. Pour plus d'informations, consultez la documentation du périphérique et du système d'exploitation mobile.</p></td>
</tr>
<tr class="even">
<td><p>Intervalle d'actualisation de stratégie de l'appareil</p></td>
<td><p>Ce paramètre indique la fréquence de transmission de la stratégie de boîte aux lettres de l'appareil mobile du serveur à l'appareil mobile.</p></td>
</tr>
<tr class="odd">
<td><p>IRM activé</p></td>
<td><p>Ce paramètre indique si la gestion des droits relatifs à l'information (IRM) est activée sur l'appareil mobile.</p></td>
</tr>
<tr class="even">
<td><p>Taille de pièce jointe maximale</p></td>
<td><p>Ce paramètre commande la taille maximale des pièces jointes téléchargeables sur l'appareil mobile. La valeur par défaut est « illimité ».</p></td>
</tr>
<tr class="odd">
<td><p>Filtre d'âge maximal du calendrier</p></td>
<td><p>Ce paramètre spécifie la plage maximale de jours de calendrier qui peut être synchronisée avec l'appareil mobile. Les valeurs suivantes sont acceptées :</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Filtre d'âge maximal du courrier électronique</p></td>
<td><p>Le paramètre indique le nombre maximal de jours d'éléments de messagerie pouvant être synchronisés avec l'appareil mobile. Les valeurs suivantes sont acceptées :</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Taille maximale de troncature de corps de message électronique</p></td>
<td><p>Le paramètre indique la taille maximale qui délimite des messages électroniques lors de la synchronisation avec l'appareil mobile. La valeur est stockée en kilo-octets (Ko).</p></td>
</tr>
<tr class="even">
<td><p>Taille maximale de troncature de corps HTML du message</p></td>
<td><p>Ce paramètre indique la taille maximale qui délimite des messages électroniques HTML lors de la synchronisation avec l'appareil mobile. La valeur est stockée en kilo-octets (Ko).</p></td>
</tr>
<tr class="odd">
<td><p>Verrouillage de temps d'inactivité maximal</p></td>
<td><p>Ce paramètre indique la période de temps pendant laquelle l'appareil mobile peut rester inactif avant qu'un mot de passe ne soit requis pour le réactiver. Vous pouvez entrer un intervalle quelconque compris entre 30 secondes et 1 heure. La valeur par défaut est 15 minutes.</p></td>
</tr>
<tr class="even">
<td><p>Nombre maximal d'échecs de mot de passe</p></td>
<td><p>Ce paramètre spécifie le nombre de tentatives dont dispose un utilisateur pour entrer le mot de passe correct pour l'appareil mobile. Vous pouvez entrer un nombre compris entre 4 et 16. La valeur par défaut est 8.</p></td>
</tr>
<tr class="odd">
<td><p>Nombre minimum de caractères complexes du mot de passe</p></td>
<td><p>Ce paramètre indique le nombre minimal de jeux de caractères complexes requis dans le mot de passe de l’appareil mobile. Un caractère complexe est tout sauf une lettre. Les jeux de caractères sont des lettres minuscules, des lettres majuscules, des numéros et des caractères spéciaux (tels que les points d’exclamation).</p></td>
</tr>
<tr class="even">
<td><p>Longueur minimale du mot de passe</p></td>
<td><p>Ce paramètre indique le nombre minimal de caractères requis dans le mot de passe de l'appareil mobile. Vous pouvez entrer un nombre compris entre 1 et 16. La valeur par défaut est 4.</p></td>
</tr>
<tr class="odd">
<td><p>Mot de passe activé</p></td>
<td><p>Ce paramètre active le mot de passe de l'appareil mobile.</p></td>
</tr>
<tr class="even">
<td><p>Expiration du mot de passe</p></td>
<td><p>Ce paramètre permet à l'administrateur de configurer un délai à l'issue duquel un mot de passe d'appareil mobile doit être modifié.</p></td>
</tr>
<tr class="odd">
<td><p>Historique du mot de passe</p></td>
<td><p>Ce paramètre indique le nombre d'anciens mots de passe qui peuvent être stockés dans la boîte aux lettres d'un utilisateur. Un utilisateur ne peut pas réutiliser un mot de passe stocké.</p></td>
</tr>
<tr class="even">
<td><p>Récupération du mot de passe activée</p></td>
<td><p>Lorsque ce paramètre est activé, l'appareil mobile génère un mot de passe de récupération qui est envoyé au serveur. Si l'utilisateur oublie le mot de passe de son appareil mobile, le mot de passe de récupération lui permet de déverrouiller l'appareil mobile et de créer un mot de passe.</p></td>
</tr>
<tr class="odd">
<td><p>Exiger le chiffrement de l'appareil</p></td>
<td><p>Ce paramètre indique si le chiffrement du périphérique est requis. Si le paramètre est défini sur <code>$true</code>, l'appareil mobile doit pouvoir prendre en charge et implémenter le chiffrement afin d'être synchronisé avec le serveur.</p></td>
</tr>
<tr class="even">
<td><p>Exiger des messages S/MIME chiffrés</p></td>
<td><p>Ce paramètre indique si les messages S/MIME doivent être chiffrés. La valeur par défaut est <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Exiger un algorithme S/MIME de chiffrement</p></td>
<td><p>Ce paramètre indique quels algorithmes requis sont à utiliser lors du chiffrement d'un message S/MIME.</p></td>
</tr>
<tr class="even">
<td><p>Exiger la synchronisation manuelle en itinérance</p></td>
<td><p>Ce paramètre indique si l'appareil mobile doit effectuer une synchronisation manuelle en mode itinérance. Autoriser la synchronisation automatique en itinérance entraîne fréquemment des coûts supplémentaires pour le plan de données de l'appareil mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Exiger un algorithme S/MIME signé</p></td>
<td><p>Ce paramètre indique les algorithmes requis à utiliser lors de la signature d'un message.</p></td>
</tr>
<tr class="even">
<td><p>Exiger des messages S/MIME signés</p></td>
<td><p>Ce paramètre indique si l'appareil mobile doit envoyer des messages S/MIME signés.</p></td>
</tr>
<tr class="odd">
<td><p>Exiger le chiffrement de la carte de stockage</p></td>
<td><p>Ce paramètre indique si la carte de stockage doit être chiffrée. Les systèmes d'exploitation d'appareil mobile ne prennent pas tous en charge le chiffrement des cartes de stockage. Pour plus d'informations, consultez la documentation de votre appareil mobile et du système d'exploitation mobile.</p></td>
</tr>
<tr class="even">
<td><p>Liste d'applications InROM non approuvées</p></td>
<td><p>Ce paramètre spécifie une liste d'applications qui ne peuvent pas être exécutées dans la mémoire ROM. La licence d’accès client Exchange Enterprise est nécessaire pour modifier les valeurs de ce paramètre.</p></td>
</tr>
</tbody>
</table>

