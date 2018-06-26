---
title: 'Gestion des droits relatifs à l’information (IRM) dans des déploiements hybrides Exchange: Exchange 2013 Help'
TOCTitle: Gestion des droits relatifs à l’information (IRM) dans des déploiements hybrides Exchange
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50479671
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestion des droits relatifs à l’information (IRM) dans des déploiements hybrides Exchange

 

_<strong>Sapplique à :</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Dernière rubrique modifiée :</strong>2016-12-09_

**Résumé** : Fonctionnement de la gestion des droits relatifs à l’information (IRM) dans un environnement hybride Exchange et configuration des fonctionnalités IRM pour qu’elles fonctionnent entre Exchange Online et vos serveurs Exchange locaux.

Les fonctionnalités de gestion des droits relatifs à l’information (IRM) contribuent à la prévention des fuites d’informations sensibles en offrant une protection persistante, en ligne et hors connexion, des messages électroniques et des pièces jointes. À la fois Exchange, dans votre organisation locale, et Exchange Online, dans Office 365 pour les entreprises, prennent en charge la gestion des droits relatifs à l’information. Il y a cependant des différences entre les deux implémentations et vous devez configurer les fonctionnalités IRM dans l’organisation Exchange Online pour que les utilisateurs de cette organisation puissent s’en servir.

La gestion des droits relatifs à l’information utilise les services AD RMS (Active Directory Rights Management Services), un composant de Windows Server 2008 et d’une version ultérieure. Les services AD RMS permettent de créer du contenu protégé par des droits tel que des messages électroniques et des pièces jointes, et de contrôler la manière dont ce contenu est utilisé ainsi que ses destinataires. Les utilisateurs peuvent spécifier des modèles qui définissent la manière dont le contenu peut être utilisé. Ils peuvent, par exemple, spécifier que l’envoi d’un message électronique à d’autres destinataires n’est pas autorisé ou bien que les informations de ce message ne peuvent pas être copiées.

