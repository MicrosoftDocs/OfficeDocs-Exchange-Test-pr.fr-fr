---
title: 'Utilisation des composants WebPart Outlook Web App: Exchange 2013 Help'
TOCTitle: Utilisation des composants WebPart Outlook Web App
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70087531
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilisation des composants WebPart Outlook Web App

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-07-31_

Avec les composants WebPart MicrosoftOfficeOutlook Web App, vous pouvez spécifier la boîte aux lettres à ouvrir, le dossier à ouvrir dans la boîte aux lettres et l’affichage du contenu à utiliser.

Les composants WebPart Outlook Web App vous permettent d’accéder au contenu Outlook Web App directement à partir d’une URL. L’URL peut être entrée dans un navigateur web ou intégrée dans une application. En général, les composants WebPart ne sont pas créés manuellement. Ils sont créés par programmation à partir de sélections effectuées dans une interface utilisateur ou directement intégrés dans une application, telle qu’une page SharePoint Server. Le code de l’interface utilisateur crée ensuite l’URL. Les composants WebPart Outlook Web App vous permettent notamment d’afficher la boîte de réception ou le calendrier d’un utilisateur sur une page SharePoint.

> [!NOTE]
> Pour utiliser les composants WebPart Outlook Web App, la boîte aux lettres de l’utilisateur et la boîte aux lettres ouverte via un composant WebPart doivent être installées dans une même forêt Active Directory.


## Autorisations pour l’utilisation des composants WebPart Outlook Web Access

Pour utiliser les composants WebPart Outlook Web App, vous devez au minimum disposer de l’accès « Réviseur » au contenu que vous ouvrez. Si vous avez intégré un composant WebPart Outlook Web App requérant une authentification pour accéder à une application, vous devez transmettre les informations d’authentification ainsi que la demande du composant WebPart. Pour cela, vous pouvez configurer le répertoire virtuel Outlook Web App afin d’utiliser l’authentification Windows intégrée. L’authentification Windows intégrée permet aux utilisateurs qui ont déjà ouvert une session via leur compte Active Directory d’utiliser Outlook Web App sans avoir à entrer de nouveau leurs informations d’identification.

## Syntaxe des composants WebPart Outlook Web App

Outlook Web App dans Exchange 2013 comporte un format d’URL à utiliser pour les demandes au répertoire virtuel /owa. Ces demandes peuvent être effectuées en saisissant une URL directement dans un navigateur Web ou en intégrant l’URL dans une application web (par exemple, une page SharePoint Server).

Les composants WebPart Outlook Web App permettent de créer des URL présentant différents niveaux de complexité. Une URL de composant WebPart simple permet d’ouvrir la boîte de réception de n’importe quelle boîte aux lettres. Une URL de composant WebPart plus complexe permet de spécifier la boîte aux lettres à ouvrir, le dossier à ouvrir dans la boîte aux lettres et l’affichage du contenu à utiliser.

En fonction des mesures de sécurité appliquées à votre réseau, il se peut que vous deviez configurer le codage de l’URL de composants WebPart. Après la configuration du codage, le code de l’IU crée l’URL en utilisant les paramètres codés dans l’URL. Les paramètres codés dans l’URL utilisent %20 à la place des espaces et %2 à la place du délimiteur de chemin « / ». Tous les exemples de cette rubrique utilisent des paramètres codés.

Le tableau suivant répertorie les paramètres d’un composant WebPart et donne des exemples de leur utilisation.

### Paramètres de composant WebPart et exemples d’utilisation

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre d’URL</th>
<th>Description</th>
<th>Valeurs et exemples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nom du serveur et répertoire (obligatoire)</p></td>
<td><p>URL du répertoire virtuel d’Outlook Web App</p></td>
<td><p>Il peut s’agir de la même URL que celle dont se servent les utilisateurs pour se connecter à Outlook Web App, par exemple :</p>
<p>https://&lt;<em>server name</em>&gt;/owa</p></td>
</tr>
<tr class="even">
<td><p>Identification de boîte aux lettres par ouverture de session explicite Exchange 2013 (facultatif)</p></td>
<td><p>Toute adresse SMTP associée à la boîte aux lettres à ouvrir</p>
<p>Si cette section de l’URL est manquante, la boîte aux lettres par défaut de l’utilisateur authentifié est ouverte.</p>
<p>Si aucun paramètre supplémentaire n’est spécifié, le comportement par défaut consiste à ouvrir la boîte de réception.</p></td>
<td><p>Pour ouvrir la boîte aux lettres dont l’adresse SMTP est tsmith@fourthcoffee.com, utilisez l’URL suivante :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (obligatoire si vous spécifiez un paramètre autre que l’identification de boîte aux lettres par ouverture de session explicite)</p></td>
<td><p>?cmd=contents affiche le composant WebPart Outlook Web App spécifié par les paramètres au lieu de l’interface utilisateur Outlook Web App complète.</p></td>
<td><p>Si aucune boîte aux lettres n’est spécifiée, le paramètre cmd apparaît après l’adresse de connexion, comme suit :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents</p>
<p>Si aucune boîte aux lettres n’est spécifiée, le paramètre cmd apparaît après l’identification de boîte aux lettres explicite, comme suit :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/&lt;<em>SMTP address</em>&gt;/?cmd=contents</p>
<p>Si aucun paramètre supplémentaire n’est spécifié, le comportement par défaut consiste à ouvrir la boîte de réception.</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>Ce paramètre doit être pris en compte lors de l’utilisation de l’authentification LiveID</p>
<p>Tous les paramètres sont ignorés lors de l’authentification LiveID si « exsvurl=1 » n’est pas indiqué. Ce paramètre est destiné uniquement aux boîtes aux lettres Office 365.</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;exsvurl=1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (facultatif)</p></td>
<td><p>Cette partie de l’URL doit être écrite à l’aide du codage URL de sorte qu’elle puisse passer les pare-feu.</p>
<p>Lorsque vous utilisez le codage URL, une espace devient %20 et un délimiteur de chemin (/) devient %2f.</p>
<p>La hiérarchie de dossiers doit démarrer à partir de la racine de la boîte aux lettres.</p>
<p>Le chemin d’accès au dossier pointe vers des dossiers ordinaires ou des dossiers de recherche.</p></td>
<td><p>Pour ouvrir le sous-dossier Projets de la boîte de réception, utilisez l’URL suivante :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;fpath= inbox%2fprojects</p></td>
</tr>
<tr class="even">
<td><p>module (facultatif)</p></td>
<td><p>Ce paramètre permet de spécifier l’un des dossiers par défaut sans connaître le nom localisé.</p></td>
<td><p>Les valeurs du paramètre de module ne sont pas sensibles à la casse et incluent les éléments suivants :</p>
<ul>
<li><p>Boîte de réception</p></li>
<li><p>Calendrier</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>Pour ouvrir le calendrier d’une boîte aux lettres indépendamment de l’emplacement, utilisez l’URL suivante :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;module=calendar</p></td>
</tr>
<tr class="odd">
<td><p>view (facultatif)</p></td>
<td><p>Ce paramètre spécifie l’affichage du dossier.</p>
<p>Lorsque ce paramètre n’est pas présent, les affichages par défaut sont les suivants :</p>
<ul>
<li><p>Calendrier   Daily</p></li>
<li><p>Messages   Messages</p></li>
</ul>

