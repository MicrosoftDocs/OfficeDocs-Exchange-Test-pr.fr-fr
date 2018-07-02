---
title: 'Indicatifs, préfixes de numéro et formats de numéro: Exchange 2013 Help'
TOCTitle: Indicatifs, préfixes de numéro et formats de numéro
ms:assetid: 26d61e55-f8dd-4d25-81f1-78a87cf88bad
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb266967(v=EXCHG.150)
ms:contentKeyID: 51407166
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Indicatifs, préfixes de numéro et formats de numéro

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-05-04_

Vous pouvez configurer plusieurs codes de numérotation utilisés par la messagerie unifiée pour établir des appels internes et externes pour les utilisateurs à extension messagerie unifiée. Il arrive fréquemment que vous souhaitiez configurer un plan de numérotation avec des codes de numérotation ou des codes d'accès, un préfixe de numéro national ou des formats de numéros nationaux, régionaux ou internationaux de façon à pouvoir contrôler la numérotation externe pour les utilisateurs au sein de votre organisation. Cette rubrique décrit les codes de numérotation, les préfixes et formats de numéros et la manière de les utiliser pour contrôler la numérotation externe pour votre organisation.

**Contenu de cette rubrique**

Vue d'ensemble

Code d'accès à une ligne extérieure

Préfixe du numéro national

Code d’accès national/régional

Code d'accès à l'international

Formats de numéro national/régional et international

## Vue d'ensemble

L'*automate d'appels* est le processus utilisé par les utilisateurs quand ils appellent un plan de numérotation de messagerie unifiée ou un standard automatique de messagerie unifiée pour effectuer un appel vers un numéro de téléphone interne ou externe. Quand un utilisateur appelle un plan de numérotation de messagerie unifiée ou un standard automatique de messagerie unifiée pour effectuer un appel, la messagerie unifiée utilise les paramètres configurés sur le plan de numérotation, le standard automatique et les stratégies de boîte aux lettres de messagerie unifiée pour effectuer l'appel. La messagerie unifiée effectue un appel sortant dans les cas suivants :

  - quand il effectue un appel vers un numéro de téléphone externe pour l'appelant ;

  - quand il transfère un appel vers un standard automatique ;

  - quand il transfère un appel vers un utilisateur (à extension messagerie unifiée ou non) de votre organisation ;

  - quand un utilisateur à extension messagerie unifiée utilise la fonctionnalité Émettre au téléphone.

Deux types d'utilisateurs se servent de l'automate d'appels : les utilisateurs authentifiés et les utilisateurs non authentifiés. Les utilisateurs non authentifiés appellent un numéro Outlook Voice Access configuré pour un plan de numérotation de messagerie unifiée, mais ne se connectent pas à leur boîte aux lettres. Ce type d'utilisateur appelle également un numéro configuré sur un standard automatique de messagerie unifiée. Les utilisateurs authentifiés appellent un numéro Outlook Voice Access et se connectent à leur boîte aux lettres. Quand des utilisateurs appellent un numéro Outlook Voice Access, ils sont initialement considérés comme non authentifiés parce qu'ils n'ont pas fourni leur numéro de poste ni leur code confidentiel, et ne se sont pas connectés à leur boîte aux lettres. Les utilisateurs sont authentifiés après avoir fourni leur numéro de poste et leur code confidentiel et s'être connectés à leur boîte aux lettres.

Quand un utilisateur authentifié appelle un standard automatique de messagerie unifiée et effectue un appel à l'aide de l'automate d'appels, les paramètres d'automate d'appels configurés sur le plan de numérotation de messagerie unifiée et le standard automatique sont utilisés. Quand un utilisateur non authentifié appelle un numéro Outlook Voice Access configuré sur un plan de numérotation, les paramètres configurés sur celui-ci sont les seuls paramètres utilisés. Quand un utilisateur s'est connecté à sa boîte aux lettres, les paramètres de configuration du plan de numérotation et de la stratégie de boîte aux lettres de messagerie unifiée associés à l'utilisateur authentifié sont appliqués à ce dernier.

