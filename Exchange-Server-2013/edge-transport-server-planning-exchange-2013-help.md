---
title: 'Planification de serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Planification de serveurs de transport Edge
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61543915
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planification de serveurs de transport Edge

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-07_

Le rôle serveur de transport Edge a été réintroduit dans Exchange Service Pack 1. Il offre une protection renforcée contre le courrier indésirable au sein des organisations Exchange. Le serveur de transport Edge applique également des stratégies aux messages en cours de transport entre des organisations. Ce rôle serveur est déployé dans le réseau de périmètre et en dehors de la forêt Active Directory. Contrairement aux serveurs d’accès au client ou de boîtes aux lettres, les serveurs de transport Edge ne disposent pas d’un accès direct à Active Directory pour obtenir des informations sur les destinataires et la configuration. Ils utilisent les services AD LDS (Active Directory Lightweight Directory Services) pour le stockage local des informations de configuration et de destinataire.

Vous pouvez ajouter un serveur de transport Edge à une organisation Exchange 2013 existante. Aucune opération de préparation d’Active Directory supplémentaire n’est nécessaire pour installer le serveur de transport Edge.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous ajoutez un serveur de transport Edge à une organisation Exchange 2010 ou Exchange 2007 existante, vous devez installer un correctif cumulatif spécifique sur vos serveurs hérités avant d’installer un serveur de transport Edge Exchange 2013. Pour plus d’informations, voir <a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a>.</td>
</tr>
</tbody>
</table>


Si vous projetez de déployer des serveurs de transport Edge, vous devez tenir compte des aspects suivants :

  - **Capacité du serveur**   La planification de la capacité du serveur inclut la planification de la surveillance des performances du serveur de transport Edge. La surveillance des performances vous aide à comprendre l’intensité du travail du serveur. Ces informations déterminent la capacité de votre configuration matérielle.

  - **Fonctionnalités de transport**   Le serveur de transport Edge peut fournir une protection contre le courrier indésirable au niveau du périmètre du réseau. Dans le cadre du processus de planification, vous devez déterminer les fonctionnalités de blocage du courrier indésirable que vous activerez au niveau du serveur de transport Edge et la manière dont elles seront configurées.

  - **Sécurité**   Le rôle serveur de transport Edge est conçu pour présenter une surface d’attaque minimale. C’est pourquoi il est important de sécuriser et de gérer correctement l’accès physique et l’accès réseau au serveur. La planification de la sécurité vous aide à vous assurer que les connexions IP ne sont activées que depuis des serveurs et des utilisateurs autorisés. Pour plus d’informations, consultez la [Liste de vérification pour la sécurité du pré-déploiement](deployment-security-checklist-exchange-2013-help.md).
    
    La pratique recommandée consiste à placer le serveur de transport Edge dans un réseau de périmètre. Pour être certain que le serveur puisse envoyer et recevoir des messages électroniques, et recevoir des mises à jour des données sur la configuration et les destinataires à partir du service Microsoft Exchange EdgeSync, vous devez autoriser la communication via les ports indiqués dans le tableau suivant.
    
    ### Paramètres de port de communication pour les serveurs de transport Edge
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Interface réseau</th>
    <th>Port ouvert</th>
    <th>Protocole</th>
    <th>Remarque</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Internet entrant et sortant</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Ce port est requis pour le flux de messagerie Internet.</p></td>
    </tr>
    <tr class="even">
    <td><p>Réseau interne entrant et sortant</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Ce port est requis pour le flux de messagerie de l’organisation Exchange.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Local uniquement</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>Ce port permet d’établir une connexion locale aux services AD LDS.</p></td>
    </tr>
    <tr class="even">
    <td><p>Entrant du réseau interne</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>LDAP sécurisé</p></td>
    <td><p>Ce port est requis pour la synchronisation EdgeSync.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Entrant du réseau interne</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>L’ouverture de ce port est facultative. Il offre davantage de flexibilité pour la gestion de serveurs de transport Edge depuis le réseau interne en vous permettant d’utiliser une connexion Bureau à distance pour gérer le serveur de transport Edge.</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le rôle serveur de transport Edge utilise des ports LDAP non standard. Les ports spécifiés dans cette rubrique sont les ports de communication LDAP configurés lors de l’installation du rôle serveur de transport Edge.</td>
    </tr>
    </tbody>
    </table>


  - **EdgeSync**   La procédure de déploiement recommandée consiste à créer un abonnement Edge pour abonner le serveur de transport Edge à l’organisation Exchange. Lorsque vous créez un abonnement Edge, les données de destinataire et de configuration sont dupliquées d’Active Directory vers le service d’annuaire AD LDS. Vous abonnez un serveur de transport Edge à un site Active Directory. Ensuite, le service Microsoft Exchange EdgeSync exécuté sur les serveurs de boîtes aux lettres de ce site met périodiquement à jour le service d’annuaire AD LDS en synchronisant les données à partir d’Active Directory. Le processus d’abonnement Edge déploie automatiquement les connecteurs d’envoi requis pour activer le flux de messagerie de l’organisation Exchange vers Internet via un serveur de transport Edge. Si vous utilisez les fonctions de recherche de destinataire ou d’agrégation de listes fiables sur le serveur de transport Edge, vous devez abonner le serveur de transport Edge à l’organisation.

