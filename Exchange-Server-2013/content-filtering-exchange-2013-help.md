---
title: 'Filtrage du contenu: Exchange 2013 Help'
TOCTitle: Filtrage du contenu
ms:assetid: d660ffbf-de05-46c2-940b-5200eca94e0a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124739(v=EXCHG.150)
ms:contentKeyID: 50479276
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrage du contenu

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

> [!NOTE]
> Le 1er novembre 2016, Microsoft a cessé de produire des mises à jour des définitions de courrier indésirable pour les filtres SmartScreen dans Exchange et Outlook. Les définitions de courrier indésirable SmartScreen existantes restent en place, mais leur efficacité se dégradera probablement au cours du temps. Pour plus d’informations, voir l’article relatif à l’<a href="https://go.microsoft.com/fwlink/p/?linkid=835894">arrêt de la prise en charge de SmartScreen dans Outlook et Exchange</a>.


L’agent de filtrage de contenu évalue les messages électroniques entrants et évalue la probabilité qu’un message entrant est légitime ou du spam. Contrairement à nombreuses autres technologies de filtrage, l’agent de filtrage de contenu utilise les caractéristiques d’un échantillon statistiquement significatif de messages électroniques. L’inclusion de messages valables dans cet échantillon réduit le risque d’erreurs. Étant donné que l’agent de filtrage de contenu reconnaît les caractéristiques des messages légitimes, spam, sa précision est augmentée. Mises à jour de l’agent de filtrage de contenu sont disponibles régulièrement par le biais de [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836).

**Contenu de cette rubrique**

Using the Content Filter agent

Configuring the Content Filter agent

## Utilisation de l’agent de filtrage du contenu

L’agent de filtrage du contenu est l’un des nombreux agents de blocage du courrier indésirable disponibles dans Exchange. Lorsque vous configurez des agents de blocage du courrier indésirable sur un serveur Exchange, les agents agissent de façon cumulative sur les messages pour réduire la quantité de messages non sollicités entrant dans l’organisation. Pour plus d'informations sur la planification et le déploiement des agents de blocage du courrier indésirable, consultez la rubrique [Protection contre le courrier indésirable](anti-spam-protection-exchange-2013-help.md).

L'agent de filtrage du contenu affecte une valeur de contrôle d'accès SCL à chaque message. La valeur de contrôle d'accès SCL est un nombre compris entre 0 et 9. Une valeur de contrôle d'accès SCL supérieure indique qu'un message est susceptible d'être un courrier indésirable.

Vous pouvez configurer l'agent de filtrage du contenu pour qu'il exécute les actions suivantes sur les messages en fonction de leur valeur SCL :

  - Supprimer le message

  - Rejeter le message

  - Mettre le message en quarantaine

Par exemple, vous pouvez déterminer que les messages dont la valeur de contrôle d'accès SCL est supérieure ou égale à 7 doivent être supprimés, tandis que les messages dont la valeur de contrôle d'accès SCL est 6 doivent être rejetés et ceux dont la valeur de contrôle d'accès SCL est 5 doivent être mis en quarantaine.

Vous pouvez ajuster le comportement de seuil de probabilité de courrier indésirable en attribuant différentes valeurs de contrôle d'accès SCL à chacune de ces actions. Pour plus d'informations sur l'ajustement du seuil de probabilité de courrier indésirable en fonction des besoins de votre organisation et la définition de seuils SCL pour chaque destinataire, consultez la rubrique [Niveau de confiance du courrier indésirable](spam-confidence-level-threshold-exchange-2013-help.md).

> [!NOTE]
> Les messages dont la taille excède 11 Mo ne sont pas analysés par le filtre de messages intelligent. Le filtre du contenu laisse passer les messages sans les analyser.


## Phrases d’autorisation et d’interdiction

Vous pouvez personnaliser la manière dont l'agent de filtrage du contenu affecte les valeurs SCL en configurant des mots personnalisés. Les mots personnalisés sont des mots ou des phrases individuels que l'agent de filtrage du contenu utilise pour appliquer le traitement de filtrage approprié. Vous pouvez configurer les mots ou phrases approuvés à l'aide de phrases d'autorisation et les mots ou phrases rejetés à l'aide de phrases d'interdiction. Lorsque l'agent de filtrage du contenu détecte une phrase d'autorisation préconfigurée dans un message entrant, il affecte la valeur SCL 0 au message. Autrement, si l'agent de filtrage du contenu détecte une phrase d'interdiction configurée dans un message entrant, il affecte la valeur SCL 9 au message.

Vous pouvez entrer des mots ou des phrases personnalisés dans une combinaison quelconque de lettres majuscules et minuscules. Toutefois, lorsque l'agent de filtrage du contenu évalue le contenu d'un message, il ignore la casse. Le nombre maximal de mots et de phrases personnalisés qu'il est possible de créer est de 800.

## Validation du cachet de courrier électronique Outlook

