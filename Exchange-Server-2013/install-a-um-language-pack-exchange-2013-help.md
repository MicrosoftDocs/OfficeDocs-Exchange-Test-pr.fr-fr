---
title: 'Installer un module linguistique de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Installer un module linguistique de messagerie unifiée
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50479495
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installer un module linguistique de messagerie unifiée

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Pour qu’une langue soit disponible dans la liste des langues de messagerie unifiée disponibles dans un plan de numérotation ou un standard automatique de messagerie unifiée, vous devez préalablement installer le module linguistique de messagerie unifiée approprié. Pour installer le module linguistique sur un serveur de boîtes aux lettres qui exécute le service de messagerie unifiée Microsoft Exchange, exécutez le fichier exécutable à extraction automatique spécifique de la langue ou la commande **setup.exe /AddUmLanguagePack**. Avant de pouvoir installer un module linguistique de messagerie unifiée, vous devez d’abord le télécharger sur un dossier local sur le serveur de boîtes aux lettres. Vous pouvez télécharger des modules linguistiques de messagerie unifiée sur la page des [modules linguistiques de messagerie unifiée pour Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=266542). Il existe un fichier exécutable distinct pour chaque langue.

Après avoir installé le module linguistique de messagerie unifiée approprié, vous pouvez afficher la liste des modules linguistiques à l’aide de la liste déroulante de la page **Paramètres** du plan de numérotation de messagerie unifiée ou de la liste déroulante **Langue de l’interface vocale automatique** sur la page **Général** d’un standard automatique de messagerie unifiée. Vous pouvez également configurer la langue par défaut pour qu’elle soit différente d’Anglais (États-Unis) sur les plans de numérotation de messagerie unifiée et les standards automatiques.

> [!CAUTION]
> Les modules linguistiques de messagerie unifiée pour Microsoft Exchange Server 2007 ou Exchange 2007 Service Pack 1 (SP1), SP2 ou SP3 ou Exchange 2010 Service Pack 1 SP1, SP2 ou SP3 ne peuvent pas être utilisés sur un serveur de boîtes aux lettres Exchange 2013.


Pour les tâches supplémentaires concernant les modules linguistiques de messagerie unifiée, consultez la rubrique [Procédures de langages, les invites et le message d'accueil de la messagerie unifiée](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Serveur de boîtes aux lettres (service de messagerie unifiée) » dans [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Vérifiez que le serveur de boîtes aux lettres est installé sur un autre ordinateur que le serveur d'accès au client ou que les serveurs d'accès au client et de boîtes aux lettres se situent sur la même ressource matérielle.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le fichier (.exe) Installation du module linguistique de messagerie unifiée pour installer un module linguistique de messagerie unifiée

1.  Dans le [centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542), téléchargez le fichier (.exe) du module linguistique de messagerie unifiée de la langue de votre choix dans un dossier local sur le serveur de boîtes aux lettres.

2.  Double-cliquez sur le fichier UMLanguagePack.*\<CultureCode\>.exe*. Par exemple, pour le module linguistique de messagerie unifiée allemand, vous devez télécharger le fichier nommé UMLanguagePack.de-DE.exe.

3.  
    
    Dans l’Assistant Installation Exchange 2013, sur la page **Contrat de licence**, lisez les conditions du contrat, sélectionnez **J’accepte les termes du contrat de licence**, puis cliquez sur **Suivant**.

4.  
    
    Dans la page **Module linguistique de messagerie unifiée**, vérifiez que la langue correcte est répertoriée dans la fenêtre **Les modules linguistiques de messagerie unifiée suivants seront installés**, puis cliquez sur **Installer**.

5.  Cliquez sur **Terminer** pour terminer l’installation du module linguistique de messagerie unifiée.

## Utiliser setup.exe pour installer un module linguistique de messagerie unifiée

Cet exemple installe le module linguistique de messagerie unifiée Japonais (ja-JP) qui a été téléchargé dans le dossier D:\\Exchange\\UMLanguagePacks sur un serveur de boîtes aux lettres.

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

Cet exemple installe les modules linguistiques de messagerie unifiée Espagnol mexicain (es-MX) et Allemand (de-DE) qui ont été téléchargés dans le dossier D:\\Exchange\\UMLanguagePacks sur un serveur de boîtes aux lettres.

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

> [!WARNING]
> Si vous n’utilisez pas le paramètre /IAcceptExchangeServerLicenseTerms, vous devez voir l’erreur suivante : Bienvenue dans le programme d’installation sans assistance de Microsoft Exchange Server 2013. Vous devez accepter les termes du contrat de licence pour installer Microsoft Exchange Server 2013. Pour lire le contrat de licence, visitez le site http://go.microsoft.com/fwlink/p/?LinkId=150127. Pour accepter le contrat de licence, ajoutez le paramètre /IAcceptExchangeServerLicenseTerms à la commande exécutée. Pour plus d’informations, exécutez setup /?.


Pour plus d’informations sur les langues de messagerie unifiée disponibles, voir [Langues de messagerie unifiée, invites et messages d’accueil](um-languages-prompts-and-greetings-exchange-2013-help.md).