## Configurer les paramètres DNS pour le rôle serveur de transport Edge

Le rôle serveur de transport Edge est déployé hors de l’organisation Exchange comme serveur autonome dans le réseau de périmètre ou comme membre d’un domaine Active Directory de réseau de périmètre. Vous devez configurer manuellement le suffixe DNS correct du rôle serveur de transport Edge avant d’installer Exchange 2013. Si aucun suffixe DNS n’est configuré, l’installation échouera.

Le serveur de transport Edge étant déployé dans le réseau de périmètre, il dispose d’interfaces réseau connectées à plusieurs segments réseau. Chacun de ces segments réseau possède une configuration IP unique. L’interface réseau connectée au segment réseau externe ou public doit être configurée pour utiliser un serveur DNS public pour la résolution de noms. Cela permet au serveur de résoudre des noms de domaine de protocole SMTP (Simple Mail Transfer Protocol) en enregistrements de ressource MX et de router les messages vers Internet.

L’interface réseau connectée au segment réseau interne ou privé doit être configurée pour utiliser un serveur DNS capable de résoudre les noms des serveurs de boîtes aux lettres de votre organisation ou doit disposer d’un fichier HOSTS. Les serveurs de transport Edge et de boîtes aux lettres doivent pouvoir utiliser la résolution d’hôte DNS pour se localiser mutuellement.

Pour activer la résolution des noms des serveurs de boîtes aux lettres par les serveurs de transport Edge, utilisez l’une des méthodes suivantes :

  - Créez manuellement des enregistrements de ressource pour les serveurs de boîtes aux lettres dans une zone de recherche directe du serveur DNS configuré sur la carte réseau interne du serveur de transport Edge.

  - Modifiez le fichier HOSTS du serveur de transport Edge pour inclure les enregistrements d’hôtes des serveurs de boîtes aux lettres. Le fichier HOSTS est un fichier texte local du même format que le fichier /etc/hosts pour UNIX 4.3 Berkeley Software Distribution (BSD). Ce fichier mappe les noms d’hôte vers des adresses IP et est stocké dans le dossier \\%Systemroot%\\System32\\Drivers\\Etc.

Pour activer la résolution des noms des serveurs de transport Edge par les serveurs de boîtes aux lettres, utilisez l’une des méthodes suivantes :

  - Créez manuellement des enregistrements de ressource pour les serveurs de transport Edge dans une zone de recherche directe du serveur DNS configuré sur le serveur de boîtes aux lettres.

  - Pour inclure les enregistrements d’hôte des serveurs de transport Edge, modifiez le fichier HOSTS sur les serveurs de boîtes aux lettres situés sur le site Active Directory auxquels ils sont abonnés.

Pour configurer les paramètres DNS du serveur de transport Edge, procédez comme suit :

1.  Vérifiez que les paramètres du serveur DNS de chaque interface réseau sont corrects pour le segment réseau.

2.  Procédez comme suit pour configurer le suffixe DNS pour le nom de serveur de transport Edge :
    
    1.  Ouvrez le Panneau de configuration et sélectionnez **Propriétés système**.
    
    2.  Choisissez l’onglet **Nom de l’ordinateur**.
    
    3.  Choisissez **Modifier**.
    
    4.  Dans la page **Modification du nom d’ordinateur**, cliquez sur **Plus**.
    
    5.  Dans le champ **Suffixe DNS principal de cet ordinateur**, entrez le nom de domaine et le suffixe DNS du serveur de transport Edge.
    
    Ce nom ne peut plus être modifié après l’installation du rôle serveur de transport Edge.

## Remplacer les paramètres DNS

Il se peut que vous deviez remplacer les paramètres de DNS par défaut du serveur Exchange, afin que les messages électroniques soient acheminés et distribués correctement. Pour ce faire, modifiez les paramètres **Recherches DNS internes** et **Recherches DNS externes** dans les propriétés du serveur de transport. Ces paramètres remplacent les paramètres de routage des messages électroniques de la carte réseau.

