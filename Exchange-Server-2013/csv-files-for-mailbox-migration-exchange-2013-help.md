---
title: 'Fichiers CSV pour la migration de boîtes aux lettres: Exchange 2013 Help'
TOCTitle: Fichiers CSV pour la migration de boîtes aux lettres
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54652746
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Fichiers CSV pour la migration de boîtes aux lettres

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2017-11-16_

Vous pouvez utiliser un fichier CSV pour migrer en bloc un nombre important de boîtes aux lettres d’utilisateurs. Vous pouvez spécifier un fichier CSV lorsque vous utilisez le Centre d’administration Exchange (CAE) ou la cmdlet **New-MigrationBatch** dans l’Environnement de ligne de commande Exchange Management Shell pour créer un lot de migration. L’utilisation d’un fichier CSV pour spécifier plusieurs utilisateurs à migrer dans un lot de migration est prise en charge dans les scénarios de migration suivants :

  - **Déplacements à l'intérieur d'organisations Exchange locales**
    
      - **Déplacement local :**  Un déplacement local est l'opération par laquelle vous déplacez des boîtes aux lettres d'une base de données de boîtes aux lettres vers une autre. Un déplacement local se produit au sein d'une forêt unique.
    
      - **Déplacement d'entreprise inter-forêts :**  Un déplacement d'entreprise inter-forêts consiste à déplacer des boîtes aux lettres vers une autre forêt. Un déplacement inter-forêts peut être entrepris soit à partir de la forêt cible qui est celle vers laquelle vous voulez déplacer les boîtes aux lettres, soit à partir de la forêt source, qui est celle hébergeant actuellement les boîtes aux lettres.

  - **Embarquement et débarquement Exchange Online**
    
      - **Migration de déplacement à distance par embarquement :**  Dans un déploiement Exchange hybride, vous pouvez déplacer des boîtes aux lettres à partir d'une organisation Exchange locale vers Exchange Online. Cette opération est également appelée migration de déplacement à distance par *embarquement* parce qu'elle consiste à embarquer des boîtes aux lettres dans Exchange Online.
    
      - **Migration de déplacement à distance par débarquement :**  Vous pouvez également opérer une migration de déplacement à distance par *débarquement*, qui consiste à migrer des boîtes aux lettres Exchange Online vers votre organisation Exchange locale.
        
        > [!NOTE]
        > Les deux migrations de déplacement à distance, par embarquement et par débarquement, sont entreprises à partir de votre organisation Exchange Online.
    
      - **Migration Exchange intermédiaire :**   Vous pouvez également migrer un sous-ensemble de boîtes aux lettres à partir d'une organisation Exchange locale vers Exchange Online. Il s'agit d'un autre type de migration par embarquement. Une migration Exchange intermédiaire permet de migrer uniquement des boîtes aux lettres Exchange 2003 et Exchange 2007. Une migration intermédiaire ne permet pas de migrer des boîtes aux lettres Exchange 2010 et Exchange 2013. Avant d'exécuter une migration intermédiaire, vous devez utiliser une synchronisation d'annuaires ou une autre méthode pour mettre en service les utilisateurs du courrier électronique au sein de votre organisation Exchange Online.
    
      - **Migration IMAP :**  Ce type de migration par embarquement migre des données de boîtes aux lettres à partir d'un serveur IMAP (y compris Exchange) vers Exchange Online. Pour une migration IMAP, vous devez mettre en service des boîtes aux lettres dans Exchange Online avant de migrer leurs données.

> [!NOTE]
> Une migration Exchange à basculement ne prend pas en charge l'utilisation d'un fichier CSV, car toutes les boîtes aux lettres d'utilisateurs locales sont migrées vers Exchange Online en un seul lot.


## Attributs pris en charge pour les fichiers CSV en relation avec les déplacements ou migrations en bloc

