---
title: 'Langues de messag. unifiée, invites et messages d’accueil: Exchange 2013 Help'
TOCTitle: Langues de messagerie unifiée, invites et messages d’accueil
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50479310
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Langues de messagerie unifiée, invites et messages d’accueil

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

Vous pouvez installer et configurer des modules linguistiques pour prendre en charge plusieurs langues dans des environnements de messagerie unifiée.

Les modules linguistiques de messagerie unifiée permettent aux appelants et aux utilisateurs d'Outlook Voice Access d'interagir avec le système de messagerie unifiée dans plusieurs langues. Après que vous avez installé une langue supplémentaire sur un serveur de boîtes aux lettres, les appelants et les utilisateurs d'Outlook Voice Access ont la possibilité d'écouter les messages électroniques et d'interagir avec le système de messagerie vocale dans cette langue.

Différents composants clés reposent sur des modules linguistiques de messagerie unifiée pour permettre aux utilisateurs et appelants d'interagir efficacement avec la messagerie unifiée dans plusieurs langues. Chaque module linguistique de messagerie unifiée comprend un moteur de synthèse vocale, les invites préenregistrées et la prise en charge de la reconnaissance vocale, ainsi que l'aperçu de messagerie vocale pour une langue spécifique. Cette rubrique présente les modules linguistiques de messagerie unifiée, les composants de messagerie unifiée qui utilisent ces modules linguistiques et la manière dont les modules linguistiques de messagerie unifiée, une fois installés, peuvent être utilisés pour configurer les plans de numérotation de messagerie unifiée et les standards automatiques de messagerie unifiée afin d'utiliser d'autres langues.

Les modules linguistiques de messagerie unifiée Microsoft Exchange sont des composants spécifiques à une version et une plateforme. Depuis Exchange Server 2007, plusieurs versions de modules linguistiques de messagerie unifiée ont été créées, notamment la version finale (RTM) d'Exchange 2007, Exchange 2007 SP1, SP2 et SP3, la version finale d'Exchange Server 2010, Exchange 2010 SP1 et SP2, ainsi que d'Exchange 2013. Pour certaines de ces versions, les téléchargements 32 et 64 bits sont disponibles mais pour d'autres, uniquement les téléchargements 64 bits sont disponibles.

Il est primordial d'installer la version et la plateforme correctes des modules linguistiques de messagerie unifiée sur un serveur de boîtes aux lettres. N'installez pas des modules linguistiques de messagerie unifiée sur un serveur de boîtes aux lettres qui exécute une version antérieure d'Exchange ou qui est conçu pour une plateforme 32 bits.

**Contenu de cette rubrique**

Présentation des modules linguistiques de messagerie unifiée

Composants et fonctionnalités de la langue de messagerie unifiée

Aperçu de messagerie vocale

Langues de messagerie unifiée

Modules linguistiques de messagerie unifiée

Langues de plan de numérotation de messagerie unifiée

Langues de standard automatique de messagerie unifiée

Processus de sélection de la langue du client

## Présentation des modules linguistiques de messagerie unifiée

Les modules linguistiques de messagerie unifiée permettent à un serveur de boîtes aux lettres d'utiliser des langues supplémentaires avec les appelants et de reconnaître leur langue lors de l'utilisation de la reconnaissance vocale ou de la transcription des messages vocaux. Les modules linguistiques de messagerie unifiée contiennent :

  - Des messages d'assistance vocaux préenregistrés dans la langue du module linguistique de messagerie unifiée. Par exemple, « Après la tonalité, veuillez enregistrer votre message. Lorsque vous avez terminé, raccrochez ou appuyez sur la touche dièse pour obtenir plus d’options. »

  - Fichiers de grammaire dans la langue du module linguistique de messagerie unifiée utilisés par un serveur de boîtes aux lettres pour vérifier le nom des utilisateurs dans l'annuaire.

  - Conversion de texte par synthèse vocale (TTS) permettant de lire le contenu (message électronique, calendrier, coordonnées, etc.) aux appelants dans la langue du module linguistique de messagerie unifiée.

  - Prise en charge de la reconnaissance vocale automatique (ASR), qui permet aux appelants d'interagir avec la messagerie unifiée à l'aide de l'interface utilisateur vocale dans la langue du module linguistique de messagerie unifiée.

  - Prise en charge de l'aperçu de messagerie vocale, qui permet aux utilisateurs de lire la transcription des messages vocaux dans une langue particulière à partir d'un client de messagerie pris en charge tel qu'Outlook ou Outlook Web App.

