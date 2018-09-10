---
title: 'Gestion des droits relatifs à l’information: Exchange 2013 Help'
TOCTitle: Gestion des droits relatifs à l’information
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50478408
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des droits relatifs à l’information

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Tous les jours, les travailleurs de l’information utilisent les messageries électroniques pour échanger des informations sensibles. Par exemple : rapports et états financiers, contrats juridiques, informations confidentielles sur des produits, comptes rendus et prévisions de ventes, analyses de la concurrence, données d’études et de brevets et informations sur les clients et le personnel. Puisqu’il est maintenant possible d’accéder à sa messagerie électronique de n’importe quel endroit du monde, les boîtes aux lettres se sont transformées en référentiels contenant de gros volumes d’informations potentiellement sensibles. En conséquence, la fuite d’informations peut représenter une sérieuse menace pour les entreprises. Pour contribuer à la prévention des fuites d’informations, Microsoft Exchange Server 2013 inclut des fonctions de gestion des droits relatifs à l’information (IRM) qui offrent une protection persistante, en ligne et hors connexion, des messages électroniques et des pièces jointes.

**Contenu de cette rubrique**

Qu’est-ce que la fuite d’informations ?

Solutions traditionnelles de prévention des fuites d’informations

Gestion des droits relatifs à l’information (IRM) dans Exchange 2013

Application de la protection IRM aux messages

Scénarios pour la protection IRM

Déchiffrement des messages protégés par IRM pour imposer les stratégies de messagerie

Pré-licence

Agents IRM

Configuration requise pour la gestion des droits relatifs à l’information (IRM)

Configuration et test de la gestion des droits relatifs à l’information (IRM)

Étendre Rights Management avec le connecteur Rights Management

## Qu’est-ce que la fuite d’informations ?

La fuite d’informations potentiellement sensibles peut s’avérer onéreuse pour une organisation et avoir un large retentissement sur elle, son activité, son personnel, ses clients et ses partenaires. Les réglementations locales et professionnelles régissent de plus en plus les modes de stockage, de transmission et de sécurisation de certains types d’information. Pour éviter toute violation des réglementations applicables, les organisations doivent se protéger contre les fuites d’information intentionnelles, intempestives ou accidentelles.

Une fuite d’informations peut avoir les conséquences suivantes :

  - **Dommages financiers**   En fonction de la taille, du secteur d’activité et des réglementations locales, la fuite d’informations peut aussi avoir un impact financier en raison de la perte de profits engendrée ou du paiement d’amendes et de dommages et intérêts punitifs imposés par les tribunaux ou les autorités réglementaires. Les sociétés de droit public risquent aussi une perte de capitalisation boursière en raison d’une couverture médiatique défavorable.

  - **Détérioration de l’image de marque et de la crédibilité**   Les fuites d’informations peuvent nuire à l’image de marque de l’organisation et à sa crédibilité auprès des clients. De plus, selon la nature des informations contenues dans les messages électroniques divulgués, la fuite peut être une source d’embarras pour l’expéditeur et l’organisation.

  - **Perte d’avantage concurrentiel**   Une des menaces les plus sérieuses posée par la fuite d’informations est la perte de l’avantage concurrentiel de l’organisation. La divulgation d’informations portant sur des plans stratégiques ou des fusions et acquisitions peut entraîner une perte de recettes ou de capitalisation boursière. La perte d’informations de recherche et développement, de données analytiques et de droits de propriété intellectuelle font partie des autres menaces possibles.

Qu’est-ce que la fuite d’informations ?

## Solutions traditionnelles de prévention des fuites d’informations

Bien que les solutions traditionnelles de prévention des fuites d’informations offrent une protection contre l’accès initial aux données, elles ne fournissent pas une protection constante. Le tableau suivant répertorie plusieurs solutions traditionnelles et leurs limites.

