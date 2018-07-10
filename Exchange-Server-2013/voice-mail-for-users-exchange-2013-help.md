---
title: 'Messagerie vocale pour les utilisateurs: Exchange 2013 Help'
TOCTitle: Messagerie vocale pour les utilisateurs
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 50478083
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Messagerie vocale pour les utilisateurs

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-02-19_

Grace à la messagerie unifiée, les utilisateurs de l'organisation Exchange peuvent recevoir tous leurs messages électroniques et messages vocaux dans une seule boîte aux lettres. La fonctionnalité de messagerie unifiée et les fonctions de messagerie vocale augmentent sensiblement la productivité de l’utilisateur et active une messagerie plus flexible au sein d’une organisation.

Lorsque vous ajoutez un utilisateur à votre organisation, vous avez la possibilité de créer une boîte aux lettres ou de connecter l'utilisateur à une boîte aux lettres existante. Une fois la boîte aux lettres créée pour l'utilisateur ou une fois l'utilisateur connecté à une boîte aux lettres existante, vous pouvez activer la boîte aux lettres pour la messagerie unifiée de sorte que l'utilisateur puisse utiliser le système de messagerie vocale et les fonctions inclues à la messagerie vocale. Une fois que la messagerie unifiée est activée pour l’utilisateur, tous les messages électroniques, messages vocaux et télécopies sont transmis dans sa boîte de réception. En utilisant Microsoft Office Outlook 2007 ou des versions ultérieures, Outlook Web App, un téléphone mobile activé pour Microsoft ExchangeActiveSync ou un téléphone standard ou mobile, l’utilisateur a accès à ses messages électroniques et vocaux, à ses contacts personnels ainsi qu’aux informations de calendrier.

**Table des matières**

Propriétés de la messagerie vocale utilisateur

La relation entre un utilisateur de messagerie vocale et autres composants de messagerie unifiée

Numéros de postes et adresses SIP

Utilisation du centre d'administration Exchange pour activer un utilisateur pour la messagerie unifiée et la messagerie vocale

Utiliser le Shell pour activer un utilisateur pour la messagerie unifiée et la messagerie vocale

Désactivation de la messagerie unifiée pour un utilisateur

## Propriétés de la messagerie vocale utilisateur

Un utilisateur doit disposer d'une boîte aux lettres avant de pouvoir être activé pour la messagerie unifiée. Mais, par défaut, un utilisateur qui dispose d’une boîte aux lettres n’est pas activé pour la messagerie unifiée. Une fois que l'utilisateur dispose de l'extension messagerie unifiée, vous pouvez gérer, modifier et configurer les propriétés de la messagerie unifiée et les fonctions de messagerie vocale pour l'utilisateur. Vous pouvez activer un utilisateur pour la messagerie unifiée au moyen de l'EAC ou du Shell. Pour plus d’informations, consultez la rubrique [Activation de la messagerie vocale pour un utilisateur](enable-a-user-for-voice-mail-exchange-2013-help.md). Pour activer plusieurs utilisateurs de messagerie unifiée, utilisez l'EAC ou la cmdlet **Enable-UMMailbox** dans l’environnement Exchange Management Shell.

## La relation entre un utilisateur de messagerie vocale et autres composants de messagerie unifiée

Lorsque vous activez un utilisateur pour la messagerie unifiée, ce dernier doit être associé ou lié à une stratégie de boîte aux lettres de messagerie unifiée existante, et vous devez fournir son numéro de poste. Vous pouvez associer un utilisateur à une stratégie de boîte aux lettres de messagerie unifiée en utilisant la cmdlet **Enable-UMMailbox** ou le Shell ou en sélectionnant la stratégie de boîtes aux lettres de messagerie unifiée lors de l'activation de l'utilisateur pour la messagerie unifiée. Par défaut, lorsque vous créez un plan de numérotation de messagerie unifiée, une nouvelle stratégie de boîte aux lettres de messagerie unifiée est créée. Cette stratégie peut être modifiée ou une autre stratégie peut être créée et liée au plan de numérotation pour déterminer les fonctions et les paramètres à appliquer à un utilisateur ou à un groupe d'utilisateurs.

Une stratégie de boîte aux lettres de messagerie unifiée contient des paramètres tels que les restrictions de numérotation et les stratégies de code confidentiel pour un utilisateur. Lors de sa création, la stratégie de boîte aux lettres de messagerie unifiée doit être associée à un plan de numérotation de messagerie unifiée. Tout serveur d'accès au client ou de boîtes aux lettres peut répondre aux appels entrants et fournir des services de messagerie vocale pour tout utilisateur à extension messagerie lié au plan de numérotation de messagerie unifiée. Une fois que la messagerie unifiée est activée pour l’utilisateur, les paramètres d’une stratégie de boîte aux lettres de messagerie unifiée s’appliquent à ce dernier.

