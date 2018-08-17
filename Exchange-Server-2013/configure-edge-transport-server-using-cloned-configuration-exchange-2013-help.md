---
title: 'Configurer un srv de transp. Edge avec la config. clonée: Exchange 2013 Help'
TOCTitle: Configurer un serveur de transport Edge à l’aide de la configuration clonée
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61180532
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurer un serveur de transport Edge à l’aide de la configuration clonée

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-04-13_

Vous pouvez utiliser les scripts de l’environnement de ligne de commande Exchange Management Shell fournis (situés dans %ExchangeInstallPath%Scripts) pour dupliquer la configuration d’un serveur de transport Edge. Ce processus est parfois appelé *configuration clonée*. La *configuration clonée* est la pratique consistant à déployer de nouveaux serveurs de transport Edge sur la base des informations de configuration d’un serveur source précédemment configuré. Les informations de configuration du serveur source précédemment configuré sont copiées, puis exportées dans un fichier XML qui est ensuite importé sur le serveur cible. Pour obtenir une vue d’ensemble de ce processus, consultez la rubrique [Configuration clonée de serveur de transport Edge](edge-transport-server-cloned-configuration-exchange-2013-help.md).

Les informations de configuration du serveur de transport Edge sont stockées dans les services AD LDS (Lightweight Directory Services) et ne sont pas répliquées entre plusieurs serveurs de transport Edge. En utilisant la configuration clonée, vous pouvez vous assurer que tous les serveurs de transport Edge déployés dans votre réseau de périmètre utilisent la même configuration.

Deux scripts de l’environnement Exchange Management Shell sont utilisés pour effectuer les tâches de configuration clonée :

  - **ExportEdgeConfig.ps1**   Exporte l’ensemble des paramètres configurés par l’utilisateur et des données d’un serveur de transport Edge, et les stocke dans un fichier XML.

  - **ImportEdgeConfig.ps1**   Durant l’étape de validation de la configuration, le script ImportEdgeConfig.ps1 contrôle le fichier XML exporté pour voir si les paramètres d’exportation spécifiques au serveur sont valides pour le serveur cible. Si les paramètres doivent être modifiés, le script écrit les paramètres non valides dans un fichier de réponses que vous pouvez modifier pour spécifier les informations du serveur cible utilisées durant l’étape d’importation de la configuration. Durant l’étape d’importation de la configuration, le script importe l’ensemble des paramètres configurés par l’utilisateur et des données stockées dans le fichier XML intermédiaire créé par le script ExportEdgeConfig.ps1.

Ces deux scripts sont situés dans le dossier %ExchangeInstallPath%Scripts.

## Avant de commencer

  - Durée d’exécution estimée de cette tâche : 30 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Serveurs de transport Edge » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - La configuration clonée ne duplique pas les paramètres d’abonnement Edge d’un serveur. Les certificats EdgeSync ne sont pas clonés. Vous devez exécuter le processus EdgeSync séparément pour chaque serveur de transport Edge. EdgeSync remplace tous les paramètres inclus dans les informations de configuration clonée et dans les informations de réplication EdgeSync.

  - Si des connecteurs d’envoi sont configurés pour utiliser des informations d’identification, le mot de passe est écrit dans le fichier XML intermédiaire comme chaîne chiffrée. Vous pouvez utiliser le paramètre *-key* avec les scripts ImportEdgeConfig.ps1 et ExportEdgeConfig.ps1 pour spécifier la chaîne de 32 octets à utiliser pour le chiffrement et le déchiffrement du mot de passe. Si vous n’utilisez pas le paramètre *-key*, une clé de chiffrement par défaut est utilisée.

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche. Pour apprendre à ouvrir l’environnement de ligne de commande Environnement de ligne de commande Exchange Management Shell dans votre organisation Exchange locale, reportez-vous à [Ouvrir le Shell](https://technet.microsoft.com/fr-fr/library/dd638134\(v=exchg.150\)).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Exportation des données de configuration du serveur source vers un fichier sur le serveur source

1.  Copiez le script ExportEdgeConfig.ps1 dans le dossier racine de votre profil utilisateur sur le serveur source.

2.  Pour exporter les données de configuration du serveur source vers un fichier sur le serveur source, utilisez la syntaxe suivante.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    Par exemple, pour exporter les données de configuration du serveur source vers le fichier C:\\CloneConfigData.xml, exécutez la commande suivante.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## Comment savoir si cette étape a fonctionné ?

Vous saurez que vous avez exporté les données de configuration source vers un fichier lorsque le message de confirmation « Données de configuration Edge exportées avec succès dans : \<chemin d’accès du fichier de sortie\> » apparaîtra.

## Étape 2 : Validation du fichier de configuration et création d’un fichier de réponses sur le serveur cible

1.  Copiez le fichier de configuration du serveur source que vous avez exporté à l’étape précédente vers le serveur de transport Edge cible.

2.  Copiez le script ImportEdgeConfig.ps1 dans le dossier racine de votre profil utilisateur sur le serveur cible.

3.  Pour valider le fichier de configuration et utiliser les résultats pour créer un fichier de réponses sur le serveur cible, utilisez la syntaxe suivante.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    Par exemple, pour valider le fichier de configuration C:\\CloneConfigData.xml et créer le fichier de réponses C:\\CloneConfigAnswer.xml, exécutez la commande suivante.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  Ouvrez le fichier de réponses et modifiez les paramètres non valides pour le serveur cible. Si aucune modification n’est requise, le fichier de réponses ne contiendra pas d’entrées. Enregistrez vos modifications.

## Comment savoir si cette étape a fonctionné ?

Vous saurez que vous avez validé le fichier de configuration et créé un fichier de réponses lorsque le message de confirmation « Fichier de réponses créé avec succès » s’affichera.

## Étape 3 : Importation du fichier de configuration sur le serveur cible

Pour importer le fichier de configuration sur le serveur cible, utilisez la syntaxe suivante.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

Par exemple, pour importer le fichier de configuration C:\\CloneConfigData.xml à l’aide du fichier de réponses C:\\CloneConfigAnswer.xml, exécutez la commande suivante.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## Comment savoir si cette étape a fonctionné ?

Vous saurez que le fichier de configuration a été importé sur le serveur cible lorsque le message de confirmation « Informations de configuration Edge importées avec succès » s’affichera.