Les modules linguistiques de messagerie unifiée comprennent des invites préenregistrées, la prise en charge de la conversion par synthèse vocale pour une langue spécifique et, dans certains cas, la prise en charge de la reconnaissance vocale. Dans les environnements multilingues, vous pouvez être amené à installer des modules linguistiques de messagerie unifiée supplémentaires parce que certains appelants préfèrent entendre des messages dans une autre langue, ou parce qu'ils reçoivent des messages électroniques dans plusieurs langues. Vous devez installer plusieurs modules linguistiques de messagerie unifiée pour prendre en charge la capacité du serveur de boîtes aux lettres à lire un message électronique contenant plusieurs langues, car le système de conversion par synthèse vocale doit savoir quelle langue sélectionner en fonction du texte du message à lire. Si le module linguistique de messagerie unifiée n'a pas été installé, le message électronique n'aura aucune logique ni cohérence quand il sera lu à l'utilisateur. L'installation du module linguistique approprié permet au moteur de synthèse vocale de lire le message électronique et les éléments de calendrier à l'utilisateur d'Outlook Voice Access en utilisant la langue correcte, mais aussi de fournir des invites préenregistrés spécifiques à la langue pour la messagerie unifiée. Dans certains cas, ils peuvent aussi prendre en charge l'ASR.

> [!NOTE]
> Le moteur de synthèse vocale convertit le texte en voix, mais n'opère pas la conversion de voix en texte. Les utilisateurs à extension messagerie unifiée peuvent envoyer un message électronique comportant un fichier vocal joint à un autre utilisateur. Ils ne peuvent cependant pas créer ni envoyer de message électronique texte.


Lorsque vous installez un module linguistique, le programme d'installation effectue les opérations suivantes :

1.  Il copie les messages d'assistance vocaux linguistiques à utiliser pour configurer des plans de numérotation et des standards automatiques de messagerie unifiée.

2.  Il permet au moteur TTS de lire des messages lorsque les utilisateurs d'Outlook Voice Access accèdent à leur boîte de réception.

3.  Il active l'ASR sur les plans de numérotation et les standards automatiques de messagerie unifiée pour la langue installée.

4.  Il active l'aperçu de messagerie vocale pour les clients dans d'autres langues.

