---
title: 'Autoriser les utilisateurs à effectuer des appels: Exchange 2013 Help'
TOCTitle: Autoriser les utilisateurs à effectuer des appels
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51407227
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoriser les utilisateurs à effectuer des appels

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-03-09_

L'*automate d'appels* est le processus permettant à des utilisateurs d'appeler un plan de numérotation de messagerie unifiée à l'aide d'un numéro Outlook Voice Access, ainsi que de passer ou transférer un appel vers un numéro de téléphone interne ou externe. La messagerie unifiée utilise un grand nombre de paramètres d'automate d'appels pour passer des appels pour les utilisateurs. Pour configurer un automate d'appels, vous devez configurer des règles de numérotation, des groupes de règles de numérotation et des autorisations de numérotation sur des plans de numérotation de messagerie unifiée, puis autoriser l'automate d'appels sur les plans de numérotation de messagerie unifiée, les stratégies de boîte aux lettres de messagerie unifiée et les standards automatiques. Vous pouvez également configurer des plans de numérotation de messagerie unifiée pour disposer d'indicatifs, d'un préfixe de numéro national et de formats de numéro nationaux, régionaux ou internationaux permettant de contrôler l'automate d'appels au sein de votre organisation. Cette rubrique décrit les règles de numérotation, les groupes de règles de numérotation, les autorisations de numérotation, ainsi que la manière de les utiliser pour autoriser et contrôler l'automate d'appels au sein de votre organisation.

**Contenu de cette rubrique**

Vue d’ensemble

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## Vue d'ensemble

L'automate d'appels intervient dans les cas suivants :

  - Un appel est passé vers un numéro de téléphone externe.

  - Un appel est transféré vers un standard automatique.

  - Un appel est transféré vers un utilisateur au sein de votre organisation.

  - Un utilisateur à extension messagerie unifiée utilise la fonctionnalité Émettre au téléphone.

Pour que l'automate d'appels fonctionne correctement, il convient de configurer correctement les paramètres suivants :

  - **Règles de numérotation**   Les règles de numérotation définissent le numéro composé par l'utilisateur à extension messagerie unifiée et le numéro composé par le PBX ou le PBX IP.

  - **Groupes de règles de numérotation**   Les groupes de règles de numérotation déterminent les types d'appels que les utilisateurs appartenant au groupe de numérotation peuvent passer.

  - **Autorisations de numérotation**   Les autorisations de numérotation déterminent les restrictions appliquées afin d'empêcher des utilisateurs d'exposer des frais de téléphone superflus ou de passer des appels longue distance.

Pour activer l'automate d'appels pour des utilisateurs appelant un plan de numérotation ou un standard automatique, procédez comme suit :

  - Assurez-vous que les passerelles VoIP représentée par une passerelle IP de messagerie unifiée liée avec un plan de numérotation utiliseront les appels sortants.

  - Créez des groupes de règles de numérotation en créant des règles de numérotation sur le plan de numérotation de messagerie unifiée.

  - Ajoutez des autorisations de numérotation pour les groupes de règles de numérotation nationales/régionales et internationales sur le plan de numérotation de messagerie unifiée, la stratégie de boîte aux lettres de messagerie unifiée ou le standard automatique associé au même plan de numérotation que la passerelle IP de messagerie unifiée.

## Types d'utilisateurs

Les utilisateurs pouvant utiliser la fonctionnalité d'automate d'appels dans une messagerie unifiée sont de deux types : les utilisateurs authentifiés et les utilisateurs non authentifiés. Tous les utilisateurs qui appellent un standard automatique de messagerie unifiée sont non authentifiés. Lorsque les utilisateurs appellent un numéro Outlook Voice Access, ils sont considérés comme non authentifiés car ils n’ont pas fourni leur numéro de poste et leur code confidentiel et ne se sont pas connectés à leur boîte aux lettres. Les utilisateurs sont authentifiés après avoir fourni leur numéro de poste et leur code confidentiel et s'être connectés avec succès à leur boîte aux lettres.

