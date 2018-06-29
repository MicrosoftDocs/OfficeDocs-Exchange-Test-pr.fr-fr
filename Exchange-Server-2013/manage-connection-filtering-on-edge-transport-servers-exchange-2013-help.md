---
title: 'Gérer le filtrage des connexions sur les serveurs de transport Edge: Exchange 2013 Help'
TOCTitle: Gérer le filtrage des connexions sur les serveurs de transport Edge
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60829282
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gérer le filtrage des connexions sur les serveurs de transport Edge

 

_**Sapplique à :**Exchange Server 2013_

_**Dernière rubrique modifiée :**2015-04-08_

Le filtrage des connexions est une fonctionnalité de blocage du courrier indésirable fournie par l’agent de filtrage de connexion, disponible uniquement sur les serveurs de transport Edge dans Microsoft Exchange 2013. Le filtrage des connexions active les fonctionnalités suivantes :

  - Liste d'adresses IP bloquées

  - Fournisseurs de listes d'adresses IP bloquées

  - Liste d'adresses IP autorisées

  - Fournisseurs de listes d'adresses IP autorisées

Chacune de ces fonctionnalités peut être activée ou désactivée séparément.

## Ce qu’il faut savoir avant de commencer

  - Durée d’exécution estimée : 15 minutes.

  - Des autorisations doivent vous être attribuées avant de pouvoir exécuter cette procédure. Pour voir les autorisations qui vous sont nécessaires, consultez l’entrée « Fonctionnalités anti-spam » dans la rubrique [Autorisations anti-spam et anti-programme malveillant](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Vous pouvez uniquement utiliser l'environnement de ligne de commande Exchange Management Shell pour effectuer cette tâche.

  - Pour des informations sur les raccourcis clavier applicables aux procédures de cette rubrique, voir Raccourcis clavier dans Exchange 2013[Raccourcis clavier dans le Centre d’administration Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.tip(EXCHG.150).gif" title="Conseil" alt="Conseil" />Conseil :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vous rencontrez des difficultés ? Demandez de l’aide en participant aux forums Exchange. Visitez les forums sur les pages <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, et <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Que souhaitez-vous faire ?

## Utiliser l'environnement de ligne de commande Exchange Management Shell pour activer ou désactiver le filtrage des connexions

Pour activer ou désactiver complètement le filtrage des connexions, vous devez activer ou désactiver l’agent de filtrage des connexions. La modification prend effet après le redémarrage du service de transport Microsoft Exchange. Lorsque vous redémarrez le service de transport Microsoft Exchange sur un serveur de transport Edge, le flux de messagerie sur le serveur est temporairement interrompu.

Pour désactiver le filtrage des connexions, exécutez la commande suivante :

    Disable-TransportAgent "Connection Filtering Agent"

Pour activer le filtrage des connexions, exécutez la commande suivante :

    Enable-TransportAgent "Connection Filtering Agent"

Pour que la modification soit prise en compte, redémarrez le service de transport Microsoft Exchange en exécutant la commande suivante :

    Restart-Service MSExchangeTransport

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé le filtrage des connexions, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled

## Procédures de configuration des listes d’adresses IP bloquées

Ces procédures s’appliquent à la liste d’adresses IP bloquées que vous configurez manuellement. Elles ne s’appliquent pas aux fournisseurs de listes d’adresses IP bloquées.

Utilisez la cmdlet **IPBlockListConfig** pour voir et modifier la façon dont le filtrage des connexions utilise la liste d’adresses IP bloquées. Utilisez la cmdlet **IPBlocklistesntry** pour voir et définir les adresses IP de la liste d’adresses IP bloquées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la configuration de la liste d’adresses IP bloquées

Pour afficher la configuration de la liste d’adresses IP bloquées, exécutez la commande suivante :

    Get-IPBlockListConfig | Format-List *Enabled,*Response

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la liste d’adresses IP bloquées

Pour désactiver la liste d’adresses IP bloquées, exécutez la commande suivante :

    Set-IPBlockListConfig -Enabled $false

Pour activer la liste d’adresses IP bloquées, exécutez la commande suivante :

    Set-IPBlockListConfig -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé la liste d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPBlockListConfig | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la liste d’adresses IP bloquées

Pour configurer la liste d’adresses IP bloquées, utilisez la syntaxe suivante :

    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]

Cet exemple de code permet de configurer la liste d’adresses IP bloquées avec les paramètres suivants :

  - La liste d’adresses IP bloquées filtre les connexions entrantes issues de serveurs de messagerie internes et externes. Par défaut, seules les connexions issues de serveurs de messagerie externes sont filtrées (*ExternalMailEnabled* est défini sur `$true` et *InternalMailEnabled* sur `$false`). Les connexions authentifiées et non authentifiées issues de partenaires externes sont considérées comme des connexions externes.

  - Le texte de réponse personnalisé pour les connexions filtrées sur la base des adresses IP qui ont été automatiquement ajoutées à la liste d’adresses IP bloquées par la fonctionnalité Réputation de l’expéditeur de l’agent d’analyse de protocole est défini sur la valeur : « La connexion de l’adresse IP {0} a été rejetée par la réputation de l’expéditeur. »

  - Le texte de réponse personnalisé pour les connexions filtrées sur la base des adresses IP qui ont été ajoutées manuellement à la liste d’adresses IP bloquées est défini sur la valeur : « La connexion de l’adresse IP {0} a été rejetée par le filtrage des connexions. »

<!-- end list -->

    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré la liste d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPBlockListConfig | Format-List *MailEnabled,*Response

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les entrées de liste d’adresses IP bloquées

Pour afficher toutes les entrées de liste d’adresses IP bloquées, exécutez la commande suivante :

    Get-IPBlockListEntry

Notez que chaque entrée de liste d’adresses IP bloquées est identifiée par un nombre entier. Ce numéro d’identification est attribuée dans l’ordre croissant à mesure que vous ajoutez des entrées à la liste d’adresses IP bloquées et à la liste d’adresses IP autorisées.

Pour afficher une entrée de liste d’adresses IP bloquées spécifique, utilisez la syntaxe suivante :

    Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

Par exemple, pour afficher l’entrée de liste d’adresses IP bloquées qui contient l’adresse IP 192.168.1.13, exécutez la commande suivante :

    Get-IPBlockListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous utilisez le paramètre <em>IPAddress</em>, l’entrée de liste d’adresses IP bloquées obtenue peut être une adresse IP individuelle, une plage d’adresses IP ou une adresse IP de routage CIDR (Classless InterDomain Routing). Pour utiliser le paramètre <em>Identity</em>, vous devez indiquer le nombre entier attribué à l’entrée de la liste d’adresses IP bloquées.</td>
</tr>
</tbody>
</table>


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter des entrées de liste d’adresses IP bloquées

Pour ajouter des entrées de liste d’adresses IP bloquées, exécutez la commande suivante :

    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]

