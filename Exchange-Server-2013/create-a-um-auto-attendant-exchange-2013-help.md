---
title: 'Créer un standard automatique de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer un standard automatique de messagerie unifiée
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50478496
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: HT
---

# Créer un standard automatique de messagerie unifiée

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-03-08_

Après avoir créé un standard automatique de messagerie unifiée, les appels entrants via le numéro de téléphone externe, auxquels répond normalement un opérateur humain, reçoivent une réponse du standard automatique. Contrairement aux autres composants de messagerie unifiée, tels que les plans de numérotation de messagerie unifiée et les passerelles IP de messagerie unifiée, vous n'êtes pas obligé de créer des standards automatiques de messagerie unifiée. Toutefois, les standards automatiques aident des appelants internes et externes à localiser des utilisateurs ou départements d'une organisation et à leur transférer des appels.

Pour découvrir d'autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Standards automatiques de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Avant d'exécuter ces procédures, vérifiez qu'un plan de numérotation de messagerie unifiée a été créé. Pour obtenir la procédure détaillée, consultez la rubrique [Créer un plan de numérotation de messagerie unifiée](https://docs.microsoft.com/fr-fr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]
> Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (CAE) pour créer un standard automatique de messagerie unifiée

1.  
    
    Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, sélectionnez le plan de numérotation pour lequel vous voulez ajouter un standard automatique, puis cliquez sur **Modifier**![Icône Modifier](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icône Modifier").

2.  Dans la page **Plan de numérotation de messagerie unifiée**, sous **Standards automatiques de messagerie unifiée**, cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

3.  Dans la page **Nouvelle standard automatique de messagerie unifiée**, entrez les informations suivantes :
    
      - **Nom**   Ce champ permet de créer le nom complet du standard automatique de messagerie unifiée. Un nom de standard automatique de messagerie unifiée est obligatoire et doit être unique. Toutefois, il est uniquement utilisé à des fins d'affichage dans l'EAC et le Shell.
        
        Si vous devez modifier le nom complet du standard automatique après sa création, vous devez d'abord supprimer le standard automatique de messagerie unifiée existant, puis créer un autre standard automatique avec le nom approprié. Si votre organisation utilise plusieurs standards automatiques de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour vos standards automatiques de messagerie unifiée. La longueur maximale d'un nom de standard automatique de messagerie unifiée est de 64 caractères pouvant contenir des espaces.
        
        Bien que vous puissiez nommer un nouveau standard automatique de messagerie unifiée pour inclure des espaces, si vous intégrez la messagerie unifiée à Office Communications Server 2007 R2 ou à Microsoft Lync Server, le nom du standard automatique ne peut pas contenir d'espaces. Par conséquent, si vous avez créé un standard automatique dont le nom complet comprend des espaces et que vous voulez l'intégrer à Office Communications Server 2007 R2 ou Lync Server, vous devez d'abord supprimer ce standard automatique, puis en créer un nouveau qui n'inclut pas d'espaces dans le nom complet.
    
      - **Créer le standard automatique comme activé**   Cochez cette case à la fin de l'exécution de l'Assistant Nouveau standard automatique de messagerie unifiée pour permettre au standard automatique de répondre aux appels entrants. Par défaut, un nouveau standard automatique est créé comme désactivé.
        
        Si vous décidez de créer un standard automatique de messagerie unifiée comme désactivé, vous pouvez utiliser le Centre d'administration Exchange (CAE) ou l'environnement de ligne de commande Exchange Management Shell pour activer le standard automatique une fois l'Assistant terminé.
    
      - **Définissez le standard automatique pour répondre aux commandes vocales**   Cochez cette case pour que le standard automatique de messagerie unifiée puisse utiliser la reconnaissance vocale. Si la reconnaissance vocale est activée pour le standard automatique, les appelants répondent aux invites personnalisées ou système utilisées par le standard automatique de messagerie unifiée en utilisant des entrées vocales ou à tonalité. Par défaut, le standard automatique n'est pas à reconnaissance vocale au moment de sa création.
        
        Pour que les appelants puissent utiliser un standard automatique à reconnaissance vocale, vous devez installer le module linguistique de messagerie unifiée approprié qui prend en charge la reconnaissance vocale automatique, puis configurer les propriétés du standard automatique pour utiliser cette langue.
    
      - **Numéros d'accès**   Ce champ permet d'entrer les numéros de poste ou de téléphone que les appelants utilisent pour atteindre le standard automatique. Tapez un numéro de poste ou un numéro de téléphone dans ce champ, puis cliquez sur **Ajouter**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter") pour ajouter le numéro à la liste. Le nombre de chiffres du numéro de poste ou du numéro de téléphone que vous composez ne doit pas correspondre au nombre de chiffres d'un numéro de poste configuré dans le plan de numérotation de messagerie unifiée associé. En effet, les appels directs sont permis aux standards automatiques de messagerie unifiée.
        
        Le nombre de numéros de poste ou de téléphone entrés est illimité. Toutefois, vous pouvez créer un standard automatique sans numéro de poste répertorié. Aucun numéro de poste ou numéro de téléphone n'est requis.
        
        Vous pouvez modifier ou supprimer un numéro de poste ou de téléphone existant. Pour modifier un numéro de poste ou un numéro de téléphone existant, cliquez sur **Modifier**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter"). Pour supprimer un numéro de poste existant ou un numéro de téléphone de la liste, cliquez sur **Supprimer**![Icône Suppression](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icône Suppression").

4.  Cliquez sur **Enregistrer**.

## Utilisation de l'environnement Shell pour créer un standard automatique de messagerie unifiée

Cet exemple crée un standard automatique de messagerie unifiée nommé `MyUMAutoAttendant` pouvant accepter des appels entrants mais qui n'est pas activé pour la reconnaissance vocale.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

Cet exemple crée un standard automatique de messagerie unifiée à reconnaissance vocale nommé `MyUMAutoAttendant`.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