Quand des utilisateurs appellent un numéro Outlook Voice Access configuré sur un plan de numérotation de messagerie unifiée, puis tentent de passer ou de transférer un appel sans se connecter à leur boîte aux lettres, seuls les paramètres d'automate d'appels du plan de numérotation de messagerie unifiée sont appliqués à l'appel. Quand des utilisateurs anonymes ou non authentifiés appellent un standard automatique de messagerie unifiée, les paramètres d'automate d'appels configurés sur le standard automatique ainsi que sur le plan de numérotation associé au standard automatique sont appliqués à l'appel.

Lorsque des utilisateurs appellent le numéro Outlook Voice Access configuré sur un plan de numérotation et se connectent avec succès à leur boîte aux lettres, ils deviennent des utilisateurs authentifiés. Lorsque les utilisateurs sont authentifiés, les paramètres de l’automate d’appels utilisent les règles de numérotation et les paramètres d’autorisation de numérotation sur la stratégie de boîte aux lettres de messagerie unifiée qui est liée à ces utilisateurs.

Retour au début

## Paramètres de l'automate d'appels

Vous devez configurer plusieurs paramètres pour appliquer les paramètres de l'automate d'appels pour votre organisation. Outre la configuration des plans de numérotation de messagerie unifiée, des standards automatiques de messagerie unifiée et des stratégies de boîte aux lettres de messagerie unifiée que vous avez créés avec les règles de numérotation et les autorisations de numérotation appropriées, vous devez configurer des codes d’accès, des préfixes et formats de numéro sur les plans de numérotation de messagerie unifiée. Les paramètres de l'automate d'appels configurés pour les plans de numérotation, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée sont les suivants :

  - codes d'accès à une ligne extérieure, nationaux/régionaux et internationaux ;

  - préfixes téléphoniques nationaux ;

  - formats de numéro de téléphone national/régional et international ;

  - groupes de règles de numérotation nationales/régionales et internationales configurés ;

  - groupes de règles de numérotation nationales/régionales et internationales autorisés ;

  - entrées de règle de numérotation :

  - autorisations de numérotation.

Pour pouvoir configurer avec succès l'automate d'appels pour votre organisation, vous devez comprendre comment chaque composant peut être utilisé avec l'automate d'appels et comment configurer les composants. Le tableau suivant présente les composants à configurer pour les plans de numérotation, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée pour permettre à l'automate d'appels de fonctionner correctement.

### Composants de l'automate d'appels

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Indicatifs, préfixes de numéro et formats de numéro</p></td>
<td><p>La messagerie unifiée utilise des indicatifs, préfixes de numéros et formats de numéros pour déterminer le numéro approprié à composer pour un appel sortant. Vous pouvez configurer des indicatifs, préfixes de numéro et formats de numéro pour restreindre les appels sortants des utilisateurs qui appellent un standard automatique de messagerie unifiée associé à un plan de numérotation de messagerie unifiée, ou des utilisateurs qui appellent un numéro Outlook Voice Access configuré sur le plan de numérotation.</p></td>
</tr>
<tr class="even">
<td><p>Groupes de règles de numérotation</p></td>
<td><p>Des groupes de règles de numérotation sont créés pour permettre aux numéros de téléphone d’être modifiés avant d’être envoyés au PBX pour les appels sortants. Les groupes de règles de numérotation suppriment ou ajoutent des chiffres aux numéros de téléphone composés par la messagerie unifiée. Par exemple, vous pouvez créer un groupe de règles de numérotation qui ajoute automatiquement le chiffre 9 comme préfixe à un numéro de téléphone de 7 chiffres pour donner accès à une ligne extérieure. Dans cet exemple, les utilisateurs qui passent des appels sortants ne doivent pas composer le 9 avant le numéro de téléphone pour joindre une personne extérieure à l'organisation.</p>
<p>Chaque groupe de règles de numérotation contient des règles de numérotation qui déterminent les types d'appels nationaux/régionaux et internationaux que les utilisateurs faisant partie de ce groupe peuvent passer. Les groupes de règles de numérotation s'appliquent aux utilisateurs associés à un plan de numérotation de messagerie unifiée, ou aux standards automatiques et stratégies de boîte aux lettres de messagerie unifiée associés au plan de numérotation de messagerie unifiée. Chaque groupe de règles de numérotation contient au moins une règle.</p></td>
</tr>
<tr class="odd">
<td><p>Entrées de règle de numérotation</p></td>
<td><p>Une de règle de numérotation permet de déterminer les types d'appels que les utilisateurs appartenant à un groupe de règles de numérotation peuvent passer. Lorsque vous créez un groupe de règles de numérotation, vous configurez une ou plusieurs règles de numérotation.</p>
<p>Lorsque vous configurez une règle de numérotation, vous devez entrer son nom, le type de numéro à transformer (<em>masque de numéro</em>) et le numéro composé. Vous pouvez également entrer un commentaire. Les commentaires permettent de décrire la manière dont la règle de numérotation est utilisée, ou de décrire un groupe d'utilisateurs auxquels elle s'applique. Lorsque vous ajoutez un masque de numéro et le numéro composé à une règle de numérotation, vous pouvez substituer la lettre x à un chiffre du numéro de téléphone, par exemple, 91425xxxxxxx. Vous pouvez également utiliser le symbole astérisque (*) comme caractère générique, par exemple, 91425*.</p></td>
</tr>
<tr class="even">
<td><p>Autorisations de numérotation</p></td>
<td><p>Une autorisation de numérotation utilise des groupes de règles de numérotation pour appliquer des restrictions de numérotation à des utilisateurs associés à une stratégie de boîte aux lettres, à un plan de numérotation ou à un standard automatique de messagerie unifiée spécifique. Il est également possible de les utiliser pour permettre à des utilisateurs d'établir des appels vers des numéros de téléphone nationaux/régionaux ou internationaux.</p>
<p>Après avoir créé des règles de numérotation sur un plan de numérotation de messagerie unifiée, vous ajoutez le groupe de règles de numérotation à une stratégie de boîte aux lettres, à un plan de numérotation ou à un standard automatique de messagerie unifiée. Une fois le groupe de règles de numérotation ajouté à une stratégie de boîte aux lettres de messagerie unifiée, l'ensemble des paramètres ou règles définis s'appliquent aux utilisateurs à extension messagerie unifiée associés à la stratégie de boîte aux lettres de messagerie unifiée.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Configuration de l'automate d'appels

