---
title: "Activ. le transfert d’appels pour utlsr de messagerie voc.: Exchange 2013 Help | Microsoft Docs"
TOCTitle: Activation du transfert d'appels pour des utilisateurs de messagerie vocale
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50555359
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Activation du transfert d'appels pour des utilisateurs de messagerie vocale

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

La fonctionnalité Règles de répondeur automatique a été introduite pour la première fois dans Exchange 2010. Grâce à cette fonctionnalité, les utilisateurs à extension messagerie vocale peuvent déterminer le mode de traitement de leurs appels entrants. Les règles de répondeur automatique et les règles de boîte de réception sont appliquées de la même manière aux appels entrants et aux messages électroniques entrants.

Les règles de répondeur automatique sont créées et configurées par un utilisateur à extension messagerie vocale à l'aide d'Outlook ou d'Outlook Web App. Ces règles sont stockées avec d'autres paramètres vocaux dans la boîte aux lettres de l'utilisateur. Pour chaque boîte aux lettres à extension messagerie unifiée, vous pouvez configurer jusqu'à neuf règles de répondeur automatique. Ces règles sont indépendantes des règles de boîte de réception qui sont paramétrées par les utilisateurs et n'utilisent pas une partie du quota de stockage des règles de boîte de réception pour l'utilisateur.

Par défaut, quand la messagerie unifiée et la messagerie vocale sont activées pour un utilisateur, aucune règle de répondeur automatique n'est configurée. Si le système de messagerie vocale répond à un appel entrant, l'appelant est invité à laisser un message vocal ou si l'appelant ne reçoit pas d'invite, il peut également laisser un message vocal à l'utilisateur.

Si les utilisateurs souhaitent uniquement que le système de messagerie vocale réponde à leurs appels entrants et enregistre un message vocal, il est inutile de créer des règles de répondeur automatique. En revanche, si vous décidez de configurer des conditions et des actions, vous pouvez le faire dans la section **Règles de répondeur automatique** dans la page **Messagerie vocale** dans Outlook Web App. Utilisez la section **Règles de répondeur automatique** pour créer, modifier et supprimer des règles de répondeur automatique.

## Anatomie des règles de répondeur automatique

Une règle de répondeur automatique se compose de deux parties : les conditions et les actions. Vous pouvez associer une ou plusieurs conditions à une seule règle de répondeur automatique. La règle de répondeur automatique ne sera traitée que si toutes les conditions de cette règle sont respectées. Vous pouvez également associer une ou plusieurs actions à une seule règle de répondeur automatique. Ces actions décident des possibilités qui s'offrent à la partie appelante quand la règle de répondeur automatique est appliquée.

Les règles de répondeur automatique prennent en charge les conditions suivantes :

  - Qui envoie l'appel entrant

  - L'heure du jour

  - Disponibilité sur Calendrier

  - Si les réponses automatiques sont ou non activées pour le courrier électronique

Les actions suivantes sont prises en charge :

  - Me joindre

  - Transférer l'appelant vers quelqu'un d'autre

  - Laisser un message vocal

Si un utilisateur enregistre un message personnalisé pour une règle de répondeur automatique, il doit inclure l'option de menu correspondant à ce message personnalisé lors de la configuration de la règle de répondeur automatique. Dans le cas contraire, la messagerie unifiée ne génère pas d'invite de menu indiquant à l'appelant les choix qui lui sont offerts. Une fois que le message d'accueil personnalisé est lu, le serveur attend la réaction de l'appelant. Si aucune option de menu n'est indiquée par le message, il ne saisira rien et le serveur lui demandera « Êtes-vous toujours là ? »

## Conditions

Les conditions sont des règles que vous pouvez appliquer aux règles de répondeur automatique. En combinant les conditions, vous pouvez créer plusieurs règles de répondeur automatique qui se déclencheront lorsque les conditions seront remplies. Pour créer une règle par défaut applicable à chaque appel, il suffit de créer une règle qui ne contient pas de conditions.

Quand vous configurez des règles de répondeur automatique, vous pouvez utiliser les trois conditions suivantes :

  - ID de l'appelant

  - Heure du jour

  - Informations de disponibilité

## Actions

Les actions servent à définir ce que vous voulez qu'il se passe lorsqu'une condition est remplie. Les deux types d'actions sont les suivants :

  - Me joindre

  - Transfert d'appel

**Ajout d'une action Me contacter**