L’exemple de code suivant permet d’ajouter l’entrée de liste d’adresses IP bloquées correspondant à la plage d’adresses IP 192.168.1.10 à 192.168.1.15 et de définir la date d’expiration de l’entrée sur le 4 juillet 2014 à 15h00.

    Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté l’entrée de liste d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que la nouvelle entrée est bien affichée.

    Get-IPBlockListEntry

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer des entrées de liste d’adresses IP bloquées

Pour supprimer des entrées de liste d’adresses IP bloquées, utilisez la syntaxe suivante :

    Remove-IPBlockListEntry <IdentityInteger>

L’exemple de code suivant permet de supprimer l’entrée de liste d’adresses IP bloquées portant la valeur d’*Identity* 3.

    Remove-IPBlockListEntry 3

L’exemple de code suivant permet de supprimer l’entrée de liste d’adresses IP bloquées qui contient l’adresse IP 192.168.1.12 sans utiliser la valeur d’*Identity*. Notez que l’entrée de liste d’adresses IP bloquées peut être une adresse IP individuelle ou une plage d’adresses IP.

    Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé l’entrée de liste d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que l’entrée que vous avez supprimée n’apparaît plus.

    Get-IPBlockListEntry

## Procédures de configuration des fournisseurs de listes d’adresses IP bloquées

Ces procédures s’appliquent aux fournisseurs de listes d’adresses IP bloquées. Elles ne s’appliquent pas à la liste d’adresses IP bloquées.