La première ligne, ou ligne d'en-tête, d'un fichier CSV utilisé pour migrer des utilisateurs répertorie les noms des attributs, ou champs, spécifiés dans les lignes suivantes. Les noms d'attributs sont séparés par des virgules. Chaque ligne sous la ligne d'en-tête représente un utilisateur et fournit les informations requises pour la migration. Les attributs de chaque ligne d'utilisateur doivent se présenter dans le même ordre que les noms d'attributs dans la ligne d'en-tête. Les valeurs d'attribut sont séparées par des virgules. Si la valeur d'attribut d'un enregistrement spécifique est nulle, n'entrez rien pour cet attribut. Assurez-vous toutefois d'inclure la virgule pour séparer la valeur nulle de l'attribut suivant.

Les valeurs d’attribut figurant dans le fichier CSV remplacent celles du paramètre correspondant quand ce dernier est utilisé lors de la création d’un lot de migration à l’aide du CAE ou de l’Environnement de ligne de commande Exchange Management Shell. Pour plus d’informations et des exemples, consultez la section Les valeurs d’attribut figurant dans le fichier CSV remplacent celles définies pour le lot de migration.

> [!TIP]
> Pour créer le fichier CSV, vous pouvez utiliser n'importe quel éditeur de texte, mais l'utilisation d'une application telle que Microsoft Excel facilite l'importation de données, ainsi que la configuration et l'organisation des fichiers CSV. Veillez à enregistrer les fichiers CSV au format .csv ou .txt.


Les sections suivantes décrivent les attributs pris en charge dans la ligne d'en-tête d'un fichier CSV pour chaque type de migration. Chaque section contient un tableau indiquant les attributs pris en charge, leur caractère obligatoire, un exemple de valeur à utiliser pour chacun d'eux, et une description.

> [!NOTE]
> Dans les sections suivantes, <em>environnement source</em> désigne l'emplacement actuel d'une boîte aux lettres d'utilisateur ou d'une base de données. <em>Environnement cible</em> désigne l'emplacement vers lequel la boîte aux lettres sera migrée ou la base de données vers laquelle elle sera déplacée.


## Déplacements locaux

Le tableau suivant décrit les attributs pris en charge dans un fichier CSV pour des déplacements locaux. Pour plus d'informations, consultez la rubrique [Gestion des déplacements locaux](manage-on-premises-moves-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Obligatoire ou facultatif</th>
<th>Valeurs acceptées</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse SMTP de l'utilisateur</p></td>
<td><p>Spécifie l'utilisateur qui sera déplacé.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Facultatif</p></td>
<td><p>Nom de base de données</p></td>
<td><p>Spécifie la base de données de boîtes aux lettres vers laquelle la boîte aux lettres principale de l'utilisateur sera déplacée. Vous pouvez spécifier des bases de données différentes dans les différentes lignes du fichier CSV. Cela vous permet de déplacer des boîtes aux lettres vers plusieurs bases de données dans un même lot de migration.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Facultatif</p></td>
<td><p>Nom de base de données</p></td>
<td><p>Spécifie la base de données de boîtes aux lettres qui est déplacée vers l’archive boîte aux lettres (si elle existe). Vous pouvez spécifier une autre base de données dans les différentes lignes du fichier CSV, ce qui vous permet de déplacer des boîtes aux lettres d’archive dans le même lot de migration de bases de données différentes.</p>

> [!NOTE]  
> Si vous ne spécifiez pas la base de données d’archive, la boîte aux lettres d’archive est déplacé vers la même base que la boîte aux lettres principale.

</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facultatif</p></td>
<td><p><code>Unlimited</code> ou un entier positif d'une valeur comprise entre <code>0</code> (par défaut) et <code>2147483647</code></p></td>
<td><p>Spécifie le nombre d’éléments erronés à ignorer si le service de migration rencontre un élément endommagé dans la boîte aux lettres. Si vous incluez cet attribut dans le fichier CSV, il remplacera la valeur par défaut ou une valeur spécifiée par vous si vous incluez le paramètre <em>BadItemLimit</em> lors de la création du lot de migration à l’aide du CAE ou de l’Environnement de ligne de commande Exchange Management Shell.</p>