Vous pouvez ajouter des modules linguistiques de messagerie unifiée à l’aide de la commande **Setup.exe** ou en exécutant le programme d’installation *\<UMLanguagePack\>*.exe après avoir téléchargé le module linguistique de messagerie unifiée à partir de la page [Exchange Server 2013 UM Language Packs - Français](https://go.microsoft.com/fwlink/p/?linkid=266542). Cependant, vous devez utiliser la commande Setup.exe pour supprimer un module linguistique de messagerie unifiée. Aucune cmdlet de l’environnement de ligne de commande Exchange Management Shell ne permet d’ajouter ou de supprimer des modules linguistiques d’un serveur de boîtes aux lettres. Pour plus d’informations sur l’installation d’un module linguistique de messagerie unifiée, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md). Pour plus d’informations sur la suppression d’un module linguistique de messagerie unifiée, consultez la rubrique [Suppression d'un module linguistique de messagerie unifiée](remove-a-um-language-pack-exchange-2013-help.md).

> [!NOTE]
> Par défaut, le module linguistique anglais (États-Unis) est installé lors de l'installation d'un serveur de boîtes aux lettres. Il ne peut pas être retiré, sauf si vous supprimez le serveur de boîtes aux lettres de l'ordinateur.


Retour au début

Le tableau suivant répertorie les modules linguistiques de messagerie unifiée actuellement disponibles. Il indique également le nom du fichier d'installation de chaque module et l'ID de culture pour chaque langue de la messagerie unifiée.

### Nom du fichier d'installation du module linguistique de messagerie unifiée et ID de culture

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
<th>Langue</th>
<th>Pays/Région</th>
<th>ID de culture</th>
<th>Nom du fichier d'installation</th>
<th>Disponibilité</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalan</p></td>
<td><p>Espagne</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack.ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Chinois (Hong Kong)</p></td>
<td><p>Chine</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack.zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Chinois (simplifié)</p></td>
<td><p>Chine</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Chinois (traditionnel)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Danois</p></td>
<td><p>Danemark</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Néerlandais</p></td>
<td><p>Pays-Bas</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>Australie</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Anglais</p></td>
<td><p>Canada</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>Inde</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack.en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Anglais</p></td>
<td><p>Royaume-Uni</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>États-Unis</p></td>
<td><p>en-US</p></td>
<td><p>Inclus avec l'installation d'un serveur de boîtes aux lettres</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Finnois</p></td>
<td><p>Finlande</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Français</p></td>
<td><p>Canada</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Français</p></td>
<td><p>France</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Allemand</p></td>
<td><p>Allemagne</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Italien</p></td>
<td><p>Italie</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Japonais</p></td>
<td><p>Japon</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Coréen</p></td>
<td><p>Coréen</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Norvégien (bokmal)</p></td>
<td><p>Norvège</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Polonais</p></td>
<td><p>Pologne</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Portugais</p></td>
<td><p>Brésil</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Portugais</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Russe</p></td>
<td><p>Russie</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack.ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Espagnol</p></td>
<td><p>Espagne</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Espagnol</p></td>
<td><p>Mexique</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Suédois</p></td>
<td><p>Suède</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Téléchargement disponible</a></p></td>
</tr>
</tbody>
</table>


Retour au début

## Composants et fonctionnalités de la langue de messagerie unifiée

Différents composants et fonctionnalités clés de la messagerie unifiée permettent aux utilisateurs et aux appelants d'interagir avec un système de messagerie vocale multilingue. Pour que ces composants et fonctionnalités fonctionnent correctement et permettent aux appelants d'interagir avec le système dans différentes langues, les modules linguistiques de messagerie unifiée doivent être installés correctement sur un serveur de boîtes aux lettres.

## Invites préenregistrées

Le rôle serveur de boîtes aux lettres est installé avec un ensemble de fichiers d'invites audio par défaut. Ces fichiers audio contiennent les enregistrements des menus Outlook Voice Access, des messages d'accueil vocaux et des chiffres utilisés par la messagerie unifiée Exchange. Les fichiers audio sont lus par un serveur de boîtes aux lettres aux appelants internes et externes entrants. Nombre de ces fichiers audio sont des invites par défaut qui fournissent aux utilisateurs de l'interface utilisateur de téléphonie et d'Outlook Voice Access les informations nécessaires pour naviguer dans l'interface utilisateur de téléphonie et l'interface utilisateur vocale. Les invites sont situées dans \<*Program Files*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<language\>. Les invites utilisées par le serveur de boîtes aux lettres pour aider les appelants à naviguer dans les menus ne doivent pas être remplacées ou modifiées.

Lorsqu'un module linguistique supplémentaire de messagerie unifiée est installé, les messages d'assistance vocaux préenregistrés pour cette langue sont également installés. Après qu'un module linguistique de messagerie unifiée a été installé, les messages d'assistance vocaux préenregistrés pour cette langue peuvent être utilisés par les plans de numérotation et les standards automatiques de messagerie unifiée.

## Langues de synthèse vocale

La messagerie automatique repose sur un moteur de synthèse vocale. La fonctionnalité TTS est fournie par le service Microsoft Speech Server. Le moteur TTS lit et convertit du texte écrit en son audible qui peut être entendu par un appelant. Le moteur TTS lit et convertit les éléments suivants dans la boîte aux lettres d'un utilisateur :

  - Corps, objet et nom des messages électroniques et vocaux

  - corps, objets, emplacements et noms des éléments de calendrier

  - noms de contacts personnels

  - messages d'accueil vocaux par défaut des utilisateurs

> [!NOTE]
> Après qu'un utilisateur a enregistré les messages d'accueil personnalisés de la messagerie vocale, la version TTS des messages d'accueil de la messagerie vocale n'est plus utilisée.


## Reconnaissance vocale

Outre la synthèse vocale, la reconnaissance vocale est également prise en charge dans la messagerie unifiée. La fonctionnalité ASR est fournie par le service Microsoft Speech Server. La reconnaissance vocale permet aux appelants d'utiliser des commandes vocales pour naviguer dans les menus et interagir avec les éléments de leur boîte aux lettres individuelle, notamment les messages, les contacts personnels et le calendrier. La prise en charge de l'ASR est incluse dans chaque module linguistique.

Retour au début

## Aperçu de messagerie vocale

Les modules linguistiques de messagerie unifiée prennent également en charge l'aperçu de messagerie vocale, qui permet aux utilisateurs d'effectuer un tri rapide de leurs messages vocaux en lisant leurs transcriptions à partir d'un client de messagerie pris en charge, tel qu'Outlook ou Outlook Web App.

Quand un appelant laisse un message électronique à un utilisateur à extension messagerie unifiée, le fichier et une transcription du message vocal sont insérés dans le corps du message vocal envoyé à la boîte aux lettres de l'utilisateur.

Tous les modules linguistiques de messagerie unifiée sont des fichiers uniques qui peuvent être téléchargés. Ces modules linguistiques incluent les messages d'assistance vocaux préenregistrés, les fichiers de grammaire, la conversion de texte par synthèse vocale et la reconnaissance vocale. En revanche, la fonctionnalité d'aperçu de messagerie vocale n'est disponible que pour certaines langues.

Les modules linguistiques de messagerie unifiée suivants prennent en charge l'ensemble des composants et des fonctionnalités, y compris l'aperçu de messagerie vocale :

  - Anglais (États-Unis)-(en-US)

  - Anglais (Canada)-(en-CA)

  - Français (France)-(fr-FR)

  - Italien - (it-IT)

  - Polonais (pl-PL)

  - Portugais (Portugal) (pt-PT)

  - Espagnol (Espagne) (es-ES)

Par défaut, une fois installé, le serveur de boîtes aux lettres envoie des aperçus de messages vocaux à des utilisateurs à extension messagerie unifiée si un module linguistique de messagerie unifiée pris en charge est installé.

Certains partenaires d'aperçu de messagerie vocale de messagerie unifiée prennent en charge la transcription améliorée pour la fonctionnalité d'aperçu de messagerie vocale. Ces partenaires emploient des personnes pour corriger les transcriptions de messagerie vocale qui ont été créées à l'aide de la reconnaissance vocale. Chaque partenaire d'aperçu de messagerie vocale doit satisfaire à un ensemble d'exigences afin d'être agréé et de pouvoir interagir avec la messagerie unifiée.

Si vous estimez que les aperçus de messages vocaux envoyés à vos utilisateurs ne sont pas assez précis, vous pouvez contacter un des partenaires agréés d’aperçu de messagerie vocale répertoriés à la page [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951) et vous inscrire auprès de lui moyennant des frais supplémentaires.

Vous pouvez télécharger les modules linguistiques de messagerie unifiée à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Pour plus d’informations, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md).

