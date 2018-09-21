---
title: 'Connexion au service d’audit administrateur: Exchange 2013 Help'
TOCTitle: Connexion au service d’audit administrateur
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50555370
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connexion au service d’audit administrateur

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2018-03-05_

Vous pouvez utiliser l'enregistrement d'audit administrateur dans Microsoft Exchange Server 2013 pour enregistrer toutes les modifications apportées par un utilisateur ou un administrateur de votre organisation. En conservant un journal des modifications, vous pouvez suivre les modifications jusqu'à la personne qui les a effectuées, renforcer vos journaux de modifications avec des enregistrements détaillés de la modification telle qu'elle a été mise en place, vous conformer aux exigences et demandes réglementaires sur les découvertes et bien plus.

Par défaut, la journalisation d'audit est activée dans les nouvelles installations d'Exchange 2013.

**Contenu de cette rubrique**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## Ce qui est analysé

Les cmdlets exécutées directement dans l'environnement de ligne de commande Exchange Management Shell sont auditées. De plus, les opérations effectuées à l'aide du Centre d'administration Exchange (CAE) sont également consignées, car elles exécutent des cmdlets en arrière-plan.

Applets de commande, où ils sont exécuté, sont audités si une applet de commande se trouve sur l’applet de commande l’audit de la liste et un ou plusieurs paramètres sur cette applet de commande se trouvent sur la liste des paramètres d’audit. L’enregistrement d’audit est destinée à afficher les actions qui ont été prises pour modifier des objets dans une organisation Exchange plutôt que les objets qui ont été visionnés.

> [!IMPORTANT]
> Une cmdlet peut ne pas être enregistrée si une erreur s'est produite avant que la cmdlet appelle l'agent d'extension du journal d'audit d'administration. Si une erreur se produit après l'appel de l'agent du journal d'audit d'administration, la cmdlet, ainsi que l'erreur qui lui est associée, est enregistrée. Pour plus d'informations, consultez la section Admin Audit Log Agent présentée ci-après dans cette rubrique.
> Les modifications apportées avec les outils de gestion Microsoft Exchange Server 2010 sont consignées, mais pas celles effectuées à l'aide des outils de gestion Microsoft Exchange Server 2007.
> Les modifications apportées à la configuration de l'enregistrement d'audit sont actualisées toutes les 60 minutes sur les ordinateurs ayant l'environnement de ligne de commande Exchange Management Shell ouvert au moment de la modification de la configuration. Si vous souhaitez appliquer les modifications immédiatement, fermez et rouvrez l'environnement de ligne de commande Exchange Management Shell sur chaque ordinateur.
> 15 minutes peuvent être nécessaires pour qu'une commande apparaisse dans les résultats de la recherche du journal d'audit après son exécution, car les entrées du journal d'audit doivent être indexées avant que ces dernières ne puissent faire l'objet d'une recherche. Si une commande n'apparaît pas dans le journal d'audit de l'administrateur, patientez quelques minutes, puis réeffectuez la recherche.



## Configuration de la journalisation d'audit

Par défaut, si l’enregistrement d’audit est activé, une entrée de journal est créée chaque fois qu’une applet de commande est exécuté. Si vous ne voulez pas auditer chaque applet de commande est exécutée, vous pouvez configurer l’enregistrement d’audit pour auditer uniquement les applets de commande et les paramètres que qui vous intéressent. Vous configurez l’enregistrement d’audit avec l’applet de commande **Set-AdminAuditLogConfig** . Les paramètres référencés dans les sections suivantes sont utilisées avec cette applet de commande.

> [!IMPORTANT]
> Les modifications apportées à la configuration de l'enregistrement d'audit sont toujours consignées, que la cmdlet <strong>Set-AdministratorAuditLog</strong> figure dans la liste des cmdlet auditées ou non et que l'enregistrement d'audit administrateur soit activé ou non.


Lorsqu'une commande est exécutée, Exchange inspecte la cmdlet utilisée. Si la cmdlet exécutée correspond à une des cmdlets fournies avec le paramètre *AdminAuditLogConfigCmdlets*, Exchange contrôle ensuite les paramètres spécifiés dans le paramètre *AdminAuditLogConfigParameters*. Si au moins un paramètre de la liste des paramètres correspond, Exchange enregistre la cmdlet exécutée dans la boîte aux lettres spécifiée à l'aide du paramètre *AdminAuditLogMailbox*. Les sections suivantes contiennent d'autres informations sur chaque aspect de la configuration de l'enregistrement d'audit.

