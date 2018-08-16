---
title: 'Règles de protection de transport: Exchange 2013 Help'
TOCTitle: Règles de protection de transport
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 50478789
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Règles de protection de transport

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Les messages électroniques et leurs pièces jointes contiennent de plus en plus souvent des informations professionnelles cruciales telles que des spécifications de produit, des documents portant sur la stratégie de l’entreprise, des données financières ou des informations d’identification personnelle telles que des détails de contact, des numéros de sécurité sociale, des numéros de cartes de crédit et des données sur les employés. Il existe un certain nombre de réglementations propres à l’industrie et locales un peu partout dans le monde qui régissent la collecte, l’enregistrement et la divulgation des informations d’identification personnelle.

Pour protéger les informations sensibles, les entreprises mettent en place des stratégies de messagerie contenant des instructions sur la façon de traiter ces informations. Dans MicrosoftExchange Server 2013, vous pouvez utiliser des règles de protection de transport pour mettre en place ces stratégies de messagerie en vérifiant le contenu des messages, en chiffrant le contenu des messages sensibles et en utilisant la gestion des droits afin de contrôler l’accès au contenu.

Pour les tâches de gestion liées à la gestion de l’IRM, voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Règles de protection de transport et AD RMS

Transport protection règles vous permettent d’utiliser des règles de transport pour IRM protéger les messages en appliquant un modèle de stratégie de droits [de services AD RMS (Active Directory Rights Management Services)](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS).

> [!NOTE]
> AD RMS est une technologie de protection des données qui fonctionne avec des clients et des applications activés pour RMS (Rights Management Service) afin de protéger les informations sensibles en ligne et hors connexion. Pour utiliser la protection IRM dans un déploiement Exchange sur site, Exchange 2013 requiert un déploiement local d'AD RMS s'exécutant sur Windows Server 2008 ou version ultérieure.


AD RMS utilise les modèles de stratégie XML pour permettre aux applications activées pour IRM d’appliquer des stratégies de protection cohérentes. Dans Windows Server 2008 et les versions ultérieures, le serveur AD RMS comprend un service Web utilisable pour énumérer et obtenir des modèles. Exchange 2013 est fourni avec le modèle Ne pas transférer.

Lorsque ce modèle est appliqué à un message, seuls les destinataires peuvent déchiffrer le message. Les destinataires ne peuvent pas transférer le message à quelqu’un d’autre, copier le contenu du message ou imprimer le message.

Des modèles RMS supplémentaires peuvent être créés dans le déploiement AD RMS local pour répondre aux exigences de protection des droits au sein de votre organisation.

> [!important]
> Si un modèle de stratégie de droits est supprimé du serveur AD RMS, vous devez modifier les règles de protection de transport qui utilisent le modèle supprimé. Si une règle de protection de transport continue à utiliser un modèle de stratégie de droits supprimé, le serveur AD RMS ne réussira pas à adresser le contenu aux destinataires et une notification d’échec de remise sera envoyée à l’expéditeur.
> Dans Windows Server 2008 et les versions ultérieures, vous pouvez archiver les modèles de stratégie des droits au lieu de les supprimer. Les modèles archivés peuvent encore être utilisés pour autoriser le contenu, mais lorsque vous créez ou modifiez une règle de protection de transport, ces modèles ne sont pas inclus dans la liste des modèles.


