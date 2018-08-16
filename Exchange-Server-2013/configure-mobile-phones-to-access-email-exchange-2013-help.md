---
title: 'Config. de l’accès à la messag. pour téléphones mobiles: Exchange 2013 Help'
TOCTitle: Configuration de l’accès à la messagerie pour les téléphones mobiles
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52057114
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration de l’accès à la messagerie pour les téléphones mobiles

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-12_

Vous pouvez configurer un téléphone mobile, tel qu'un téléphone Windows, de façon à pouvoir utiliser MicrosoftExchange ActiveSync. Vous devez effectuer cette procédure sur chaque téléphone mobile appartenant à votre organisation.

## Conditions préalables

  - Vous avez pris connaissance de la documentation du fabricant du téléphone mobile que vous voulez configurer.

  - Exchange ActiveSync est activé dans votre organisation.

> [!NOTE]
> Pour obtenir des informations spécifiques de l’appareil relatives à la configuration de la messagerie Microsoft Exchange sur un téléphone ou une tablette, consultez la rubrique <a href="https://support.office.com/fr-fr/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">Configurer un appareil mobile à l’aide d’Office 365 pour les entreprises</a>.


## Configurer un téléphone mobile pour utiliser Exchange ActiveSync

La plupart des téléphones et appareils mobiles peuvent utiliser la découverte automatique pour configurer le client de messagerie mobile de manière à utiliser Exchange ActiveSync. Vous devez être en possession de deux informations pour configurer un compte de messagerie sur la plupart des téléphones mobiles :

  - Adresse de messagerie de l’utilisateur

  - Mot de passe de l’utilisateur

Si le téléphone mobile ne peut pas contacter le serveur Exchange automatiquement via la découverte automatique, vous devez configurer le téléphone mobile manuellement. Pour configurer manuellement le téléphone, vous avez besoin de l’adresse de messagerie et du mot de passe de l’utilisateur, ainsi que du nom du serveur Exchange ActiveSync. Dans de nombreuses organisations, le nom du serveur Exchange ActiveSync est identique au nom du serveur Outlook Web App sans /owa, par exemple, mail.contoso.com.

## Synchronisation avec Windows Phone

Si vous configurez un téléphone mobile Windows Phone afin de le synchroniser avec une boîte aux lettres Exchange utilisant Exchange ActiveSync, seul un sous-ensemble des paramètres de stratégie de boîte aux lettres de l'appareil mobile est pris en charge. Ces paramètres de stratégie sont détaillés dans la rubrique [Stratégies de boîte aux lettres d’appareil mobile prises en charge pour des téléphones et appareils Windows Phone](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md).

Si vous configurez des paramètres de stratégie de boîte aux lettres d’appareil mobile qui ne sont pas pris en charge par la version de Windows Phone que vous utilisez, vous devez également définir le paramètre de stratégie **AllowNonProvisionableDevices** sur True ou créer une stratégie de boîte aux lettres d’appareil mobile distincte pour les appareils Windows Phone.