Pour plus d'informations sur la gestion de la configuration de la journalisation d'audit, consultez la rubrique [Gestion de la journalisation d’audit de l’administrateur](manage-administrator-audit-logging-exchange-2013-help.md).

Retour au début

## Cmdlets

Vous pouvez contrôler quelles cmdlets sont auditées en fournissant une liste de cmdlets et leurs paramètres associés que vous souhaitez enregistrer. Lorsque vous configurez la journalisation d'audit, vous pouvez opter pour un audit de chaque cmdlet ou désigner des cmdlets spécifiques à vérifier à l'aide du paramètre *AdminAuditLogConfigCmdlets*. Vous pouvez spécifier les noms complets des cmdlets, par exemple **New-Mailbox**, ou les noms partiels des cmdlets et placer ces noms entre des caractères génériques tels qu'un astérisque (`*`). Par exemple, pour tenir le journal de chaque exécution d'une cmdlet contenant la chaîne `Transport`, vous pouvez spécifier une valeur de`*Transport*`. Vous pouvez mélanger des noms complets et partiels de cmdlets pour personnaliser la configuration de l'enregistrement d'audit en fonction de vos besoins.

## Paramètres

En plus de spécifier quelles cmdlets doivent être enregistrées dans le journal, vous pouvez également indiquer que les cmdlets ne seront enregistrés que si certains paramètres associés sont utilisés. Utilisez le paramètre *AdminAuditLogConfigParameters* pour spécifier quels paramètres doivent être enregistrés. Comme pour les cmdlets, vous pouvez spécifier les noms complets des paramètres, par exemple `Database`, ou utiliser des noms partiels placés entre des caractères génériques (`*`), tels que `*Address*`, ou une combinaison des deux.

## Limite d'âge de journal d'audit

Par défaut, l'enregistrement d'audit est configuré pour stocker les entrées de journal d'audit pendant 90 jours. Après 90 jours, l'entrée du journal d'audit est supprimée. Vous pouvez modifier la durée de vie du journal d'audit à l'aide du paramètre *AdminAuditLogAgeLimit*. Vous pouvez spécifier le nombre de jours, d'heures, de minutes et de secondes correspondant à la durée pendant laquelle les entrées de journal d'audit peuvent être conservées. Pour spécifier une valeur, utilisez le format `dd.hh:mm:ss` où ce qui suit s'applique :

  - **jj**   Le nombre de jours durant lesquels conserver l'entrée du journal d'audit.

  - **hh**   Le nombre d'heures durant lesquelles conserver l'entrée du journal d'audit.

  - **mm**   Le nombre de minutes durant lesquelles conserver l'entrée du journal d'audit.

  - **ss**   Le nombre de secondes durant lesquelles conserver l'entrée du journal d'audit.

Vous devez spécifier plusieurs années à l'aide du champ `dd`. Par exemple, 365 jours correspondent à une année, 730 jours à deux ans, 913 jours à deux ans et six mois. Par exemple, pour définir la durée de vie du journal d'audit sur deux ans et six mois, utilisez la syntaxe `913.00:00:00`.

> [!CAUTION]
> Vous pouvez définir la limite d'âge du journal d'audit sur une valeur inférieure à la durée de vie actuelle. Si vous procédez de la sorte, toute entrée de journal d'audit dont l'âge dépasse la nouvelle limite d'âge sera supprimée.
> Si vous définissez la durée de vie sur 0, Exchange supprimera toutes les entrées dans le journal d'audit.
> Nous vous conseillons d'attribuer les autorisations pour configurer la limite d'âge du journal d'audit uniquement aux utilisateurs de confiance.


## Journalisation des informations détaillées

Par défaut, le journal d'audit de l'administrateur ne consigne que le nom de la cmdlet, les paramètres de la cmdlet (et les valeurs spécifiées), l'objet qui a été modifié, le nom de l'utilisateur qui a exécuté la cmdlet, l'heure d'exécution de la cmdlet et le serveur sur lequel elle a été exécutée. Le journal d’audit de l’administrateur ne consigne pas les propriétés qui ont été modifiées sur l’objet. Si vous souhaitez inclure les propriétés modifiées de l'objet dans le journal d'audit, vous pouvez activer la journalisation des informations détaillées en définissant le paramètre *LogLevel* sur `Verbose`. Lorsque vous activez la journalisation des informations détaillées, en plus des informations consignées par défaut, les propriétés modifiées sur un objet, notamment leurs anciennes et nouvelles valeurs, sont incluses dans le journal d'audit.

