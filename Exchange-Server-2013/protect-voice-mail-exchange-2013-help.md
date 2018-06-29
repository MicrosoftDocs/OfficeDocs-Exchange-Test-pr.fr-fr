---
title: 'Protéger la messagerie vocale: Exchange 2013 Help'
TOCTitle: Protéger la messagerie vocale
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52057134
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Protéger la messagerie vocale

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2016-12-09_

Certains systèmes téléphoniques PBX (Private Branch eXchange) et PBX IP existants permettent à l'appelant de marquer un message vocal comme privé, empêchant ainsi le destinataire de le transférer à un tiers. Dans les systèmes de messagerie vocale intégrés, il est possible d'accéder à un message vocal de plusieurs façons, ce qui rend délicate la tâche d'empêcher que les messages marqués comme étant privés soient écoutés par un tiers à qui ils ne sont pas destinés.

La messagerie unifiée peut être configurée de manière utiliser Active Directory Rights Management Services (AD RMS) pour protéger les messages vocaux d'une organisation. Cette fonctionnalité est appelée Messagerie vocale protégée.

Quand un message vocal est protégé, le destinataire ne peut non seulement pas le transférer, mais la messagerie unifiée garantit également que seuls le ou les destinataires peuvent accéder à son contenu. Il est possible d'accéder à des messages vocaux protégés par le biais de MicrosoftOutlook 2010 ou une version ultérieure, Outlook Web App ou Outlook Voice Access.

**Contenu de cette rubrique**

Overview of Protected Voice Mail

Overview of Active Directory Rights Management Services

Client support and end-user features

Protected voice mail structure

Composing a Protected Voice Mail message

UM mailbox policies

Text message notifications and Protected Voice Mail

## Présentation de la fonction Messagerie vocale protégé

La fonctionnalité de messagerie vocale protégée est disponible dans Exchange 2010 et les versions ultérieures de la messagerie unifiée. Elle peut être configurée sur une stratégie de boîte aux lettres de messagerie unifiée, et tous les paramètres de la messagerie vocale protégée peuvent être configurés via la console de gestion Exchange, l'environnement de ligne de commande Exchange Management Shell dans Exchange 2010 ou à l'aide du Centre d'administration Exchange (CAE) ou des cmdlets de l'environnement de ligne de commande Exchange Management Shell dans Exchange 2013.

La fonction Messagerie vocale protégée est implémentée par l'application de la gestion des droits relatifs à l'information (IRM) aux messages vocaux. Lorsque les messages vocaux sont protégés par la messagerie unifiée :

  - Les utilisateurs peuvent répondre aux messages vocaux protégés.

  - Les destinataires d'un message vocal ne peuvent pas le transférer.

  - Les utilisateurs ne peuvent pas enregistrer une copie du message vocal.

  - Les utilisateurs ne peuvent pas enregistrer ou copier les données audio jointes au message vocal.

  - Un message vocal ne peut être ouvert que par son ou ses destinataires.

Tant les messages vocaux de répondeur automatique que les messages vocaux interpersonnels (messages vocaux envoyés à un utilisateur via Outlook Voice Access) peuvent être protégés par la messagerie unifiée. Toutefois, les types de messages suivants ne seront pas protégés :

  - Messages de télécopie.

  - Messages non vocaux. Par exemple, les messages électroniques ou les demandes de réunion, même s'ils sont créés via Outlook Voice Access (réponses vocales).

Retour au début

## Présentation d'Active Directory Rights Management Services

AD RMS, un composant de Windows Server 2008 et des versions ultérieures, permet de protéger les fichiers de manière à ce que ceux-ci ne soient lus que par les destinataires choisis par l'expéditeur. AD RMS permet de protéger un fichier en spécifiant les droits dont doit disposer un utilisateur pour y accéder. Il est possible de configurer ces droits pour que l'utilisateur puisse ouvrir, modifier, imprimer, transférer ou traiter les informations d'une autre manière grâce à la gestion des droits. Avec AD RMS, vous pouvez sécuriser vos données lorsqu'elles sont distribuées hors de votre réseau.

Un système AD RMS dispose d'un composant serveur et d'un composant client, qui contiennent les éléments suivants :

  - Un serveur qui a Windows Server 2008 R2 ou une version ultérieure installée qui exécute le rôle de serveur RMS Active Directory, qui gère les certificats et les licences.

  - Un serveur de base de données.

  - Le client AD RMS. La dernière version du client AD RMS est incluse dans les systèmes d'exploitation Windows 7 et Windows 8.

