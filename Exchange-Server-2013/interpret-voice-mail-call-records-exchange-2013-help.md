---
title: 'Interpréter les enregist. d’appel de messagerie vocale: Exchange 2013 Help'
TOCTitle: Interpréter les enregistrements d'appel de messagerie vocale
ms:assetid: 368d9c58-61a2-43d5-8189-d3469a9e2a8d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659061(v=EXCHG.150)
ms:contentKeyID: 50555379
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interpréter les enregistrements d'appel de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

Pour consulter des informations détaillées à propos des appels gérés par les serveurs Exchange un jour donné, exportez les données d'appel de ce jour du rapport de statistiques des appels. Les données d'appel quotidiennes, disponibles pour les 90 derniers jours, vous permettent de diagnostiquer les problèmes liés à la qualité audio ou aux appels rejetés et fournissent des informations concernant les audits et les rapports sur les serveurs Exchange de votre organisation.

Pour d'autres tâches relatives aux rapports de messagerie unifiée, consultez la rubrique [Procédures de rapports de messagerie unifiée](um-reports-procedures-exchange-2013-help.md).

## Utiliser le Centre d'administration Exchange (CAE) pour exporter des enregistrements d'appels de messagerie unifiée quotidiens

1.  Dans le CAE, accédez à **Messagerie unifiée** \> **Autres options** ![Icône Options supplémentaires](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icône Options supplémentaires") \> **Statistiques d'appels**.

2.  Sous **Afficher**, cliquez sur **Quotidiennement (90 jours)**, puis choisissez le plan de numérotation de messagerie unifiée, la passerelle IP de messagerie unifiée ou les deux. Le rapport est automatiquement mis à jour à mesure que vous choisissez les options.

3.  Sélectionnez le jour pour lequel vous souhaitez exporter les enregistrements d'appels et cliquez sur **Jour d'exportation**.

4.  Dans la zone de confirmation **Téléchargement de fichier**, cliquez sur **Ouvrir** ou **Enregistrer**.
    
    Le fichier exporté s'appellera um_cdr_*AAAA-MM-JJ*.csv, où *AAAA-MM-JJ* représente l'année, le mois et le jour d'exécution du rapport.
    
    > [!NOTE]
    > dans la page du rapport, vous pouvez télécharger un modèle Microsoft Excel que vous pouvez utiliser pour importer le fichier .csv d'un jour spécifique.


5.  Utilisez une application telle qu'Excel pour traiter le fichier .csv et générer vos propres rapports personnalisés.

## Interprétation des données d'appel de messagerie unifiée

Les données d'appel de messagerie unifiée que vous exportez incluent les informations détaillées suivantes à propos de chaque appel géré par la messagerie unifiée durant ce jour spécifique.

> [!NOTE]
> Dans le rapport de statistiques des appels, les jours sont entendus en heure UTC.


  - **CallStartTime   **Date et heure auxquelles la messagerie unifiée a géré l'appel, à l'heure UTC. La date et l'heure UTC sont représentées au format suivant : *AAAA-MM-JJ hh:mm:SSZ*, où *AAAA* = année, *MM* = mois, *JJ* = jour, *hh* = heure, au format 24 heures, *mm* = minutes, ss = secondes. Z signifie Zoulou, qui est une façon de dénoter UTC (comme +*hh*:*mm* ou -*hh*:*mm*, qui permet d'obtenir le décalage horaire par rapport à l'heure UTC). Étant donné que tous les appels de ce rapport sont à l'heure UTC, il s'agira toujours de Z.
    
    Par exemple, pour un appel passé le 23.06.13 à 14:23, l'heure de début d'appel est indiquée de la façon suivante :23/06/2013 14:23:11Z.

  - **Type d'appel   **Le type d'appel :
    
      - **Message vocal du répondeur automatique**   L'appel n'a pas obtenu de réponse et a été transféré aux serveurs Exchange, et l'appelant a laissé un message vocal.
    
      - **Appel manqué du répondeur automatique**   L'appel n'a pas obtenu de réponse et a été transféré aux serveurs de messagerie unifiée, et l'appelant n'a pas laissé de message vocal.
    
      - **Accès abonné**   Un appel a été effectué vers le numéro d'accès d'abonné. L'appelant s'est connecté et a été authentifié dans la messagerie unifiée avec son poste et son mot de passe pour accéder aux messages électroniques, aux calendriers et aux messages vocaux sur son téléphone.
    
      - **Standard automatique**   L’appel a abouti sur un standard automatique de messagerie unifiée. Ces appels sont en général des appels pour lesquels l'appelant a composé le numéro de téléphone principal de votre organisation.
    
      - **Télécopie**   Appel durant lequel une tonalité de télécopie a été détectée. Si vous avez configuré des partenaires de télécopie, cet appel a été transféré vers le partenaire de télécopie.
    
      - **PlayOnPhone**   Appel passé par la messagerie unifiée parce que l'utilisateur a cliqué sur le bouton Émettre au téléphone dans Microsoft Outlook Web App ou Outlook.
    
      - **Me contacter**   Appel sortant passé par la messagerie unifiée résultant d'une règle Me contacter dans une règle de répondeur automatique.
    
      - **Numéro pilote non authentifié**   Appel effectué vers le numéro Outlook Voice Access. L'appelant ne s'est pas connecté et n'a pas été authentifié.
    
      - **Enregistrement des messages d'accueil**   Appel passé par la messagerie unifiée pour enregistrer des messages d'accueil personnels pour un utilisateur.
    
      - **Aucun**   Appel passé mais dont le type n'a pas été défini.

  - **CallIdentity** Identité des appels SIP, telle que fournie par la passerelle IP de la messagerie unifiée.

  - **ParentCallIdentity** Identité SIP de la session dont provient cet appel. Cette zone est utilisée lors de l'utilisation de la fonctionnalité Me contacter des règles de répondeur automatique ou des appels de transfert d'appels, notamment des transferts d'appels entre les standards automatiques de messagerie unifiée.

  - **UMServerName** Nom du serveur de boîtes aux lettres qui gère l'appel, le cas échéant. Ces informations sont fournies uniquement quand vous disposez d'un serveur de boîtes aux lettres local.

  - **DialPlanName** Plan de numérotation de messagerie unifiée qui a géré l'appel.

  - **Durée de l'appel** Durée totale de l'appel.

  - **IPGatewayAddress** Nom de domaine complet de la passerelle IP ayant traité l'appel.

  - **CalledPhoneNumber** Numéro de téléphone ou adresse SIP du destinataire visé par l'appel (pour les utilisateurs de plans de numérotation SIP, tels que Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server).

  - **CallerPhoneNumber** Numéro de téléphone ou adresse SIP de l'appelant.

  - **OfferResult**   État de l'appel :
    
      - **Réponse**   La messagerie unifiée a répondu à l'appel ou a passé un appel. L'appel n'a pas été transféré ni redirigé. Ces appels incluent les appels passés à Outlook Voice Access, Émettre au téléphone ou aux standards automatiques de messagerie unifiée, ainsi que les appels gérés par la messagerie unifiée quand l'extension appelée n'a pas répondu au téléphone.
    
      - **Échec**   La messagerie unifiée a accepté ou a passé un appel, mais ce dernier a échoué. Ces appels incluent les appels pour lesquels le numéro ou l'adresse appelés sont occupés, ne répondent pas ou n'existent pas, pour lesquels l'appelant a raccroché avant que l'appel ait pu être connecté, pour lesquels les paramètres du plan de numérotation de messagerie unifiée ou de la stratégie de boîte aux lettres de messagerie unifiée ont empêché l'appel, ou pour lesquels la passerelle VoIP ou le PBX IP de votre système téléphonique n'ont pas pu être joints.
    
      - **Refusé**   La messagerie unifiée a rejeté l'appel, généralement en raison d'une erreur de configuration. Ces appels incluent les appels pour lesquels la passerelle IP de messagerie unifiée n'est pas associée à un plan de numérotation de messagerie unifiée ou pour lesquels il existe des problèmes d'incompatibilité.
    
      - **Redirigé**   La messagerie unifiée a accepté l'appel, mais l'a redirigé vers un autre serveur de boîtes aux lettres. Ces appels incluent ceux pour lesquels l'appelant a utilisé le menu Messagerie unifiée pour appeler un contact de l'annuaire ou des contacts personnels, ou pour lesquels l'appelant a contacté un numéro Outlook Voice Access à l'aide d'un numéro de téléphone qui n'est pas associé à la boîte aux lettres de l'utilisateur. Dans ces cas, la messagerie unifiée transfère l'appel vers le serveur Exchange associé à ce compte d'utilisateur.
    
      - **Aucun**   L'état de l'appel est inconnu.

  - **DropCallReason** Raison pour laquelle l'appel a été déconnecté, si la messagerie unifiée était en mesure d'en déterminer la raison. Par exemple, si l'appelant a raccroché, la colonne affiche Raccrochage.

  - **ReasonForCall** Mode de connexion de l'appel :
    
      - **Direct**   L'appelant a directement composé le numéro appelé.
    
      - **DivertForward**   L'appelant a composé un numéro et la personne appelée a redirigé l'appel vers la messagerie vocale de la messagerie unifiée.
    
      - **DivertBusy**  L'appelant a composé un numéro et la ligne était occupée. L'appel a donc été redirigé vers la messagerie vocale de la messagerie unifiée.
    
      - **DivertNoAnswer   **L'appelant a composé un numéro et la personne n'a pas répondu, donc l'appel a été redirigé vers la messagerie vocale de la messagerie unifiée.
    
      - **Sortant**   L'appel a été passé par la messagerie unifiée, par exemple, pour lire un message vocal à l'aide de la fonctionnalité Émettre au téléphone.
    
      - **Aucun**   Aucune raison n'a été signalée pour cet appel.

  - **DialedString** Adresse ou numéro de téléphone de la personne à qui cet appel a été transféré ou référencé. Cette valeur fait également référence à l'adresse ou au numéro de téléphone appelés par les appels Émettre au téléphone.

  - **CallerMailboxAlias** Alias de la boîte aux lettres (c'est-à-dire la partie de l'adresse de messagerie qui précède le symbole @) de l'appelant. Cette valeur est disponible uniquement si l'appelant s'est connecté à Outlook Voice Access.

  - **CalleeMailboxAlias** Alias de la boîte aux lettres du destinataire visé par l'appel, si le destinataire désigné est un utilisateur à extension messagerie unifiée.

  - **Nom du standard automatique** Nom du standard automatique associé à cet appel.

  - **Score NMOS**   Note moyenne d'opinion de réseau (NMOS) de cet appel. Le score NMOS évalue la qualité audio de l'appel, sur une échelle de 1 à 5, 5 indiquant une excellente qualité.
    
    > [!NOTE]
    > <strong>Remarque</strong>   Le score NMOS maximal possible pour un appel dépend du codec audio utilisé. Il est possible que le score NMOS ne soit pas disponible pour des appels très courts d'une durée inférieure à 10 secondes.


  - **NMOSDegradation** Niveau de dégradation audio du score NMOS, à partir de la valeur la plus élevée possible pour le codec audio utilisé. Par exemple, si la valeur de dégradation NMOS d'un appel est égale à 1,2 et que le score NMOS signalé de l'appel est égal à 3,3, le score NMOS maximal de cet appel en particulier est de 4,5 (1,2 + 3,3).

  - **NMOSDegradation Jitter** Valeur de dégradation NMOS totale due à l'instabilité.

  - **NMOSDegradation PacketLoss** Valeur de dégradation NMOS totale due à la perte de paquets.

  - **Instabilité** Variation moyenne de l'arrivée des paquets de données pour un appel.

  - **PacketLoss** Pourcentage moyen de la perte de paquets de données pour l'appel sélectionné. La perte de paquets est une indication de la fiabilité de la connexion.

  - **Aller-retour** Durée moyenne de l'aller-retour, en millisecondes, de l'audio pour l'appel sélectionné. Le score d'aller-retour mesure la latence de la connexion.

  - **BurstDensity** Pourcentage de paquets perdus et ignorés pendant une période de rafale (taux de perte élevé).

  - **Durée d'écart de rafale** Durée moyenne de perte de paquets pendant les rafales de pertes pour l'appel sélectionné.

  - **Codec audio** Codec audio utilisé pendant un appel.

