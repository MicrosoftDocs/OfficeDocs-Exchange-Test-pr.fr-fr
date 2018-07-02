---
title: 'Message d’accueil, annonces, menus et invites: Exchange 2013 Help'
TOCTitle: Message d’accueil, annonces, menus et invites
ms:assetid: df61105d-c9d8-452c-b028-50cbda47aecf
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124902(v=EXCHG.150)
ms:contentKeyID: 54652781
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Message d’accueil, annonces, menus et invites

 

_**Sapplique à :**Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-03-09_

Lors de l'installation de la messagerie unifiée, un jeu courant de fichiers audio par défaut est utilisé pour le système de messagerie vocale ainsi que les invites de menu et les messages d'accueil, et des messages d'information automatiques sont installés. Même si vous pouvez créer un standard automatique de messagerie unifiée complet ou un plan de numérotation qui utilise uniquement les messages audio par défaut, ces derniers sont trop génériques pour constituer une interface publique acceptable pour de nombreuses sociétés. Cette rubrique présente les invites système et de menu, les messages d'accueil et les messages d'information automatiques utilisés par les plans de numérotation et les standards automatiques de messagerie unifiée, ainsi que leur utilisation lorsque les appelants accèdent au système de messagerie unifiée.

**Contenu de cette rubrique**

Vue d'ensemble des invites audio et des messages d'accueil

Invites système

Messages d'accueil et annonces des plans de numérotation de messagerie unifiée

Messages d'accueil, annonces et invites de menu des standards automatiques de messagerie unifiée

Messages d'accueil, annonces et invites de menu personnalisés, et menus de navigation

## Vue d'ensemble des invites audio et des messages d'accueil

Une fois la messagerie unifiée installée, les fichiers audio pour les plans de numérotation et les standards automatiques de messagerie unifiée sont copiés sur le serveur de boîtes aux lettres. Par défaut, le programme d'installation copie les fichiers audio dans le dossier Program Files\\Microsoft\\Exchange Server\\V15\\Unified Messaging\\Prompts*\\\<langue\>*. Si vous avez installé la version en anglais (É.U.), un dossier nommé \\en est créé au cours de l'installation pour conserver les versions en anglais É.U des invites système. Le serveur de boîtes aux lettres lit ces invites aux appelants pour qu'ils puissent entendre les messages d'accueil, les invites de menu et les messages d'information automatiques, et ainsi naviguer dans les menus de la messagerie unifiée.

Ces fichiers ou invites audio de système ne doivent pas être remplacés. Toutefois, la messagerie unifiée vous permet de personnaliser les messages d'accueil, les invites de menu et les messages d'information automatiques des plans de numérotation et des standards automatiques de messagerie unifiée.

Le tableau suivant détaille les invites et les messages d'accueil utilisés avec les plans de numérotation de messagerie unifiée.

### Invites audio des plans de numérotation de messagerie unifiée

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Invites et messages d'accueil</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Invites système</p></td>
<td><p>Ne doivent pas être modifiées.</p></td>
</tr>
<tr class="even">
<td><p>Message d'accueil</p></td>
<td><p>Le message d'accueil par défaut est une invite du système lue par défaut. Vous pouvez toutefois utiliser un fichier d'accueil personnalisé que vous créez.</p></td>
</tr>
<tr class="odd">
<td><p>Message d'information automatique</p></td>
<td><p>Par défaut, les messages d'information automatiques sont désactivés. Si vous activez un message d'information automatique, vous devez spécifier un fichier de message d'accueil personnalisé.</p></td>
</tr>
</tbody>
</table>


Le tableau suivant détaille les invites et les messages d'accueil utilisés avec les standards automatiques de messagerie unifiée.

