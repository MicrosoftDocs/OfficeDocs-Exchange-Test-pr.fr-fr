---
title: 'Préparation d’Active Directory et des domaines: Exchange 2013 Help'
TOCTitle: Préparation d’Active Directory et des domaines
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50479592
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Préparation d’Active Directory et des domaines

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Avant d’installer Microsoft Exchange Server 2013, vous devez préparer votre forêt Active Directory et ses domaines. Exchange doit préparer Active Directory afin de pouvoir stocker des informations sur les boîtes aux lettres de vos utilisateurs et la configuration des serveurs Exchange de l’organisation. Si vous n’êtes pas familier avec les forêts ou les domaines Active Directory, consultez la rubrique [Vue d’ensemble des services de domaine Active Directory](https://go.microsoft.com/fwlink/p/?linkid=399226).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Que vous installiez pour la première fois Exchange dans votre environnement ou que vous possédiez déjà les versions antérieures d’Exchange Server, vous devez préparer Active Directory pour Exchange 2013. Vous pouvez consultez <a href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Modifications apportées au schéma Active Directory d’Exchange 2013</a> pour plus d’informations sur les nouvelles classes de schéma et les attributs ajoutés par Exchange 2013 dans Active Directory, y compris ceux créés par les mises à jour cumulatives (CU) et les Service Packs (SP).</td>
</tr>
</tbody>
</table>


Il existe deux façons de préparer Active Directory pour Exchange. La première consiste à confier la tâche à l'Assistant d'installation Exchange 2013. Si vous n'avez pas un grand déploiement Active Directory et n'avez pas une équipe distincte qui gère Active Directory, nous vous recommandons d'utiliser l'Assistant. Le compte que vous utilisez doit être un membre des groupes de sécurité Administrateurs du schéma et Administrateurs d'entreprise. Pour plus d'informations sur l'utilisation de l'Assistant d'installation, consultez la rubrique [Installer Exchange 2013 à l’aide de l’Assistant Installation](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

Si vous avez un grand déploiement Active Directory ou si une équipe distincte gère Active Directory, cette rubrique vous intéresse. Suivez les étapes de cette rubrique pour mieux contrôler chaque étape de la préparation, et savoir qui peut effectuer chaque étape. Par exemple, les administrateurs Exchange n'ont peut-être pas les autorisations nécessaires pour étendre le schéma Active Directory.

Ce qu'il faut savoir avant de commencer ?

1\. Étendre le schéma Active Directory

2\. Préparer Active Directory

3\. Préparer les domaines Active Directory

Comment savoir si cela a fonctionné ?

Vous voulez savoir ce qui se passe lorsqu’Active Directory est préparé pour Exchange ? Consultez la rubrique [Quels sont les changements constatés dans Active Directory avec l’installation d’Exchange 2013 ?](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer ?

  - Durée d'exécution estimée : 10 à 15 minutes minimum (sans la réplication Active Directory), en fonction de la taille de l'organisation et du nombre de domaines enfants.

  - L'ordinateur que vous utilisez pour exécuter ces étapes doit répondre à la [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md). En outre, votre forêt Active Directory doit répondre aux exigences de la section « Réseau et serveurs d'annuaire » dans [Configuration requise pour Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Si votre organisation dispose de plusieurs domaines Active Directory, nous vous recommandons d'effectuer les opérations suivantes :
    
      - Exécutez les commandes à partir d'un site Active Directory ayant un serveur Active Directory à partir de chaque domaine.
    
      - Installez le premier serveur Exchange dans un site Active Directory avec un serveur de catalogue global accessible en écriture à partir de chaque domaine.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## 1\. Étendre le schéma Active Directory

La première étape pour préparer votre organisation pour Exchange 2013 est d'étendre le schéma Active Directory. Exchange stocke un grand nombre d'informations dans Active Directory mais avant de le faire, il doit ajouter et mettre à jour les classes, les attributs et d'autres éléments. Si vous voulez savoir ce qui a changé lorsque le schéma est étendu, consultez [Modifications apportées au schéma Active Directory d’Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Avant d'étendre le schéma, il y a quelques éléments à garder à l'esprit :

  - Le compte auquel vous êtes connecté doit être un membre des groupes de sécurité Administrateurs du schéma et Administrateurs d'entreprise.

  - L'ordinateur sur lequel vous exécuterez la commande pour étendre le schéma doit être dans les mêmes domaine et site Active Directory que le contrôleur de schéma.

  - Si vous utilisez le paramètre *DomainController*, veillez à utiliser le nom de contrôleur de domaine qui est le contrôleur de schéma.

  - La seule façon d'étendre le schéma pour Exchange est d'utiliser les étapes de cette rubrique ou d'utiliser l'installation de Exchange 2013. Les autres méthodes d'extension du schéma ne sont pas prises en charge.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Si vous n'avez pas une équipe distincte qui gère votre schéma Active Directory, vous pouvez ignorer cette étape et passer directement à Préparer Active Directory. Si le schéma n'est pas étendu à l'étape 1, les commandes de l'étape 2 étendront le schéma pour vous. Si vous décidez d'ignorer l'étape 1, les informations mentionnées ci-dessus que vous devez garder à l'esprit continuent à s'appliquer.</td>
</tr>
</tbody>
</table>


Lorsque vous êtes prêt, effectuez les opérations suivantes pour étendre votre schéma Active Directory. Si vous avez plusieurs forêts Active Directory, assurez-vous que vous êtes connecté à la forêt correcte.

1.  Assurez-vous que l'ordinateur est prêt à exécuter l'installation de Exchange 2013. Pour connaître les conditions requises pour exécuter l'installation, consultez la section [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md) dans [Conditions préalables pour Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Ouvrez une fenêtre d'invite de commande Windows et accédez à l'endroit où vous avez téléchargé les fichiers d'installation Exchange.

3.  Exécutez la commande suivante pour étendre le schéma :
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

Une fois l’extension du schéma terminée, vous devez attendre que Active Directory réplique les modifications apportées à l’ensemble de vos contrôleurs de domaine. Si vous souhaitez vérifier l’état de la réplication, vous pouvez utiliser l’outil `repadmin`. `Repadmin` qui est inclus dans le cadre de la fonction des Outils de service de domaine Active Directory dans Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2. Pour plus d’informations sur son utilisation, consultez la rubrique [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 2\. Préparer Active Directory

Maintenant que le schéma Active Directory a été étendu, vous pouvez préparer d'autres parties de Active Directory pour Exchange 2013. Lors de cette étape, Exchange créera des conteneurs, des objets et d'autres éléments dans Active Directory, qu'il utilisera pour stocker des informations. L'ensemble de tous les conteneurs, objets, attributs Exchange, etc., est appelé l'*organisation Exchange*.

Avant de préparer Active Directory pour Exchange, vous devez garder quelques éléments à l'esprit :

  - Le compte que vous utilisez doit être un membre du groupe de sécurité Administrateurs d'entreprise. Si vous avez ignoré l'étape 1 parce que vous souhaitez que la commande *PrepareAD* étende le schéma, le compte que vous utilisez doit également être un membre du groupe de sécurité Administrateurs du schéma.

  - L'ordinateur sur lequel vous exécuterez la commande doit être dans les mêmes domaine et site Active Directory que le contrôleur de schéma. Il devra également communiquer avec tous les domaines de la forêt sur le port TCP 389.

  - Patientez jusqu'à ce que Active Directory ait répliqué les modifications apportées à l'étape 1 sur tous vos contrôleurs de domaine avant d'effectuer cette étape.

Lorsque vous exécuterez la commande ci-dessous pour préparer Active Directory pour Exchange, vous devrez nommer l'organisation Exchange. Ce nom est utilisé en interne par Exchange et n'est normalement pas visible par les utilisateurs. Le nom de la société où Exchange est installé est souvent utilisé pour le nom de l'organisation. Le nom que vous utilisez n'affectera pas la fonctionnalité de Exchange ou ne déterminera pas ce que vous pouvez utiliser pour les adresses de messagerie. Vous pouvez le nommer comme vous le souhaitez, tant que vous gardez les éléments suivants à l'esprit :

  - Vous pouvez utiliser des lettres majuscules ou minuscules de A à Z.

  - Vous pouvez utiliser des chiffres de 0 à 9.

  - Le nom peut contenir des espaces tant qu'ils ne sont pas au début ou à la fin du nom.

  - Vous pouvez utiliser un trait d'union ou un tiret dans le nom.

  - Le nom peut comporter jusqu'à 64 caractères mais ne peut pas être vide.

  - Le nom ne peut pas être modifié après sa définition.

Lorsque vous êtes prêt, procédez comme suit pour préparer Active Directory pour Exchange. Si le nom de l'organisation contient des espaces, vous devez le mettre entre guillemets (").

1.  Ouvrez une fenêtre d'invite de commande Windows et accédez à l'endroit où vous avez téléchargé les fichiers d'installation Exchange.

2.  Exécutez la commande suivante :
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

Une fois la préparation de Active Directory pour Exchange terminée, vous devrez attendre que Active Directory réplique les modifications apportées à l’ensemble de vos contrôleurs de domaine. Si vous souhaitez vérifier l’état de la réplication, vous pouvez utiliser l’outil `repadmin`. `repadmin` est inclus dans le cadre de la fonction des Outils de service de domaine Active Directory dans Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2. Pour plus d’informations sur l’utilisation de l’outil, consultez la rubrique [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 3\. Préparer les domaines Active Directory

L'étape finale pour préparer Active Directory pour Exchange est de préparer chacun des domaines Active Directory où Exchange sera installé ou bien où se trouveront les utilisateurs à extension messagerie. Cette étape crée des conteneurs et des groupes de sécurité supplémentaires, et définit des autorisations de sorte que Exchange puisse y accéder.

Si vous avez plusieurs domaines dans votre forêt Active Directory, vous disposez de deux choix pour les préparer. Sélectionnez l'option qui correspond à ce que vous souhaitez faire. Si vous avez un seul domaine, vous pouvez ignorer cette étape car la commande *PrepareAD* de l'étape 2 a déjà préparé le domaine pour vous.

## Préparer tous les domaines dans ma forêt Active Directory

Pour préparer tous vos domaines Active Directory, vous pouvez utiliser le paramètre *PrepareAllDomains* lorsque vous exécutez l'installation. Le programme d'installation préparera tous les domaines pour Exchange dans votre forêt Active Directory pour vous.

Avant de préparer tous les domaines dans votre forêt Active Directory, gardez les points suivants à l'esprit :

  - Le compte que vous utilisez doit être un membre du groupe de sécurité Administrateurs d'entreprise.

  - Patientez jusqu'à ce que Active Directory ait répliqué les modifications apportées à l'étape 2 sur tous vos contrôleurs de domaine. Si vous ne le faites pas, vous pouvez obtenir une erreur lorsque vous essayez de préparer le domaine.

Lorsque vous êtes prêt, procédez comme suit pour préparer tous les domaines dans votre forêt Active Directory pour Exchange.

1.  Ouvrez une fenêtre d'invite de commande Windows et accédez à l'endroit où vous avez téléchargé les fichiers d'installation Exchange.

2.  Exécutez la commande suivante :
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## Me laisser choisir les domaines Active Directory que je souhaite préparer

Si vous souhaitez choisir les domaines Active Directory que vous souhaitez préparer, vous pouvez utiliser le paramètre *PrepareDomain* lorsque vous exécutez le programme d'installation. Lorsque vous utilisez le paramètre *PrepareDomain*, vous devez inclure le nom de domaine complet (FQDN) du domaine que vous souhaitez préparer.

Avant de préparer les domaines dans votre forêt Active Directory, gardez les points suivants à l'esprit :

  - Le compte que vous utilisez doit disposer des autorisations selon le moment où le domaine a été créé.
    
      - **Domaine créé avant l'exécution de PrepareAD**   Si le nom de domaine a été créé **avant** que vous ayez exécuté la commande *PrepareAD* à l'étape 2 ci-dessus, le compte que vous utilisez doit être un membre du groupe Administrateurs du domaine dans le domaine que vous souhaitez préparer.
    
      - **Domaine créé après l'exécution de PrepareAD**   Si le nom de domaine a été créé **après** que vous avez exécuté la commande *PrepareAD* à l'étape 2 ci-dessus, le compte que vous utilisez doit 1) être membre du groupe de rôles Gestion de l'organisation et 2) être membre du groupe Administrateurs du domaine dans le domaine que vous souhaitez préparer.

  - Patientez jusqu'à ce que Active Directory ait répliqué les modifications apportées à l'étape 2 sur tous vos contrôleurs de domaine. Si vous ne le faites pas, vous pouvez obtenir une erreur lorsque vous essayez de préparer le domaine.

  - Vous devez préparer tous les domaines où un serveur Exchange sera installé. Vous aurez également besoin de préparer tous les domaines qui contiendront des utilisateurs à extension messagerie, même si ces domaines ne contiendront aucun serveur Exchange.

  - Vous n'avez pas besoin d'exécuter la commande *PrepareDomain* dans le domaine où la commande *PrepareAD* a été exécutée. La commande *PrepareAD* prépare automatiquement ce domaine.

Lorsque vous êtes prêt, procédez comme suit pour préparer un domaine individuel dans votre forêt Active Directory pour Exchange.

1.  Ouvrez une fenêtre d'invite de commande Windows et accédez à l'endroit où vous avez téléchargé les fichiers d'installation Exchange.

2.  Exécutez la commande suivante. Incluez le nom de domaine complet (FQDN) du domaine que vous souhaitez préparer. Si vous souhaitez préparer le domaine dans lequel vous exécutez la commande, vous n'avez pas à inclure le nom de domaine complet.
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Répétez les étapes pour chaque domaine Active Directory où vous installerez un serveur Exchange ou bien où les utilisateurs à extension messagerie seront situés.

## Comment savoir si cela a fonctionné ?

Une fois que vous avez suivi toutes les étapes ci-dessus, vous pouvez vérifier que tout a bien fonctionné. Pour ce faire, vous utiliserez un outil appelé ADSI Edit (Active Directory Service Interfaces Editor). ADSI Edit est inclus dans le cadre de la fonction des Outils de services de domaine Active Directory dans Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2. Si vous souhaitez en savoir plus, consultez [ADSI Edit (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="Avertissement" alt="Avertissement" />Avertissement :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ne modifiez jamais les valeurs dans ADSI Edit, sauf si vous êtes invité à le faire par le support Microsoft. La modification des valeurs dans ADSI Edit peut causer des dommages irréparables à votre organisation Exchange et Active Directory.</td>
</tr>
</tbody>
</table>


Une fois qu’Exchange étend votre schéma Active Directory et prépare Active Directory pour Exchange, plusieurs propriétés sont mises à jour pour indiquer que la préparation est terminée. Utilisez les informations de la liste ci-dessous pour vérifier que ces propriétés ont les valeurs correctes. Chaque propriété doit correspondre à la valeur dans le tableau ci-dessous pour la version d’Exchange 2013 que vous installez.

  - Dans le contexte d’appellation **Schéma**, vérifiez que la propriété **rangeUpper** sur **ms-Exch-Schema-Verision-Pt** est définie sur la valeur indiquée pour votre version d’Exchange 2013 dans le tableau Versions d’Active Directory dans Exchange 2013.
    
     

  - Dans le contexte d’appellation **Configuration**, vérifiez que la propriété **objectVersion** dans CN=\<*your organization*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domain* est définie sur la valeur indiquée pour votre version d’Exchange 2013 dans le tableau Versions d’Active Directory dans Exchange 2013.
    
     

  - Dans le contexte d’appellation **Par défaut**, vérifiez que la propriété **objectVersion** dans le **conteneur d’objets système Microsoft Exchange** sous DC=\<*root domain* est définie sur la valeur indiquée pour votre version d’Exchange 2013 dans le tableau Versions d’Active Directory dans Exchange 2013.
    
     

Vous pouvez également examiner le journal d'installation d'Exchange pour vérifier que la préparation d'Active Directory s'est terminée correctement. Pour plus d'informations, consultez la rubrique [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md). Vous ne pouvez pas utiliser la cmdlet **Get-ExchangeServer** mentionnée dans la rubrique [Vérifier une installation d’Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md) tant que vous n'avez pas terminé l'installation d'au moins un rôle serveur de boîtes aux lettres et un rôle serveur d'accès au client dans un site Active Directory.

## Versions d’Active Directory dans Exchange 2013

Le tableau suivant vous montre les objets Exchange 2013 dans Active Directory qui sont mis à jour chaque fois que vous installez une nouvelle version de Exchange 2013. Vous pouvez comparer les versions d'objet que vous voyez avec les valeurs du tableau ci-dessous pour vérifier que la version de Exchange 2013 que vous avez installée a correctement mis à jour Active Directory lors de l'installation.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Version d’Exchange</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Contexte de nommage</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>Conteneur</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Objets systèmeMicrosoft Exchange</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 et versions ultérieures</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

