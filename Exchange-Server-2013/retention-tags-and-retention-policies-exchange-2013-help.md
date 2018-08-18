---
title: 'Balises et stratégies de rétention: Exchange 2013 Help'
TOCTitle: Balises et stratégies de rétention
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 50478029
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Balises et stratégies de rétention

 

_**Sapplique à :** Exchange Online, Exchange Server 2013_

_**Dernière rubrique modifiée :** 2016-12-09_

Dans Microsoft Exchange Server 2013 et Exchange Online, la gestion des enregistrements de messagerie (MRM) permet aux organisations de gérer le cycle de vie des messages électroniques et de réduire les risques juridiques associés aux communications par messagerie électronique et par d’autres moyens. La gestion des enregistrements de messagerie facilite la conservation des messages nécessaire pour se conformer à la stratégie de la société, aux réglementations gouvernementales ou aux exigences légales, ainsi que la suppression du contenu dépourvu de valeur légale ou commerciale.

Regardez cette [vidéo](http://go.microsoft.com/fwlink/?linkid=825854) pour obtenir un aperçu rapide de la façon d’appliquer des balises de rétention et une stratégie de rétention à une boîte aux lettres dans Exchange Online.

Vous recherchez des procédures détaillées pour gérer MRM ? Voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

**Contenu de cette rubrique**

Stratégie de gestion des enregistrements de messagerie

Balises de rétention

Stratégies de rétention

Assistant Dossier géré

Blocage de rétention

## Stratégie de gestion des enregistrements de messagerie

La gestion des enregistrements de messagerie dans Exchange 2013 et Exchange Online est réalisée à l’aide de *balises de rétention* et de *stratégies de rétention*. Avant d’aborder en détail chacune de ces fonctions de rétention, il est important de comprendre comment elles sont utilisées dans le cadre de la stratégie MRM globale. Cette stratégie est basée sur :

  - L’attribution de *balises de stratégie de rétention* (RPT) aux dossiers par défaut, tels que les dossiers Boîte de réception et Éléments supprimés.

  - L’application de *balises de stratégie par défaut* (DPT) aux boîtes aux lettres pour gérer la rétention de tous les éléments non balisés.

  - La possibilité pour l’utilisateur d’attribuer des *balises personnelles* aux dossiers personnalisés et aux éléments individuels.

  - La séparation de la fonctionnalité de gestion des enregistrements de messagerie des habitudes des utilisateurs en matière de classement et de gestion de leurs boîtes de réception. Les utilisateurs ne sont pas obligés de classer leurs messages dans des dossiers gérés en fonction des exigences en matière de rétention. Les messages individuels peuvent avoir une balise de rétention différente de celle appliquée au dossier qui les contient.

La figure suivante illustre les tâches impliquées dans la mise en œuvre de cette stratégie.

![Utilisation de stratégies de rétention de messagerie](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "Utilisation de stratégies de rétention de messagerie")

Retour au début

## Balises de rétention

Comme illustré dans la figure précédente, les balises de rétention servent à appliquer des paramètres de rétention aux dossiers et aux éléments individuels, tels que des messages électroniques et la messagerie vocale. Ces paramètres spécifient la durée pendant laquelle un message reste dans une boîte aux lettres et l’action à entreprendre lorsque ce message atteint l’âge de rétention indiqué. Lorsqu’il atteint son âge de rétention, un message est déplacé dans l’archive locale de l’utilisateur ou supprimé.

![Paramètres dans une balise de rétention](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "Paramètres dans une balise de rétention")

Les balises de rétention autorisent les utilisateurs à baliser leurs propres dossiers de boîtes aux lettres et éléments individuels pour la rétention. Les utilisateurs ne sont plus tenus de classer les éléments dans les dossiers gérés configurés par un administrateur, en fonction des exigences de rétention des messages.

## Types de balise de rétention

Les balises de rétention sont classées selon les trois types suivants en fonction de qui peut les appliquer et d’où elles peuvent être appliquées dans une boîte aux lettres.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de balise de rétention</th>
<th>Appliqué…</th>
<th>Appliqué par…</th>
<th>Actions disponibles...</th>
<th>Détails</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Balise de stratégie par défaut (DPT)</p></td>
<td><p>Automatiquement à toute la boîte aux lettres</p>
<p>Une DPT s’applique aux éléments <em>non marqués</em>, c’est-à-dire aux éléments auxquels aucune balise de rétention n’est appliquée directement ou par héritage à partir du dossier.</p></td>
<td><p>Administrateur</p></td>
<td><ul>
<li><p>Déplacer vers l’archive</p></li>
<li><p>Supprimer et autoriser la récupération</p></li>
<li><p>Supprimer définitivement</p></li>
</ul></td>
<td><p>Les utilisateurs ne peuvent pas modifier les balises de stratégie par défaut appliquées à une boîte aux lettres.</p></td>
</tr>
<tr class="even">
<td><p>Balise de stratégie de rétention (RPT)</p></td>
<td><p>Automatiquement à un dossier par défaut</p>
<p>Les dossiers par défaut sont des dossiers créés automatiquement dans toutes les boîtes aux lettres, par exemple : <strong>Boîte de réception</strong>, <strong>Éléments supprimés</strong> et <strong>Éléments envoyés</strong>. Consultez la liste des dossiers par défaut pris en charge dans <a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">Dossiers par défaut prenant en charge les balises de stratégie de rétention</a>.</p></td>
<td><p>Administrateur</p></td>
<td><ul>
<li><p>Supprimer et autoriser la récupération</p></li>
<li><p>Supprimer définitivement</p></li>
</ul></td>
<td><p>Les utilisateurs ne peuvent pas modifier la balise de stratégie de rétention appliquée à un dossier par défaut.</p></td>
</tr>
<tr class="odd">
<td><p>Balise personnelle</p></td>
<td><p>Manuellement aux éléments et aux dossiers</p>
<p>Les utilisateurs peuvent automatiser le balisage à l’aide de règles de boîte de réception pour déplacer un message vers un dossier qui a une balise particulière ou pour appliquer une balise personnelle au message.</p></td>
<td><p>Utilisateurs</p></td>
<td><ul>
<li><p>Déplacer vers l’archive</p></li>
<li><p>Supprimer et autoriser la récupération</p></li>
<li><p>Supprimer définitivement</p></li>
</ul></td>
<td><p>Les balises personnelles permettent à vos utilisateurs de déterminer la durée de rétention d’un élément. Par exemple, la boîte aux lettres peut faire en sorte qu’une balise de stratégie par défaut (DPT) supprime les éléments dans sept ans, mais un utilisateur peut créer une exception pour certains éléments tels que des bulletins d’informations et des notifications automatisées en appliquant une balise personnelle qui les supprime sous trois jours.</p></td>
</tr>
</tbody>
</table>


## Plus d’informations sur les balises personnelles

Les balises personnelles sont accessibles aux utilisateurs d’Outlook 2010 et d’Outlook Web App dans le cadre de leur stratégie de rétention. Dans Outlook 2010 et Outlook Web App, les balises personnelles avec l’action **Déplacer vers l’archive** apparaissent en tant que **Stratégie d’archivage**, et les balises personnelles avec l’action **Supprimer et autoriser la récupération** ou **Supprimer définitivement** apparaissent en tant que **Stratégie de rétention** comme le montre l’illustration suivante.

![Balises personnelles dans Outlook 2010 et Outlook Web App](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Balises personnelles dans Outlook 2010 et Outlook Web App")

Les utilisateurs peuvent appliquer des balises personnelles aux dossiers qu’ils créent ou à des éléments individuels. Les messages avec balise personnelle appliquée sont toujours traités conformément aux paramètres de la balise personnelle. Les utilisateurs peuvent appliquer une balise personnelle à un message afin qu’il soit déplacé ou supprimé avant ou après avoir spécifié les paramètres dans les balises de stratégie par défaut ou les balises de stratégie de rétention appliquées à la boîte aux lettres de cet utilisateur. Vous pouvez également créer des balises personnelles avec la rétention désactivée. Ceci permet à l’utilisateur de baliser des éléments afin qu’ils ne soient jamais déplacés vers une archive ou qu’ils n’expirent jamais.

> [!NOTE]
> Les utilisateurs peuvent appliquer des stratégies d’archivage à des dossiers par défaut, des dossiers ou des sous-dossiers créés par l’utilisateur et des éléments individuels. Les utilisateurs peuvent appliquer une stratégie de rétention à des dossiers ou des sous-dossiers créés par l’utilisateur et à des éléments individuels (y compris à des sous-dossiers et des éléments d’un dossier par défaut) mais pas à des dossiers par défaut.


Les utilisateurs peuvent également utiliser le Centre d’administration Exchange (CAE) pour sélectionner des balises personnelles supplémentaires qui ne sont pas liées à leur stratégie de rétention. Les balises sélectionnées deviennent alors accessibles dans Outlook 2010 et Outlook Web App. Pour permettre aux utilisateurs de sélectionner des balises supplémentaires à partir du Centre d’administration Exchange, vous devez ajouter le [Rôle MyRetentionPolicies](myretentionpolicies-role-exchange-2013-help.md) à la stratégie d’attribution de rôle de l’utilisateur. Pour en savoir plus sur les stratégies d’attribution de rôle pour les utilisateurs, voir la rubrique [Présentation des stratégies d’attribution de rôle de gestion](understanding-management-role-assignment-policies-exchange-2013-help.md). Si vous autorisez des utilisateurs à sélectionner des balises personnelles supplémentaires, toutes les balises personnelles de votre organisation Exchange deviennent accessibles.

> [!NOTE]
> Les balises personnelles sont une fonctionnalité essentielle. Les boîtes aux lettres avec des stratégies qui contiennent ces balises (ou suite à l’ajout de balises aux boîtes aux lettres) requièrent une Licence d’Accès Client (CAL) pour Exchange Enterprise.


Retour au début

## Âge de rétention

Lorsque vous activez une balise de rétention, vous devez lui attribuer un âge de rétention. Cet âge indique le nombre de jours pendant lequel un message est conservé jusqu’à son arrivée dans la boîte aux lettres de l’utilisateur.

L’âge de rétention est calculé de manière différente pour les éléments non périodiques (tels que des messages électroniques) et pour ceux comportant une date de fin ou pour les éléments périodiques (réunions et tâches, par exemple). Pour apprendre à calculer l’âge de rétention pour différents types d’éléments, voir [Méthode de calcul de l’âge de rétention](how-retention-age-is-calculated-exchange-2013-help.md).

De plus, vous pouvez créer des balises de rétention avec la rétention désactivée ou désactiver les balises après leur création. Étant donné que les messages avec une balise désactivée appliquée ne sont pas traités, aucune action de rétention n’est effectuée. Les utilisateurs peuvent donc employer une balise personnelle désactivée en tant que balise **Ne jamais déplacer** ou **Ne jamais supprimer** pour remplacer une balise de stratégie par défaut ou une balise de stratégie de rétention qui s’appliquerait en temps normal au message.

## Actions de rétention

Lors de la création ou de la configuration d’une balise de rétention, vous pouvez sélectionner l’une des actions de rétention suivantes à effectuer lorsqu’un élément atteint son âge de rétention :


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Action de rétention</th>
<th>Action effectuée...</th>
<th>Sauf...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Déplacer vers l’archive</strong> 1</p></td>
<td><ul>
<li><p>Déplace le message vers la boîte aux lettres d’archivage de l’utilisateur.</p></li>
<li><p>Uniquement disponible pour les balises de stratégie par défaut et les balises personnelles</p></li>
</ul>
<p>Pour plus d’informations sur l’archivage, consultez la rubrique :</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archivage inaltérable dans Exchange 2013</a></p></li>
<li><p><a href="https://technet.microsoft.com/fr-fr/library/dn922147(v=exchg.150)">Boîtes aux lettres d’archivage dans Exchange Online</a></p></li>
</ul></td>
<td><ul>
<li><p>Si l’utilisateur e dispose pas d’une boîte aux lettres d’archivage, aucune action n’est effectuée.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Supprimer et autoriser la récupération</strong></p></td>
<td><ul>
<li><p>Imite le comportement de l’utilisateur lorsqu’il vide le dossier Éléments supprimés.</p></li>
<li><p>Les éléments sont déplacés vers <a href="recoverable-items-folder-exchange-2013-help.md">Dossier Éléments récupérables</a> dans la boîte aux lettres et conservés jusqu’à la fin de la période de <em>rétention des éléments supprimés</em>.</p></li>
<li><p>Fournit à l’utilisateur une deuxième chance de récupérer l’élément à l’aide de la boîte de dialogue <strong>Récupérer les éléments supprimés</strong> dans Outlook ou Outlook Web App.</p></li>
</ul></td>
<td><ul>
<li><p>Si vous avez configuré la période de rétention des éléments supprimés à zéro jour, les éléments sont définitivement supprimés. Pour plus d’informations, consultez la rubrique <a href="https://technet.microsoft.com/fr-fr/library/dn163584(v=exchg.150)">Modifier la durée de conservation des éléments supprimés définitivement pour une boîte aux lettres Exchange Online</a>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Supprimer définitivement</strong></p></td>
<td><ul>
<li><p>Supprime définitivement les messages.</p></li>
<li><p>Vous ne pouvez plus récupérer les messages une fois qu’ils sont définitivement supprimés.</p></li>
</ul></td>
<td><ul>
<li><p>Si la boîte aux lettres est placée en <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservation inaltérable et conservation pour litige</a> ou en suspension pour litige, les éléments sont conservés dans le dossier Éléments récupérables en fonction des paramètres de blocage. La fonction <a href="in-place-ediscovery-exchange-2013-help.md">Découverte électronique locale</a> renverra toujours ces éléments dans les résultats de recherche.</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Marquer comme limite de rétention passée</strong></p></td>
<td><ul>
<li><p>Marque un message comme expiré. Dans Outlook 2010 ou versions ultérieures et dans Outlook Web App, les éléments expirés sont affichés avec la notification « Cet élément a expiré » et « Cet élément expirera dans 0 jours ». Dans Outlook 2007, ces éléments sont affichés sous forme de texte barré.</p></li>
</ul></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 1   Dans un déploiement hybride Exchange, vous pouvez activer une boîte aux lettres d’archivage en nuage pour une boîte aux lettres principale locale. Si vous attribuez une stratégie d’archivage à une boîte aux lettres locale, les éléments sont déplacés vers l’archive en nuage. Si un élément est déplacé vers la boîte aux lettres d’archivage, aucune copie n’est conservée dans la boîte aux lettres locale. Si la boîte aux lettres locale est placée en conservation, une stratégie d’archivage déplacera les éléments vers la boîte aux lettres d’archivage en nuage dans laquelle ils sont conservés pendant la durée spécifiée par la conservation.


Pour plus d’informations sur la création de balises de rétention, voir [Créer une stratégie de rétention](create-a-retention-policy-exchange-2013-help.md).

Retour au début

## Stratégies de rétention

Pour appliquer des balises de rétention à une boîte aux lettres, vous devez les ajouter à une stratégie de rétention, puis appliquer la stratégie aux boîtes aux lettres. Une boîte aux lettres ne peut pas avoir plusieurs stratégies de rétention. Vous pouvez à tout moment associer ou non des balises de rétention à une stratégie de rétention, et les modifications prennent automatiquement effet pour toutes les boîtes aux lettres auxquelles la stratégie est appliquée.

Une stratégie de rétention peut avoir les balises de rétention suivantes :


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type de balise de rétention</th>
<th>Balises dans une stratégie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Balise de stratégie par défaut (DPT)</p></td>
<td><ul>
<li><p>Une balise de stratégie par défaut avec l’action <strong>Déplacer vers l’archive</strong></p></li>
<li><p>Une balise de stratégie par défaut avec l’action <strong>Supprimer et autoriser la récupération</strong> ou <strong>Supprimer définitivement</strong></p></li>
<li><p>Une balise de stratégie par défaut pour les messages vocaux avec l’action <strong>Supprimer et autoriser la récupération</strong> ou <strong>Supprimer définitivement</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Balises de stratégie de rétention (RPT)</p></td>
<td><ul>
<li><p>Une balise de stratégie de rétention pour chaque dossier par défaut pris en charge</p>
> [!NOTE]
> Il n’est pas possible d’associer plusieurs balises de stratégie de rétention à la même stratégie de rétention pour un dossier par défaut particulier (comme le dossier <strong>Éléments supprimés</strong>).

</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Balises personnelles</p></td>
<td><ul>
<li><p>N’importe quel nombre de balises personnelles</p></li>
</ul>
> [!TIP]
> Un grand nombre de balises personnelles dans une stratégie peuvent dérouter les utilisateurs. Il est conseillé de ne pas ajouter plus de 10 balises personnelles à une stratégie de rétention.

</td>
</tr>
</tbody>
</table>


> [!NOTE]
> Bien qu’une stratégie de rétention n’ait pas besoin d’être associée à une balise, il n’est pas conseillé d’utiliser ce scénario. Si les boîtes aux lettres dont les stratégies de rétention ne sont pas associées à une balise de rétention, leurs éléments risquent de ne jamais expirer.


Une stratégie de rétention peut contenir des balises d’archive (balises qui déplacent les éléments vers la boîte aux lettres d’archives personnelles) et les balises de rétention (balises qui suppriment des éléments). Ces deux types de balises peuvent être appliqués à un élément de boîte aux lettres. Les boîtes aux lettres d’archives ne possèdent pas de stratégie de rétention distincte. La même stratégie de rétention s’applique à la boîte aux lettres principale et d’archive.

Lorsque vous prévoyez de créer des stratégies de rétention, vous devez déterminer si elles doivent inclure des balises d’archive et de suppression. Comme indiqué précédemment, une stratégie de rétention peut comporter une balise de stratégie par défaut utilisant l’action **Déplacer vers l’archive** et une balise de stratégie par défaut associée à l’action **Supprimer et autoriser la récupération** ou **Supprimer définitivement**. La balise de stratégie par défaut avec l’action **Déplacer vers l’archive** doit avoir un âge de rétention inférieur à la balise de stratégie par défaut associée à une action de suppression. Par exemple, vous pouvez utiliser une balise de stratégie par défaut avec l’action **Déplacer vers l’archive** pour déplacer des éléments vers la boîte aux lettres d’archive dans un délai de deux ans, et une balise associée à l’action de suppression pour supprimer des éléments de la boîte aux lettres sur une période de sept ans. Les éléments présents à la fois dans des boîtes aux lettres principales et d’archivage sont supprimés au bout de sept ans.

Pour obtenir la liste des tâches de gestion relatives aux stratégies de rétention, voir [Procédures de gestion des enregistrements de messagerie](messaging-records-management-procedures-exchange-2013-help.md).

## Stratégie de rétention par défaut

Exchange Le programme d’installation crée la stratégie de rétention appelée **Stratégie MRM par défaut**. La stratégie MRM par défaut est appliquée automatiquement aux nouvelles boîtes aux lettres dans Exchange Online. Dans Exchange Server, la stratégie est appliquée automatiquement si vous créez une archive pour le nouvel utilisateur et que vous n’indiquez pas de stratégie de rétention.

Vous pouvez modifier les balises incluses dans la stratégie MRM par défaut (par exemple, en modifiant la durée ou l’action de rétention), désactiver une balise ou modifier la stratégie en ajoutant ou en supprimant des balises. La stratégie mise à jour est appliquée aux boîtes aux lettres lors du prochain traitement de ces dernières par l’Assistant Dossier géré.

Pour plus d’informations, y compris une liste des balises de rétention liées à la stratégie, voir [Stratégie de rétention par défaut dans Exchange Online et Exchange Server](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md).

Retour au début

## Assistant Dossier géré

L’Assistant Dossier géré, assistant de boîte aux lettres exécuté sur les serveurs de boîtes aux lettres, traite les boîtes aux lettres auxquelles une stratégie de rétention est appliquée.

L’Assistant Dossier géré applique la stratégie de rétention en contrôlant les éléments de la boîte aux lettres et en déterminant s’ils font l’objet d’une rétention. Il marque ensuite les éléments soumis à la rétention avec les balises appropriées et déclenche l’action de rétention spécifiée sur les éléments qui dépassent leur âge de rétention.

L’Assistant Dossier géré est un assistant basé sur la limitation. Ces types d’assistant sont continuellement exécutés et n’ont pas besoin d’être planifiés. Les ressources système qu’ils peuvent utiliser sont limitées. Vous pouvez configurer l’Assistant dossier géré pour traiter toutes les boîtes aux lettres sur un serveur de boîte aux lettres dans une période donnée (appelée *cycle de travail*). En outre, à un intervalle spécifié (appelé *point de contrôle du cycle de travail*), l’assistant actualise la liste des boîtes aux lettres à traiter. Durant ce processus, l’assistant ajoute de nouvelles boîtes aux lettres créées ou déplacées dans la file d’attente. Il redéfinit également la priorité des boîtes aux lettres existantes qui n’ont pas été correctement traitées suite à des erreurs et les déplace à un niveau supérieur de la file d’attente afin qu’elles puissent être traitées dans le même cycle de travail.

Vous pouvez également exécuter la cmdlet [Start-ManagedFolderAssistant](https://technet.microsoft.com/fr-fr/library/aa998864\(v=exchg.150\)) pour déclencher manuellement l’assistant afin qu’il traite une boîte aux lettres spécifique. Pour en savoir plus, voir [Configurer l’Assistant Dossier géré](configure-the-managed-folder-assistant-exchange-2013-help.md).

> [!NOTE]
> L’Assistant Dossier géré n’intervient pas sur les messages ne faisant pas l’objet d’une rétention, ce qui est indiqué par la désactivation de la balise de rétention. Vous pouvez également désactiver une balise de rétention pour suspendre temporairement le traitement des éléments comportant cette balise.


## Déplacement d’éléments d’un dossier à un autre

Un élément de boîte aux lettres déplacé d’un dossier à un autre hérite des balises appliquées au dossier vers lequel il se déplace. Si un élément est déplacé vers un dossier auquel aucune balise n’est attribuée, la balise de stratégie par défaut lui est appliquée. Si une balise est explicitement attribuée à l’élément, la balise est toujours prioritaire sur les balises au niveau des dossiers ou la balise par défaut.

## Application d’une balise de rétention à un dossier dans l’archive

Lorsque l’utilisateur applique une balise personnelle à un dossier dans l’archive, si un dossier portant le même nom existe déjà dans la boîte aux lettres principale et possède une autre balise, la balise de ce dossier dans l’archive est modifiée pour correspondre à celle du dossier figurant dans la boîte aux lettres principale. Il s’agit d’éviter toute confusion sur les éléments d’un dossier dans l’archive ayant un comportement d’expiration différent de celui du même dossier situé dans la boîte aux lettres principale de l’utilisateur. Par exemple, l’utilisateur dispose d’un dossier nommé Projet Contoso dans la boîte aux lettres principale avec une balise *Supprimer – 3 ans* et un dossier Projet Contoso existe également dans la boîte aux lettres d’archivage. Si l’utilisateur applique une balise personnelle *Supprimer – 1 an* pour supprimer des éléments dans le dossier au bout d’un an, lorsque la boîte aux lettres est de nouveau traitée, la balise du dossier est redéfinie sur Supprimer – 3 ans.

## Suppression d’une balise de rétention d’une stratégie de rétention

Lorsqu’une balise de rétention est supprimée de la stratégie de rétention appliquée à une boîte aux lettres, la balise n’est plus accessible à l’utilisateur et ne peut pas être appliquée aux éléments de la boîte aux lettres.

Les éléments existants marqués par cette balise continuent à être traités par l’Assistant Dossier géré en fonction de ces paramètres, et toute action de rétention spécifiée dans la balise est appliquée à ces messages.

Toutefois, si vous supprimez la balise, la définition correspondante stockée dans Active Directory est supprimée. L’Assistant Dossier géré traite alors tous les éléments d’une boîte aux lettres et marque à nouveau ceux auxquels la balise supprimée a été appliquée. Selon le nombre de boîtes aux lettres et de messages, ce processus peut entraîner une consommation considérable en ressources sur tous les serveurs de boîtes aux lettres contenant des boîtes aux lettres dont les stratégies de rétention incluent la balise supprimée.

> [!Important]
> Si une balise de rétention est supprimée d’une stratégie de rétention, tous les éléments de boîte aux lettres existants auxquels la balise est appliquée continuent à expirer conformément aux paramètres de la balise. Pour empêcher l’application des paramètres de la balise aux éléments, vous devez supprimer la balise. La balise est supprimée de toutes les stratégies de rétention dans lesquelles elle est incluse.


## Désactivation d’une balise de rétention

Si vous désactivez une balise de rétention, l’Assistant Dossier géré ignore les éléments auxquels elle est appliquée. Les éléments contenant des balises dont la rétention est désactivée ne sont jamais déplacés ou supprimés, selon l’action de rétention qui a été spécifiée. Étant donné que ces éléments sont toujours considérés comme éléments balisés, la balise de stratégie par défaut ne leur est pas appliquée. Par exemple, si vous souhaitez corriger les paramètres de balise de rétention, vous pouvez désactiver temporairement une balise de rétention pour que l’Assistant Dossier géré arrête le traitement des messages avec cette balise.

> [!NOTE]
> La période de rétention d’une balise de rétention désactivée s’affiche pour l’utilisateur en tant que <strong>Jamais</strong>. Si un utilisateur balise un élément en pensant ne jamais le supprimer, l’activation ultérieure de la balise provoquera une suppression involontaire des éléments que l’utilisateur n’a pas voulu supprimer. Il en va de même pour les balises associées à l’action <strong>Déplacer vers l’archive</strong>.


Retour au début

## Blocage de rétention

Lorsque les utilisateurs sont temporairement absents du bureau et n’ont pas accès à leur messagerie électronique, les paramètres de rétention peuvent être appliqués aux nouveaux messages avant qu’ils ne reviennent au bureau ou n’accèdent à leur messagerie. Selon la stratégie de rétention, les messages peuvent être supprimés ou placés dans l’archive personnelle de l’utilisateur. Vous pouvez empêcher temporairement les stratégies de rétention de traiter une boîte aux lettres sur une période déterminée en activant le blocage de rétention pour la boîte aux lettres. Dans ce cas, vous pouvez également ajouter un commentaire sur le blocage de rétention destiné à l’utilisateur de la boîte aux lettres (ou un autre utilisateur autorisé à accéder à la boîte aux lettres), qui indique notamment à quels moments le blocage doit commencer et s’arrêter. Ce type de commentaire s’affiche dans les clients Outlook pris en charge. Vous pouvez également localiser le commentaire sur le blocage de rétention dans la langue choisie par l’utilisateur.

> [!NOTE]
> L’activation du blocage de rétention pour une boîte aux lettres n’a aucune incidence sur le traitement des quotas de stockage de boîte aux lettres. Selon l’utilisation de la boîte aux lettres et les quotas applicables, envisagez une augmentation temporaire du quota de stockage de boîte aux lettres pour les utilisateurs lorsqu’ils sont en congés ou n’ont pas accès à leur messagerie électronique sur une période prolongée. Pour plus d’informations sur les quotas de stockage de boîte aux lettres, voir <a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configuration de quotas de stockage pour une boîte aux lettres</a>.


Pendant une absence prolongée du bureau, les utilisateurs peuvent accumuler un nombre important de messages électroniques. Selon la quantité de messages et la durée de l’absence, les utilisateurs peuvent mettre plusieurs semaines à trier leurs messages, voire davantage. Dans ce cas, prenez en considération le temps supplémentaire nécessaire aux utilisateurs pour rattraper le temps perdu sur ces messages avant de les supprimer du blocage de rétention.

Si votre organisation n’a jamais mis en place la gestion des enregistrements de messagerie et que vos utilisateurs ne sont pas familiarisés avec ses fonctionnalités, vous pouvez également utiliser le blocage de rétention lors de la phase initiale de *mise en route et de formation* de votre déploiement de la gestion des enregistrements de messagerie. Vous pouvez créer et déployer des stratégies de rétention, et former les utilisateurs aux stratégies sans risquer de déplacer ou de supprimer des éléments avant qu’ils ne puissent les baliser. Quelques jours avant la fin de la période de mise en route et de formation, il convient de rappeler aux utilisateurs le délai de mise en route. Passé ce délai, vous pouvez supprimer le blocage de rétention des boîtes aux lettres d’utilisateurs, permettant ainsi à l’Assistant Dossier géré de traiter les éléments qu’elles contiennent et d’adopter la mesure de rétention spécifiée.

Pour plus d’informations sur l’activation du blocage de rétention pour une boîte aux lettres, consultez la rubrique [Placer une boîte aux lettres en blocage de rétention](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Retour au début

