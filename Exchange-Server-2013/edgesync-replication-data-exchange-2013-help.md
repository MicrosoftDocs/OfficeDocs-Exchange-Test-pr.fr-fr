---
title: 'Données de réplication EdgeSync: Exchange 2013 Help'
TOCTitle: Données de réplication EdgeSync
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61180547
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Données de réplication EdgeSync

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Lorsque vous déployez un serveur de transport Edge, il n’a pas accès à Active Directory. Pour effectuer des tâches de recherche de destinataires et d’agrégation de listes fiables, et pour implémenter la sécurité de domaine à l’aide d’une authentification MTLS (Mutual Transport Layer Security), le serveur de transport Edge a besoin de données d’Active Directory. Ces données sont répliquées vers le serveur de transport Edge à l’aide d’EdgeSync et le serveur de transport Edge stocke toutes les informations répliquées dans Active Directory Lightweight Directory Services (AD LDS).

Cette rubrique porte sur les données répliquées d’Active Directory vers AD LDS sur un serveur de transport Edge abonné à un site Active Directory. Pour plus d’informations sur EdgeSync et les abonnements Edge, voir [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

Quatre types de données sont répliqués vers AD LDS et utilisés par le serveur de transport Edge :

informations d’abonnement Edge ;

informations de configuration ;

informations sur le destinataire ;

informations de topologie.

## informations d’abonnement Edge ;

Exchange 2013 étend les schémas Active Directory et AD LDS pour fournir des attributs sur l’objet **ms-Exch-ExchangeServer** afin de représenter les données nécessaires au contrôle de la synchronisation EdgeSync. Ces attributs fournissent trois fonctions à EdgeSync :

  - configuration et maintenance automatiques des informations d’identification utilisées pour sécuriser la connexion LDAP entre un serveur de boîtes aux lettres et un serveur de transport Edge abonné ;

  - arbitrage du processus de verrouillage et de bail de synchronisation, garantissant qu’un seul serveur à la fois tente de se synchroniser avec un serveur de transport Edge individuel. Pour plus d’informations sur le processus de verrouillage et de bail, voir [Abonnements Edge](edge-subscriptions-exchange-2013-help.md) ;

  - optimisation de la synchronisation EdgeSync pour conserver un enregistrement de l’état de synchronisation actuel. Un affichage simple de l’état de synchronisation permet d’éviter une synchronisation manuelle excessive.

Le tableau suivant indique les extensions de schéma spécifiques des abonnements Edge. Les valeurs affectées à ces attributs sont maintenues par l’abonnement Edge et EdgeSync ; elles ne sont pas destinées à être modifiées manuellement.

### Extensions du schéma d’abonnement Edge

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l’attribut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>Clé publique actuelle du certificat utilisé par le serveur. Cette valeur est stockée par les serveurs de transport Edge et les serveurs de boîtes aux lettres. La clé publique permet de chiffrer les informations d’identification utilisées pour authentifier le serveur durant une communication avec les protocoles LDAP et SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>Liste des informations d’identification qu’EdgeSync utilise pour établir une session LDAP authentifiée avec AD LDS. Sur les serveurs de boîtes aux lettres, cet attribut ne contient que des informations d’identification que le serveur de boîtes aux lettres utilise pour authentifier les serveurs de transport Edge abonnés. Sur les serveurs de transport Edge, cet attribut contient les informations d’identification de chaque serveur de transport de boîtes aux lettres dans le site Active Directory abonné qui participe à la synchronisation EdgeSync. Cet attribut n’est présent que sur les serveurs de boîtes aux lettres exécutant la synchronisation EdgeSync et sur les serveurs de transport Edge abonnés.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>Utilisé pour l’arbitrage entre les serveurs de boîtes aux lettres lorsque plusieurs serveurs de boîtes aux lettres tentent d’opérer une réplication sur le même serveur de transport Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Uniquement présent dans AD LDS sur l’objet serveur de transport Edge. Cet attribut suit l’état de la réplication sur une instance AD LDS et inclut des informations sur la réplication.</p></td>
</tr>
</tbody>
</table>


Retour au début

## informations de configuration ;

Lorsque vous abonnez un serveur de transport Edge à une organisation, vous pouvez gérer les objets de configuration communs au serveur et à l’organisation Exchange à partir de cette dernière. Ces modifications sont ensuite répliquées vers le serveur de transport Edge à l’aide d’EdgeSync. Ce processus permet de maintenir une configuration cohérente sur tous les serveurs impliqués dans le traitement de message.

Un sous-ensemble des données de configuration pour l’organisation Exchange doit également être maintenu sur le serveur de transport Edge. Lors de la synchronisation EdgeSync, les données de configuration dont le serveur de transport Edge a besoin sont écrites dans la partition de configuration d’AD LDS. Les données de configuration écrites sur AD LDS sont les suivantes :

  - **Serveurs de boîtes aux lettres**   Le nom de domaine complet (FQDN) de chaque serveur de boîtes aux lettres du site Active Directory abonné est mis à la disposition de la banque AD LDS locale sur le serveur de transport Edge. Ces informations permettent de générer une liste de serveurs hôtes actifs pour le connecteur d’envoi des messages entrants.

  - **Domaines acceptés**   Tous les domaines faisant autorité, de relais interne et de relais externe configurés pour l’organisation Exchange sont écrits sur AD LDS. Le fait que les domaines acceptés soient accessibles au serveur de transport Edge permet à l’organisation Exchange d’effectuer un filtrage des domaines et de rejeter le trafic SMTP non valide entrant le plus rapidement possible. Pour plus d’informations sur les domaines acceptés, voir [Domaines acceptés](accepted-domains-exchange-2013-help.md).

  - **Classifications des messages**   Si des classifications des messages sont disponibles sur le serveur de transport Edge, les agents de transport et la conversion de contenu peuvent agir sur les classifications des messages dans le réseau de périmètre. Par exemple, l’agent de filtrage de pièces jointe peut appliquer la classification Pièce jointe supprimée lors de la suppression d’une pièce jointe, ce qui envoie un texte d’information à un utilisateur Microsoft Outlook ou un utilisateur Outlook Web App pour l’informer de ce qui s’est produit. Les agents développés pour un usage par des applications tierces peuvent utiliser les classifications des messages d’une façon similaire.

  - **Domaines distants**   Toutes les entrées de domaine distant configurées pour l’organisation Exchange sont écrites sur AD LDS. Les entrées de domaine distant contrôlent les paramètres de message d’absence du bureau et les paramètres de format de message pour un domaine distant. Pour plus d’informations sur les domaines distants, voir [Domaines distants](remote-domains-exchange-2013-help.md).

  - **Connecteurs d’envoi**   Par défaut, la création d’un abonnement Edge crée automatiquement les connecteurs d’envoi obligatoires pour activer le flux de messagerie de bout en bout entre l’organisation Exchange et Internet, lors de l’abonnement du serveur de transport Edge. Tous les connecteurs d’envoi existants sur le serveur de transport Edge sont supprimés. Si vous voulez configurer des connecteurs d’envoi supplémentaires, configurez le connecteur d’envoi à l’intérieur de l’organisation Exchange et sélectionnez l’abonnement Edge comme serveur source pour le connecteur. Pour plus d’informations, voir [Abonnements Edge](edge-subscriptions-exchange-2013-help.md).

  - **Serveurs SMTP internes**   La valeur de l’attribut *InternalSMTPServers* est stockée dans l’objet **TransportConfig** pour l’organisation Exchange et le serveur de transport Edge local. Lors de la synchronisation EdgeSync, la valeur stockée sur l’objet serveur de transport Edge local est remplacée par la valeur stockée sur cet objet pour l’organisation Exchange. Cet attribut spécifie une liste d’adresses IP de serveur SMTP interne ou des plages d’adresses IP qui doivent être ignorées par l’ID de l’expéditeur et le filtrage des connexions.

  - **Listes des domaines sécurisés**   Les attributs *TLSReceiveDomainSecureList* et *TLSSendDomainSecureList* sont stockés sur l’objet **TransportConfig** pour l’organisation Exchange et le serveur de transport Edge local. Lors de la synchronisation EdgeSync, la valeur stockée sur l’objet serveur de transport Edge local est remplacée par la valeur stockée sur cet objet pour l’organisation Exchange. Ces attributs spécifient la liste des domaines distants configurés pour l’authentification TLS mutuelle.

Retour au début

## informations sur le destinataire ;

Les informations sur le destinataire répliquées vers AD LDS incluent uniquement un sous-ensemble des attributs de destinataire. Seules les données requises par le transport Edge pour exécuter certaines tâches de blocage du courrier indésirable sont répliquées. Les informations sur le destinataire répliquées vers AD LDS comprennent :

  - **Destinataires   **La liste des destinataires dans l’organisation Exchange est répliquée vers AD LDS. Chaque destinataire est identifié par le GUID Active Directory qui lui est attribué. Si vous configurez le compte d’un destinataire pour refuser la réception du courrier extérieur à l’organisation, ce destinataire n’est pas répliqué vers AD LDS. Si vous désactivez ou supprimez la boîte aux lettres d’un destinataire, celle-ci n’est plus répliquée vers AD LDS.

  - **Adresses proxy**   Toutes les adresses proxy affectées à chaque destinataire sont répliquées vers AD LDS sous la forme de données hachées. Il s’agit d’un hachage unidirectionnel utilisant l’algorithme SHA (Secure Hash Algorithm)-256. L’algorithme SHA-256 génère un message de 256 bits résumant les données originales. Le stockage d’adresses proxy sous la forme de données hachées permet de sécuriser ces informations en cas d’endommagement du serveur de transport Edge ou d’AD-LDS. Les adresses proxy sont référencées lorsque le serveur de transport Edge effectue la tâche de blocage du courrier indésirable de recherche de destinataire.

  - **Liste des expéditeurs approuvés, des expéditeurs bloqués et des destinataires approuvés**   Les listes des expéditeurs approuvés, des expéditeurs bloqués et des destinataires approuvés qui sont définies dans l’instance Outlook de chaque destinataire sont regroupées et répliquées vers AD LDS. Ces paramètres sont stockés dans la base de données de boîtes aux lettres où se trouve la boîte aux lettres du destinataire. La collection de listes fiables d’un utilisateur Outlook correspond aux données combinées provenant de la liste des expéditeurs approuvés, de la liste des destinataires approuvés, de la liste des expéditeurs bloqués et des contacts externes de l’utilisateur. Le fait que des données de collection de listes fiables soient disponibles dans AD LDS permet au serveur de transport Edge de filtrer correctement les expéditeurs, réduisant ainsi les coûts fixes d’exploitation pour le filtrage des messages. Ces informations sont envoyées sous la forme de données hachées.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Bien que les données des destinataires approuvés soient stockées dans Outlook et puissent être regroupées en une collection de listes fiables sur l’instance AD LDS sur le serveur de transport Edge, la fonctionnalité de filtrage du contenu n’agit pas sur les données des destinataires approuvés.</td>
    </tr>
    </tbody>
    </table>


  - **Paramètres de blocage du courrier indésirable par destinataire**   Vous pouvez utiliser la cmdlet **Set-Mailbox** pour attribuer des paramètres de seuil de blocage du courrier indésirable par destinataire qui diffèrent des paramètres de blocage du courrier indésirable à l’échelle de l’organisation. Si vous configurez des paramètres de blocage du courrier indésirable par destinataire, ces derniers remplacent les paramètres utilisés à l’échelle de l’organisation. La réplication de ces paramètres vers AD LDS permet de prendre en considération les paramètres de destinataire avant de relayer le message à l’organisation Exchange. Ces informations sont envoyées sous la forme de données hachées.

Retour au début

## informations de topologie.

Les informations de topologie incluent la notification des nouveaux serveurs de transport Edge inscrits ou des abonnements Edge supprimés. Ces données sont actualisées toutes les cinq minutes.

Retour au début

