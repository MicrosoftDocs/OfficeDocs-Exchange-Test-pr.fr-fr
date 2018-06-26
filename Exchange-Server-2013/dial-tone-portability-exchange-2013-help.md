---
title: 'Portabilité de tonalité: Exchange 2013 Help'
TOCTitle: Portabilité de tonalité
ms:assetid: ea62fae0-5e0a-460c-beb6-52532c8c8dbc
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd876950(v=EXCHG.150)
ms:contentKeyID: 51407244
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Portabilité de tonalité

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2013-01-28_

La portabilité de tonalité est une fonctionnalité de Microsoft Exchange Server 2013 qui offre une solution de continuité de l'activité limitée en cas de pannes nuisant au fonctionnement d'une base de données de boîtes aux lettres, d'un serveur ou d'un site entier. La portabilité de tonalité permet aux utilisateurs de disposer d'une boîte aux lettres temporaire pour envoyer et recevoir des messages électroniques pendant que leur boîte aux lettres est restaurée ou réparée. La boîte aux lettres temporaire peut être située sur le même serveur de boîtes aux lettres Exchange 2013 ou sur un autre serveur de boîtes aux lettres Exchange 2013 dans votre organisation qui contient des bases de données possédant la même version de schéma de base de données. Cela permet à un autre serveur d'héberger les boîtes aux lettres d'utilisateurs qui étaient auparavant sur un serveur qui n'est plus disponible. Les clients qui prennent en charge le service de découverte automatique sont automatiquement redirigés vers le nouveau serveur sans qu'il soit nécessaire de mettre à jour manuellement le profil de Bureau des utilisateurs. Une fois que les données de la boîte aux lettres d'origine d'un utilisateur sont restaurées, un administrateur peut fusionner la boîte aux lettres restaurée et la boîte aux lettres de tonalité dans une boîte aux lettres mise à jour.

Le processus d'utilisation de la portabilité de tonalité est appelé *récupération de tonalité*. Une récupération de tonalité implique la création d'une base de données vide sur un serveur de boîtes aux lettres pour remplacer la base de données endommagée. Cette base de données vide, appelée *base de données de tonalité*, permet aux utilisateurs d'envoyer et de recevoir des messages électroniques pendant la récupération de la base de données endommagée.

Il existe trois options pour la récupération de tonalité :

  - **Récupération de tonalité sur le serveur hébergeant la base de données endommagée**   Si le serveur hébergeant la base de données endommagée est toujours opérationnel, nous vous conseillons d'effectuer une récupération de tonalité sur ce serveur. Le temps mort est ainsi réduit, car vous n'avez pas besoin de transférer des fichiers de base de données d'un serveur à un autre. De plus, vous n'avez pas besoin de reconfigurer les profils de messagerie des clients qui ne prennent pas en charge le service de découverte automatique.

  - **Récupération de tonalité à l'aide d'un serveur secondaire pour la base de données de tonalité**   Si un serveur tombe en panne et doit être reconstruit, le moyen le plus efficace pour fournir aux utilisateurs des fonctionnalités de messagerie de base est de créer une base de données de tonalité sur un autre serveur et d'utiliser la portabilité de base de données pour déplacer la configuration des boîtes aux lettres des utilisateurs vers ce nouveau serveur. Étant donné que ce processus implique de replacer la base de données de tonalité sur le serveur (récupéré) d'origine, cette option rend plus long le processus de récupération globale. En outre, ce processus est plus complexe que l'exécution d'une récupération de tonalité sur le serveur d'origine. Lorsque vous effectuez ce processus, le serveur qui héberge la base de données de tonalité doit disposer des ressources suffisantes pour prendre en charge la charge ajoutée des utilisateurs supplémentaires. De plus, si le client de l'utilisateur ne prend pas en charge la découverte automatique, son profil de messagerie doit être reconfiguré pour pointer vers le serveur de tonalité.

  - **Récupération de tonalité sur et à l'aide d'un serveur secondaire pour la base de données de tonalité**   Cette option est similaire à la précédente, sauf que le serveur d'origine n'est pas récupéré. Nous vous recommandons l'utilisation de cette option lorsqu'il est impossible ou inconcevable de récupérer le serveur endommagé. Dans ce scénario, les utilisateurs continuent à utiliser le serveur secondaire une fois l'opération de récupération terminée. Lorsque vous effectuez ce processus, le serveur qui héberge la base de données de tonalité doit disposer des ressources suffisantes pour prendre en charge la charge ajoutée des utilisateurs supplémentaires. De plus, si le client de l'utilisateur ne prend pas en charge la découverte automatique, son profil de messagerie doit être reconfiguré pour pointer vers le serveur de tonalité.

Les trois options suivent la même procédure de base :

1.  **Création d'une base de données de tonalité vide pour remplacer la base de données endommagée.**
    
    Cette nouvelle base de données permet aux utilisateurs qui disposaient d'une boîte aux lettres dans la base de données endommagée d'envoyer et de recevoir des messages. La portabilité de tonalité vous permet de diriger un utilisateur vers une autre base de données sans qu'il soit nécessaire de déplacer la boîte aux lettres de cet utilisateur. En revanche, si vous avez créé la base de données de tonalité sur un serveur différent du serveur hébergeant la base de données endommagée, vous devez déplacer la configuration de la boîte aux lettres vers ce nouveau serveur.

2.  **Restauration de l'ancienne base de données.**
    
    Utilisez le logiciel de sauvegarde et de récupération que vous utilisez habituellement pour restaurer la base de données endommagée. S'il n'existe aucune sauvegarde de la base de données endommagée, essayez de récupérer la base de données endommagée par d'autres moyens. Si vous utilisez le même serveur pour la récupération de tonalité, vous devez restaurer la base de données dans une base de données de récupération (RDB).

3.  **Remplacement de la base de données de tonalité par la base de données restaurée.**
    
    Une fois la base de données endommagée restaurée, remplacez-la par la base de données de tonalité. Ainsi, les utilisateurs pourront envoyer et recevoir des messages électroniques et accéder aux données dans la base de données restaurée. Si les utilisateurs ont été transférés vers une base de données de tonalité sur un autre serveur, vous devez replacer la configuration des boîtes aux lettres des utilisateurs sur le serveur d'origine.

4.  **Fusion des bases de données.**
    
    Pour transférer les données de la base de données de tonalité dans la base de données restaurée, vous devez fusionner les données à l'aide de la cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/fr-fr/library/ff829875\(v=exchg.150\)).

Pour obtenir la procédure détaillée d'exécution d'une récupération de tonalité, consultez la rubrique [Réalisation d’une récupération de tonalité](perform-a-dial-tone-recovery-exchange-2013-help.md).

