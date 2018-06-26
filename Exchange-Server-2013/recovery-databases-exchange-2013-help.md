---
title: 'Récupérer des bases de données: Exchange 2013 Help'
TOCTitle: Récupérer des bases de données
ms:assetid: f3c6fd0b-2e25-442e-a0fc-46f663130c3e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876954(v=EXCHG.150)
ms:contentKeyID: 50479561
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Récupérer des bases de données

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2012-11-02_

Une base de données de récupération (RDB) est une base de données de boîtes aux lettres spéciale qui vous permet de monter une base de données de boîtes aux lettres restaurée et d’extraire des données à partir de la base de données restaurée, dans le cadre d’une opération de récupération. La cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)) permet d’extraire des données d’une base de données de récupération. Une fois extraites, les données peuvent être exportées dans un dossier ou fusionnées avec les données d’une boîte aux lettres existante. Les bases de données de récupération vous permettent de récupérer des données à partir d’une sauvegarde ou d’une copie de base de données sans perturber l’accès des utilisateurs aux données actuelles.

Microsoft Exchange Server 2013 permet de restaurer des données directement dans une base de données de récupération. Le montage des données récupérées sous forme de base de données de récupération permet à l’administrateur de restaurer des boîtes aux lettres individuelles ou des éléments individuels d’une boîte aux lettres. La restauration d’une base de données de récupération peut s’effectuer de deux façons :

  - Si une base de données de récupération existe déjà, l’application peut démonter la base de données, restaurer les données dans celle-ci et dans les fichiers journaux, puis la remonter.

  - La base de données et les fichiers journaux peuvent être restaurés vers tout emplacement sur le disque. Exchange analyse les données restaurées et relit les journaux de transaction pour mettre à jour les bases de données. Il reste ensuite à configurer une base de données de récupération pour pointer vers les fichiers de bases de données déjà récupérés.

## Différences entre une base de données de boîtes aux lettres et une base de données de récupération

Les bases de données de récupération sont différentes des bases de données de boîtes aux lettres standard à plusieurs égards :

  - La création d’une base de données de récupération s’effectue à l’aide de l’environnement de ligne de commande Exchange Management Shell.

  - Il n’est pas possible d’envoyer ni de recevoir du courrier vers ou depuis une base de données de récupération. L’accès des clients à une base de données de récupération (avec les protocoles SMTP, POP3 et IMAP4) est bloqué. Cela afin d’empêcher l’utilisation d’une base de données de récupération pour insérer du courrier dans le système de messagerie ou en supprimer.

  - L’accès MAPI des clients à l’aide de Microsoft OfficeOutlook ou Outlook Web App est bloqué. L’accès MAPI est pris en charge pour une base de données de récupération mais uniquement par les outils et les applications de récupération. Pour accéder à une boîte aux lettres dans une base de données de récupération à l’aide de MAPI, le GUID de la boîte aux lettres et celui de la base de données doivent être spécifiés.

  - Il n’est pas possible de connecter des boîtes aux lettres dans une base de données de récupération à des comptes d’utilisateur. Pour permettre à un utilisateur d’accéder aux données d’une boîte aux lettres se trouvant dans une base de données de récupération, cette boîte aux lettres doit être fusionnée avec une boîte aux lettres existante ou exportée dans un dossier.

  - Les stratégies de gestion du système et des boîtes aux lettres ne sont pas appliquées. Cela permet d’éviter que des éléments dans une base de données de récupération soient supprimés par le système au cours du processus de récupération.

  - Il n’est pas possible de procéder à la maintenance en ligne des bases de données de récupération.

  - Il n’est pas possible d’activer l’enregistrement circulaire pour les bases de données de récupération.

  - Une seule base de données de récupération peut être montée à la fois sur un serveur de boîtes aux lettres. L’utilisation d’une base de données de récupération n’est pas prise en compte dans la limite de la base de données par serveur de boîtes aux lettres.

  - Vous ne pouvez pas créer des copies d’une base de données de récupération.

  - Une base de données de récupération peut être utilisée comme cible uniquement pour des opérations de restauration.

  - Une base de données récupérée, montée en tant que base de données de récupération, n’est liée en aucune façon à la boîte aux lettres d’origine.

