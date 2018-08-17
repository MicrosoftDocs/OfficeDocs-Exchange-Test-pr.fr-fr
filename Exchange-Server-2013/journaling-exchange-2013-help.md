---
title: 'Journalisation: Exchange 2013 Help'
TOCTitle: Journalisation
ms:assetid: 6a20f207-4485-44ef-b010-ec760eb5165b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998649(v=EXCHG.150)
ms:contentKeyID: 50478360
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Journalisation

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

La journalisation peut aider votre organisation à répondre aux exigences réglementaires, légales et de conformité organisationnelle en enregistrant les communications électroniques échangées. Lors de la planification de la rétention et de la conformité de la messagerie, il est important de comprendre la journalisation, son intégration dans les stratégies de conformité de votre organisation et la sécurisation des messages journalisés à l'aide de Microsoft Exchange Server 2013.

**Contenu de cette rubrique**

Why journaling is important

Journaling agent

Journal rules

Journal rule replication

Journal reports

Interoperability with Exchange 2010 and Exchange 2007

Troubleshooting

## Pourquoi la journalisation est-elle importante ?

Tout d’abord, il est important de comprendre la différence entre journalisation et stratégie d’archivage des données :

  - La *journalisation* est la capacité d’enregistrer toutes les communications, y compris les communications électroniques, au sein d’une organisation afin de les utiliser en relation avec la stratégie de rétention ou d’archivage du courrier électronique de l’organisation. Pour répondre à un nombre croissant d’exigences de conformité réglementaire, de nombreuses organisations doivent conserver les enregistrements des communications échangées au cours des tâches de travail quotidiennes des employés.

  - L’*archivage des données* fait référence à la sauvegarde des données, en les supprimant de leur environnement natif et en les stockant ailleurs, ce qui permet de réduire la contrainte de stockage de données. Vous pouvez utiliser la journalisation Exchange comme outil dans le cadre de votre stratégie de rétention ou d'archivage du courrier électronique.

Bien que la journalisation puisse ne pas être exigée par une réglementation spécification, la conformité peut être obtenue par le biais de la journalisation dans le cadre de certaines réglementations. Par exemple, les responsables d’entreprise dans certains secteurs financiers peuvent être tenus responsables des déclarations de leurs employés auprès de leurs clients. Pour vérifier l’exactitude des déclarations, un responsable peut configurer un système où les directeurs examinent régulièrement une partie des communications entre les employés et les clients. Chaque trimestre, les directeurs vérifient la conformité et approuvent la conduite de leurs employés. Après que tous les directeurs ont notifié leur approbation au responsable, celui-ci notifie la conformité, au nom de la société, à l’organe régulateur. Dans cet exemple, les messages électroniques peuvent être l’un des types de communication entre employés et clients que les directeurs doivent examiner ; la journalisation permet donc de collecter tous les messages électroniques envoyés par des employés en relation avec les clients. D’autres méthodes de communication avec les clients, telles que les télécopies et les conversations téléphoniques, peuvent aussi être soumises à réglementation. La capacité de journalisation de toutes les classes de données dans une entreprise est une fonctionnalité précieuse de l’architecture informatique.

La liste suivante répertorie quelques-unes des réglementations américaines et internationales les plus connues où la journalisation peut vous aider à constituer la plupart de vos stratégies :

  - Loi Sarbanes-Oxley de 2002 (SOX)

  - Règle 17a-4 de la SEC (Securities Exchange Commission)

  - National Association of Securities Dealers 3010 & 3110 (NASD 3010 & 3110)

  - Loi Gramm-Leach-Bliley (loi de modernisation financière)

  - Financial Institution Privacy Protection Act de 2001

  - Financial Institution Privacy Protection Act de 2003

  - Healthcare Insurance Portability and Accountability Act de 1996 (HIPAA)

  - Uniting and Strengthening America by Providing Appropriate Tools Required to Intercept and Obstruct Terrorism Act de 2001 (Patriot Act)

  - Directive relative à la protection des données de l’Union européenne (EUDPD)

  - Loi japonaise sur la protection des informations personnelles

Retour au début

## Agent de journalisation

