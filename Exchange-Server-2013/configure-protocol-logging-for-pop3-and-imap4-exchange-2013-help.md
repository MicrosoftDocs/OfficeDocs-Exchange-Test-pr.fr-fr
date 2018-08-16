---
title: 'Config. la journalisation du protocole pour POP3 et IMAP4: Exchange 2013 Help'
TOCTitle: Configurer la journalisation du protocole pour POP3 et IMAP4
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50555388
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer la journalisation du protocole pour POP3 et IMAP4

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-11-27_

Vous pouvez utiliser l’environnement de ligne de commande Exchange Management Shell pour activer, désactiver ou modifier les paramètres d’enregistrement dans le journal de protocole pour POP3 et IMAP4. Par défaut, l'enregistrement dans le journal de protocole n'est pas activé.

L’enregistrement dans le journal de protocole vous permet de vérifier les connexions POP3 et IMAP4 dans votre environnement Exchange. Cette opération peut être utile si vous effectuez des dépannages relatifs aux performances POP3 ou IMAP4. Pour plus d’informations, consultez la rubrique [Journalisation du protocole pour POP3 et IMAP4](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md). Pour plus d’informations sur POP3 et IMAP4, consultez la rubrique [POP3 et IMAP4 dans Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Ce qu’il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 5 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrées « Paramètres POP3 » et « Paramètres IMAP4 » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer le journal du protocole pour POP3 ou IMAP4

Cet exemple active le journal du protocole pour IMAP4 ou POP3 sur le serveur d’accès au client CAS01.

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true

> [!NOTE]
> Une fois que vous avez modifié les paramètres d’enregistrement dans le journal de protocole pour POP3 ou IMAP4, vous devez redémarrer les services que vous utilisez : POP3 ou IMAP4. Pour obtenir des informations sur la procédure de redémarrage des services POP3 et IMAP4, voir <a href="start-and-stop-the-pop3-services-exchange-2013-help.md">Démarrage et arrêt des services POP3</a> et <a href="start-and-stop-the-imap4-services-exchange-2013-help.md">Démarrer et arrêter les services IMAP4</a>.


Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)) et [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour désactiver le journal du protocole pourPOP3 ou IMAP4

Cet exemple désactive le journal du protocole pour IMAP4 ou POP3 sur le serveur d’accès au client CAS01.

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false

> [!NOTE]
> Une fois que vous avez modifié les paramètres d’enregistrement dans le journal de protocole pour POP3 ou IMAP4, vous devez redémarrer les services que vous utilisez : POP3 ou IMAP4. Pour obtenir des informations sur la procédure de redémarrage des services POP3 et IMAP4, voir <a href="start-and-stop-the-pop3-services-exchange-2013-help.md">Démarrage et arrêt des services POP3</a> et <a href="start-and-stop-the-imap4-services-exchange-2013-help.md">Démarrer et arrêter les services IMAP4</a>.


Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)) et [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour modifier le journal du protocole pour POP3 ou IMAP4

Pour modifier les paramètres d’enregistrement POP3 ou IMAP4, exécutez les cmdlets **Set-ImapSettings** ou **Set-PopSettings** avec un ou plusieurs paramètres suivants.

  - *LogFileLocation*   Ce paramètre spécifie l’emplacement des fichiers journaux du protocole  POP3 ou IMAP4. Par défaut, les fichiers journaux du protocole POP3 sont situés dans le répertoire C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3. Cet exemple active le journal du protocole POP3 sur le serveur d’accès au client CAS01. Il redéfinit également le répertoire de ce même journal à C:\\Pop3Logging.
    
        Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"

  - *LogFileRollOverSettings*   Ce paramètre définit la fréquence à laquelle le journal du protocole POP3 ou IMAP4 crée un nouveau fichier journal. Par défaut, un nouveau fichier journal est créé chaque jour. Les valeurs possibles sont les suivantes :
    
    Horaire
    
    Quotidien
    
    Hebdomadaire
    
    Mensuel
    
    Ce paramètre s’applique uniquement lorsque la valeur du paramètre *LogPerFileSizeQuota* est définie sur zéro. Cet exemple montre comment modifier l’enregistrement dans le journal de protocole POP3 sur le serveur d’accès au client CAS01 pour créer un nouveau fichier journal toutes les heures.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly

  - *LogPerFileSizeQuota*   Ce paramètre définit en octets la taille maximale des fichiers journaux du protocole POP3 ou IMAP4. Par défaut, cette valeur est définie sur zéro. Si la valeur définie est définie sur zéro, un nouveau fichier journal de protocole est créé selon la fréquence spécifiée par le paramètre *LogFileRollOverSettings*.
    
    Cet exemple montre comment modifier l’enregistrement dans le journal de protocole POP3 sur le serveur d’accès au client CAS01 pour créer un nouveau fichier journal lorsqu’un fichier journal atteint 2 mégaoctets (Mo).
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    
    Cet exemple modifie le journal du protocole POP3 sur le serveur d’accès au client CAS01 pour utiliser le même fichier journal indépendamment de sa date de création et de sa taille.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited

> [!NOTE]
> Une fois que vous avez modifié les paramètres d’enregistrement dans le journal de protocole pour POP3 ou IMAP4, vous devez redémarrer les services que vous utilisez : POP3 ou IMAP4. Pour obtenir des informations sur la procédure de redémarrage des services POP3 et IMAP4, voir <a href="start-and-stop-the-pop3-services-exchange-2013-help.md">Démarrage et arrêt des services POP3</a> et <a href="start-and-stop-the-imap4-services-exchange-2013-help.md">Démarrer et arrêter les services IMAP4</a>.


Pour des informations détaillées sur la syntaxe et les paramètres, consultez les rubriques [Set-ImapSettings](https://technet.microsoft.com/fr-fr/library/aa998252\(v=exchg.150\)) et [Set-PopSettings](https://technet.microsoft.com/fr-fr/library/aa997154\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell pour vérifier les paramètres d’enregistrement dans le journal de protocole POP3 : Si l’enregistrement dans le journal de protocole POP3 est activé, la valeur du paramètre *ProtocolLogEnabled* est `True`. Si l’enregistrement dans le journal de protocole POP3 est désactivé, la valeur est `False`. Vous pouvez également vous assurer que les valeurs des paramètres *LogFileLocation*, *LogPerFileSizeQuota* et *LogFileRollOverSettings* sont correctes.

    Get-PopSettings | format-list

Exécutez la commande suivante dans l’environnement de ligne de commande Exchange Management Shell pour vérifier les paramètres d’enregistrement dans le journal de protocole IMAP4 : Si l’enregistrement dans le journal de protocole IMAP4 est activé, la valeur du paramètre *ProtocolLogEnabled* est `True`. Si l’enregistrement dans le journal de protocole IMAP4 est désactivé, la valeur est `False`. Vous pouvez également vous assurer que les valeurs des paramètres *LogFileLocation*, *LogPerFileSizeQuota* et *LogFileRollOverSettings* sont correctes.

    Get-ImapSettings | format-list

## Pour plus d'informations

Après avoir configuré les paramètres de journal du protocole pour POP3 et IMAP4, vous souhaitez peut-être réaliser les opérations suivantes :

[Démarrer et arrêter les services IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md)

[Démarrage et arrêt des services POP3](start-and-stop-the-pop3-services-exchange-2013-help.md)