## Utilisation d’une base de données de récupération

Avant de commencer à utiliser une base de données de récupération, certaines conditions doivent être respectées. Une base de données de récupération peut uniquement être utilisée pour les bases de données de boîtes aux lettres Exchange 2013. Les bases de données de boîtes aux lettres d’une version antérieure d’Exchange ne sont pas prises en charge. En outre, la boîte aux lettres cible utilisée pour l’extraction et la fusion de données doit se trouver dans la même forêt Active Directory que la base de données montée dans la base de données de récupération.

Une base de données de récupération peut être utilisée pour récupérer des données dans les cas suivants :

  - **Récupération de tonalité sur un même serveur**   Vous pouvez procéder à une récupération à partir d’une base de données de récupération, dans le cadre d’une opération de récupération de tonalité, une fois que la base de données d’origine sauvegardée est restaurée.

  - **Récupération de tonalité sur un serveur alternatif**   Vous pouvez utiliser un serveur alternatif pour héberger la base de données de tonalités. Vous pouvez ensuite récupérer les données à partir d’une base de données de récupération une fois que la base de données d’origine sauvegardée est récupérée.

  - **Récupération de boîte aux lettres**   Vous pouvez récupérer une boîte aux lettres individuelle après une sauvegarde lorsque la période de rétention de la boîte aux lettres supprimée est terminée. Vous pouvez ensuite extraire les données de la boîte aux lettres restaurée et les copier dans un dossier cible ou les fusionner avec les données d’une autre boîte aux lettres.

  - **Récupération d’un élément spécifique**   Vous pouvez restaurer des données sauvegardées qui ont été supprimées ou purgées d’une boîte aux lettres.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Les listes de contrôle d’accès des dossiers (ACL) ne sont pas conservées lors de la récupération du contenu d’une boîte aux lettres dans une boîte aux lettres active. Étant donné que le processus de récupération implique en général de récupérer les données d’une boîte aux lettres et de les réinsérer dans la base de données d’origine, il n’est pas nécessaire de récupérer ou de copier les listes de contrôle d’accès.</td>
</tr>
</tbody>
</table>


Les bases de données de récupération sont conçues pour la récupération de bases de données de boîtes aux lettres selon les conditions et scénarios suivants :

  - Les informations logiques sur la base de données d’origine et les boîtes aux lettres dans cette base de données restent intactes dans Active Directory.

  - Vous ne devez récupérer qu’une seule boîte aux lettres ou qu’une seule base de données. Les scénarios de récupération sont les suivants :
    
      - Récupération ou réparation d’une base de données lorsqu’une base de données de tonalités est utilisée, dans le but de fusionner les deux bases de données.
    
      - Récupération d’une base de données sur un serveur autre que le serveur d’origine de la base de données. Le cas échéant, vous pouvez ensuite fusionner les données récupérées sur le serveur d’origine.
    
      - Récupération des éléments que des utilisateurs ont supprimés de leur boîte aux lettres une fois que la période de rétention des éléments supprimés s’est écoulée.

Les bases de données de récupération ne sont généralement pas conçues pour les scénarios dans lesquels vous devez restaurer des serveurs complets ou plusieurs bases de données, ou lorsque l’urgence de la situation nécessite de changer ou de reconstruire votre topologie Active Directory.

Pour plus d’informations sur la création d’une base de données de récupération, voir [Créer une base de données de récupération](create-a-recovery-database-exchange-2013-help.md). Pour plus d’informations sur l’utilisation d’une base de données de récupération, voir [Restaurer des données à l’aide d’une base de données de récupération](restore-data-using-a-recovery-database-exchange-2013-help.md).

