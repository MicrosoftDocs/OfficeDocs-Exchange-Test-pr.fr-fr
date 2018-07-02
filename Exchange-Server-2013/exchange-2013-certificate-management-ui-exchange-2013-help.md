---
title: 'Interface utilisateur de la gestion de certificats Exchange 2013: Exchange 2013 Help'
TOCTitle: Interface utilisateur de la gestion de certificats Exchange 2013
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52062976
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interface utilisateur de la gestion de certificats Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2014-04-21_

La gestion des certificats dans un déploiement Exchange Server est l’une des tâches administratives les plus importantes. Il est primordial de s’assurer que les certificats sont installés et configurés de manière appropriée dans le but de fournir une infrastructure de messagerie sécurisée pour l’entreprise. Dans Exchange 2010, la console de gestion Exchange était la méthode principale de gestion des certificats. Dans Exchange 2013, la fonctionnalité de gestion des certificats se fait dans la console d’administration Exchange, la nouvelle interface utilisateur administrative d’Exchange 2013. Exchange 2013 vise à alléger la charge de travail des administrateurs en minimisant le nombre de certificats à gérer et le nombre d’opérations de certificat à effectuer, ainsi qu’en permettant une gestion centralisée.

## Certificats de serveurs d’accès au client

Le serveur d’accès au client d’Exchange 2013 est un serveur léger sans état, conçu pour accepter les connexions client entrantes et les rediriger via proxy vers le serveur de boîtes aux lettres approprié. L’interface utilisateur de gestion des certificats Exchange sur le serveur d’accès au client vous permet d’effectuer diverses tâches, comme la demande de nouveaux certificats et le renouvellement de certificats expirés ou sur le point de l’être.

## Présentation de l’interface utilisateur de gestion des certificats

Vous pouvez accéder à l’interface utilisateur de gestion de certificats Exchange via le CAE en sélectionnant **Serveurs**, puis **Certificats**. L’interface utilisateur de gestion permet d’effectuer les actions suivantes :

  - **Créer un certificat**   Sélectionnez **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour lancer l’Assistant Nouveau certificat Exchange.

  - **Modifier un certificat existant**   Sélectionnez **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier") pour un certificat valide pour accéder à la page de propriétés du certificat.

  - **Supprimer un certificat**   Sélectionnez **Supprimer**![Icône Supprimer](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icône Supprimer") pour lancer la boîte de dialogue de confirmation de suppression d’un certificat sélectionné.

  - **Effectuer des actions supplémentaires**   Sélectionnez **Plus d’options**![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") pour exporter ou importer un certificat. Pour exporter un certificat, celui-ci doit être valide.

## Expiration de certificat

Dans les versions précédentes de Microsoft Exchange, il n’existait pas de moyen simple de voir si un certificat numérique arrivait expiration. Dans Exchange 2013, le centre de notifications affiche des avertissements lorsqu’un certificat stocké sur l’un des serveurs d’accès au client Exchange 2013 est sur le point d’expirer.

## Certificats de serveur de boîtes aux lettres

Une différence essentielle entre Exchange 2010 et Exchange 2013 est que les certificats utilisés sur le serveur de boîtes aux lettres Exchange 2013 sont auto-signés. Comme tous les clients se connectent à un serveur de boîte aux lettres Exchange 2013 via un serveur d’accès au client Exchange 2013, les seuls certificats à gérer sont ceux du serveur d’accès au client. Le serveur d’accès au client approuve automatiquement le certificat auto-signé sur le serveur de boîtes aux lettres, de sorte que les clients ne reçoivent pas d’avertissement à propos d’un certificat auto-signé non approuvé, à condition que le serveur d’accès au client dispose d’un certificat non auto-signé provenant d’une autorité de certification Windows ou d’un tiers approuvé. Il n’existe pas d’outils ou de cmdlets permettant de gérer les certificats auto-signés sur le serveur de boîtes aux lettres. Une fois le serveur installé correctement, vous ne devriez pas avoir à vous préoccuper des certificats sur le serveur de boîtes aux lettres.

## Expiration des certificats auto-signés

Par défaut, le certificat auto-signé installé sur le serveur de boîtes aux lettres Exchange 2013 expirera au bout de cinq ans à compter de la date d’installation.

## Cmdlets liées aux certificats

Vous pouvez utiliser les cmdlets suivantes pour gérer les certificats numériques sur un serveur d’accès client Exchange :

  - Import-ExchangeCertificate   Cette cmdlet permet d’importer des certificats sur un serveur. Vous pouvez importer un certificat signé par une autorité de certification (pour terminer une demande de signature de certificat en attente) ou un certificat doté d’une clé privée (fichiers PKCS\#12, portant généralement l’extension .pfx, précédemment exportés à partir d’un serveur avec la clé privée).

  - Remove-ExchangeCertificate   Cette cmdlet permet de supprimer des certificats d’un serveur.

  - Enable-ExchangeCertificate   Cette cmdlet permet d’attribuer des services à un certificat.

  - Get-ExchangeCertificate   Cette cmdlet permet de récupérer un certificat Exchange en fonction d’une série de critères.

  - New-ExchangeCertificate   Cette cmdlet permet de créer un certificat auto-signé ou une demande de signature de certificat.