Quand un appelant sélectionne Me contacter, le système de messagerie vocale essaie de vous contacter sur deux numéros de téléphone différents au maximum, puis vous passe l'appelant si vous êtes disponible à l'un de ces numéros.

  - Vous pouvez spécifier le texte qui sera lu à l'appelant. Par exemple, si vous sélectionnez « Affaires urgentes » pour informer vos correspondants qu'ils ne doivent sélectionner cette action que pour parler d'un problème urgent avec vous, la messagerie vocale diffusera le message « Pour les affaires urgentes, appuyez sur la touche1 ».

  - Vous devez associer l'action Me contacter au numéro sur le clavier du téléphone sur lequel l'appelant devra appuyer pour sélectionner cette action. Dans l'exemple ci-dessous, la touche de téléphone **1** est le numéro sur lequel appuieront les appelants pour vous joindre à l'un des numéros de téléphone que vous avez indiqués.

  - Ensuite, vous devez spécifier le ou les deux numéros de téléphone que le système de messagerie vocale composera. Si vous spécifiez deux numéros de téléphone, le deuxième numéro sera composé si vous n'êtes pas joignable au premier. Chaque numéro de téléphone que vous spécifiez est associé à une durée. Cette durée est la période de temps pendant laquelle la messagerie vocale essaie de composer le numéro de téléphone avant de passer au numéro suivant. Ou si vous n'êtes pas joignable, la messagerie vocale reviendra au menu d'options.

  - Une fois que vous avez entré ces informations, cliquez sur **Appliquer** pour enregistrer les paramètres de recherche.

**Ajout d'actions de transfert d'appel**

En définissant une option de transfert d'appel, vous offrez à l'appelant la possibilité d'être transféré vers le numéro de téléphone d'une autre personne. Plusieurs options vous permettent de transférer un appel entrant vers un autre numéro de téléphone ou contact.

  - Vous pouvez spécifier le texte qui sera lu à l'appelant. Par exemple, vous pouvez entrer « Affaires importantes » pour informer vos correspondants qu'ils doivent sélectionner cette action si un problème important est la raison de leur appel et s'ils ont besoin de parler à quelqu'un.

  - Vous devez associer l'action **Transfert d'appel** au numéro sur le clavier du téléphone sur lequel l'appelant appuiera pour sélectionner cette action.

  - Lorsque vous sélectionnez l'action de transfert d'appel, vous devez spécifier une personne ou un numéro de téléphone vers laquelle/lequel l'appelant sera transféré. Vous pouvez choisir un numéro de téléphone ou sélectionner un contact à appeler lorsque l'appelant appuie sur la bonne touche sur le clavier du téléphone. Si vous désignez un contact enregistré dans l'annuaire de votre entreprise, la messagerie vocale essaiera de transférer l'appel vers le numéro de poste de ce contact.

  - Outre l'indication d'un correspondant ou d'un numéro vers lequel l'appelant sera transféré, vous devez également spécifier le numéro sur le clavier sur lequel l'appelant appuiera pour sélectionner l'action de Transfert d'appel.

  - Une fois que vous avez entré ces informations, cliquez sur **Appliquer** pour enregistrer les paramètres de transfert d'appel.

## Sélection d'une règle de répondeur automatique pour chaque appel entrant

Après avoir créé et configuré des règles de répondeur automatique, la messagerie unifiée pourra :

1.  Déterminer si l'utilisateur a créé des règles de répondeur automatique. Dans le cas contraire, la messagerie unifiée offrira à l'utilisateur la possibilité de laisser un message vocal.

2.  Si au moins une règle de répondeur automatique a été configurée, la messagerie unifiée les évaluera chacune. La première règle dont les conditions sont respectées est traitée.

3.  Après avoir évalué toutes les règles, si la messagerie unifiée n'en trouve aucune dont les conditions sont respectées, la messagerie unifiée demandera à l'appelant de laisser un message vocal.

## Règles de numérotation

Selon la configuration d'une règle de répondeur automatique, un appel entrant peut générer un transfert d'appel. Si cela se produit, le numéro cible du transfert sera soumis aux règles de numérotation, et aux restrictions de la stratégie de boîte aux lettres de messagerie unifiée à laquelle la partie appelée est associée. Pour plus d'informations sur les règles d'automate d'appels et de numérotation ainsi que sur les restrictions, consultez la rubrique [Autoriser les utilisateurs à effectuer des appels](allow-users-to-make-calls-exchange-2013-help.md).

## Activation/désactivation des règles de répondeur automatique

Par défaut, les règles de répondeur automatique sont automatiquement activées pour les utilisateurs à extension messagerie unifiée. Toutefois, il est possible de désactiver les règles de répondeur automatique pour les utilisateurs en désactivant la fonctionnalité sur une stratégie de boîte aux lettres de messagerie unifiée ou la boîte aux lettres de l'utilisateur. Pour plus d'informations sur l'activation ou la désactivation des règles de répondeur automatique, consultez les rubriques suivantes :

  - [Activation ou désactivation de la création de règles de répondeur automatique par des utilisateurs de la même stratégie de boîte aux lettres de messagerie unifiée](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [Autoriser ou empêcher un utilisateur de créer des règles de répondeur automatique d'appel](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)

