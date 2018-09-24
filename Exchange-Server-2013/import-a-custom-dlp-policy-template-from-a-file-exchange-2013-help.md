---
title: 'Import de mod. de strat. DLP personnalisé d’un fichier: Exchange 2013 Help'
TOCTitle: Importer un modèle de stratégie DLP personnalisé à partir d’un fichier
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50477343
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importer un modèle de stratégie DLP personnalisé à partir d’un fichier

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-08-09_

Vous pouvez gérer des informations sensibles par le biais de stratégies DLP en important un fichier qui contient les paramètres de stratégie des informations. Modèles de stratégie DLP peuvent être développés indépendamment d’Exchange en tant que fichiers XML. Toutefois, ils doivent satisfaire les conditions de format spécifique pour fonctionner correctement. Autrement, les stratégies qui sont exportés à partir d’une version antérieure d’Exchange peuvent être importés dans Microsoft Exchange Server 2013.

> [!CAUTION]
> Vous devez activer vos stratégies DLP en mode Test avant de les exécuter dans votre environnement de production. Au cours de ces tests, nous vous recommandons de configurer des boîtes aux lettres d'exemple d'utilisateur et d'envoyer des messages de test qui appellent vos stratégies de test afin de confirmer les résultats.


## Ce qu'il faut savoir avant de commencer

  - Durée d’exécution estimée : 15 minutes

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Protection contre la perte de données » dans la rubrique [Stratégie de messagerie et autorisations de conformité](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Que souhaitez-vous faire ?

## Utiliser le CAE pour importer un modèle de stratégie DLP personnalisé depuis un fichier

Utilisez la procédure suivante pour importer un modèle de stratégie DLP personnalisé à partir d’un fichier. Afin d’éviter toute confusion, indiquez un nom unique pour chaque partie de votre stratégie ou de règle lorsque vous avez la possibilité de fournir votre propre nom.

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Cliquez sur la flèche située en regard de l'icône **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis cliquez sur **Importer la stratégie**.

3.  Dans la page **Importer la stratégie**, complétez les champs suivants :
    
    1.  **Sélectionnez le fichier à importer**   Ajoutez le nom du fichier de stratégie à installer.
    
    2.  **Nom**   Ajoutez un nom qui distinguera cette stratégie des autres.
    
    3.  **Description**   Facultatif, ajoutez une description qui résume cette stratégie.
    
    4.  **Autres options**   Sélectionnez le mode ou l'état de cette stratégie. La nouvelle stratégie n'est pas activée tant que vous ne l'avez pas spécifié. Le mode par défaut d'une stratégie est test sans notifications.
    
    5.  Cliquez sur **Suivant** pour valider et importer la stratégie.

## Utiliser le Shell pour importer un modèle de stratégie DLP personnalisé à partir d’un fichier

Cet exemple importe un fichier de modèle de stratégie DLP personnalisé dans le fichier C:\\My Documents\\DLP Backup.xml. Importation d’une collection de stratégies DLP à partir d’un fichier XML, supprime ou remplace toutes les stratégies DLP préexistants qui ont été définis dans votre organisation. Assurez-vous que vous disposez d’une sauvegarde de votre collection de stratégies DLP actuelle avant d’importer et remplacer vos stratégies DLP actuels.

```powershell
Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))
```

## Pour plus d'informations

[Protection contre la perte de données](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

