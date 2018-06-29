---
title: 'Configurer un standard automatique de messagerie unifiée: Exchange 2013 Help'
TOCTitle: Configurer un standard automatique de messagerie unifiée
ms:assetid: 0a3492f8-8aba-4904-96fd-6e023175012a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ673508(v=EXCHG.150)
ms:contentKeyID: 50477523
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurer un standard automatique de messagerie unifiée

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Dernière rubrique modifiée :**2015-03-09_

La messagerie unifiée permet non seulement aux utilisateurs d’accéder à la messagerie vocale, mais également de créer un ou plusieurs standards automatiques de messagerie unifiée en fonction des besoins de l’organisation. Les standards automatiques de messagerie unifiée permettent de créer un système de menus vocal pour une organisation, qui laisse les appelants internes et externes localiser, passer ou transférer des appels à des utilisateurs ou des services d’une organisation.

Pour les autres tâches de gestion relatives aux standards automatiques de messagerie unifiée, consultez la rubrique [Procédures relatives au standard automatique de messagerie unifiée](um-auto-attendant-procedures-exchange-2013-help.md).

## Les standards automatiques

Dans des environnements de messagerie unifiée ou de téléphonie, un standard automatique ou un système de menus de standard automatique transfère les appelants vers le poste d’un utilisateur ou d’un département sans intervention d’un réceptionniste ou d’un opérateur. Dans de nombreux systèmes de standard automatique, vous pouvez joindre un réceptionniste ou un opérateur en appuyant sur la touche zéro ou en prononçant le mot zéro. Certains systèmes de standard automatique comportent des menus d’information uniquement pour les messages et des menus vocaux qui permettent à une organisation d’indiquer ses heures d’ouverture, l’itinéraire d’accès à ses locaux, les opportunités d’emploi et d’autres réponses à des questions fréquemment posées. Une fois le message lu, les appelants sont transférés vers le réceptionniste ou l’opérateur, ou peuvent revenir au menu principal.

Bien que les standards automatiques puissent être très utiles, ils peuvent être une source de confusion et de frustration pour l’appelant s’ils ne sont pas conçus et configurés correctement. Par exemple, dans des organisations de taille importante, si un standard automatique n’est pas conçu correctement, les appelants peuvent être confrontés à une série interminable de questions et d’invites de menu avant d’être mis en relation avec la personne qui doit répondre à leur question.

## Comment configurer un standard automatique ?

Dans le Centre d’administration Exchange, vous configurez et gérez des standards automatiques de messagerie unifiée pour répondre automatiquement aux appels adressés à votre organisation et permettre aux appelants de sélectionner eux-mêmes différentes options au moyen des touches de leur téléphone. Vous pouvez disposer d’un seul standard automatique de messagerie unifiée fournissant une navigation de menu de base pour les personnes qui appellent votre organisation, ou disposer de plusieurs standards automatiques imbriqués avec branchement qui offrent davantage de possibilités à vos appelants. Toutefois, dans les deux cas, vous devez planifier et configurer soigneusement vos standards automatiques.

Pour planifier et créer une structure de standard automatique de messagerie unifiée, procédez comme suit :

1.  Déterminez si les utilisateurs sont autorisés à se servir de la saisie vocale pour interagir avec le standard automatique.

2.  Déterminez quelle langue utiliser dans votre principal standard automatique et précisez si vous devez en créer d’autres pour prendre en charge des langues supplémentaires.

3.  Déterminez les heures d’ouverture et de fermeture du standard automatique et définissez les heures d’ouverture à l’aide de l’option **Heures d’ouverture**. Bien que cela ne soit pas obligatoire, vous pouvez également déterminer le calendrier des vacances pour ce standard automatique.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Vous devez également définir le fuseau horaire du standard.</td>
    </tr>
    </tbody>
    </table>


4.  Déterminez si le système doit générer des messages d’accueil standard pendant les heures d’ouverture et en dehors de ces heures ou si vous préférez créer des enregistrements personnalisés.
    
    Si vous voulez utiliser des messages d’accueil personnalisés, planifiez-les et enregistrez-les pour qu’ils soient lus pendant les heures d’ouverture et en dehors de ces heures. Le cas échéant, vous pouvez également créer un message d’information automatique personnalisé. Par exemple, vous pouvez utiliser ce message d’accueil pendant les heures d’ouverture : « Bienvenue chez Contoso. Pour choisir l’anglais, appuyez sur 1 ou dites 1, pour choisir l’espagnol, appuyez sur 2 ou dites 2. » Pour votre message d’accueil en dehors des heures d’ouverture, vous pouvez enregistrer le script suivant : « Bienvenue chez Contoso. Nos bureaux sont actuellement fermés. Ils seront ouverts lundi à 8h00. »

