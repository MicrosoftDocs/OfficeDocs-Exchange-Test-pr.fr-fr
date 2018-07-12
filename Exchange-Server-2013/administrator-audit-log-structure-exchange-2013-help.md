---
title: 'Structure du journal d’audit de l’administrateur: Exchange 2013 Help'
TOCTitle: Structure du journal d’audit de l’administrateur
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50555437
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Structure du journal d’audit de l’administrateur

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-03-09_

Les journaux d’audit de l’administrateur contiennent un enregistrement de tous les cmdlets et paramètres exécutés dans l’environnement de la ligne de commande Exchange Management Shell et par le Centre d’administration Exchange (EAC). Ils sont créés à la demande lorsque vous exécutez le rapport du journal d’audit de l’administrateur dans le Centre d’administration Exchange (CAE), ou lorsque vous exécutez la cmdlet **New-AdminAuditLogSearch** dans l’environnement de ligne de commande Exchange Management Shell. Pour plus d’informations sur les journaux d’audit, voir [Connexion au service d’audit administrateur](administrator-audit-logging-exchange-2013-help.md).

Les journaux d’audit sont des fichiers XML et peuvent contenir plusieurs entrées de journal d’audit. Le tableau suivant décrit chaque balise XML et ses attributs associés.

Souhaitez-vous rechercher des tâches de gestion relatives aux journaux d’audit de l’administrateur ? Voir [Gestion de la journalisation d’audit de l’administrateur](manage-administrator-audit-logging-exchange-2013-help.md).

### Balises XML et attributs des journaux d’audit

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Élément</th>
<th>Attribut</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Il s’agit de la balise de déclaration de document XML. Elle est incluse dans chaque fichier XML de journal d’audit et contient le numéro de version XML et la valeur de codage de caractère.</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Cette balise contient toutes les entrées du journal d’audit dans le fichier XML. La balise <code>Event</code> est un enfant de cette balise.</p>
<p>Il y a qu’un seule balise <code>SearchResults</code> par fichier XML.</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p></p></td>
<td><p>Cette balise contient l’entrée du journal d’audit pour une cmdlet individuelle. Cette balise contient les attributs <code>Caller</code>, <code>Cmdlet</code>, <code>ObjectModified</code>, <code>RunDate</code>, <code>Succeeded</code>, <code>Error</code> et <code>OriginatingServer</code>. Les balises <code>CmdletParameters</code> et <code>ModifiedProperties</code> sont des enfants de cette balise.</p>
<p>Il existe une balise <code>Event</code> par entrée de journal d’audit.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Caller</code></p></td>
<td><p>Cet attribut contient le compte de l’utilisateur qui a exécuté la cmdlet dans l’attribut <code>Cmdlet</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>Cet attribut contient le nom de la cmdlet exécutée par l’utilisateur dans l’attribut <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>Cet attribut contient l’objet modifié par la cmdlet spécifiée dans l’attribut <code>Cmdlet</code>. La balise <code>ModifiedProperties</code> affiche les propriétés qui ont été modifiées sur cet objet.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>Cet attribut contient la date et l’heure de l’exécution de la cmdlet dans l’attribut <code>Cmdlet</code>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>Cet attribut spécifie si la cmdlet a été correctement exécutée dans l’attribut <code>Cmdlet</code>. La valeur est <code>True</code> ou <code>False</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Error</code></p></td>
<td><p>Cet attribut contient le message d’erreur qui est généré en cas d’échec de l’exécution de la cmdlet dans l’attribut <code>Cmdlet</code>. Si aucune erreur ne s’est produite, la valeur est définie sur <code>None</code>.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>Cet attribut contient le serveur dans lequel la cmdlet spécifiée dans l’attribut <code>Cmdlet</code> a été exécutée.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Cette balise contient tous les paramètres spécifiés au moment de l’exécution de la cmdlet. La balise <code>Parameter</code> est un enfant de cette balise.</p>
<p>Il existe une seule balise <code>CmdletParameters</code> par balise <code>Event</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p></p></td>
<td><p>Cette balise contient un paramètre individuel spécifié au moment de l’exécution de la cmdlet. Cette balise contient les attributs <code>Name</code> et <code>Value</code>.</p>
<p>Il peut exister plusieurs balises <code>Parameter</code> par balise <code>CmdletParameters</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Cet attribut contient le nom du paramètre spécifié au moment de l’exécution de la cmdlet.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Value</code></p></td>
<td><p>Cet attribut contient la valeur fournie pour le paramètre spécifié dans l’attribut <code>Name</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Cette balise contient toutes les propriétés modifiées par la cmdlet exécutée. La balise <code>Property</code> est un enfant de cette balise.</p>
<p>Il existe une balise <code>ModifiedProperties</code> par balise <code>Event</code>.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ159813.important(EXCHG.150).gif" title="Important" alt="Important" />Important :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cette balise n’est renseignée que si le paramètre <em>LogLevel</em> de la cmdlet <strong>Set-AdminAuditLogConfig</strong> est défini à <code>Verbose</code>.</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p></p></td>
<td><p>Cette balise contient une propriété individuelle spécifiée au moment de l’exécution de la cmdlet. Cette balise contient les attributs <code>Name</code>, <code>OldValue</code> et <code>NewValue</code>.</p>
<p>Il peut exister plusieurs balises <code>Property</code> par balise <code>ModifiedProperties</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Cet attribut contient le nom de la propriété modifiée au moment de l’exécution de la cmdlet.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>Cet attribut contient la valeur contenue dans la propriété spécifiée dans l’attribut <code>Name</code> avant sa modification.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>Cet attribut contient la valeur utilisée pour modifier la propriété dans l’attribut <code>Name</code>.</p></td>
</tr>
</tbody>
</table>


## Exemple d’entrée de journal d’audit

Vous trouverez ci-dessous un exemple type d’entrée de journal d’audit. Selon les informations contenues dans l’entrée de journal, nous savons que les événements suivants se sont produits :

  - Le 18/10/2012 à 15h48 heure avancée du Pacifique (UTC-7), l’utilisateur `Administrator` a exécuté la cmdlet **Set-Mailbox**.

  - Les deux paramètres suivants ont été fournis lors de l’exécution de la cmdlet **Set-Mailbox** :
    
      - *Identity* avec une valeur de `david`
    
      - *ProhibitSendReceiveQuota* avec une valeur de `10GB`

  - Les deux propriétés suivantes sur l’objet `david`ont été modifiées :
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Les propriétés modifiées sont enregistrées dans le journal d’audit parce que le paramètre <em>LogLevel</em> de la cmdlet <code>Set-AdminAuditLogConfig</code> a été défini à <code>Verbose</code> dans cet exemple.</td>
    </tr>
    </tbody>
    </table>
    
      - *ProhibitSendReceiveQuota* avec une nouvelle valeur « `10GB` », remplaçant la valeur précédente qui était « `35GB` ».

  - L’opération s’est terminée sans erreurs.

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>

