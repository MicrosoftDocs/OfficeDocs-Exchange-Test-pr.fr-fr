---
title: 'Activer la transcription des msg vocaux pour les utlsr: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Activer la transcription des messages vocaux pour les utilisateurs
ms:assetid: c5192e05-905c-440f-beec-1f697edc15b3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff629381(v=EXCHG.150)
ms:contentKeyID: 51407235
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activer la transcription des messages vocaux pour les utilisateurs

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2016-12-09_

La fonctionnalité Aperçu de messagerie vocale est destinée aux utilisateurs qui reçoivent leurs messages vocaux à partir de la messagerie unifiée. Grâce à une version texte des enregistrements audio, elle améliore les fonctionnalités de messagerie vocale existantes de la messagerie unifiée. Le texte du message vocal est affiché dans des messages électroniques dans MicrosoftOutlook Web App, Outlook 2010 ou une version ultérieure, ainsi que dans d'autres programmes de messagerie pris en charge. Pour plus d'informations, consultez le site consacré aux [technologies vocales de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348).

## Les utilisateurs doivent-ils utiliser un programme de messagerie électronique spécifique ?

Non. L'aperçu de messagerie vocale est intégré dans le texte de corps du message de n'importe quel programme de messagerie, y compris les programmes mobiles. Bien qu'il soit possible pour les utilisateurs de faire appel à d'autres programmes de messagerie pour la réception de messages vocaux, Outlook et Outlook Web App offrent les meilleurs résultats. Par exemple, dans Outlook 2010 et les versions ultérieures, quand vous cliquez sur un mot en particulier dans le texte d'aperçu du message vocal, la lecture audio du message vocal débute à partir de ce mot. Cette fonction est très utile si vous souhaitez écouter une portion précise d'un message vocal.

## Les utilisateurs peuvent-ils rechercher des messages vocaux spécifiques ?

Oui. Les mots et les expressions dans l'aperçu de messagerie vocale sont automatiquement indexés pour permettre l'affichage des messages vocaux dans les résultats de la recherche. Dans Outlook 2010 et les versions ultérieures ou dans Outlook Web App, les utilisateurs peuvent également exploiter la zone **Notes audio** pour ajouter le texte d'un message vocal. Ces notes apparaissent aussi dans les recherches pour faciliter la localisation d'un message.

## Pourquoi cette fonctionnalité s'appelle-t-elle « Aperçu de messagerie vocale » ?

Il est primordial d'identifier comme il se doit les exigences des utilisateurs. L'aperçu de messagerie vocale ne génère pas nécessairement un texte identique à celui que laissent les appelants dans leurs messages vocaux. En fait, il est généralement, et pour ainsi dire, inexact. L'utilisation du terme « transcription » sous-entendrait qu'un affichage plus fidèle est généralement garanti. Le terme « aperçu » suggère que l'utilisateur doit être capable de comprendre le sens général du contenu vocal, ce qui est beaucoup plus proche de la fonction réelle de l'outil.

## Quels sont les éléments qui rendent l'aperçu du texte des messages vocaux plus ou moins inexact ?

La précision du texte d'aperçu des messages vocaux dépend de nombreux facteurs qui, parfois, ne peuvent être contrôlés. Néanmoins, la précision de l'aperçu est plus facilement garantie dans les conditions suivantes :

  - L'appelant laisse un message vocal simple sans termes argotiques, sans jargon technique ou sans expressions ou termes inhabituels.

  - L'appelant adopte un langage facile à identifier et que le système de message vocale peut aisément interpréter. En règle générale, les messages vocaux laissés par des appelants qui ne s'expriment pas dans un langage ni trop rapide, ni trop lent et avec un accent trop prononcé, produiront des phrases et des expressions d'une plus grande clarté.

  - Le message vocal ne contient pas de bruit de fond et d'écho, et la qualité audio est régulière.

## Quelles langues peuvent être utilisées avec la fonctionnalité Aperçu de messagerie vocale ?

La visualisation du texte d'aperçu de messagerie vocale est possible dans les langues suivantes :

  - Anglais (États-Unis) - (en-US)

  - Anglais (Canada) - (en-CA)

  - Français (France) - (fr-FR)

  - Italien (it-IT)

  - Polonais (pl-PL)

  - Portugais (Portugal) (pt-PT)

  - Espagnol (Espagne) - (es-ES)