### Invites audio pour les standards automatiques de messagerie unifiée

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Invites et messages d'accueil</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Invites système</p></td>
<td><p>Ne doivent pas être modifiées.</p></td>
</tr>
<tr class="even">
<td><p>Invites de menu pendant les heures d'ouverture</p></td>
<td><p>Par défaut, les invites de menu pendant les heures d'ouverture sont activées et une invite du système est lue. Vous pouvez toutefois utiliser un fichier d'accueil personnalisé que vous créez.</p></td>
</tr>
<tr class="odd">
<td><p>Invites de menu en dehors des heures d'ouverture.</p></td>
<td><p>Par défaut, les invites de menu en dehors des heures d'ouverture sont activées et une invite du système est lue. Vous pouvez toutefois utiliser un fichier d'accueil personnalisé que vous créez.</p></td>
</tr>
<tr class="even">
<td><p>Message d'accueil pendant les heures d'ouverture</p></td>
<td><p>Par défaut, un message d'accueil pendant les heures d'ouverture est activé et une invite du système est lue. Vous pouvez toutefois utiliser un fichier d'accueil personnalisé que vous créez. Ce message est également appelé message d'accueil.</p></td>
</tr>
<tr class="odd">
<td><p>Message d'accueil en dehors des heures d'ouverture</p></td>
<td><p>Par défaut, un message d'accueil en dehors des heures d'ouverture est activé et une invite du système est lue. Vous pouvez toutefois utiliser un fichier d'accueil personnalisé que vous créez. Ce message est également appelé message d'accueil.</p></td>
</tr>
<tr class="even">
<td><p>Message d'information automatique</p></td>
<td><p>Par défaut, les messages d'information automatiques sont désactivés. Si vous activez un message d'information automatique, vous devez spécifier un fichier de message d'accueil personnalisé.</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification des messages d'assistance vocale système installés n'est pas prise en charge.</td>
</tr>
</tbody>
</table>


Vue d'ensemble des invites audio et des messages d'accueil

## Invites système

La messagerie unifiée est installée avec un ensemble d'invites audio par défaut à utiliser avec Outlook Voice Access, les plans de numérotation et les standards automatiques. Des centaines d'invites système pour chaque langue sont installées sur le serveur de boîtes aux lettres. Le serveur de boîtes aux lettres lit les fichiers audio de ces invites système aux appelants quand ils accèdent au système de messagerie vocale. Voici quelques exemples de ces invites système :

  - « Entrez votre code confidentiel. »

  - « Pour accéder à votre boîte aux lettres, entrez votre poste. »

  - « Pour contacter quelqu'un, appuyez sur la touche dièse. »

  - « Épelez le nom de la personne que vous appelez, en commençant par le nom. »

  - « Pour joindre une personne, dites son nom. »

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification des invites système installées n'est pas prise en charge.</td>
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
<td>Lorsque le service de messagerie unifiée démarre sur le serveur de boîtes aux lettres, il vérifie que toutes les invites système sont disponibles. Si une invite du système est introuvable, la messagerie unifiée renvoie un message d'erreur. Pour corriger cette erreur, recherchez l'événement à l'aide de l'Observateur d'événements et copiez le fichier correspondant dans la fenêtre <strong>Propriétés des événements</strong> du DVD d'installation vers le dossier approprié sur le serveur de boîtes aux lettres.</td>
</tr>
</tbody>
</table>


## Messages d'accueil et annonces des plans de numérotation de messagerie unifiée

Après avoir installé un serveur de boîtes aux lettres et créé un plan de numérotation de messagerie unifiée, vous avez la possibilité d'utiliser les fichiers audio des invites système par défaut créés lors de l'installation ou de créer des fichiers personnalisés utilisables avec des plans de numérotation de messagerie unifiée.

Les plans de numérotation de messagerie unifiée contiennent un message d'accueil et message d'information automatique facultatif que vous pouvez modifier. Le message d'accueil est utilisé quand un utilisateur d'Outlook Voice Access ou un autre appelant appelle le numéro d'accès d'abonné. Les appelants entendent le message d'accueil par défaut, « Bienvenue, vous êtes connecté à MicrosoftExchange ». Vous pouvez modifier ce message d'accueil par défaut afin de le personnaliser pour votre société, par exemple, « Bienvenue sur Outlook Voice Access pour Woodgrove Bank ». Si vous décidez de personnaliser ce message d'accueil, vous devez d'abord enregistrer un message personnalisé, l'enregistrer en tant que fichier .wav, puis configurer le plan de numérotation pour qu'il utilise ce message personnalisé.

La messagerie unifiée permet de faire suivre le message d'accueil d'un message d'information automatique. Par défaut, aucun message d'information automatique n'est configuré. Toutefois, vous pouvez en fournir une pour les appelants. Vous pouvez utiliser le message d'information automatique pour les annonces générales qui changent plus souvent que le message d'accueil ou pour les annonces requises par les stratégies de conformité d'entreprise. S'il est important que les appelants entendent le message d'information automatique dans son intégralité, vous pouvez le configurer comme ne pouvant pas être interrompu. Cela empêche les appelants d'appuyer sur une touche ou d'énoncer une commande qui interrompe et mette fin au message d'information automatique.

Le tableau suivant décrit les messages d'accueil et les messages d'information automatiques des plans de numérotation de messagerie unifiée.

