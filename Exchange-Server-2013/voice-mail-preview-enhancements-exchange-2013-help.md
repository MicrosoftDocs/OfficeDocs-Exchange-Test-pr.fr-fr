---
title: "Améliorations d'aperçu de messagerie vocale: Exchange 2013 Help"
TOCTitle: Améliorations d'aperçu de messagerie vocale
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 50477744
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Améliorations d'aperçu de messagerie vocale

 

_**Sapplique à :** Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2012-07-05_

La fonctionnalité Aperçu de messagerie vocale est destinée aux utilisateurs qui reçoivent leurs messages vocaux via la messagerie unifiée Microsoft Exchange Server 2010 ou Exchange Server 2013. Grâce à une version texte des enregistrements audio, elle améliore les fonctionnalités de messagerie vocale de la messagerie unifiée. Le texte du message vocal apparaît dans un message électronique dans Microsoft Office Outlook Web App, Outlook 2010 ou d’autres programmes de messagerie.

## Améliorations de la fonction Aperçu de messagerie vocale

Dans Exchange 2013, la messagerie unifiée inclut plusieurs améliorations de l’interface utilisateur pour les clients Outlook Web App et Outlook, ainsi que des améliorations stimulant la confiance et la précision pour la fonction Aperçu de messagerie vocale. De la même façon, les services vocaux ont été améliorés dans Microsoft Speech Platform (Version 11.0) et Unified Communications Managed API (UCMA) 4.0 pour optimiser la génération de la grammaire et la prise en charge linguistique.

La messagerie unifiée a introduit la fonctionnalité Aperçu de messagerie vocale dans Exchange 2010. La fonction Aperçu de messagerie vocale utilise la reconnaissance vocale automatique (ASR) pour ajouter la version texte d’un fichier audio d’un message vocal à un message audio. ASR n’est pas entièrement précis, surtout s’il est utilisé pour enregistrer des sons transmis par téléphone qui incluent des voix et des bruits inconnus.

Certaines organisations nécessitent systématiquement des transcriptions parfaites (ou presque) des messages vocaux pour certains de leurs utilisateurs, voire tous. Le Programme Partenaires de l’aperçu de messagerie vocale aide à satisfaire les exigences de ces organisations. Le Programme Partenaires de l’aperçu de messagerie vocale a été conçu pour Exchange 2010 en vue d’améliorer les résultats de la fonction Aperçu de messagerie vocale, mais les utilisateurs d’Exchange 2010 ne l’ont pas utilisé en raison des frais généraux et des coûts associés. Pour résoudre ce problème, les améliorations de la fonction Aperçu de messagerie vocale apportées par Exchange 2013 sont les suivantes :

  - **Normalisation audio améliorée**   La normalisation audio est le processus consistant à augmenter (ou à réduire) de manière uniforme l’amplitude d’un signal audio entier pour que l’amplitude maximum résultante corresponde à une valeur spécifiée ou à la norme. La messagerie unifiée normalise l’enregistrement audio avant de le compresser et de l’envoyer à l’utilisateur.

  - **Reconnaissance vocale améliorée**   En collectant des messages vocaux (uniquement si l’utilisateur d’Exchange choisit de partager ces informations), les résultats des aperçus de messagerie vocale permettent d’ajouter des mots et des expressions au moteur vocal. Cela est possible en attribuant au paramètre *VoiceMailAnalysisEnabled* la valeur `$true` via la cmdlet **Set-UMMailbox** ou en attribuant au paramètre *AllowVoiceMailAnalysis* la valeur `$true` dans la cmdlet **Set-UMMailboxPolicy**. De la même façon, la messagerie unifiée Exchange 2013 exploite plus efficacement les informations des threads de messagerie créés par un utilisateur d’Outlook Voice Access. Il s’agit là d’informations concernant le participant (contact personnel ou Active Directory), son pays, sa ville, son entreprise, ainsi que le numéro de téléphone de l’utilisateur d’Outlook Voice Access.

  - **Score de confiance de la fonction Aperçu de messagerie vocale**   Le score de confiance correspond au numéro affecté par la messagerie unifiée et directement associé à la précision globale de la transcription. Les calculs d’évaluation du niveau de confiance utilisés par la messagerie unifiée ont été ajustés afin d’être plus précis et de représenter la précision réelle d’un message transcrit.

  - **Filtrage**   Les mots offensifs sont détectés et filtrés et les résultats sont mis en cache et stockés dans la boîte aux lettres de l’utilisateur.

  - **Masquage de l’aperçu du texte**   Si le score de confiance d’un aperçu de messagerie vocale est inférieur à un certain seuil, le texte de la fonction Aperçu de messagerie vocale est masqué. Si le texte est masqué, le message vocal inclut du texte indiquant que le score de confiance du message vocal était trop faible pour permettre l’affichage de résultats.

  - **Performances de la transcription**   La fonction Aperçu de messagerie vocale est une opération sollicitant beaucoup de ressources de l’unité centrale et qui prend environ deux fois plus de temps que le traitement d’un fichier audio. Si la génération du texte de l’aperçu de messagerie vocale prend trop longtemps, la limitation d’unité centrale interrompt le traitement de l’aperçu. Dans Exchange 2010, la messagerie unifiée n’a pas essayé de transcrire les messages vocaux d’une longueur supérieure à 75 secondes. Dans Exchange 2013, le message vocal entier est transcrit, mais le texte du message n’est pas inclus si sa longueur est supérieure à 75 secondes.

  - **Modèles de couleurs**   En raison de la confusion provoquée par les diverses couleurs utilisées pour distinguer les scores faible, moyen et élevé de confiance associés à un aperçu de messagerie vocale, le modèle de couleurs a été supprimé dans Exchange 2013 pour Outlook Web App et Outlook.