Un groupe de règles de numérotation se compose d'une ou plusieurs règles de numérotation configurées sur un plan de numérotation de messagerie unifiée. Deux types de groupes de règles de numérotation peuvent être configurés pour un plan de numérotation de messagerie unifiée : national/régional et international. Les groupes de règles de numérotation nationales/régionales s'appliquent à des numéros de téléphone composés à l'intérieur du pays ou de la région. Les groupes de règles de numérotation internationales s'appliquent aux numéros de téléphone internationaux composés à partir d'un pays ou d'une région vers un autre pays ou une autre région.

Chaque plan de numérotation de messagerie unifiée peut contenir un ou plusieurs groupes de règles de numérotation. Pour appliquer un groupe de règles de numérotation à un ensemble d'utilisateurs, après l'avoir créé, vous devez l'ajouter à la liste des groupes de règles de numérotation autorisés pour le plan de numérotation, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée associés au plan de numérotation de messagerie unifiée.

Les groupes de règles de numérotation vous permettent de spécifier des règles de numérotation à appliquer à un groupe d'utilisateurs à extension messagerie unifiée appartenant à une catégorie spécifique. Par exemple, vous pouvez utiliser des groupes de règles de numérotation pour spécifier le groupe d'utilisateurs qui peut passer des appels internationaux et le groupe qui ne peut passer que des appels nationaux ou locaux. Vous pouvez créer un groupe de règles de numérotation à l'aide du Centre d'administration Exchange (CAE) ou de la cmdlet **Set-UMDialPlan** dans l'environnement de ligne de commande Exchange Management Shell. Lorsque vous créez un groupe de règles de numérotation, vous devez définir au moins une règle de numérotation pour ce groupe.

Quand un utilisateur compose un numéro de téléphone, la messagerie unifiée vérifie si l'une des règles de numérotation correspond à ce numéro. Si la messagerie unifiée trouve une correspondance, elle utilise la règle de numérotation pour déterminer le numéro à composer en consultant le numéro de téléphone ou les chiffres répertoriés dans la section **Numéro composé** de la règle de numérotation. Le numéro figurant dans le champ **Numéro composé** de la règle de numérotation est celui qui sera composé.

