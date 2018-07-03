---
title: 'Règles de protection Outlook: Exchange 2013 Help'
TOCTitle: Règles de protection Outlook
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50479083
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Règles de protection Outlook

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Chaque jour, les professionnels de l’information échangent des informations sensibles par courrier électronique, y compris des données et des rapports financiers, des informations relatives aux clients et aux employés, et des informations et spécifications confidentielles relatives aux produits. Dans Microsoft Exchange Server 2013, Microsoft Outlook et Microsoft OfficeOutlook Web App, les utilisateurs peuvent protéger les messages avec la gestion des droits relatifs à l’information (IRM) en appliquant un modèle de stratégie des droits des services AD RMS (Active Directory Rights Management Services). Pour cela, AD RMS doit être déployé au sein de l’organisation. Pour plus d’informations sur AD RMS, voir [Services AD RMS (Active Directory Rights Management Services)](https://go.microsoft.com/fwlink/p/?linkid=129823).

Toutefois, lorsque le choix est laissé aux utilisateurs, ceux-ci ont la possibilité d'envoyer les messages en texte clair sans protection IRM. Dans les organisations qui utilisent la messagerie électronique en tant que service hébergé, il existe un risque de fuite lorsqu’un message quitte le client pour être acheminé et stocké en dehors des limites de l’organisation. Malgré les procédures et contrôles bien définis que les hébergeurs de messagerie peuvent mettre en place pour limiter le risque de fuite d’information, une fois qu’un message quitte les limites d’une organisation, celle-ci n’a plus le contrôle des informations. Les règles de protection Outlook peuvent vous protéger contre ce type de fuite d'informations.

Pour les tâches de gestion liées à la gestion de l’IRM, voir [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

## Protection IRM automatique dans Outlook

Dans Exchange 2013, les règles de protection Outlook aident votre organisation à se protéger contre les risques de fuite d'information en appliquant automatiquement la protection IRM aux messages dans Exchange 2013. Les messages sont protégés par IRM avant qu'ils ne quittent le client Outlook. Cette protection est également appliquée à toutes les pièces jointes dont les formats de fichier sont pris en charge.

Lorsque vous créez des règles de protection Outlook pour un serveur Exchange 2013, les règles sont automatiquement distribuées vers Outlook 2010 à l'aide des services Web Exchange. Pour qu'Outlook 2010 puisse appliquer la règle, le modèle de stratégie des droits AD RMS que vous spécifiez doit être disponible sur tous les ordinateurs de l'organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si un modèle de stratégie des droits est supprimé du serveur AD RMS, vous devez modifier chacune des règles de protection Outlook qui utilise le modèle supprimé. Si une règle de protection Outlook continue à utiliser un modèle de stratégie des droits supprimé alors que le déchiffrement de transport est activé dans l’organisation, l’agent de déchiffrement ne pourra pas déchiffrer le message protégé, car le modèle ne sera plus valide. Si le déchiffrement du transport est configuré comme étant obligatoire, le service de transport rejettera le message et enverra une notification d’échec de remise à l’expéditeur. Pour plus d’informations sur le déchiffrement du transport, voir <a href="transport-decryption-exchange-2013-help.md">Déchiffrement du transport</a>. Pour plus d’informations sur les modèles de stratégie des droits des services AD RMS, consultez les <a href="https://go.microsoft.com/fwlink/p/?linkid=179455">considérations relatives au modèle de stratégie AD RMS</a>.<br />
Dans Windows Server 2008 et les versions ultérieures, vous pouvez archiver les modèles de stratégie des droits au lieu de les supprimer. Les modèles archivés peuvent servir à concéder du contenu sous licence. Toutefois, lorsque vous créez ou modifiez une règle de protection Outlook, les modèles archivés ne sont pas inclus dans la liste des modèles.</td>
</tr>
</tbody>
</table>


Les règles de protection Outlook sont similaires aux règles de protection du transport. dans la mesure où elles sont appliquées en fonction de conditions de message et protègent les messages par le biais d'un modèle de stratégie des droits d'accès AD RMS. Cependant, des règles de protection du transport sont appliquées dans le service de transport du serveur de boîtes aux lettres par l’agent de règles de transport. Les règles de protection de Outlook sont appliquées dans Outlook 2010, avant que le message quitte l’ordinateur de l’utilisateur. Les messages protégés par une règle de protection Outlook entrent dans le pipeline de transport avec la protection IRM déjà appliquée. En outre, les messages protégés par une règle de protection Outlook sont également enregistrés dans un format chiffré dans le dossier Éléments envoyés de la boîte aux lettres de l'expéditeur.

> [!NOTE]
> Si le déchiffrement de transport est activé dans votre organisation Exchange, les messages auxquels une protection IRM est appliquée par le biais d’une règle de protection Outlook issue du serveur AD RMS de votre organisation peuvent être déchiffrés par l’agent de déchiffrement installé sur le service de transport. Le contenu des messages peut être inspecté par l’agent de règles de transport et d’autres agents de transport installés sur le service de transport. Pour plus d'informations sur le déchiffrement du transport, voir <a href="transport-decryption-exchange-2013-help.md">Déchiffrement du transport</a>.


Lorsque vous utilisez des règles de protection du transport, les utilisateurs n’ont pas d’indication sur le fait que le message sera automatiquement protégé ou non sur le service de transport. En revanche, lorsqu'une règle de protection Outlook est appliquée à un message dans Outlook 2010, les utilisateurs savent qu'il sera protégé par IRM. Si nécessaire, les utilisateurs peuvent également sélectionner un autre modèle de stratégie des droits.

## Création de règles de protection Outlook

Pour créer des règles de protection Outlook , vous devez utiliser la cmdlet [New-OutlookProtectionRule](https://technet.microsoft.com/fr-fr/library/dd298182\(v=exchg.150\)) de l'environnement de ligne de commande Exchange Management Shell. Pour obtenir des instructions détaillées, voir [Créer une règle de protection d'Outlook](create-an-outlook-protection-rule-exchange-2013-help.md).

Lorsque vous créez une règle, vous pouvez indiquer si l'utilisateur peut la remplacer, soit en supprimant la protection IRM, soit en appliquant un autre modèle de stratégie des droits AD RMS que celui que vous avez spécifié. Si un utilisateur remplace la protection IRM appliquée par une règle de protection Outlook, Outlook 2010 insère l'en-tête `X-MS-Outlook-Client-Rule-Overridden` dans le message, qui vous signale que la règle a été remplacée par l'utilisateur.

## Prédicats dans les règles de protection Outlook

Les règles de protection Outlook vous permettent d'utiliser des prédicats pour appliquer automatiquement la protection IRM dans Outlook 2010 :

  - **FromDepartment**   Le prédicat *FromDepartment* recherche l'attribut de service de l'expéditeur dans Active Directory et applique automatiquement une protection IRM au message si le service de l'expéditeur correspond à celui spécifié dans la règle. Ainsi, vous pouvez créer une règle de protection Outlook pour protéger automatiquement tous les messages envoyés par le service Recherche.

  - **SentTo**   Votre organisation peut être amenée à protéger des messages envoyés à certains destinataires sensibles, comme les groupes de distribution Toute la société ou Finance. Le prédicat *SentTo* vous permet de créer une règle de protection Outlook pour appliquer automatiquement une protection IRM à tous les messages envoyés à des destinataires spécifiques.

  - **SentToScope**   Le prédicat *SentToScope* vous permet de créer une règle de protection Outlook pour appliquer automatiquement une protection IRM aux messages envoyés à l'intérieur ou à l'extérieur de l'organisation. Par exemple, vous pouvez combiner les prédicats *SentToScope* et *FromDepartment* pour appliquer une protection IRM aux messages envoyés par un service donné aux utilisateurs internes.

