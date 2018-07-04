---
title: 'Configuration des télécopies entrantes: Exchange 2013 Help'
TOCTitle: Configuration des télécopies entrantes
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52057081
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration des télécopies entrantes

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La messagerie unifiée Exchange Microsoft repose sur des solutions de partenaires de télécopie agréés pour des fonctionnalités de télécopie améliorées, telles que la télécopie sortante ou le routage de télécopie. Par défaut, les serveurs Exchange ne sont pas configurés pour autoriser la remise des télécopies entrantes à un utilisateur activé pour la messagerie unifiée. Au lieu de cela, un serveur Exchange redirige les appels de télécopie entrants vers une solution de partenaire de télécopie agréé. Le serveur du partenaire de télécopie reçoit les données de télécopie et les envoie à la boîte aux lettres de l’utilisateur dans un message électronique avec la télécopie incluse en tant que pièce jointe .tif.

Pour plus d'informations sur les partenaires de télécopie, consultez la rubrique [Microsoft Pinpoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238).

## Déploiement et configuration de la télécopie

La messagerie unifiée transfère les appels de télécopie entrants à une solution partenaire de télécopie dédiée qui établit ensuite l'appel de télécopie avec l'expéditeur de télécopie et la reçoit de la part de l'utilisateur à extension messagerie unifiée. Toutefois, pour permettre aux utilisateurs à extension messagerie unifiée de recevoir des télécopies dans leur boîte aux lettres, vous devez d’abord activer la télécopie entrante et définir l’URI du partenaire de télécopie sur la stratégie de boîte aux lettres de messagerie unifiée qui est liée à l’utilisateur ou aux utilisateurs à extension messagerie unifiée. Vous pouvez autoriser ou empêcher la télécopie entrante pour des plans de numérotation de messagerie unifiée, des stratégies de boîte aux lettres de messagerie unifiée et la boîte aux lettres d'un utilisateur à extension messagerie unifiée. Pour plus de détails, consultez les rubriques suivantes :

  - [Autoriser les utilisateurs dans le même plan de numérotation pour recevoir des télécopies](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [Empêcher les utilisateurs dans le même plan de numérotation à partir de la réception de télécopies](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [Activer l’envoi de télécopies pour un groupe d’utilisateurs](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Désactiver pour un groupe d’utilisateurs de télécopie](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Permettent aux utilisateurs de recevoir des télécopies](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [Empêcher un utilisateur de recevoir des télécopies](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## Étape 1 : Déploiement de la messagerie unifiée

Avant de configurer la télécopie pour votre organisation locale ou hybride, vous devez déployer des serveurs d'accès au client et de boîtes aux lettres, puis configurer vos passerelles VoIP pour autoriser la télécopie. Pour plus d'informations sur le déploiement de la messagerie unifiée, consultez la rubrique [Déploiement de la messagerie unifiée Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md). Pour plus de détails sur le déploiement de passerelles VoIP et de PBX, consultez la rubrique [Connecter la messagerie unifiée pour votre système téléphonique](connect-um-to-your-telephone-system-exchange-2013-help.md).

> [!NOTE]
> L'envoi et la réception de télécopies à l'aide de T.38 ou G.711 ne sont pas pris en charge dans un environnement où la messagerie unifiée et MicrosoftOffice Communications Server 2007 R2 ou Microsoft Lync Server sont intégrés.


## Étape 2 : Configuration des serveurs de partenaire de télécopie

Ensuite, vous devez activer la télécopie entrante et configurer les URI du partenaire de télécopie sur chaque stratégie de boîte aux lettres de messagerie unifiée dont vous avez besoin dans votre organisation. Pour déployer la télécopie entrante, vous devez intégrer une solution de partenaire de télécopie agréé avec la messagerie unifiée Exchange. Pour plus d'informations, consultez la rubrique [Gestionnaire de télécopies pour la messagerie unifiée Exchange](fax-advisor-for-exchange-um-exchange-2013-help.md). Pour obtenir la liste des partenaires de télécopie agréés, consultez la rubrique [Microsoft Pinpoint pour les partenaires de télécopie](https://go.microsoft.com/fwlink/?linkid=190238)

> [!NOTE]
> Comme le serveur du partenaire de télécopie est en dehors de votre organisation, les ports de pare-feu doivent être configurés pour autoriser les ports en protocole T.38 qui activent la télécopie sur un réseau IP. Par défaut, le protocole T.38 utilise le port TCP 6004. Il peut également utiliser le port UDP (User Datagram Protocol) 6044, mais cela dépend du fabricant du matériel. Les ports de pare-feu doivent être configurés pour autoriser les données de télécopie qui utilisent les ports TCP ou UDP, ou les plages de ports définies par le fabricant.


## Étape 3 : Activation de la télécopie sur la messagerie unifiée

Trois composants doivent être configurés correctement pour que les utilisateurs puissent recevoir des télécopies via la messagerie unifiée :

  - Plans de numérotation de messagerie unifiée

  - Stratégies de boîte aux lettres de messagerie unifiée

  - Boîtes aux lettres de messagerie unifiée

La télécopie peut être activée ou désactivée sur les plans de numérotation de messagerie unifiée, les stratégies de boîte aux lettres de messagerie unifiée ou la boîte aux lettres d'un utilisateur à extension messagerie unifiée. Les stratégies de boîte aux lettres de messagerie unifiée peuvent être activées ou désactivées pour la télécopie à l'aide du Centre d'administration Exchange (CAE) ou de l'environnement de ligne de commande Exchange. L'activation et la désactivation de plans de numérotation et d'utilisateurs à extension messagerie unifiée doit se faire à l'aide de l'environnement de ligne de commande Exchange Management Shell. Le tableau suivant présente les options disponibles, ainsi que les cmdlets et paramètres utilisés pour l'activation et la désactivation de la télécopie


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Composant de messagerie unifiée</th>
<th>Activer/désactiver à l'aide du CAE ?</th>
<th>Exemple d'utilisation de l'environnement de ligne de commande pour activer la télécopie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plan de numérotation</p></td>
<td><p>Non</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>Stratégie de boîte aux lettres de messagerie unifiée</p></td>
<td><p>Oui</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Utilisateur à extension messagerie unifiée</p></td>
<td><p>Non</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


Par défaut, bien que le plan de numérotation de messagerie unifiée et la boîte aux lettres de l'utilisateur autorisent les télécopies entrantes, vous devez d'abord autoriser l'envoi des télécopies entrantes dans la stratégie de boîte aux lettres de messagerie unifiée attribuée à l'utilisateur à extension messagerie unifiée, puis entrer l'URI du serveur de partenaire de télécopie.

Pour permettre à des utilisateurs à extension messagerie unifiée de recevoir des télécopies, procédez comme suit :

  - Vérifiez que chaque plan de numérotation de messagerie unifiée permet aux utilisateurs associés au plan de numérotation de recevoir des télécopies. Par défaut, tous les utilisateurs associés à un plan de numérotation peuvent recevoir des télécopies. Pour que les utilisateurs à extension messagerie unifiée reçoivent des messages de télécopie dans leur boîte aux lettres, chaque passerelle VoIP ou PBX IP doit être configuré pour accepter les appels de télécopie entrants. Vous devez également activer la réception des messages de télécopie par les utilisateurs associés au plan de numérotation. Pour plus d'informations sur la manière de permettre ou d'empêcher des utilisateurs associés à un plan de numérotation de recevoir des télécopies, consultez la rubrique [Permettent aux utilisateurs de recevoir des télécopies](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    
    > [!NOTE]
    > Si vous empêchez la réception de messages de télécopie sur un plan de numérotation, aucun utilisateur associé à ce dernier ne peut recevoir de télécopie, même si vous configurez les propriétés d'un utilisateur particulier pour l'autoriser à recevoir des télécopies. L'activation ou la désactivation de la télécopie sur un plan de numérotation de messagerie unifiée prime sur la configuration d'un utilisateur à extension messagerie unifiée individuel.


  - Configurez la stratégie de boîte aux lettres de messagerie unifiée associée à l'utilisateur à extension messagerie unifiée. La stratégie de boîte aux lettres de messagerie unifiée doit être configurée pour autoriser les télécopies entrantes, y compris l'URI de partenaire de télécopie et le nom du serveur du partenaire de télécopie. Le paramètre *FaxServerURI* doit présenter la forme suivante : sip:\<*URI de serveur de télécopie*\>:\<*port*\>;\<*transport*\>, où « URI de serveur de télécopie » est soit un nom de domaine complet (FQDN), soit une adresse IP de serveur de partenaire de télécopie. « Port » est le port sur lequel le serveur de télécopie écoute les appels de télécopie entrants et « transport » est le protocole de transport utilisé pour la télécopie entrante (UDP, TCP ou TLS). Par exemple, vous pouvez configurer une stratégie de boîte aux lettres de messagerie unifiée pour recevoir des télécopies comme suit.
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - Pour plus d'informations, consultez la rubrique [Définir le partenaire de serveur de télécopie URI pour permettre l’envoi de télécopies](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md).
    
    > [!WARNING]
    > Bien que vous puissiez inclure plusieurs entrées dans le format pour l'<em>FaxServerURI</em> en les séparant par des points-virgules, une seule entrée est utilisée. Ce paramètre ne permet d’utiliser qu’une seule entrée et l’ajout de plusieurs entrées ne permet pas d’équilibrer la charge des demandes de télécopie.


  - Vérifiez que la boîte aux lettres à extension messagerie unifiée peut recevoir des messages de télécopie. Par défaut, tous les utilisateurs associés à un plan de numérotation peuvent recevoir des télécopies. Toutefois, il peut arriver que des utilisateurs ne puissent pas recevoir de télécopies en raison de la désactivation de cette option sur leur boîte aux lettres. Pour plus d'informations sur l'activation de la réception des télécopies pour un utilisateur à extension messagerie unifiée, consultez la rubrique [Permettent aux utilisateurs de recevoir des télécopies](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    
    Vous pouvez empêcher un utilisateur associé à un plan de numérotation de recevoir des messages de télécopie. Pour ce faire, configurez les propriétés de l'utilisateur à l'aide de la cmdlet **Set-UMMailbox** dans l'environnement de ligne de commande. Vous pouvez également utiliser la cmdlet **Set-UMMailboxPolicy** pour empêcher plusieurs utilisateurs de recevoir des messages de télécopie. Pour plus d'informations sur la manière d'empêcher un ou plusieurs utilisateurs de recevoir des messages de télécopie, consultez la rubrique [Empêcher un utilisateur de recevoir des télécopies](prevent-a-user-from-receiving-faxes-exchange-2013-help.md).

## Étape 4 : Configuration de l'authentification

En plus de configurer vos plans de numérotation de messagerie unifiée, les stratégies de boîte aux lettres de messagerie unifiée et les utilisateurs à extension messagerie unifiée, vous devez configurer une authentification entre vos serveurs Exchange et le serveur de partenaire de télécopie. Les serveurs Exchange doivent pouvoir authentifier l'origine des messages prétendant provenir du serveur de partenaire de télécopie. Les messages non authentifiés prétendant provenir d’un serveur de partenaire de télécopie ne sont pas traités par un serveur Exchange.

Pour authentifier la connexion du partenaire de télécopie aux serveurs Exchange, vous pouvez utiliser les solutions suivantes :

  - Mutual TLS ;

  - validation de l'ID de l'expéditeur ;

  - connecteur de réception dédié.

Un connecteur de réception devrait suffire pour l'authentification des serveurs de partenaire de télécopie déployés dans votre organisation. Le connecteur de réception veillera à ce que les serveurs Exchange traitent tout le trafic provenant du serveur de partenaire de télécopie comme étant authentifié.

Le connecteur de réception sera configuré sur un serveur Exchange utilisé par le serveur du partenaire de télécopie pour soumettre les messages de télécopie SMTP. Il doit être configuré avec les valeurs suivantes :

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

Pour plus d'informations, consultez la rubrique [Connecteurs](connectors-exchange-2013-help.md).

Si le serveur du partenaire de télécopie envoie du trafic réseau à un serveur Exchange sur un réseau public, par exemple, un serveur de partenaire de télécopie basé sur un service hébergé dans le nuage, nous vous recommandons d’authentifier le serveur du partenaire de télécopie à l’aide d’un contrôle de l’ID de l’expéditeur. Ce type d'authentification garantit que l'adresse IP de provenance du message de télécopie est autorisée à envoyer des messages électroniques de la part du domaine du partenaire de télécopie d'où le message prétend provenir. DNS est utilisé pour stocker les enregistrements d'ID de l'expéditeur (ou les enregistrements SPF), et les partenaires de télécopie doivent publier leurs enregistrements SPF dans la zone de recherche directe DNS. Exchange valide les adresses IP à l'aide d'une requête DNS. Toutefois, l'Agent d'ID de l'expéditeur doit être en cours d'exécution sur un serveur de boîtes aux lettres pour pouvoir exécuter la requête DNS.

Vous pouvez également utiliser TLS pour chiffrer le trafic réseau ou Mutual TLS pour le chiffrement et l'authentification entre le serveur du partenaire de télécopie et les serveurs Exchange.