Dans une organisation Exchange 2013, tout le trafic de messagerie est acheminé par des serveurs de boîtes aux lettres. Pendant leur durée de vie, tous les messages parcourent au moins un serveur exécutant le service de transport. L'*agent de journalisation* est un agent de transport axé sur la conformité qui traite les messages sur les serveurs de boîtes aux lettres. Il se déclenche à partir des événements de transport **OnSubmittedMessage** et **OnRoutedMessage**.

> [!NOTE]  
> Dans Exchange 2013, l'agent de journalisation est un agent intégré. Les agents intégrés ne figurent pas dans la liste des agents renvoyés par la cmdlet <strong>Get-TransportAgent</strong>. Pour plus d'informations, consultez la rubrique <a href="transport-agents-exchange-2013-help.md">Agents de transport</a>.


Exchange 2013 fournit les options de journalisation suivantes :

  - La **journalisation standard** est configurée sur une base de données de boîtes aux lettres. Elle permet à l'agent de journalisation de journaliser tous les messages échangés depuis des boîtes aux lettres situées dans une base de données de boîtes aux lettres spécifique. Pour journaliser l'ensemble des messages des expéditeurs et des destinataires, vous devez configurer la journalisation sur toutes les bases de données de boîtes aux lettres de tous les serveurs de boîtes aux lettres au sein de l'organisation.

  - **Journalisation étendue**   La journalisation étendue permet à l'agent de journalisation de réaliser une journalisation plus détaillée en utilisant les règles de journal. Au lieu de journaliser toutes les boîtes aux lettres résidant dans une base de données de boîtes aux lettres, il est possible de configurer des règles de journal correspondant aux besoins de votre organisation en journalisant des destinataires individuels ou des membres de groupes de distribution. Pour utiliser la journalisation étendue, vous devez disposer d'une licence d'accès client entreprise Exchange.

Lorsque vous activez la journalisation standard sur une base de donnée de boîtes aux lettres, ces informations sont enregistrées dans Active Directory et lues par l'agent de journalisation. De même, les règles de journal configurées avec la journalisation étendue sont également enregistrées dans Active Directory et appliquées par l'agent de journalisation. Pour plus d'informations sur la configuration de la journalisation standard et de la journalisation premium, consultez la rubrique [Gérer la journalisation](manage-journaling-exchange-2013-help.md).

Retour au début

## Règles de journalisation

Voici les principaux aspects des règles de journal :

  - **Étendue d’une règle de journal**   Définit quels messages sont journalisés par l’agent de journalisation.

  - **Destinataire du journal**   Spécifie l’adresse SMTP du destinataire que vous souhaitez journaliser.

  - **Boîte aux lettres de journalisation**   Spécifie une ou plusieurs boîtes aux lettres servant à la collecte des états de journal.

## Étendue d'une règle de journal

Vous pouvez utiliser une règle de journal pour journaliser uniquement les messages internes, uniquement les messages externes ou les deux. La liste suivante décrit ces étendues :

  - **Messages internes uniquement**   Règles de journal dont l’étendue est définie sur les messages internes de journal envoyés entre des destinataires situés au sein de votre organisation Exchange.

  - **Messages externes uniquement**   Règles de journal dont l’étendue est définie sur les messages externes de journal envoyés à des destinataires ou reçus en provenance d’expéditeurs situés en dehors de votre organisation Exchange.

  - **Tous les messages**   Règles de journal dont l’étendue est définie sur tous les messages de journal qui transitent par votre organisation quelle que soit l’origine ou la destination. Ces entrées incluent les messages qui ont déjà été traités par des règles de journal de portées interne et externe.

## Destinataire du journal

Vous pouvez mettre en place des règles de journal ciblées en spécifiant l’adresse SMTP du destinataire que vous voulez journaliser. Le destinataire peut être une boîte aux lettres Exchange, un groupe de distribution, un utilisateur de messagerie ou un contact. Ces destinataires peuvent être soumis à des exigences réglementaires ou être impliqués dans des actions judiciaires dans le cadre desquels les messages électroniques ou d’autres communications sont collectés à des fins de preuve. En ciblant des destinataires ou des groupes de destinataires spécifiques, vous pouvez aisément configurer un environnement de journalisation conforme aux processus ainsi qu’aux exigences légales et réglementaires de votre organisation. En ciblant uniquement des destinataires spécifiques devant être journalisés, vous réduisez aussi les frais de stockage et les autres coûts associés à la conservation de grandes quantités de données.

