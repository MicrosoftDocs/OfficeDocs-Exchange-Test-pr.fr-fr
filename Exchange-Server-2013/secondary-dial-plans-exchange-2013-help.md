---
title: 'Plans de numérotation secondaires: Exchange 2013 Help'
TOCTitle: Plans de numérotation secondaires
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54915108
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Plans de numérotation secondaires

 

_**Sapplique à :** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2015-03-09_

Quand vous activez la messagerie unifiée pour un utilisateur, vous devez attribuer un numéro de poste et une stratégie de boîte aux lettres de messagerie unifiée qui associera l'utilisateur à un plan de numérotation de messagerie unifiée Après avoir activé la messagerie unifiée pour l'utilisateur, vous pouvez attribuer des numéros de poste supplémentaires pour cet utilisateur dans le même plan de numérotation, mais les numéros de poste au sein de ce plan de numérotation doivent être uniques. Dans certains déploiements, le même numéro de poste doit être attribué à un utilisateur dans deux plans de numérotation distincts. Si c'est le cas, vous pouvez associer l'utilisateur à un plan de numérotation de messagerie unifiée secondaire. Cette opération peut être utile, par exemple, si l'utilisateur possède deux téléphones physiques ou se déplace d'un lieu à un autre.

**Table des matières**

Vue d’ensemble

Use of secondary extensions

UM features that operate differently for secondary dial plans

## Vue d'ensemble

Quand vous activez la messagerie unifiée pour un utilisateur, vous devez définir un numéro de poste et une stratégie de boîte aux lettres de messagerie unifiée qui associe l'utilisateur à un plan de numérotation de messagerie unifiée unique. Quand vous activez la messagerie unifiée pour un utilisateur et que celui-ci est lié à une stratégie de boîte aux lettres de messagerie unifiée liée à un plan de numérotation URI SIP ou E.164, vous devez aussi fournir une adresse SIP ou un numéro E.164 avec le numéro de poste de l’utilisateur. La messagerie unifiée utilise le plan de numérotation et l'extension, avec l'adresse SIP ou le numéro E.164, pour localiser l'utilisateur quand un message vocal est soumis à la boîte aux lettres de l'utilisateur.

Si vous utilisez des plans de numérotation de poste téléphonique et si vous devez fournir le même numéro de poste pour un utilisateur, vous devez créer un plan de numérotation secondaire, activer la messagerie unifiée pour l’utilisateur et indiquer le même numéro de poste pour l’utilisateur. car le numéro de poste doit être unique dans un plan de numérotation.

> [!NOTE]
> Il n'y a aucune limite au nombre de numéros de poste secondaires que vous pouvez ajouter pour un utilisateur à extension messagerie unifiée.


Parfois, un utilisateur se déplace d'un lieu à un autre, possède deux téléphones au minimum ou veut recevoir ses messages vocaux sur un numéro de poste DID (Direct Inward Dial) et ses messages de télécopie sur un autre numéro de poste DID. Pour ce faire, vous devez ajouter un poste DID supplémentaire à la boîte aux lettres de l'utilisateur et, dans certains cas, ajouter un plan de numérotation secondaire.

Dans certaines configurations, après avoir ajouté un deuxième poste sur un plan de numérotation principal ou ajouté un seul ou plusieurs numéros de poste à un plan de numérotation secondaire, l'utilisateur peut recevoir des messages vocaux ou des télécopies en utilisant un ou plusieurs numéros de poste. Si vous voulez que la messagerie unifiée réponde à ces appels de télécopie et les envoie au deuxième numéro de poste DID, vous devez configurer l'équipement téléphonique dans votre organisation pour transférer les appels de télécopie vers le deuxième numéro de poste DID.

La boîte aux lettres d'un utilisateur à extension messagerie unifiée peut toutefois être associée à :

  - un numéro de poste, une adresse SIP (Session Initiation Protocol) ou une adresse E.164 unique dans un seul plan de numérotation ;

  - plusieurs numéros de poste sur un seul plan de numérotation ;

  - plusieurs numéros de poste sur deux plans de numérotation distincts.

