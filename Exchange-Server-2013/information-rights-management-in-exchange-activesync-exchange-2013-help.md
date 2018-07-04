---
title: 'Gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50479493
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les professionnels de l’information utilisent fréquemment la messagerie pour échanger des informations confidentielles. Pour sécuriser ces informations, les organisations peuvent utiliser la gestion des droits relatifs à l’information (IRM) afin d’appliquer une protection permanente au contenu de la messagerie. Étant donné que les appareils mobiles sont de plus en plus utilisés pour accéder à la messagerie électronique, il est important que les utilisateurs des appareils mobiles soient en mesure de créer et d’utiliser du contenu protégé par IRM.

**Contenu de cette rubrique**

Protection IRM mobile dans Exchange 2013

Conditions requises

Sécurité

Activation d’IRM dans Exchange ActiveSync

Souhaitez-vous rechercher les tâches de gestion liées à IRM ? Voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Protection IRM mobile dans Exchange 2013

Dans Exchange 2013, IRM dans Microsoft Exchange ActiveSync permet à vos utilisateurs d’accéder aux fonctionnalités IRM complètes sur n’importe quel appareil Exchange ActiveSync pris en charge, sans avoir à configurer d’autorisations AD RMS ou à connecter l’appareil à un ordinateur pour activer IRM dessus. De plus, l’appareil mobile n’a pas besoin d’exécuter Windows. Exchange ActiveSync est concédé sous licence par Microsoft aux fabricants d’appareils mobiles, aux fabricants d’ordinateurs OEM et d’autres. Pour connaître la liste des détenteurs de licence Exchange ActiveSync actuels, consultez la rubrique Exchange ActiveSync Protocol de la page [Microsoft Technology Licensing](https://go.microsoft.com/fwlink/p/?linkid=198562).

À l’aide d’IRM dans Exchange ActiveSync, les utilisateurs d’appareils mobiles peuvent :

  - Créer des messages protégés par IRM.

  - Lire des messages protégés par IRM.

  - Répondre à des messages protégés par IRM et les transférer.

Protection IRM mobile dans Exchange 2013

## Conditions requises

Les conditions suivantes s’appliquent :

  - Les serveurs d’accès au client de votre organisation doivent exécuter Exchange 2010 SP1 ou version ultérieure.

  - Un serveur AD RMS doit être déployé dans votre organisation.

  - La technologie IRM doit être activée pour les messages internes. Ceci est une condition préalable qui s’applique à toutes les fonctionnalités IRM d’Exchange 2010. Pour plus d’informations, voir [Activer ou désactiver la technologie IRM pour les messages internes](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Lorsque vous activez IRM dans Exchange ActiveSync, il est recommandé d’utiliser les paramètres de stratégie d’Exchange ActiveSync illustrés dans le tableau ci-dessous pour mieux sécuriser les appareils mobiles.

  - Les appareils qui prennent en charge le protocole Exchange ActiveSync version 14.1, notamment les appareils Windows Phone, peuvent prendre en charge les fonctionnalités IRM dans Exchange ActiveSync. L’application de messagerie mobile de l’appareil doit prendre en charge la balise RightsManagementInformation définie dans Exchange ActiveSync version 14.1.

Protection IRM mobile dans Exchange 2013

## Sécurité

Lorsque vous activez IRM dans Exchange ActiveSync, le serveur d’accès au client déchiffre les messages protégés par IRM avant de rendre les messages accessibles à l’appareil mobile pris en charge. Lors de la synchronisation, les messages protégés par IRM se trouvent sur l’appareil mobile dans un format non chiffré. La protection IRM est appliquée par l’application cliente de messagerie compatible avec IRM sur l’appareil mobile.

IRM dans Exchange ActiveSync ne déchiffre pas les pièces jointes protégées par IRM sur le serveur d’accès au client. L’accès aux fichiers protégés par IRM s’effectue par l’application utilisée pour créer ou afficher le fichier. Par exemple, sur un appareil Windows Phone, la protection IRM pour les fichiers Microsoft Office est appliquée par [Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121). Pour accéder aux fichiers Office protégés par IRM, les utilisateurs doivent connecter leur appareil à un ordinateur, puis activer Office Mobile avec le serveur RMS.

Lorsque vous activez IRM dans Exchange ActiveSync, il est recommandé d’utiliser les paramètres de stratégie d’Exchange ActiveSync illustrés dans le tableau ci-dessous pour mieux sécuriser les appareils mobiles.

### Paramètres de stratégie d’Exchange ActiveSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Configuration à l’aide de l’Assistant Nouvelle stratégie de boîte aux lettres Exchange ActiveSync</th>
<th>Configuration à l’aide de la cmdlet New-ActiveSyncMailboxPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Demandez que l’utilisateur entre un mot de passe pour accéder aux informations sur son appareil mobile.</p></td>
<td><p>Cochez la case <strong>Exiger un mot de passe</strong>.</p></td>
<td><p>Définissez le paramètre <em>DevicePasswordEnabled</em> sur <code>$true</code>.</p></td>
</tr>
<tr class="even">
<td><p>Activez le chiffrement pour l’appareil mobile.</p></td>
<td><p>Cochez la case <strong>Exiger un mot de passe</strong>, puis la case <strong>Exiger le chiffrement du périphérique</strong>.</p></td>
<td><p>Définissez le paramètre <em>RequireDeviceEncryption</em> sur <code>$true</code>.</p>
> [!NOTE]
> Lorsque vous définissez le paramètre <em>RequireDeviceEncryption</em> sur <code>$true</code>, les appareils mobiles qui ne prennent pas en charge le chiffrement ne parviendront pas à se connecter.

</td>
</tr>
<tr class="odd">
<td><p>N’autorisez pas les appareils mobiles non configurables à se synchroniser avec le serveur Exchange.</p></td>
<td><p>Décochez la case <strong>Autoriser les périphériques non configurables</strong>.</p></td>
<td><p>Définissez le paramètre <em>AllowNonProvisionableDevices</em> sur <code>$false</code>.</p></td>
</tr>
</tbody>
</table>


Pour en savoir plus, voir [Stratégies de boîte aux lettres d'appareil mobile](mobile-device-mailbox-policies-exchange-2013-help.md).

Protection IRM mobile dans Exchange 2013

## Activation d’IRM dans Exchange ActiveSync

Pour activer IRM dans Exchange ActiveSync, procédez comme suit :

1.  Ajoutez la boîte aux lettres de fédération (une boîte aux lettres système créée par le programme d’installation d’Exchange 2013 et Exchange 2010) au groupe de super utilisateurs dans AD RMS. Cela permet aux serveurs Exchange 2013 et Exchange 2010 d’accéder aux messages protégés par IRM.  Pour plus d’informations, voir [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

2.  Utilisez la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)) dans l’environnement de ligne de commande Exchange Management Shell pour activer IRM sur le serveur d’accès au client. Cette opération active la gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync et dans Microsoft OfficeOutlook Web App pour votre organisation. Pour plus d’informations, voir [Activer ou désactiver la gestion des droits relatifs à l’information (IRM) sur les serveurs d’accès au client](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

Protection IRM mobile dans Exchange 2013

