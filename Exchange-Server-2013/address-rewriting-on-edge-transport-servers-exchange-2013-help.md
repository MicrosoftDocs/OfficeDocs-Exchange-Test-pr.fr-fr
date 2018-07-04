---
title: 'Réécriture d’adresses sur des serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Réécriture d’adresses sur des serveurs de transport Edge
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060519
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Réécriture d’adresses sur des serveurs de transport Edge

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

La réécriture d’adresses modifie les adresses de messagerie des expéditeurs et des destinataires dans les messages entrant dans votre organisation ou en sortant par le biais d’un serveur de transport Edge. Deux agents de transport sur le serveur de transport Edge fournissent la fonctionnalité de réécriture : l’agent de réécriture d’adresses pour les messages entrants et l’agent de réécriture d’adresses pour les messages sortants. La principale raison de la réécriture d’adresses sur les messages sortants est de présenter un seul domaine de messagerie cohérent aux destinataires externes. La principale raison de la réécriture d’adresses sur les messages entrants est de délivrer les messages au bon destinataire.

L’*entrée de réécriture d’adresses*, que vous créez, indique les adresses internes (les adresses de messagerie à modifier)​et les adresses externes (les adresses de messagerie finales que vous voulez). Vous pouvez indiquer si les adresses de messagerie doivent être réécrites dans les messages entrants et sortants ou dans les messages sortants uniquement. Vous pouvez créer des entrées d’écriture d’adresses pour un seul utilisateur (remplacer chris@contoso.com par support@contoso.com), pour tous les utilisateurs dans un seul domaine (remplacer contoso.com par fabrikam.com) ou pour les utilisateurs dans plusieurs sous-domaines avec des exceptions (remplacer \*.fabrikam.com par contoso.com, sauf pour legal.fabrikam.com).

> [!NOTE]
> Indépendamment de la façon dont vous prévoyez d’utiliser la réécriture d’adresses, vous devez vérifier que les adresses de messagerie obtenues sont uniques dans votre organisation afin de ne pas vous retrouver avec des doublons. En effet, la réécriture d’adresses ne vérifie pas le caractère unique d’une adresse de messagerie réécrite.


**Contenu de cette rubrique**

Scénarios de réécriture d’adresses

Modification des propriétés de message par la réécriture d’adresses

Éléments non modifiés par la réécriture d’adresses

Considérations pour la réécriture d’adresses sortantes uniquement

Considérations pour la réécriture d’adresses pour les messages entrants et sortants

Considérations pour la réécriture d’adresses de messagerie dans plusieurs domaines

Priorité des entrées de réécriture d’adresses

Messages protégés par des droits, signés et chiffrés numériquement

## Scénarios de réécriture d’adresses