> [!NOTE]
> Les chaînes des affichages par défaut sont automatiquement codées dans l’URL.

<p>Le tri par défaut d’un affichage correspond à la manière dont le dossier doit être trié s’il a été ouvert dans le client Outlook Web App.</p>
<p>Les chaînes identifiant les affichages ne sont pas localisées et ne sont pas sensibles à la casse.</p></td>
<td><p>Les affichages disponibles varient en fonction du type de dossier.</p>
<p>Affichages du calendrier :</p>
<ul>
<li><p>Daily   Affichage du calendrier quotidien</p></li>
<li><p>Weekly   Affichage du calendrier hebdomadaire</p></li>
<li><p>Monthly   Affichage du calendrier mensuel</p></li>
</ul>
<p>Affichages des messages :</p>
<ul>
<li><p>Messages   Affichage des messages, avec tri par défaut</p></li>
<li><p>By%20Sender   Affichage des messages triés par expéditeur dans l’ordre alphabétique</p></li>
<li><p>By%20Subject   Affichage des messages triés par objet dans l’ordre alphabétique</p></li>
<li><p>By%20Conversation%20Topic   Affichage Conversation non disponible dans la version Light d’Outlook Web App</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y (facultatif)</p></td>
<td><p>Spécifie la date à laquelle le calendrier doit s’afficher. Ces paramètres peuvent apparaître dans n’importe quel ordre et être utilisés individuellement ou non.</p>
<p>Si l’un de ces paramètres n’est pas spécifié, les valeurs par défaut sont le jour, le mois et l’année en cours. Par exemple, si la date du jour est le 3 mai 2016 et si vous spécifiez la valeur « 9 » pour le mois de septembre, la date affichée sera le 3 septembre 2016.</p></td>
<td><p>Les valeurs valides pour les paramètres de données sont les suivantes :</p>
<p>d=[1-31] ;</p>
<p>m=[1-12] ;</p>
<p>y=[année indiquée par quatre chiffres].</p>
<p>Pour ouvrir un calendrier à la date du 3 mai 2016, vous devez utiliser l’URL suivante : https://&lt;<em>server name</em>&gt;/owa/?cmd=content&amp;fpath=calendar&amp;view=daily&amp;d=3&amp;m=5&amp;y=2016</p></td>
</tr>
<tr class="odd">
<td><p>part (facultatif)</p></td>
<td><p>Indique qu’Outlook Web App doit afficher un composant WebPart réduit.</p></td>
<td><p>Lorsque vous utilisez les composants WebPart pour accéder au contenu Outlook Web App, l’IU qui s’affiche est plus petite que l’IU Outlook Web App complète. Le paramètre part réduit davantage l’IU. L’exemple d’URL suivant affiche la liste des tâches dans le plus petit format de composant WebPart :</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;part=1</p>
<p>Le paramètre part ne s’applique pas au module calendrier.</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>Le paramètre de ce composant inclut le contrôle de liste des dossiers pour les utilisateurs qui souhaitent naviguer dans les sous-dossiers. Il s’applique uniquement aux dossiers de messagerie.</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;folderlist=1</p></td>
</tr>
</tbody>
</table>


## Entrer manuellement les composants WebPart Outlook Web App

Les composants WebPart Outlook Web App peuvent également être entrés manuellement dans un navigateur web. Par exemple, un utilisateur peut se servir d’une URL de composant WebPart Outlook Web App pour ouvrir le calendrier d’un autre utilisateur.

Les exemples ci-dessous montrent comment accéder directement aux affichages courants d’Outlook Web App :

  - **Boîte de réception :**  https://*\<server name\>*/owa/?cmd=contents\&module=inbox

  - **Calendrier (aujourd’hui) :** https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&exsvurl=1

  - **Calendrier (semaine) :**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=weekly\&exsvurl=1

  - **Calendrier (mois) :**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=monthly\&exsvurl=1

## Pour plus d'informations

  - [Personnaliser les pages de connexion, de sélection de la langue et d’erreur pour Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Création d’un thème pour Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

