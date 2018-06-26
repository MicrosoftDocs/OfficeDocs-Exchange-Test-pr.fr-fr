---
title: 'Conserver les destinataires Cci et les destinataires de groupe de distribution étendu pour la découverte électronique: Exchange 2013 Help'
TOCTitle: Conserver les destinataires Cci et les destinataires de groupe de distribution étendu pour la découverte électronique
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62516960
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conserver les destinataires Cci et les destinataires de groupe de distribution étendu pour la découverte électronique

 

_**Sapplique à :**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Dernière rubrique modifiée :**2017-06-19_

Place maintenez Litigation Hold et [les stratégies de rétention Office 365](http://go.microsoft.com/fwlink/?linkid=827811) (créé dans le Centre de conformité et sécurité dans Office 365 ) permettent de conserver le contenu des boîtes aux lettres afin de répondre aux exigences de l’e-Discovery et de conformité réglementaire. Informations sur les destinataires adressé directement dans les champs à et Cc les champs d’un message est inclus par défaut dans tous les messages, mais votre organisation peut demander la possibilité de rechercher et de reproduire des informations sur tous les destinataires d’un message. Cela inclut :

  - **Les destinataires spécifiés dans le champ Cci d’un message :** les destinataires en copie carbone invisible sont stockés dans le message qui se trouve dans la boîte aux lettres de l’expéditeur, mais ne figurent pas dans les en-têtes du message remis aux destinataires.

  - **Les destinataires de groupe de distribution étendu :** les destinataires qui reçoivent le message car ils sont membres d’un groupe de distribution auquel le message a été adressé, figurent dans le champ À, Cc ou Cci.

Exchange Online et Exchange Server 2013 (à jour Cumulative 7 et versions ultérieures) conservent des informations sur la Cci et destinataires de groupes de distribution de développé. Vous pouvez rechercher ces informations à l’aide d’une recherche d’e-Discovery en Place dans le Centre d’administration Exchange (FAC) ou une recherche de contenu dans le Centre de conformité et sécurité.

## Conservation des destinataires en copie carbone invisible et des destinataires de groupe de distribution étendu

Comme indiqué précédemment, les informations sur les destinataires en copie carbone cachée sont stockées avec le message dans la boîte aux lettres de l’expéditeur. Cette information est indexé et disponibles à la recherche d’e-Discovery et le maintient.

Informations sur les destinataires de groupe de distribution de développé sont stockées avec le message une fois que vous placez une boîte aux lettres sur Place ou en cas de litige. Dans Office 365, ces informations sont également stockées lorsqu’une stratégie de rétention Office 365 est appliquée à une boîte aux lettres. L’appartenance au groupe de distribution est déterminé au moment où que le message est envoyé. La liste des destinataires de développé stockée avec le message n’est pas concernée par les modifications apportées à l’appartenance au groupe après l’envoi du message.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Informations sur...</th>
<th>Stockage dans...</th>
<th>Stockage par défaut ?</th>
<th>Accessibles à...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinataires À et Cc</p></td>
<td><p>Propriétés de message dans les boîtes aux lettres de l’expéditeur et des destinataires</p></td>
<td><p>Oui</p></td>
<td><p>Expéditeur, destinataires et responsables de la mise en conformité</p></td>
</tr>
<tr class="even">
<td><p>Destinataires en copie carbone invisible</p></td>
<td><p>Propriété de message dans la boîte aux lettres de l’expéditeur</p></td>
<td><p>Oui</p></td>
<td><p>Expéditeurs et responsables de la mise en conformité</p></td>
</tr>
<tr class="odd">
<td><p>Destinataires de groupe de distribution étendu</p></td>
<td><p>Propriétés de message dans la boîte aux lettres de l’expéditeur</p></td>
<td><p>N° Informations de destinataire de groupe de distribution de développé sont stockées après qu’une boîte aux lettres est placée sur la Place ou en cas de litige ou affectées à une stratégie de rétention Office 365.</p></td>
<td><p>Responsables de la mise en conformité</p></td>
</tr>
</tbody>
</table>


## Recherche de messages envoyés aux destinataires en copie carbone invisible et aux destinataires de groupe de distribution étendu

Lors de la recherche de messages envoyés à un destinataire, les résultats de découverte électronique incluent désormais les messages envoyés à un groupe de distribution dont le destinataire est membre. Le tableau suivant présente les scénarios où les messages envoyés à des destinataires en copie carbone invisible et à des destinataires de groupe de distribution étendu sont renvoyés dans les recherches de découverte électronique.

Scénario 1 : John est membre du groupe de distribution Ventes aux États-Unis. Ce tableau présente les résultats de la recherche de découverte électronique lorsque Bob envoie un message à John directement ou indirectement via un groupe de distribution.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Lorsque vous recherchez les messages envoyés dans la boîte aux lettres de Bob...</th>
<th>Et le message est envoyé avec...</th>
<th>Les résultats incluent le message...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>À:John</p></td>
<td><p>John dans le champ À</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>À:John</p></td>
<td><p>Ventes aux États-Unis dans le champ À</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>À:Ventes aux États-Unis</p></td>
<td><p>Ventes aux États-Unis dans le champ À</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>John dans le champ Cc</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>Ventes aux États-Unis dans le champ Cc</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p>Cc:Ventes aux États-Unis</p></td>
<td><p>Ventes aux États-Unis dans le champ Cc</p></td>
<td><p>Oui</p></td>
</tr>
</tbody>
</table>


Scénario 2 : Bob envoie un courrier électronique à John (À/Cc) et Jack (Cci, directement ou indirectement via un groupe de distribution). Le tableau ci-dessous montre les résultats de la recherche de découverte électronique.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Lorsque vous recherchez...</th>
<th>Pour les messages envoyés...</th>
<th>Les résultats incluent le message...</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Boîte aux lettres de Bob</p></td>
<td><p>À/Cc:John</p></td>
<td><p>Oui</p></td>
<td><p>Indique que Jack était inclus dans le champ Cci</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de Bob</p></td>
<td><p>Cci:Jack</p></td>
<td><p>Oui</p></td>
<td><p>Indique que Jack était inclus dans le champ Cci</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres de Bob</p></td>
<td><p>Cci:Jack (via un groupe de distribution)</p></td>
<td><p>Oui</p></td>
<td><p>La liste des membres du groupe de distribution indiqué dans le champ Cci, étendu lors de l’envoi du message, est visible dans l’aperçu de la recherche de découverte électronique, l’exportation et les journaux.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de John</p></td>
<td><p>À/Cc:John</p></td>
<td><p>Oui</p></td>
<td><p>Aucune indication des destinataires en copie carbone invisible.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres de John</p></td>
<td><p>Cci:Jack (directement ou via un groupe de distribution)</p></td>
<td><p>Non</p></td>
<td><p>Les informations du champ Cci ne sont pas stockées dans le message remis aux destinataires. Vous devez les rechercher dans la boîte aux lettres de l’expéditeur.</p></td>
</tr>
<tr class="even">
<td><p>Boîte aux lettres de Jack</p></td>
<td><p>À/Cc:John (directement ou via un groupe de distribution)</p></td>
<td><p>Oui</p></td>
<td><p>Les informations des champs À/Cc sont incluses dans le message remis à tous les destinataires.</p></td>
</tr>
<tr class="odd">
<td><p>Boîte aux lettres de Jack</p></td>
<td><p>Cci:Jack (directement ou via un groupe de distribution)</p></td>
<td><p>Non</p></td>
<td><p>Les informations du champ Cci ne sont pas stockées dans le message remis aux destinataires. Vous devez les rechercher dans la boîte aux lettres de l’expéditeur.</p></td>
</tr>
</tbody>
</table>


## Questions fréquemment posées

**Q. quand et où sont stockées les informations de destinataire Cci ?**  
Informations relatives aux destinataires Cci d’a sont conservés par défaut dans le message d’origine dans la boîte aux lettres de l’expéditeur. Si le destinataire de Cci est un groupe de distribution, l’appartenance au groupe de distribution est uniquement développé si la boîte aux lettres de l’expéditeur est bloqué ou affectée à une stratégie de rétention Office 365.

**Q. quand et où la liste de distribution étendue groupe de destinataires est stockés ?**  
L’appartenance au groupe d’a. est développée au moment où le message est envoyé. La liste des membres du groupe de distribution étendues est stockée dans le message d’origine dans la boîte aux lettres de l’expéditeur. Boîte aux lettres de l’expéditeur doit être sur Place maintenez, Litigation Hold, ou affectées à une stratégie de rétention Office 365.

**Q. Les destinataires indiqués dans les champs À et Cc peuvent-ils voir les destinataires indiqués dans le champ Cci ?**  
R. Non. Ces informations ne sont pas incluses dans les en-têtes de message et ne sont pas visibles pour les destinataires indiqués dans les champs À et Cc. L’expéditeur peut voir le champ Cci stocké dans le message original de sa boîte aux lettres. Les responsables de la mise en conformité peuvent voir ces informations lors d’une recherche dans la boîte aux lettres de l’expéditeur.

**Q. Comment puis-je assurer de développé des destinataires de groupes sont toujours conservées ?**  
A. Pour garantir la distribution de développé les membres du groupe sont toujours conservées avec un message, [Placement de toutes les boîtes aux lettres en conservation](place-all-mailboxes-on-hold-exchange-2013-help.md) ou créer une stratégie de rétention de l’entreprise Office 365.

**Q. Quels types de groupe sont pris en charge ?**  
R. Les groupes de distribution, les groupes de sécurité à extension messagerie et les groupes de distribution dynamique sont pris en charge.

**Q. Y a-t-il une limite en ce qui concerne le nombre de destinataires de groupes de distribution étendus et stockés dans le message ?**  
R. Jusqu’à 10 000 membres d’un groupe de distribution sont conservés.

**Q. Les groupes de distribution imbriqués sont-ils pris en charge ?**  
R. Oui, 25 niveaux de groupes de distribution imbriqués sont étendus.

**Q. Où les informations du champ Cci et les informations relatives aux destinataires de groupe de distribution étendu sont-elles visibles ?**  
R. Ces informations sont visibles pour les responsables de la mise en conformité lors d’une recherche de découverte électronique. Les destinataires en Cci et les destinataires de groupe de distribution étendu sont inclus dans les résultats de recherche copiés vers une boîte aux lettres de découverte ou exportés vers un fichier PST et dans le journal de découverte électronique inclus dans les résultats de la recherche. Les informations relatives aux destinataires en copie carbone invisible sont également disponibles dans l’aperçu de la recherche.

**Q. Que se passe-t-il si un membre d’un groupe de distribution est masqué dans la liste d’adresses globale (LAG) de l’organisation ?**  
R. Il n’y a aucune conséquence. Même si des destinataires sont masqués dans la LAG, ils restent inclus dans la liste des destinataires pour le groupe de distribution étendu.