Quand la messagerie unifiée est activée pour un utilisateur, vous devez spécifier un numéro de poste et une stratégie de boîte aux lettres de messagerie unifiée. La messagerie unifiée a besoin du numéro de poste pour identifier l'utilisateur quand celui-ci se connecte à Outlook Voice Access pour récupérer des messages. La stratégie de boîte aux lettres de messagerie unifiée contient une collection de propriétés de configuration avec des valeurs que la messagerie unifiée attribue à tout utilisateur à extension messagerie unifiée dans le cadre de cette stratégie. La stratégie de boîte aux lettres de messagerie unifiée est similaire à la « classe de service » présente dans d'autres systèmes (par exemple, messagerie vocale ou PBX), en ceci que modifier une valeur de stratégie de boîte aux lettres de messagerie unifiée peut affecter le comportement pour de nombreux utilisateurs associés.

Une propriété d'une stratégie de boîte aux lettres de messagerie unifiée fait référence à un plan de numérotation de messagerie unifiée. Cela représente un groupe de postes téléphoniques. Le plan de numérotation de ce groupe n'autorise pas les doublons parmi les numéros de postes.

Par conséquent, le numéro de poste d’un utilisateur est unique dans le plan de numérotation de messagerie unifiée dans lequel l’extension messagerie unifiée est activée. En fait, la paire plan de numérotation de messagerie unifiée/numéro de poste doit être unique au sein de l'organisation. Ainsi, la messagerie unifiée identifie de manière unique un utilisateur à extension messagerie unifiée dans une organisation. Utiliser un plan de numérotation secondaire permet de pouvoir garder plus facilement le plan de numérotation et le numéro de poste uniques au sein d'une organisation. Imaginez par exemple qu'une organisation possède deux plans de numérotation de messagerie unifiée : plan de numérotation A et plan de numérotation B. Le numéro de poste d'un utilisateur dans le plan de numérotation A est 55555 et, dans le plan de numérotation B, 66666. Lorsque vous utilisez un plan de numérotation secondaire, le poste de l'utilisateur du plan de numérotation A peut être 55555 et son poste dans le plan de numérotation B peut également être 55555. Dans les deux cas, le poste de l'utilisateur au sein du plan de numérotation utilisé est unique.

Le tableau suivant définit les termes utilisés pour décrire les postes principaux et secondaires, les numéros Outlook Voice Access et les plans de numérotation de messagerie unifiée.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Terme</th>
<th>Définition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>extension principale</p></td>
<td><p>Le numéro de poste indiqué lorsque l'utilisateur a une extension de messagerie unifiée.</p></td>
</tr>
<tr class="even">
<td><p>plan de numérotation principal</p></td>
<td><p>Le plan de numérotation principal de messagerie unifiée indiqué lorsque l'utilisateur a une extension messagerie unifiée. L'utilisateur à extension messagerie unifiée est associé au plan de numérotation lorsque l'utilisateur est lié à la stratégie de boîte aux lettres de messagerie unifiée.</p></td>
</tr>
<tr class="odd">
<td><p>numéro Outlook Voice Access principal</p></td>
<td><p>Numéro Outlook Voice Access pour le plan de numérotation principal de l’utilisateur. Les appels de l'utilisateur sont transférés à ce numéro en cas d'absence de réponse ou si la ligne est occupée. Il s'agit également du numéro que l'utilisateur compose quand il souhaite se connecter à Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p>extension secondaire</p></td>
<td><p>Un ou plusieurs numéros de poste qui peuvent être ajoutés à la configuration d’un utilisateur à extension messagerie unifiée.</p></td>
</tr>
<tr class="odd">
<td><p>plan de numérotation secondaire</p></td>
<td><p>Un plan de numérotation secondaire différent du plan de numérotation principal dans lequel une ou plusieurs extensions secondaires peuvent être configurées.</p></td>
</tr>
<tr class="even">
<td><p>numéro Outlook Voice Access secondaire</p></td>
<td><p>Numéro Outlook Voice Access du plan de numérotation secondaire d’un utilisateur. Un utilisateur peut composer ce numéro à partir du numéro de poste secondaire quand il souhaite se connecter à Outlook Voice Access.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Utilisation de postes secondaires

Dans la plupart des déploiements, une seule extension est configurée par utilisateur à extension messagerie unifiée. Cependant, certains déploiements plus avancés exigent que vous ajoutiez des extensions secondaires pour vos utilisateurs.

