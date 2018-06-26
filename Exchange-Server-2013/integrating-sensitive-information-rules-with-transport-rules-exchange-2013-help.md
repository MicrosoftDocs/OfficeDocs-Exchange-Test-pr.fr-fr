---
title: "Intégration des règles d'informations sensibles aux règles de transport: Exchange 2013 Help"
TOCTitle: Intégration des règles d'informations sensibles aux règles de transport
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50477400
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intégration des règles d'informations sensibles aux règles de transport

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-01-14_

Dans Microsoft Exchange, vous pouvez créer des stratégies DLP qui contiennent des règles non seulement pour les classifications de messages traditionnelles et les règles de transport existantes, mais vous pouvez également les combiner avec des règles pour les informations sensibles figurant dans des messages. Le cadre des règles de transport existantes offre de nombreuses possibilités de définition des stratégies de messagerie couvrant l'ensemble des contrôles logiciels et matériels. Exemples :

  - limitation de l'interaction entre les destinataires et les expéditeurs, y compris les interactions entre les services d'une organisation ;

  - application de stratégies distinctes pour les communications à l'intérieur et à l'extérieur d'une organisation ;

  - blocage du contenu inapproprié entrant ou sortant d'une organisation ;

  - filtrage d'informations confidentielles ;

  - suivi ou archivage des messages échangés avec des individus particuliers ;

  - redirection des messages entrants et sortants pour inspection avant remise ;

  - application de clauses d'exclusion de responsabilité à des messages transitant par l'organisation.

Les règles de transport permettent d'appliquer des stratégies de messagerie aux messages électroniques qui circulent dans le pipeline du service de transport sur des serveurs de boîtes aux lettres et de transport Edge. Ces règles permettent aux administrateurs système d'appliquer des stratégies de messagerie, de renforcer la sécurité des messages, de protéger les systèmes de messagerie et d'éviter la perte accidentelle d'informations. Pour plus d'informations sur les règles de transport, consultez la rubrique [Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) ( Exchange Server 2013) ou [Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\)) (Exchange Online).

## Règles pour les informations sensibles dans le cadre des règles de transport

Les règles pour les informations sensibles sont intégrées au cadre des règles de transport par l'introduction d'une condition que vous personnalisez : **Si le message contient...Informations sensibles**. Vous pouvez configurer cette condition avec un ou plusieurs types d'informations sensibles contenues dans les messages. Lorsque plusieurs stratégies DLP ou règles dans une stratégie sont configurées avec cette condition, cette stratégie ou cette règle est satisfaite lorsqu'une des conditions est remplie. Les règles de stratégie Exchange examinent l'objet et le corps d'un message, ainsi que les pièces jointes. Si la règle s'applique à un de ces composants de message, les actions de cette règle s'appliquent.

Il est possible de combiner la condition sur les informations sensibles avec n'importe laquelle des règles de transport existantes pour définir des stratégies de messagerie. Dans ce cas, la condition s'applique avec les autres règles et la règle logique AND. Par exemple, deux conditions différentes sont ajoutées avec une instruction AND de manière à ce que ces deux conditions doivent être remplies pour appliquer l'action. N'importe quelle action de règle de transport peut être configurée comme résultat des règles contenant une correspondance avec un type d'information sensible. L'agent des règles de transport, qui analyse les messages pour appliquer ces règles, peut analyser de nombreux types de fichiers différents. Pour en savoir plus sur les types de fichiers pris en charge, consultez la rubrique [Utiliser des règles de transport pour analyser les pièces jointes des messages](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013) ou [Utiliser des règles de flux de messagerie pour analyser les pièces jointes des messages](https://technet.microsoft.com/fr-fr/library/jj919236\(v=exchg.150\)) (Exchange Online).

Les règles sont également utilisables dans la partie exception de la définition d'une règle. Leur utilisation dans la définition d'une exception est indépendante de leur utilisation en tant que condition dans la règle. Cela vous offre la souplesse de définir des règles qui comportent la condition spécifiant plusieurs types d'informations à appliquer en tant que partie de la condition et également différents types d'informations dans la condition. Cela permet d'appliquer des stratégies telles que la correspondance avec des règles particulières traditionnelles de classification des messages, mais sans correspondance avec d'autres types d'informations sensibles avant d'appliquer les actions que vous définissez dans une stratégie.

## Pour plus d'informations

[Protection contre la perte de données](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Éléments recherchés par les types d’informations sensibles dans Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Règles de transport ou de flux de messagerie](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Règles de flux de messagerie (règles de transport) dans Exchange Online](https://technet.microsoft.com/fr-fr/library/jj919238\(v=exchg.150\))Exchange Online

[Création d'une stratégie personnalisée de protection contre la perte de données (DLP)](create-a-custom-dlp-policy-exchange-2013-help.md)