Si la messagerie vocale est installée dans un déploiement local ou hybride, vous pouvez télécharger les modules linguistiques pour la messagerie unifiée à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/?linkid=266542).

Si vous avez un déploiement local ou hybride, après l'installation d'un module linguistique, vous pouvez configurer les plans de numérotation et les standards automatique de manière à utiliser la langue que vous avez choisie. Pour les clients en ligne, il n'est pas nécessaire d'installer de module linguistique pour la messagerie unifiée. De nombreuses sociétés disposent d'un seul plan de numérotation de messagerie unifiée. La messagerie unifiée tentera de générer un aperçu du message vocal dans la langue par défaut du plan de numérotation, mais cette opération ne réussira que si la langue par défaut prend en charge l'aperçu de messagerie vocale. Un plan de numérotation de messagerie unifiée peut uniquement être configuré pour la création d'aperçus de la messagerie vocale dans une langue à la fois.

Pour configurer la messagerie unifiée et créer des aperçus de la messagerie vocale dans une langue autre que l'anglais des États-Unis (en-US), procédez comme suit :

1.  Vérifiez que la fonctionnalité Aperçu de messagerie vocale est prise en charge dans la langue de votre choix.

2.  Si vous avez un déploiement local ou hybride, téléchargez et installez le module linguistique approprié pour la messagerie vocale. Le téléchargement et l'installation du module linguistique n'impliquent pas la configuration de la langue par défaut du plan de numérotation.

3.  Configurez le plan de numérotation avec la langue à utiliser dans l'aperçu de messagerie vocale. Pour plus d'informations, consultez la rubrique [Définir la langue par défaut sur un plan de numérotation](set-the-default-language-on-a-dial-plan-exchange-2013-help.md).

La manière dont l'aperçu de messagerie vocale affiche le texte dans les langues prises en charge dépend du type de message vocal envoyé. Deux types sont à distinguer :

  - **Les messages vocaux enregistrés quand un utilisateur ne répond pas à son téléphone.**
    
    Pour ces messages, la langue employée dans l'aperçu de messagerie vocale est déterminée en fonction de la langue parlée de l'appelant, moyennant la prise en charge de cette dernière. Par exemple, si un appelant laisse un message vocal en italien, le texte d'aperçu de messagerie vocale s'affichera dans cette même langue si celle-ci a été configurée dans le plan de numérotation. En revanche, si le message laissé par l'appelant est en japonais, aucun texte d'aperçu ne sera inclus avec le message, car la langue japonaise n'est pas disponible.

  - **Les messages vocaux envoyés par un utilisateur Outlook Voice Access.**
    
    Pour les messages envoyés par un utilisateur d'Outlook Voice Access, la langue utilisée pour l'aperçu de messagerie vocale est contrôlée par l'administrateur de la messagerie vocale. Ainsi, la langue du texte de l'aperçu du message vocal sera identique à celle du système de messagerie vocale. En revanche, si un appelant parlant une langue non prise en charge pour la fonctionnalité d'aperçu de messagerie vocale utilise Outlook Voice Access pour laisser un message, aucun texte d'aperçu ne sera inséré dans le message. Pour plus d'informations sur Outlook Voice Access, consultez la rubrique [Configuration d’Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## La messagerie vocale sait-elle quand un aperçu est inexact ?

Un niveau de fiabilité est déterminé pour chaque aperçu de messagerie vocale inclus dans un message vocal. Le système de messagerie vocale évalue la correspondance entre l'enregistrement et les mots, les chiffres et les phrases. Si des correspondances sont détectées facilement, le niveau de fiabilité est élevé. Un niveau de fiabilité plus élevé est généralement associé à une plus haute précision.

Si le niveau de fiabilité s'avère inférieur à une valeur donnée, l'expression **Aperçu de messagerie vocale (fiabilité basse)** au-dessus du texte de l'aperçu de messagerie vocale. Si le niveau de fiabilité est faible, il est probable que le texte de l'aperçu manquera de précision.

La messagerie unifiée fait appel à la fonctionnalité de reconnaissance vocale pour calculer la fiabilité dans l'aperçu, mais elle n'a aucun moyen de distinguer les termes incorrects de ceux qui le sont.