Le composant serveur est constitué de plusieurs services web exécutés sur un serveur Microsoft, tel que Windows Server 2008 ou une version ultérieure. Le composant client peut être exécuté sur le système d'exploitation client ou serveur et comprend des fonctions qui permettent d'activer une application destinée à chiffrer et déchiffrer les contenus, à récupérer des modèles et des listes de révocation et à acquérir des licences et des certificats sur un serveur.

À l’aide de AD RMS et le client AD RMS, vous pouvez augmenter la stratégie de sécurité d’une organisation en protégeant les informations via des stratégies d’utilisation persistantes qui restent avec les informations, quel que soit l’endroit où il est déplacé. Vous pouvez utiliser AD RMS pour éviter que des informations sensibles, telles que les rapports financiers, des spécifications de produit, des données client et confidentielles e-mail et messagerie de messages vocaux, par accident ou intentionnellement tombent entre de mauvaises mains. Pour plus d’informations, consultez [Vue d’ensemble de AD RMS](https://go.microsoft.com/fwlink/p/?linkid=199436).

Dans la messagerie unifiée Exchange, vous pouvez utiliser les fonctionnalités de Gestion des droit relatifs à l'information (IRM) pour appliquer une protection permanente aux messages et pièces jointes.

Avec les fonctionnalités IRM et de messagerie vocale protégée, votre organisation et vos utilisateurs sont à même de contrôler les droits octroyés aux destinataires en ce qui concerne l'accès aux messages vocaux et électroniques. La gestion des droits relatifs à l'information peut être également utilisée pour autoriser ou restreindre les actions des destinataires, comme le transfert d'un message à d'autres destinataires, l'impression d'un message ou d'une pièce jointe ou l'extraction du contenu d'un message ou d'une pièce jointe par une opération copier-coller.

## Configuration requise pour la Gestion des droits relatifs à l'information (IRM)

Avant de pouvoir implémenter IRM dans Exchange, vous devez tout d’abord déployer et configurer votre infrastructure AD RMS. Pour plus d’informations, consultez [Services AD RMS (Active Directory Rights Management Services) de](https://go.microsoft.com/fwlink/p/?linkid=199439). Pour implémenter la technologie IRM pour prendre en charge de la messagerie vocale protégé dans votre organisation Exchange, votre déploiement doit remplir les conditions suivantes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Serveur</th>
<th>Conditions requises</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster AD RMS</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard ou Enterprise avec SP1 ou Windows Server 2012 Standard ou Datacenter. Pour plus d'informations sur la configuration système requise, consultez la rubrique <a href="exchange-2013-system-requirements-exchange-2013-help.md">Configuration requise pour Exchange 2013</a>.</p></li>
<li><p><strong>Point de connexion de service (SCP)</strong>   Exchange 2013 et les applications compatibles AD RMS utilisent le point de connexion de service enregistré dans Active Directory pour détecter les clusters AD RMS et les URL. AD RMS vous permet d'enregistrer le point de connexion de service dans le programme d'installation d'AD RMS. Si le compte utilisé pour installer AD RMS n'est pas membre du groupe de sécurité Administrateurs d'entreprise, il est possible d'effectuer l'enregistrement du point de connexion de service après l'installation. La forêt Active Directory comporte un seul point de connexion de service pour AD RMS.</p></li>
<li><p><strong>Autorisations</strong>   Les serveurs du groupe de serveurs Exchange ou les serveurs Exchange individuels doivent recevoir les autorisations de lecture et d'exécution sur le pipeline de certification du serveur AD RMS. Sur des serveurs AD RMS, le chemin d'accès par défaut est \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx.</p></li>
<li><p><strong>Super utilisateurs AD RMS</strong>   Pour activer le déchiffrement du transport, le déchiffrement d'états de journal, la Gestion des droits relatifs à l'information dans Outlook Web App et pour la recherche Exchange, vous devez ajouter la boîte aux lettres de remise fédérée (une boîte aux lettres système créée par le programme d'installation d'Exchange) au groupe des super utilisateurs AD RMS sur le cluster AD RMS. Pour plus d'informations, consultez <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Ajouter la boîte aux lettres de fédération au groupe de super utilisateurs AD RMS</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Configuration et test de la Gestion des droits relatifs à l'information (IRM)

Vous devez utiliser l'environnement de ligne de commande Exchange Management Shell pour configurer les fonctionnalités IRM. Pour configurer les fonctionnalités IRM individuelles, utilisez la cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979792\(v=exchg.150\)). Pour plus d'informations sur la configuration des fonctionnalités IRM, consultez la rubrique [Procédures de gestion des droits relatifs à l’information](information-rights-management-procedures-exchange-2013-help.md).

Après avoir configuré un serveur Exchange, vous pouvez utiliser la cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/fr-fr/library/dd979798\(v=exchg.150\)) pour tester de bout en bout votre déploiement IRM. Cette cmdlet vérifie la configuration IRM d'une organisation et doit être exécutée préalablement à l'activation de la fonction Messagerie vocale protégée. La cmdlet **Test-IRMConfiguration** exécute les tests suivants :

  - Elle inspecte la configuration IRM de votre organisation Exchange.

  - Elle contrôle les informations relatives à la version et aux correctifs du serveur AD RMS.

  - Elle vérifie s'il est possible d'activer un serveur Exchange pour RMS en récupérant le certificat de compte de droits et le certificat de licence client (CLC).

  - Elle acquiert des modèles de stratégie de droits AD RMS à partir du serveur AD RMS.

  - Elle vérifie que l'expéditeur spécifié peut envoyer des messages protégés par IRM.

  - Elle récupère une licence d'utilisation de super utilisateur pour le destinataire spécifié.

  - Elle acquiert une pré-licence pour le destinataire spécifié.

Retour au début

## Prise en charge des clients et fonctionnalités destinées aux utilisateurs finaux

Le logiciel client de messagerie utilisé pour écouter un message vocal protégé doit prendre en charge IRM et pouvoir lire un message vocal protégé par messagerie unifiée. Les clients de messagerie pris en charge sont les suivants : MicrosoftOutlook 2010 ou une version ultérieure, Outlook Web App et Outlook Voice Access. Le tableau suivant contient la liste des clients de messagerie et indique s'ils sont pris en charge ou non.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Client de messagerie</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Les messages vocaux protégés sont pris en charge dans Outlook 2010 et les versions ultérieures.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App dans Exchange 2010 ou les versions ultérieures prend en charge les messages vocaux protégés. Les versions antérieures d'Outlook Web App, appelé Outlook Web Access, ne les prennent pas en charge.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Outlook Voice Access dans Exchange 2010 et les versions ultérieures prend en charge la messagerie vocale protégée. La version d'Outlook Voice Access incluse dans Exchange 2007 ne prend pas en charge la fonction Messagerie vocale protégée.</p></li>
<li><p>La boîte aux lettres de l'utilisateur doit se trouver sur un serveur de boîtes aux lettres dans Exchange 2010 ou une version ultérieure.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile ou Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile ne prend pas en charge la messagerie vocale protégée. En revanche, Windows Phone 7 et Windows Phone 8 prennent en charge la messagerie vocale protégée.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Exchange 2010 SP1 et les versions ultérieures prennent en charge la messagerie vocale protégée.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Autres clients de messagerie</p></td>
<td><ul>
<li><p>La fonction Messagerie vocale protégée n'est pas prise en charge.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Retour au début

## Structure des messages vocaux protégés

Deux messages sont en fait impliqués pour chaque message protégé. Le premier message est le message externe, qui n'est pas chiffré. Il contient une pièce jointe nommée message.rpmsg, qui renferme le message vocal protégé par IRM et les données de contrôle de gestion des droits internes. Les données de contrôle de gestion des droits contiennent une clé de contenu et des informations relatives aux droits qui spécifient les personnes pouvant accéder au message vocal et de quelle manière.

Les messages vocaux protégés sont affichés dans la boîte de réception de l'utilisateur dans le dossier de recherche de la **Messagerie vocale**. L'utilisateur peut écouter les messages vocaux par le biais du lecteur audio intégré, tout comme il écouterait un message vocal ordinaire, sauf que le bouton Transférer est désactivé et qu'une notification apparaîtra en haut du message indiquant qu'il est protégé et ne peut être transféré.

Pour les clients de messagerie qui ne prennent pas en charge la messagerie vocale protégée, le corps du message externe est simplement affiché. Les administrateurs peuvent inclure un texte lorsque le logiciel du client ne prend pas en charge la messagerie vocale protégée à l’aide de stratégies de boîte aux lettres de messagerie unifiée. Vous pouvez personnaliser le texte par défaut inclus dans le message électronique en configurant une stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez par exemple configurer une stratégie de boîte aux lettres de messagerie unifiée avec un texte du type : *« Vous ne pouvez ouvrir ce message vocal car il est protégé. Pour afficher ou écouter ce message, connectez-vous à votre boîte aux lettres sur https://mail.contoso.com ou appelez le +1 (425) 555-1234 pour accéder à Outlook Voice Access. »*

Retour au début

## Création d'un message vocal protégé

Il existe deux cas dans lesquels il est possible de créer des messages vocaux protégés :

  - **Répondeur automatique**   Le répondeur se met en marche quand une personne appelle un utilisateur à extension messagerie unifiée, mais que cet utilisateur ne répond pas ou qu'il transmet l'appel directement à la messagerie vocale. Dans les scénarios de répondeur automatique, le système de messagerie vocale lit une série d'invites vocales après que l'appelant a enregistré un message vocal.
    
    L'appelant peut alors choisir parmi plusieurs options de message, notamment celle de marquer le message comme étant un message privé en appuyant sur la touche dièse (\#). Si l'appelant appuie sur la touche \#, il peut suivre les instructions de la messagerie unifiée pour marquer le message comme étant privé, supprimer cette option pour le message ou indiquer qu'il s'agit d'un message important. Le diagramme suivant montre les options du menu à disposition des appelants qui souhaitent laisser un message vocal privé à leur interlocuteur.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Pour les appels arrivant sur le répondeur automatique, la messagerie unifiée utilise les paramètres de la messagerie vocale protégée de la stratégie de boîte aux lettres de messagerie unifiée du destinataire du message, car l'appelant n'est pas authentifié.</td>
    </tr>
    </tbody>
    </table>
    
    **Création d'un message vocal protégé à l'aide du répondeur automatique**
    
    ![Créer des messages vocaux protégés à l’aide du répondeur automatique](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "Créer des messages vocaux protégés à l’aide du répondeur automatique")  

  - **Outlook Voice Access**   Outlook Voice Access permet aux utilisateurs à extension messagerie unifiée d'accéder à leur boîte aux lettres à partir de téléphones analogiques, numériques ou cellulaires en composant leur numéro Outlook Voice Access. Les utilisateurs à extension messagerie unifiée peuvent accéder à deux interfaces utilisateur de messagerie unifiée : l'interface utilisateur téléphonique et l'interface utilisateur vocale.
    
    Les utilisateurs d'Outlook Voice Access peuvent rechercher leurs contacts dans le répertoire et leur envoyer des messages vocaux. Si la fonction Messagerie vocale protégée a été activée pour les destinataires utilisateurs de messagerie unifiée, les appelants peuvent marquer les messages comme étant privés après les avoir enregistrés. Les administrateurs peuvent également configurer une stratégie de boîte aux lettres de messagerie unifiée pour s'assurer que tous les messages vocaux envoyés par des utilisateurs authentifiés sont protégés par la messagerie unifiée.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Si un appelant est authentifié, les paramètres de messagerie vocale protégée sur la stratégie de boîte aux lettres de messagerie unifiée qui est liée à l’appelant sont appliqués, indépendamment des paramètres de stratégie de boîte aux lettres de messagerie unifiée pour le destinataire prévu du message vocal.</td>
    </tr>
    </tbody>
    </table>
    
    **Créer un message protégé à l'aide de l'interface utilisateur vocale**
    
    ![Créer des messages vocaux protégés à l’aide de l’interface vocale](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "Créer des messages vocaux protégés à l’aide de l’interface vocale")  
    
    **Créer un message protégé à l'aide de l'interface utilisateur de téléphonie**
    
    ![Créer la messagerie vocale protégée à l’aide des entrées à tonalité](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "Créer la messagerie vocale protégée à l’aide des entrées à tonalité")  

Retour au début

## Stratégies de boîte aux lettres de messagerie unifiée

Vous pouvez créer une stratégie de boîte aux lettres de messagerie unifiée pour appliquer un jeu commun de paramètres de stratégie de messagerie unifiée, par exemple, des paramètres de stratégie de code confidentiel, des restrictions d'appel et des paramètres de messagerie vocale protégée, à une série de boîtes aux lettres à extension messagerie unifiée. Pour plus d'informations sur les stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md).

