---
title: 'Créer un plan de numérotation de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Créer un plan de numérotation de messagerie unifiée
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50478742
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: HT
---

# Créer un plan de numérotation de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2013-04-16_

Un plan de numérotation de messagerie unifiée contient des informations de configuration relatives à votre réseau téléphonique. Un plan de numérotation de messagerie unifiée établit un lien entre le numéro de poste téléphonique d'un utilisateur à extension messagerie vocale et sa boîte aux lettres. Lorsque vous créez un plan de numérotation de messagerie unifiée, vous pouvez configurer le nombre de chiffres des numéros de postes, le type d'URI (Uniform Resource Identifier) et les paramètres de sécurité VoIP (Voice over IP) pour le plan de numérotation.

Lorsque vous créez un plan de numérotation de messagerie unifiée, une stratégie de boîte aux lettres de messagerie unifiée est également créée. La stratégie de la boîte aux lettres de messagerie unifiée est nommée Stratégie par défaut \<*DialPlanName*\>.

Pour les autres tâches de gestion relatives aux plans de numérotation de messagerie unifiée, consultez la rubrique [Procédures de plan de numérotation de messagerie unifiée](um-dial-plan-procedures-exchange-2013-help.md).

## Ce qu'il faut savoir avant de commencer

  - Durée d'exécution estimée : 3 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l'entrée « Plans de numérotation de messagerie unifiée » dans la rubrique [Autorisations de messagerie unifiée](unified-messaging-permissions-exchange-2013-help.md).

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser le Centre d'administration Exchange (EAC) pour créer un plan de numérotation de messagerie unifiée

1.  
    
    Dans le CAE, accédez à **Messagerie unifiée** \> **Plans de numérotation de messagerie unifiée**, puis cliquez sur **Nouveau**![Icône Ajouter](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icône Ajouter").

2.  Dans la page **Nouveau plan de numérotation de messagerie unifiée**, complétez les champs suivants :
    
      - **Nom**   Tapez le nom du plan de numérotation. Un nom de plan de numérotation de messagerie unifiée est obligatoire et doit être unique. Toutefois, il est uniquement utilisé à des fins d'affichage dans le CAE et l'environnement Shell. Si vous devez modifier le nom complet du plan de numérotation après sa création, vous devez d'abord supprimer le plan de numérotation de messagerie unifiée existant, puis créer un autre plan de numérotation avec le nom approprié. Si votre organisation utilise plusieurs plans de numérotation de messagerie unifiée, nous vous recommandons d'utiliser des noms significatifs pour vos plans de numérotation de messagerie unifiée. La longueur maximale d'un nom de plan de numérotation de messagerie unifiée est de 64 caractères pouvant contenir des espaces. Toutefois, il ne peut contenir aucun des caractères suivants : " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Un nom de plan de numérotation de messagerie unifiée peut contenir des espaces, sauf dans le cas où vous intégrez la messagerie unifiée à Office Communications Server 2007 R2 ou à Microsoft Lync Server. Par conséquent, si vous avez créé un plan de numérotation dont le nom complet comprend des espaces et que vous souhaitez l'intégrer à Office Communications Server 2007 R2 ou Microsoft Lync Server, vous devez d'abord supprimer ce plan de numérotation, puis en créer un dont le nom complet ne comporte pas d'espaces.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Bien que le champ destiné au nom du plan de numérotation puisse accepter 64 caractères, la longueur du nom du plan de numérotation ne peut pas être supérieure à 49 caractères. Si vous tentez de créer un nom de plan de numérotation contenant plus de 49 caractères, un message d'erreur s'affiche. Ce message indique que la stratégie de boîte aux lettres de messagerie unifiée n'a pas pu être générée parce que le nom du plan de numérotation de messagerie unifiée est trop long. En effet, comme évoqué précédemment, lorsque vous créez un plan de numérotation, une stratégie de boîte aux lettres de messagerie unifiée par défaut nommée Stratégie par défaut <em>&lt;DialPlanName&gt;</em> est également créée. Après l'ajout des 15 caractères de la stratégie par défaut au nom du plan de numérotation, le nombre total de caractères dépasse la limite. Le paramètre <em>name</em> des plans de numérotation de messagerie unifiée et des stratégies de boîte aux lettres de messagerie unifiée peut comporter jusqu'à 64 caractères. Toutefois, si le nom du plan de numérotation comporte plus de 49 caractères, le nom de la stratégie de boîte aux lettres de messagerie unifiée par défaut sera supérieur à 64 caractères, ce qui n'est pas permis par le système.</td>
        </tr>
        </tbody>
        </table>
    
      - **Longueur des numéros de poste (chiffres)**   Entrez le nombre de chiffres pour le plan de numérotation. Le nombre de chiffres des numéros de poste est basé sur le plan de numérotation téléphonique créé sur un PBX (Private Branch eXchange) ou un PBX IP. Par exemple, si un utilisateur associé à un plan de numérotation téléphonique compose un poste à 4 chiffres pour appeler un autre utilisateur du même plan de numérotation téléphonique, vous sélectionnez 4 pour le nombre de chiffres du poste.
        
        Ce champ est obligatoire et sa plage de valeurs s'étend de 1 à 20. La longueur de poste classique est comprise entre 3 et 7 chiffres. Si votre environnement téléphonique existant inclut des numéros de postes, vous devez spécifier un nombre de chiffres correspondant au nombre de chiffres de ces postes.
        
        Lorsque vous créez un plan de numérotation SIP (Session Initiation Protocol) ou E.164 et lui associez un utilisateur à extension messagerie unifiée, vous devez toujours entrer le numéro de poste qui sera utilisé par l'utilisateur. Ce numéro de poste est utilisé par des utilisateurs d'Outlook Voice Access pour accéder à leur boîte aux lettres.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Type UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sécurité UI\_VoIP)
    
      - **Langue audio**   Cette liste permet d'indiquer la langue par défaut pour les utilisateurs d'Outlook Voice Access. Ce paramètre ne s'applique pas à la configuration linguistique sur un standard automatique de messagerie unifiée. Vous pouvez définir la même langue ou une langue différente pour Outlook Voice Access et pour un standard automatique de messagerie unifiée. Quand un utilisateur appelle un utilisateur associé à un plan de numérotation, la langue audio est la langue par défaut utilisée par l'opérateur dont la voix a été enregistrée. Les messages système diffusés aux appelants sont également lus dans cette langue. La langue choisie dans le plan de numérotation de messagerie unifiée est utilisée dans différentes circonstances : pour lire les éléments de calendrier, de messagerie vocale et de courrier électronique, pour prononcer le nom de l'utilisateur si aucun message d'accueil personnel n'a été enregistré, pour transcrire un message vocal à l'aide de la fonctionnalité d'aperçu du message vocal et pour permettre le bon fonctionnement de la reconnaissance vocale.
    
      - **Code de pays/région**   Ce champ permet d'entrer le code numérique du pays/de la région à utiliser pour les appels sortants. Ce numéro précèdera le numéro de téléphone composé. Ce champ peut recevoir 1 à 4 chiffres. Par exemple, aux États-Unis, le code du pays/de la région est 1. Au Royaume-Uni, ce code est 44.

3.  Cliquez sur **Enregistrer**.

## Utilisation de l'environnement de ligne de commande pour créer un plan de numérotation de messagerie unifiée

Cet exemple crée un plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` qui utilise des numéros de poste à quatre chiffres.

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

Cet exemple crée un nouveau plan de numérotation de messagerie unifiée nommé `MyUMDialPlan` qui utilise des numéros de poste à cinq chiffres et qui prend en charge les URI SIP.

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