Tous les messages échangés avec des destinataires de journalisation spécifiés dans une règle de journal sont journalisés. Si vous spécifiez un groupe de distribution comme destinataire de la journalisation, tous les messages échangés avec les membres du groupe de distribution sont journalisés. Si vous ne spécifiez pas de destinataire de journalisation, tous les messages échangés avec les destinataires correspondant à l’étendue de la règle de journal sont journalisés.

**Destinataires du journal à extension messagerie unifiée**

De nombreuses organisations qui mettent en œuvre la journalisation peuvent aussi utiliser la messagerie unifiée pour consolider leur infrastructure de courrier électronique, de messagerie vocale et de télécopie. Cependant, vous pouvez ne pas vouloir que le traitement de la journalisation génère des états de journal pour les messages générés par la messagerie unifiée. Dans ces cas, vous pouvez décider de journaliser les messages vocaux et les messages de notification d’appel en absence qui sont traités par un serveur Exchange exécutant le service de messagerie unifiée ou bien d’ignorer ces messages. Si votre organisation n'exige pas la journalisation de tels messages, vous pouvez réduire la quantité d'espace disque requise pour stocker les états de journal en ignorant ces messages.

> [!NOTE]
> Les messages contenant des télécopies qui sont générées par le service de messagerie unifiée sont toujours journalisés, même si vous désactivez la journalisation des messages vocaux de messagerie unifiée et les messages de notification d'appel en absence.


Pour plus d’informations sur l’activation ou la désactivation des messages vocaux et de notification d’appel en absence, consultez la rubrique [Désactiver ou activer la journalisation des notifications d’appel en absence et de la messagerie vocale](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md).

## Boîte aux lettres de journalisation

La boîte aux lettres de la journalisation sert à collecter les états de journal. La manière dont vous configurez la boîte aux lettres de journalisation dépend des stratégies de l'organisation, ainsi que des exigences légales et réglementaires. Vous pouvez spécifier une boîte aux lettres de journalisation que vous pouvez utiliser pour collecter les messages correspondant à toutes les règles de journal configurées dans l’organisation ou utiliser différentes boîtes aux lettres de journalisation pour différentes règles ou groupes de règles de journal.

> [!IMPORTANT]  
> Vous ne pouvez pas désigner une boîte aux lettres Office 365 comme boîte aux lettres de journalisation. Vous pouvez fournir des états du journal à un système d’archivage local ou à un service d’archivage tiers. Si vous exécutez un déploiement hybride avec vos boîtes aux lettres partagées entre les serveurs locaux et Office 365, vous pouvez désigner une boîte aux lettres locale comme boîte aux lettres de journalisation de vos boîtes aux lettres Office 365 et locales.


> [!IMPORTANT]  
> Les boîtes aux lettres de journalisation contiennent des informations très sensibles. Vous devez sécuriser les boîtes aux lettres de journalisation parce qu'elles collectent des messages échangés avec des destinataires au sein de votre organisation. Ces messages peuvent être visés par des actes de procédure ou faire l'objet d'exigences réglementaires. Diverses lois exigent que les messages soient conservés à l'abri de toute falsification avant leur présentation à une autorité de vérification. Il est souhaitable que votre organisation élabore des stratégies définissant qui peut accéder aux boîtes aux lettres de journalisation en son sein, en limitant cet accès aux personnes ayant un besoin direct d'y accéder. Consultez vos représentants légaux pour vous assurer que votre solution de journalisation est conforme à l'ensemble des lois et réglementations applicables à votre organisation.


