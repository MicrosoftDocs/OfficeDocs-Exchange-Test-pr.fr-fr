---
title: 'Gestion des enregistrements de messagerie: Exchange 2013 Help'
TOCTitle: Gestion des enregistrements de messagerie
ms:assetid: 0dd92e9c-881e-43c0-9bbf-f41fdc9dfd87
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335093(v=EXCHG.150)
ms:contentKeyID: 50477552
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestion des enregistrements de messagerie

 

_**Sapplique à :**Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :**2016-02-01_

Les utilisateurs envoient et reçoivent du courrier électronique tous les jours. S’ils ne sont pas gérés, les messages électroniques générés et reçus chaque jour risquent d’inonder les utilisateurs, de réduire leur productivité et d’exposer votre entreprise à de nombreux risques. La gestion du cycle de vie de la messagerie est une composante essentielle pour la plupart des organisations.

La gestion des enregistrements de messagerie (MRM) est la technologie de gestion des enregistrements dans Exchange Server 2013 et Exchange Online qui permet aux organisations de gérer le cycle de vie de la messagerie et de réduire les risques juridiques associés au courrier électronique. Le déploiement de la gestion des enregistrements de messagerie peut aider votre organisation de plusieurs façons :

  - **Répondre aux besoins de l’entreprise**   Selon les stratégies de messagerie de votre organisation, vous devrez éventuellement conserver des messages électroniques importants pendant un certain temps. Par exemple, la boîte aux lettres d’un utilisateur peut contenir des messages importants relatifs à la stratégie commerciale, aux transactions, au développement de produits ou aux communications avec le client.

  - **Répondre aux exigences juridiques et réglementaires**   De nombreuses organisations sont obligées par la loi et les réglementations de conserver les messages pendant une durée déterminée et de les supprimer par la suite. En conservant les messages plus longtemps que nécessaire, vous risquez d’augmenter les risques juridiques ou financiers auxquels votre organisation est exposée.

  - **Améliorer la productivité de l’utilisateur**   S’il n’est pas géré, le volume sans cesse croissant de messages électroniques stockés dans les boîtes aux lettres des utilisateurs risque également d’affecter leur productivité. Par exemple, même si les abonnements à des bulletins d’informations et des notifications automatisées comportent une certaine valeur informationnelle lorsqu’ils sont reçus, les utilisateurs ne peuvent pas les supprimer pas après les avoir lu (souvent, ils ne sont jamais lus). Bon nombre de ces types de messages n’ont aucune valeur de rétention au-delà de quelques jours. L’utilisation de la gestion des enregistrements de messagerie pour supprimer ces messages permet de réduire l’encombrement d’informations dans les boîtes aux lettres des utilisateurs, augmentant ainsi la productivité.

  - **Améliorer la gestion du stockage**   En raison des attentes alimentées par les services de messagerie gratuits, de nombreux utilisateurs conservent les anciens messages pendant des périodes prolongées ou ne les suppriment jamais. La gestion de boîtes aux lettres volumineuses est une pratique de plus en plus courante et les utilisateurs ne devraient pas être obligés de changer leurs habitudes de travail pour respecter des quotas limitant la taille de leur boîte aux lettres. Toutefois, la conservation des messages au-delà de la période nécessaire pour des raisons commerciales, juridiques ou réglementaires entraîne également une augmentation des coûts de stockage.

La gestion MRM offre la flexibilité nécessaire pour implémenter la stratégie de gestion des enregistrements qui répond le mieux aux besoins de votre organisation. Si vous maîtrisez bien la gestion des enregistrements de messagerie, l’archivage local et le blocage sur place, vous pouvez satisfaire vos exigences en termes de gestion du stockage de boîte aux lettres et de conformité à la réglementation en matière de rétention.

Souhaitez-vous rechercher les tâches de gestion relatives à la gestion des enregistrements de messagerie ? Voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## MRM dans Exchange Server 2013 et Exchange Online

Dans Exchange Server 2013 et Exchange Online, la gestion des enregistrements de messagerie est effectuée en utilisant des balises et des stratégies de rétention. Les balises de rétention permettent d’appliquer des paramètres de rétention à une boîte aux lettres complète et à des dossiers de boîtes aux lettres par défaut, tels que Boîte de réception et Éléments supprimés. Vous pouvez également créer et déployer des balises de rétention que les utilisateurs d’Outlook 2010 et les versions ultérieures, ainsi que d’Outlook Web App peuvent appliquer à des dossiers ou messages individuels. Une fois les balises de rétention créées, vous les ajoutez à une stratégie de rétention que vous appliquez ensuite à des utilisateurs. L’Assistant Dossier géré traite les boîtes aux lettres et applique des paramètres de rétention dans la stratégie de rétention de l’utilisateur. Pour en savoir plus sur les stratégies de rétention, consultez la rubrique [Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md).