## Numéros de postes et adresses SIP

Lorsque vous activez un utilisateur pour la messagerie unifiée, vous devez définir au moins un numéro de poste qui sera utilisé par la messagerie unifiée pour remettre des messages vocaux à la boîte aux lettres de l’utilisateur. Une fois l’utilisateur activé pour la messagerie unifiée, vous pouvez ajouter des numéros de postes secondaires à la boîte aux lettres de l’utilisateur, les modifier ou les supprimer en configurant l’adresse proxy de messagerie unifiée Exchange (adresse proxy EUM) sur la boîte aux lettres de l'utilisateur ou ajouter ou supprimer des postes secondaires pour l’utilisateur dans le centre d'administration Exchange. Vous pouvez supprimer le numéro de poste principal dans l'EAC en supprimant l'adresse proxy EUM. Cependant, il est recommandé de ne pas le supprimer. La suppression du numéro de poste principal ne permet pas la transmission correcte des appels vers la boîte aux lettres de l'utilisateur.

> [!NOTE]
> Il n'existe pas de limite au nombre de numéros de poste secondaires que vous pouvez ajouter pour l'utilisateur à extension messagerie unifiée, mais il ne peut y avoir qu'un seul numéro de poste principal par utilisateur.


La boîte aux lettres d’un utilisateur à extension messagerie unifiée ne peut être associée qu’à un seul plan de numérotation de messagerie unifiée. L'utilisateur à extension messagerie unifiée peut toutefois être associée à :

  - un seul numéro de poste principal, une adresse SIP (Session Initiation Protocol) ou une adresse E.164 dans un plan de numérotation unique.

  - plusieurs numéros de postes secondaires, adresses SIP ou adresses E.164 dans un plan de numérotation unique.

  - plusieurs numéros de postes principaux, adresses SIP ou adresses E.164 dans deux plans de numérotation distincts.

> [!NOTE]
> Chaque numéro de poste, adresse SIP et numéro E.164 doit être unique au sein du plan de numérotation et le nombre de chiffres du plan de numérotation sera utilisé pour tous les utilisateurs liés au plan de numérotation.


Prenons l’exemple d’un utilisateur à extension messagerie unifiée qui voyage fréquemment entre New York et Tokyo. La boîte aux lettres de l’utilisateur est associée au plan de numérotation de New York et un seul numéro de poste est configuré sur sa boîte aux lettres. Un deuxième numéro de poste est configuré sur la boîte aux lettres de l’utilisateur pour le plan de numérotation de Tokyo. Lorsque des appelants composent l’un des numéros de postes et laissent un message vocal à l’utilisateur, le message vocal est remis à la même boîte aux lettres à extension messagerie unifiée.

Retour au début

## Utilisation du centre d'administration Exchange pour activer un utilisateur pour la messagerie unifiée et la messagerie vocale

Après avoir créé une boîte aux lettres Exchange pour l'utilisateur, vous pouvez configurer les paramètres de la boîte aux lettres de messagerie unifiée en utilisant **Afficher les détails** sous **Messagerie unifiée** dans l'EAC. Lorsque vous activez un utilisateur, il existe plusieurs paramètres à configurer :

1.  **Adresse SIP**   il s'agit de l'adresse SIP de l'utilisateur. Vous trouverez ces paramètres si une stratégie de boîtes aux lettres de messagerie unifiée qui est liée à un plan de numérotation SIP URI est attribuée à l'utilisateur que vous activez pour la messagerie unifiée. Les plans de numérotation SIP URI sont utilisés lorsque vous intégrez Office Communications Server 2007 R2 ou Microsoft Lync Server. Lorsque vous attribuez à l’utilisateur une stratégie de boîte aux lettres de messagerie unifiée qui est associée à un URI SIP ou un plan de numérotation E.164, vous devez toujours entrer un numéro de poste pour l’utilisateur. Le numéro de poste principal est utilisé par l'utilisateur pour accéder à Outlook Voice Access.

2.  **Numéro de poste**   Vous devez entrer manuellement le numéro de poste pour l'utilisateur que vous activez pour la messagerie unifiée.
    
    Vous devez indiquer un numéro de poste valide pour l’utilisateur ; le numéro doit comporter le nombre de chiffres spécifié dans le plan de numérotation. Vous ne pouvez entrer que des caractères numériques ou des chiffres de 1 à 20. Le numéro de poste type est composé de 3 à 7 chiffres et est configuré sur le plan de numérotation auquel la stratégie de boîte aux lettres est liée et à partir duquel elle est attribuée à l'utilisateur.

