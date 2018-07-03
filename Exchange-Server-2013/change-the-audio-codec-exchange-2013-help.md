---
title: 'Modifier le codec audio: Exchange 2013 Help'
TOCTitle: Modifier le codec audio
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 50477540
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifier le codec audio

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-22_

La messagerie unifiée peut utiliser un codec parmi quatre pour créer des messages vocaux : MP3, Windows Media Audio (WMA), Group System Mobile (GSM) 06.10 et G.711 Pulse Code Modulation (PCM) Linear. Par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, celui-ci utilise le codec audio MP3 pour enregistrer des messages vocaux. Le format audio MP3 est très utilisé par plusieurs systèmes d'exploitation, clients de messageries et lecteurs MP3. Toutefois, après la création du plan de numérotation de messagerie unifiée, vous pouvez le configurer pour utiliser divers formats audio, dont les codecs audio suivants : WMA, GSM 06.10 ou G.711 PCM Linear. Pour pouvoir écouter le message vocal, vous devez installer un logiciel audio compatible sur le téléphone mobile ou l'ordinateur.

Pour les autres tâches relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : moins d'une minute.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez Entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](create-a-um-dial-plan-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange pour modifier le codec audio sur un plan de numérotation de messagerie unifiée

1.  Dans le Centre d'administration Exchange, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**.

2.  Dans l'affichage Liste, sélectionnez le plan de numérotation de messagerie unifiée à modifier, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

3.  Dans la page **Plan de numérotation de messagerie unifiée**, cliquez sur **Configurer**.

4.  Dans **Paramètres**, sous **Codec audio**, utilisez la liste déroulante pour activer une des options suivantes :
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  Cliquez sur **Enregistrer**.

## Utiliser l'environnement Shell pour modifier le codec audio sur un plan de numérotation de messagerie unifiée

Cet exemple définit le codec audio sur un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` pour G.711.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

Cet exemple définit le codec audio sur un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` pour WMA.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