Lorsqu’un message atteint l’âge de rétention spécifié dans la balise de rétention applicable, l’Assistant Dossier géré adopte l’action de rétention spécifiée par la balise. Vous pouvez ensuite supprimer définitivement des messages ou les supprimer tout en ayant la possibilité de les récupérer. Si une archive a été configurée pour l’utilisateur, vous pouvez également utiliser les balises de rétention pour déplacer des éléments vers l’archive locale de l’utilisateur.

## Stratégies de gestion des enregistrements de messagerie

Vous pouvez utiliser des stratégies de rétention pour appliquer une rétention élémentaire des messages à une boîte aux lettres complète ou des dossiers par défaut spécifiques. Bien qu’il existe plusieurs stratégies pour déployer la gestion des enregistrements de messagerie, voici quelques-unes des plus courantes :

**Supprimer tous les messages après une période déterminée**   Dans cette stratégie, vous implémentez une seule stratégie de gestion des enregistrements de messagerie qui supprime tous les messages après un certain temps. Dans cette stratégie, il n’y a aucune classification des messages. Vous pouvez implémenter cette stratégie en créant une balise de stratégie par défaut pour la boîte aux lettres. Toutefois, la conservation des messages pendant la période spécifiée n’est pas garantie. Les utilisateurs peuvent toujours supprimer des messages avant la fin de la période de rétention.