## Cmdlets de test

Les cmdlets qui commencent par le verbe **Test** ne sont pas enregistrées par défaut. Vous pouvez indiquer que les cmdlets **Test** doivent être enregistrées en définissant le paramètre *TestCmdletLoggingEnabled* sur `$true`. Bien que vous puissiez activer la journalisation des cmdlets de test, nous vous recommandons de ne le faire que sur de courtes périodes, car elles peuvent générer une quantité importante d'informations.

## Journaux d'audit

Chaque fois qu'une cmdlet est enregistrée, une entrée de journal d'audit est créée. Les journaux d'audits sont stockés dans une boîte aux lettres d'arbitrage dédiée et cachée qui n'est accessible qu'à l'aide du Centre d'administration Exchange (CAE) ou de la cmdlet **Search-AdminAuditLog** ou **New-AdminAuditLogSearch**. Son ouverture n'est pas possible avec Microsoft Outlook Web App ou Microsoft Outlook. Les sections ci-dessous fournissent les informations suivantes :

  - Le contenu des journaux

  - Les rapports disponibles dans la page d'**audit** du Centre d'administration Exchange

  - Les cmdlets de recherche de journal d'audit

## Contenu des journaux d'audit

Chaque entrée de journal d'audit contient les informations décrites dans le tableau suivant. Le journal d'audit contient une ou plusieurs entrées de journal d'audit. Le nombre d'entrées de journal d'audit est contrôlé par la limite d'âge du journal d'audit spécifiée à l'aide de la cmdlet **Set-AdminAuditLogConfig**. Toute entrée du journal d'audit qui dépasse la limite d'âge est supprimée.

### Champs d'entrée de journal d'audit

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Champ</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>Ce champ est utilisé en interne par Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>Ce champ contient l'objet modifié par la cmdlet spécifiée dans le champ <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>Ce champ contient le nom de la cmdlet exécutée par l'utilisateur dans le champ <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>Ce champ contient les paramètres spécifiés lorsque la cmdlet dans le champ <code>CmdletName</code> a été exécutée. La valeur spécifiée avec le paramètre est également stockée dans ce champ, mais invisible dans la sortie par défaut, le cas échéant. Pour plus d'informations sur l'accès aux informations supplémentaires dans ce champ, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes">Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>Ce champ contient les propriétés modifiées sur l'objet dans le champ <code>ObjectModified</code>. L'ancienne valeur de la propriété et la nouvelle valeur stockée sont également stockées dans ce champ, mais sont invisibles dans la sortie par défaut. Pour plus d'informations sur l'accès aux informations supplémentaires dans ce champ, consultez la rubrique <a href="https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes">Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur</a>.</p>

> [!IMPORTANT]  
> Ce champ est uniquement renseigné si le paramètre <em>LogLevel</em> de la cmdlet <strong>Set-AdminAuditLogConfig</strong> est défini sur <code>Verbose</code>.

</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>Ce champ contient le compte d'utilisateur de l'utilisateur qui a exécuté la cmdlet dans le champ <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>Ce champ indique si la cmdlet dans le champ <code>CmdletName</code> a été correctement exécutée. La valeur est <code>True</code> ou <code>False</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>Ce champ contient le message d'erreur généré si la cmdlet dans le champ <code>CmdletName</code> n'a pas été correctement exécutée.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>Ce champ contient la date et l'heure à laquelle la cmdlet dans le champ <code>CmdletName</code> a été exécutée. La date et l'heure sont enregistrées au format temps universel coordonné (UTC).</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>Ce champ indique le serveur sur lequel la cmdlet spécifiée dans le champ <code>CmdletName</code> a été exécutée.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Ce champ est utilisé en interne par Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>Ce champ est utilisé en interne par Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>Ce champ est utilisé en interne par Exchange.</p></td>
</tr>
</tbody>
</table>


Retour au début

## Rapports d'audit du Centre d'administration Exchange (CAE)