Vous devez configurer plusieurs paramètres pour contrôler l'automate d'appels pour votre organisation. Pour contrôler l'automate d'appels, vous devez configurer les plans de numérotation de messagerie unifiée, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée dans la messagerie unifiée. Vous pouvez configurer les paramètres suivants pour les plans de numérotation de messagerie unifiée, les standards automatiques et les stratégies de boîte aux lettres de messagerie unifiée afin de contrôler l'automate d'appels :

  - codes d'accès à une ligne extérieure, nationaux/régionaux et internationaux ;

  - préfixes des numéros nationaux ;

  - formats de numéros de téléphone nationaux/régionaux et internationaux ;

  - groupes de règles de numérotation nationales/régionales et internationales ;

  - groupes de règles de numérotation nationales/régionales et internationales autorisés ;

  - entrées de règle de numérotation.

Vous configurez les codes d’accès, les préfixes des numéros et les formats de numéros sur un plan de numérotation de messagerie unifiée dans la page **Codes de numérotation** du Centre d’administration Exchange (CAE). Vous pouvez également configurer les paramètres à l’aide de la cmdlet **Set-UMDialPlan** dans l’environnement de ligne de commande Exchange Management Shell. Vous pouvez choisir de configurer tous les paramètres, aucun des paramètres ou seulement certains des paramètres. Chaque paramètre contrôle une partie spécifique du processus de numérotation externe.

La messagerie unifiée utilise les codes d'accès, les préfixes de numéros et les formats de numéros pour déterminer le numéro approprié à composer. Vous pouvez les configurer afin de restreindre les appels sortants pour les utilisateurs qui composent un numéro de standard automatique de messagerie unifiée associé à un plan de numérotation de messagerie unifiée, ou qui composent un numéro Outlook Voice Access configuré pour le plan de numérotation.

Pour plus d'informations sur l'automate d'appels dans la messagerie unifiée, consultez la rubrique [Indicatifs, préfixes de numéro et formats de numéro](dial-codes-number-prefixes-and-number-formats-exchange-2013-help.md).

Vue d'ensemble

## Code d'accès à une ligne extérieure

Vous pouvez configurer un code d'accès à une ligne extérieure, également appelé *code d'accès spécialisé*, pour chaque plan de numérotation créé. Il s'agit du numéro utilisé pour accéder à une ligne téléphonique externe. Ce numéro est également configuré sur les PBX (autocommutateurs privés) ou les PBX IP de votre organisation. Dans la plupart des réseaux téléphoniques, les utilisateurs composent le numéro 9 pour accéder à une ligne externe et effectuer un appel vers un numéro externe.

Nous vous recommandons de configurer un code d'accès à une ligne extérieure pour chaque plan de numérotation que vous créez. Ce code de numérotation s’applique à tous les utilisateurs liés à une stratégie de boîte aux lettres de messagerie unifiée associée au plan de numérotation de messagerie unifiée. Lorsqu’un appelant associé au plan de numérotation effectue un appel et lorsque le plan de numérotation compose le numéro d’appel sortant, la messagerie unifiée ajoute le code d’accès à une ligne extérieure (généralement le 9) avant la chaîne du numéro composé afin que le PBX ou le PBX IP puisse composer correctement le numéro. Si vous ne configurez pas le code d’accès à une ligne extérieure, le PBX et le PBX IP risquent de ne pas reconnaître le numéro transmis. Par exemple, comme indiqué précédemment, dans de nombreuses organisations, le code d'accès que les utilisateurs composent pour accéder à une ligne extérieure est le 9. Ce code est configuré sur un PBX ou un PBX IP. La messagerie unifiée doit ajouter le code d'accès à une ligne extérieure (9) devant la chaîne du numéro de téléphone pour que le PBX ou le PBX IP puisse composer le numéro sortant correctement. Si vous configurez le code de numérotation de sorte que la messagerie unifiée ajoute le code d'accès à une ligne extérieure, la messagerie unifiée peut utiliser ce dernier pour accéder à une ligne extérieure avant de composer la chaîne du numéro de téléphone externe. Le code de numérotation que vous configurez s'applique à tous les utilisateurs associés à une stratégie de boîte aux lettres de messagerie unifiée, elle-même liée au plan de numérotation de messagerie unifiée.