Utilisez la cmdlet **IPBlockListProvidersConfig** pour voir et modifier la façon dont le filtrage des connexions utilise l’ensemble des fournisseurs de listes d’adresses IP bloquées. Utilisez la cmdlet **IPBlockListProvider** pour voir, configurer et tester les fournisseurs de listes d’adresses IP bloquées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la configuration de tous les fournisseurs de listes d’adresses IP bloquées

Pour afficher la façon dont le filtrage des connexions utilise l’ensemble des fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante :

    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver tous les fournisseurs de listes d’adresses IP bloquées

Pour désactiver tous les fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante :

    Set-IPBlockListProvidersConfig -Enabled $false

Pour activer tous les fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante :

    Set-IPBlockListProvidersConfig -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé tous les fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPBlockListProvidersConfig | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer tous les fournisseurs de listes d’adresses IP bloquées

Pour configurer la façon dont le filtrage des connexions utilise l’ensemble des fournisseurs de listes d’adresses IP bloquées, utilisez la syntaxe suivante :

    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

L’exemple de code suivant permet de configurer tous les fournisseurs de listes d’adresses IP bloquées avec les paramètres suivants :

  - Les fournisseurs de listes d’adresses IP bloquées filtrent les connexions entrantes issues de serveurs de messagerie internes et externes. Par défaut, seules les connexions issues de serveurs de messagerie externes sont filtrées (*ExternalMailEnabled* est défini sur `$true` et *InternalMailEnabled* sur `$false`). Les connexions authentifiées et non authentifiées issues de partenaires externes sont considérées comme des connexions externes.

  - Les messages envoyés aux destinataires internes chris@fabrikam.com et michelle@fabrikam.com sont exclus du filtrage par les fournisseurs de listes d’adresses IP bloquées. Si vous souhaitez ajouter des destinataires à la liste sans modifier les destinataires existants, utilisez la syntaxe : `@{Add="<recipient1>","<recipient2>"...}`.

<!-- end list -->

    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true