La page **Audit** du CAE contient plusieurs rapports qui fournissent des informations sur différents types de modifications de configuration d'administration et de conformité. Les rapports suivants fournissent des informations sur les modifications de configuration dans votre organisation :

  - **Rapport de groupe de rôles d'administrateur**   Ce rapport vous permet de rechercher les modifications dans les groupes de rôles de gestion que vous spécifiez au cours d'une période. Les résultats renvoyés incluent les groupes de rôles qui ont été modifiés, par qui et leur date ainsi que les modifications qui ont été apportées. 3 000 entrées maximum peuvent être renvoyées. Si votre recherche peut renvoyer plus de 3 000 entrées, utilisez le rapport **Journal d'audit de l'administrateur** ou la cmdlet **Search-AdminAuditLog**.

  - **Journal d'audit de l'administrateur**   Ce rapport vous permet d'exporter les entrées de journal d'audit enregistrées au cours d'une période spécifiée vers un fichier XML, puis d'envoyer ce dernier par courrier électronique à un destinataire donné. Pour plus d'informations sur le contenu du fichier XML, consultez la rubrique [Structure du journal d’audit de l’administrateur](administrator-audit-log-structure-exchange-2013-help.md).

Pour plus d'informations sur l'utilisation de ces rapports, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes).

Pour plus d'informations sur les autres rapports inclus dans la page **Audit**, consultez la rubrique [Rapports d’audit Exchange](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports).

## Cmdlet Search-AdminAuditLog

Lorsque vous exécutez la cmdlet **Search-AdminAuditLog**, toutes les entrées de journaux d'audit qui correspondent aux critères de recherche spécifiés sont renvoyées. Vous pouvez spécifier les critères de recherche suivants :

  - **Cmdlet**   Spécifie les cmdlets que vous souhaitez rechercher dans le journal d'audit administrateur.

  - **Paramètres**   Spécifie les paramètres, séparés par des virgules, que vous souhaitez rechercher dans le journal d'audit de l'administrateur. Vous ne pouvez rechercher des paramètres que si vous avez spécifié une cmdlet à rechercher.

  - **Date de fin**   Étend les résultats du journal d'audit administrateur aux entrées du journal survenues à la date spécifiée ou avant cette date.

  - **Date de début**   Étend les résultats du journal d'audit administrateur aux entrées du journal survenues à la date spécifiée ou après cette date.

  - **Identificateurs d'objets**   Précise que seules des entrées du journal d'audit administrateur contenant les objets modifiés spécifiés peuvent être renvoyées

  - **Identificateurs d'utilisateurs**   Précise que seules des entrées du journal d'audit administrateur contenant les ID spécifiés de l'utilisateur qui a exécuté la cmdlet peuvent être renvoyées.

  - **Exécution réussie**   Spécifie si seules les entrées du journal d'audit administrateur qui signalaient une réussite ou un échec doivent être renvoyées.

Chaque entrée de journal d'audit renvoyée contient les informations décrites dans le tableau dans Audit Log Contents. Par défaut, seules les 1 000 premières entrées de journal qui correspondent aux critères que vous spécifiez sont renvoyées. Cependant, vous pouvez annuler cette valeur par défaut et renvoyer plus ou moins d'entrées à l'aide du paramètre *ResultSize*. Vous pouvez spécifier une valeur de `Unlimited` avec le paramètre *ResultSize* pour renvoyer toutes les entrées de journal correspondant aux critères spécifiés.

Pour obtenir des informations sur l'utilisation de la cmdlet **Search-AdminAuditLog**, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes).

## Cmdlet New-AdminAuditLogSearch

La cmdlet **New-AdminAuditLogSearch** effectue des recherches dans le journal d'audit tout comme la cmdlet **Search-AdminAuditLog**. Cependant, plutôt que d'afficher les résultats de la recherche du journal d'audit dans l'environnement de ligne de commande Exchange Management Shell, la cmdlet **New-AdminAuditLogSearch** effectue la recherche, puis envoie les résultats par courrier électronique au destinataire spécifié. Les résultats sont inclus en tant que pièce jointe XML dans le message électronique.

Vous pouvez utiliser les mêmes critères de recherche avec la cmdlet **New-AdminAuditLogSearch** que ceux utilisés avec la cmdlet **Search-AdminAuditLog**. Pour obtenir la liste des critères de recherche, consultez la rubrique Search-AdminAuditLog Cmdlet.