Les scénarios suivants sont des exemples de l’utilisation de la réécriture d’adresses :

  - **Consolidation de groupe**   Certaines organisations segmentent leurs activités internes en domaines distincts en fonction d’exigences commerciales ou techniques. Cette configuration peut avoir pour effet que les messages électroniques semblent provenir de groupes distincts, voire d’organisations différentes.
    
    L’exemple suivant montre comment une organisation, Contoso, Ltd., peut masquer ses sous-domaines internes pour les destinataires externes :
    
      - Les domaines northamerica.contoso.com, europe.contoso.com et asia.contoso.com des adresses de messagerie des messages sortants sont réécrits pour que tous les messages semblent provenir d’un seul et même domaine contoso.com. Tous les messages sont réécrits au fur et à mesure qu’ils transitent par les serveurs de transport Edge qui assurent la connectivité SMTP entre l’organisation et Internet.
    
      - Les messages entrants vers des destinataires contoso.com sont relayés par le serveur de transport Edge vers un serveur de boîtes aux lettres. Le message est remis au bon destinataire en fonction de l’adresse de proxy configurée sur la boîte aux lettres du destinataire.

  - **Fusions et acquisitions**   Une société acquise peut continuer à fonctionner comme une entreprise distincte, mais vous pouvez utiliser la réécriture d’adresses pour faire en sorte que les deux organisations paraissent être une seule et même organisation.
    
    L’exemple suivant montre comment Contoso, Ltd. peut masquer le domaine de messagerie d’une société acquise qui s’appellerait Fourth Coffee :
    
      - Contoso, Ltd. souhaite que tous les messages sortant de l’organisation Exchange Fourth Coffee semblent provenir de contoso.com. Tous les messages des deux organisations sont envoyés via les serveurs de transport Edge de Contoso, Ltd., où les adresses électroniques des messages sont réécrites de façon à ce qu’une adresse *user*@fourthcoffee.com devienne *user*@contoso.com.
    
      - Les adresses de messagerie des messages entrants envoyés à *user*@contoso.com sont réécrites et acheminées vers les boîtes aux lettres *user*@fourthcoffee.com. Les messages entrants qui sont envoyés à *user*@fourthcoffee.com sont acheminés directement vers les serveurs de messagerie de Fourth Coffee.

  - **Partenaires**   De nombreuses organisations utilisent des partenaires externes pour fournir des services à leurs clients, d’autres organisations ou leur propre organisation. Afin d’éviter toute confusion, l’organisation peut remplacer le domaine de messagerie de l’organisation partenaire par son propre domaine de messagerie.
    
    L’exemple suivant montre comment Contoso, Ltd. peut masquer le domaine de messagerie d’un partenaire :
    
      - Contoso, Ltd. apporte son soutien à une organisation de plus grande taille, Wingtip Toys. Wingtip Toys souhaite une expérience unifiée pour ses clients et exige que tous les messages du service de support technique de Contoso, Ltd. apparaissent comme s’ils étaient expédiés par Wingtip Toys. Tous les messages sortants concernant Wingtip Toys sont expédiés via leurs serveurs de transport Edge et toutes les adresses de messagerie contoso.com sont réécrites en tant qu’adresses wingtiptoys.com.
    
      - Les messages entrants à destination de support@wingtiptoys.com sont acceptés par les serveurs de transport Edge de Wingtip Toys, leurs adresses sont réécrites, puis ils sont routés vers l’adresse de messagerie support@contoso.com.

Retour au début

## Modification des propriétés de message par la réécriture d’adresses

Un message électronique SMTP standard est constitué d’une *enveloppe de message* et d’un contenu de message. L’enveloppe de message contient les informations requises pour la transmission et la remise du message entre serveurs de messagerie SMTP. Le contenu du message comporte les champs d’en-tête de message (collectivement appelés l’*en-tête de message*) et le corps du message. L’enveloppe de message est décrite dans la spécification RFC 2821 et l’en-tête de message est décrit dans la spécification RFC 2822.

Lorsqu’un expéditeur rédige un message électronique et le soumet en vue de sa remise, le message contient les informations de base requises pour la conformité aux normes SMTP, telles que l’expéditeur, un destinataire, la date et l’heure de rédaction du message, une ligne d’objet facultative et un corps de message facultatif. Ces informations sont contenues dans le message proprement dit et, par définition, dans l’en-tête du message.

Le serveur de messagerie de l’expéditeur génère une enveloppe de message pour le message en utilisant les informations concernant l’expéditeur et le destinataire trouvées dans l’en-tête du message. Il transmet ensuite le message sur Internet afin qu’il soit remis au serveur de messagerie du destinataire. Les destinataires ne voient jamais l’enveloppe du message, car elle est générée par le processus de transmission du message et ne fait, en réalité, pas partie du message.

La réécriture d’adresses modifie une adresse de messagerie en réécrivant des champs spécifiques dans l’en-tête du message ou l’enveloppe du message. La réécriture d’adresses modifie plusieurs champs dans les messages sortants, mais un seul champ dans les messages électroniques entrants. Le tableau suivant indique les champs d’en-tête SMTP réécrits dans les messages sortants et entrants.

### Champs de message SMTP réécrits sur les messages sortants et entrants

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom du champ</th>
<th>Emplacement</th>
<th>Messages sortants</th>
<th>Messages entrants</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>Enveloppe de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>Enveloppe de message</p></td>
<td><p>Non réécrit</p></td>
<td><p>Réécrit</p></td>
</tr>
<tr class="odd">
<td><p><strong>To</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="odd">
<td><p><strong>From</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="even">
<td><p><strong>Sender</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>En-tête de message</p></td>
<td><p>Réécrit</p></td>
<td><p>Non réécrit</p></td>
</tr>
</tbody>
</table>


Retour au début

## Éléments non modifiés par la réécriture d’adresses