Pour plus d’informations, voir [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/fr-fr/library/aa998543\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré tous les fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les fournisseurs de listes d’adresses IP bloquées

Pour afficher une liste récapitulative de tous les fournisseurs de listes d’adresses IP bloquées, exécutez la commande suivante :

    Get-IPBlockListProvider

Pour afficher les détails d’un fournisseur spécifique, utilisez la syntaxe suivante :

    Get-IPBlockListProvider <IPBlockListProviderIdentity>

L’exemple de code suivant permet d’afficher des informations relatives au fournisseur nommé « Contoso IP Block List Provider ».

    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un fournisseur de listes d’adresses IP bloquées

Pour ajouter un fournisseur de listes d’adresses IP bloquées, utilisez la syntaxe suivante :

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

Cet exemple de code permet de créer un fournisseur de listes d’adresses IP bloquées nommé « Contoso IP Block List Provider » avec les options suivantes :

  - **Nom de domaine complet à utiliser pour le fournisseur**   rbl.contoso.com

  - **Code de masque de bits à utiliser par le fournisseur**   127.0.0.1

<!-- end list -->

    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous ajoutez un nouveau fournisseur de listes d’adresses IP bloquées, il est activé par défaut (la valeur <em>Enabled</em> est <code>$true</code>) et sa valeur de priorité est incrémentée (la valeur <em>Priority</em> de la première entrée est de 1).</td>
</tr>
</tbody>
</table>


Pour plus d’informations, voir [Add-IPBlockListProvider](https://technet.microsoft.com/fr-fr/library/bb124358\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté un fournisseur de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que le nouveau fournisseur de listes d’adresses IP bloquées apparaît.

    Get-IPBlockListProvider

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver un fournisseur de listes d’adresses IP bloquées

Pour activer ou désactiver un fournisseur de listes d’adresses IP bloquées spécifique, utilisez la syntaxe suivante :

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>

L’exemple de code suivant permet de désactiver le fournisseur de listes d’adresses IP bloquées nommé Contoso IP Block List Provider.

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false

L’exemple de code suivant permet de activer le fournisseur de listes d’adresses IP bloquées nommé Contoso IP Block List Provider.

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé un fournisseur de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer un fournisseur de listes d’adresses IP bloquées

Les options de configuration disponibles dans la cmdlet **Set-IPBlockListProvider** sont identiques à celles de la cmdlet **New-IPBlockListProvider**.

Pour configurer un fournisseur de listes d’adresses IP bloquées existant, utilisez la syntaxe suivante :

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

Par exemple, pour ajouter le code d’état d’adresse IP 127.0.0.1 à la liste des codes d’état existants pour le fournisseur nommé Contoso IP Block List Provider, exécutez la commande suivante :

    Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

Pour plus d’informations, voir [Set-IPBlockListProvider](https://technet.microsoft.com/fr-fr/library/bb124979\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré un fournisseur de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour tester un fournisseur de listes d’adresses IP bloquées

Pour tester un fournisseur de listes d’adresses IP bloquées, utilisez la syntaxe suivante.

    Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>

L’exemple de code suivant permet de tester le fournisseur de listes d’adresses IP bloquées nommé Contoso IP Block List Provider en vérifiant l’adresse IP 192.168.1.1.

    Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un fournisseur de listes d’adresses IP bloquées

Pour supprimer un fournisseur de listes d’adresses IP bloquées, utilisez la syntaxe suivante :

    Remove-IPBlockListProvider <IPBlockListProviderIdentity>

L’exemple de code suivant permet de supprimer le fournisseur de listes d’adresses IP bloquées nommé Contoso IP Block List Provider.

    Remove-IPBlockListProvider "Contoso IP Block list Provider"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé un fournisseur de listes d’adresses IP bloquées, exécutez la commande suivante et assurez-vous que le fournisseur de listes d’adresses IP bloquées que vous avez supprimé n’apparaît plus.

    Get-IPBlockListProvider

## Procédure de configuration des listes d’adresses IP autorisées

Ces procédures s’appliquent à la liste d’adresses IP autorisées que vous configurez manuellement. Elles ne s’appliquent pas aux fournisseurs de listes d’adresses IP autorisées.

Utilisez la cmdlet **IPAllowListConfig** pour voir et modifier la façon dont le filtrage des connexions utilise la liste d’adresses IP autorisées. Utilisez la cmdlet **IPAllowlistesntry** pour voir et définir les adresses IP dans la liste d’adresses IP autorisées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la configuration de la liste d’adresses IP autorisées

Pour afficher la configuration de la liste d’adresses IP autorisées, exécutez la commande suivante :

    Get-IPAllowListConfig | Format-List *Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver la liste d’adresses IP autorisées

Pour désactiver la liste d’adresses IP autorisées, exécutez la commande suivante :

    Set-IPAllowListConfig -Enabled $false

Pour activer la liste d’adresses IP autorisées, exécutez la commande suivante :

    Set-IPAllowListConfig -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé la liste d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPAllowListConfig | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer la liste d’adresses IP autorisées

Pour configurer la liste d’adresses IP autorisées, utilisez la syntaxe suivante :

    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>

Cet exemple de code permet de configurer la liste d’adresses IP autorisées pour filtrer les connexions entrantes issues de serveurs de messagerie internes et externes. Par défaut, seules les connexions issues de serveurs de messagerie externes sont filtrées (*ExternalMailEnabled* est défini sur `$true` et *InternalMailEnabled* sur `$false`). Les connexions authentifiées et non authentifiées issues de partenaires externes sont considérées comme des connexions externes.

    Set-IPAllowListConfig -InternalMailEnabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré la liste d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPAllowListConfig | Format-List *MailEnabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les entrées de liste d’adresses IP autorisées

Pour afficher toutes les entrées de liste d’adresses IP autorisées, exécutez la commande suivante :

    Get-IPAllowListEntry

Notez que chaque entrée de liste d’adresses IP autorisées est identifiée par un nombre entier. Ce numéro d’identification est attribuée dans l’ordre croissant à mesure que vous ajoutez des entrées à la liste d’adresses IP bloquées et à la liste d’adresses IP autorisées.

Pour afficher une entrée de liste d’adresses IP autorisées spécifique, utilisez la syntaxe suivante :

    Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

Par exemple, pour afficher l’entrée de liste d’adresses IP autorisées qui contient l’adresse IP 192.168.1.13, exécutez la commande suivante :

    Get-IPAllowListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous utilisez le paramètre <em>IPAddress</em>, l’entrée de liste d’adresses IP autorisées obtenue peut être une adresse IP individuelle, une plage d’adresses IP ou une adresse IP de routage CIDR (Classless InterDomain Routing). Pour utiliser le paramètre <em>Identity</em>, vous devez indiquer de nombre entier attribué à l’entrée de la liste d’adresses IP autorisées.</td>
</tr>
</tbody>
</table>


## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter des entrées de liste d’adresses IP autorisées

Pour ajouter des entrées de liste d’adresses IP autorisées, exécutez la commande suivante :

    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]

Cet exemple de code permet d’ajouter l’entrée de liste d’adresses IP autorisées correspondant à la plage d’adresses IP 192.168.1.10 à 192.168.1.15 et de définir la date d’expiration de l’entrée sur le 4 juillet 2014 à 15h00.

    Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté l’entrée de liste d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que la nouvelle entrée est bien affichée.

    Get-IPAllowListEntry

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer des entrées de liste d’adresses IP autorisées

Pour supprimer des entrées de liste d’adresses IP autorisées, exécutez la commande suivante :

    Remove-IPAllowListEntry <IdentityInteger>

L’exemple de code suivant permet de supprimer l’entrée de liste d’adresses IP autorisées portant la valeur d’*Identity* 3.

    Remove-IPAllowListEntry 3

Cet exemple de code permet de supprimer l’entrée de liste d’adresses IP autorisées qui contient l’adresse IP 192.168.1.12 sans utiliser la valeur d’*Identity*. Notez que l’entrée de liste d’adresses IP autorisées peut être une adresse IP individuelle ou une plage d’adresses IP.

    Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé l’entrée de liste d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que l’entrée que vous avez supprimée n’apparaît plus.

    Get-IPAllowListEntry

## Procédures de configuration des fournisseurs de listes d’adresses IP autorisées

Ces procédures s’appliquent aux fournisseurs de listes d’adresses IP autorisées. Elles ne s’appliquent pas à la liste d’adresses IP autorisées.

Utilisez la cmdlet **IPAllowListProvidersConfig** pour voir et modifier la façon dont le filtrage des connexions utilise l’ensemble des fournisseurs de listes d’adresses IP autorisées. Utilisez la cmdlet **IPAllowListProvider** pour voir, configurer et tester les fournisseurs de listes d’adresses IP autorisées.

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher la configuration de tous les fournisseurs de listes d’adresses IP autorisées

Pour voir la façon dont le filtrage des connexions utilise tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante :

    Get-IPAllowListProvidersConfig | Format-List *Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver tous les fournisseurs de listes d’adresses IP autorisées

Pour désactiver tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante :

    Set-IPAllowListProvidersConfig -Enabled $false

Pour activer tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante :

    Set-IPAllowListProvidersConfig -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPAllowListProvidersConfig | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer tous les fournisseurs de listes d’adresses IP autorisées

Pour configurer la façon dont le filtrage des connexions utilise tous les fournisseurs de listes d’adresses IP autorisées, utilisez la syntaxe suivante :

    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

Cet exemple de code permet de configurer tous les fournisseurs de listes d’adresses IP autorisées pour filtrer les connexions entrantes issues de serveurs de messagerie internes et externes. Par défaut, seules les connexions issues de serveurs de messagerie externes sont filtrées (*ExternalMailEnabled* est défini sur `$true` et *InternalMailEnabled* sur `$false`). Les connexions authentifiées et non authentifiées issues de partenaires externes sont considérées comme des connexions externes.

    Set-IPAllowListProvidersConfig -InternalMailEnabled $true

Pour plus d’informations, voir [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/fr-fr/library/aa998543\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPAllowListProvidersConfig | Format-List *MailEnabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour afficher les fournisseurs de listes d’adresses IP autorisées

Pour afficher une liste récapitulative de tous les fournisseurs de listes d’adresses IP autorisées, exécutez la commande suivante :

    Get-IPAllowListProvider

Pour afficher les détails d’un fournisseur spécifique, utilisez la syntaxe suivante :

    Get-IPAllowListProvider <IPAllowListProviderIdentity>

Cet exemple de code permet d’afficher des informations relatives au fournisseur nommé « Contoso IP Allow List Provider ».

    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour ajouter un fournisseur de listes d’adresses IP autorisées

Pour ajouter un fournisseur de listes d’adresses IP autorisées, utilisez la syntaxe suivante :

    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

Cet exemple de code permet de créer un fournisseur de listes d’adresses IP autorisées nommé « Contoso IP Allow List Provider » avec les options suivantes :

  - **Nom de domaine complet à utiliser pour le fournisseur**   allow.contoso.com

  - **Code de masque de bits à utiliser par le fournisseur**   127.0.0.1

<!-- end list -->

    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/JJ159664.note(EXCHG.150).gif" title="Remarque" alt="Remarque" />Remarque :</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lorsque vous ajoutez un nouveau fournisseur de listes d’adresses IP autorisées, il est activé par défaut (la valeur <em>Enabled</em> est <code>$true</code>) et la valeur de priorité est incrémentée (la valeur de <em>Priority</em> de la première entrée est de 1).</td>
</tr>
</tbody>
</table>


Pour plus d’informations, voir [Add-IPBlockListProvider](https://technet.microsoft.com/fr-fr/library/bb124358\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien ajouté le fournisseur de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que le nouveau fournisseur de listes d’adresses IP autorisées s’affiche.

    Get-IPAllowListProvider

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour activer ou désactiver un fournisseur de listes d’adresses IP autorisées

Pour activer ou désactiver un fournisseur de listes d’adresses IP autorisées spécifique, utilisez la syntaxe suivante :

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>

L’exemple de code suivant permet de désactiver le fournisseur de listes d’adresses IP autorisées nommé Contoso IP Allow List Provider.

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false

L’exemple de code suivant permet d’activer le fournisseur de listes d’adresses IP autorisées nommé Contoso IP Allow List Provider.

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien activé ou désactivé un fournisseur de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que la valeur affichée est celle que vous avez configurée.

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour configurer un fournisseur de listes d’adresses IP autorisées

Les options de configuration disponibles dans la cmdlet **Set-IPAllowListProvider** sont identiques à celles de la cmdlet **New-IPAllowListProvider**.

Pour configurer un fournisseur de listes d’adresses IP autorisées, utilisez la syntaxe suivante :

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

Par exemple, pour ajouter le code d’état de l’adresse IP 127.0.0.1 à la liste des codes d’état existants pour le fournisseur de listes d’adresses IP autorisées nommé Contoso IP Allow List Provider, exécutez la commande suivante :

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

Pour plus d’informations, voir [Set-IPBlockListProvider](https://technet.microsoft.com/fr-fr/library/bb124979\(v=exchg.150\)).

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien configuré un fournisseur de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que les valeurs affichées sont celles que vous avez configurées.

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour tester un fournisseur de listes d’adresses IP autorisées

Pour tester un fournisseur de listes d’adresses IP autorisées, utilisez la syntaxe suivante :

    Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>

L’exemple de code suivant permet de tester le fournisseur de listes d’adresses IP autorisées nommé Contoso IP Allow List Provider en vérifiant l’adresse IP 192.168.1.1.

    Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1

## Utiliser l’environnement de ligne de commande Exchange Management Shell pour supprimer un fournisseur de listes d’adresses IP autorisées

Pour supprimer un fournisseur de listes d’adresses IP autorisées, utilisez la syntaxe suivante :

    Remove-IPAllowListProvider <IPAllowListProviderIdentity>

L’exemple de code suivant permet de supprimer le fournisseur de listes d’adresses IP autorisées nommé Contoso IP Allow List Provider.

    Remove-IPAllowListProvider "Contoso IP Allow List Provider"

## Comment savoir si cela a fonctionné ?

Pour vérifier que vous avez bien supprimé le fournisseur de listes d’adresses IP autorisées, exécutez la commande suivante et assurez-vous que le fournisseur de listes d’adresses IP autorisées que vous avez supprimé n’apparaît plus.

    Get-IPAllowListProvider