Le tableau suivant présente un exemple de groupes de règles de numérotation et de règles de numérotation. Dans cet exemple, Local-Calls-Only et Low-Rate sont les groupes de règles de numérotation qui ont été créés. Le groupe de règles de numérotation Local-Calls-Only comporte deux règles de numérotation : 91425\* et 91206\*. Par ailleurs, la règle de numérotation Low-Rate comporte également deux règles de numérotation : 91509\* et 91360\*.

### Groupes de règles de numérotation et règles de numérotation

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>NumberMask</th>
<th>DialedNumber</th>
<th>Commentaire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local-Calls-Only</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>Appels locaux</p></td>
</tr>
<tr class="even">
<td><p>Local-Calls-Only</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>Appels locaux</p></td>
</tr>
<tr class="odd">
<td><p>Low-Rate</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>Appels nationaux</p></td>
</tr>
<tr class="even">
<td><p>Low-Rate</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>Appels nationaux</p></td>
</tr>
</tbody>
</table>


Par exemple, quand un utilisateur compose le numéro 9-1-425-555-1234, la messagerie unifiée compose le numéro 4255551234. La messagerie unifiée supprime tout caractère non numérique (dans cet exemple, les tirets) et applique le masque de numéro de la règle de numérotation. Dans cet exemple, la messagerie unifiée applique le masque de numéro 91\*. Celui-ci indique au serveur de messagerie unifiée de ne pas composer les chiffres 9 et 1, mais de composer tous les autres chiffres du numéro de téléphone qui s'affichent à droite du chiffre 1. Il s'agit de tous les chiffres représentés par l'astérisque (\*).

Le CAE et l'environnement de ligne de commande Exchange Management Shell permettent de créer et de configurer un ou plusieurs groupes de règles de numérotation pour les appels nationaux/régionaux et internationaux et les règles de numérotation. En revanche, si vous créez des groupes de règles de numérotation et des règles de numérotation nombreux ou complexes, vous pouvez utiliser un fichier .csv (valeurs séparées par des virgules) dans l'environnement de ligne de commande. Vous pouvez importer ou exporter une liste de groupes de règles de numérotation et de règles de numérotation.

Pour importer une liste de groupes de règles de numérotation et de règles de numérotation que vous avez définie dans un fichier .csv, exécutez la cmdlet **Set-UMDialPlan** comme suit :

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

Pour extraire une liste des groupes de règles de numérotation configurés sur un plan de numérotation de messagerie unifiée, exécutez la cmdlet **Get-UMDialPlan**, comme suit :

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

Le fichier .csv doit être créé et enregistré au format correct. Chaque ligne du fichier .csv représente une règle de numérotation. En revanche, chaque règle de numérotation est configurée sur le même groupe de règles de numérotation. Chaque règle du fichier comporte quatre sections séparées par des virgules. Ces sections reprennent le nom, le masque de numéro, le numéro composé et un commentaire. Chaque section est obligatoire et vous devez y entrer des informations correctes, à l'exception de la section de commentaire. Il ne peut pas y avoir d'espaces entre l'entrée de texte et la virgule de la section suivante, et il ne peut pas y avoir de ligne vide entre des règles ou à la fin. Voici un exemple de fichier .csv que vous pouvez utiliser pour créer des groupes de règles de numérotation et des règles de numérotation nationales/régionales :

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9xxxxxxx,9xxxxxxx,Local call**

**Any,91\*,91\*,Open access to in-country/region numbers**

**Long-distance,91408\*,91408\*,long distance**

Voici un exemple de fichier .csv que vous pouvez utiliser pour créer des groupes de règles de numérotation et des règles de numérotation internationales.

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, international call**

**International, 901133\*, 901133\*, international call**

Retour au début

## Application des groupes de règles de numérotation configurés

Les groupes de règles de numérotation sont créés sur un plan de numérotation de messagerie unifiée. Vous pouvez créer des groupes de règles de numérotation nationales/régionales ou internationales à l'aide de du CAE ou de la cmdlet **Set-UMDialPlan** dans l'environnement de ligne de commande. Après avoir créé les groupes de règles de numérotation appropriés sur un plan de numérotation de messagerie unifiée et défini les entrées de règle de numérotation, vous pouvez appliquer les groupes de règles de numérotation que vous avez créés à un plan de numérotation ou à un standard automatique de messagerie unifiée, ou à des utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée, puis autoriser l'automate d'appels en fonction de la manière dont l'utilisateur accède au système de messagerie vocale.