Pour plus d’informations sur la création de modèles de AD RMS, voir [Guide pas à pas de AD RMS droits de stratégie de modèles de déploiement](https://go.microsoft.com/fwlink/p/?linkid=136593).

## Protection automatique à l'aide de règles de protection de transport

Les messages contenant des informations professionnelles cruciales ou des informations d’identification personnelle peuvent être identifiés à l’aide d’une combinaison de conditions de règle de transport, y compris les expressions régulières pour identifier des modèles de texte tels que les numéros de sécurité sociale. Les organisations requièrent différents niveaux de protection pour les informations sensibles. Certaines informations peuvent être restreintes aux employés, entrepreneurs ou partenaires alors que d’autres informations peuvent être restreintes uniquement aux employés à temps plein. Le niveau de protection voulu peut être appliqué aux messages en appliquant un modèle de stratégie de droits approprié. Par exemple, les utilisateurs peuvent marquer un message ou une pièce jointe comme Confidentiel. Comme illustré dans la figure suivante, vous pouvez créer une règle de protection de transport pour rechercher le mot « Confidentiel » dans le contenu d’un message et appliquer automatiquement une protection IRM au message.

Pour plus d’informations sur la création des règles de transport permettant l’application de la protection des droits, consultez [Créer une règle de protection de transport](create-a-transport-protection-rule-exchange-2013-help.md).

## Protection persistante des pièces jointes aux messages électroniques

Les utilisateurs envoient des informations professionnelles cruciales et des informations d'identification personnelle dans les pièces jointes aux messages électroniques en utilisant des formats de fichier Microsoft Office courants tels que Microsoft OfficeWord, Excel et PowerPoint. Tous ces formats de fichier prennent en charge une protection permanente via IRM ; ainsi, vous êtes assuré que les informations professionnelles cruciales et les informations d’identification personnelle contenues dans ces documents sont correctement protégées. Les règles de protection de transport appliquent la même protection aux messages électroniques et aux pièces jointes dans les formats de fichier pris en charge.

## Agent de règles de transport et agent de chiffrement

Lorsque vous utilisez des règles de protection de transport pour appliquer une protection IRM aux messages en fonction de conditions de règle, l’agent de règles de transport sur le service de transport vérifie les messages. S’ils respectent toutes les conditions sans exception, il marque le message de façon à ce qu’une protection IRM soit appliquée. L’agent de cryptage, agent de transport intégré qui déclenche l’événement **OnRoutedMessage**, applique réellement une protection IRM au message. L’agent de cryptage agit sur les messages uniquement si la protection IRM est activée pour les messages internes. Pour plus d’informations sur l’activation de la protection IRM, voir [Activer ou désactiver la technologie IRM pour les messages internes](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

Lorsque le service de transport redémarre et traite le premier message qui nécessite le chiffrement IRM, l’agent de cryptage doit être en mesure d’atteindre un serveur AD RMS dans l’organisation. Pour les messages suivants, l’agent n’a pas besoin de contacter le serveur AD RMS. En cas d’échec du chiffrement d’un message dû à des conditions temporaires, Exchange fait trois nouvelles tentatives à 10 minutes d’intervalle. Après trois tentatives, si le message ne peut pas être chiffré, il n’est pas remis aux destinataires. Une notification d’échec de remise est envoyée à l’expéditeur. Nous vous recommandons de prévoir un déploiement AD RMS de haute disponibilité pour être sûr qu’il n’y aura aucun impact sur le flux des messages.

Lorsque vous prévoyez d’utiliser des règles de protection de transport, vous devez prendre en compte le type d’information à protéger et prévoir d’établir les règles en conséquence. Dans Exchange 2013, les règles de transport disposent d’un grand nombre de prédicats permettant de vérifier le contenu des messages, notamment les pièces jointes prises en charge, les en-têtes de messages, les adresses d’expéditeurs et de destinataires, leurs attributs Active Directory tels que le service, l’appartenance au groupe de distribution et le rôle de responsable de l’expéditeur envers les destinataires. Pour plus d’informations sur les prédicats de règle de transport disponibles dans Exchange 2013, consultez la rubrique [Conditions de règles de transport (prédicats)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Vous devez également prendre en compte le trafic de messagerie au sein de votre organisation et le nombre de messages qui seront protégés à l’aide des règles de protection de transport. L’application d’une protection IRM à un grand nombre de messages nécessite davantage de ressources sur le serveur de boîtes aux lettres. En outre, la protection d’un grand nombre de messages ou de tous les messages a également une incidence sur l’utilisation du client, en particulier pour les utilisateurs de Microsoft Outlook.