## Langues de messagerie unifiée

Pour permettre aux appelants d'utiliser les fonctionnalités multilingues de la messagerie unifiée, vous devez d'abord installer un module linguistique de messagerie unifiée. Ensuite, vous avez la possibilité de configurer d'autres composants de messagerie unifiée.

  - Installez le module linguistique de messagerie unifiée sur les serveurs de boîtes aux lettres de votre organisation.

  - Si nécessaire, configurez la langue par défaut pour un plan de numérotation de messagerie unifiée. Cela permet aux utilisateurs d'Outlook Voice Access associés au plan de numérotation de messagerie unifiée d'utiliser la nouvelle langue lorsqu'ils accèdent à leur boîte aux lettres. Cependant, les utilisateurs peuvent toujours configurer leur paramètre de langue dans les Options Outlook Web App.

  - Si vous devez activer plusieurs langues sur des standards automatiques, configurez le paramètre de langue sur un standard automatique de messagerie unifiée. Par défaut, un standard automatique de messagerie unifiée utilise la langue du plan de numérotation de messagerie unifiée. Toutefois, vous avez la possibilité de modifier ce paramètre et de permettre à des appelants non authentifiés de se connecter à votre organisation et de naviguer dans les menus du standard automatique dans la langue spécifiée pour le standard automatique de messagerie unifiée.