### Solutions traditionnelles

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Solution</th>
<th>Description</th>
<th>Limites</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Protocole TLS (Transport Layer Security)</p></td>
<td><p>Le protocole TLS est un protocole Internet normalisé de sécurisation des échanges sur un réseau qui fait appel au chiffrement. Dans un environnement de messagerie, le protocole TLS permet de sécuriser les échanges entre serveurs et entre clients et serveurs.</p>
<p>Par défaut, Exchange 2010 utilise le protocole TLS pour tous les transferts internes de messages. Le protocole TLS opportuniste est également activé par défaut pour les sessions impliquant des hôtes externes. Exchange essaie d’abord d’utiliser le chiffrement TLS pour la session, mais si une connexion TLS ne peut pas être établie avec le serveur de destination, Exchange utilise le protocole SMTP. Il est également possible de configurer la sécurité de domaine en intégrant le mécanisme Mutual TLS pour les organisations externes .</p></td>
<td><p>Le protocole TLS protège uniquement la session SMTP entre deux hôtes SMTP. En d’autres termes, TLS protège les informations en mouvement, mais ne protège pas l’information au niveau du message ni dans ses autres aspects. À moins d’utiliser une autre méthode de chiffrement, les messages contenus dans les boîtes aux lettres des expéditeurs et des destinataires restent sans protection. Pour les messages électroniques envoyés à des destinataires extérieurs à l’organisation, le protocole TLS ne peut être exigé que pour le premier saut. Lorsqu’un hôte SMTP distant à l’extérieur de votre organisation reçoit le message, il peut le relayer à un autre hôte SMTP via une session non chiffrée. Puisque le protocole TLS est un mécanisme de la couche transport, il ne permet pas de contrôler ce que le destinataire fait avec le message.</p></td>
</tr>
<tr class="even">
<td><p>Chiffrement des messages électroniques</p></td>
<td><p>Les utilisateurs peuvent utiliser des technologies de chiffrement des messages telles que S/MIME.</p></td>
<td><p>Les utilisateurs décident si un message doit être chiffré ou non. Le déploiement d’une infrastructure à clé publique (PKI) avec sa charge connexe de gestion des certificats des utilisateurs et la protection des clés privées entraîne des coûts supplémentaires. Une fois qu’un message est déchiffré, le destinataire peut faire ce qu’il veut des informations qu’il contient sans possibilité de contrôle. Le contenu déchiffré peut être copié, imprimé ou transféré. Par défaut, les pièces jointes enregistrées ne sont pas protégées.</p>
<p>Votre organisation ne peut pas accéder aux messages chiffrés à l’aide de technologies telles que S/MIME. Comme l’organisation ne peut pas inspecter le contenu du message, elle ne peut pas appliquer les stratégies de messagerie, procéder à une analyse des messages pour rechercher les virus ou contenus malveillants, ni effectuer toute autre action exigeant l’accès au contenu.</p></td>
</tr>
</tbody>
</table>


Enfin, les solutions traditionnelles manquent souvent d’outils de contrôle obligatoire permettant d’appliquer les stratégies de messagerie destinées à empêcher les fuites d’informations. Par exemple, un utilisateur envoie un message contenant des informations sensibles et le marque comme **Confidentiel** et **Ne pas transférer**. Une fois le message remis au destinataire, l’expéditeur ou l’organisation ne dispose plus d’aucun moyen de contrôle de l’information. Le destinataire peut transférer le message volontairement ou par mégarde (en utilisant des fonctions telles que les règles de transfert automatique) à des comptes de messagerie externes et exposer votre organisation à des risques de fuites d’informations importantes.

Qu’est-ce que la fuite d’informations ?

## Gestion des droits relatifs à l’information (IRM) dans Exchange 2013

