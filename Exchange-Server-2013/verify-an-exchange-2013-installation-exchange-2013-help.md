---
title: 'Vérifier une installation d’Exchange 2013: Exchange 2013 Help'
TOCTitle: Vérifier une installation d’Exchange 2013
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50479633
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Vérifier une installation d’Exchange 2013

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-07_

Après l’installation de Microsoft Exchange Server 2013, nous vous recommandons de la vérifier en exécutant la cmdlet **Get-ExchangeServer** et en examinant le fichier journal de l’installation. En cas d’échec ou d’erreur dans le processus d’installation, vous pouvez utiliser le fichier journal d’installation pour identifier la source du problème.

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Avez-vous trouvé ce que vous cherchez ? Veuillez prendre une minute pour [nous envoyer votre avis à l'adresse](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) au sujet des informations que vous souhaitiez y trouver.

## Exécuter Get-ExchangeServer

Pour vérifier si Exchange 2013 a été installé avec succès, exécutez la cmdlet **Get-ExchangeServer** dans l'environnement de ligne de commandeExchange Management Shell. Une liste de tous les rôles serveur Exchange 2013 installés sur le serveur spécifié lors de l'exécution de cette cmdlet est affichée.

Pour obtenir des informations détaillées sur la syntaxe et les paramètres, voir [Get-ExchangeServer](https://technet.microsoft.com/fr-fr/library/bb123873\(v=exchg.150\)).

## Examen du fichier journal d'installation

Vous pouvez également recueillir plus d'informations sur l'installation et la configuration de Exchange 2013 en examinant le fichier journal de l'installation.

L'installation de Exchange enregistre les événements logs dans le journal **Application** de **l'Observateur d'événements** sur les ordinateurs qui exécutent Windows Server 2008 R2 Service Pack 1 (SP1) et Windows Server 2012. Examinez le journal **Application** et vérifiez l'absence d'avertissements ou de messages d'erreur concernant l'installation de Exchange. Ces fichiers journaux contiennent un historique de chaque action effectuée par le système pendant l'installation de Exchange 2013 et des éventuelles erreurs survenues. Par défaut, la méthode de journalisation est `Verbose`. Vous trouverez des informations pour chaque rôle serveur installé.

Le fichier journal se trouve à l'emplacement suivant : *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log. La variable *\<system drive\>* représente le répertoire racine du lecteur où le système d'exploitation est installé.

Ce fichier suit la progression de chaque tâche effectuée pendant l'installation et la configuration d'Exchange 2013. Le fichier contient des informations sur l'état des contrôles de conditions préalables et de préparation du système effectués avant le début de l'installation, sur la progression de l'installation de l'application et sur les changements de configuration apportés au système. Ce fichier journal permet de vérifier que les rôles serveur ont été installés comme prévu.

Nous vous conseillons de commencer l'examen du fichier journal d’installation en y cherchant les erreurs éventuelles. Si vous trouvez une entrée indiquant qu'une erreur s'est produite, lisez le texte associé afin de déterminer la cause de l'erreur.