Quand Microsoft Lync Server est utilisé pour la fonctionnalité Voix Entreprise, la messagerie unifiée peut fournir le système de messagerie vocale. Cependant, le plan de numérotation de messagerie unifiée utilisé pour la fonctionnalité Voix Entreprise doit être un plan de numérotation URI SIP spécifique des configurations de messagerie unifiée avec Lync Server. Dans ces déploiements, l’extension de l’utilisateur est fournie par un point de terminaison des communications unifiées Microsoft, tel que MicrosoftOffice Communicator, exécuté sur l’ordinateur de l’utilisateur, ou Office Communicator Phone Edition, exécuté sur un appareil téléphonique IP pris en charge. Ainsi, dans la plupart des cas, le plan de numérotation principal de l’utilisateur doit être le même plan de numérotation URI SIP que celui utilisé avec Lync Server. Mais si l'utilisateur demande davantage de numéros de poste, vous ne devez pas ajouter d'autre extension secondaire au plan de numérotation principal. Vous devez ajouter un plan de numérotation secondaire, puis ajouter l'extension secondaire ou l'adresse proxy EUM à l'utilisateur à extension messagerie unifiée.

Pour plus d'informations sur l'ajout, la suppression ou la modification de postes, consultez l'une des rubriques suivantes :

  - [Modifier un numéro de poste](change-an-extension-number-exchange-2013-help.md)

  - [Ajouter un numéro de poste](add-an-extension-number-exchange-2013-help.md)

  - [Supprimer un numéro de poste](remove-an-extension-number-exchange-2013-help.md)

Si vous devez modifier des adresses SIP ou des numéros E.164 pour des utilisateurs à extension messagerie unifiée, consultez les rubriques suivantes :

  - [Ajouter une adresse SIP](add-a-sip-address-exchange-2013-help.md)

  - [Modifier une adresse SIP](change-a-sip-address-exchange-2013-help.md)

  - [Supprimer une adresse SIP](remove-a-sip-address-exchange-2013-help.md)

  - [Ajouter un numéro E.164](add-an-e-164-number-exchange-2013-help.md)

  - [Modifier un numéro E.164](change-an-e-164-number-exchange-2013-help.md)

  - [Supprimer un numéro E.164](remove-an-e-164-number-exchange-2013-help.md)

## Répondeur automatique

La messagerie unifiée offre les deux éléments suivants :

  - **Répondeur automatique**   Se produit quand l'utilisateur ne répond pas au téléphone et que la messagerie unifiée prend l'appel.

  - **Outlook Voice Access**   Utilisé par les utilisateurs quand ils se connectent au système de messagerie vocale pour accéder à leur boîte aux lettres.

On utilise fréquemment deux configurations :

  - Un utilisateur à extension messagerie unifiée a deux numéros de poste (un principal, un secondaire) dans le plan de numérotation principal. Ces extensions correspondent aux différents téléphones du bureau de l'utilisateur et sont connectés au même PBX. Ces différents numéros sont disponibles pour deux audiences distinctes. Dans cette configuration, l'extension principale correspond au numéro professionnel « général » et l'extension secondaire au numéro « spécifique à une tâche », une ligne d'assistance ou un numéro de télécopie dédié par exemple.

  - Un utilisateur à extension messagerie unifiée passe une certaine période, peut-être trois semaines sur quatre, dans le bureau principal de son entreprise et le reste du temps dans un autre bureau sur l’un des sites distants de l’entreprise. Les deux bureaux ont des PBX différents et les numéros de poste sont uniques à chaque PBX. Dans cet exemple, la configuration de l'utilisateur compte une extension principale dans le plan de numérotation principal du PBX du bureau principal et une extension secondaire dans un plan de numérotation secondaire sur le PBX de l'autre bureau.

Dans les deux configurations, les messages vocaux ou les messages de notification d’appel en absence qui sont générés en cas d’appels sans réponse à l’une ou l’autre des extensions seront envoyés à la boîte de réception de l’utilisateur.

## Outlook Voice Access

Vous souhaitez peut-être que les utilisateurs à extension messagerie unifiée puissent se connecter à Outlook Voice Access depuis n'importe quel poste, principal ou secondaire. Même si cette option est possible, toutes les extensions n'auront peut-être pas le même fonctionnement en raison de certaines restrictions architecturales. Pour se connecter à Outlook Voice Access, les utilisateurs à extension messagerie unifiée doivent procéder comme suit :