## Préfixe du numéro national

Il est également possible de configurer le préfixe du numéro national et le code du pays/de la région pour un plan de numérotation de messagerie unifiée. La messagerie unifiée utilise le numéro entré pour composer le préfixe de numéro national correct ou le code de pays/région quand un utilisateur effectue un appel sortant vers un numéro du même pays ou de la même région ou un numéro international. Par exemple, si un utilisateur d'Amérique du Nord effectue un appel international sortant vers l'Europe, la messagerie unifiée ajoute le préfixe du numéro national avant la chaîne de numéro qu'il envoie au PBX pour passer l'appel sortant. Le numéro 1 est utilisé comme préfixe national pour l'Amérique du Nord.

## Code d’accès national/régional

Il est possible de configurer un code d'accès de pays/région sur un plan de numérotation de messagerie unifiée. Le code d'accès de pays/région se compose des chiffres associés à un pays ou une région spécifique. La messagerie unifiée utilise le code d'accès de pays/région pour composer le numéro de téléphone approprié quand un appel est passé vers un numéro de téléphone situé dans le même pays ou la même région. La messagerie unifiée ajoute ce numéro avant la chaîne du numéro qu'il envoie au PBX ou au PBX IP dans le cas d'un appel sortant. Par exemple, la messagerie unifiée ajoute le numéro 1 à la chaîne du numéro pour un appel passé aux États-Unis à destination d'un numéro aux États-Unis. Pour le Royaume-Uni, le code de pays/région est le 44.

## Code d'accès à l'international

Il est possible de configurer un code d'accès à l'international sur un plan de numérotation de messagerie unifiée. Le code d'accès à l'international contient des chiffres utilisés pour accéder à des numéros de téléphone internationaux. La messagerie unifiée utilise le code d'accès à l'international pour composer le code d'accès à l'international correct quand un appel est effectué à partir d'un téléphone dont le numéro se situe dans le pays ou la région, mais quand le numéro appelé se situe dans un autre pays ou une autre région. La messagerie unifiée ajoute ce numéro avant la chaîne du numéro qu'il envoie au PBX ou au PBX IP dans le cas d'un appel sortant. Par exemple, la messagerie unifiée utilise le code d'accès 011 comme code d'accès à l'international pour appeler les États-Unis. Pour l'Europe, le code d'accès à l'international est le 00.

Vue d'ensemble

## Formats de numéro national/régional et international

Vous pouvez définir la configuration des appels entrants pour les formats de numéros nationaux, régionaux et internationaux sur un plan de numérotation de messagerie unifiée. Après avoir configuré ces paramètres, la messagerie unifiée est capable de reconnaître des appels entrants en provenance de numéros nationaux, régionaux et internationaux d'autres plans de numérotation de messagerie unifiée appartenant à la même organisation. Vous pouvez également ajouter des formats de numéros pour des appels entrants qui sont passés dans un plan de numérotation unique. La configuration de ces options permet également à votre organisation d'économiser de l'argent en bloquant les appels sortants qui ne doivent pas être effectués par des utilisateurs au sein de l'organisation et contribue à empêcher toute fraude. La messagerie unifiée utilise les informations que vous configurez pour examiner le format de numéro de l'appel entrant et vérifier que le modèle de numéro correspond avant d'accepter l'appel. Par exemple, une organisation peut disposer de plusieurs plans de numérotation. Si vous avez un plan de numérotation pour les États-Unis et un autre pour le Royaume-Uni, vous pouvez permettre aux utilisateurs du plan de numérotation pour les États-Unis d'utiliser la messagerie unifiée pour passer des appels vers des utilisateurs situés dans le plan de numérotation au Royaume-Uni, mais ne pas autoriser les utilisateurs du plan de numérotation pour les États-Unis à passer directement des appels nationaux, régionaux ou internationaux.

