---
title: "Définition de la sécurité des codes confidentiels d'Outlook Voice Access: Exchange 2013 Help"
TOCTitle: Définition de la sécurité des codes confidentiels d'Outlook Voice Access
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50555510
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Définition de la sécurité des codes confidentiels d'Outlook Voice Access

 

_**Sapplique à :** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :** 2013-04-16_

Quand des utilisateurs de la messagerie unifiée se connectent au système de messagerie vocale au moyen d'un téléphone, ils utilisent Outlook Voice Access pour accéder au système de menus. Pour pouvoir accéder au système de messagerie vocale, le système invite les utilisateurs à entrer leur code confidentiel. En tant qu'administrateur, vous pouvez configurer des paramètres et des critères de code confidentiel et effectuer des tâches de gestion des codes confidentiels. Quand la messagerie unifiée a été activée pour un utilisateur et qu'un code confidentiel a été généré, le code confidentiel est chiffré et stocké dans la boîte aux lettres de l'utilisateur.

> [!NOTE]
> Les utilisateurs d'Outlook Voice Access doivent utiliser des entrées en mode de numérotation multifréquences (également appelé numérotation en fréquences vocales) pour entrer leur code confidentiel et accéder à leur boîte aux lettres à extension messagerie unifiée. La reconnaissance vocale n'est pas disponible pour l'entrée de code confidentiel.


**Contenu de cette rubrique**

Présentation du code confidentiel

Critères de code confidentiel

Gestion des codes confidentiels d'Outlook Voice Access

## Présentation du code confidentiel

Un code confidentiel est une chaîne numérique utilisée dans certains systèmes pour authentifier un utilisateur et lui permettre d'accéder au système. Des codes confidentiels sont le plus souvent utilisés pour les distributeurs automatiques de billets (DAB). Ils sont également utilisés à la place des mots de passe alphanumériques pour les systèmes de messagerie vocale. La force d'un code confidentiel dépend de sa longueur, de son niveau de protection et de la difficulté à le deviner.

Dans la messagerie unifiée, les utilisateurs d'Outlook Voice Access entrent leur code confidentiel sur un téléphone analogique, numérique ou mobile afin de pouvoir accéder aux informations de messagerie électronique, de messagerie vocale, de contacts et de calendrier dans leur boîte aux lettres Exchange Server.

Dans la messagerie unifiée, les stratégies de code confidentiel sont définies et configurées selon une stratégie de boîte aux lettres de messagerie unifiée. Vous pouvez créer plusieurs stratégies de boîte aux lettres de messagerie unifiée selon vos critères. Quand vous activez la messagerie vocale d'un utilisateur, vous liez cet utilisateur à une stratégie de boîte aux lettres de messagerie unifiée existante. Les stratégies de code confidentiel de messagerie unifiée qui sont configurées dans la stratégie de boîte aux lettres de messagerie unifiée doivent être conformes aux critères de sécurité de votre organisation.

## Critères de code confidentiel

Les paramètres de configuration de code confidentiel que vous pouvez définir dans une stratégie de boîte aux lettres de messagerie unifiée sont décrits ci-dessous.

## Longueur minimale du code confidentiel

Le paramètre **Longueur minimale du code confidentiel** indique le nombre minimal de chiffres qu'un code confidentiel de boîte aux lettres doit contenir. La valeur de ce paramètre est comprise entre 4 et 24 et la valeur par défaut est 6. Si vous entrez 0, les utilisateurs ne sont pas obligés d'entrer un code confidentiel.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Nous vous déconseillons de définir ce paramètre sur 0. Si vous définissez ce paramètre sur zéro (0), vous diminuez considérablement le niveau de sécurité de votre réseau.</td>
</tr>
</tbody>
</table>


Si vous modifiez la longueur minimale du code confidentiel pour une valeur supérieure, pour pouvoir continuer, les utilisateurs actuels d'Outlook Voice Access sont invités à créer un code confidentiel respectant le nouveau nombre minimal de chiffres.

> [!NOTE]
> Une valeur plus élevée favorise la création d'un environnement de messagerie unifiée plus sécurisé. Toutefois, en définissant une valeur trop élevée, l'utilisateur risque plus facilement d'oublier son code confidentiel.


## Application de la durée de vie du code confidentiel

Le paramètre **Appliquer la durée de vie du code confidentiel** contrôle l'intervalle de temps, en jours, entre la date où les utilisateurs d'Outlook Voice Access ont modifié leur code confidentiel pour la dernière fois et la date où ils seront contraints de le modifier à nouveau. La valeur est comprise entre 0 et 999 et la valeur par défaut est 60 jours. Si la valeur 0 est entrée, le code confidentiel n'a pas de date d'expiration.

> [!NOTE]
> La messagerie unifiée n'informe pas les utilisateurs lorsque leur code confidentiel est sur le point d'expirer.


## Nombre d'échecs de connexion avant la réinitialisation du code confidentiel

Le paramètre **Nombre d'échecs de connexion avant réinitialisation du code confidentiel** spécifie le nombre de tentatives de connexion consécutives infructueuses qui précèdent la réinitialisation automatique du code confidentiel de la boîte aux lettres. Pour désactiver cette fonctionnalité, définissez ce paramètre sur illimité. Sinon, il doit être défini sur un nombre inférieur au paramètre **Nombre d'échecs de connexion avant verrouillage**. La valeur de ce paramètre est comprise entre 1 et 998 et la valeur par défaut est 5.

> [!NOTE]
> Pour augmenter la sécurité des utilisateurs à messagerie unifiée, entrez un nombre inférieur à 5.


## Nombre d'échecs de connexion avant verrouillage

