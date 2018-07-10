---
title: 'Account setup in Outlook for iOS and Android using basic authentication: Exchange 2013 Help'
TOCTitle: Account setup in Outlook for iOS and Android using basic authentication
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518367
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Account setup in Outlook for iOS and Android using basic authentication

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-04-30_

**Résumé** : Comment les utilisateurs de votre organisation Exchange 2013 peuvent rapidement configurer leurs comptes Outlook pour iOS et Android à l’aide de l’authentification de base.

Outlook pour iOS et Android permet aux administrateurs Exchange de « transférer » leurs configurations de compte vers leurs utilisateurs en local qui utilisent l’authentification de base via le protocole ActiveSync. Cette fonctionnalité marche avec n’importe quel fournisseur Mobile Device Management (MDM) qui utilise le canal [Configuration d’application gérée](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) pour iOS ou le canal [Android dans l’entreprise](https://developer.android.com/samples/apprestrictions/index.html) pour Android.

Pour les utilisateurs locaux inscrits auprès de Microsoft Intune, vous pouvez déployer les paramètres de configuration de compte à l’aide d’Intune dans le portail Azure.

Une fois qu’une configuration de compte a été créée et que l’utilisateur a inscrit son appareil, Outlook pour iOS et Android détecte un compte et invite l’utilisateur à l’ajouter. La seule information que l’utilisateur doit saisir pour terminer le processus de configuration est son mot de passe. Ensuite, le contenu de boîte aux lettres de l’utilisateur charge et l’utilisateur peut commencer à utiliser l’application.

Les images suivantes présentent un exemple du processus de configuration de l’utilisateur final une fois que Outlook pour iOS et Android a été configuré dans Intune sur le portail Azure.

![Configuration locale du compte dans Outlook pour iOS et Android](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Configuration locale du compte dans Outlook pour iOS et Android")

## Créer une stratégie de configuration d’application pour Outlook pour iOS et Android à l’aide de Microsoft Intune

Si vous utilisez Microsoft Intune en tant que fournisseur de gestion des appareils mobiles, les étapes suivantes vous permettront de déployer des paramètres de configuration de compte pour vos boîtes aux lettres en local qui utilisent l’authentification de base avec le protocole ActiveSync. Une fois la configuration créée, vous pouvez attribuer les paramètres à des groupes d’utilisateurs, comme indiqué dans la section suivante, Attribuer des paramètres de configuration.

> [!NOTE]
> Si les utilisateurs de votre organisation utilisent iOS et Android pour les appareils de travail, vous devez créer une stratégie de configuration d’application distincte pour chaque plateforme.


1.  Connectez-vous au portail Azure.

2.  Sélectionnez **Plus de services \> Surveillance + Gestion \> Intune**.

3.  Sur le panneau **Applications mobiles** de la liste Gérer, sélectionnez **Stratégies de configuration d’application**.

4.  Sur le panneau **Stratégies de configuration d’application**, choisissez **Ajouter**.

5.  Sur le panneau **Ajouter une configuration d’application**, saisissez un **nom** et une **description** facultative pour les paramètres de configuration d’application.

6.  Pour le type **Inscription d’appareil**, choisissez **Appareils gérés**.

7.  Pour **Plateforme**, sélectionnez **iOS** ou **Android for Work**.

8.  Sélectionnez **Applications associées**, puis, dans le panneau **Applications ciblées**, sélectionnez **Microsoft Outlook pour iOS** ou **Microsoft Outlook pour Android**.

9.  Cliquez sur **OK** pour revenir au panneau **Ajouter une configuration d’application**.

10. Choisissez **Paramètres de configuration**. Sur le panneau **Paramètres de configuration**, définissez les paires clé/valeur qui fournissent des configurations pour Outlook pour iOS et Android. Les paires clé/valeur que vous saisissez sont définies plus loin dans cet article, dans la section Paires clé/valeur.
    
    > [!NOTE]
    > Pour saisir les paires clé/valeur, vous avez le choix entre utiliser le concepteur de configuration ou saisir la liste des propriétés XML.


11. Lorsque vous avez terminé, choisissez **OK**.

12. Sur le panneau **Ajouter une configuration d’application**, choisissez **Créer**.

La stratégie de configuration nouvellement créée apparaît sur le panneau **Stratégies de configuration d’application**.

## Attribuer des paramètres de configuration

Vous attribuez les paramètres que vous avez créés dans la section précédente à des groupes d’utilisateurs dans Azure Active Directory. Lorsqu’un utilisateur dispose de l’application Microsoft Outlook, celle-ci est gérée par les paramètres que vous avez spécifiés. Pour ce faire, procédez comme suit :

1.  Sur le panneau **Applications mobiles** du tableau de bord de gestion des applications mobiles Intune, choisissez **Stratégies de configuration d’application**.

2.  Dans la liste des stratégies de configuration d’application, sélectionnez celle que vous voulez affecter, puis cliquez sur **Affectations**.

3.  Sur le panneau **Affectations**, choisissez **Sélectionner des groupes**.

4.  Sur le panneau **Sélectionner des groupes**, choisissez le groupe Azure AD auquel vous souhaitez affecter la stratégie de configuration d’application, puis choisissez **Sélectionner** et **Enregistrer**.

## Paire clé/valeur

Lorsque vous créez une stratégie de configuration d’application dans le portail Azure ou via votre fournisseur MDM, vous devez disposer des paires clé/valeur suivantes :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Clé</th>
<th>Valeurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>Cette valeur indique le compte de messagerie de nom d’affichage tel que les utilisateurs le voient sur leur appareil.</p>
<p><strong>Valeurs acceptées</strong> : String</p>
<p><strong>Valeur par défaut si aucune indication</strong> : True</p>
<p><strong>Exemple</strong> : user@companyname.com</p>
<p><strong>Jeton Intune*</strong> : {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>Cette valeur indique l’adresse de messagerie à utiliser pour envoyer et recevoir des e-mails.</p>
<p><strong>Valeurs acceptées</strong> : String</p>
<p><strong>Valeur par défaut si aucune indication</strong> : True</p>
<p><strong>Exemple</strong> : user@companyname.com</p>
<p><strong>Jeton Intune*</strong> : {{mail}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>Cette valeur indique le nom principal d’utilisateur pour le profil d’e-mail utilisé pour authentifier le compte.</p>
<p><strong>Valeurs acceptées</strong> : String</p>
<p><strong>Valeur par défaut si aucune indication</strong> : True</p>
<p><strong>Exemple</strong> : userupn@companyname.com</p>
<p><strong>Jeton Intune*</strong> : {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>Cette valeur indique la méthode d’authentification pour l’utilisateur.</p>
<p><strong>Valeurs acceptées</strong> : « Nom d’utilisateur et mot de passe » ; « Certificats »</p>
<p><strong>Valeur par défaut si aucune indication</strong> : « Nom d’utilisateur et mot de passe »</p>
<p><strong>Exemple</strong> : « Nom d’utilisateur et mot de passe »</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>Cette valeur indique le nom d’hôte de votre serveur Exchange.</p>
<p><strong>Valeurs acceptées</strong> : String</p>
<p><strong>Valeur par défaut si aucune indication</strong> : True</p></td>
</tr>
</tbody>
</table>


**\*** Les utilisateurs Microsoft Intune peuvent utiliser des jetons qui s’adaptent à la valeur correcte en fonction de l’utilisateur inscrit MDM. Consultez la rubrique [Ajouter des stratégies de configuration d’applications pour les appareils iOS gérés](https://docs.microsoft.com/fr-fr/intune/app-configuration-policies-use-ios) pour plus d’informations.