La réécriture d’adresses ne modifie aucun champ d’en-tête de message qui empêcherait le système SMTP de fonctionner correctement. Par exemple, la modification de certains champs d’en-tête pourrait affecter la détection de boucle de routage, invalider la signature ou rendre illisible un message protégé par des droits. Par conséquent, les champs d’en-tête suivants ne sont pas modifiés par la réécriture d’adresses.

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - Les champs d’en-tête situés dans des parties MIME

La réécriture d’adresses ne tient pas compte des domaines qui ne sont pas contrôlés par l’organisation Exchange. En d’autres termes, la réécriture d’adresses ne réécrit pas les champs d’en-tête qui contiennent des domaines pour lesquels l’organisation Exchange ne fait pas autorité. La réécriture de ces domaines entraînerait une forme incontrôlable de retard de message.

La réécriture d’adresses ne modifie pas non plus les champs d’en-tête de messages imbriqués dans un autre message. Les expéditeurs et les destinataires s’attendent à ce que les messages imbriqués restent intacts et soient remis sans modification, pour autant qu’ils ne déclenchent pas de règles de transport implémentées entre l’expéditeur et le destinataire.

Retour au début

## Considérations pour la réécriture d’adresses sortantes uniquement

La réécriture d’adresses pour les messages sortants uniquement sur un serveur de transport Edge modifie l’adresse de messagerie de l’expéditeur quand le message quitte l’organisation Exchange. Vous pouvez configurer la réécriture d’adresses pour les messages sortants uniquement pour un seul utilisateur (remplacement de chris@contoso.com par support@contoso.com) ou pour tous les utilisateurs dans un seul domaine (remplacement de contoso.com par fabrikam.com). Vous devez configurer la réécriture d’adresses pour les messages sortants uniquement pour les utilisateurs dans plusieurs sous-domaines (remplacement de \*.fabrikam.com par contoso.com).

L’adresse de messagerie réécrite doit être configurée en tant qu’adresse proxy sur les destinataires concernés. Par exemple, si l’adresse laura@sales.contoso.com est réécrite et remplacée par laura@contoso.com, l’adresse proxy laura@contoso.com doit être configurée sur la boîte aux lettres de Laura. Cette opération est nécessaire pour que les réponses et les messages entrants soient remis correctement.

Retour au début

## Considérations pour la réécriture d’adresses pour les messages entrants et sortants

La réécriture d’adresses pour les messages entrants et sortants ou la réécriture d’adresses *bidirectionnelle* sur un serveur de transport Edge modifie l’adresse de messagerie de l’expéditeur dans les messages quittant l’organisation Exchange et modifie l’adresse de messagerie du destinataire dans les messages entrant dans l’organisation Exchange.

Vous pouvez configurer la réécriture d’adresses pour les messages sortants uniquement pour un seul utilisateur (remplacer chris@contoso.com par support@contoso.com) et tous les utilisateurs dans un seul domaine (remplacer contoso.com par fabrikam.com). Vous ne pouvez pas configurer la réécriture d’adresses bidirectionnelle pour des utilisateurs dans plusieurs sous-domaines (remplacer \*.fabrikam.com par contoso.com).

Retour au début

## Considérations pour la réécriture d’adresses de messagerie dans plusieurs domaines

Lorsque vous regroupez plusieurs domaines ou sous-domaines internes en un seul domaine externe, vous devez prendre en compte les facteurs suivants :

  - **Vérifier les alias uniques**   Tous les alias de messagerie (la partie à gauche du signe @) doivent être uniques, quel que soit le sous-domaine. Par exemple, si l’adresse joe@sales.contoso.com existe, l’adresse joe@marketing.contoso.com ne peut pas exister également car l’adresse de messagerie réécrite pour les deux utilisateurs serait joe@contoso.com.

  - **Ajouter des adresses proxy**   L’adresse de messagerie réécrite doit être configurée en tant qu’adresse proxy pour tous les expéditeurs concernés dans les domaines concernés. Par exemple, si l’adresse joe@sales.contoso.com est réécrite et remplacée par joe@contoso.com, vous devez ajouter l’adresse proxy joe@contoso.com à la boîte aux lettres de Joe. Cette opération est nécessaire pour que les réponses et les messages entrants soient remis correctement.

  - **Contacts de messagerie pour les organisations autres qu’Exchange**   Si vous réécrivez des adresses de messagerie à partir d’un système de messagerie autre qu’Exchange, vous devez créer des contacts de messagerie pour représenter les utilisateurs dans le système de messagerie autre qu’Exchange. Ces contacts de messagerie doivent contenir les adresses de messagerie d’origine et les adresses de messagerie réécrites. Par exemple, si l’adresse joe@unix.contoso.com est réécrite et remplacée par joe@contoso.com, vous devez créer un contact de messagerie avec joe@unix.contoso.com en tant qu’adresse de messagerie externe et joe@contoso.com en tant qu’adresse proxy.

