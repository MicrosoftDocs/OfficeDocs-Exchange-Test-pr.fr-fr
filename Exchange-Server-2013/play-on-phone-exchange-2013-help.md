---
title: 'Émettre au téléphone: Exchange 2013 Help'
TOCTitle: Émettre au téléphone
ms:assetid: 511e4950-340a-48cc-a020-35d11e76b993
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn205136(v=EXCHG.150)
ms:contentKeyID: 54652731
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Émettre au téléphone

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-25_

Après l'arrivée d'un message vocal, les utilisateurs peuvent choisir d'écouter ce dernier à l'aide des haut-parleurs ou du casque de leur ordinateur ou d'utiliser la fonctionnalité Lire sur le téléphone. La fonctionnalité Lire sur le téléphone est incluse dans Microsoft Outlook et Outlook Web App, et les paramètres de cette fonctionnalité se trouvent dans la section **Lire sur le téléphone** sous les options **Messagerie vocale**. Cette rubrique décrit la manière dont un utilisateur à extension messagerie unifiée peut utiliser la fonctionnalité Lire sur le téléphone.

## Qu'est-ce que la fonctionnalité Lire sur le téléphone ?

La fonctionnalité Lire sur le téléphone permet aux utilisateurs à extension messagerie unifiée de lire les messages vocaux au téléphone. Dans certaines situations (environnement de travail organisé en box, utilisation d'un ordinateur public, ordinateur ne permettant pas de lire des fichiers multimédias ou réception d'un message confidentiel), il se peut qu'un utilisateur à extension messagerie unifiée ne souhaite ou ne puisse pas lire un message vocal sur les haut-parleurs de son ordinateur. L'utilisateur peut alors lire le message vocal en utilisant un téléphone (privé ou professionnel) ou un téléphone mobile. Pour passer en revue les paramètres de la fonctionnalité Lire sur le téléphone, dans Outlook, accédez à **Fichier** \> **Informations** \> **Gérer la messagerie vocale**. En cliquant sur le bouton **Gérer la messagerie vocale**, vous vous connecterez automatiquement à Outlook Web App. Vous pouvez également vous connecter à Outlook Web App à l'aide d'un navigateur web. Dans Outlook Web App, accédez à la section **Options** \> **Téléphone** \> **Messagerie vocale** \> **Lire sur le téléphone** dans la page **Messagerie vocale**.

Quand l'utilisateur clique sur l'option de la barre d'outils Lire sur le téléphone de l'écran de la messagerie vocale, la boîte de dialogue **Lire sur le téléphone** s'ouvre. La boîte de dialogue **Lire sur le téléphone** fournit les commandes permettant de sélectionner ou d'entrer le numéro de téléphone à utiliser pour lire un message vocal, de démarrer ou de terminer un appel et d'afficher un message d'état pour analyser l'appel. Si l'utilisateur est lié à un plan de numérotation URI SIP, son adresse SIP apparaît dans la boîte de dialogue **Composer**. S'il est lié à un plan de numérotation E.164, son numéro E.164 complet apparaît dans la boîte de dialogue **Composer**.

> [!NOTE]
> Un seul message vocal peut être lu à la fois. Si l'utilisateur tente de démarrer un second appel Lire sur le téléphone alors qu'un appel est déjà en cours, un message d'erreur s'affiche.


## Liste des numéros de téléphone les plus récemment utilisés

Les utilisateurs ont accès à une liste de numéros de téléphone qu'ils ont le plus utilisés dernièrement dans la boîte de dialogue **Composer**. Le numéro de téléphone spécifié dans la section **Lire sur le téléphone** est toujours affiché en première position et est automatiquement sélectionné comme numéro principal de l'utilisateur. Les utilisateurs peuvent se servir du menu déroulant pour sélectionner d'autres numéros de téléphone à composer à la place du numéro de téléphone configuré comme numéro principal.

> [!NOTE]
> Pour permettre aux utilisateurs qui utilisent la fonctionnalité Lire sur le téléphone de composer un numéro de téléphone externe sans utiliser de code d'accès à une ligne extérieure, par exemple 425-555-1234 au lieu de 9-425-555-1234, configurez des règles de numérotation des appels nationaux sur un plan de numérotation de messagerie unifiée incluant la ligne suivante : group1, 9xxxxxxxxxx, 91xxxxxxxxxx. Après avoir configuré les règles de numérotation du pays ou du département, ajoutez cette liste à la stratégie de boîte aux lettres de messagerie unifiée.


## Boutons Lire sur le téléphone

La boîte de dialogue **Lire sur le téléphone** permet aux utilisateurs de **Composer** et de **Raccrocher**. Lors de la première ouverture de la boîte de dialogue **Lire sur le téléphone**, le bouton **Composer** est activé et le bouton **Raccrocher** est désactivé. Une fois l'appel passé, le bouton **Composer** est désactivé jusqu'à la fin de l'appel. Vous pouvez mettre fin à l'appel en cliquant sur le bouton **Raccrocher** ou en raccrochant physiquement le téléphone. La fermeture de la boîte de dialogue **Lire sur le téléphone** à l'aide du bouton **Fermer** met fin à un éventuel appel en cours. L'option **Lire sur le téléphone** et d'autres options sont également disponibles dans l'aperçu du **volet de lecture** dans Outlook. Si vous ouvrez le message vocal dans une autre fenêtre, le bouton **Lire sur le téléphone** se situe dans la barre d'outils.

## Section Objet, Envoyé et État

La section inférieure de la boîte de dialogue **Lire sur le téléphone** affiche l'objet du message vocal, les date et heure d'envoi, ainsi qu'un message indiquant l'état actuel de l'appel. Toute erreur spécifique à l'opération Lire sur le téléphone est affichée dans cette section de la boîte de dialogue **Lire sur le téléphone**.

## Validation du numéro de téléphone

La fonctionnalité Lire sur le téléphone ne réalise qu'une simple validation lors de l'entrée de données dans la boîte de dialogue **Lire sur le téléphone**. La fonctionnalité Lire sur le téléphone ne valide pas les numéros de téléphone. Si un numéro de téléphone est incorrect, la messagerie unifiée renvoie un code d'erreur explicatif à l'utilisateur.