3.  **Paramètres de code confidentiel pour l'utilisateur :** 
    
      - **Code confidentiel configuré automatiquement**   Ce paramètre génère automatiquement un code confidentiel pour l'utilisateur à extension messagerie à utiliser pour l'accès à la messagerie vocale via Outlook Voice Access. Il s’agit du paramètre par défaut. Lorsque vous cliquez sur ce bouton, un code confidentiel est automatiquement généré d’après les stratégies de code confidentiel configurées dans la stratégie de boîte aux lettres de messagerie unifiée attribuée à l’utilisateur. Il est recommandé d’utiliser ce paramètre afin de protéger le code confidentiel de l’utilisateur. Le code confidentiel est envoyé à l’utilisateur dans le message de bienvenue qu’il reçoit après avoir été activé pour la messagerie unifiée. Par défaut, il devra modifier ce code confidentiel lorsqu’il se connecte pour la première fois à sa boîte aux lettres pour accéder à sa messagerie vocale.
    
      - **Entrer un code confidentiel**   Ce paramètre permet de spécifier manuellement un code confidentiel que l'utilisateur utilisera pour accéder au système de messagerie vocale.
        
        Le code confidentiel doit être conforme aux paramètres de stratégie de code confidentiel configurés dans la stratégie de boîtes aux lettres de messagerie unifiée associée à cet utilisateur à extension messagerie. Par exemple, si la stratégie de boîte aux lettres de messagerie unifiée est configurée pour accepter uniquement les codes confidentiels contenant au moins sept chiffres, le code confidentiel entré dans ce champ doit comporter au moins sept chiffres.
    
      - **exiger que l'utilisateur réinitialise son code confidentiel à la première connexion**   Ce paramètre oblige l'utilisateur à réinitialiser son code confidentiel de messagerie vocale lorsqu'il accède au système de messagerie vocale depuis un téléphone en utilisant Outlook Voice Access pour la première fois. Il sera invité à saisir un code confidentiel avec lequel il est davantage familiarisé. Cette meilleure pratique de sécurité contraint les utilisateurs à extension messagerie unifiée à modifier leur code confidentiel lorsqu’ils se connectent pour la première fois pour se protéger contre les accès autorisés à leurs données et à leur boîte de réception. Cette case à cocher est activée par défaut.

## Utiliser le Shell pour activer un utilisateur pour la messagerie unifiée et la messagerie vocale

Cet exemple active la messagerie unifiée et la messagerie vocale sur la boîte aux lettres de jccolon@contoso.com, définit le poste et règle manuellement le code confidentiel de l'utilisateur, puis affecte une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` à l'utilisateur.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

Cet exemple active la messagerie unifiée et la messagerie vocale sur la boîte aux lettres de jccolon@contoso.com, affecte une stratégie de boîte aux lettres de messagerie unifiée nommée `MyUMMailboxPolicy` à l'utilisateur et définit le numéro de poste, l'adresse SIP et définit manuellement le code confidentiel pour l'utilisateur.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## Désactivation de la messagerie unifiée pour un utilisateur

Lorsque vous désactivez la messagerie unifiée pour un utilisateur, le compte d’utilisateur peut encore être affiché lorsqu’un appelant effectue une recherche dans l’annuaire à l’aide d’un menu de standard automatique de messagerie unifiée ou à l’aide d’Outlook Voice Access. L’appelant peut localiser un utilisateur dans l’annuaire, mais lorsqu’il essaie de le contacter, il est ramené au menu principal de la messagerie unifiée. Les appelants peuvent être incommodés par le système à cause de ça. Vous pouvez empêcher les appelants d’utiliser la recherche dans l’annuaire pour contacter un utilisateur qui a été désactivé pour la messagerie unifiée en connectant l’utilisateur à un autre système de messagerie vocale, en supprimant l’utilisateur de la recherche dans l’annuaire de standard automatique de messagerie unifiée ou en supprimant le compte de l’utilisateur.

Après qu’un compte d’utilisateur à extension messagerie unifiée a été désactivé pour la messagerie unifiée, il se peut que cet utilisateur puisse encore accéder à sa boîte aux lettres personnelle à extension messagerie unifiée via Outlook Voice Access ou Microsoft Outlook. Cela peut se produire lorsque toutes les modifications ne sont pas cohérentes dans le répertoire. Afin de réduire le risque qu’un utilisateur ait accès à sa boîte aux lettres même si son compte a été désactivé pour la messagerie unifiée, vous pouvez obliger manuellement la réplication à se produire ou supprimer toutes les informations de messagerie unifiée de la boîte aux lettres de l’utilisateur une fois ce dernier désactivé pour la messagerie unifiée.

