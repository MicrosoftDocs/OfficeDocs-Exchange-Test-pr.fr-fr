---
title: 'Mise en quarantaine du courrier indésirable: Exchange 2013 Help'
TOCTitle: Mise en quarantaine du courrier indésirable
ms:assetid: 4535496f-de6a-43df-8e53-c9a97f65cccc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997692(v=EXCHG.150)
ms:contentKeyID: 50478045
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mise en quarantaine du courrier indésirable

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-12_

De nombreuses organisations sont tenues, en vertu d’exigences légales et réglementaires, de conserver ou de remettre tous les messages électroniques légitimes. Dans Microsoft Exchange Server 2013, la mise en quarantaine du courrier indésirable est une fonctionnalité de l’agent de filtrage du contenu qui réduit le risque de perte de messages légitimes. La mise en quarantaine du courrier indésirable fournit un emplacement de stockage temporaire pour les messages identifiés comme courrier indésirable, qui ne doivent pas être remis à une boîte aux lettres d'utilisateur au sein de l'organisation.

Les messages identifiés comme courrier indésirable par l'agent de filtrage du contenu sont consignés dans un rapport de non-remise (NDR) et déposés dans une boîte aux lettres de mise en quarantaine du courrier indésirable dans l'organisation. Vous pouvez gérer les messages déposés dans la boîte aux lettres de mise en quarantaine du courrier indésirable et prendre des mesures appropriées. Par exemple, vous pouvez déléguer des messages ou permettre que les messages marqués comme faux positifs dans le filtrage du courrier indésirable soient routés vers leurs destinataires. En outre, vous pouvez configurer la boîte aux lettres de mise en quarantaine des messages indésirables afin de supprimer automatiquement les messages à l'issue d'une période déterminée.

**Contenu de cette rubrique**

Spam confidence level

Spam quarantine

## Seuil de probabilité de courrier indésirable (SCL)

Quand un utilisateur externe envoie des messages électroniques à un serveur Exchange exécutant les fonctionnalités de blocage du courrier indésirable, ces dernières évaluent de façon cumulée les caractéristiques des messages et agissent comme suit :

  - Les messages suspectés d'être du courrier indésirable sont filtrés.

  - Une valeur leur est attribuée indiquant le niveau de probabilité qu'il s'agisse de courrier indésirable. Cette valeur est stockée avec le message en tant que propriété appelée contrôle d'accès SCL.

La fonctionnalité de mise en quarantaine du courrier indésirable utilise la valeur SCL pour déterminer le niveau de probabilité pour que le message soit un courrier indésirable. La valeur SCL est une valeur numérique comprise entre 0 et 9, avec 0 pour les messages les moins susceptibles d'être du courrier indésirable et 9 pour les messages les plus susceptibles d'être du courrier indésirable.

Vous pouvez configurer la messagerie de telle sorte qu'une certaine valeur SCL entraîne la suppression, le rejet ou la mise en quarantaine du message. La valeur qui déclenche l'un de ces actions est appelée *Seuil de mise en quarantaine SCL*. Au niveau du filtrage du contenu, vous pouvez configurer l'agent de filtrage du contenu pour qu'il base ses actions sur le seuil de mise en quarantaine SCL. Par exemple, vous pouvez définir les conditions suivantes :

  - Le seuil de suppression SCL est défini sur 8.

  - Le seuil de rejet SCL est défini sur 7.

  - Le seuil de mise en quarantaine SCL est défini sur 6.

  - Le seuil de dossier de courrier indésirable SCL est défini sur 5.

En fonction des seuils SCL précédents, tous les messages électroniques dont la valeur SCL est 6 sont déposés dans la boîte aux lettres de mise en quarantaine du courrier indésirable.

Pour plus d’informations, consultez la rubrique [Gérer le filtrage du contenu](manage-content-filtering-exchange-2013-help.md).

Retour au début

## Mise en quarantaine du courrier indésirable

À la réception de messages par le serveur Exchange qui exécute tous les agents de blocage du courrier indésirable par défaut, le filtre de contenu est appliqué comme suit :

  - Si la valeur SCL est supérieur à la valeur de seuil de mise en quarantaine SCL mais inférieure au seuil de suppression ou de rejet SCL, le message est placé dans la boîte aux lettres de mise en quarantaine du courrier indésirable.

  - Si la valeur SCL est inférieure au seuil de mise en quarantaine, le message est déposé dans la boîte de réception du destinataire.

L’administrateur des messages utilise Microsoft Outlook pour surveiller la boîte aux lettres de mise en quarantaine du courrier indésirable afin de détecter d’éventuels faux positifs. S'il trouve un faux positif, l'administrateur peut envoyer le message à la boîte aux lettres du destinataire.

L'administrateur des messages peut examiner les marquages de courrier indésirable si l'une des conditions suivantes est vraie :

  - un trop grand nombre de faux positifs sont filtrés dans la boîte aux lettres de mise en quarantaine du courrier indésirable.

  - le volume de courrier indésirable rejeté ou supprimé est insuffisant.

Pour plus d'informations, consultez la rubrique [Marquages de courrier indésirable](anti-spam-stamps-exchange-2013-help.md).

Vous pouvez alors ajuster les paramètres SCL afin de filtrer plus précisément le courrier indésirable entrant dans l'organisation. Pour plus d’informations, consultez la rubrique [Niveau de confiance du courrier indésirable](spam-confidence-level-threshold-exchange-2013-help.md).

Pour configurer la mise en quarantaine du courrier indésirable, procédez comme suit :

1.  Vérifiez que le filtrage de contenu est activé.

2.  Créez une boîte aux lettres conçue pour la mise en quarantaine du courrier indésirable.

3.  Spécifiez la boîte aux lettres de mise en quarantaine du courrier indésirable.

4.  Définissez le seuil de mise en quarantaine SCL.

5.  Gérez la boîte aux lettres de mise en quarantaine du courrier indésirable.

6.  Ajustez le seuil de mise en quarantaine SCL selon les besoins.

Pour plus d'informations, consultez la rubrique [Configuration d’une boîte aux lettres de mise en quarantaine du courrier indésirable](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

Retour au début