Dans Exchange 2013, vous pouvez utiliser les fonctionnalités IRM pour appliquer une protection permanente aux messages et pièces jointes. IRM utilise Active Directory Rights Management Services (AD RMS), une technologie de protection des informations inhérente à Windows Server 2008 et versions ultérieures. Grâce aux fonctionnalités IRM d’Exchange 2013, votre organisation et vos utilisateurs peuvent contrôler les droits dont disposent les destinataires sur leurs courriers électroniques. La gestion des droits relatifs à l’information permet également d’autoriser ou de restreindre les actions des destinataires, comme le transfert d’un message à d’autres destinataires, l’impression d’un message ou d’une pièce jointe ou l’extraction du contenu d’un message ou d’une pièce jointe par une opération copier-coller. La protection IRM peut être appliquée par des utilisateurs dans Microsoft Outlook ou Microsoft Office Outlook Web App, ou elle peut se baser sur les stratégies de messagerie de votre organisation et être appliquée à l’aide des règles de protection du transport ou des règles de protection Outlook. Contrairement aux autres solutions de chiffrement des messages électroniques, la gestion des droits relatifs à l’information permet également à votre organisation de déchiffrer le contenu protégé pour imposer la conformité à la stratégie de messagerie.

AD RMS fait appel à des certificats ou licences XrML (eXtensible Rights Markup Language) pour certifier les ordinateurs et les utilisateurs et pour protéger le contenu. Lorsque le contenu d’un document ou d’un message est protégé par AD RMS, une licence XrML, contenant les droits d’accès au contenu par les utilisateurs, est jointe à ce contenu. Pour accéder au contenu protégé par IRM, les applications activées pour AD RMS doivent fournir une licence d’utilisation pour l’utilisateur autorisé à partir du cluster AD RMS.

> [!NOTE]
> Dans Exchange 2013, l’agent de pré-licence joint une licence d’utilisation aux messages protégés via le cluster AD RMS dans votre organisation. Pour plus d’informations, voir Pré-licence plus loin dans cette rubrique.


Les applications servant à créer le contenu doivent être activées pour RMS pour appliquer une protection de contenu permanente en utilisant les services AD RMS. Les applications Microsoft Office, telles que Word, Excel, PowerPoint et Outlook sont activées pour RMS et peuvent être utilisées pour créer et consommer des contenus protégés.

La gestion des droits relatifs à l’information vous aide à effectuer les opérations suivantes :

  - Empêcher un destinataire autorisé d’un contenu protégé par IRM de transférer, modifier, imprimer, télécopier, enregistrer ou couper et coller ce contenu.

  - Protéger les formats de fichier de pièce jointe pris en charge en leur conférant le même niveau de protection que celui du message.

  - Prendre en charge l’expiration des messages et pièces jointes protégés par IRM pour qu’ils ne puissent plus être consultés après la période spécifiée.

  - Empêcher la copie d’un contenu protégé par IRM à l’aide de l’outil Capture dans Microsoft Windows.

Toutefois, la gestion des droits relatifs à l’information ne peut pas empêcher la copie d’informations à l’aide des méthodes suivantes :

  - Programmes de capture d’écran tiers

  - Utilisation de périphériques d’acquisition d’images, tels qu’un appareil photo, pour photographier le contenu protégé par IRM qui est affiché à l’écran

  - Mémorisation des informations ou leur transcription manuelle par les utilisateurs