### Messages d'accueil et messages d'information automatiques des plans de numérotation de messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Message d'accueil</th>
<th>Exemple par défaut</th>
<th>Exemple personnalisé</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Message d'accueil</p></td>
<td><p>« Bienvenue, vous êtes connecté à MicrosoftExchange. »</p></td>
<td><p>« Bienvenue sur Outlook Voice Access pour Woodgrove Bank. »</p></td>
</tr>
<tr class="even">
<td><p>Message d'information automatique</p></td>
<td><p>Par défaut, aucun message d'information automatique n'est configuré.</p></td>
<td><p>« En utilisant ce système, vous acceptez d'adhérer à toutes les stratégies d'entreprise lors de l'accès au système. »</p></td>
</tr>
</tbody>
</table>


Lorsque vous personnalisez et configurez les messages d'accueil et les annonces ayant valeur d'informations, assurez-vous que le paramètre de langue configuré sur le plan de numérotation de messagerie unifiée est le même que la langue des invites personnalisées que vous créez. Sinon, un appelant pourrait entendre un message ou message d'accueil dans une langue, et un autre message ou message d'accueil dans une autre langue.

Vue d'ensemble des invites audio et des messages d'accueil

## Messages d'accueil, annonces et invites de menu des standards automatiques de messagerie unifiée

Comme les plans de numérotation de messagerie unifiée, les standards automatiques de messagerie unifiée possèdent un message d'accueil, un message d'information automatique facultatif et une invite de menu personnalisée facultative. Vous pouvez configurer différentes versions du message d'accueil et de l'invite de menu pendant les heures d'ouverture et en dehors de celles-ci. Vous pouvez toutes les modifier.

Le message d'accueil est la première chose que l'appelant entend quand un standard automatique de messagerie unifiée répond à son appel. Par défaut, celui-ci dit, « Bienvenue sur le standard automatique MicrosoftExchange. » Le fichier audio lu pour l'appel est l'invite du système par défaut pour le standard automatique de messagerie unifiée. Toutefois, vous pouvez personnaliser ce message d'accueil pour représenter votre société, par exemple, « Merci d'avoir appelé Woodgrove Bank. ». Pour personnaliser ce message d'accueil, enregistrez le message personnalisé, enregistrez-le en tant que fichier .wav, puis configurez le standard automatique pour qu'il utilise ce message personnalisé. Vous pouvez également personnaliser les invites de menu.

La messagerie unifiée permet également de faire suivre un message d'accueil durant les heures d'ouverture ou en dehors des heures d'ouverture d'un message d'information automatique. Par défaut, aucun message d'information automatique n'est configuré, mais vous pouvez en fournir une aux appelants. Le message d'information automatique peut rappeler les heures d'ouverture de votre société, par exemple, « Nous sommes ouverts de 8h00 à 17h00, du lundi au vendredi, et de 8h30 à 13h00 le samedi. » Le message d'information automatique peut également fournir des informations requises conformément à la stratégie d'entreprise, par exemple : « Les appels peuvent être analysés à des fins de formation. ». S'il est important que les appelants entendent le message d'information automatique dans son intégralité, vous pouvez le configurer comme ne pouvant pas être interrompu. Cela empêche l'appelant d'appuyer sur une touche ou d'énoncer une commande qui interrompe et mette fin au message d'information automatique.

Le tableau suivant décrit les messages d'accueil et les messages d'information automatiques des standards automatiques de messagerie unifiée.