Pour en savoir plus sur les fonctionnalités IRM dans Exchange 2010, consultez la rubrique suivante : [Présentation de la gestion des droits relatifs à l’information](https://technet.microsoft.com/fr-fr/library/dd638140\(v=exchg.141\).aspx).

Pour plus d’informations sur la gestion des droits relatifs à l’information dans Exchange 2013 et Exchange 2016, consultez la rubrique [Gestion des droits relatifs à l’information](https://technet.microsoft.com/fr-fr/library/dd638140\(v=exchg.150\)).

Pour plus d’informations sur les services AD RMS, consultez la rubrique [Présentation des services AD RMS (Active Directory Rights Management Services)](http://go.microsoft.com/fwlink/p/?linkid=215243).

## Différences entre les fonctionnalités IRM dans Exchange local et Exchange Online

La fonctionnalité IRM disponible dans votre organisation Exchange locale peut être différente de celle disponible dans votre organisation Exchange Online. Le tableau suivant présente un récapitulatif des caractéristiques et des fonctionnalités disponibles dans chaque organisation. (Pour en savoir plus sur ces fonctionnalités, consultez la rubrique : [Gestion des droits relatifs à l’information](https://technet.microsoft.com/fr-fr/library/dd638140\(v=exchg.150\)))

### Fonctionnalités IRM disponibles

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fonctionnalité</th>
<th>Disponible dans Exchange 2007 et les versions antérieures</th>
<th>Disponible dans Exchange 2010</th>
<th>Disponible dans Exchange Online et Exchange 2013 et les versions ultérieures</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Protection manuelle des messages dans Outlook</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Protection manuelle des messages dans Outlook Web App</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Affichage des messages protégés par IRM dans Outlook</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Affichage des messages protégés par IRM dans Outlook Web App</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Agent de pré-licence IRM</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Modèles de stratégie RMS</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Déchiffrement du transport</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Déchiffrement de l'état de journal</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Service de recherche Exchange et déchiffrement de découverte</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Règles de protection Outlook automatiques</p></td>
<td><p>Non</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Règles de protection du transport automatiques</p></td>
<td><p>Non</p></td>
<td><p>Oui</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


## Gestion des droits relatifs à l’information dans les déploiements hybrides

Exchange utilise des serveurs AD RMS dans la forêt Active Directory dans laquelle le serveur Exchange est installé. Pour vos serveurs Exchange locaux, le serveur AD RMS local est utilisé. Pour votre organisation Exchange Online, les serveurs AD RMS gérés dans les centres de données Office 365 sont utilisés. La configuration AD RMS utilisée par chaque organisation Exchange est indépendante de tout autre déploiement AD RMS.

La configuration AD RMS, et donc la configuration de la gestion des droits relatifs à l’information, n’est pas automatiquement répliquée entre votre organisation Exchange locale et l’organisation Exchange Online. Tous les modèles AD RMS que vous avez définis ne sont pas automatiquement copiés dans l’organisation Exchange Online. Si vous souhaitez que les mêmes modèles AD RMS soient disponibles dans l’organisation Exchange Online, vous devez effectuer un export manuel de ces modèles depuis votre organisation locale et les appliquer à l’organisation Office 365. Consultez la section Configurer la Gestion des droits relatifs à l’information (IRM) dans les déploiements hybrides plus loin dans cette rubrique.

## Expérience utilisateur

La configuration IRM appliquée à un utilisateur dépend de l’application cliente dont l’utilisateur se sert et de l’emplacement de sa boîte aux lettres. Le tableau suivant présente le serveur AD RMS dont un utilisateur se servira.

### Serveur AD RMS actif

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Boîte aux lettres locale</th>
<th>Boîte aux lettres Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Clients de bureau Outlook</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS local</p></td>
</tr>
<tr class="even">
<td><p>Outlook sur le web</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS Exchange Online</p></td>
</tr>
<tr class="odd">
<td><p>Périphérique ActiveSync</p></td>
<td><p>AD RMS local</p></td>
<td><p>Technologie AD RMS d’Exchange Online</p></td>
</tr>
</tbody>
</table>


Selon la configuration AD RMS utilisée dans votre organisation locale et votre organisation Exchange Online, il est possible qu’un utilisateur se servant d’Outlook 2007 et d’Outlook sur le web puisse voir différents modèles AD RMS. C’est la raison pour laquelle nous vous recommandons d’utiliser les mêmes modèles dans votre organisation locales et votre organisation Exchange Online.

Il ne devrait y avoir aucune différence d’expérience de gestion des droits relatifs à l’information pour les utilisateurs clients d’Outlook, que leur boîte aux lettres soit dans l’organisation locale ou Exchange Online.

Un utilisateur d’Outlook sur le web dont la boîte aux lettres se trouve sur un serveur Exchange local peut accéder aux messages protégés par des droits uniquement après avoir installé le complément de gestion des droits pour Internet Explorer. Ils ne peuvent répondre à des messages protégés par des droits ni en créer.

Un utilisateur d’Outlook sur le web dont la boîte aux lettres se trouve dans Exchange Online peut accéder à des messages protégés par des droits sans logiciel supplémentaire. Il peut, en outre, répondre et créer des nouveaux messages protégés par des droits.

## Fonctionnalité des serveurs

Les serveurs Exchange locaux utilisent l’agent de pré-licence AD RMS pour déchiffrer les messages protégés par des droits afin que les utilisateurs n’aient pas à fournir d’informations d’identification lorsqu’ils ouvrent ces messages. Le serveur Exchange local contacte le serveur AD RMS local pour vérifier les stratégies et droits d’utilisation et demander l’autorisation de déchiffrer le message.

L’organisation Exchange Online fournit plusieurs fonctionnalités de gestion des droits relatifs à l’information supplémentaires qui utilisent la technologie Exchange Online AD RMS. Ces fonctionnalités, telles que le déchiffrement des rapports de journal, permettent de mettre à disposition des services d’Exchange le contenu des messages protégés par des droits à des fins de traitement supplémentaire. Les contenus déchiffrés d’un message de journal, par exemple, peuvent être enregistrés avec le message initial protégé par des droits afin de faciliter la découverte. En outre, les modèles de gestion des droits relatifs à l’information peuvent être automatiquement appliqués aux messages à l’aide des règles de protection Outlook ou des règles de transport pour s’assurer de la conformité des messages par rapport aux stratégies des organisations en matière de protection des informations.

## Configurer la Gestion des droits relatifs à l’information (IRM) dans les déploiements hybrides

La gestion des droits relatifs à l’information dans Exchange s’appuie sur la technologie AD RMS déployée dans la forêt Active Directory dans laquelle réside le serveur Exchange. La configuration AD RMS n’est pas automatiquement synchronisée entre l’organisation locale et l’organisation Exchange Online. Vous devez effectuer un export manuel de la configuration AD RMS, réputée pour être un domaine de publication approuvé, de votre serveur AD RMS local et importer cette configuration dans l’organisation Exchange Online. Le domaine de publication approuvé inclut la configuration AD RMS, y compris les modèles, dont a besoin l’organisation Exchange Online pour utiliser la gestion des droits relatifs à l’information.

Pour plus d’informations, consultez la rubrique [Considérations relatives au domaine de publication approuvé de la technologie AD RMS](http://go.microsoft.com/fwlink/p/?linkid=215244).

Outre l’application de votre configuration AD RMS locale à l’organisation Exchange Online, vous devez vous assurer que vos serveurs AD RMS peuvent être contactés par les applications clientes Outlook et ActiveSync externes à votre réseau local. Vous devez procéder à cette vérification si vous souhaitez que ces clients accèdent aux messages protégés par des droits en dehors de votre réseau local.

Après avoir configuré votre réseau local et exporté les données de domaine de publication approuvé, vous devez configurer l'organisation Exchange Online en important les données de domaine de publication approuvé et en activant la gestion des droits relatifs à l'information.

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Chaque fois que vous modifiez votre configuration AD RMS locale, vous devez appliquer la nouvelle configuration manuellement à l’organisation Exchange Online. Pour ce faire, exportez les données de domaine de publication approuvé de votre serveur AD RMS local et importez-les dans l’organisation Exchange Online.</td>
</tr>
</tbody>
</table>


## Configuration de la gestion des droits relatifs à l’information (IRM) dans les déploiements hybrides Exchange

Si vous utilisez la gestion des droits relatifs à l’information (IRM) dans votre organisation Exchange locale et souhaitez que les utilisateurs d’Exchange Online y recourent également, vous devez effectuer les opérations suivantes :

1.  Configurer votre serveur AD RMS (Active Directory Rights Management Services) local.

2.  Activer IRM dans votre organisation Exchange Online.

3.  Distribuer les modèles AD RMS importés aux utilisateurs de l'organisation Exchange Online.

## Comment configurer des serveurs AD RMS locaux ?

Pour configurer la fonctionnalité IRM dans un déploiement hybride, vous devez utiliser Windows PowerShell pour accéder à votre serveur AD RMS local. Pour plus d'informations, consultez la rubrique suivante : [Utilisation de Windows PowerShell pour administrer AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

Procédez comme suit pour exporter les données de domaine de publication approuvé de votre serveur AD RMS local, puis configurer l'accès au serveur AD RMS pour les clients externes.

1.  Exportez les données de domaine de publication approuvé de votre organisation locale. Pour plus d'informations, consultez la rubrique suivante : [Exportation d'un domaine de publication approuvé](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  Configurer l'accès aux serveurs AD RMS des clients externes. Pour plus d'informations, consultez la rubrique suivante : [Ajout d'une URL de cluster Extranet](http://go.microsoft.com/fwlink/p/?linkid=214945)

## Comment activer IRM dans l'organisation Exchange Online ?

Une fois les données de domaine de publication approuvé de vos serveurs AD RMS locaux exportées, vous devez les importer dans l'organisation Exchange Online, puis activer IRM.

1.  Dans l'organisation Exchange Online, importez les données de domaine de publication approuvé.
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Activez IRM dans l'organisation Exchange Online.
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## Comment distribuer les modèles AD RMS dans l'organisation Exchange Online ?

Après avoir activé IRM dans l'organisation Exchange Online, vous devez distribuer les modèles AD RMS importés. Les utilisateurs et fonctionnalités d'Exchange Online suivants utilisent des modèles AD RMS :

  - Utilisateurs d’Outlook sur le web

  - Utilisateurs d’Exchange ActiveSync

  - Règles de transport

  - Déchiffrement de l'état de journal

  - Règles de protection d'Outlook

<!-- end list -->

1.  Dans l'organisation Exchange Online, récupérez une liste des modèles AD RMS.
    
        Get-RMSTemplate -Type All

2.  Distribuez les modèles AD RMS aux utilisateurs et fonctionnalités de l'organisation Exchange Online.
    
        Set-RMSTemplate <template name> -Type Distributed
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous ne pouvez pas modifier le modèle AD RMS « Ne pas transférer ».</td>
    </tr>
    </tbody>
    </table>


3.  Répétez l'étape 2 pour tous les modèles AD RMS à distribuer.

## Comment savoir si cela a fonctionné ?

Les utilisateurs d'Outlook sur le web doivent pouvoir appliquer les modèles AD RMS aux nouveaux messages. Les utilisateurs d'Outlook sur le web et d'Exchange ActiveSync doivent pouvoir lire les messages auxquels des modèles AD RMS sont appliqués. En outre, tous les modèles AD RMS qui ont été importés de votre organisation locale doivent être répertoriés lorsque vous exécutez la cmdlet **Get-RMSTemplate**.

Exécutez la commande suivante dans l'organisation Exchange Online.

    Get-RMSTemplate 

Pour plus d'informations, consultez la rubrique suivante : [Gestion des droits relatifs à l’information dans Outlook Web App](https://technet.microsoft.com/fr-fr/library/dd876891\(v=exchg.150\))