> [!IMPORTANT]  
> Les boîtes aux lettres de journalisation doivent accepter les messages d’une taille égale ou supérieure à la taille maximale des messages définie dans votre organisation. Si vous avez configuré des exceptions pour les paramètres MaxSendSize et MaxReceiveSize sur la boîte aux lettres d’un utilisateur individuel qui sont supérieures au paramètre général dans TransportConfig, vous devez définir les paramètres MaxSendSize et MaxReceiveSize de la boîte aux lettres de journalisation en conséquence afin de garantir que les messages envoyés dans la boîte aux lettres de journalisation sont acceptés et pas mis en attente ou rejetés. Les messages rejetés par la boîte aux lettres de journalisation feront régulièrement l’objet de nouvelles tentatives, ce qui entraîne une augmentation inutile de la base de données et le gaspillage de ressources. En outre, il est recommandé d’installer une autre boîte aux lettres de journalisation afin d’éviter la non-remise des messages.


## Autre boîte aux lettres de journalisation

Si la boîte aux lettres de journalisation est indisponible, vous ne souhaiterez peut-être pas autoriser la collecte des états de journal rejetés dans les files d’attente des messages sur les serveurs de boîtes aux lettres. Dans ce cas, vous pouvez configurer une autre boîte aux lettres de journalisation afin de stocker ces états de journal. La boîte aux lettres de journalisation alternative reçoit les états de journal sous forme de pièces jointes dans les notifications d’échec de remise générées lorsque la boîte aux lettres de journalisation ou le serveur qui l’héberge refuse de remettre l’état de journal ou devient indisponible.

Une fois la boîte aux lettres de journalisation à nouveau disponible, vous pouvez utiliser la fonctionnalité **Envoyer à nouveau** de OfficeOutlook pour envoyer les états de journal pour remise à la boîte aux lettres de journalisation.

Lorsque vous configurez une autre boîte aux lettres de journalisation, tous les états de journal rejetés ou qui n’ont pas pu être remis dans toute votre organisation Exchange sont remis à l’autre boîte aux lettres de journalisation. Par conséquent, il est important de s'assurer que l'autre boîte aux lettres de journalisation et le serveur de boîtes aux lettres qui l'héberge peuvent prendre en charge plusieurs états de journal.

> [!CAUTION]
> Si vous configurez une boîte aux lettres de journalisation alternative, vous devez veiller à ce qu’elle ne soit pas indisponible en même temps que les boîtes aux lettres de journalisation. Si l'autre boîte aux lettres de journalisation devient indisponible ou rejette des états de journal, ceux-ci sont perdus et irrécupérables.


Dans la mesure où l’autre boîte aux lettres de journalisation collecte tous les états de journal rejetés pour toute l’organisation Exchange, vous devez vérifier que cela ne va pas à l’encontre des règles ou règlements applicables à votre organisation. Si des règles ou règlements empêchent votre organisation d'autoriser le stockage d'états de journal envoyés à différentes boîtes aux lettres de journalisation dans la même autre boîte aux lettres de journalisation, il se peut que vous ne puissiez pas configurer une autre boîte aux lettres de journalisation. Consultez vos représentants légaux afin de déterminer si vous pouvez utiliser une autre boîte aux lettres de journalisation.

Lorsque vous configurez une autre boîte aux lettres de journalisation, vous devez spécifier les mêmes critères que ceux utilisés lors de la configuration de la boîte aux lettres de journalisation.

> [!IMPORTANT]  
> L'autre boîte aux lettres de journalisation doit être traitée comme une boîte aux lettres dédiée spéciale. Les messages adressés directement à l'autre boîte aux lettres de journalisation ne sont pas journalisés.


Retour au début

## Réplication de règle de journal

Les règles de journal sont stockées dans Active Directory et appliquées par tous les serveurs de boîtes aux lettres dans l'organisation Exchange 2013. Quand vous créez, modifiez ou supprimez une règle de journal, la modification est répliquée sur tous les serveurs Active Directory de l'organisation. Tous les serveurs de boîtes aux lettres de l'organisation récupèrent alors la configuration de la règle de journal actualisée à partir des serveurs Active Directory et appliquent les règles de journal nouvelles ou modifiées.

En répliquant toutes les règles de journal dans l'ensemble de l'organisation, Exchange 2013 permet de déployer un ensemble cohérent de règles de journal au sein de l'organisation. Tous les messages qui transitent par votre organisation Exchange 2013 sont soumis aux mêmes règles de journal.