La messagerie unifiée s'efforce néanmoins d'améliorer la précision de ses aperçus. Par exemple, elle tente d'établir une correspondance entre le numéro de téléphone de l'appelant (si disponible) et les contacts personnels de l'utilisateur et le carnet d'adresses ou les contacts de réseaux sociaux de votre organisation. Si la messagerie unifiée détecte une correspondance, elle inclura le nom de l'appelant, avec ses listes standard de noms et de mots, au moment d'appliquer l'outil de reconnaissance vocale à l'enregistrement vocal.

## Est-il possible d'utiliser l'aperçu de messagerie vocale s'il n'est pas d'une précision à 100 % ?

Les utilisateurs obtiendront sans doute de meilleurs résultats avec l'aperçu de messagerie vocale s'ils ne lisent pas trop attentivement, mot à mot, l'aperçu. À la place, leur recherche doit se concentrer sur des noms, des numéros de téléphone et des expressions (par exemple, « Rappelez-moi » ou « J'ai besoin de vous parler ») pouvant donner des indications sur les motifs de l'appel.

La fonctionnalité Aperçu de messagerie vocale n'a pas pour but d'énoncer fidèlement des messages mais elle peut aider les utilisateurs à répondre à de multiples questions, notamment :

  - Ce message vocal est-il en rapport avec mon travail ?

  - Revêt-il une importance cruciale pour moi ?

  - L'appelant a-t-il laissé un numéro où le joindre ? Le numéro est-il différent des numéros dont je dispose pour cet appelant ?

  - L'appelant considère-t-il ce message vocal comme urgent ?

  - Dois-je quitter une réunion pour rappeler cette personne ?

  - J'attendais un appel de confirmation de ma demande. S'agit-il de l'appel en question ?

## Est-il possible d'activer ou de désactiver l'aperçu de messagerie vocale ?

Oui. Si vous avez activé la fonctionnalité d'aperçu de messagerie vocale, les utilisateurs peuvent l'activer et la désactiver à volonté à l'aide d'Outlook 2010 ou une version ultérieure ou d'Outlook Web App. Par contre, la langue du plan de numérotation doit prendre en charge cette fonctionnalité et le module linguistique de messagerie unifiée de la langue en question doit être installé.

Bien que les paramètres d'aperçu de messagerie vocale soient les mêmes, que l'utilisateur ait recours à Outlook 2010 ou une version ultérieure ou à Outlook Web App, le mode d'accès sera différent :

**Outlook Web App**

Pour accéder aux paramètres d'aperçu de messagerie vocale dans Outlook Web App, cliquez sur **Paramètres** \> **Téléphone** \> **Messagerie vocale**. Dans la page **Messagerie vocale**, les paramètres sont disponibles sous **Aperçu de messagerie vocale**.

Par défaut, ces deux options de la fenêtre Aperçu de messagerie vocale sont disponibles quand un utilisateur bénéficie de la messagerie unifiée. Si le plan de numérotation de messagerie unifiée est configuré pour l'utilisation d'un module linguistique prenant en charge l'aperçu de messagerie vocale, la messagerie unifiée créera des aperçus pour les utilisateurs dans les cas suivants :

  - Un appelant laisse un message vocal parce que l'utilisateur ne répond pas au téléphone.

  - Un utilisateur à extension messagerie unifiée se connecte à Outlook Voice Access et enregistre un message vocal destiné à un ou plusieurs destinataires.

Quand un appelant laisse un message vocal et que l'option **Inclure du texte d'aperçu avec les messages vocaux que je reçois** est sélectionnée, la messagerie unifiée crée un aperçu de message vocal dans le message électronique, il y joint le fichier audio et le transmet vers la boîte aux lettres du destinataire. Vous pouvez choisir de désactiver cette option si la langue configurée dans le plan de numérotation ne prend pas en charge la fonctionnalité d'aperçu de messagerie vocale et si vous ne souhaitez inclure aucun aperçu dans les messages vocaux.

Lorsque des utilisateurs se connectent à Outlook Voice Access et envoient un message vocal à un autre utilisateur, ils peuvent décocher la case **Inclure du texte d'aperçu avec les messages vocaux que j'envoie par le biais d'Outlook Voice Access**. Ils peuvent notamment l'envisager s'ils envoient des messages vocaux dans une langue que l'aperçu de messagerie vocale ne prend pas en charge ou s'ils ne veulent pas inclure l'aperçu dans le message vocal parce qu'il est trop long.