**Déplacer les messages vers les boîtes aux lettres d’archivage**   Dans cette stratégie, vous implémentez des stratégies de gestion des enregistrements de messagerie qui déplacent des éléments vers la boîte aux lettres de l’utilisateur. Une boîte aux lettres d’archivage représente du stockage supplémentaire pour les utilisateurs qui gèrent des contenus anciens ou rarement sollicités. Les balises de rétention qui déplacent des éléments sont également connues sous le nom de *stratégies d’archivage*. Dans la même stratégie de rétention, vous pouvez combiner une balise de stratégie par défaut et des balises personnelles pour déplacer des éléments, et une balise de stratégie par défaut, des balises de stratégie de rétention et des balises personnelles pour supprimer des éléments. Pour en savoir plus sur les stratégies d’archivage, voir :

  - **Exchange Server 2013:** [Archivage inaltérable dans Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [Boîtes aux lettres d’archivage dans Exchange Online](https://technet.microsoft.com/fr-fr/library/dn922147\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans un déploiement hybride Exchange, vous pouvez activer une boîte aux lettres d’archivage en nuage pour une boîte aux lettres principale locale. Si vous attribuez une stratégie d’archivage à une boîte aux lettres locale, les éléments sont déplacés vers l’archive en nuage. Si un élément est déplacé vers la boîte aux lettres d’archivage, une copie n’est pas conservée dans la boîte aux lettres locale. Si la boîte aux lettres locale est placée en conservation, une stratégie d’archivage déplacera les éléments vers la boîte aux lettres d’archivage en nuage dans laquelle ils sont conservés pendant la durée spécifiée par la conservation.</td>
</tr>
</tbody>
</table>


**Supprimer les messages en fonction de l’emplacement du dossier**   Dans cette stratégie, vous implémentez des stratégies de gestion des enregistrements de messagerie en fonction de l’emplacement des messages. Par exemple, vous pouvez indiquer que les messages contenus dans la boîte de réception sont conservés pendant un an et que les messages du dossier Courrier indésirable sont conservés pendant 60 jours. Vous pouvez mettre en œuvre cette stratégie en utilisant une combinaison de balises de stratégie de rétention pour chaque dossier par défaut que vous souhaitez configurer et une balise de stratégie par défaut pour la boîte aux lettres entière. La balise de stratégie par défaut s’applique à tous les dossiers personnalisés et à tous les dossiers par défaut auxquels une balise de stratégie de rétention n’est pas appliquée.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dans Exchange 2013, vous pouvez créer des balises de stratégie de rétention pour les dossiers Calendrier et Tâches. Si vous souhaitez que certains éléments de ces dossiers ou d’autres dossiers par défaut n’expirent pas, vous pouvez créer une balise de rétention désactivée pour ce dossier par défaut.</td>
</tr>
</tbody>
</table>


**Autoriser les utilisateurs à classer les messages**    Dans cette stratégie, vous implémentez des stratégies de gestion des enregistrements de messagerie qui incluent un paramètre de rétention de référence pour tous les messages mais autorisent les utilisateurs à classer les messages en fonction des exigences commerciales ou réglementaires. Dans ce cas, les utilisateurs constituent un élément important de votre stratégie de gestion des enregistrements. Souvent, ils ont une meilleure compréhension de la valeur de rétention d’un message.

Les utilisateurs peuvent appliquer différents paramètres de rétention aux messages qui doivent être conservés pendant une période plus ou moins longue. Vous pouvez mettre en œuvre cette stratégie en utilisant une combinaison des éléments suivants :

  - Une balise de stratégie par défaut

  - Des balises personnelles que les utilisateurs peuvent appliquer à des messages personnalisés ou des messages individuels

  - (Facultatif) Vous pouvez ajouter des balises de stratégie de rétention pour provoquer l’expiration d’éléments dans des dossiers par défaut spécifiques

Vous pouvez, par exemple, utiliser une stratégie de rétention avec des balises personnelles dont la période de rétention est plus courte (à savoir 2 jours, 1 semaine ou 1 mois), ainsi que des balises personnelles dont la période de rétention est plus longue (à savoir 1, 2 ou 5 ans). Les utilisateurs peuvent appliquer des balises personnelles dotées de périodes de rétention plus courtes à des éléments, tels que des abonnements à des bulletins d’informations susceptibles de perdre leur valeur dans les jours suivant leur réception, et appliquer des balises dotées de périodes plus longues pour préserver les éléments à forte valeur commerciale. Ils peuvent également automatiser le processus en utilisant les règles de boîte de réception dans Outlook pour appliquer une balise personnelle aux messages qui correspondent aux conditions de règle.

**Conserver les messages à des fins de découverte électronique**   Dans cette stratégie, vous implémentez des stratégies de gestion des enregistrements de messagerie qui suppriment des messages des boîtes aux lettres après une période spécifiée mais les conservent aussi dans le dossier Éléments récupérables pour la [Découverte électronique locale](in-place-ediscovery-exchange-2013-help.md), même si les messages ont été supprimés par l’utilisateur ou par un autre processus.

Vous pouvez répondre à cette exigence en utilisant une combinaison de stratégies de rétention et le [Conservation inaltérable et conservation pour litige](in-place-hold-and-litigation-hold-exchange-2013-help.md) ou la suspension pour litige. Les stratégies de rétention permettent de supprimer les messages de la boîte aux lettres à la fin de la période spécifiée. La suspension pour litige ou le blocage sur place temporel permet de conserver les messages qui ont été supprimés ou modifiés avant cette période. Par exemple, pour conserver des messages pendant sept ans, vous pouvez créer une stratégie de rétention avec une balise de stratégie par défaut (DPT) qui supprime les messages dans sept ans et une suspension pour litige pour conserver les messages pendant sept ans. Les messages qui ne sont pas supprimés par les utilisateurs le seront au bout de sept ans et les messages supprimés par les utilisateurs avant que la période de sept ans ne soit écoulée seront conservés pendant sept ans dans le dossier Éléments récupérables. Pour en savoir plus sur ce dossier, consultez la rubrique [Dossier Éléments récupérables](recoverable-items-folder-exchange-2013-help.md).

Vous pouvez, si vous le souhaitez, utiliser des balises de stratégie de rétention pour permettre aux utilisateurs de nettoyer leurs boîtes aux lettres. Toutefois, la suspension pour litige et le blocage sur place continuent à conserver les messages supprimés jusqu’à l’expiration de la période de blocage.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Une suspension pour litige ou un blocage sur place temporel ressemble à ce qui était communément appelé une <em>mise en suspens temporaire pour raisons juridiques</em> dans Exchange 2010. La mise en suspens temporaire pour raisons juridiques a été implémentée en configurant la période de rétention des éléments supprimés pour une base de données de boîtes aux lettres ou une boîte aux lettres individuelle. Toutefois, la rétention des éléments supprimés permet de conserver les éléments supprimés et modifiés à la date de suppression. La suspension pour litige et le blocage sur place conservent les éléments en fonction de leur date de réception ou de création. Cela permet de garantir que les messages sont conservés pendant au moins la période spécifiée.</td>
</tr>
</tbody>
</table>


## Pour plus d'informations

[Des enregistrements de messagerie terminologie de gestion dans Exchange 2013](messaging-records-management-terminology-in-exchange-2013-exchange-2013-help.md)

[Balises et stratégies de rétention](retention-tags-and-retention-policies-exchange-2013-help.md)

