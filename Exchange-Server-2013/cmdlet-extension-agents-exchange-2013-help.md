---
title: 'Agents d’extension des cmdlets: Exchange 2013 Help'
TOCTitle: Agents d’extension des cmdlets
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50555336
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agents d’extension des cmdlets

 

_**Sapplique à :** Exchange Server 2013_

_**Dernière rubrique modifiée :** 2015-03-09_

Les agents d’extension de cmdlet sont des composants de Microsoft Exchange Server 2013 appelés par des cmdlets d’Exchange 2013 lors de l’exécution des cmdlets. Comme leur nom l’indique, les agents d’extension de cmdlet étendent les fonctionnalités des cmdlets qui les appellent en contribuant au traitement des données ou en effectuant des opérations supplémentaires conformément aux exigences des cmdlets. Les agents d’extension de cmdlet sont accessibles sur tout rôle serveur.

Les agents peuvent modifier, remplacer ou étendre les fonctionnalités des cmdlets Exchange Management Shell. Un agent peut attribuer une valeur à un paramètre requis qui n’est pas spécifiée pour une commande, remplacer une valeur attribuée par un utilisateur, effectuer d’autres opérations non comprises dans le flux de travail de la cmdlet pendant son exécution, et davantage.

Par exemple, la cmdlet **New-Mailbox** accepte le paramètre *Database* qui spécifie la base de données de boîtes aux lettres dans laquelle créer une nouvelle boîte aux lettres. Dans Microsoft Exchange Server 2007, la commande échoue si vous ne spécifiez pas le paramètre *Database* lors de l’exécution de la cmdlet **New-Mailbox**. Cependant, dans Exchange 2013, la cmdlet **New-Mailbox** appelle l’agent de `Mailbox Resources Management` au moment de l’exécution de la cmdlet. Si le paramètre *Database* n’est pas spécifié, l’agent `Mailbox Resources Management` détermine automatiquement une base de données de boîtes aux lettres appropriée sur laquelle créer la nouvelle boîte aux lettres et insère cette valeur dans le paramètre *Database*.

Les agents d’extension de cmdlet ne peuvent être appelés que par des cmdlets Exchange 2013 et Microsoft Exchange Server 2010. Les cmdlets Exchange 2007 et celles fournies par d’autres produits Microsoft et tiers ne peuvent pas appeler des agents d’extension de cmdlet. De même, les scripts ne peuvent pas appeler directement les agents d’extension de cmdlet. Toutefois, si les scripts contiennent les cmdlets Exchange 2013, celles-ci continuent à appeler les agents d’extension de cmdlet.