## Modules linguistiques de messagerie unifiée

Installez un module linguistique de messagerie unifiée sur un serveur de boîtes aux lettres à l'aide de Setup.exe. Suite à l'installation, la langue associée au module linguistique est ajoutée à la liste des langues disponibles. Vous pouvez voir les langues installées à l'aide de la cmdlet [Obtenir-UMService](https://technet.microsoft.com/fr-fr/library/jj552407\(v=exchg.150\)) de l'environnement de ligne de commande Exchange Management Shell.

Lors de l’installation du module linguistique de messagerie unifiée, les fichiers utilisés par le moteur de synthèse vocale et les invites préenregistrées pour la langue choisie sont copiés et mis à disposition des utilisateurs qui se connectent au système de messagerie vocale. Vous pouvez télécharger les modules linguistiques de messagerie unifiée à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Pour plus d’informations, consultez la rubrique [Installer un module linguistique de messagerie unifiée](install-a-um-language-pack-exchange-2013-help.md).

## Langues de plan de numérotation de messagerie unifiée

Chaque plan de numérotation de messagerie unifiée créé contient un paramètre de langue par défaut. Le paramètre de langue du plan de numérotation de messagerie unifiée est nécessaire, car la messagerie unifiée peut être amenée à utiliser la conversion de synthèse vocale ou à lire une invite audio standard pour les utilisateurs d'Outlook Voice Access quand ils accèdent à leur boîte aux lettres. Vous n'avez pas besoin de sélectionner une langue de plan de numérotation par défaut.

Lorsque vous installez Exchange, l'anglais (É.U.) est la langue par défaut et la seule option de langue disponible pour votre plan de numérotation. Après que vous avez installé un module linguistique de messagerie unifiée sur un serveur de boîtes aux lettres, la langue associée au module linguistique est aussi répertoriée comme une option disponible lorsque vous configurez la langue par défaut du plan de numérotation.

La langue par défaut est importante pour les appelants. Quand un utilisateur d'Outlook Voice Access appelle le système de messagerie vocale, la langue utilisée dépend du paramètre de langue d'Outlook Web App défini lors de la première connexion de l'utilisateur à sa boîte aux lettres. La messagerie unifiée compare la langue définie dans Outlook Web App à la liste des langues disponibles sur le plan de numérotation auquel l'utilisateur est associé. Si aucune correspondance n'est trouvée, la langue par défaut du plan de numérotation est utilisée. Par exemple, si vous avez un plan de numérotation ne contenant que des utilisateurs de France, vous pouvez modifier le paramètre de la langue par défaut du plan de numérotation en français.

## Langues de standard automatique de messagerie unifiée

Par défaut, comme les standards automatiques de messagerie unifiée sont associés à un plan de numérotation de messagerie unifiée lors de leur création, ils utilisent le paramètre de langue par défaut de ce plan. Cependant, ce paramètre peut être modifié après la création du standard automatique de messagerie unifiée.