1.  Composer un numéro Outlook Voice Access.

2.  Saisir leur numéro de poste en cas d'appel depuis un autre numéro de téléphone.

3.  Entrer leur code confidentiel si la fonctionnalité Voix Entreprise n'est pas activée et qu'ils appellent depuis un téléphone de communications unifiées, Office Communicator ou Lync Server.

**Scénarios d'utilisation**

  - **Poste unique avec Outlook Voice Access**   Si l'utilisateur a un seul poste principal, il doit toujours appeler numéro Outlook Voice Access de son plan de numérotation de messagerie unifiée principal. S'il appelle depuis son numéro de poste, il ne sera pas invité à saisir son numéro de poste et l'étape 2 des étapes précédentes est ignorée.

  - **Deux postes dans le plan de numérotation principal avec Outlook Voice Access**   Si l'utilisateur n'a que deux postes, un principal et un secondaire, et que ces deux postes se trouvent dans le même plan de numérotation de messagerie unifiée, il doit toujours appeler le numéro Outlook Voice Access du plan de numérotation. S'il appelle à partir de l'extension principale ou secondaire, il ne sera pas invité à saisir son numéro de poste et l'étape 2 des étapes précédentes est ignorée. Les fonctionnalités d'Outlook Voice Access sont les mêmes, peu importe le poste utilisé pour se connecter.

  - **Postes dans le plan de numérotation principal et dans un plan de numérotation secondaire avec Outlook Voice Access**   Si l'utilisateur n'a que deux poste, un principal et un secondaire, et que ces deux postes se trouvent dans des plans de numérotation de messagerie unifiée différents (principal et secondaire), il doit appeler le numéro Outlook Voice Access correspondant à son plan de numérotation. Depuis son poste principal, il doit appeler le numéro Outlook Voice Access du plan de numérotation principal, et depuis son poste secondaire, le numéro Outlook Voice Access du plan de numérotation secondaire. S'il procède de la sorte, il ne sera pas invité à saisir son numéro de poste et l'étape 2 des étapes précédentes est ignorée.
    
    Les fonctionnalités d'Outlook Voice Access n'impliquant pas de numérotation sortante (« Appeler l'expéditeur » ou « Appeler le bureau », par exemple) sont les mêmes, peu importe le poste utilisé pour se connecter. Cependant, les fonctionnalités d'Outlook Voice Access impliquant une numérotation sortante ne fonctionnent pas comme prévu quand l'utilisateur se connecte au plan de numérotation secondaire, sauf si les règles de numérotation sortante sont exactement les mêmes dans les deux plans de numérotation. Pour garantir un comportement identique en matière de numérotation sortante, vous devez vérifier que la configuration des propriétés suivantes est identique dans les plans de numérotation principal et secondaire :
    
      - Codes de numérotation (accès spécialisé, national et international)
    
      - Codes de numérotation nationaux ou régionaux
    
      - Règles de numérotation
    
      - Noms de groupe de règles de numérotation

Un utilisateur à extension messagerie unifiée est associé à une stratégie de boîte aux lettres de messagerie unifiée, et cette stratégie est liée au plan de numérotation principal de l'utilisateur. Les paramètres de stratégie de boîte aux lettres de messagerie unifiée associés au plan de numérotation principal de l'utilisateur à extension messagerie unifiée seront appliqués à l'utilisateur. Si un utilisateur est associé à un plan de numérotation secondaire possédant un deuxième numéro de poste dans le plan de numérotation secondaire, les paramètres de stratégie de boîte aux lettres de messagerie unifiée associés au plan de numérotation principal seront encore appliqués. Dans Outlook Voice Access, les mêmes paramètres de stratégie de boîte aux lettres de messagerie unifiée que ceux associés au plan de numérotation principal sont appliqués, que l'utilisateur appelle le plan de numérotation principal ou un plan de numérotation secondaire.

Les propriétés **AllowedInCountryOrRegionGroups** et **AllowedInternationalGroups** de la stratégie de boîte aux lettres de messagerie unifiée contiennent les noms des groupes de règles de numérotation qui sont configurés dans les propriétés **ConfiguredInCountryOrRegionGroups** et **ConfiguredInternationalGroups** d'un plan de numérotation de messagerie unifiée. Quand un utilisateur à extension messagerie unifiée appelle Outlook Voice Access, les règles d'appels sortants de la stratégie de boîte aux lettres de messagerie unifiée associées au plan de numérotation principal ou secondaire sont appliquées aux appels émis par l'utilisateur, selon que l'utilisateur à extension messagerie unifiée ait appelé le numéro Outlook Voice Access du plan de numérotation principal ou secondaire.

Par exemple, si un plan de numérotation principal nommé « Plan de numérotation Contoso 1 » possède une règle de numérotation nommée « États-Unis et Canada » dans sa propriété **ConfiguredInCountryOrRegionGroups**, la propriété **AllowedInCountryOrRegionGroups** de la stratégie de boîte aux lettres de messagerie unifiée « Stratégie de messagerie unifiée Contoso 1 » peut également contenir la règle « États-Unis et Canada ». Si vous voulez ajouter une extension secondaire dans « Plan de numérotation Contoso 2 » pour un utilisateur de « Stratégie de messagerie unifiée Contoso 2 », vous devrez vous assurer que la propriété **ConfiguredInCountryOrRegionGroups** de « Plan de numérotation Contoso 2 » contient également une règle appelée « États-Unis et Canada ». Dans le cas contraire, si l'utilisateur se connecte à Outlook Voice Access à partir de son poste secondaire, la messagerie unifiée ne trouve pas de règle nommée « États-Unis et Canada » dans le plan de numérotation secondaire. Dans ce cas, la messagerie unifiée permet simplement à l'utilisateur de composer des numéros autorisés pour tout appelant du plan de numérotation secondaire, méthode qui pourrait s'avérer plus restrictive.

Retour au début

## Fonctionnalités de la messagerie unifiée fonctionnant différemment pour les plans de numérotation secondaire

Certaines fonctions de messagerie unifiée peuvent utiliser des plans de numérotation secondaires mais ne fonctionnent pas correctement dans certaines situations. Il est important de comprendre la manière dont chacune de ces fonctions est affectée lorsque vous configurez des utilisateurs à extension messagerie unifiée qui utilisent un plan de numérotation secondaire.

## Émettre au téléphone

Dans Outlook Web App, la fonctionnalité Émettre au téléphone utilise la passerelle VoIP associée au plan de numérotation principal de l’utilisateur pour passer l’appel sortant. Elle applique les règles de numérotation du plan de numérotation principal et la stratégie de boîte aux lettres de messagerie unifiée associée à la boîte aux lettres de l'utilisateur.

## Recherche de répertoires (Outlook Voice Access)

Le recherche de répertoire pour un utilisateur ayant été authentifié respectera les règles suivantes :

  - Il ne sera possible de rechercher un utilisateur puis de lui laisser un message vocal ou d'appeler un utilisateur que si l'utilisateur effectuant la recherche est à extension messagerie unifiée et possède un poste principal dans le même plan de numérotation que l'utilisateur appelé. Dans ce cas, une recherche par nom, alias et extension principale permettra de localiser l'utilisateur. Cependant, une recherche à l'aide de l'extension secondaire ne permettra pas de localiser l'utilisateur.

  - Si l'utilisateur faisant l'objet de la recherche est activé pour la messagerie unifiée et possède une extension secondaire dans le plan de numérotation appelé, alors une recherche par nom, alias et extension secondaire permettra de le localiser. Cependant, même si les options permettant de laisser un message vocal et d'appeler le contact sont proposées, l'option Appel du contact échoue. Dans ce cas, une recherche en fonction de l'extension principale ne permettra pas de localiser l'utilisateur.

  - Pour localiser et pouvoir appeler ou laisser un message vocal à l'utilisateur recherché, l'utilisateur à extension messagerie unifiée doit utiliser Outlook Voice Access via le numéro Outlook Voice Access de son plan de numérotation principal et effectuer une recherche par nom, alias ou poste principal. En cas d'appel passé à l'utilisateur recherché à l'aide du numéro Outlook Voice Access du plan de numérotation secondaire, la recherche de l'utilisateur n'aboutit que si elle est effectuée en utilisant le nom, l'alias ou le poste secondaire. Si l'utilisateur a recours à l'extension principale, il aura uniquement la possibilité de laisser un message vocal.

## Recherche de répertoires (Outlook Voice Access)

Le recherche de répertoire pour un utilisateur n'ayant pas été authentifié respectera les règles suivantes :

  - L'utilisateur recherché sera localisé et l'option permettant de lui laisser un message vocal ou de l'appeler ne sera disponible que si l'utilisateur est activé pour la messagerie unifiée et possède une extension principale dans le plan de numérotation appelé. Dans ce cas, une recherche par nom, alias et extension principale permettra de localiser l'utilisateur. Cependant, une recherche à l'aide de l'extension secondaire ne permettra pas de localiser l'utilisateur.

  - Si l’utilisateur recherché est à extension messagerie unifiée, possède un poste secondaire dans le plan de numérotation appelé et que l’option **Transfert et recherche** \> **Autoriser les appelants à** \> **Laisser des messages vocaux sans faire sonner le téléphone de l’utilisateur** est sélectionnée dans le plan de numérotation appelé, alors une recherche par nom, alias ou poste secondaire permettra de le localiser. Cependant, l'appelant aura la possibilité de laisser un message vocal, mais il ne pourra pas appeler.

  - Pour localiser un utilisateur et pouvoir l'appeler ou lui laisser un message vocal, l'appelant doit composer le numéro Outlook Voice Access du plan de numérotation principal de l'utilisateur et effecteur une recherche en fonction du nom, de l'alias ou du poste secondaire de l'utilisateur. En cas d'appel du numéro Outlook Voice Access secondaire de l'utilisateur, ce dernier n'est localisé que si l'option **Autoriser les appelants à rechercher par nom ou alias** est définie sur **Dans toute l'organisation**. Dans ce cas, seule l'option permettant de laisser un message vocal sera proposée.

## Appeler l'expéditeur (Outlook Voice Access)

Quand un utilisateur appelle Outlook Voice Access et sélectionne l'option Appeler l'expéditeur, il peut envoyer un message électronique ou un message vocal à un utilisateur à extension messagerie unifiée. Les options disponibles varient selon que l'appelant est associé au même plan de numérotation que l'expéditeur appelé. Les appels passés à un utilisateur à extension messagerie unifiée quand l'appelant compose un numéro Outlook Voice Access et que l'appelant est authentifié respectent les règles suivantes :

  - **Messages électroniques**   Si l’expéditeur du message électronique est un utilisateur à extension messagerie unifiée, sélectionner l’option Appeler l’expéditeur se traduit par un appel à l’extension principale de l’expéditeur configurée dans le plan de numérotation principal de l’utilisateur. Dans le cas où le poste principal de l’expéditeur se trouve dans un plan de numérotation différent de celui de l’appelant, l’invite « Appeler l’expéditeur » ne sera proposée que si un numéro professionnel, personnel ou de mobile est configuré pour l’expéditeur et que les règles de numérotation configurées permettent cet appel.

  - **Messages vocaux**   Si l'appelant est un utilisateur à extension messagerie unifiée, la sélection de l'option Appeler l'expéditeur se traduit toujours par un appel au poste que l'expéditeur utilise pour laisser son message vocal. Si plusieurs chiffres de cette extension sont différents de ceux du plan de numérotation appelé, l'invite Appeler l'expéditeur ne sera pas proposée, à moins que les règles de numérotation en place n'autorisent l'appel. Par exemple :
    
      - L'option « Appeler l'expéditeur » ne sera proposée que si l'expéditeur utilise une extension du plan de numérotation qui a été utilisé pour envoyer le message vocal.
    
      - L'option « Appeler l'expéditeur » sera exécutée si l'expéditeur utilise une extension d'un plan de numérotation différent du plan utilisé avec Outlook Voice Access pour envoyer le message vocal et si les deux plans de numérotation ont le même nombre de chiffres. L'appel aboutira si la passerelle VoIP et l'infrastructure du PBX autorisent le transfert d'appels
    
      - L'option « Appeler l'expéditeur » ne sera pas exécutée si l'expéditeur utilise une extension d'un plan de numérotation différent du plan utilisé avec Outlook Voice Access pour envoyer le message vocal, si les plans de numérotation ont un nombre de chiffres différent et si aucune règle de l'automate d'appels ne correspond à l'extension de l'expéditeur.

Retour au début