### Messages d'accueil, messages d'information automatiques et invites de menu des standards automatiques de messagerie unifiée

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Message d'accueil</th>
<th>Exemple par défaut</th>
<th>Exemple personnalisé</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Message d'accueil pendant les heures d'ouverture</p></td>
<td><p>« Bienvenue sur le standard automatique Microsoft Exchange. »</p></td>
<td><p>« Merci d'avoir appelé Woodgrove Bank. »</p></td>
</tr>
<tr class="even">
<td><p>Message d'accueil en dehors des heures d'ouverture</p></td>
<td><p>Aucun message d'accueil par défaut pendant les heures d'ouverture n'est lu tant que vous n'avez pas configuré le standard automatique. Toutefois, le message d'accueil par défaut pendant les heures d'ouverture est lu aux appelants toute la journée.</p></td>
<td><p>« Vous avez appelé Woodgrove Bank en dehors des heures d'ouverture. Nous sommes ouverts de 8h00 à 17h00 du lundi au vendredi. »</p></td>
</tr>
<tr class="odd">
<td><p>Message d'information automatique</p></td>
<td><p>Par défaut, aucun message d'information automatique n'est configuré.</p></td>
<td><p>« Les appels peuvent être analysés à des fins de formation. »</p></td>
</tr>
<tr class="even">
<td><p>Invite du menu principal pendant les heures d'ouverture</p></td>
<td><p>Aucune invite de menu pendant les heures d'ouverture par défaut n'est lue tant que vous n'avez pas configuré les mappages de touches du standard automatique.</p></td>
<td><p>« Pour le support technique, appuyez sur 1 ou dites 1. Pour les services d'administration, appuyez sur 2 ou dites 2. Pour le service des ventes, appuyez sur 3 ou dites 3. »</p></td>
</tr>
<tr class="odd">
<td><p>Invite du menu principal en dehors des heures d'ouverture</p></td>
<td><p>Aucune invite du menu principal en dehors des heures d'ouverture par défaut n'est lue tant que vous n'avez pas configuré les mappages de touches et les heures d'ouverture sur le standard automatique.</p></td>
<td><p>« Votre appel est important pour nous. Toutefois, vous appelez Woodgrove Bank en dehors de nos heures d'ouverture. Si vous voulez laisser un message, appuyez sur 1 ou dites 1 et nous vous rappellerons dès que possible. »</p></td>
</tr>
</tbody>
</table>


Comme pour les plans de numérotation de messagerie unifiée, assurez-vous que le paramètre de langue configuré sur le standard automatique de messagerie unifiée est le même que la langue des messages d'accueil personnalisés que vous créez et qu'il est défini sur la même langue que le plan de numérotation de messagerie unifiée. Sinon, un appelant pourrait entendre un message ou message d'accueil dans une langue, et un autre message ou message d'accueil dans une autre langue.

Vue d'ensemble des invites audio et des messages d'accueil

## Messages d'accueil, annonces et invites de menu personnalisés, et menus de navigation

Bien que les messages d'assistance vocale du système ne doivent pas être remplacés ou modifiés, vous pouvez cependant personnaliser les messages d'accueil, les messages d'information automatiques, les invites de menu et les menus de navigation utilisés avec les plans de numérotation et les standards automatiques de messagerie unifiée. Suite à l'installation, vous pouvez configurer les plans de numérotation de messagerie unifiée et les standards automatiques pour qu'ils utilisent des fichiers audio personnalisés (.wav ou .wma). Procédez comme suit pour activer les invites vocales personnalisées à l'intention des appelants :

1.  Enregistrez les messages d'accueil, les annonces et les invites personnalisés et enregistrez-les en tant que fichiers .wav. Le codec audio Linear PCM (16 bits/échantillon), 8 kilohertz (KHz), doit être utilisé pour coder les fichiers .wav. Si vous n'utilisez pas ce format spécifique pour les fichiers .wav, une erreur est générée indiquant que le format du fichier source n'est pas pris en charge. Bien qu'une erreur soit générée, celle-ci n'apparaît pas dans l'Observateur d'événements.

2.  Configurez le plan de numérotation ou le standard automatique de messagerie unifiée pour qu'il utilise les messages d'accueil, les annonces et les invites personnalisés.

Par défaut, lorsque vous créez un standard automatique de messagerie unifiée, les messages d'assistance vocale ou messages d'accueil pendant ou en dehors des heures d'ouverture ne sont pas configurés et aucun mappage de touches n'est défini pour les messages d'assistance vocale de menu principal pendant ou en dehors des heures d'ouverture. Pour configurer correctement des messages d'accueil et des invites personnalisés pour un standard de messagerie automatique, vous devez :

  - configurer les heures d'ouverture et de fermeture dans la page **Heures d'ouverture** ;

  - créer les fichiers (.wav ou .wma) audio d'accueil à utiliser pour les messages d'accueil pendant et en dehors des heures d'ouverture ;

  - configurer les messages d'accueil pendant et en dehors des heures d'ouverture dans la page **Messages d'accueil** ;

  - créer les fichiers de message d'accueil à utiliser pour les messages d'accueil de menu principal pendant et en dehors des heures d'ouverture ;

  - configurer le message d'accueil de menu principal pendant et en dehors des heures d'ouverture dans la page **Messages d'accueil** ;

  - activer et configurer la navigation de menu pendant et en dehors des heures d'ouverture dans la page **Navigation de menu**.

Vue d'ensemble des invites audio et des messages d'accueil