## Vérification des alias uniques

Lorsque vous réécrivez des adresses de messagerie dans plusieurs sous-domaines, vous devez vous assurer que tous les alias de messagerie sont uniques, quel que soit le sous-domaine. Imaginons, par exemple, la configuration suivante :

Les utilisateurs suivants appartiennent aux sous-domaines sales.contoso.com, marketing.contoso.com et research.contoso.com :

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

Supposons que vous vouliez réécrire les sous-domaines sales.contoso.com, marketing.contoso.com et research.contoso.com afin de les remplacer par le domaine unique contoso.com.

Lorsque les adresses de messagerie de chaque sous-domaine sont réécrites, un conflit se produit entre chris@sales.contoso.com et chris@research.contoso.com car, lors de leur réécriture, les deux adresses de messagerie sont remplacées par chris@contoso.com. Pour résoudre ce problème, vous devez modifier l’adresse de messagerie de l’un des destinataires concernés. Par exemple, vous pouvez remplacer l’adresse chris@research.contoso.com par christopher@research.contoso.com. Ainsi, lors de la réécriture, cette adresse de messagerie sera remplacée par christopher@contoso.com.

Retour au début

## Priorité des entrées de réécriture d’adresses

Si l’adresse de messagerie d’un utilisateur correspond à plusieurs entrées de réécriture d’adresses, l’adresse de messagerie n’est réécrite qu’une seule fois, en fonction de la correspondance la plus proche. La liste suivante indique l’ordre de priorité décroissante des entrées de réécriture d’adresses :

1.  **Adresses de messagerie individuelles**   Une entrée de réécriture d’adresse est configurée pour réécrire l’adresse de messagerie john@contoso.com en la remplaçant par support@contoso.com.

2.  **Mappage de domaine ou de sous-domaine**   Une entrée de réécriture d’adresse est configurée pour réécrire toutes les adresses de messagerie contoso.com en les remplaçant par northwindtraders.com ou toutes les adresses de messagerie sales.contoso.com par contoso.com.

3.  **Regroupement de domaine**   Une entrée de réécriture d’adresse est configurée pour réécrire les domaines d’adresses de messagerie \*.contoso.com et les remplacer par contoso.com.

Par exemple, imaginez un serveur de transport Edge sur lequel les entrées suivantes de réécriture d’adresses pour les messages sortants sont configurées :

  - le domaine d’adresses de messagerie \*.contoso.com est réécrit et remplacé par contoso.com

  - le sous-domaine d’adresses de messagerie japan.sales.contoso.com est réécrit et remplacé par contoso.jp

Si masato@japan.sales.contoso.com envoie un message électronique, l’adresse est réécrite et remplacée par masato@contoso.jp car cette entrée est celle qui correspond le plus à l’adresse de messagerie de l’expéditeur.

Retour au début

## Messages protégés par des droits, signés et chiffrés numériquement

La réécriture d’adresses ne devrait pas affecter la plupart des messages signés, chiffrés et protégés par des droits. Si la réécriture d’adresses risque de modifier ou de rendre incorrect l’état de la sécurité de ces types de messages de quelque façon que ce soit, la réécriture d’adresses n’est pas appliquée.

Les valeurs suivantes peuvent être réécrites car les informations ne font pas partie de la signature, du chiffrement ou de la protection par des droits du message :

  - Champs dans l’enveloppe de message

  - En-têtes de corps de message de niveau supérieur

Les valeurs suivantes peuvent être réécrites car les informations font partie de la signature, du chiffrement ou de la protection par des droits du message :

  - Champs d’en-tête situés à l’intérieur de parties MIME pouvant être signés

  - Paramètre de chaîne de limite du type de contenu MIME

Retour au début

