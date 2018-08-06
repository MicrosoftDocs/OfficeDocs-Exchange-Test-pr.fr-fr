---
title: 'Connecteur étranger pour remettre les msg vers une psrl non-SMTP télécopie | Microsoft Docs'
TOCTitle: Créer un connecteur étranger pour remettre les messages vers une passerelle non-SMTP télécopie
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50478252
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Créer un connecteur étranger pour remettre les messages vers une passerelle non-SMTP télécopie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2012-10-17_

Vous pouvez avoir un scénario dans lequel vous voulez envoyer et recevoir des messages d'un serveur passerelle de fax qui n'utilise pas SMTP comme mécanisme de transport principal. Suivez les étapes indiquées dans la présente procédure pour créer un connecteur étranger qui remet à et reçoit des messages d'un système étranger.

> [!TIP]
> Dans la plupart des cas où vous devez communiquer des messages sortants à un système autre que SMTP, nous recommandons l’utilisation de connecteurs d’agent de remise, parce qu’ils permettent la gestion de file d’attente de messages, que les messages n’ont pas à être écrits dans le système de fichiers, et pour d’autres raisons avantageuses. La rubrique <a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agents de remise et connecteurs d’agent de remise</a> fournit de plus amples détails.


Intéressé par des scénarios où cette procédure est utilisée ? Consultez les rubriques suivantes :

  - [Planification et déploiement](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## Ce qu’il faut savoir avant de commencer ?

  - Durée d’exécution estimée de cette tâche : 30 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Connecteurs étrangers » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Comment procéder ?

## Étape 1 : Utilisez le Shell pour créer un connecteur étranger qui envoie des message vers un serveur passerelle non SMTP

1.  Exécutez la commande suivante pour créer le connecteur étranger :
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    Dans cet exemple, Hub01 et Hub02 sont des serveurs sources désignés dans votre organisation pour remettre des messages à un système étranger. L'utilisation de plusieurs serveurs source assure la tolérance de pannes.

Une fois le connecteur étranger créé, vous pouvez configurer les répertoires de dépôt, de collecte et de relecture, en fonction des besoins de votre organisation.

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que le connecteur étranger est créé avec succès, exécutez la commande suivante :

    Get-ForeignConnector | Format-List Name

Vérifiez que le nom pour le connecteur étranger que vous avez créé s'affiche.

## Étape 2 : Utilisez le Shell pour configurer le répertoire de dépôt pour un serveur de boîtes aux lettres exécutant le service de transport

Le répertoire de dépôt pour un serveur de boîtes aux lettres exécutant le service de transport permet de remettre des messages sortants depuis un connecteur étranger.

Vous créez un répertoire à utiliser comme répertoire de dépôt sur votre système de fichiers local. Vous pouvez également utiliser un répertoire sur un partage de fichiers réseau.

1.  Exécutez le script suivant pour spécifier le répertoire de dépôt de votre connecteur étranger (modifiez la valeur du paramètre *DropDirectory* vers un chemin d'accès approprié pour votre environnement) :
    
        Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement défini le répertoire de dépôt, vous pouvez exécuter le script de cmdlet et vérifier la valeur du paramètre *DropDirectory* :

    Get-ForeignConnector "Contoso Foreign Connector" | Format-List

Une fois le connecteur étranger créé et le répertoire de dépôt spécifié, vous pouvez envoyer un message au moyen du serveur de boîtes aux lettres dans lequel vous avez créé votre connecteur étranger et vérifier qu'un fichier est remis au répertoire de dépôt.

## Étape 3 : Utilisez le Shell pour configurer le répertoire de collecte pour un service de transport sur un serveur de boîtes aux lettres

Le répertoire de collecte pour le service de transport sur un serveur de boîtes aux lettres permet de collecter les messages générés par des systèmes non SMTP. Utilisez cette procédure lorsque vous voulez collecter de nouveaux messages générés par un système non SMTP, tel qu'un serveur de passerelle de fax, par le biais du transfert de fichiers.

Pour obtenir des instructions détaillées pour la configuration de votre répertoire de collecte, consultez [Configurer le répertoire de collecte et le répertoire de relecture](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement défini le répertoire de collecte, vous pouvez exécuter la commande suivante et vérifier la valeur du paramètre *PickupDirectoryPath* :

    Get-TransportService | Format-List PickupDirectoryPath

## Étape 4 : Utilisez le Shell pour configurer le répertoire de relecture pour un service de transport sur un serveur de boîtes aux lettres

Le répertoire de relecture pour le service de transport sur un serveur de boîtes aux lettres permet de collecter les messages générés par des systèmes non SMTP. Utilisez cette procédure pour configurer le répertoire de relecture lorsque vous voulez soumettre à nouveau des messages électroniques, généralement depuis un serveur de passerelle de fax étranger non SMTP, généré dans votre environnement Exchange et exporté depuis le transport Exchange.

Pour obtenir des instructions détaillées pour la configuration de votre répertoire de collecte, consultez [Configurer le répertoire de collecte et le répertoire de relecture](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez correctement défini le répertoire de relecture, vous pouvez exécuter la commande suivante et vérifier la valeur du paramètre *ReplayDirectoryPath* :

    Get-TransportService | Format-List ReplayDirectoryPath

## Pour plus d'informations

[Connecteurs étrangers](foreign-connectors-exchange-2013-help.md)

[Agents de remise et connecteurs d’agent de remise](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