Vous pouvez configurer les options de la messagerie vocale protégée via le Centre d'administration Exchange (CAE) ou la cmdlet **Set-UMMailboxPolicy** dans l'environnement de ligne de commande Exchange Management Shell. Le tableau suivant recense les paramètres permettant de configurer la fonction Messagerie vocale protégée.

**Paramètres de messagerie vocale protégée**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre de l'environnement de ligne de commande Exchange Management Shell</th>
<th>Quels sont les paramètres disponibles dans le CAE ?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>ProtectAuthenticatedVoiceMail</em> permet de spécifier si les utilisateurs à extension messagerie unifiée peuvent envoyer des messages vocaux protégés quand ils accèdent à leur boîte aux lettres via Outlook Voice Access. Le paramètre par défaut est <code>None</code>. Cela signifie qu'aucune protection n'est appliquée lors de la création des messages vocaux et que les appelants ne peuvent pas marquer leurs messages comme étant privés. Si la valeur est définie sur <code>Private</code>, seuls les messages marqués comme étant privés par l'appelant seront protégés. Si la valeur est définie sur <code>All</code>, tous les messages vocaux seront protégés, quelle que soit l'option choisie par l'appelant.</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>ProtectUnauthenticatedVoiceMail</em> spécifie si les serveurs de boîtes aux lettres qui répondent aux appels destinés aux utilisateurs à extension messagerie unifiée associés à une stratégie de boîte aux lettres de messagerie unifiée créent des messages vocaux protégés. Ce paramètre s'applique aussi lorsqu'un message est envoyé depuis un standard automatique de messagerie unifiée à un utilisateur de messagerie unifiée. Le paramètre par défaut est <code>None</code>. Cela signifie qu'aucune protection n'est appliquée aux messages vocaux et que l'appelant ne pourra pas marquer son message comme étant privé. Si la valeur est définie sur <code>Private</code>, seuls les messages marqués comme étant privés par l'appelant seront protégés. Si la valeur est définie sur <code>All</code>, tous les messages vocaux seront protégés, que l'appelant ait marqué son message comme étant privé ou non.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>ProtectedVoiceMailText</em> permet de spécifier le texte à inclure dans le corps du message externe d'un message vocal protégé. Ce texte est affiché dans tous les clients de messagerie qui ne prennent pas en charge les messages vocaux protégés. Veuillez noter que la messagerie unifiée fournit toujours un texte par défaut lorsque cette propriété est configurée sur <code>Null</code> ou qu'elle n'est pas renseignée.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>RequireProtectedPlayOnPhone</em> permet de spécifier si les utilisateurs associés à la stratégie de boîte aux lettres de messagerie unifiée doivent écouter leurs messages vocaux protégés par le biais du téléphone (par le biais de la fonction Émettre au téléphone). La valeur par défaut est <code>$false.</code>. Lorsque cette valeur est configurée sur <code>$true</code>, le lecteur audio intégré aux formulaires de messagerie vocale protégée dans Outlook ou Outlook Web App est désactivé. Veuillez noter qu'il est toujours possible d'accéder à la fonction Aperçu du message vocal. L'utilisateur ne peux lire le fichier audio ni avec le lecteur intégré ni avec tout autre lecteur afin d'écouter le message vocal.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>Oui</p></td>
<td><p>Le paramètre <em>AllowVoiceResponseToOtherMessageTypes</em> permet de spécifier si les appelants authentifiés pour accéder à leur courrier électronique via Outlook Voice Access sont autorisés à composer une réponse vocale aux messages électroniques et aux demandes de réunion.</p></td>
</tr>
</tbody>
</table>


Pour plus d'informations sur la gestion des paramètres de messagerie vocale protégée, consultez la rubrique [Procédures de la messagerie vocale protégées](protected-voice-mail-procedures-exchange-2013-help.md) ou [Set-UMMailboxPolicy](https://technet.microsoft.com/fr-fr/library/bb124903\(v=exchg.150\)).

Retour au début

## Notifications par message texte et messagerie vocale protégée

Les utilisateurs qui configurent leur compte de messagerie unifiée pour envoyer des notifications par message texte (appelés également notifications par SMS) à leur téléphone mobile quand ils reçoivent des messages vocaux, recevront aussi une transcription du message vocal (Aperçu de messagerie vocale) dans le corps du message texte. Ceci représente toutefois un problème de sécurité car le contenu des messages vocaux devrait tout le temps être protégé.

Lorsque la messagerie unifiée crée des messages de notification pour un message vocal protégé, elle vérifie d'abord si le message vocal est marqué comme étant privé. Si c'est le cas, elle n'ajoutera pas la transcription du texte audio au message envoyé au téléphone cellulaire. Au lieu de cela, le texte suivant sera inclus dans le texte du message : « Utilisez Outlook Voice Access pour accéder à ce message vocal protégé. »

Retour au début