> [!TIP]
> Nous vous recommandons d'utiliser la valeur par défaut (0) et d'augmenter le nombre limite d'éléments erronés uniquement pour un utilisateur particulier en cas d'échec du déplacement ou de la migration de ce dernier.

<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>Facultatif</p></td>
<td><p>Utilisez l'une des valeurs suivantes :</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (valeur par défaut)</p></li>
</ul></td>
<td><p>Spécifie s'il faut déplacer la boîte aux lettres principale, la boîte aux lettres d'archivage ou les deux boîtes aux lettres de l'utilisateur.</p></td>
</tr>
</tbody>
</table>


## Migrations de déplacement à distance par embarquement dans un déploiement hybride

Dans un déploiement hybride, vous pouvez déplacer des boîtes aux lettres d'une organisation Exchange locale vers Exchange Online. Lors de l'embarquement de boîtes aux lettres, le lot de migration est créé dans l'organisation Exchange Online et son traitement est initié par un administrateur Exchange Online. Pour plus d'informations, consultez la rubrique [Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides](https://technet.microsoft.com/fr-fr/library/jj906432\(v=exchg.150\)).

Le tableau suivant décrit les attributs pris en charge dans un fichier CSV pour des migrations de déplacement à distance par embarquement.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Obligatoire ou facultatif</th>
<th>Valeurs acceptées</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse SMTP de l'utilisateur</p></td>
<td><p>Spécifie l'adresse de messagerie de l'utilisateur à extension messagerie au sein de l'organisation Exchange Online. Elle correspond à la boîte aux lettres d'utilisateur locale qui sera migrée.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facultatif</p></td>
<td><p><code>Unlimited</code> ou un entier positif d'une valeur comprise entre <code>0</code> (par défaut) et <code>2147483647</code></p></td>
<td><p>Spécifie le nombre d’éléments erronés à ignorer si le service de migration rencontre un élément endommagé dans la boîte aux lettres. Si vous incluez cet attribut dans le fichier CSV, il remplacera la valeur par défaut ou la valeur spécifiée par vous si vous incluez le paramètre <em>BadItemLimit</em> lors de la création du lot de migration à l’aide du CAE ou de l’Environnement de ligne de commande Exchange Management Shell.</p>

> [!TIP]
> Nous vous recommandons d'utiliser la valeur par défaut (0) et d'augmenter le nombre limite d'éléments erronés uniquement pour un utilisateur particulier en cas d'échec du déplacement ou de la migration de ce dernier.

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Facultatif</p></td>
<td><p><code>Unlimited</code> ou un entier positif d'une valeur comprise entre <code>0</code> (par défaut) et une valeur maximale</p></td>
<td><p>Spécifie le nombre d'éléments de grande taille de la boîte aux lettres de l'utilisateur qui seront ignorés. Lorsque le nombre d'éléments de grande taille dépasse cette valeur, la migration de la boîte aux lettres échoue.</p>
<p>La valeur par défaut est 0, ce qui signifie que la migration échoue si la boîte aux lettres contient des éléments de grande taille.</p>
<p>Lors de l'embarquement de boîtes aux lettres dans Exchange Online, la taille des éléments migrés n'excède pas 35 Mo.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Facultatif</p></td>
<td><p>Utilisez l'une des valeurs suivantes :</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (valeur par défaut)</p></li>
</ul></td>
<td><p>Spécifie s'il faut déplacer la boîte aux lettres principale, la boîte aux lettres d'archivage ou les deux boîtes aux lettres de l'utilisateur.</p></td>
</tr>
</tbody>
</table>


## Déplacements d'entreprise inter-forêts et migrations de déplacement à distance par débarquement dans un déploiement hybride

Comme indiqué précédemment, les déplacements inter-forêts sont entrepris à partir de la forêt cible ou de la forêt source. Les migrations de déplacement à distance par débarquement sont entreprises à partir de votre organisation Exchange Online. Pour plus d'informations, consultez les rubriques suivantes :

  - [Préparer les boîtes aux lettres pour les demandes de déplacement inter-forêts](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Déplacement de boîtes aux lettres entre des organisations locales et Exchange Online dans des déploiements hybrides](https://technet.microsoft.com/fr-fr/library/jj906432\(v=exchg.150\))

Le tableau suivant décrit les attributs pris en charge dans un fichier CSV pour des déplacements d'entreprise inter-forêts et des migrations de déplacement à distance par débarquement dans un déploiement Exchange hybride.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Obligatoire ou facultatif</th>
<th>Valeurs acceptées</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse SMTP de l'utilisateur</p></td>
<td><p>Pour des déplacements d'entreprise inter-forêts, cet attribut spécifie la boîte aux lettres ou l'utilisateur à extension messagerie au sein de la forêt source.</p>
<p>Pour les migrations de déplacement à distance par débarquement, il spécifie la boîte aux lettres Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Obligatoire pour les migrations de déplacement à distance par débarquement et les déplacements d’entreprise inter-forêts entrepris à partir de la forêt source. Cet attribut peut également être spécifié lors de la création du lot de migration dans le CAE ou dans l’Environnement de ligne de commande Exchange Management Shell.</p>
<p>Cet attribut est facultatif pour les déplacements d'entreprise inter-forêts entrepris à partir de la forêt cible.</p></td>
<td><p>Nom de base de données</p></td>
<td><p>Spécifie la base de données de boîtes aux lettres dans la forêt cible, vers laquelle la boîte aux lettres principale de l'utilisateur sera déplacée. Vous pouvez spécifier des bases de données différentes dans les différentes lignes du fichier CSV. Cela vous permet de déplacer des boîtes aux lettres vers plusieurs bases de données dans un même lot de migration.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Facultatif</p></td>
<td><p>Nom de base de données</p></td>
<td><p>Spécifie la base de données de boîtes aux lettres dans la forêt cible, vers laquelle la boîte aux lettres d'archivage de l'utilisateur sera déplacée. Vous pouvez spécifier des bases de données différentes dans les différentes lignes du fichier CSV. Cela vous permet de déplacer des boîtes aux lettres d'archivage vers plusieurs bases de données dans un même lot de migration.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facultatif</p></td>
<td><p><code>Unlimited</code> ou un entier positif d'une valeur comprise entre <code>0</code> (par défaut) et <code>2147483647</code></p></td>
<td><p>Spécifie le nombre d’éléments erronés à ignorer si le service de migration rencontre un élément endommagé dans la boîte aux lettres. Si vous incluez cet attribut dans le fichier CSV, il remplacera la valeur par défaut ou la valeur spécifiée par vous si vous incluez le paramètre <em>BadItemLimit</em> lors de la création du lot de migration à l’aide du CAE ou de l’Environnement de ligne de commande Exchange Management Shell.</p>
> [!TIP]
> Nous vous recommandons d'utiliser la valeur par défaut (0) et d'augmenter le nombre limite d'éléments erronés uniquement pour un utilisateur particulier en cas d'échec du déplacement ou de la migration de ce dernier.

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Facultatif</p></td>
<td><p><code>Unlimited</code> ou un entier positif d'une valeur comprise entre <code>0</code> (par défaut) et une valeur maximale</p></td>
<td><p>Spécifie le nombre d'éléments de grande taille de la boîte aux lettres de l'utilisateur qui seront ignorés. Lorsque le nombre d'éléments de grande taille dépasse cette valeur, la migration de la boîte aux lettres échoue.</p>
<p>La valeur par défaut est 0, ce qui signifie que la migration échoue si la boîte aux lettres contient des éléments de grande taille.</p>
<p>Lors de l'embarquement de boîtes aux lettres dans Exchange Online, la taille des éléments migrés n'excède pas 35 Mo.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Facultatif</p></td>
<td><p>Utilisez l'une des valeurs suivantes :</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (valeur par défaut)</p></li>
</ul></td>
<td><p>Spécifie s'il faut déplacer la boîte aux lettres principale, la boîte aux lettres d'archivage ou les deux boîtes aux lettres de l'utilisateur.</p></td>
</tr>
</tbody>
</table>


## Migration Exchange intermédiaire

Lorsque vous voulez recourir à une migration Exchange intermédiaire pour migrer des boîtes aux lettres locales Exchange 2003 et Exchange 2007 vers Exchange Online, vous devez utiliser un fichier CSV afin d'identifier le groupe d'utilisateurs pour un lot de migration. Une migration Exchange intermédiaire n'impose aucune limite au nombre de boîtes aux lettres que vous pouvez migrer vers le nuage. Toutefois, le fichier CSV d'un lot de migration peut contenir au maximum 1 000 lignes. Pour migrer plus de 1 000 boîtes aux lettres, vous devez créer des fichiers CSV supplémentaires, et les utiliser pour créer de nouveaux lots de migration. Pour plus d'informations sur les migrations Exchange intermédiaires, consultez la rubrique [Migration de boîtes aux lettres vers Exchange Online à l’aide d’une migration intermédiaire](https://technet.microsoft.com/fr-fr/library/jj874018\(v=exchg.150\)).

Le tableau suivant décrit les attributs pris en charge dans un fichier CSV pour une migration Exchange intermédiaire.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Obligatoire ou facultatif</th>
<th>Valeurs acceptées</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse SMTP de l'utilisateur</p></td>
<td><p>Spécifie l'adresse de messagerie de l'utilisateur à extension messagerie (ou une boîte aux lettres si vous réessayez d'effectuer la migration) dans Exchange Online. Elle correspond à la boîte aux lettres d'utilisateur locale qui sera migrée. Des utilisateurs à extension messagerie sont créés dans Exchange Online suite à une synchronisation d'annuaires ou à un autre processus de mise en service. L'adresse de messagerie de l'utilisateur à extension messagerie doit correspondre à la propriété <em>WindowsEmailAddress</em> pour la boîte aux lettres locale correspondante.</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>Facultatif</p></td>
<td><p>Un mot de passe ne peut pas compter plus de huit caractères, et doit respecter les restrictions de mot de passe appliquées à votre organisation Office 365.</p></td>
<td><p>Ce mot de passe est défini pour le compte d'utilisateur quand l'utilisateur à extension messagerie correspondant dans Exchange Online est converti en boîte aux lettres durant la migration.</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>Facultatif</p></td>
<td><p><code>True</code> ou <code>False</code></p></td>
<td><p>Spécifie si les utilisateurs doivent modifier le mot de passe la première fois qu'ils se connectent à leur boîte aux lettres Exchange Online.</p>

> [!NOTE]  
> Si vous avez implémenté une solution d'authentification unique en déployant Active Directory Federation Services 2.0 (AD FS 2.0) dans votre organisation locale, vous devez utiliser la valeur <code>False</code> pour cet attribut.

</td>
</tr>
</tbody>
</table>


## Migrations IMAP

Un fichier CSV pour un lot de migration IMAP ne peut pas contenir plus de 50 000 lignes. Cependant, nous vous conseillons de migrer les utilisateurs en plusieurs lots plus petits. Pour plus d'informations sur les migrations IMAP, consultez les rubriques suivantes :

  - [Migration du courrier électronique à partir d'un serveur IMAP vers des boîtes aux lettres Exchange Online](https://technet.microsoft.com/fr-fr/library/jj874015\(v=exchg.150\))

  - [Fichiers CSV pour des lots de migration IMAP](https://technet.microsoft.com/fr-fr/library/jj200730\(v=exchg.150\))

Le tableau suivant décrit les attributs pris en charge dans un fichier CSV pour une migration IMAP.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribut</th>
<th>Obligatoire ou facultatif</th>
<th>Valeurs acceptées</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatoire</p></td>
<td><p>Adresse SMTP de l'utilisateur</p></td>
<td><p>Spécifie l'identifiant d'utilisateur pour la boîte aux lettres Exchange Online de l'utilisateur.</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>Obligatoire</p></td>
<td><p>Chaîne identifiant l'utilisateur dans le système de messagerie IMAP, dans un format pris en charge par le serveur IMAP.</p></td>
<td><p>Spécifie le nom de connexion du compte de l'utilisateur dans le système de messagerie IMAP (environnement source). En plus du nom d'utilisateur, vous pouvez utiliser les informations d'identification d'un compte disposant des autorisations nécessaires pour accéder à des boîtes aux lettres sur le serveur IMAP. Pour plus d'informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/jj200730(v=exchg.150)">Fichiers CSV pour des lots de migration IMAP</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>Obligatoire</p></td>
<td><p>Chaîne de mot de passe.</p></td>
<td><p>Spécifie le mot de passe du compte d'utilisateur désigné par l'attribut UserName.</p></td>
</tr>
</tbody>
</table>


## Les valeurs d'attribut figurant dans le fichier CSV remplacent celles définies pour le lot de migration.

Les valeurs d’attribut figurant dans le fichier CSV remplacent celles du paramètre correspondant quand ce dernier est utilisé lors de la création d’un lot de migration à l’aide du CAE ou de l’Environnement de ligne de commande Exchange Management Shell. Si vous voulez que la valeur du lot de migration soit appliquée à un utilisateur, vous devez laisser cette cellule vide dans le fichier CSV. Cela vous permet de combiner et de faire correspondre certaines valeurs d’attribut pour des utilisateurs sélectionnés dans un seul lot de migration.

Par exemple, nous allons dire que vous créez un lot dans la Environnement de ligne de commande Exchange Management Shell principal d’un utilisateur inter-forêts entreprise déplacer vers déplacer des boîtes aux lettres d’archive vers la forêt cible avec la commande Environnement de ligne de commande Exchange Management Shell.

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart

> [!NOTE]
> Étant donné que la valeur par défaut est déplacer primaire et d’archiver des boîtes aux lettres, vous n’êtes pas obligé de spécifier explicitement dans la commande Environnement de ligne de commande Exchange Management Shell.


Une portion du fichier CrossForestBatch1.csv pour ce lot de migration ressemble à ceci :

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

Comme les valeurs figurant dans le fichier CSV remplacent celles du lot de migration, les boîtes aux lettres principale et d'archivage de l'utilisateur user1 sont déplacées respectivement vers EXCH-MBX-01 et EXCH-MBX-A01 dans la forêt cible. Les boîtes aux lettres principale et d'archivage de l'utilisateur user2 sont déplacées vers EXCH-MBX-02 ou EXCH-MBX-03. La boîte aux lettres principale de l'utilisateur user3 est déplacée vers EXCH-MBX-01, et sa boîte aux lettres d'archivage vers EXCH-MBX-A02 ou EXCH-MBX-A03.

Dans un autre exemple, imaginons que vous créiez un lot pour une migration de déplacement à distance par embarquement dans un déploiement hybride afin de déplacer des boîtes aux lettres d'archivage vers Exchange Online avec la commande suivante.

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

Toutefois, vous pouvez également déplacer les boîtes aux lettres principales d'utilisateurs sélectionnés. Dans ce cas, une portion du fichier OnBoarding1.csv pour ce lot de migration ressemblerait à ceci :

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

Comme la valeur du type de boîte aux lettres figurant dans le fichier CSV remplace les valeurs du paramètre *MailboxType* dans la commande de création du lot, seules les boîtes aux lettres d'archivage des utilisateurs user1 et user2 sont migrées vers Exchange Online. En revanche, les boîtes aux lettres principales et d'archivage des utilisateurs user3 et user4 sont déplacées vers Exchange Online.