Souhaitez-vous rechercher les tâches de gestion liées aux agents d’extension de cmdlet ? Voir [Gérer des agents d’extension de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Priorité de l’agent

La priorité d’un agent détermine l’ordre dans lequel celui-ci est appelé lors de l’exécution d’une cmdlet. Un agent dont la priorité est élevée, proche de zéro (0), est appelé en premier. La priorité d’un agent devient importante quand plusieurs agents tentent de définir la valeur de la même propriété. L’agent dont la priorité est élevée réussit à définir une valeur de propriété, alors que toutes les tentatives ultérieures de définition de la même propriété par les agents dont la priorité est moins élevée sont ignorées. Par exemple, si la propriété **Name** sur un objet est modifiée par un agent avec la priorité 3 et qu’un autre agent avec la priorité 6 modifie le même objet, la modification apportée par l’agent avec la priorité 6 est ignorée.

Si vous voulez utiliser l’`Scripting agent` pour définir la valeur des propriétés qui peuvent être définies par d’autres agents dont la priorité est élevée, vous disposez des options suivantes :

  - Désactivez l’agent qui définit actuellement la propriété.

  - Définissez l’`Scripting agent` sur une priorité supérieure à celle de l’agent existant à remplacer.

  - Conservez la priorité des agents et veillez à ce que le script exécuté dans le cadre de l’`Scripting agent` respecte la valeur des autres agents.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La modification de la priorité ou le remplacement de la fonctionnalité d’un agent intégré est une opération avancée. Assurez-vous que vous comprenez totalement les modifications que vous effectuez.</td>
</tr>
</tbody>
</table>


Pour plus d’informations sur la modification de la priorité d’un agent, voir [Gérer des agents d’extension de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Agents intégrés

Exchange 2013 inclut plusieurs agents qui peuvent être appelés au moment de l’exécution d’une cmdlet. Le tableau suivant répertorie les agents, leur ordre et indique s’ils sont activés par défaut. Vous ne pouvez ni ajouter ni supprimer des agents d’un serveur qui exécute Exchange 2013. Cependant, vous pouvez utiliser l’`Scripting agent` pour exécuter des scripts Windows PowerShell afin d’étendre les fonctionnalités des cmdlets qui l’utilisent. Pour plus d’informations sur l’`Scripting agent`, consultez la section « Agent de script » plus loin dans cette rubrique.

Vous pouvez activer ou désactiver la plupart des agents ou encore modifier la priorité des agents si vous voulez remplacer les fonctionnalités d’un agent spécifique par des fonctionnalités d’un script personnalisé que vous appelez à l’aide de l’`Scripting agent`. Cependant, certains agents ne peuvent pas être désactivés. Les agents qui ne peuvent pas être désactivés sont appelés *agents système* et leur propriété *IsSystem* est définie sur `$True`. Le tableau suivant fournit des informations sur les agents d’extension de cmdlet d’Exchange 2013, y compris les agents système.

La configuration des agents est enregistrée au niveau de l’organisation. Lorsque vous activez ou désactivez un agent, ou que définissez sa priorité, vous définissez la configuration de cet agent sur tous les serveurs de l’organisation. sauf en cas d’ajout de scripts à l’`Scripting agent`. Vous devez mettre à jour les scripts sur chaque serveur individuellement. Pour plus d’informations sur les scripts de configuration à utiliser avec l’`Scripting agent`, consultez la section « Agent de script » plus loin dans cette rubrique.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le changement de priorité des agents, ou l’activation ou la désactivation des agents, peut provoquer des effets non voulus si vous ne comprenez pas complètement le rôle de chaque agent et comment ils interagissent avec les cmdlets Exchange. Avant de changer la configuration d’un agent, veillez à bien comprendre les changements et résultats voulus et vérifiez que votre script personnalisé fonctionnera comme prévu.</td>
</tr>
</tbody>
</table>


### Agents d’extension de cmdlet Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom de l’agent</th>
<th>Priorité</th>
<th>Activé par défaut</th>
<th>Agent système</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>Oui</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>Non</p></td>
</tr>
</tbody>
</table>


## Agent de script

Vous pouvez utiliser l’agent d’extension de cmdlets `Scripting agent` dans Exchange 2013 pour insérer votre propre logique de script dans l’exécution des cmdlets Exchange. L’`Scripting agent` vous permet d’ajouter des conditions, de remplacer des valeurs et de configurer la génération des rapports.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ673034.Caution(EXCHG.150).gif" title="Attention" alt="Attention" />Attention :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous activez l’agent d’extension de cmdlets <code>Scripting agent</code>, celui-ci est appelé chaque fois qu’une cmdlet est exécutée sur un serveur exécutant Exchange 2013. Ceci inclut non seulement les cmdlets que vous exécutez directement dans l’environnement de ligne de commande Exchange Management Shell, mais également les cmdlets exécutées par les services Exchange et le Centre d’administration Exchange (EAC). Il est vivement conseillé de tester vos scripts et toutes les modifications que vous avez apportées au fichier de configuration avant de copier le fichier de configuration mis à jour dans vos serveurs Exchange 2013 et d’activer l’agent d’extension de cmdlets <code>Scripting agent</code>.</td>
</tr>
</tbody>
</table>


Chaque fois qu’une cmdlet Exchange est exécutée, elle appelle l’agent d’extension de cmdlets de l’`Scripting agent`. Lorsque cet agent est appelé, la cmdlet vérifie si des scripts sont configurés pour être appelés par la cmdlet. Si un script doit être exécuté pour une cmdlet, cette dernière tente d’appeler toutes les API définies dans le script. Les API suivantes sont disponibles et appelées dans l’ordre suivant :

1.  **ProvisionDefaultProperties**   Cette API permet de définir les valeurs des propriétés pour des objets lors de leur création. Lorsque vous sélectionnez une valeur, elle est renvoyée à la cmdlet qui définit la valeur sur la propriété. Vous pouvez renseigner des valeurs pour les propriétés si l’utilisateur n’en a pas spécifié ou bien remplacer la valeur saisie par l’utilisateur. Cette API respecte les valeurs définies par des agents de priorité supérieure. L’agent d’extension de cmdlets de l’`Scripting agent` ne remplace pas les valeurs définies par des agents de priorité supérieure.

2.  **UpdateAffectedIConfigurable**   Cette API permet de définir des valeurs de propriétés pour des objets une fois que toutes les autres tâches de traitement sont terminées, même si l’API `Validate` n’a pas encore été appelée. Cette API respecte les valeurs définies par des agents de priorité supérieure. L’agent d’extension de cmdlets de l’`Scripting agent` ne remplace pas les valeurs définies par des agents de priorité supérieure.

3.  **Validate**   Cette API permet de valider les valeurs des propriétés d’un objet qui sont sur le point d’être définies par la cmdlet. Cette API est appelée juste avant l’écriture de données par une cmdlet. Vous pouvez configurer les contrôles de validation qui permettent la réussite ou l’échec d’une cmdlet. Si une cmdlet réussit les contrôles de validation dans cette API, elle est autorisée à écrire les données. Si la cmdlet échoue aux contrôles de validation, elle renvoie toutes les erreurs définies dans cette API.

4.  **OnComplete**   Cette API est utilisée une fois toutes les tâches de traitement de la cmdlet terminées. Elle peut être utilisée pour exécuter des tâches de post-traitement, comme par exemple, écrire des données dans une base de données externe.

> [!NOTE]
> L’agent d’extension de cmdlets de l’<code>Scripting agent</code> n’est pas appelé lorsque des cmdlets contenant le verbe <code>Get</code> sont exécutées.


## Fichier de configuration de l’agent de script

Le fichier de configuration de l’`Scripting agent` contient tous les scripts que vous voulez que l’`Scripting agent` exécute. Les scripts du fichier de configuration sont contenus dans des balises XML qui définissent le début et la fin du script et divers paramètres d’entrée nécessaires pour transmettre les données au script. Les scripts sont écrits à l’aide de la syntaxe Windows PowerShell. Le fichier de configuration est un fichier XML qui utilise les éléments ou les attributs présentés dans le tableau suivant.

### Attributs du fichier de configuration de l’agent de script

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Éléments</th>
<th>Attribut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>Non applicable</p></td>
<td><p>Cet élément contient tous les scripts que l’agent d’extension de cmdlets <code>Scripting agent</code> peut exécuter. La balise <code>Feature</code> est un enfant de cette balise.</p>
<p>Le fichier de configuration ne contient qu’une seule balise <code>Configuration</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>Non applicable</p></td>
<td><p>Cet élément contient un ensemble de scripts associés à une fonctionnalité. Chaque script défini dans la balise enfant <code>ApiCall</code> s’étend à une partie spécifique du pipeline d’exécution des cmdlets. Cette balise contient les attributs <code>Name</code> et <code>Cmdlets</code>.</p>
<p>La balise <code>Feature</code> peut englober plusieurs balises <code>Configuration</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Cet attribut contient le nom de la fonctionnalité. Utilisez cet attribut pour identifier la fonctionnalité qui est étendue par les scripts contenus dans la balise.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>Cet attribut contient la liste des cmdlets Exchange utilisées par l’ensemble des scripts de cette extension de fonctionnalité. Vous pouvez spécifier plusieurs cmdlets en séparant chacune d’elles par une virgule.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>Non applicable</p></td>
<td><p>Cet élément contient des scripts qui peuvent étendre une partie du pipeline d’exécution des cmdlets. Chaque script est défini par le nom de l’appel API dans le pipeline d’exécution des cmdlets qu’il étend. Les noms d’API suivants peuvent être étendus :</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Cet attribut inclut le nom de l’appel API qui étend le pipeline d’exécution des cmdlets.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>Non applicable</p></td>
<td><p>Cet élément contient des fonctions qui peuvent être utilisées par tout script dans le fichier de configuration.</p></td>
</tr>
</tbody>
</table>


Chaque serveur Exchange 2013 inclut le fichier ScriptingAgentConfig.xml.sample dans le dossier \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents. Le nom de ce fichier doit être modifié à ScriptingAgentConfig.xml sur chaque serveur Exchange 2013 si vous activez l’agent d’extension de cmdlets Agent de script. L’exemple de fichier de configuration contient des modèles de script que vous pouvez utiliser pour mieux comprendre la procédure d’ajout de scripts au fichier de configuration.

Après avoir ajouté un script au fichier de configuration, ou si vous apportez une modification au fichier de configuration, vous devez mettre le fichier à jour sur chaque serveur Exchange 2013 de votre organisation. Cette opération est essentielle pour vous assurer que chaque serveur contient une version actualisée des scripts exécutés par l’agent d’extension de cmdlets de l’`Scripting Agent`.

Certains caractères utilisés généralement dans les scripts ont également une signification particulière dans XML. Pour utiliser ces caractères dans votre script, utilisez des séquences d’échappement. Par exemple, les caractères suivants utilisent une séquence d’échappement :

  - Plutôt qu’un signe Supérieur à (`>`), utilisez `&gt;`

  - Plutôt qu’un signe Inférieur à (`<`), utilisez `$lt;`

  - Plutôt qu’une esperluette (`&`), utilisez `&amp;`

## Activer l’agent de script

L’agent d’extension de cmdlets de l’`Scripting agent` est désactivé par défaut. Lorsque vous activez l’`Scripting agent`, celui-ci est activé pour toute l’organisation Exchange 2013. Avant d’activer l’`Scripting agent`, vérifiez que le fichier de configuration de l’`Scripting agent` a été correctement renommé et mis à jour avec vos scripts sur chaque serveur Exchange 2013. Vous recevrez un message d’erreur chaque fois qu’une cmdlet est exécutée si vous n’avez pas renommé le fichier de configuration correctement ou copié un fichier de configuration sur cet ordinateur à partir d’un autre serveur Exchange 2013.

Pour activer l’`Scripting agent`, procédez comme suit :

1.  Renommez le fichierScriptingAgentConfig.xml.sample dans **\<chemin d’installation\>\\V15\\Bin\\CmdletExtensionAgents** en ScriptingAgentConfig.xml sur chacun des serveurs Exchange 2013 de votre organisation.
    
    > [!NOTE]
    > Vous pouvez copier le fichier de configuration d’un serveur Exchange 2013 dans d’autres serveurs Exchange 2013. Assurez-vous de mettre à jour le fichier de configuration désiré avant de le copier.


2.  Ajoutez votre script au fichier de configuration renommé sur chaque serveur Exchange 2013 de votre organisation.

3.  Activez l’agent d’extension de cmdlet de l’`Scripting agent`. Pour plus d’informations sur l’activation des agents d’extension de cmdlets, consultez la rubrique [Gérer des agents d’extension de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Priorité de l’agent de script

Par défaut, l’agent d’extension de cmdlets de l’`Scripting agent` est exécuté après tous les autres agents, à l’exception de l’agent de l’`Scripting agent`. Si vous souhaitez qu’un script que vous créez remplace un agent existant, vous devez désactiver l’autre agent ou modifier la priorité de l’un des agents pour que l’agent d’extension de cmdlets de l’`Scripting agent` soit exécuté en premier. Pour plus d’informations sur la manière de désactiver ou de modifier la priorité des agents, consultez [Gérer des agents d’extension de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