Le paramètre de langue du standard automatique de messagerie unifiée est nécessaire parce que la messagerie unifiée peut être amenée à utiliser la conversion TTS ou à lire un message d'assistance vocal standard à un appelant. La messagerie unifiée ne vérifie pas si la langue des messages d'assistance vocaux personnalisés du standard automatique correspond au paramètre de la langue du standard automatique. Toutefois, nous vous recommandons de veiller à ce que le paramètre de langue du standard automatique corresponde à la langue des messages d'assistance vocaux personnalisés. Sinon, l'appelant risque d'entendre le système passer d'une langue à l'autre.

La possibilité de modifier le paramètre de la langue du standard automatique de messagerie unifiée est également utile si vous avez besoin de plusieurs standards automatiques spécifiques à la langue pour les appelants.

## Processus de sélection de la langue du client

Les modules linguistiques de messagerie unifiée permettent aux appelants et aux utilisateurs d'Outlook Voice Access d'interagir avec le système de messagerie unifiée dans plusieurs langues. Après que vous avez installé des modules linguistiques supplémentaires sur un serveur de boîtes aux lettres, les appelants et utilisateurs d'Outlook Voice Access peuvent entendre les messages vocaux et interagir avec le système de messagerie vocale. Les utilisateurs d'Outlook Web App et d'Outlook 2010 ou version ultérieure peuvent voir la transcription d'un message vocal à l'aide de l'aperçu de messagerie vocale dans une langue spécifique.

Pour prendre en charge une langue spécifique, un module linguistique de client de messagerie unifiée pour cette langue doit être installé sur chaque serveur de boîtes aux lettres.

Dans certains cas, si le module linguistique de messagerie unifiée spécifique d’une langue n’a pas été installé et n’est pas disponible, il est possible d’utiliser une langue de base client. Les langues de base client de messagerie unifiée peuvent être utilisées à la place de certaines langues, mais il est possible qu'elles ne soient pas disponibles pour d'autres. Si aucun module linguistique de messagerie unifiée n’est installé pour une langue spécifique et qu’aucune langue de base n’est disponible, l’anglais américain (en-US) est utilisé.

Le tableau suivant comporte une liste des langues client et des langues de base utilisées si aucun module linguistique de messagerie unifiée spécifique n’a été installé sur un serveur de boîtes aux lettres.

### Langues de base client de messagerie unifiée

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Langage</th>
<th>Pays/Région</th>
<th>ID de culture</th>
<th>Première langue choisie, si installée</th>
<th>Deuxième langue choisie, si installée</th>
<th>Troisième langue choisie, si installée</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalan</p></td>
<td><p>Espagne</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chinois (Hong Kong)</p></td>
<td><p>Chine</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>Chinois (simplifié)</p></td>
<td><p>Chine</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>Chinois (traditionnel)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>Danois</p></td>
<td><p>Danemark</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Néerlandais</p></td>
<td><p>Pays-Bas</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>Australie</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Anglais</p></td>
<td><p>Canada</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>Inde</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Anglais</p></td>
<td><p>Royaume-Uni</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Anglais</p></td>
<td><p>États-Unis</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Finnois</p></td>
<td><p>Finlande</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Français</p></td>
<td><p>Canada</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Français</p></td>
<td><p>France</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Allemand</p></td>
<td><p>Allemagne</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Italien</p></td>
<td><p>Italie</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Japonais</p></td>
<td><p>Japon</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Coréen</p></td>
<td><p>Corée</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Norvégien (bokmal)</p></td>
<td><p>Norvège</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Polonais</p></td>
<td><p>Pologne</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Portugais</p></td>
<td><p>Brésil</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Portugais</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Russe</p></td>
<td><p>Russie</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Espagnol</p></td>
<td><p>Espagne</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Espagnol</p></td>
<td><p>Mexique</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Suédois</p></td>
<td><p>Suède</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Retour au début