Vous pouvez appliquer les groupes de règles de numérotation que vous avez créés sur un plan de numérotation de messagerie unifiée aux éléments suivants :

  - **Même plan de numérotation**   Les paramètres s'appliquent à tous les utilisateurs qui appellent le numéro Outlook Voice Access, mais ne se connectent pas à leur boîte aux lettres. Pour appliquer un groupe de règles de numérotation nationale/régionale nommé `MyAllowedDialRuleGroup` au même plan de numérotation, utilisez la cmdlet **Set-UMDialPlan** de l'environnement de ligne de commande.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Une ou plusieurs stratégies de boîte aux lettres de messagerie unifiée   **Les paramètres configurés sur une stratégie de boîte aux lettres de messagerie unifiée s'appliquent à tous les utilisateurs associés à cette stratégie. Les paramètres configurés sur une stratégie de boîte aux lettres de messagerie unifiée s'appliquent aux utilisateurs qui appellent un numéro Outlook Voice Access et se connectent à leur boîte aux lettres . Pour appliquer un groupe de règles de numérotation nationale/régionale nommé `MyAllowedDialRuleGroup` à une seule stratégie de boîte aux lettres de messagerie unifiée, utilisez la page **Autorisation de numérotation** de la stratégie de boîte aux lettres dans le CAE ou la cmdlet **Set-UMMailboxPolicy** dans l'environnement de ligne commande comme suit.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Un ou plusieurs standards automatiques associés au plan de numérotation de messagerie unifiée   **Cela s'applique à tous les utilisateurs qui appellent un standard automatique de messagerie unifiée. Pour appliquer le groupe de règles de numérotation nationale/régionale nommé `MyAllowedDialRuleGroup` à un seul standard automatique de messagerie unifiée, utilisez la page **Autorisation de numérotation** du standard automatique dans le CAE ou la cmdlet **Set-UMAutoAttendant** dans l'environnement de ligne commande comme suit.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

Le tableau suivant résume la manière dont les groupes de règles de numérotation sont appliqués dans une messagerie unifiée.

### Application des règles de l'automate d'appels

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Type d'appelant</th>
<th>Étendue</th>
<th>Paramètres de l'automate d'appels appliqués</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numéro Outlook Voice Access</p></td>
<td><p>L'utilisateur appelle un numéro Outlook Voice Access et se connecte à sa boîte aux lettres</p></td>
<td><p>Stratégie de boîte aux lettres de messagerie unifiée</p></td>
</tr>
<tr class="even">
<td><p>Appelant anonyme</p></td>
<td><p>L'utilisateur appelle un numéro Outlook Voice Access de plan de numérotation</p></td>
<td><p>Plan de numérotation de messagerie unifiée</p></td>
</tr>
<tr class="odd">
<td><p>Appelant anonyme</p></td>
<td><p>L'utilisateur appelle un numéro pilote de standard automatique ou de poste</p></td>
<td><p>Standard automatique de messagerie unifiée</p></td>
</tr>
<tr class="even">
<td><p>Appelant de l'intérieur de l'organisation</p></td>
<td><p>L'utilisateur appelle le numéro Émettre au téléphone</p></td>
<td><p>Stratégie de boîte aux lettres de messagerie unifiée</p></td>
</tr>
</tbody>
</table>


Retour au début

## Application des règles de numérotation

Le processus d'automate d'appels intervient dans les cas suivants :

  - La messagerie unifiée passe un appel vers un numéro de téléphone externe pour l'appelant.

  - La messagerie unifiée transfère un appel à un standard automatique.

  - La messagerie unifiée transfère un appel vers un utilisateur au sein de votre organisation.

  - Un utilisateur à extension messagerie unifiée utilise la fonctionnalité Émettre au téléphone.

Dans chaque scénario d'automate d'appels, une messagerie unifiée applique les règles de numérotation configurées, puis passe l'appel pour l'utilisateur. Toutefois, en fonction du scénario et de la manière dont l'utilisateur passe l'appel, la messagerie unifiée peut appliquer uniquement certaines règles de numérotation au numéro de téléphone composé. Dans d'autres scénarios d'automate d'appels, la messagerie unifiée applique toutes les règles de l'automate d'appels configurées au numéro de téléphone composé.

Retour au début