> [!IMPORTANT]  
> Réplication de règles de journal au sein d’une organisation dépend de la réplication Active Directory. Temps de réplication entre les contrôleurs de domaine Active Directory varie selon le nombre de sites dans l’organisation et de la vitesse des liaisons et d’autres facteurs en dehors du contrôle du Microsoft Exchange. Lorsque vous implémentez des règles de journal dans votre organisation, tenez compte des retards de réplication. Pour plus d’informations sur la réplication de Active Directory, consultez <a href="https://go.microsoft.com/fwlink/?linkid=274904">Introduction à la réplication Active Directory et de topologie de gestion à l’aide de Windows PowerShell</a>.


> [!IMPORTANT]  
> Chaque serveur de boîtes aux lettres met en cache l'appartenance au groupe de distribution pour éviter des allers-retours répétés vers Active Directory. La mise en cache des groupes développés réduit le nombre de requêtes que chaque serveur de boîtes aux lettres doit adresser à un contrôleur de domaine Active Directory. Par défaut, les entrées dans le cache de groupes développés expirent dans quatre heures. Par conséquent, si vous spécifiez un groupe de distribution comme destinataire du journal, les modifications apportées à l'appartenance au groupe de distribution peuvent ne pas être appliquées aux règles de journal jusqu'à la mise à jour du cache des groupes développés. Pour forcer une mise à jour immédiate du cache de destinataires, vous devez arrêter et démarrer le service de transport Microsoft Exchange. Vous devez procéder ainsi pour chaque serveur de boîtes aux lettres sur lequel vous souhaitez forcer la mise à jour du cache des destinataires.


Retour au début

## États de journal

Un *état de journal* est le message que génère l'agent de journalisation quand un message correspond à une règle de journal et doit être envoyé à la boîte aux lettres de journalisation. Le message d'origine correspondant à la règle de journal est inclus, sans modification, en pièce jointe à l'état de journal. Le corps d'un état de journal contient des informations figurant dans le message d'origine, telles que l'adresse de messagerie de l'expéditeur, l'objet, l'ID de message et les adresses de messagerie des destinataires. Ce processus est également appelé journalisation des enveloppes, et c'est la seule méthode de journalisation prise en charge par Exchange 2013.

## États de journal et messages protégés par IRM

Les états de journal et les messages protégés par IRM (gestion des droits relatifs à l'information) doivent être pris en compte lors de la mise en œuvre de la journalisation dans un environnement Exchange 2013. Les messages protégés par IRM auront une incidence sur les capacités de recherche et de détection de systèmes d'archivage tiers qui n'intègrent pas le service RMS. Dans Exchange 2013, vous pouvez configurer le déchiffrement des états de journal pour enregistrer une copie du message en texte clair dans un état de journal.

Retour au début

## Interopérabilité avec Exchange 2007

Il y a peu de différences entre la fonctionnalité de journalisation d’Exchange 2013, d’Exchange 2010 et d’Exchange 2007. Néanmoins, dans Exchange 2010 et versions ultérieures, le programme d’installation crée un conteneur séparé dans Active Directory pour stocker les règles de journal. Lorsque vous installez le premier serveur Exchange 2010 ou versions ultérieures dans une organisation Exchange 2007, le programme d’installation crée une copie des règles de journal existantes dans Exchange 2007 et les stocke dans le nouveau conteneur. Une fois l’installation terminée, les règles de journal des deux versions d’Exchange sont cohérentes.

Après l’installation, si vous modifiez la configuration des règles de journal sur les serveurs Exchange 2010 ou versions ultérieures, vous devrez apporter les mêmes modifications sur Exchange 2007 pour garantir leur cohérence. De même, les modifications apportées aux règles de journal sur Exchange 2007 doivent aussi être appliquées dans Exchange 2010 ou versions ultérieures. Vous pouvez également exporter les règles de journal à partir d’Exchange 2007 et les importer dans Exchange 2013.

Retour au début

## Résolution des problèmes

Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), et [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351). Si vous rencontrez des problèmes avec la boîte aux lettres **JournalingReportDNRTo**, consultez [Règles de transport et de boîtes aux lettres dans Exchange Online ne fonctionnent pas comme prévu](https://go.microsoft.com/fwlink/p/?linkid=331674).