5.  Planifiez la structure de votre standard automatique en fonction des besoins de votre entreprise. Par exemple, une entreprise multinationale possédant des bureaux en Allemagne et au Royaume-Uni peut avoir besoin d’une structure de standard automatique en plusieurs langues. Le siège social d’une autre organisation peut être implanté sur un premier site, son service des ventes sur un deuxième site et son service clientèle sur un troisième site. Dans ce cas de figure, cette organisation aura besoin d’un standard automatique qui est directement lié à sa structure.

6.  Déterminez s’il faut utiliser des standards automatiques de secours DTMF ou d’autres standards automatiques lorsque les commandes vocales du standard automatique ne fonctionnent pas.

7.  Planifiez la navigation de menu pendant les heures d’ouverture et en dehors de ces heures. Pour chaque standard automatique, y compris les standards automatiques DTMF, vous devrez planifier et configurer les invites de menu et les entrées de navigation de menu. Vous devrez le faire pour les heures d’ouverture et de fermeture.

8.  Voici un exemple de feuille de calcul à utiliser pour planifier la navigation de menu pendant et en dehors des heures d’ouverture.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Touche</strong></th>
    <th><strong>Invite/Nom d’entrée du menu de navigation</strong></th>
    <th><strong>Réponse à enregistrer</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1</p></td>
    <td><p>Sélection de la langue anglaise.</p></td>
    <td><p>« Appuyez sur 1 ou dites 1 pour utiliser l’anglais. »</p></td>
    </tr>
    <tr class="even">
    <td><p>2</p></td>
    <td><p>Solde du compte</p></td>
    <td><p>« Appuyez sur 2 ou dites 2 pour obtenir le solde de votre compte. »</p></td>
    </tr>
    <tr class="odd">
    <td><p>3</p></td>
    <td><p>Transfert au service des ventes</p></td>
    <td><p>« Appuyez sur 3 ou dites 3 pour être transféré à notre service des ventes. »</p></td>
    </tr>
    <tr class="even">
    <td><p>4</p></td>
    <td><p>Transfert au service clientèle</p></td>
    <td><p>« Appuyez sur 4 ou dites 4 pour être transféré au prochain représentant du service clientèle. »</p></td>
    </tr>
    <tr class="odd">
    <td><p>5</p></td>
    <td><p>Heures d’ouverture</p></td>
    <td><p>Pas de réponse requise.</p></td>
    </tr>
    <tr class="even">
    <td><p>6</p></td>
    <td><p>Adresse de l’entreprise</p></td>
    <td><p>Pas de réponse requise.</p></td>
    </tr>
    </tbody>
    </table>


9.  À l’aide de votre plan de navigation de menu, enregistrez les invites indiquant aux appelants ce qu’ils peuvent faire. Par exemple, selon la structure de standard automatique choisie pour la navigation de menu en dehors des heures d’ouverture (voir tableau ci-dessus), vous pouvez enregistrer le script suivant : « Pour laisser un message au service des ventes, appuyez sur un. Pour connaître nos heures d’ouverture, appuyez sur deux. Pour notre adresse, appuyez sur trois.»

10. Déterminez comment les appelants accéderont à votre organisation. Demandez-vous comment ils rechercheront des utilisateurs dans votre organisation et comment ils les contacteront. Déterminez également comment transférer les appelants, notamment comment les transférer directement à une personne ou un représentant de l’organisation, et s’ils pourront parler à un opérateur pendant les heures d’ouverture et en dehors de ces heures.

11. Déterminez les appels que les appelants peuvent passer lorsqu’ils utilisent un standard automatique spécifique. Par exemple, précisez s’ils sont autorisés à appeler des utilisateurs dans un plan de numérotation, à appeler n’importe quel numéro de poste ou s’ils peuvent passer des appels à l’extérieur de votre organisation.

12. Lorsque vous aurez planifié les paramètres, les messages d’accueil et la navigation de menu de votre standard automatique, puis créé les fichiers audio qui contiennent vos messages d’accueil enregistrés, ainsi que les invites et réponses de navigation de menu, vous serez prêt à créer et à configurer votre standard automatique. Voici comment procéder :
    
      - [Créer un standard automatique de messagerie unifiée](create-a-um-auto-attendant-exchange-2013-help.md)
    
      - [Gérer un standard automatique de messagerie unifiée](manage-a-um-auto-attendant-exchange-2013-help.md)

13. Si vous avez créé la structure du standard automatique de messagerie unifiée et défini ses paramètres, activez-le pour qu’il puisse commencer à accepter les appels.

