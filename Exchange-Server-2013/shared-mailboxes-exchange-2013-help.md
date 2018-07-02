---
title: 'Boîtes aux lettres partagées: Exchange 2013 Help'
TOCTitle: Boîtes aux lettres partagées
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 50477612
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Boîtes aux lettres partagées

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-06-04_

Découvrez la boîte aux lettres partagée Exchange dans Microsoft Exchange Server 2013, les raisons de son utilisation et la méthode de conversion d’une boîte aux lettres déléguée en boîte aux lettres partagée Exchange.

Une boîte aux lettres partagée est une boîte aux lettres à laquelle plusieurs utilisateurs ont accès pour lire et envoyer des messages électroniques. Des boîtes aux lettres partagées peuvent également être utilisées pour disposer d’un calendrier commun, permettant à plusieurs utilisateurs de planifier et consulter les temps de travail ou de congés.

Les boîtes aux lettres partagées ne sont pas prises en charge sur les appareils mobiles.

**Pourquoi configurer une boîte aux lettres partagée ?**

  - Elle fournit une adresse de messagerie générale (par exemple : info@contoso.com ou ventes@contoso.com) que les clients peuvent utiliser pour obtenir des renseignements sur votre société.

  - Elle permet aux services qui fournissent des services centralisés aux employés, tels que le support technique, les ressources humaines ou le service d’impression, de répondre aux questions des employés.

  - Elle permet à plusieurs utilisateurs de lire et de répondre à des messages envoyés à une adresse électronique (par exemple : une adresse spécifiquement utilisée par le support technique).

## Qu'est-ce que les boîtes aux lettres partagées ?

Une boîte aux lettres partagée est un type de boîte aux lettres utilisateur qui ne dispose pas de ses propres nom d’utilisateur et mot de passe. Par conséquent, les utilisateurs ne peuvent pas s’y connecter directement. Pour accéder à une boîte aux lettres partagée, les utilisateurs doivent d'abord recevoir les autorisations Envoyer en tant que ou Accès total à la boîte aux lettres. Une fois cette opération terminée, les utilisateurs se connectent à leurs propres boîtes aux lettres, puis accèdent à la boîte aux lettres partagée en l’ajoutant à leur profil Outlook. Dans Exchange 2003 et les versions antérieures, les boîtes aux lettres partagées ne représentaient qu'une boîte aux lettres normale à laquelle un administrateur pouvait accorder un accès délégué. Avec Exchange 2007, les boîtes aux lettres partagées sont devenues leur propre type de destinataire :

  - **RecipientType** : UserMailbox

  - **RecipientTypeDetails** : SharedMailbox

Dans la version précédente d'Exchange, la création d'une boîte aux lettres partagée impliquait un processus en plusieurs étapes dans lequel vous deviez utiliser l'environnement de ligne de commande Exchange Management Shell pour réaliser certaines tâches. Dans Exchange 2013, vous pouvez utiliser le Centre d'administration Exchange (CAE) pour créer une boîte aux lettres partagée en une seule étape. Pour plus d'informations, consultez la rubrique [Créer une boîte aux lettres partagée](create-a-shared-mailbox-exchange-2013-help.md). En fait, le CAE comporte une zone de fonctionnalités entièrement consacrée aux boîtes aux lettres partagées. Il vous suffit d'accéder à **Destinataires**\>**Boîtes aux lettres partagées** pour afficher toutes les tâches de gestion pour les boîtes aux lettres partagées.

Vous pouvez utiliser les autorisations suivantes avec une boîte aux lettres partagée.

  - **Accès total**   L’autorisation Accès total permet à un utilisateur d’ouvrir la boîte aux lettres partagée et d’agir comme le propriétaire de cette boîte aux lettres. Une fois qu’il a accédé à la boîte aux lettres partagée, l’utilisateur peut créer des éléments de calendrier, lire, afficher, supprimer et modifier des courriers électroniques, créer des tâches et contacts de calendrier. Toutefois, un utilisateur doté d’une autorisation Accès total ne peut pas envoyer de messages à partir de la boîte aux lettres partagée à moins de disposer de l’autorisation Envoyer en tant que ou Envoyer de la part de.

  - **Envoyer en tant que**   L’autorisation Envoyer en tant que permet à un utilisateur d’emprunter l’identité du propriétaire de la boîte aux lettres partagée pour envoyer des messages. Par exemple, si Kweku se connecte à la boîte aux lettres partagée du service Marketing et envoie un message, le service Marketing semblera en être l’expéditeur.

  - **Envoyer de la part de**   L’autorisation Envoyer de la part de permet à l’utilisateur d’envoyer des messages de la part de la boîte aux lettres partagée. Par exemple, si John se connecte à la boîte aux lettres partagée Reception Building 32 et envoie un message, ce dernier semblera avoir été envoyé par « John de la part de Reception Building 32 ». Vous ne pouvez pas utiliser le CAE pour accorder des autorisations Envoyer de la part de ; vous devez utiliser la cmdlet [Set-Mailbox](https://technet.microsoft.com/fr-fr/library/bb123981\(v=exchg.150\)) avec le paramètre *GrantSendonBehalf*.

## Conversion de boîtes aux lettres partagées

Dans les versions précédentes d'Exchange, vous pouvez utiliser une boîte aux lettres normale en tant que boîte aux lettres déléguée. Si vous disposez de boîtes aux lettres déléguées, vous pouvez utiliser l'environnement de ligne de commande Exchange Management Shell pour convertir ces boîtes aux lettres déléguées en boîtes aux lettres partagées. Pour plus d'informations, consultez la rubrique [Convertir une boîte aux lettres](convert-a-mailbox-exchange-2013-help.md).