Après exécution de la cmdlet **New-AdminAuditLogSearch**, Exchange peut prendre jusqu'à 15 minutes pour remettre le rapport au destinataire spécifié. Le rapport sous forme de fichier XML joint peut avoir une taille maximale de 10 mégaoctets (Mo). Le fichier XML contient les mêmes informations décrites dans le tableau dans Audit Log Contents. Pour plus d'informations sur la structure du fichier XML, consultez la rubrique [Structure du journal d’audit de l’administrateur](administrator-audit-log-structure-exchange-2013-help.md).

> [!NOTE]  
> Outlook Web App ne vous permet pas d’ouvrir des pièces jointes au format XML par défaut. Vous pouvez soit configurer Exchange de façon à autoriser l’affichage des pièces jointes au format XML à l’aide d’Outlook Web App, soit utiliser un autre client de messagerie électronique, tel que Microsoft Outlook, de façon à afficher la pièce jointe. Pour plus d’informations sur la configuration d’Outlook Web App afin de permettre l’affichage d’une pièce jointe au format XML, consultez la rubrique <a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Affichage ou configuration des répertoires virtuels d’Outlook Web App</a>.


Pour des informations sur l'utilisation de la cmdlet **New-AdminAuditLogSearch**, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes).

Retour au début

## Entrées de journal d'audit manuelles

En plus d'enregistrer les cmdlets Exchange lorsqu'elles sont exécutées, Exchange 2013 vous permet d'écrire manuellement des entrées de journal dans le journal d'audit. Exchange 2013 prend en charge cette fonctionnalité à l'aide de la cmdlet **Write-AdminAuditLog**. Les situations dans lesquelles vous devrez ajouter manuellement une entrée de journal sont les suivantes :

  - Entrée et sortie de script personnalisé

  - Informations de contrôle de modification

  - Heures de début et de fin de maintenance

À l'aide de la cmdlet **Write-AdminAuditLog**, vous spécifiez une chaîne de texte à inclure dans le journal d'audit à l'aide du paramètre *Comment*. Le paramètre *Comment* accepte une chaîne alphanumérique comportant jusqu'à 500 caractères. Les informations incluses dans l'entrée de journal manuelle et la chaîne de commentaire sont exactement les mêmes que celles enregistrées avec une cmdlet Exchange. Pour une description de chaque champ du journal d'audit, consultez le tableau dans Audit Log Contents.

Vous pouvez extraire les entrées de journal d'audit manuelles de la même manière que n'importe quelle autre entrée à l'aide de la page **Audit** du Centre d'administration Exchange ou de la cmdlet **Search-AdminAuditLog** ou **New-AdminAuditLogSearch**.

Pour afficher le contenu du paramètre *Comment* sur la cmdlet **Write-AdminAuditLog** dans une entrée de journal d'audit manuelle, consultez la rubrique [Rechercher les modifications des groupes de rôles ou les journaux d’audit de l’administrateur](https://docs.microsoft.com/fr-fr/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes).

## Réplication Active Directory

L'enregistrement d'audit d'administrateur s'appuie sur la réplication Active Directory pour répliquer les paramètres de configuration que vous spécifiez pour les contrôleurs de domaine de votre organisation. Selon vos paramètres de réplication, les modifications que vous apportez ne prendront peut-être pas immédiatement effet sur l'ensemble des serveurs Exchange 2013 ou Exchange 2010 de votre organisation.

## Agent du journal d'audit d'administration

L'agent d'extension de la cmdlet intégré au Journal d'audit d'administration effectue la journalisation d'audit des opérations des cmdlets dans Exchange 2013. Cet agent lit la configuration de la journalisation d'audit, puis effectue une évaluation de chaque cmdlet exécutée dans votre organisation. Si le critère que vous avez spécifié dans la configuration du journal d'audit correspond à la cmdlet exécutée, l'agent génère un journal d'audit.

L'agent du journal d'audit d'administration est activé par défaut afin que l'enregistrement d'audit puisse fonctionner. Il ne peut pas être désactivé et sa priorité ne peut pas être modifiée. Pour plus d'informations sur les agents d'extension de cmdlet, consultez la rubrique [Agents d’extension des cmdlets](cmdlet-extension-agents-exchange-2013-help.md).

