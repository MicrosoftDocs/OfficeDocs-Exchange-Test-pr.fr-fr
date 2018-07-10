---
title: "Stratégies d'adresse de messagerie: Exchange 2013 Help"
TOCTitle: Stratégies d'adresse de messagerie
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50478911
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Stratégies d'adresse de messagerie

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-07-21_

Les destinataires (utilisateurs, ressources, contacts et groupes) sont tout objet à extension messagerie dans Active Directory auquel Microsoft Exchange peut remettre ou router des messages. Pour qu'un destinataire puisse recevoir ou envoyer des messages électroniques, il doit avoir une adresse de messagerie. Les stratégies d’adresse de messagerie génèrent les adresses de messagerie principales et secondaires pour vos destinataires, de façon à ce qu’ils puissent recevoir et envoyer des messages.

Par défaut, Exchange contient une stratégie d’adresse de messagerie pour chaque utilisateur à extension messagerie. Cette stratégie par défaut spécifie l’alias du destinataire comme partie locale de l’adresse de messagerie et utilise le domaine accepté par défaut. La partie locale d’une adresse de messagerie correspond au nom qui apparaît devant le signe @. Toutefois, vous pouvez modifier la manière dont les adresses de messagerie de vos destinataires s’affichent. Par exemple, vous pouvez spécifier que les adresses s’affichent sous la forme *prénom*.*nom*@contoso.com.

En outre, si vous voulez indiquer des adresses de messagerie supplémentaires pour tous les destinataires ou uniquement un sous-ensemble de ces derniers, vous pouvez modifier la stratégie par défaut ou créer des stratégies supplémentaires. Par exemple, la boîte aux lettres de l’utilisateur David Hamilton peut recevoir des messages électroniques adressés à hdavid@mail.contoso.com et à hamilton.david@mail.contoso.com.

Vous recherchez les tâches de gestion relatives aux stratégies d’adresse de messagerie ? Voir [Procédures des stratégies d'adresse de messagerie](email-address-policy-procedures-exchange-2013-help.md).

## Comportements des stratégies de destinataire

Exchange applique une stratégie à tous les destinataires qui correspondent aux critères de filtrage des destinataires :

  - Les stratégies de destinataire sont appliquées dans l’ordre, de la priorité la plus élevée à la plus faible. En cas de conflit entre plusieurs stratégies, la stratégie avec la priorité la plus élevée est appliquée. La stratégie de destinataire par défaut a toujours la priorité la plus basse et est appliquée si aucune des autres stratégies ne correspond.
    
    Lorsque vous créez une stratégie de destinataire, mais que vous n’indiquez aucune priorité spécifique, la stratégie est ajoutée avec la priorité la plus élevée. Si vous indiquez une priorité déjà associée à une stratégie existante, la stratégie existante et toutes les stratégies dotées d’une priorité plus basse sont déplacées d’un cran vers le bas. La nouvelle stratégie est insérée au niveau de priorité indiqué.
    
    La fonctionnalité de stratégie de destinataire comporte deux fonctionnalités : les domaines acceptés et les stratégies d’adresse de messagerie. Pour plus d’informations sur les domaines acceptés, consultez la rubrique [Domaines acceptés](accepted-domains-exchange-2013-help.md).

  - Lorsque vous exécutez la cmdlet **Update-EmailAddressPolicy** dans l’environnement de ligne de commande Exchange Management Shell, l’objet destinataire est mis à jour avec la stratégie d’adresse de messagerie.

  - Chaque fois qu’un objet destinataire est modifié et enregistré, Exchange applique les critères et paramètres d’adresse de messagerie corrects. Lors de la modification et de l'enregistrement d'une adresse de messagerie, tous les destinataires associés sont mis à jour avec la modification. En outre, en cas de modification d’un objet destinataire, l’appartenance à une stratégie d’adresse de messagerie de ce destinataire est réévaluée et appliquée.

## Création de stratégies d’adresse de messagerie

Lors de la création d’une stratégie d’adresse de messagerie, les types d’adresse de messagerie suivants peuvent être utilisés :

  - **Adresse de messagerie SMTP prédéfinie**. Les adresses de messagerie SMTP *prédéfinies* sont des types d’adresse de messagerie fréquemment utilisés qui vous sont fournis.

  - **Adresse de messagerie SMTP personnalisée**. Si vous ne voulez pas utiliser l’une des adresses de messagerie SMTP prédéfinies, vous pouvez spécifier une adresse de messagerie SMTP personnalisée.
    
    Lors de la création d’une adresse de messagerie SMTP personnalisée, vous pouvez utiliser les variables indiquées dans le tableau suivant pour spécifier d’autres valeurs pour la partie locale de l’adresse de messagerie.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variable</th>
    <th>Valeur</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Prénom</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Initiale intermédiaire</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Nom</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nom d’affichage</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Utilise les <em>x</em> premières lettres du nom. Par exemple, si <em>x</em> = 2, les deux premières lettres du nom sont utilisées.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Utilise les <em>x</em> premières lettres du prénom. Par exemple, si <em>x</em> = 2, les deux premières lettres du prénom sont utilisées.</p></td>
    </tr>
    </tbody>
    </table>


  - **Adresse de messagerie non SMTP**. Les types d’adresses de messagerie non SMTP suivants sont pris en charge :
    
      - EX (nom complet du préfixe d’adresse proxy DN héritée)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Adresse proxy de messagerie unifiée Exchange (adresse proxy EUM)
    
    > [!NOTE]
    > Dans Exchange, toutes les adresses de messagerie non SMTP sont considérées comme des adresses personnalisées. Exchange ne fournit aucune boîte de dialogue ou page de propriétés unique pour les types d’adresses de messagerie X.400, GroupWise ou Lotus Notes. Si vous ajoutez une adresse de messagerie personnalisée non SMTP, vous devez disposer des fichiers bibliothèque de liens dynamiques correspondants. Si vous ne fournissez pas les fichiers DLL appropriés, vous ne pourrez pas créer de stratégie d’adresse de messagerie personnalisée. L’erreur suivante sera enregistrée dans l’Observateur d’événements : « L’objet de description de l’adresse de messagerie dans l’annuaire Microsoft Exchange pour le type d’adresse &quot; SADF &quot; sur les ordinateurs &quot; i386 &quot; est manquant. »


Pour des instructions détaillées sur la création d’une stratégie d’adresse de messagerie, voir les rubriques suivantes :

[Création d'une stratégie d'adresse de messagerie](create-an-email-address-policy-exchange-2013-help.md)

[Créer une stratégie d'adresses de messagerie en utilisant des filtres de destinataires](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

