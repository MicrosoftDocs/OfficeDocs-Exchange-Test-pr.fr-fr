---
title: 'Protection des données de formulaire avec l’empreinte numérique de document'
TOCTitle: Protection des données de formulaire avec la création d’une empreinte numérique de document
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61204566
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protection des données de formulaire avec la création d’une empreinte numérique de document

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2014-09-11_

Si votre organisation utilise des formulaires pour recueillir des informations sensibles, les utilisateurs peuvent essayer d’envoyer ces formulaires par message électronique à des contacts extérieurs, ce qui entraîne un risque de sécurité. La protection contre la perte de données (DLP) dans Exchange vous aide à protéger ces informations en les détectant avec la [Création d’une empreinte numérique de document](overview-of-document-fingerprinting-in-exchange.md). Pour utiliser la création d’une empreinte numérique de document, il suffit de télécharger un formulaire vierge, tel qu’un document de propriété intellectuelle, un formulaire officiel ou un autre formulaire standard utilisé dans votre organisation. Ensuite, ajoutez l’empreinte numérique de document obtenue à une stratégie DLP ou à une règle de transport. Voici comment procéder.

> [!VIDEO https://www.microsoft.com/fr-fr/videoplayer/embed/2210a683-cfe1-4f03-a3f3-6bd7d0483e5a]

## Utilisation du Centre d’administration Exchange (CAE) pour créer une empreinte numérique de document

![Chemin d’accès vers la création d’une empreinte numérique de document dans le Centre d’administration Exchange mis en surbrillance](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "Chemin d’accès vers la création d’une empreinte numérique de document dans le Centre d’administration Exchange mis en surbrillance")

1.  Dans le CAE, accédez à **Gestion de la conformité** \> **Protection contre la perte de données**.

2.  Cliquez sur **Gérer les empreintes de document**.

3.  Sur la page des empreintes numériques de document, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour créer une empreinte numérique de document.

4.  Remplissez les champs **Nom** et **Description** pour l’empreinte numérique de document. (Le nom que vous choisissez apparaîtra dans la liste des types d’informations sensibles.)

5.  Pour télécharger un formulaire, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

6.  Choisissez un formulaire, puis cliquez sur **Ouvrir**. (Assurez-vous que le fichier que vous téléchargez contient du texte, qu’il n’est pas protégé par mot de passe et qu’il fait partie des types de fichier pris en charge dans les règles de transport. Pour obtenir la liste des types de fichier pris en charge, voir [Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\)). Si ce n’est pas le cas, vous obtiendrez une erreur lorsque vous essaierez de créer l’empreinte.) Répétez l’opération pour tous les fichiers supplémentaires que vous souhaitez ajouter à la liste de documents de cette empreinte numérique de document. Vous pourrez également ajouter ou supprimer des fichiers de cette empreinte numérique de document ultérieurement si vous le souhaitez.

7.  Cliquez sur **Enregistrer**.

L’empreinte numérique de document fait désormais partie de vos types d’informations sensibles et vous pouvez l’ajouter à une stratégie DLP ou à une règle de transport via la condition **Le message contient des informations sensibles...**.

![Condition « Appliquer cette règle si » mise en surbrillance](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "Condition « Appliquer cette règle si » mise en surbrillance")

Pour plus d’informations sur l’ajout de règles à une stratégie DLP, consultez la section « Modifier une stratégie DLP » de l’article [Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md), et pour plus d’informations sur la modification des règles de transport, consultez l’article [Intégration des règles d'informations sensibles aux règles de transport](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). Si vous souhaitez créer une stratégie, consultez [Création d'une stratégie DLP à partir d'un modèle](how-to-new-dlp-data-loss-prevention-policy-template.md).

## Utilisez l’environnement de ligne de commande Exchange Management Shell pour créer un package de règles de classification basé sur l’empreinte numérique de document.

> [!TIP]
> Même si vous pouvez créer et modifier des packages de règles de classification dans l’environnement Exchange Management Shell, vous trouverez peut-être que la création d’empreintes numériques de document est un peu plus simple dans le CAE. Nous vous recommandons de l’essayer dans le CAE avant de tenter cette procédure dans l’environnement Exchange Management Shell.


La protection contre la perte de données utilise des packages de règles de classification pour détecter le contenu sensible dans les messages. Pour créer un package de règles de classification basé sur une empreinte numérique de document, utilisez les cmdlets **New-Fingerprint** et **New-DataClassification**. Comme les résultats de **New-Fingerprint** ne sont pas stockés en dehors de la règle de classification des données, vous devez toujours exécuter les cmdlets **New-Fingerprint** et **New-DataClassification** ou **Set-DataClassification** dans la même session PowerShell. L’exemple suivant crée une empreinte numérique de document à partir du fichier C:\\My Documents\\Contoso Employee Template.docx. La nouvelle empreinte est stockée en tant que variable pour que vous puissiez l’utiliser avec la cmdlet **New-DataClassification** dans la même session PowerShell.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

À présent, nous allons créer une règle de classification des données nommée « Contoso Employee Confidential » qui utilise l’empreinte numérique de document du fichier C:\\My Documents\\Contoso Customer Information Form.docx.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

Vous pouvez désormais utiliser la cmdlet **Get-DataClassification** pour trouver tous les packages de règles de classification des données DLP et, dans cet exemple, « Contoso Customer Confidential » fait partie de la liste des packages de règles de classification des données.

Enfin, ajoutez le package de règles de classification des données « Contoso Customer Confidential » à une stratégie DLP.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

L’agent DLP détecte désormais les documents qui correspondent à l’empreinte numérique de document Contoso Customer Form.docx.

Pour obtenir des informations sur la syntaxe et les paramètres, consultez les rubriques [New-Fingerprint](https://technet.microsoft.com/fr-fr/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/fr-fr/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/fr-fr/library/dn584141\(v=exchg.150\)) et [Get-DataClassification](https://technet.microsoft.com/fr-fr/library/jj215720\(v=exchg.150\)).

## Pour plus d’informations

[Création d’une empreinte numérique de document](overview-of-document-fingerprinting-in-exchange.md)

[Gestion de stratégies de protection contre la perte de données (DLP)](manage-dlp-policies-exchange-2013-help.md)

[Intégration des règles d'informations sensibles aux règles de transport](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

