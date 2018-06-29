---
title: 'Configuration du flux de messagerie et de l’accès au client: Exchange 2013 Help'
TOCTitle: Configuration du flux de messagerie et de l’accès au client
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50478073
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuration du flux de messagerie et de l’accès au client

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-12-09_

Tâches consécutives à l’installation pour le flux de messagerie et l’accès client Exchange Server 2013, incluant comment configurer un certificat SSL.

Une fois Microsoft Exchange Server 2013 installé dans votre organisation, vous devez configurer Exchange Server 2013 pour le flux de messagerie et l'accès au client. Si vous n'effectuez pas ces étapes supplémentaires, vous ne pourrez pas envoyer de messages via Internet, et les clients externes tels que les périphériques Microsoft Office Outlook et ActiveSync ne pourront pas se connecter à votre organisation Exchange.

Les étapes de la présente rubrique supposent un déploiement Exchange de base avec un site Active Directory unique et un espace de noms SMTP unique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette rubrique utilise des valeurs d'exemple telles que Ex2013CAS, contoso.com, mail.contoso.com et 172.16.10.11. Remplacez ces valeurs d'exemple par les noms serveurs, noms de domaine complet et adresses IP pour votre organisation.</td>
</tr>
</tbody>
</table>


Pour les autres tâches de gestion relatives au flux de messagerie, aux clients et aux périphériques, consultez les rubriques [Flux de messagerie](mail-flow-exchange-2013-help.md) et [Clients et mobilité](clients-and-mobile-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée de cette tâche : 50 minutes

  - Les procédures décrites dans cette rubrique requièrent des autorisations spécifiques. Consultez chaque procédure pour savoir quelles autorisations sont nécessaires.

  - Il est possible que vous receviez des avertissements de certificats lors de la connexion au site web du centre d'administration Exchange (CAE) tant que vous n'avez pas configuré un certificat SSL (Secure Sockets Layer) sur le serveur d'accès au client. Vous verrez comment effectuer cette opération plus loin dans cette rubrique.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Chaque organisation demande au minimum un serveur d'accès au client et un serveur de boîtes aux lettres dans la forêt Active Directory. De plus, chaque site Active Directory qui contient un serveur de boîtes aux lettres doit également contenir au moins un serveur d'accès au client. Si vous séparez les rôles de vos serveurs, nous vous recommandons d'installer le serveur ayant le rôle de serveur de boîtes aux lettres en premier.</td>
</tr>
</tbody>
</table>


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


## Comment procéder ?

## Étape 1 : créer un connecteur d'envoi

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Connecteurs d'envoi » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Avant d'envoyer un message sur Internet, vous devez créer un connecteur d'envoi sur le serveur de boîtes aux lettres. Procédez comme suit.

1.  Ouvrez le CAE en accédant à l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Saisissez votre nom d'utilisateur et votre mot de passe dans **Domain\\user name** et **Password** puis cliquez sur **Se connecter**.

3.  Accédez à **Flux de messagerie**\>**Connecteurs d'envoi**. Dans la page **Connecteurs d'envoi**, cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans l'Assistant **Nouveau connecteur d'envoi**, spécifiez un nom pour le connecteur d'envoi, puis sélectionnez **Internet**. Cliquez sur **Suivant**.

5.  Vérifiez que la case **Enregistrement MX associé au domaine destinataire** est cochée. Cliquez sur **Suivant**.

6.  Sous **Espace d'adressage**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Ajouter un domaine**, vérifiez que **SMTP** est sélectionné dans le champ **Type**. Dans le champ **Nom de domaine complet**, entrez **\***. Cliquez sur **Enregistrer**.

7.  Vérifiez que la case **Connecteur d'envoi délimité** n'est pas cochée et cliquez sur **Suivant**.

8.  Sous **Serveur source**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Dans la fenêtre **Sélectionner le serveur**, sélectionnez un serveur de boîtes aux lettres. Cliquez ensuite sur **Ajouter** puis **OK**.

9.  Cliquez sur **Terminer**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un connecteur de réception entrant par défaut est créé lors de l'installation d'Exchange 2013. Ce connecteur de réception accepte les connexions SMTP anonymes provenant de serveurs externes. Aucune autre configuration n'est nécessaire s'il s'agit de la fonctionnalité souhaitée. Si vous désirez restreindre les connexions entrantes à partir de serveurs externes, modifiez le connecteur de réception du <strong>&lt;serveur d'accès au client&gt; frontal par défaut</strong> sur le serveur d'accès au client.</td>
</tr>
</tbody>
</table>


## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien créé un connecteur d'envoi sortant, procédez comme suit :

1.  Dans l'EAC, vérifiez que le nouveau connecteur d'envoi apparait dans **Flux de messagerie** \> **Connecteurs d'envoi**.

2.  Ouvrez Outlook Web App et envoyez un message électronique vers un destinataire externe. Si le destinataire reçoit le message, vous avez correctement configuré le connecteur d'envoi.

## Étape 2 : ajouter des domaines acceptés supplémentaires

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Domaines acceptés » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Par défaut, lorsque vous déployez une nouvelle organisation Exchange 2013 dans une forêt Active Directory, Exchange utilise le nom de domaine du domaine Active Directory, où Setup /PrepareAD a été exécuté. Si vous souhaitez que les destinataires reçoivent et envoient des messages vers et depuis un autre domaine, vous devez l'ajouter comme un domaine accepté. Ce domaine est également ajouté comme adresse SMTP principale sur la stratégie d'adresse de messagerie par défaut au cours de la prochaine étape.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Un enregistrement de ressource MX DNS (Domain Name System) public est requis pour chaque domaine SMTP pour lequel vous acceptez des messages électroniques en provenance d'Internet. Chaque enregistrement MX doit se résoudre dans le serveur côté Internet qui reçoit les messages électroniques pour votre organisation.</td>
</tr>
</tbody>
</table>


1.  Ouvrez le CAE en recherchant l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Saisissez votre nom d'utilisateur et votre mot de passe dans **Domain\\user name** et **Password** puis cliquez sur **Se connecter**.

3.  Accédez à **Flux de messagerie**\>**Domaines acceptés**. Dans la page **Domaines acceptés**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans l'Assistant **Nouveau domaine accepté**, spécifiez un nom pour le domaine accepté.

5.  Dans le champ **Domaine accepté**, spécifiez le domaine destinataire SMTP à ajouter. Par exemple, contoso.com.

6.  Sélectionnez **Domaine faisant autorité**, puis cliquez sur **Enregistrer**.

## Comment savoir si cette étape a fonctionné ?

Pour vérifier qu'un domaine accepté a bien été créé, procédez comme suit :

  - Dans le CAE, vérifiez que le domaine accepté apparaît dans **Flux de messagerie**\>**Domaines acceptés**.

## Étape 3 : configurer la stratégie d'adresse de messagerie par défaut

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Stratégies d'adresse de messagerie » dans la rubrique [Autorisations pour configurer les adresses de messagerie et les carnets d’adresses](email-address-and-address-book-permissions-exchange-2013-help.md).

Si vous avez ajouté un domaine accepté à l'étape précédente et que vous souhaitez l'ajouter à chaque destinataire dans l'organisation, vous devez mettre à jour la stratégie d'adresse de messagerie par défaut.

1.  Ouvrez le CAE en recherchant l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Saisissez votre nom d'utilisateur et votre mot de passe dans **Domain\\user name** et **Password** puis cliquez sur **Se connecter**.

3.  Accédez à **Flux de messagerie**\>**Stratégie d'adresse de messagerie**. Dans la page **Stratégie d'adresse de messagerie**, sélectionnez **Stratégie par défaut**, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Dans la page **Stratégie d'adresse de messagerie par défaut**, cliquez sur **Format d'adresse de messagerie**.

5.  Sous **Format d'adresse de messagerie**, cliquez sur l'adresse SMTP à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

6.  Dans la page **Format d'adresse de messagerie**, dans le champ **Paramètres des adresses de messagerie**, spécifiez le domaine destinataire SMTP à appliquer à tous les destinataires dans l'organisation Exchange. Ce domaine doit correspondre au domaine accepté ajouté à l'étape précédente. Par exemple, @contoso.com. Cliquez sur **Enregistrer**.

7.  Cliquez sur **Enregistrer**

8.  Dans le volet d'informations **Stratégie par défaut**, cliquez sur **Appliquer**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous recommandons de configurer un nom d'utilisateur principal (UPN) qui corresponde à l'adresse de messagerie principale de chaque utilisateur. Si vous ne fournissez pas de nom d'utilisateur principal correspondant à l'adresse de messagerie d'un utilisateur, celui-ci devra indiquer manuellement son nom de domaine/d'utilisateur ou son nom d'utilisateur principal en plus de son adresse de messagerie. Si le nom d'utilisateur principal correspond à l'adresse de messagerie, Outlook Web App, ActiveSync et Outlook feront automatiquement correspondre l'adresse de messagerie avec le nom d'utilisateur principal.</td>
</tr>
</tbody>
</table>


## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré la stratégie d'adresse de messagerie par défaut, procédez comme suit :

1.  Dans l'EAC, accédez à **Destinataires** \> **Boîtes aux lettres**.

2.  Sélectionnez une boîte aux lettres, puis, dans le volet d'informations des destinataires, vérifiez que le champ **Boîte aux lettres utilisateurs** a été défini sur *\<alias\>*@*\<nouveau domaine accepté\>*. Par exemple, david@contoso.com.

3.  Créez éventuellement un nouvelle boîte aux lettres et vérifiez qu'elle dispose d'une adresse de messagerie avec le nouveau domaine accepté en procédant comme suit :
    
    1.  Accédez à **Destinataires**\>**Boîtes aux lettres**, cliquez sur **Nouvelle** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"), puis sélectionnez **Boîte aux lettres utilisateur**.
    
    2.  Dans la page Nouvelle boîte aux lettres utilisateur, fournissez les informations requises pour créer une nouvelle boîte aux lettres. Cliquez sur **Enregistrer**.
    
    3.  Sélectionnez une nouvelle boîte aux lettres, puis, dans le volet d'informations des destinataires, vérifiez que le champ **Boîte aux lettres utilisateur** est défini sur *\<alias\>*@*\<nouveau domaine accepté\>*. Par exemple, david@contoso.com.

## Étape 4 : configurer des URL externes

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Paramètres de répertoire virtuel *\<Service\>* » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Avant que les clients puissent se connecter à votre nouveau serveur à partir d'Internet, vous devez configurer les domaines externes (ou URL) des répertoires virtuels du serveur d'accès au client, puis configurer vos enregistrements DNS (service de noms de domaine) public. Les étapes suivantes permettent de configurer le même domaine externe sur l'URL externe de chaque répertoire virtuel. Si vous désirez configurer différents domaines externes sur une ou plusieurs URL externes de répertoire virtuel, vous devez configurer les URL externes manuellement. Pour plus d'informations, consultez la rubrique [Gestion des répertoires virtuels](virtual-directory-management-exchange-2013-help.md).

1.  Ouvrez le CAE en recherchant l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Saisissez votre nom d'utilisateur et votre mot de passe dans **Domain\\user name** et **Password** puis cliquez sur **Se connecter**.

3.  Accédez à **Serveurs**\>**Serveurs**, sélectionnez le nom du serveur d'accès au client connecté à Internet, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Cliquez sur **Outlook Anywhere**.

5.  Dans le champ **Spécifier le nom d’hôte externe**, spécifiez le nom de domaine complet accessible en externe du serveur d’accès au client. Par exemple, mail.contoso.com.

6.  Profitez-en également pour définir le nom de domaine complet accessible en interne du serveur d’accès au client. Dans le champ **Spécifier le nom d’hôte interne**, indiquez le nom de domaine complet utilisé à l’étape précédente. Par exemple, mail.contoso.com.

7.  Cliquez sur **Enregistrer**.

8.  Accédez à **Serveurs**\>**Répertoires virtuels**, puis cliquez sur **Configurer le domaine d'accès externe** ![Icône Configurer](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "Icône Configurer")

9.  Sous **Sélectionnez les serveurs d'accès au client à utiliser avec l'URL externe**, cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter")

10. Sélectionnez les serveurs d'accès au client à configurer, puis cliquez sur **Ajouter**. Après avoir ajouté tous les serveurs d’accès au client à configurer, cliquez sur **OK**.

11. Dans **Entrer le nom de domaine que vous utiliserez avec vos serveurs d'accès au client externes**, tapez le domaine externe à appliquer. Par exemple, mail.contoso.com. Cliquez sur **Enregistrer**.
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Certaines organisations choisissent un nom de domaine complet Outlook Web App unique pour protéger les utilisateurs contre les modifications apportées au nom de domaine complet des serveurs sous-jacents. De nombreuses organisations utilisent owa.contoso.com comme nom de domaine complet Outlook Web App au lieu de mail.contoso.com. Pour configurer un nom de domaine complet Outlook Web App unique, procédez comme suit lorsque vous avez terminé l'étape précédente. Pour suivre cette liste de contrôle, vous devez avoir configuré un nom de domaine complet Outlook Web App unique.
    <ol>
    <li><p>Sélectionnez <strong>owa (site web par défaut)</strong> et cliquez sur <strong>Modifier</strong> <img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />.</p></li>
    <li><p>Dans <strong>URL externe</strong>, tapez <strong>https://</strong>, puis le nom de domaine complet Outlook Web App unique à utiliser. Ajoutez ensuite <strong>/owa</strong>. Par exemple, https://owa.contoso.com/owa.</p></li>
    <li><p>Cliquez sur <strong>Enregistrer</strong>.</p></li>
    <li><p>Sélectionnez <strong>ecp (site web par défaut)</strong> et cliquez sur <strong>Modifier</strong> <img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icône Modifier" alt="Icône Modifier" />.</p></li>
    <li><p>Dans <strong>URL externe</strong>, tapez <strong>https://</strong>, puis le nom de domaine complet Outlook Web App indiqué à l’étape précédente. Ajoutez ensuite <strong>/ecp</strong>. Par exemple, https://owa.contoso.com/ecp.</p></li>
    <li><p>Cliquez sur <strong>Enregistrer</strong>.</p></li>
    </ol></td>
    </tr>
    </tbody>
    </table>


Après avoir configuré l'URL externe sur les répertoires virtuels du serveur d'accès au client, vous devez configurer vos enregistrements DNS publics pour le service de découverte automatique, Outlook Web App et le flux de messagerie. Les enregistrements DNS publics doivent pointer vers le nom de domaine complet ou l'adresse IP externe de votre serveur d'accès au client côté Internet et utiliser les noms de domaine complets accessibles depuis l'extérieur que vous avez configurés sur votre serveur d'accès au client. Les exemples suivants présentent les enregistrements DNS recommandés que vous devez créer pour activer le flux de messagerie et la connectivité client externe.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Type d’enregistrement DNS</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez bien configuré l'URL externe sur les répertoires virtuels du serveur d'accès au client, procédez comme suit :

1.  Dans le CAE, accédez à **Serveurs** \> **Répertoires virtuels**.

2.  Dans le champ **Sélectionner le serveur**, sélectionnez le serveur d'accès au client connecté à Internet.

3.  Sélectionnez un répertoire virtuel, puis, dans le volet d'informations du répertoire virtuel, vérifiez que le champ **URL externe** est renseigné avec le nom de domaine complet et le service corrects, comme indiqué ci-dessous :
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Répertoire virtuel</th>
    <th>Valeur d’URL externe</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Découverte automatique</strong></p></td>
    <td><p>Aucune URL externe affichée</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Pour vérifier que vous avez configuré correctement vos enregistrements DNS publics, procédez comme suit :

1.  Ouvrez une invite de commandes et exécutez `nslookup.exe`.

2.  Mettez en place un serveur DNS qui peut interroger votre zone DNS publique.

3.  Dans `nslookup`, recherchez l'enregistrement de chaque nom de domaine complet que vous avez créé. Vérifiez que la valeur renvoyée pour chaque nom de domaine complet est correcte.

4.  Dans `nslookup`, tapez `set type=mx` puis recherchez le domaine accepté ajouté à l'étape 1. Vérifiez que la valeur renvoyée correspond au nom de domaine complet du serveur d'accès au client.

## Étape 5 : configurer des URL internes

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Paramètres de répertoire virtuel *\<Service\>* » dans la rubrique [Autorisations des clients et des périphériques mobiles](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Avant que les clients puissent se connecter à votre nouveau serveur à partir de votre intranet, vous devez configurer les domaines internes, ou les URL, sur les répertoires virtuels du serveur d’accès au client, puis configurer vos enregistrements de service de nom de domaine (DNS) privés.

La procédure suivante vous permet de choisir si vos utilisateurs utilisent la même URL sur votre intranet et sur Internet pour accéder à votre serveur Exchange, ou s'ils utilisent une URL distincte. Votre choix dépend du schéma d'adressage que vous avez mis en place ou que vous comptez utiliser. Si vous mettez en place un nouveau schéma d’adressage, nous vous conseillons d’utiliser la même URL pour les accès internes et externes. Comme il est plus facile de mémoriser une seule adresse, les utilisateurs gagnent en simplicité pour accéder à votre serveur Exchange. Quel que soit votre choix, assurez-vous de configurer une zone DNS privée pour l'espace d'adressage que vous configurez. Pour plus d'informations sur l'administration des zones DNS, consultez la page [Administration du serveur DNS](http://go.microsoft.com/fwlink/p/?linkid=190631).

Pour plus d'informations sur les URL internes et externes des répertoires virtuels, consultez la rubrique [Gestion des répertoires virtuels](virtual-directory-management-exchange-2013-help.md).

## Configuration d'une adresse identique pour les URL internes et externes

1.  Ouvrez l'environnement de ligne de commande Exchange Management Shell sur votre serveur d'accès au client.

2.  Stockez le nom d'hôte de votre serveur d'accès au client dans une variable qui sera utilisée à l'étape suivante. Par exemple, Ex2013CAS.
    
        $HostName = "Ex2013CAS"

3.  Exécutez chacune des commandes suivantes dans l'environnement de ligne de commande Exchange Management Shell pour configurer chaque URL interne de sorte à ce qu'elle soit identique à l'URL externe du répertoire virtuel.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  Pendant que nous sommes dans l’environnement de ligne de commande Exchange Management Shell, nous allons également configurer le carnet d’adresses en mode hors connexion de sorte que la découverte automatique sélectionne le bon répertoire virtuel pour le distribuer. Pour cela, exécutez les commandes suivantes.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Après avoir configuré l'URL interne sur les répertoires virtuels du serveur d'accès au client, vous devez configurer vos enregistrements DNS privés pour Outlook Web App (et autres). En fonction de votre configuration, vous devez faire pointer vos enregistrements DNS privés vers l’adresse IP interne ou externe, ou le nom de domaine complet (FQDN) de votre serveur d’accès au client. Voici des exemples d'enregistrements DNS conseillés, à créer pour activer la connexion du client interne.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Type d’enregistrement DNS</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Comment savoir si cette étape a fonctionné ?

Pour vous assurer d'avoir configuré correctement l'URL interne sur les répertoires virtuels du serveur d'accès au client, procédez comme suit :

1.  Dans l'EAC, accédez à **Serveurs** \> **Répertoires virtuels**.

2.  Dans le champ **Sélectionner le serveur**, sélectionnez le serveur d'accès au client connecté à Internet.

3.  Sélectionnez un répertoire virtuel, puis cliquez sur **Modifier** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Vérifiez que le champ **URL interne** présente le nom de domaine complet et le service corrects, comme indiqué ci-dessous :
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Répertoire virtuel</th>
    <th>Valeur de l'URL interne</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Découverte automatique</strong></p></td>
    <td><p>Aucune URL interne affichée</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Pour vous assurer d'avoir configuré correctement vos enregistrements DNS privés, procédez comme suit :

1.  Ouvrez une invite de commandes et exécutez `nslookup.exe`.

2.  Mettez en place un serveur DNS qui peut interroger votre zone DNS privée.

3.  Dans `nslookup`, recherchez l'enregistrement de chaque nom de domaine complet que vous avez créé. Vérifiez que la valeur renvoyée pour chaque nom de domaine complet est correcte.

## Configuration des URL internes et externes différentes

1.  Ouvrez le CAE en accédant à l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Accédez à **Serveurs** \> **Répertoires virtuels**.

3.  Dans le champ **Sélectionner le serveur**, sélectionnez le serveur d'accès au client connecté à Internet.

4.  Sélectionnez le répertoire virtuel à modifier, puis cliquez sur **Modifier** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Dans **URL interne**, remplacez le nom d'hôte situé entre **https://** et la première barre oblique (**/**) par le nouveau nom de domaine complet à utiliser. Par exemple, pour changer le FQDN du répertoire virtuel EWS de Ex2013CAS.corp.contoso.com à internal.contoso.com, changez l'URL interne de https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx à https://internal.contoso.com/ews/exchange.asmx.

6.  Cliquez sur **Enregistrer**.

7.  Répétez les étapes 5 et 6 pour chaque répertoire virtuel que vous souhaitez changer.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les URL internes des répertoires virtuels ECP et OWA doivent être les mêmes.<br />
    Vous ne pouvez pas définir une URL interne sur le répertoire virtuel du service de découverte automatique.</td>
    </tr>
    </tbody>
    </table>


8.  Enfin, vous devez ouvrir l’environnement de ligne de commande Exchange Management Shell et configurer le carnet d’adresses en mode hors connexion de sorte que la découverte automatique sélectionne le bon répertoire virtuel pour distribuer le carnet d’adresses. Pour cela, exécutez les commandes suivantes.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Après avoir configuré l'URL interne sur les répertoires virtuels du serveur d'accès au client, vous devez configurer vos enregistrements DNS privés pour Outlook Web App (et autres). En fonction de votre configuration, vous devez faire pointer vos enregistrements DNS privés vers l’adresse IP interne ou externe, ou le nom de domaine complet de votre serveur d’accès au client. Voici un exemple d’enregistrement DNS recommandé que vous devez créer pour activer la connectivité du client interne si vous avez configuré vos URL internes de répertoire virtuel pour qu’elles utilisent internal.contoso.com.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Type d’enregistrement DNS</th>
<th>Valeur</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Comment savoir si cette étape a fonctionné ?

Pour vous assurer d'avoir configuré correctement l'URL interne sur les répertoires virtuels du serveur d'accès au client, procédez comme suit :

1.  Dans l'EAC, accédez à **Serveurs** \> **Répertoires virtuels**.

2.  Dans le champ **Sélectionner le serveur**, sélectionnez le serveur d'accès au client connecté à Internet.

3.  Sélectionnez un répertoire virtuel, puis cliquez sur **Modifier** ![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

4.  Vérifiez que le champ **URL interne** présente le nom de domaine complet correct. Par exemple, vous avez pu définir les URL internes sur internal.contoso.com.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Répertoire virtuel</th>
    <th>Valeur de l'URL interne</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Découverte automatique</strong></p></td>
    <td><p>Aucune URL interne affichée</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Pour vous assurer d'avoir configuré correctement vos enregistrements DNS privés, procédez comme suit :

1.  Ouvrez une invite de commandes et exécutez `nslookup.exe`.

2.  Mettez en place un serveur DNS qui peut interroger votre zone DNS privée.

3.  Dans `nslookup`, recherchez l'enregistrement de chaque nom de domaine complet que vous avez créé. Vérifiez que la valeur renvoyée pour chaque nom de domaine complet est correcte.

## Étape 6 : configurer un certificat SSL

Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Gestion des certificats » dans la rubrique [Autorisations de flux de messagerie](mail-flow-permissions-exchange-2013-help.md).

Certains services, tels qu'Outlook Anywhere et ActiveSync Exchange, exigent la configuration de certificat sur votre serveur Exchange 2013. Les étapes suivantes indiquent comment configurer un certificat SSL depuis une autorité de certification tierce :

1.  Ouvrez le CAE en recherchant l'URL de votre serveur d'accès au client. Par exemple, https://Ex2013CAS/ECP.

2.  Saisissez votre nom d'utilisateur et votre mot de passe dans **Domain\\user name** et **Password** puis cliquez sur **Se connecter**.

3.  Accédez à **Serveurs**\>**Certificats**. Dans la page **Certificats**, vérifiez que votre serveur d'accès au client est sélectionné dans le champ **Sélectionner le serveur**, puis cliquez sur **Nouveau** ![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

4.  Dans l'assistant **Nouveau certificat Exchange**, sélectionnez **Créer une demande pour un certificat depuis une autorité de certification** puis cliquez sur **Suivant**.

5.  Spécifiez un nom pour ce certificat, puis cliquez sur **suivant**.

6.  Si vous souhaitez demander un certificat de caractère générique, sélectionnez **Demander un certificat de caractère générique** puis spécifiez le domaine racine de tous les sous-domaines dans le champ **Domaine racine**. Si vous ne souhaitez pas demander de certificat de caractère générique et si vous voulez à la place spécifier chaque domaine à ajouter au certificat, ne renseignez pas cette page. Cliquez sur **Suivant**.

7.  Cliquez sur **parcourir** et spécifiez un serveur Exchange pour y stocker le certificat. Le serveur que vous sélectionnez doit être le serveur d'accès au Client connecté à Internet. Cliquez sur **Suivant**.

8.  Pour chaque service de la liste, vérifiez que les noms de serveur externe et interne que les utilisateurs utiliseront pour se connecter au serveur Exchange sont corrects. Par exemple :
    
      - Si vous avez configuré vos URL internes et externes pour qu’elles soient identiques, **Outlook Web App (accès à partir d’Internet)** et **Outlook Web App (accès à partir de l’Intranet)** doivent afficher owa.contoso.com. **OAB (accès à partir d’Internet)** et **OAB (accès à partir de l’Intranet)** doivent afficher mail.contoso.com.
    
      - Si vous avez configuré les URL internes pour être internal.contoso.com, **Outlook Web App (accès à partir d’Internet)** doit afficher owa.contoso.com et **Outlook Web App (accès à partir de l’Intranet)** doit afficher internal.contoso.com.
    
    Ces domaines serviront à créer la demande de certificat SSL. Cliquez sur **Suivant**.

9.  Ajoutez tous les domaines supplémentaires que vous voulez inclure sur le certificat SSL.

10. Sélectionnez le domaine qui sera le nom commun du certificat, puis cliquez sur **Définir comme nom commun**. Par exemple, contoso.com. Cliquez sur **Suivant**.

11. Fournissez des informations sur votre organisation. Ces informations seront incluses dans le certificat SSL. Cliquez sur **Suivant**.

12. Spécifiez l'emplacement du réseau dans lequel vous voulez enregistrer cette demande de certificat. Cliquez sur **Terminer**.

Après avoir enregistré la demande de certificat, soumettez la demande à votre autorité de certification (CA). Il peut s'agir d'un CA interne ou tiers, en fonction de votre organisation. Les clients qui se connectent au serveur d'accès au client doivent approuver le CA que vous utiliser. Après avoir reçu le certificat de l'autorité de certification, procédez comme suit :

1.  Dans la page **Serveur** \> **Certificats** de l'EAC, sélectionnez la demande de certificat créée lors des étapes précédentes.

2.  Dans le volet d'informations de demande de certificat, cliquez sur **Terminer** sous **État**.

3.  Dans la page Effectuer la demande en attente, spécifiez le chemin d'accès au fichier du certificat SSL et cliquez sur **OK**.

4.  Sélectionnez le nouveau certificat ajouté, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

5.  Dans la page Certificat, cliquez sur **Services**.

6.  Sélectionnez les services que vous souhaitez attribuer à ce certificat. Au minimum, vous devez sélectionner **SMTP** et **IIS**. Cliquez sur **Enregistrer**.

7.  Si vous recevez l'avertissement **Remplacer le certificat SMTP par défaut existant ?**, cliquez sur **Oui**.

## Comment savoir si cette étape a fonctionné ?

Pour vérifier que vous avez ajouté correctement le nouveau certificat, procédez comme suit :

1.  Dans l'EAC, accédez à **Serveurs** \> **Certificats**.

2.  Sélectionnez le nouveau certificat puis, dans le volet d'informations du certificat, vérifiez que les options suivantes sont vraies :
    
      - **État** indique **Valide**
    
      - **Attribué aux services** indique, au minimum, **IIS** et **SMTP**.

## Comment savoir si cette tâche a fonctionné ?

Pour vérifier que vous avez configuré le flux de messagerie et l'accès au client externe, procédez comme suit :

1.  Dans Outlook, sur un périphérique ActiveSync Exchange ou sur les deux, créez un nouveau profil. Vérifiez qu'Outlook ou l'appareil mobile a bien créé le nouveau profil.

2.  Dans Outlook ou sur l'appareil mobile, envoyez un nouveau message vers un destinataire externe. Vérifiez que le destinataire externe reçoit le message.

3.  Dans la boîte aux lettres du destinataire externe, répondez au message envoyé depuis la boîte aux lettres Exchange. Vérifiez que la boîte aux lettres Exchange reçoit le message.

4.  Accédez à https://owa.contoso.com/owa et vérifiez qu'il n'y a aucun avertissement de certificat.