Le paramètre **Nombre d'échecs de connexion avant verrouillage** spécifie le nombre d'erreurs d'entrée du code confidentiel dans des appels successifs que des utilisateurs d'Outlook Voice Access peuvent effectuer avant que leur boîte aux lettres ne soit verrouillée. Par défaut, après 5 tentatives effectuées, le code confidentiel est automatiquement réinitialisé. La valeur de ce paramètre est comprise entre 1 et 999 et la valeur par défaut est 15.

> [!NOTE]
> Pour accroître le niveau de sécurité, diminuez le nombre de tentatives infructueuses autorisées. Mais gardez à l'esprit que réduire ce nombre à un nombre inférieur à la valeur par défaut peut entraîner le verrouillage inutile de l'accès des utilisateurs à leur boîte aux lettres. La messagerie unifiée génère des événements d'avertissement que vous pouvez afficher à l'aide de l'observateur d'événements en cas d'échec d'authentification du code confidentiel pour un utilisateur à extension messagerie unifiée ou si l'utilisateur ne parvient pas à se connecter au système.


## Autoriser les modèles courants de codes confidentiels

Le paramètre **Autoriser les modèles courants de codes confidentiels** permet d'activer ou de désactiver l'utilisation de modèles numériques courants lors de la création d'un code confidentiel. Par défaut, ce paramètre est désactivé, ce qui interdit à des utilisateurs d'Outlook Voice Access d'entrer les modèles numériques suivants :

  - **Nombres séquentiels**   Valeurs de code confidentiel constituées entièrement de nombres consécutifs. 1234 et 65432 sont des exemples de nombres séquentiels de code confidentiel.

  - **Chiffres répétés**  Valeurs de code confidentiel constituées de chiffres répétés. Par exemple, 11111 et 22222 sont des nombres à chiffres répétés.

  - **Suffixe d'une extension de boîte aux lettres**   Valeurs de code confidentiel correspondant au suffixe d'une extension de boîte aux lettres d'utilisateur. Si l'extension de boîte aux lettres est 36697, le code confidentiel ne peut pas être 6697.

## Nombre de recyclages du code confidentiel

Le paramètre **Nombre de recyclages du code confidentiel** définit le nombre de codes confidentiels différents qu'un utilisateur doit utiliser avant de pouvoir réutiliser un code confidentiel qui a déjà été utilisé. La valeur de ce paramètre est comprise entre 1 et 20 et la valeur par défaut est 5.

## Gestion des codes confidentiels d'Outlook Voice Access

Quand vous effectuez la planification des codes confidentiels d'Outlook Voice Access, vous devez choisir les niveaux de sécurité appropriés pour votre organisation. Vous devez porter une attention particulière aux critères de code confidentiel d'Outlook Voice Access et à la conformité de vos paramètres de sécurité de code confidentiel par rapport à la stratégie de sécurité de votre organisation.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il s'agit d'une pratique recommandée en matière de sécurité pour l'implémentation de critères stricts de codes confidentiels destinés aux utilisateurs d'Outlook Voice Access. Cette pratique qui accroît le niveau de sécurité de votre réseau peut être appliquée via la création de stratégies de code confidentiel sur la stratégie de boîte aux lettres de messagerie unifiée qui exigent des codes confidentiels de 6 chiffres ou plus.</td>
</tr>
</tbody>
</table>


Après avoir défini les critères de codes confidentiels d'Outlook Voice Access, vous devez créer et configurer une stratégie de boîte aux lettres de messagerie unifiée pour appliquer vos critères de code confidentiel dans votre organisation. Pour plus d'informations sur la création d'une stratégie de boîte aux lettres de messagerie unifiée, consultez la rubrique [Créer une stratégie de boîte aux lettres de messagerie unifiée](create-a-um-mailbox-policy-exchange-2013-help.md). Pour plus d'informations sur la gestion des stratégies de boîte aux lettres de messagerie unifiée, consultez la rubrique [Gérer une stratégie de boîte aux lettres de messagerie unifiée](manage-a-um-mailbox-policy-exchange-2013-help.md).

> [!NOTE]
> Une fois la stratégie de boîte aux lettres de messagerie unifiée créée, vous devez lier les utilisateurs à extension messagerie unifiée à la stratégie de boîte aux lettres de messagerie unifiée appropriée. Pour ce faire, utilisez la cmdlet <strong>Enable-UMMailbox</strong> dans l'environnement de ligne de commande Exchange Management Shell ou le Centre d'administration Exchange (CAE). Pour plus d'informations sur la cmdlet de l'environnement de ligne de commande Exchange Management Shell, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/aa998033(v=exchg.150)">Enable-UMMailbox</a>.


Parfois, les utilisateurs d'Outlook Voice Access oublient leur code confidentiel ou l'accès à la messagerie vocale de leur boîte aux lettres leur est verrouillé. Dans ce cas, il se peut que vous deviez réinitialiser le code confidentiel de l'utilisateur de la messagerie unifiée. Pour plus d'informations, consultez la rubrique [Réinitialisation d'un code confidentiel de messagerie vocale](reset-a-voice-mail-pin-exchange-2013-help.md).

Vous pouvez récupérer des informations de code confidentiel d'un utilisateur à extension de messagerie unifiée. Les informations renvoyées sont calculées à l'aide des données chiffrées du code confidentiel stockées dans la boîte aux lettres de l'utilisateur. Cela vous permet d'afficher des informations sur le code confidentiel de l'utilisateur et de déterminer si ce dernier peut encore accéder ou non à sa boîte aux lettres. Pour plus d'informations, consultez la rubrique [Extraction des informations de code confidentiel de messagerie vocale](retrieve-voice-mail-pin-information-exchange-2013-help.md).