L’agent de filtrage du contenu inclut également la validation du cachet de courrier électronique Microsoft Office Outlook, fonction de preuve de calcul qu’Outlook applique aux messages sortants pour aider les systèmes de messagerie des destinataires à distinguer les messages légitimes de ceux qui ne le sont pas. Celle-ci permet de réduire la probabilité de faux positifs. Dans le contexte de filtrage du courrier indésirable, un *faux positif* existe quand un filtre de courrier indésirable identifie incorrectement un message provenant d'un expéditeur légitime comme du courrier indésirable. Lorsque la validation du cachet de courrier électronique Outlook est activée, l’agent de filtrage du contenu analyse le message entrant afin de voir s’il contient un en-tête de cachet de calcul. La présence d'un en-tête de cachet de calcul valide et résolu dans le message indique que l'ordinateur client qui a généré le message a résolu le cachet de calcul.

Le temps de traitement requis par les ordinateurs n'est pas important pour la résolution des cachets de calcul individuels. Toutefois, le traitement des cachets pour de nombreux messages peut être prohibitif pour un expéditeur malveillant. Une personne qui envoie des millions de message indésirables est peu susceptible d'investir dans le pouvoir de traitement requis afin de résoudre les cachets de calcul pour tous les courriers indésirables sortants. Si un message électronique d’un expéditeur contient un cachet de calcul valide et résolu, il est peu probable que l’expéditeur soit malveillant. Dans ce cas, l'agent de filtrage du contenu abaisse la valeur SCL. Si la fonction de validation du cachet est activée et qu'un message entrant ne contient pas d'en-tête de cachet de calcul ou contient un en-tête de cachet de calcul non valide, l'agent de filtrage du contenu ne modifie pas la valeur de seuil de probabilité de courrier indésirable.

## Ignorance du destinataire, de l’expéditeur et du domaine de l’expéditeur

Dans certaines organisations, tous les messages électroniques adressés à certains alias doivent être acceptés. Ce scénario peut occasionner des problèmes si votre organisation opère dans un secteur qui gère des volumes importants de courrier indésirable.

Par exemple, une société appelée Woodgrove Bank possède un alias customerloans@woodgrovebank.com qui fournit un support basé sur des messages électroniques aux clients externes. Les administrateurs Exchange configurent l’agent de filtrage du contenu afin de définir des phrases d’interdiction qui filtrent les mots ou les phrases qui sont généralement utilisés dans les courriers indésirables envoyés par des agences de prêt sans scrupules. Pour empêcher le rejet des messages légitimes, les administrateurs définissent des exceptions de filtrage du contenu en entrant une liste de destinataires de messages électroniques SMTP dans la configuration de l’agent de filtrage du contenu.

Vous pouvez également spécifier des expéditeurs et des domaines d'expéditeur que l'agent de filtrage du contenu ne doit pas bloquer.

## Agrégation de listes fiables

Dans Exchange 2013, l’agent de filtrage du contenu utilise les listes des expéditeurs approuvés Outlook, la liste des expéditeurs bloqués et les listes des destinataires approuvés Outlook, ainsi que les contacts approuvés Outlook pour optimiser le filtrage du courrier indésirable. L’*agrégation de listes fiables* est un ensemble de fonctionnalités de blocage du courrier indésirable partagé par Outlook et Exchange. Comme son nom l’indique, cette fonctionnalité collecte des données des listes fiables de blocage du courrier indésirable que les utilisateurs Outlook configurent et met ces données à la disposition des agents de blocage du courrier indésirable sur le serveur Exchange. Les messages électroniques que les utilisateurs Outlook reçoivent de contacts que ces utilisateurs ont ajoutés à leur liste des destinataires ou expéditeurs approuvés Outlook ou à leur liste de contacts approuvés sont identifiés par l’agent de filtrage du contenu comme fiables. L'agent de filtrage des expéditeurs effectue également un filtrage des expéditeurs par destinataire à l'aide de la liste des expéditeurs bloqués que les utilisateurs configurent. Pour plus d’informations, consultez la rubrique [Agrégation de listes fiables](safelist-aggregation-exchange-2013-help.md).

## Configuration de l’agent de filtrage du contenu

Vous configurez l’agent de filtrage du contenu à l’aide de l’environnement de ligne de commande Exchange Management Shell.

> [!NOTE]
> Les modifications de la configuration que vous apportez à l’agent de filtrage du contenu dans l’environnement de ligne de commande Exchange Management Shell ne sont effectuées que sur l’ordinateur local. Si l’agent de filtrage du contenu est exécuté sur plusieurs serveurs Exchange de votre organisation, vous devez apporter les modifications de la configuration du filtrage de contenu sur chaque ordinateur.


L’agent de filtrage du contenu dépend des mises à jour pour déterminer si un message n’est pas indésirable et peut être remis en toute confiance. Ces mises à jour contiennent des données sur l’hameçonnage de sites Web, l’heuristique de blocage du courrier indésirable Microsoft SmartScreen et d’autres mises à jour du filtre de messages intelligent. Les mises à jour du filtrage du contenu comprennent environ 6 Mo de données utiles pour des périodes plus longues que les autres données de mise à jour du blocage du courrier indésirable.

Les mises à jour du filtrage du contenu sont disponibles sur la page [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836). Les données de mise à jour du filtrage du contenu sont actualisées et mises à disposition pour téléchargement toutes les deux semaines.

Pour plus d'informations sur la configuration du filtrage du contenu, voir [Gérer le filtrage du contenu](manage-content-filtering-exchange-2013-help.md).