Pour en savoir plus sur AD RMS, voir [Services AD RMS (Active Directory Rights Management Services)](https://go.microsoft.com/fwlink/p/?linkid=129823).

## Modèles de stratégie de droits AD RMS

AD RMS utilise les modèles de stratégie des droits d’accès XrML pour permettre aux applications compatibles avec la gestion de droits relatifs à l’information d’appliquer des stratégies de protection cohérentes. Dans Windows Server 2008 et les versions ultérieures, le serveur AD RMS comprend un service Web utilisable pour énumérer et obtenir des modèles. Exchange 2013 est fourni avec le modèle Ne pas transférer. Lorsque ce modèle est appliqué à un message, seuls les destinataires peuvent déchiffrer le message. Les destinataires ne peuvent pas transférer le message, copier son contenu ou l’imprimer. Vous pouvez créer des modèles RMS supplémentaires sur le serveur AD RMS de votre organisation pour répondre aux exigences de protection IRM.

La protection IRM est appliquée en utilisant un modèle de stratégie de droits d’accès AD RMS. Ces modèles de stratégie permettent de contrôler les autorisations des destinataires sur un message. En appliquant le modèle approprié de stratégie de droits d’accès au message, les actions comme répondre, répondre à tous, transférer, extraire les informations d’un message, enregistrer ou imprimer un message peuvent être contrôlées.

Pour plus d’informations sur les modèles de stratégie de droits, consultez les [considérations relatives aux modèles de stratégie AD RMS](https://go.microsoft.com/fwlink/p/?linkid=179455).

Pour plus d’informations sur la création des modèles de stratégie de droits AD RMS, consultez le [guide détaillé sur la création et le déploiement de modèles de stratégie de droits AD RMS](https://go.microsoft.com/fwlink/p/?linkid=136593).

Qu’est-ce que la fuite d’informations ?

## Application de la protection IRM aux messages

Dans Exchange 2010, la protection IRM peut être appliquée aux messages à l’aide des méthodes suivantes :

  - **Manuellement par les utilisateurs Outlook**   Les utilisateurs d’Outlook peuvent protéger leurs messages par IRM en appliquant les modèles de stratégie de droits d’accès AD RMS mis à leur disposition. Ce processus utilise la fonctionnalité IRM dans Outlook, mais pas Exchange. Il est toutefois possible d’utiliser Exchange pour accéder aux messages et prendre des mesures (telles que l’application des règles de transport) pour faire appliquer la stratégie de messagerie de votre organisation. Pour plus d’informations sur l’utilisation de l’IRM dans Outlook, voir [Présentation de l’IRM pour les messages électroniques](https://go.microsoft.com/fwlink/p/?linkid=166897).

  - **Manuellement par les utilisateurs Outlook Web App**   Lorsque vous activez IRM dans Outlook Web App, les utilisateurs peuvent activer une protection IRM pour les messages qu’ils envoient et afficher les messages protégés par IRM qu’ils reçoivent. Dans la Mise à jour cumulative 1 (CU1) Exchange 2013, les utilisateurs d’Outlook Web App peuvent afficher des pièces jointes protégées par IRM à l’aide de l’affichage de document WebReady. Pour plus d’informations sur IRM dans Outlook Web App, consultez la rubrique [Gestion des droits relatifs à l’information dans Outlook Web App](information-rights-management-in-outlook-web-app-exchange-2013-help.md).

  - **Manuellement par les utilisateurs d’appareils Windows Mobile et Exchange ActiveSync**   Dans la version de publication (RTM) d’Exchange 2010, les utilisateurs d’appareils Windows Mobile peuvent afficher et créer des messages protégés par IRM. Avec cette méthode, l’utilisateur doit connecter son appareil Windows Mobile pris en charge à un ordinateur et l’activer pour les fonctionnalités IRM. Dans Exchange 2010 SP1, vous pouvez activer IRM dans Microsoft Exchange ActiveSync afin de permettre aux utilisateurs de périphériques Exchange ActiveSync (notamment les appareils Windows Mobile) d’afficher, de transférer, de créer des messages protégés par IRM et d’y répondre. Pour plus d’informations sur IRM dans Exchange ActiveSync, consultez la rubrique [Gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync](information-rights-management-in-exchange-activesync-exchange-2013-help.md).

  - **Automatiquement dans Outlook 2010 et version ultérieure**   Outlook 2010 (et version ultérieure) permet de créer des règles de protection Outlook pour activer une protection IRM automatique des messages. Les règles de protection Outlook sont déployées automatiquement chez les clients Outlook 2010, et la protection IRM est appliquée par Outlook 2010 lorsque l’utilisateur compose un message. Pour plus d’informations sur les règles de protection d’Outlook, consultez la rubrique [Règles de protection Outlook](outlook-protection-rules-exchange-2013-help.md).

  - **Automatiquement sur les serveurs de boîtes aux lettres**   Vous pouvez créer des règles de protection du transport pour activer une protection IRM automatique des messages sur les serveurs de boîtes aux lettres Exchange 2013. Pour plus d’informations sur les règles de protection du transport, consultez la rubrique [Règles de protection de transport](transport-protection-rules-exchange-2013-help.md).
    
    > [!NOTE]
    > La protection IRM n’est pas appliquée à nouveau aux messages qui sont déjà protégés par IRM. Par exemple, si un utilisateur active la protection IRM d’un message dans Outlook ou Outlook Web App, cette protection n’est pas appliquée au message en utilisant une règle de protection du transport.


Qu’est-ce que la fuite d’informations ?

## Scénarios pour la protection IRM

Les scénarios de protection IRM sont décrits dans le tableau suivant.

### Scénarios pour la protection IRM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Envoi de messages protégés par IRM</th>
<th>Pris en charge</th>
<th>Conditions requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Au sein du même déploiement d’Exchange 2013 en local</p></td>
<td><p>Oui</p></td>
<td><p>Pour plus d’informations sur les conditions requises, voir Configuration requise pour la gestion des droits relatifs à l’information (IRM) plus loin dans cette rubrique.</p></td>
</tr>
<tr class="even">
<td><p>Entre différentes forêts au sein d’un déploiement en local</p></td>
<td><p>Oui</p></td>
<td><p>Pour plus d’informations sur les conditions requises, consultez la rubrique relative à la <a href="https://go.microsoft.com/fwlink/p/?linkid=199009">configuration d’AD RMS pour l’intégrer avec Exchange Server 2010 dans plusieurs forêts</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Entre un déploiement d’Exchange 2013 en local et une organisation Exchange virtuelle (dans le nuage)</p></td>
<td><p>Oui</p></td>
<td><ul>
<li><p>Utilisez un serveur AD RMS local.</p></li>
<li><p>Exportez le domaine de publication sécurisé depuis votre serveur AD RMS local.</p></li>
<li><p>Importez le domaine de publication sécurisé dans votre organisation dans le nuage.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Pour les destinataires externes</p></td>
<td><p>Non</p></td>
<td><p>Exchange 2010 n’inclut pas de solution permettant l’envoi de messages protégés par IRM à des destinataires externes dans une organisation non fédérée. AD RMS propose des solutions faisant appel aux stratégies d’approbation. Vous pouvez configurer une stratégie d’approbation entre votre cluster AD RMS et le compte Microsoft (appelé précédemment Windows Live ID). Pour les messages envoyés entre deux organisations, vous pouvez créer une approbation fédérée entre les deux forêts Active Directory via les services de fédération Active Directory (AD FS). Pour en savoir plus, voir <a href="https://go.microsoft.com/fwlink/p/?linkid=182909">Présentation des stratégies d’approbation AD RMS</a>.</p></td>
</tr>
</tbody>
</table>


Qu’est-ce que la fuite d’informations ?

## Déchiffrement des messages protégés par IRM pour imposer les stratégies de messagerie

Pour faire appliquer les stratégies de messagerie et aux fins de conformité réglementaire, vous devez pouvoir accéder au contenu chiffré des messages. Pour satisfaire les obligations de détection légale afférentes aux litiges, audits réglementaires ou enquêtes internes, vous devez aussi être en mesure de rechercher les messages chiffrés. Pour faciliter ces tâches, Exchange 2013 inclut les fonctionnalités IRM suivantes :

  - **Déchiffrement du transport**   Pour appliquer les stratégies de messagerie, les agents de transport, tels que l’agent de règles de transport, doivent pouvoir accéder au contenu des messages. Le déchiffrement du transport permet aux agents de transport installés sur les serveurs Exchange 2013 d’accéder au contenu des messages. Pour plus d’informations, consultez la rubrique [Déchiffrement du transport](transport-decryption-exchange-2013-help.md).

  - **Déchiffrement de l’état de journal**   Pour répondre aux obligations réglementaires ou commerciales, les organisations peuvent utiliser la journalisation pour préserver le contenu des messages. L’agent de journalisation crée un état de journal pour les messages soumis à la journalisation et inclut les métadonnées relatives aux messages dans ce rapport. Le message d’origine est joint à l’état du journal. Si un message contenu dans l’état du journal est protégé par IRM, la fonction de déchiffrement de l’état du journal joint une copie du message en texte clair à l’état du journal. Pour plus d’informations, consultez la rubrique [Déchiffrement de l'état de journal](journal-report-decryption-exchange-2013-help.md).

  - **Déchiffrement IRM pour Exchange Search**   Cette fonctionnalité de Déchiffrement IRM pour Exchange Search permet à Exchange Search d’indexer le contenu des messages protégés par IRM. Lorsqu’un gestionnaire de découverte effectue une recherche In-Place eDiscovery (découverte électronique sur place), les messages protégés par IRM ayant été indexés font partie des résultats de la recherche. Pour plus d’informations, voir [Découverte électronique locale](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).
    
    > [!NOTE]
    > Dans Exchange 2010 SP1, les membres du groupe de rôles Gestion de la découverte peuvent accéder aux messages protégés par IRM renvoyés par une détection et résidant dans une boîte aux lettres de détection. Pour activer cette fonctionnalité, utilisez le paramètre <em>EDiscoverySuperUserEnabled</em> avec la cmdlet <a href="https://technet.microsoft.com/fr-fr/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a>. Pour plus d’informations, voir <a href="configure-irm-for-exchange-search-and-https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">Configurer IRM pour la recherche et la découverte locale dans Exchange</a>.


Pour activer ces fonctionnalités de déchiffrement, les serveurs Exchange doivent pouvoir accéder au message. Cela est possible en ajoutant la boîte aux lettres de fédération (une boîte aux lettres système créée par le programme d’installation d’Exchange) au groupe des super utilisateurs sur le serveur AD RMS. Pour plus d’informations, consultez la rubrique [Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

Qu’est-ce que la fuite d’informations ?

## Pré-licence

Pour afficher les messages et pièces jointes protégés par IRM, Exchange 2013 joint automatiquement une pré-licence aux messages protégés. Ainsi, le client n’a pas besoin de revenir plusieurs fois au serveur AD RMS pour récupérer une licence d’utilisation et autorise la consultation hors ligne des messages et pièces jointes protégés par IRM. Le service de pré-licence permet également aux messages protégés par IRM de s’afficher dans Outlook Web App. Lorsque vous activez les fonctionnalités de gestion des droits relatifs à l’information, la pré-licence est activée par défaut.

Qu’est-ce que la fuite d’informations ?

## Agents IRM

Dans Exchange 2013, la fonctionnalité IRM est activée via les agents de transport dans le service de transport des serveurs de boîtes aux lettres. Les agents IRM sont installés par le programme d’installation d’Exchange sur un serveur de boîtes aux lettres. Vous ne pouvez pas contrôler les agents IRM en utilisant les tâches de gestion des agents de transport.

> [!NOTE]
> Dans Exchange 2013, les agents IRM sont des agents intégrés. Les agents intégrés ne figurent pas dans la liste des agents renvoyés par la cmdlet <strong>Get-TransportAgent</strong>. Pour plus d’informations, consultez la rubrique <a href="transport-agents-exchange-2013-help.md">Agents de transport</a>.


Le tableau suivant répertorie les agents IRM mis en œuvre dans le service de transport des serveurs de boîtes aux lettres.

### Agents IRM dans le service de transport des serveurs de boîtes aux lettres

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Agent</th>
<th>Événement</th>
<th>Fonction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agent de déchiffrement RMS</p></td>
<td><p>OnEndOfData (SMTP) et OnSubmittedMessage</p></td>
<td><p>Déchiffre les messages pour autoriser l’accès aux agents de transport.</p></td>
</tr>
<tr class="even">
<td><p>Agent de règles de transport</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Marque les messages répondant aux conditions d’une règle de protection de transport comme devant recevoir une protection IRM par l’agent de chiffrement RMS.</p></td>
</tr>
<tr class="odd">
<td><p>Agent de chiffrement RMS</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Applique la protection IRM aux messages marqués par l’agent de règles de transport et chiffre à nouveau les messages déchiffrés au cours du transport.</p></td>
</tr>
<tr class="even">
<td><p>Agent de pré-licence</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Joint une pré-licence aux messages protégés par IRM.</p></td>
</tr>
<tr class="odd">
<td><p>Agent de déchiffrement du rapport de journal</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>Déchiffre les messages protégés par IRM qui sont joints aux états de journal et incorpore des versions en texte clair aux messages d’origine chiffrés.</p></td>
</tr>
</tbody>
</table>


Pour plus d’informations sur les agents de transport, consultez la rubrique [Agents de transport](transport-agents-exchange-2013-help.md).

Qu’est-ce que la fuite d’informations ?

## Configuration requise pour la gestion des droits relatifs à l’information (IRM)

Pour implémenter IRM dans votre organisation Exchange 2013, votre déploiement doit répondre aux conditions décrites dans le tableau suivant.

### Configuration requise pour la gestion des droits relatifs à l’information (IRM)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveur</th>
<th>Configuration requise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster AD RMS</p></td>
<td><ul>
<li><p><strong>Système d’exploitation</strong>   Windows Server 2012, Windows Server 2008 R2 ou Windows Server 2008 SP2 avec le correctif <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973247">Rôle d’Active Directory Rights Management Services dans Windows Server 2008</a> est requis.</p></li>
<li><p><strong>Point de connexion de service</strong>   Exchange 2010 et les applications compatibles AD RMS utilisent le point de connexion de service enregistré dans Active Directory pour détecter un cluster AD RMS et les URL. AD RMS vous permet d’enregistrer le point de connexion de service à partir du programme d’installation d’AD RMS. Si le compte utilisé pour installer AD RMS n’est pas membre du groupe de sécurité Administrateurs d’entreprise, il est possible d’effectuer l’enregistrement du point de connexion de service une fois que l’installation est terminée. La forêt Active Directory comporte un seul point de connexion de service pour AD RMS.</p></li>
<li><p><strong>Autorisations</strong>   Les autorisations de lecture et d’exécution sur le pipeline de certification du serveur AD RMS (fichier <code>ServerCertification.asmx</code> sur les serveurs AD RMS) doivent être attribuées aux éléments suivants :</p>
<ul>
<li><p>Groupe de serveurs Exchange ou serveurs Exchange spécifiques</p></li>
<li><p>Groupe de services AD RMS sur les serveurs AD RMS</p></li>
</ul>
<p>Par défaut, le fichier ServerCertification.asmx se trouve dans le dossier <code>\inetpub\wwwroot\_wmcs\certification\</code> sur les serveurs AD RMS. Pour plus de détails, consultez la rubrique relative à la <a href="https://go.microsoft.com/fwlink/p/?linkid=186951">définition des autorisations dans le pipeline de certification du serveur AD RMS</a>.</p></li>
<li><p><strong>Super utilisateurs AD RMS</strong>   Pour activer le déchiffrement du transport, le déchiffrement d’états de journal, la gestion des droits relatifs à l’information dans Outlook Web App et pour Exchange Search, vous devez ajouter la boîte aux lettres de fédération (une boîte aux lettres système créée par le programme d’installation d’Exchange 2013) au groupe des super utilisateurs sur le cluster AD RMS. Pour plus d’informations, consultez la rubrique <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010 ou version ultérieure est requis.</p></li>
<li><p>Le correctif <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973136">CORRECTIF : ArgumentNullException exception message d’erreur lorsqu’une application.NET_Framework_2.0_SP2-based tente de traiter une réponse avec contenu zero-length à une demande de service ASP.NET Web asynchrone : « La valeur ne peut pas être Null »</a> est recommandé pour Microsoft .NET Framework 2.0 SP2.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Les utilisateurs peuvent définir une protection IRM pour les messages Outlook. Outlook 2003 prend en charge les modèles AD RMS pour les messages protégés par IRM.</p></li>
<li><p>Les règles de protection d’Outlook sont une fonctionnalité d’Exchange 2010 et d’Outlook 2010. Les versions antérieures d’Outlook ne prennent pas en charge cette fonctionnalité.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Les appareils qui prennent en charge le protocole Exchange ActiveSync version 14.1, notamment les périphériques Windows Mobile, peuvent prendre en charge les fonctionnalités IRM dans Exchange ActiveSync. L’application de messagerie sur un appareil mobile doit prendre en charge la balise <strong>RightsManagementInformation</strong> définie dans le protocole Exchange ActiveSync version 14.1. Dans Exchange 2013, IRM dans Exchange ActiveSync permet aux utilisateurs disposant d’appareils pris en charge d’afficher, de transférer, de créer des messages protégés par IRM et d’y répondre, sans devoir connecter l’appareil à un ordinateur et l’activer pour IRM. Pour plus d’informations, consultez la rubrique <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Gestion des droits relatifs à l’information (IRM) dans Exchange ActiveSync</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


> [!NOTE]
> <em>« Cluster</em> <em>AD RMS »</em> est le terme utilisé pour un déploiement AD RMS dans une organisation, y compris le déploiement d’un seul serveur. AD RMS est un service Web. Il n’exige pas l’installation du composant Clustering avec basculement de Windows Server. Pour la haute disponibilité et l’équilibrage de la charge, vous pouvez déployer plusieurs serveurs AD RMS dans le cluster et utiliser la fonctionnalité d’équilibrage de la charge réseau.


> [!IMPORTANT]
> Un environnement de production ne prend pas en charge l’installation d’AD RMS et d’Exchange sur le même serveur.


Les fonctionnalités IRM d’Exchange 2013 prennent en charge les formats de fichiers Microsoft Office. Vous pouvez étendre la protection IRM à d’autres formats de fichiers en déployant des protections personnalisées. Pour plus d’informations, consultez la page [Partenaires Microsoft](https://go.microsoft.com/fwlink/p/?linkid=210336).

Qu’est-ce que la fuite d’informations ?

## Configuration et test de la gestion des droits relatifs à l’information (IRM)

Vous devez utiliser l’environnement de ligne de commande Exchange pour configurer les fonctionnalités IRM dans Exchange 2013. Pour configurer les fonctionnalités IRM individuelles, utilisez la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)). Vous pouvez activer ou désactiver IRM pour les messages internes, le déchiffrement du transport, le déchiffrement des rapports de journal, Exchange Search et Outlook Web App. Pour plus d’informations sur la configuration des fonctions de gestion des droits relatifs à l’information, consultez la rubrique [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

Après avoir installé un serveur Exchange 2013, vous pouvez utiliser la cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979798\(v=exchg.150\)) pour tester de bout en bout votre déploiement IRM. Ces tests servent à vérifier la fonctionnalité de gestion des droits relatifs à l’information immédiatement après sa configuration initiale et de manière continue. La cmdlet exécute les tests suivants :

  - Elle inspecte la configuration IRM de votre organisation Exchange 2013.

  - Elle contrôle les informations relatives à la version et aux correctifs du serveur AD RMS.

  - Elle vérifie s’il est possible d’activer un serveur Exchange pour RMS en récupérant le certificat de compte de droits (RAC) et le certificat de licence client.

  - Elle acquiert des modèles de stratégie de droits AD RMS à partir du serveur AD RMS.

  - Elle vérifie que l’expéditeur spécifié peut envoyer des messages protégés par IRM.

  - Elle récupère une licence d’utilisation de super utilisateur pour le destinataire spécifié.

  - Elle acquiert une pré-licence pour le destinataire spécifié.

Qu’est-ce que la fuite d’informations ?

## Étendre Rights Management avec le connecteur Rights Management

Le connecteur Microsoft Rights Management (connecteur RMS) est une application facultative qui améliore la protection des données de votre serveur Exchange 2013 en utilisant des services Microsoft Rights Management en nuage. Une fois que vous avez installé le connecteur RMS, il protège en continu les données au cours de la durée de vie des informations et, comme ces services sont personnalisables, vous pouvez définir le niveau de protection dont vous avez besoin. Par exemple, vous pouvez limiter l’accès d’utilisateurs spécifiques à des courriers électroniques ou définir des droits d’affichage seul pour certains messages.

Pour en savoir plus sur le connecteur RMS et son installation, consultez la rubrique [Déploiement du connecteur Azure Rights Management](https://technet.microsoft.com/fr-fr/library/dn375964.aspx).

